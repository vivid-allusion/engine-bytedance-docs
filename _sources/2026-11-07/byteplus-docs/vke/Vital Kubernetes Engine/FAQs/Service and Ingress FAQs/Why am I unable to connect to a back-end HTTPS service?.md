---
title: "Why am I unable to connect to a back-end HTTPS service?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Cannot-connect-to-back-end-HTTPS-Services"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue description

Accessing the back\-end HTTPS service via an Ingress fails with the "The plain HTTP request was sent to HTTPS port" error.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis

The Ingress Controller uses the default HTTP protocol to send requests to back\-end pods.

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution

Configure the annotation `nginx.ingress.kubernetes.io/backend-protocol:"HTTPS"` in the Ingress resource to change the request protocol from the Ingress Controller to back\-end pods to HTTPS.
