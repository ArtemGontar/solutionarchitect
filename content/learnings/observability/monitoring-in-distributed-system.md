---
title: "Monitoring and metrics in distributed systems"
description: "Key methods and frameworks for monitoring and measuring distributed systems: the RED Method, the USE Method, and the Four Golden Signals method."
date: 2022-10-24T14:53:07+02:00
keywords:
 - monitoring
 - metrics
 - distributed systems
 - RED Method
 - USE Method
 - Four Golden Signals method
 - request rate
 - errors
 - duration
 - utilization
 - saturation
 - latency
 - traffic
 - error rates
 - resource utilization
draft: false
authors: ["Artsiom Hontar"]
categories: ["Observability"]
series: ["Observability"]
tags: ["Distributed systems", "Observability"]
---

Table of content:
1. [Introduction to distributed systems and observability](/learnings/observability/intro-to-distributed-observability/)
2. (->) Monitoring and metrics in distributed systems
3. [Logging and Tracing in distributed systems](/learnings/observability/logging-and-tracing-in-distributed-system/)
4. [Alerting and incident response in distributed systems](/learnings/observability/alerting-and-incidents-in-distributed-system/)
6. [Debugging distributed systems using tracing and logs](/learnings/observability/debugging-distributed-system)
7. [Understanding distributed system performance using metrics and traces](/learnings/observability/understanding-performance-in-distributed-system/)
8. [Implementing distributed tracing in Golang using OpenTracing](/learnings/observability/implementing-distributed-tracing/)
9. [Logging Golang applications with Loki](/learnings/observability/logging-golang-with-loki/)
10. [Monitoring Golang applications with Prometheus](/learnings/observability/monitoring-golang-with-prometheus/)
11. [Visualizing and alerting on distributed system data with Grafana](/learnings/observability/vizualize-and-alerting-with-grafana/)


![Poster](/learnings/observability/monitoring-in-distributed-system/poster.jpg)

## Monitoring and Metrics: Essential Tools for Understanding System Behavior

Monitoring and metrics are essential tools for understanding the behavior of distributed systems. By collecting and analyzing data on system performance, we can identify and resolve issues, optimize resources, and improve the overall reliability and effectiveness of our systems.

![Metrics](/learnings/observability/monitoring-in-distributed-system/metrics.jpg)

## Components of an Observability System: Data Collection, Storage, Processing, Alerting, and Visualization

- Data collection: This involves gathering data from various sources, such as system logs, application metrics, and hardware performance metrics. It is important to choose the right tools and technologies for collecting this data, as well as to define clear goals and metrics that will help us understand and improve our systems.

- Data storage and processing: Once the data has been collected, it needs to be stored and processed in a way that allows us to access and analyze it easily. This often involves using a time-series database or data lake, as well as tools for querying and visualizing the data.

- [Alerting](/learnings/observability/alerting-and-incidents-in-distributed-system/): Monitoring and metrics can help us identify problems and issues in our systems, but it is important to have a system in place for alerting when these issues occur. This can involve setting up thresholds or rules for triggering alerts, as well as defining appropriate responses and escalation processes.

- [Dashboards and visualization](/learnings/observability/vizualize-and-alerting-with-grafana/): Visualizing the data collected by our monitoring and metrics systems can be a powerful way to understand and communicate the performance and behavior of our systems. Dashboards and visualization tools can help us see trends, identify patterns, and spot potential issues more easily.

## Methods and Frameworks for Monitoring and Measuring Distributed Systems: The RED Method, The USE Method, and The Four Golden Signals

There are several key methods and frameworks that can help us effectively monitor and measure distributed systems, including the RED Method, the USE Method, and the Four Golden Signals method.

### The RED Method

[The RED Method](https://grafana.com/files/grafanacon_eu_2018/Tom_Wilkie_GrafanaCon_EU_2018.pdf) (Request Rate, Errors, and Duration) is a simple and effective way to monitor distributed systems. It involves collecting data on request rate (how many requests are being handled per second), errors (how many requests are failing), and duration (how long requests are taking to complete). By tracking these three metrics, we can identify issues with request volume, error rates, and performance, and take appropriate action to resolve them.

### The USE Method
[The USE Method](https://www.brendangregg.com/usemethod.html) (Utilization, Saturation, and Errors) is another useful tool for monitoring distributed systems. It involves collecting data on utilization (how much of a resource is being used), saturation (how close a resource is to being fully utilized), and errors (how many errors are occurring). By tracking these three metrics, we can identify issues with resource utilization, saturation, and error rates, and take appropriate action to resolve them.

### The Four Golden Signals
[The Four Golden Signals](https://sre.google/sre-book/monitoring-distributed-systems/#xref_monitoring_golden-signals) method is a more comprehensive approach to monitoring distributed systems. It involves collecting data on latency (how long it takes for a request to be completed), traffic (how much traffic is being handled by the system), errors (how many errors are occurring), and saturation (how close a resource is to being fully utilized). By tracking these four metrics, we can identify issues with latency, traffic, error rates, and resource utilization, and take appropriate action to resolve them.

## Summary

Monitoring and metrics are essential for understanding and improving the performance, reliability, and correctness of distributed systems. By implementing effective monitoring and metrics practices, and using methods and frameworks like the RED Method, the USE Method, and the Four Golden Signals method, we can build systems that are more resilient, scalable, and able to deliver value to our users.

Resources:
- [The RED Method presentation](https://grafana.com/files/grafanacon_eu_2018/Tom_Wilkie_GrafanaCon_EU_2018.pdf)
- [The USE Method post](https://www.brendangregg.com/usemethod.html)
- [The Four Golden Signals SRE book](https://sre.google/sre-book/monitoring-distributed-systems/#xref_monitoring_golden-signals)