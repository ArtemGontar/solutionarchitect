---
title: "Why do you need a reverse proxy server in 5 acts"
description: "This article describes the use of reverse proxy servers, which are a type of proxy server that relays client requests from the external network to one or more servers located on the internal network. The article explains how reverse proxy servers can be used to solve a variety of problems, including adding HTTPS support to a website, load balancing between multiple servers, protecting against hacking and DDoS attacks, optimizing network performance through request compression and caching, and conducting A/B testing. The article mentions several specific reverse proxy servers, including Nginx, Envoy, HAProxy, and Traefik, as well as cloud provider-specific proxy servers such as AWS Elastic LoadBalancer, Google Cloud Load Balancer, DigitalOcean Load Balancer, and Azure Load Balancer. The article includes illustrations to help clarify the concepts being discussed."
date: 2021-01-24T11:13:07+02:00
keywords:
- proxy
- reverse proxy
- proxy server
- nginx
- envoy
- traefik
draft: false
---

There are a wide variety of reverse proxy servers currently available. I will only list a couple of them.

- Nginx
- Envoy
- HAProxy
- Traefik

Also, every self-respecting cloud provider has its own proxy server.

- AWS Elastic LoadBalancer
- Google Cloud Load Balancer
- DigitalOcean Load Balancer
- Azure load balancer

Let's define the word reverse proxy server.

A reverse proxy is a type of proxy server that relays client requests from the external network to one or more servers that are logically located on the internal network. At the same time, for the client it looks as if the requested resources are located directly on the proxy server.

And stick the picture for clarity.

![reverse_proxy1](/posts/tools/reverse_proxy1.png)

## What problem do proxy servers solve?

### Act first

We have a website that does not support HTTPS (because TLS / SSL communication was not programmed). Telling developers to cut it down is easy, but the developers themselves can be stressful with the implementation. If we have a monolith application, we need to make changes to this, most often not a flexible unit, and deliver it to production, if we have light microservices, we need to visit each one, we need to make small edits to each one + again deliver all this.

How do we solve the problem? We take an idle SysOps / DevOps, we say that we need https. Some Ops puts us a proxy server configures it to accept HTTPS traffic + SSL termination. Problem solved, solution price: 1 Some Ops.

![reverse_proxy2](/posts/tools/reverse_proxy2.png)

### Act second

Yes, we still have the same application, but the engineers made it so that it could scale horizontally, and they raised two copies of the application. Super! How to configure so that the traffic arrives evenly on both?

And again the server comes to the rescue, which acts as a "load balancer". Plus, you can also configure the viability check, suddenly one copy falls, why should we upset users. To temporarily place everyone on the remaining server, and the trick is in the bag. After fixing a broken server, the proxy server will automatically return it to service, and you can balance yourself longer.

As a result: two birds with one stone, so to speak.

### Act third

We were hacked by "hackers", trouble. Letting this happen again - well, you just can't.

What do we need for this? A promising Chinese development is a firewall to filter traffic from unwanted users and defend against DDoS attacks.

Well, the proxy server will help us to solve this problem, we "broadcast" all these settings to it and no "hackers" will bypass our mega-services. The main thing is to set it up correctly so that the CEO does not consider it a hacker during demos.

![reverse_proxy3](/posts/tools/reverse_proxy3.png)

### Act fourth

Well, well, HTTPS is there, the balancer is there, protection from hackers is, it would seem, sit and chill yourself in front of the telecom, but again something is wrong. Requests on the network go around for a long time, a couple of dozen did not return at all, clients are in a panic.

Analyzing the problem, yeah, to the fortuneteller - we have a huge "payload in requests" and a couple of "popular" endpoints (users love a part of the service and actively use it).

Well, we sculpt the compression of the request at the level of our proxy server and cache the responses of the application servers on it. What is this? Two birds with one stone again? Yes sir!

Now requests for a cold one return nowhere faster, and with a cache, and even more so.

### Act fifth

We have already made life simple for the clients of our application, it's time to think about yourself.

New features in production delivery suffers what if?

A/B testing can be configured with a proxy server, what could be better than a complete system failure with bugs in a new release? That's right, some users only have a refusal.

After the introduction of this feature, the reputation of your application will not suffer as much as it did before the introduction of A/B testing, because negative comments will be written only by a narrow circle of "lucky ones".

![reverse_proxy4](/posts/tools/reverse_proxy4.png)

## Summarizing the above

Functions that proxy servers provide:

- Supports SSL / TLS traffic
- SSL / TLS termination
- Load balancing
- Checking the health of target servers
- Compression of content
- Caching requests
- Firewall / DDoS protection
- A/B testing

In total, by adding a proxy server to your application, your life will become 