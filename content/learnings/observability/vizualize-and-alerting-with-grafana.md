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
3. [Logging and Tracing in distributed systems](/learnings/observability/logging-and-tracking-in-distributed-system/)
4. [Alerting and incident response in distributed systems](/learnings/observability/alerting-and-incidents-in-distributed-system/)
6. [Debugging distributed systems using tracing and logs](/learnings/observability/debugging-distributed-system)
7. [Understanding distributed system performance using metrics and traces](/learnings/observability/understanding-performance-in-distributed-system/)
8. [Implementing distributed tracing in Golang using OpenTracing](/learnings/observability/implementing-distributed-tracing/)
9. [Logging Golang applications with Loki](/learnings/observability/logging-golang-with-loki/)
10. [Monitoring Golang applications with Prometheus](/learnings/observability/monitoring-golang-with-prometheus/)
11. (->) Visualizing and alerting on distributed system data with Grafana

![Poster](/learnings/observability/vizualize-and-alerting-with-grafana/poster.jpg)

Grafana is a popular open-source visualization and monitoring platform that is widely used to visualize and alert on data from distributed systems. In this article, we will explore how to use Grafana to visualize and alert on distributed system data, with examples and screenshots from some of the most popular Grafana dashboards.

To use Grafana, we first need to install it and set it up. Grafana can be installed on a variety of platforms, including Linux, Windows, and Docker, and can be configured to collect data from a variety of sources, including Prometheus, Loki, Elasticsearch, and InfluxDB.

Once Grafana is installed and configured, we can use it to visualize and alert on distributed system data. Grafana provides a rich set of visualization options that can be used to create custom dashboards and panels to display data from our distributed system. Some of the visualization options available in Grafana include graphs, tables, heatmaps, and gauges.

To create a visualization in Grafana, we need to select a data source and a query. The data source is the source of the data that we want to visualize, such as a Prometheus server or an Elasticsearch cluster. The query is the expression that we use to filter and aggregate the data from the data source. Grafana supports a variety of query languages, depending on the data source, such as PromQL for Prometheus, LokiQL for Loki, and Elasticsearch Query DSL for Elasticsearch.

In addition to visualizing data, Grafana also provides a rich set of alerting options that can be used to create custom alerts based on data from our distributed system. Grafana alerts can be triggered based on various criteria, such as the value of a metric, the rate of change of a metric, or the occurrence of a certain pattern in the data.

![Istio workload dashboard](/learnings/observability/vizualize-and-alerting-with-grafana/istio-workload-dashboard.jpg)

To create an alert in Grafana, we need to define an alert rule that specifies the conditions under which the alert should be triggered. The alert rule can be based on a query that returns a single value, such as a metric or a scalar, or a query that returns a series of values, such as a time series or a table. Grafana supports a variety of alerting options, including thresholds, time periods, and evaluation intervals, that can be used to fine-tune the behavior of the alert.

![Alert view](/learnings/observability/vizualize-and-alerting-with-grafana/rules-groups.jpg)

Once an alert is triggered, Grafana can send notifications to one or more notification channels, such as email, Slack, or PagerDuty, to inform the relevant parties about the alert. Grafana also provides a rich set of options for managing and tracking alerts, including alert history, alert states, and alert silencing.

Grafana is a powerful and flexible tool for visualizing and alerting on distributed system data. By using Grafana and its rich set of visualization and alerting options, we can gain valuable insights into the behavior and performance of our distributed systems and take appropriate action to optimize and improve them. Some of the most popular Grafana dashboards include the Prometheus Stats dashboard, the Kubernetes dashboard, and the MySQL dashboard. These dashboards provide a wealth of information and can be customized to suit the needs of a particular system.

![Vendor dashboards](/learnings/observability/vizualize-and-alerting-with-grafana/vendor-dashboards.jpg)