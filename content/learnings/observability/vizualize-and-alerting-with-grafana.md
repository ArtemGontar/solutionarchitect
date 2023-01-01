---
title: "Visualizing and alerting on distributed system data with Grafana"
description: "Guide to using Grafana to visualize and alert on distributed system data"
date: 2022-12-31T14:53:07+02:00
keywords:
 - Grafana
 - visualization
 - monitoring
 - alerting
 - distributed systems
 - data sources
 - query languages
 - dashboards
 - panels
 - graphs
 - tables
 - heatmaps
 - gauges
 - alert rules
 - thresholds
 - time periods
 - evaluation intervals
 - notification channels
 - alert history
 - alert states
 - alert silencing
 - Prometheus
 - Loki
 - Elasticsearch
 - InfluxDB
 - PromQL
 - LokiQL
 - Elasticsearch Query DSL
 - Prometheus Stats dashboard
 - Kubernetes dashboard
 - MySQL dashboard
authors: ["Artsiom Hontar"]
categories: ["Observability"]
series: ["Observability"]
tags: ["Distributed systems", "Observability"]
draft: false
---

Table of content:
1. [Introduction to distributed systems and observability](/learnings/observability/intro-to-distributed-observability/)
2. [Monitoring and metrics in distributed systems](/learnings/observability/monitoring-in-distributed-system/)
3. [Logging and Tracing in distributed systems](/learnings/observability/logging-and-tracing-in-distributed-system/)
4. [Alerting and incident response in distributed systems](/learnings/observability/alerting-and-incidents-in-distributed-system/)
6. [Debugging distributed systems using tracing and logs](/learnings/observability/debugging-distributed-system)
7. [Understanding distributed system performance using metrics and traces](/learnings/observability/understanding-performance-in-distributed-system/)
8. [Implementing distributed tracing in Golang using OpenTracing](/learnings/observability/implementing-distributed-tracing/)
9. [Logging Golang applications with Loki](/learnings/observability/logging-golang-with-loki/)
10. [Monitoring Golang applications with Prometheus](/learnings/observability/monitoring-golang-with-prometheus/)
11. (->) Visualizing and alerting on distributed system data with Grafana

![Poster](/learnings/observability/vizualize-and-alerting-with-grafana/poster.jpg)

## Installing and Configuring Grafana
Grafana is a popular open-source visualization and monitoring platform that is widely used to visualize and alert on data from distributed systems. In this article, we will explore how to use Grafana to visualize and alert on distributed system data, with examples and screenshots from some of the most popular Grafana dashboards.

To use Grafana, we first need to install it and set it up. Grafana can be installed on a variety of platforms, including Linux, Windows, and Docker, and can be configured to collect data from a variety of sources, including Prometheus, Loki, Elasticsearch, and InfluxDB.

### Installing Grafana: Docker

To install and configure Grafana, follow these steps:

Download and install Grafana:
1. Pull the Grafana Docker image from Docker Hub and run it using the following command:
```bash
docker run -d --name=grafana -p 3000:3000 grafana/grafana
```

2. Start the Grafana container using the following command:
```bash
docker start grafana
```

### Installing Grafan: Kubernetes

To install and configure Grafana on a Kubernetes cluster, you will need to follow these steps:

Install the Grafana Helm chart. The Helm chart is a package manager for Kubernetes that makes it easy to install and manage applications on a cluster. To install the Grafana Helm chart, you will need to have Helm installed on your cluster. You can install Helm using the instructions in the Helm documentation.
Once Helm is installed, you can use it to install the Grafana Helm chart. To do this, run the following command:

```bash
helm install --name grafana stable/grafana
```

This will install Grafana and all its dependencies on your cluster. The `--name` flag specifies the name of the Helm release, which will be used to identify the Grafana installation.

Expose the Grafana service. The Grafana service is the Kubernetes service that exposes the Grafana API and UI to the rest of the cluster. To expose the Grafana service, you can use the `kubectl expose` command. For example:
```bash
kubectl expose deployment grafana --type=LoadBalancer --port=3000 --target-port=3000
```
This command will create a LoadBalancer service that exposes the Grafana API and UI on port 3000. The `--type` flag specifies the type of service to create, while the `--port` and `--target-port` flags specify the port to expose and the target port on the Grafana pod, respectively.

