---
title: "How do I  fix the problem of not retaining source IP addresses in Ingress pods?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Cannot-retain-source-IP-addresses-in-Ingress-pods"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue description

The source IP address (real client IP address) cannot be retained in the Ingress pod. The displayed IP address is that of the node, an IP address in the `100.xxx.xxx.xxx` segment, or another address.

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution


* Check whether the Nginx Ingress Controller has enabled the setting to retain the source IP address. If not, you can add `enable-real-ip: "true"` in the Nginx Ingress Controller configuration file to enable this setting.

* Confirm whether the Nginx Ingress Controller is fronted by an upstream load balancer and whether the `X-Forwarded-For `request header is configured.
