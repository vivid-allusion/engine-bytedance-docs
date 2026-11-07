---
title: "How do I handle an incorrect canary Ingress or its impact on other traffic?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Incorrect-canary-rules-or-rules-affecting-other-traffic"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue description

A canary Ingress has been configured, but traffic is not distributed according to the canary Ingress, or normal Ingress traffic is routed to the canary Service.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis

In the Nginx Ingress Controller, canary rules are not applied to a single Ingress, but to all Ingresses that use the same Service. For details, see [An Ingress with canary will impact all Ingresses with the same Service](https://github.com/kubernetes/ingress-nginx/issues/4667).

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution

For Ingresses that need to enable canary support (including those using service\-match and `canary-*` related annotations), create independent Services (including both production and canary Services) and point them to the original Pods, and then enable canary support for the corresponding Ingress.
