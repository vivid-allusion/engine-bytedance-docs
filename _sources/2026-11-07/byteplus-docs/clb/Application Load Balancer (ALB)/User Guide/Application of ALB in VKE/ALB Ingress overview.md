---
title: "ALB Ingress overview"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-Ingress-overview"
---

Application Load Balancer (ALB) offers deep integration with Vital Kubernetes Engine (VKE). ALB can replace the native Nginx Ingress of Kubernetes. It allows you to attach applications created in VKE to ALB instances, eliminating the need for separate development and maintenance.​ Through its powerful performance and advanced routing capabilities, ALB contributes to greater overall stability for Kubernetes clusters.​

<span id=".5Z-65pys5qaC5b-1"></span>
## Terms

**Ingress**

Ingress (routing rules) is an independent resource in a Kubernetes cluster. It governs inbound HTTP and HTTPS traffic to services within the cluster by defining forwarding rules based on domain names and paths, enabling fine\-grained traffic distribution.

**Ingress Controller**

The executor of traffic forwarding. It parses the forwarding rules defined by Ingress and routes requests to the appropriate backend services.​

**ALB Ingress**

In cloud native scenarios, the system demands high elasticity and must possess the capability to manage massive volumes of Layer 7 traffic.​ ​​ALB Ingress is a service offered by ALB, integrated with VKE, for cloud native scenarios. Compared to the native Nginx Ingress in Kubernetes, ALB provides a more robust ingress traffic management solution. It supports both HTTP and HTTPS protocols, is equipped with advanced routing capabilities, and is better suited for cloud native scenarios.​

<span id=".YWxiLWluZ3Jlc3Mt5bel5L2c5rWB56iL"></span>
## ALB Ingress workflow

The ALB Ingress workflow diagram is as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ab89e757f6874a2c9ee3cabac2316d79~tplv-goo7wpa0wc-image.image) </span>


* Log in to the VKE console. In the Ingress configuration, set the load balancer's **Ingress type** to **ALB**. Then, configure the traffic forwarding rules, specifying the load balancer, URL, TLS settings, and the target port of the backend service.​

* When a user accesses the service, ALB routes traffic to the appropriate backend service based on the configured forwarding rules. The request ultimately reaches the individual workloads attached to that service.​
