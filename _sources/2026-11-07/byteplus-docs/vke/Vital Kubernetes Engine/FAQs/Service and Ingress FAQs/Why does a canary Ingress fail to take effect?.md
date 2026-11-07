---
title: "Why does a canary Ingress fail to take effect?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Canary-rules-do-not-take-effect"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue description

A canary Ingress is configured in the cluster, but the canary Ingress does not take effect.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis

Possible reasons are as follows:


* You specified `canary-*` related annotations, but did not specify the `nginx.ingress.kubernetes.io/canary: "true"` annotation.

* For Nginx Ingress Controller versions earlier than 0.47.0, if you use `canary-* `annotations, you need to specify the service domain name in the Host field of the Ingress configuration..


<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution

Specify `nginx.ingress.kubernetes.io/canary: "true"` or update the Host field in the Ingress as needed.
