---
title: "Why does the \"lb is provisioning\" event occur when I configure a Layer 4 LoadBalancer via Annotation?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Event-lb-is-provisioning-occurs-when-configuring-a-layer-4-load-balancer-by-using-annotations"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue description

The "Error ensuring load balancer: lb is provisioning" event is reported during an attempt to configure a Layer 4 Load Balancer.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis

This event indicates that the CLB instance is still being created, and the service is temporarily not available.

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution

Under normal circumstances, this event only lasts for a short time (within 30 seconds). If this event occurs frequently or persists for a longer time, [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000210).
