---
title: "Monitoring Golang applications with Prometheus"
description: "Guide to using Prometheus to monitor Golang applications"
date: 2022-12-12T14:53:07+02:00
keywords:
 - monitoring
 - Golang
 - Prometheus
 - metrics
 - counter
 - gauge
 - histogram
 - HTTP handler
 - query language
 - visualization
 - Grafana
 - performance
 - health
 - reliability
 - optimization
authors: ["Artsiom Hontar"]
categories: ["Observability"]
series: ["Observability"]
tags: ["Distributed systems", "Observability"]
draft: false
---

**Table of content**:
1. [Introduction to distributed systems and observability](/learnings/observability/intro-to-distributed-observability/)
2. [Monitoring and metrics in distributed systems](/learnings/observability/monitoring-in-distributed-system/)
3. [Logging and Tracing in distributed systems](/learnings/observability/logging-and-tracing-in-distributed-system/)
4. [Alerting and incident response in distributed systems](/learnings/observability/alerting-and-incidents-in-distributed-system/)
6. [Debugging distributed systems using tracing and logs](/learnings/observability/debugging-distributed-system)
7. [Understanding distributed system performance using metrics and traces](/learnings/observability/understanding-performance-in-distributed-system/)
8. [Implementing distributed tracing in Golang using OpenTracing](/learnings/observability/implementing-distributed-tracing/)
9. [Logging Golang applications with Loki](/learnings/observability/logging-golang-with-loki/)
10. (->) Monitoring Golang applications with Prometheus
11. [Visualizing and alerting on distributed system data with Grafana](/learnings/observability/vizualize-and-alerting-with-grafana/)

![Poster](/learnings/observability/monitoring-golang-with-prometheus/poster.jpg)

Prometheus is a popular open-source monitoring tool that is widely used to monitor the performance and health of applications and systems. In this article, we will explore how to use Prometheus to monitor Golang applications.

## Using Prometheus with Golang

To use Prometheus with Golang, we first need to install the [Prometheus client library for Golang](https://github.com/prometheus/client_golang). This can be done using the following command:

```bash
go get github.com/prometheus/client_golang/prometheus
```
Once the library is installed, we can start using it in our Golang code. The Prometheus client library provides a number of types and functions that can be used to collect and expose metrics from our application.

One of the key concepts in Prometheus is the metric. A metric is a quantitative measure of some aspect of our application, such as the number of requests processed, the response time of a service, or the CPU usage of a process. Prometheus provides a number of different metric types, including counter, gauge, and histogram, which can be used to track different types of metrics.

To collect metrics in our Golang application, we can use the `NewCounter`, `NewGauge`, and `NewHistogram` functions from the Prometheus client library. These functions take a number of arguments, including the name of the metric, any relevant labels, and the help text for the metric. For example:

```golang
requestCounter := prometheus.NewCounter(
    prometheus.CounterOpts{
        Name: "myapp_request_total",
        Help: "Total number of requests processed by the application",
    },
)

responseTime := prometheus.NewHistogram(
    prometheus.HistogramOpts{
        Name:    "myapp_response_time_seconds",
        Help:    "Response time of the application in seconds",
        Buckets: prometheus.LinearBuckets(0, 0.1, 10),
    },
)
```

Once we have defined our metrics, we can use them to track the performance and behavior of our application. For example, we can use a counter to track the number of requests processed, or a histogram to track the distribution of response times. To record a value for a metric, we can use the `Inc` or `Observe` functions from the Prometheus client library. For example:

```golang
requestCounter.Inc()

responseTime.Observe(time.Since(start).Seconds())
```

Once we have collected metrics from our application, we need to expose them to Prometheus in a format that it can understand. To do this, we can use the Prometheus HTTP handler provided by the client library. The HTTP handler exposes the collected metrics over HTTP in a format that Prometheus can scrape and process. To use the HTTP handler, we need to register it with an HTTP server and specify a path for Prometheus to scrape. For example:

```golang
http.Handle("/metrics", prometheus.Handler())
http.ListenAndServe(":8080", nil)
```

Once the metrics are exposed to Prometheus, we can use Prometheus to monitor and visualize them. Prometheus provides a rich query language and a powerful visualization tool called Grafana that can be used to analyze and understand the collected metrics.

## Summary

Monitoring Golang applications with Prometheus is a powerful and effective way to understand the performance and behavior of our applications. By using the Prometheus client library and its integrations with other tools such as Grafana, we can gain valuable insights into the health and performance of our systems and take appropriate action to optimize and improve them.

## Resources
- [Prometheus client library for Golang](https://github.com/prometheus/client_golang)