Access the Grafana UI. Once the Grafana service is exposed, you can access the Grafana UI using a web browser. To do this, you will need to get the public IP address or hostname of the service. You can use the `kubectl get service` command to get the public IP address or hostname of the Grafana service. For example:

```bash
kubectl get service grafana
```

This command will print the public IP address or hostname of the Grafana service, along with other information about the service. You can use the public IP address or hostname to access the Grafana UI in a web browser by visiting http://<public-ip-or-hostname>:3000.

### Configure Grafana
- Open the Grafana web interface in your web browser by going to http://<localhost>:3000 (if you are running Grafana on the same machine) or http://<server_ip>:3000 (if you are running Grafana on a remote machine).
- Log in to Grafana using the default username and password (admin/admin).
- Change the default password by going to the "Configuration" tab in the left menu and clicking on the "Change password" button.
- Add a data source by going to the "Data Sources" tab in the left menu and clicking on the "Add data source" button. Select the type of data source you want to add (e.g. Prometheus, Loki, Elasticsearch, etc.) and enter the necessary details for the data source.
- Create a dashboard by going to the "Dashboards" tab in the left menu and clicking on the "Create new dashboard" button. Add panels to the dashboard by clicking on the "Add panel" button and selecting the type of panel you want to add (e.g. graph, table, heatmap, etc.). Select the data source and specify the query for the panel using the appropriate query language (e.g. PromQL, LokiQL, Elasticsearch Query DSL, etc.).

## Visualizing Distributed System Data with Grafana
Once Grafana is installed and configured, we can use it to visualize and alert on distributed system data. Grafana provides a rich set of visualization options that can be used to create custom dashboards and panels to display data from our distributed system. Some of the visualization options available in Grafana include graphs, tables, heatmaps, and gauges.

To create a visualization in Grafana, we need to select a data source and a query. The data source is the source of the data that we want to visualize, such as a Prometheus server or an Elasticsearch cluster. The query is the expression that we use to filter and aggregate the data from the data source. Grafana supports a variety of query languages, depending on the data source, such as PromQL for Prometheus, LokiQL for Loki, and Elasticsearch Query DSL for Elasticsearch.

In addition to visualizing data, Grafana also provides a rich set of alerting options that can be used to create custom alerts based on data from our distributed system. Grafana alerts can be triggered based on various criteria, such as the value of a metric, the rate of change of a metric, or the occurrence of a certain pattern in the data.

![Istio workload dashboard](/learnings/observability/vizualize-and-alerting-with-grafana/istio-workload-dashboard.jpg)

## Alerting on Distributed System Data with Grafana
To create an alert in Grafana, we need to define an alert rule that specifies the conditions under which the alert should be triggered. The alert rule can be based on a query that returns a single value, such as a metric or a scalar, or a query that returns a series of values, such as a time series or a table. Grafana supports a variety of alerting options, including thresholds, time periods, and evaluation intervals, that can be used to fine-tune the behavior of the alert.

![Alert view](/learnings/observability/vizualize-and-alerting-with-grafana/rules-groups.jpg)

Once an alert is triggered, Grafana can send notifications to one or more notification channels, such as email, Slack, or PagerDuty, to inform the relevant parties about the alert. Grafana also provides a rich set of options for managing and tracking alerts, including alert history, alert states, and alert silencing.

## Popular Grafana Dashboards for Distributed Systems
Grafana is a powerful and flexible tool for visualizing and alerting on distributed system data. By using Grafana and its rich set of visualization and alerting options, we can gain valuable insights into the behavior and performance of our distributed systems and take appropriate action to optimize and improve them. Some of the most popular Grafana dashboards include the Prometheus Stats dashboard, the Kubernetes dashboard, and the MySQL dashboard. These dashboards provide a wealth of information and can be customized to suit the needs of a particular system.

![Vendor dashboards](/learnings/observability/vizualize-and-alerting-with-grafana/vendor-dashboards.jpg)