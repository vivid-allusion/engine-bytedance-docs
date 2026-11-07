---
title: "What is an API gateway"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/What_is_an_API_Gateway"
---

API Gateway (APIG) is a cloud\-based gateway hosting service with high scalability and high availability. Provide intelligent routing, multi\-protocol support, and AI model proxy. Combining the autoscaler, authentication and authorization, and canary release ensures the efficient and stable operation of the AI service.

<span id=".5Lqn5ZOB5p625p6E"></span>
## Why choose an API gateway

API Gateway is a cloud\-native gateway service hosted on BytePlus, and supports connection to Vital Kubernetes Engine clusters, Elastic Compute Service, Function Service, microservices engine, and other cloud\-based foundational resources. It provides north\-south and east\-west traffic management for users' cloud applications. It also supports connecting to AI frameworks and services deployed in the cloud. The API gateway mainly provides the following features, depending on the backend cloud products it connects to:


|Main features |Feature description |
|---|---|
|Traffic gateway |Built on Envoy, compatible with the Kubernetes Ingress standard, and supports connecting to Vital Kubernetes Engine clusters, ECS instances, and veFaaS function instances. It is responsible for providing ingress traffic management for clusters, ECS, or function instances, including routing policy, security authentication, protocol forwarding, monitoring, alerting, and other features. |
|Microservice gateway |Connect to the microservices engine (MSE) registration center to provide registered applications with cloud\-native gateway features, enabling a highly available and scalable Ingress traffic management approach. Leverage microservice governance capabilities, such as full\-link canary release and other methods, to enhance application stability across the entire chain. |
|AI gateway |In large language model scenarios, provide a unified entry point and a standardized API layer that allows clients to use the same client to access multiple model vendors. This approach hides differences in API calls between vendors and reduces adaptation costs. Requests can also be intelligently routed to different large models based on the proportion of traffic in each scenario. Additionally, provide security authentication and observability capabilities for invoking large models. |


<span id=".5Lqn5ZOB5p625p6E"></span>
## Product Architecture

Building on traditional traffic gateways, the API gateway integrates comprehensive service discovery and service governance capabilities, bridging internal and external networks within the microservices architecture to quickly enable secure communication between services and between services and clients.

<span id="67ueowGv"></span>
## Learning resources


* [Growth roadmap](https://docs.byteplus.com/en/docs/6569)

* [Getting started](https://docs.byteplus.com/en/docs/apig/Quick_guide)

* [Best practices](https://docs.byteplus.com/en/docs/apig/Best_practices)

* [AI gateway](https://docs.byteplus.com/en/docs/apig/What_is_the_AI_Gateway)

* [FAQs](https://docs.byteplus.com/en/docs/apig/FAQs)
