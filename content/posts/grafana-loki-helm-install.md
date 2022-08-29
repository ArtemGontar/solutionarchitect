---
title: "How to configure Grafana Loki with Helm into Kubernetes"
date: 2022-01-24T11:13:07+02:00
keywords:
- grafana
- loki
- observability
- helm
- kubernetes
- configure
- promtail
draft: false
---

## About to start configuring

Here you can find a repository with grafana charts: [https://github.com/grafana/helm-charts](https://github.com/grafana/helm-charts)

The first thing we need is to add the repository to helm:

```bash
helm repo add grafana https://grafana.github.io/helm-charts
helm repo update
```

Now we are interested in: loki-stack, grafana, promtail charts

The easiest way to install loki-stack with the default configuration:

```bash
# default
helm upgrade --install loki grafana/loki-stack

# default in your namespace
helm upgrade --install loki --namespace=<your-namespace> grafana/loki-stack
```

The commands above will put you Loki + Promtail, without Grafana, Loki itself will store the data in the file system. Which is only suitable for just playing around with the Loki installation.

To add Grafana to the installation, you need to use:

```bash
helm upgrade --install loki loki/loki-stack --set grafana.enabled=true
```

Grafana ships with built-in support for Loki for versions greater than [6.0](https://grafana.com/grafana/download/6.0.0). Using [6.3](https://grafana.com/grafana/download/6.3.0) or later is highly recommended to take advantage of the new [LogQL](https://grafana.com/docs/loki/latest/logql/) functionality.

1. Log into your Grafana instance. If this is your first time running Grafana, the username and password are both defaulted to `admin`.
2. In Grafana, go to `Configuration` > `Data Sources` via the cog icon on the left sidebar.
3. Click the big button.
    
    + Add data source
    
4. Choose Loki from the list.
5. The HTTP URL field should be the address of your Loki server. For example, when running locally or with Docker using port mapping, the address is likely `http://localhost:3100`. When running with docker-compose or Kubernetes, the address is likely `http://loki:3100`.
6. To see the logs, click on the sidebar, select the Loki data source in the top-left dropdown, and then choose a log stream using the button.
    
    Explore
    
    Log labels
    
7. Learn more about querying by reading about Loki’s query language [LogQL](https://grafana.com/docs/loki/latest/logql/).

With this configuration, there is already more interest, it will be possible to show a demo with a UI display of logs, and play with LogQL through the interface in Grafana.

## Change log-shipper

By default, Promtail is installed in the chart with a locked stack. Here is what the developers themselves write about it:

> Promtail is the client of choice when you’re running Kubernetes, as you can configure it to automatically scrape logs from pods running on the same node that Promtail runs on. Promtail and Prometheus running together in Kubernetes enables powerful debugging: if Prometheus and Promtail use the same labels, users can use tools like Grafana to switch between metrics and logs based on the label set.
Promtail is also the client of choice on bare-metal since it can be configured to tail logs from all files given a host path. It is the easiest way to send logs to Loki from plain-text files (e.g., things that log to /var/log/*.log).
> 

But also, you can use another provider from the list of supported([https://grafana.com/docs/loki/latest/clients/](https://grafana.com/docs/loki/latest/clients/))

- [Docker Driver](https://grafana.com/docs/loki/latest/clients/docker-driver/)
- [Fluentd](https://grafana.com/docs/loki/latest/clients/fluentd/)
- [Fluent Bit](https://grafana.com/docs/loki/latest/clients/fluentbit/)
- [Logstash](https://grafana.com/docs/loki/latest/clients/logstash/)

This is necessary if you already have a configured log deliverer, here is an example of how to deploy a loki-stack with fluent-bit:

```bash
helm upgrade --install loki loki/loki-stack \
--set fluent-bit.enabled=true,promtail.enabled=false
```

## Building loki-stack separately

In Promtail helm chart's configuration set your lokiAddress:

```yaml
config:
  # -- The Loki address to post logs to.
  # Must be reference in `config.file` to configure `client.url`.
  # See default config in `values.yaml`
  lokiAddress: http://loki:3100/loki/api/v1/push
```

Installing Loki + Promtail + Grafana

```bash
helm upgrade --install loki grafana/loki
helm upgrade --install loki grafana/promtail
helm upgrade --install loki grafana/grafana
```

## Configuring Promtail

Promtail is deployed as a DeamonSet, first, make sure you set all the required tolerations for this pod:

```yaml
# For example DeamonSet can be scheduled to nodes with NoSchedule, NoExecute taints
tolerations:
  - effect: NoSchedule
    operator: Exists
  - effect: NoExecute
    operator: Exists
```

Further, if you are using Prometheus to collect metrics (via the Promethues operator) and want to monitor Promtail (recommended), you need to enable ServiceMonitor:

```yaml
serviceMonitor:
  # -- If enabled, ServiceMonitor resources for Prometheus Operator are created
  enabled: tr
  # -- Alternative namespace for ServiceMonitor resources
  namespace: null
  # -- Namespace selector for ServiceMonitor resources
  namespaceSelector: {}
  # -- ServiceMonitor annotations
  annotations: {}
  # -- Additional ServiceMonitor labels
  labels: {}
  # -- ServiceMonitor scrape interval
  interval: null
  # -- ServiceMonitor scrape timeout in Go duration format (e.g. 15s)
  scrapeTimeout: null
```

Set up scrapeConfigs - needed so that Promtail knows what it needs and what it doesn't need to collect logs from. More information can be found here: [https://grafana.com/docs/loki/latest/clients/promtail/scraping/](https://grafana.com/docs/loki/latest/clients/promtail/scraping/) 

## Configuring Loki

The main thing to configure in Loki is storage, Loki has two types of stored data: indexes and chunks. The default is boltdb-shipper for index storage and filesystem for chunks storage.

```yaml
## Defualt config for storage
schema_config:
    configs:
    - from: 2020-10-24
      store: boltdb-shipper
      object_store: filesystem
      schema: v11
      index:
        prefix: index_
        period: 24h
storage_config:
    boltdb_shipper:
      active_index_directory: /data/loki/boltdb-shipper-active
      cache_location: /data/loki/boltdb-shipper-cache
      cache_ttl: 24h         # Can be increased for faster performance over longer query periods, uses more disk space
      shared_store: filesystem
    filesystem:
      directory: /data/loki/chunks
```

> BoltDB Shipper lets you run Loki without any dependency on NoSQL stores for storing index. It locally stores the index in BoltDB files instead and keeps shipping those files to a shared object store i.e the same object store which is being used for storing chunks. It also keeps syncing BoltDB files from shared object store to a configured local directory for getting index entries created by other services of same Loki cluster. This helps run Loki with one less dependency and also saves costs in storage since object stores are likely to be much cheaper compared to cost of a hosted NoSQL store or running a self hosted instance of Cassandra.
> 

But with the object store, everything is not so simple, you can store data as with the default configuration. The disadvantage of this solution is the lack of persistent storage, if your virtual machine fails, the chance of losing data is very high. The second disadvantage is the limitation on disk memory. If the first can be dealt with by setting PersistentVolume, then the memory limit is not so simple.

Therefore, if this is a significant limitation for you, you can use Blob storages, such as Google Cloud Storage, S3 (Simple Storage Service)

```yaml
schema_config:
      configs:
      - from: 2020-05-15
        store: boltdb-shipper # aws
        object_store: s3
        schema: v11
        index:
          prefix: loki_
          period: 24h
    storage_config:
      boltdb_shipper:
        active_index_directory: /data/loki/boltdb-shipper-active
        cache_location: /data/loki/boltdb-shipper-cache
        cache_ttl: 24h         # Can be increased for faster performance over longer query periods, uses more disk space
        shared_store: filesystem
      aws:
				# Use it in case you add IAMRole to your EC2 inctances(nodes) (recomended)
        s3: s3://us-west-2/bucket_name
				# Use it in case you cannot add IAMRole to your EC2 inctances(nodes)
      # s3: s3://access_key:secret_access_key@region/bucket_name
```

One of the killer features of Loki (if you work with Prometheus) is alerting, it is configured in exactly the same way as in Prometheus. And Alertmanager can send these alerts.

In order to set up alerting in Loki, you need to enable the Ruler component

```yaml
ruler:
      storage:
        type: local
        local:
          directory: /rules
      rule_path: /tmp/scratch
      alertmanager_url: http://alertmanager.<your-namespace>.svc.cluster.local:9093
      ring:
        kvstore:
          store: inmemory
      enable_api: true
      enable_alertmanager_v2: true
```

Then the matter is small, it remains to add the rules by which alerts will be triggered

```yaml
alerting_groups:
  - name: example
    interval: 1h
    rules:
- alert: HighPercentageError
        expr: |
          sum(rate({app="foo", env="production"} |= "error" [5m])) by (job)
            /
          sum(rate({app="foo", env="production"}[5m])) by (job)
            > 0.05
        for: 10m
        labels:
            severity: page
        annotations:
            summary: High request latency
```

## C**onclusion**

We figured out how to install Grafana Loki in Kubernetes cluster.

If your workload is too heavy and you need to look for logs often and over a long period of time, you can go even further and install [loki-distributed]([https://github.com/grafana/helm-charts/tree/main/charts/loki-distributed](https://github.com/grafana/helm-charts/tree/main/charts/loki-distributed))