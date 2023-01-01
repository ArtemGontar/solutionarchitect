---
title: "Logging Golang applications with Loki"
description: "Guide to using Loki to log Golang applications"
date: 2022-12-05T14:53:07+02:00
keywords:
 - logging
 - Golang
 - Loki
 - log streams
 - metadata
 - query language
 - visualization
 - Grafana
 - performance
 - analysis
 - structured data
 - log level
 - log messages
 - filters, search
 - optimization
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
9. (->) Logging Golang applications with Loki
10. [Monitoring Golang applications with Prometheus](/learnings/observability/monitoring-golang-with-prometheus/)
11. [Visualizing and alerting on distributed system data with Grafana](/learnings/observability/vizualize-and-alerting-with-grafana/)

![Poster](/learnings/observability/logging-golang-with-loki/poster.jpg)

Loki is a popular open-source logging platform that is designed to be easy to use and scalable. In this article, we will explore how to use Loki to log Golang applications.

## Using Zap and Promtail to Log and Monitor a Golang Application in Kubernetes

To use the most popular logging library for Golang, [Zap](https://github.com/uber-go/zap), we first need to install it and its dependencies. This can be done using the following command:

```golang
go get github.com/uber-go/zap
```

Once Zap is installed, we can start using it in our Golang code. Zap provides a number of types and functions for creating and logging messages, as well as for configuring the logging output.

To create a new logger in Zap, we can use the NewProduction function. This function returns a logger that is optimized for production use, with a JSON output format and a low-level output sink. For example:

```golang
logger, err := zap.NewProduction()
if err != nil {
    // handle error
}
defer logger.Sync()
```

Once we have created a logger, we can use it to log messages using the Info, Warn, and Error functions. These functions take a message string as an argument, and log it to the output sink along with any relevant metadata. For example:

```golang
logger.Info("This is a log message")
logger.Warn("This is a warning message")
logger.Error("This is an error message")
```

In addition to logging messages, Zap also allows us to attach structured data to our log messages. Structured data is data that is organized in a defined format, such as JSON or YAML, and can be queried or filtered more easily. To attach structured data to a log message, we can use the With function from the Zap library. This function takes a field name and value as arguments, and adds the field

To configure Promtail to scrape logs from a Golang application pod, you will need to follow these steps:

1. Install Promtail on your cluster. If you are using [Helm](https://helm.sh/), you can use the official Promtail chart to install Promtail. If you are not using Helm, you can follow the instructions in the [Promtail documentation](https://grafana.com/docs/loki/latest/clients/promtail/) to install Promtail manually.

2. Create a `Service` and a `Deployment` for your Golang application. The Service will be used to expose your application to the rest of the cluster, while the Deployment will manage the deployment and scaling of your application. You can use [Kubernetes manifests](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) to define your `Service` and `Deployment`.

3. Configure your Golang application to write logs to `stdout` and `stderr`. This will allow Promtail to scrape the logs from your application pod using the `stdout` and `stderr` log streams.

4. Create a `ConfigMap` for Promtail. The `ConfigMap` will contain the configuration for Promtail, including the target pods and log paths to scrape. You can use the [scrape_configs](https://grafana.com/docs/loki/latest/clients/promtail/scraping/) field in the Promtail configuration to specify the target pods and log paths. For example:

5. Deploy the `ConfigMap` and the Promtail deployment. You can use `kubectl` or a configuration management tool to deploy the `ConfigMap` and the Promtail deployment to your cluster.

6. Verify that Promtail is correctly scraping logs from your Golang application pod. You can use the `kubectl logs` command to view the logs of your Promtail pod, and check that it is correctly scraping logs from your application pod. You can also use Loki and Grafana to query and visualize the logged data.

That's it! You should now have Promtail configured to scrape logs from your Golang application pod. You can use Promtail and Loki to monitor and troubleshoot your application, and use Grafana to visualize and analyze your logged data.

## Sending Logs to Loki from Golang: Using the Loki Client Library and Query Language

To use Loki with Golang, we first need to install the Loki client library for Golang. This can be done using the following command:

```bash
go get github.com/grafana/loki/pkg/promtail/client
```

Once the library is installed, we can start using it in our Golang code. The Loki client library provides a number of types and functions that can be used to send log messages to a Loki server.

One of the key concepts in Loki is the log stream. A log stream is a group of log messages that share a common label or metadata. Log streams can be used to organize and filter log messages, and can be queried using the Loki query language.

To send log messages to Loki from our Golang application, we can use the New function from the Loki client library to create a new log stream. This function takes a number of arguments, including the name of the log stream, any relevant labels, and the address of the Loki server. For example:

```golang
logger, err := client.New("http://localhost:3100", "my-app", map[string]string{"env": "production"})
if err != nil {
    // handle error
}
```

Once we have created a log stream, we can use it to send log messages to Loki. To do this, we can use the Info, Warn, and Error functions from the Loki client library. These functions take a log message as an argument, and send it to the Loki server along with any relevant metadata. For example:

```golang
logger.Info("This is a log message")
logger.Warn("This is a warning message")
logger.Error("This is an error message")
```

In addition to sending log messages to Loki, we can also use the Loki client library to attach structured data to our log messages. Structured data is data that is organized in a defined format, such as JSON or YAML, and can be queried using the Loki query language. To attach structured data to a log message, we can use the WithFields function from the Loki client library. This function takes a map of field names and values as an argument, and adds the fields to the log message. For example:

```golang
logger.WithFields(map[string]interface{}{
    "user_id": 123456,
    "action": "login",
}).Info("User logged in")
```

Once we have sent log messages to Loki, we can use the Loki query language and Grafana, the visualization tool provided by Loki, to search, filter, and visualize the log data. The Loki query language is a powerful and flexible tool that allows us to search and filter log messages using various criteria, such as log level, log stream, and metadata. Grafana provides a rich set of visualization options that can be used to analyze and understand the logged data.

## Summary

Logging Golang applications with Loki is a powerful and effective way to understand and analyze the behavior and performance of our applications. By using the Loki client library and its integrations with other tools such as Grafana, we can gain valuable insights into the operation and performance of our systems and take appropriate action to optimize and improve them.

## Resources
- [Zap](https://github.com/uber-go/zap)
- [Promtail Golang client](https://pkg.go.dev/github.com/grafana/loki/pkg/promtail)
- [Helm](https://helm.sh/docs/)
- [Promtail documentation](https://grafana.com/docs/loki/latest/clients/promtail/)
- [Kubernetes deployment manifests](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)
- [Kubernetes service manifests](https://kubernetes.io/docs/concepts/services-networking/service/)