---
title: "Why does a \"loadbalancer for service not found\" event occur when I configure Layer 4 load balancing using Annotation?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Event-loadbalancer-for-service-not-found-occurs-when-configuring-a-layer-4-load-balancer"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue description

In the process of configuring Layer 4 load balancing using Annotation, the "loadbalancer for service not found, but the status.LoadBalancer.Ingress not nil, it may be caused by lb deleted" event is reported.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis

This event indicates that the Service has already been associated with a CLB instance. Possible reasons are as follows:


* `service.beta.kubernetes.io/system-volcengine-loadbalancer-create-response-id` or `service.beta.kubernetes.io/volcengine-loadbalancer-id` was changed to a non\-existent CLB instance ID.

* The CLB instance was accidentally deleted.


<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution


1. Check whether the CLB instance ID specified in `service.beta.kubernetes.io/system-volcengine-loadbalancer-create-response-id` or `service.beta.kubernetes.io/volcengine-loadbalancer-id` exists.

2. If the CLB instance does not exist or was accidentally deleted, log in to the [Load Balancer console](https://console.byteplus.com/clb) to re\-create the CLB instance, or directly use the load balancer created by Annotation and create a LoadBalancer Service. For details, see [Configuring CLB LoadBalancer Services by using annotations](https://docs.byteplus.com/en/docs/vke/Configuring-a-LoadBalancer-Service-using-annotations).
