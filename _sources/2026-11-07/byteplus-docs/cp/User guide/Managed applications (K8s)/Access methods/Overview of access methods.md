---
title: "Overview of access methods"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Overview_of_access_methods"
---

After the application is deployed, it cannot be accessed directly by other applications. Code Pipeline enables public and private network access to applications using native Kubernetes service discovery. This article introduces the currently supported application publishing methods.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Managed applications deployed only to <strong>Container Service VKE clusters</strong> support the following application publishing methods.</div>



|Application release methods |Description |Documentation Link |
|---|---|---|
|Public NAT for internet endpoint |Use the LoadBalancer mode of the Service to associate a public cloud load balancer (CLB), so that backend instances can be accessed directly via the load balancer's public IP address. |[Add load balancer (public network)](https://docs.byteplus.com/en/docs/cp/Add_a_load_balancer_public_network) |
|VPC internal network access |Use the LoadBalancer mode of Service to associate a private network CLB within a VPC, and directly access the backend instances of the service via the private IP. |[Add load balancing (internal network)](https://docs.byteplus.com/en/docs/cp/Add_intranet_load_balancing) |
|Cluster internal access |When using the ClusterIP mode of Service, a fixed IP address (the ClusterIP) is automatically generated.<br><br>When accessing a ClusterIP from within the cluster, requests are forwarded to the backend instances of the service and are load balanced across these instances. |[Add a service](https://docs.byteplus.com/en/docs/cp/Add_Service) |
|Public/private network access |Use the API Gateway as the traffic entry point for the service to directly access backend instances via public or private network domain names. |[Add an API gateway](https://docs.byteplus.com/en/docs/cp/Add_an_API_gateway) |
