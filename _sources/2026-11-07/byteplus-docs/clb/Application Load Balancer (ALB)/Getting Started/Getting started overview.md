---
title: "Getting started overview"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-quick-start-Overview"
---

This topic introduces the quick start process for Application Load Balancer (ALB). If you are using ALB for the first time, you can refer to the simulation scenario below to quickly familiarize yourself with the ALB console, complete basic configurations, and start using the Layer 7 load balancing service.

## Prerequisites

* Before creating an instance, you need to plan the region for your ALB instance based on the primary geographical distribution of your business, aiming to reduce access latency.

* Prepare the [VPC](https://docs.byteplus.com/en/docs/vpc/What-is-VPC) and [Backend ECS instances](https://docs.byteplus.com/en/docs/ecs/Instance-overview) required for subsequent configuration in the selected region in advance.

## **Simulation scenarios**

Assume your company operates an online e\-commerce platform that receives a large volume of user requests daily. For such high\-traffic, high\-concurrency business scenarios, you can use ALB to ensure service availability. In this scenario, assume your website is deployed in Beijing:

* You want to create a public ALB instance that can be accessed over the internet. This instance has an IPv4 address, its listener uses HTTP as the listening protocol, and it listens on port 80.

* You plan to add two ECS instances as backend servers to a server group. The port for both backend servers is 8080. Both backend servers have the same weight. The load balancing algorithm is Weighted Round Robin (WRR).

* You need ALB to monitor the operational status of the backend servers.

## Procedures

ALB operates at the application layer and supports various Layer 7 protocols such as HTTP, HTTPS, HTTP/2, WebSocket, and QUIC. When using the ALB service for the first time, you can quickly create an ALB instance by following the workflow below to forward client access requests to backend servers.

A brief description of the operations corresponding to each step is as follows:

|Procedures |Actions |Explanation |
|---|---|---|
|1 |[Create an ALB instance](https://docs.byteplus.com/docs/clb/Creating-an-ALB-instance) |The instance accepts access requests from clients and forwards them to the backend servers. |
|2 |[Creating a server group](https://docs.byteplus.com/docs/clb/ALB-Creating-a-server-group) |After creating the instance, you need to create a server group and add the backend servers that will actually handle the business traffic. |
|3 |[Creating an HTTP listener](https://docs.byteplus.com/docs/clb/ALB-Creating-an-HTTP-listener) |After creating the server group and adding servers, you need to create an HTTP listener and associate the server group with it. |
