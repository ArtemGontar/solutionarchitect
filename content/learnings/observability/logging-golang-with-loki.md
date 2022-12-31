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
3. [Logging and Tracing in distributed systems](/learnings/observability/logging-and-tracking-in-distributed-system/)
4. [Alerting and incident response in distributed systems](/learnings/observability/alerting-and-incidents-in-distributed-system/)
6. [Debugging distributed systems using tracing and logs](/learnings/observability/debugging-distributed-system)
7. [Understanding distributed system performance using metrics and traces](/learnings/observability/understanding-performance-in-distributed-system/)
8. [Implementing distributed tracing in Golang using OpenTracing](/learnings/observability/implementing-distributed-tracing/)
9. (->) Logging Golang applications with Loki
10. [Monitoring Golang applications with Prometheus](/learnings/observability/monitoring-golang-with-prometheus/)
11. [Visualizing and alerting on distributed system data with Grafana](/learnings/observability/vizualize-and-alerting-with-grafana/)

![Poster](/learnings/observability/logging-golang-with-loki/poster.jpg)

Loki is a popular open-source logging platform that is designed to be easy to use and scalable. In this article, we will explore how to use Loki to log Golang applications.

## Code Sample

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