---
title: "How do I fix a cross-origin Ingress access failure?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/CORS-configuration-for-an-Ingress-becomes-invalid"
---

## Issue description

The cross\-origin access configuration for Ingress\-nginx in the VKE cluster did not take effect.

## Solution

To enable cross\-origin access, add the following settings to the annotations section of the Ingress.

```yaml
nginx.ingress.kubernetes.io/enable-cors: "true"
nginx.ingress.kubernetes.io/cors-allow-methods: "PUT, GET, POST, DELETE, PATCH, OPTIONS"
nginx.ingress.kubernetes.io/cors-allow-credentials: "true"
```

> **Warning**

> Check whether the request method is included in the allowed methods in the CORS configuration and whether `nginx.ingress.kubernetes.io/cors-allow-origin: "*"` is configured. If the configuration is set to the default value `"*"`, this may also cause the issue. In this case, delete this annotation.
