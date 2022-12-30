---
title: "Monitoring Golang applications with Prometheus"
description: "Guide to implementing distributed tracing in Golang using the OpenTracing library"
date: 2022-11-28T20:35:04+02:00
keywords:
 - distributed tracing
 - Golang
 - OpenTracing
 - performance
 - reliability
 - HTTP
 - logrus
 - gin
 - request flow
 - trace data
 - metadata
 - timestamps
 - error codes
 - logging
 - HTTP framework
draft: false
authors: ["Artsiom Hontar"]
categories: ["Observability"]
series: ["Observability"]
tags: ["Distributed systems", "Observability"]
---

Table of content:
1. [Introduction to distributed systems and observability](/learnings/observability/intro-to-distributed-observability/)
2. [Monitoring and metrics in distributed systems](/learnings/observability/monitoring-in-distributed-system/)
3. [Logging and Tracing in distributed systems](/learnings/observability/logging-and-tracking-in-distributed-system/)
4. [Alerting and incident response in distributed systems](/learnings/observability/alerting-and-incidents-in-distributed-system/)
6. [Debugging distributed systems using tracing and logs](/learnings/observability/debugging-distributed-system)
7. [Understanding distributed system performance using metrics and traces](/learnings/observability/understanding-performance-in-distributed-system/)
8. (->) Implementing distributed tracing in Golang using OpenTracing
9. [TBD] Logging Golang applications with Loki
10. [TBD] Monitoring Golang applications with Prometheus
11. [TBD] Visualizing and alerting on distributed system data with Grafana

![Poster](/learnings/observability/implementing-distributed-tracing/poster.jpg)

Distributed tracing is a powerful tool for understanding the interactions and performance of distributed systems. It involves collecting and storing data on the flow of requests and responses through different components and services, and can be used to identify performance bottlenecks and other issues. In this article, we will explore how to implement distributed tracing in Golang using OpenTracing, a popular open-source tracing library.

## Code sample

To use OpenTracing in Golang, we first need to install the library and its dependencies. This can be done using the following command:

```bash
go get github.com/opentracing/opentracing-go
```

Once the library is installed, we can start using it in our Golang code. To begin a trace, we can use the StartSpan function from the OpenTracing library. This function takes a number of arguments, including the name of the span, the parent span (if any), and any relevant tags or metadata. For example:

```go
span := opentracing.StartSpan("my-span", 
    opentracing.ChildOf(parentSpan.Context()))
defer span.Finish()
```

Once we have started a span, we can use it to track the flow of requests and responses through our distributed system. To do this, we can use the Inject and Extract functions from the OpenTracing library. The Inject function allows us to inject trace data into a request, such as a HTTP header or a message payload. The Extract function allows us to extract trace data from a request, such as a HTTP header or a message payload. For example:

```go
carrier := opentracing.HTTPHeadersCarrier(httpReq.Header)
err := tracer.Inject(span.Context(), opentracing.HTTPHeaders, carrier)
if err != nil {
    // handle error
}

spanContext, err := tracer.Extract(opentracing.HTTPHeaders, carrier)
if err != nil {
    // handle error
}
```

Once we have injected and extracted trace data, we can use it to follow the flow of requests and responses through our system. For example, we can use the trace data to link together multiple requests and responses, or to understand the performance of different components and services.

## Advanced features

There are also several advanced features and options available in the OpenTracing library that can be used to further customize and optimize the tracing process. For example, we can use the SetOperationName function to set the operation name of a span, or the SetTag function to add custom tags and metadata to a span. We can also use the FinishWithOptions function to specify custom timestamps or error codes when finishing a span.

In addition to using the OpenTracing library directly, we can also use it in combination with other tools and libraries to further enhance our tracing capabilities. For example, we can use the OpenTracing integration with the logrus logging library to link log events with trace data, or use the OpenTracing integration with the gin HTTP framework to automatically instrument HTTP requests and responses.

Overall, implementing distributed tracing in Golang using OpenTracing is a powerful and flexible way to understand and improve the performance of distributed systems. By using this library and its advanced features and integrations, we can gain valuable insights into the behavior and performance of our systems, and take appropriate action to optimize and improve them.