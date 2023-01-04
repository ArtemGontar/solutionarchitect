---
title: "k6: Performance testing"
description: "Performance testing is an essential part of development process, it helps ensure that our applications can handle the expected load and usage."
date: 2022-12-21T20:13:07+02:00
keywords:
  - k6
  - performance testing
  - load testing
  - stress testing
  - capacity testing
  - web application performance
  - scalability testing
  - stability testing
  - load impact
  - open source performance testing
draft: false
authors: ["Andrei Yarashenka"]
categories: ["Performance"]
tags: ["k6", "Grafana Labs"]
---

Hello and welcome to this post on the k6 performance testing tool.

![Poster](/posts/performance/poster.svg#center)

## What is performance testing?

Performance testing is an important part of the software development process, as it helps ensure that our applications can handle the expected load and usage. In this video, we will be introducing [k6](https://k6.io/), a popular open-source tool for performance testing.

First, let's define what performance testing is. Performance testing is the process of evaluating the speed, scalability, and stability of a software application under a certain workload. It helps us identify and fix performance issues before our application is deployed to production.

There are several types of performance tests, including load testing, stress testing, and capacity testing. Load testing involves simulating a certain number of users or requests to see how the application performs under normal conditions. Stress testing pushes the application to its limits to see how it handles extreme workloads. Capacity testing determines the maximum capacity of an application, such as the maximum number of users it can handle or the maximum amount of data it can process.

## What is k6 performance tool?

Now, let's talk about [k6](https://k6.io/). k6 is a modern, open-source load testing tool that allows you to easily and accurately test the performance of your web applications. It was developed by Load Impact, a company specializing in performance testing solutions.

One of the main features of k6 is its simplicity. It has a simple, easy-to-use interface and requires minimal setup. It also has a wide range of options for customizing your tests, including the ability to use JavaScript to write custom test scripts.

Another key feature of k6 is its accuracy. It uses real browsers to simulate user requests, which provides more accurate results compared to other tools that use simple HTTP requests. It also has a number of advanced features for analyzing and visualizing test results, including graphs, charts, and metrics.

Finally, k6 is highly scalable. It can simulate thousands of users and requests, making it suitable for testing applications of any size. It also has built-in support for cloud-based load testing, allowing you to easily test your application under heavy workloads.

## Hands on example

First, you will need to install k6 on your machine. You can do this by running the following command:

```bash
npm install -g k6
```

Next, create a new script file called "test.js" and add the following code:

```jsx
import http from "k6/http";

export default function() {
  http.get("http://example.com");
}
```

This script will send a GET request to the specified URL.

To run the test, use the following command:

```bash
k6 run test.js
```

This will run the test with a single virtual user. To simulate multiple users, you can use the **`-u`** flag to specify the number of virtual users, like this:

```bash
k6 run -u 10 test.js
```

This will run the test with 10 virtual users.

You can also specify a duration for the test using the **`-d`** flag, like this:

```bash
k6 run -u 10 -d 30s test.js
```

This will run the test for 30 seconds with 10 virtual users.

Here is an output of command above:

![Output](/posts/performance/output.svg#center)

k6 also provides a number of options for customizing and analyzing your tests. For example, you can use the **`http.batch()`** function to send multiple requests in a single batch, or use the **`check()`** function to add assertions to your tests. You can also use the **`-o`** flag to specify an output file for storing the test results.

For more information on using k6 and all of its features, be sure to check out the k6 documentation and examples.

I hope this helps give you an idea of how to use k6 for performance testing. Happy testing!

## Summary

In summary, k6 is a powerful and easy-to-use performance testing tool that can help you ensure the speed, scalability, and stability of your web applications. If you're looking for a tool to help with performance testing, be sure to check out k6.

### About Author

[Andrei Yarashenka](https://www.linkedin.com/in/andreika-kanareika/) is a skilled software engineer with experience in a variety of technologies, including ASP.NET, SQL, RavenDB, message brokers, Docker, and Angular, [Azure certified](https://www.credly.com/badges/28869c94-6bc8-49e9-a1bb-531d4c35efaa?source=linked_in_profile). He is proficient in designing microservices architecture and has experience with testing frameworks such as NUnit and XUnit. Andrei is also familiar with agile methodologies such as Scrum and Kanban.