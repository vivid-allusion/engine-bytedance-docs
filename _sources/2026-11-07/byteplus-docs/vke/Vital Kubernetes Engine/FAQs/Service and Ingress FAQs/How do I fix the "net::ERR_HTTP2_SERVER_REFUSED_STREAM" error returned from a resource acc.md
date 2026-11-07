---
title: "How do I fix the \"net::ERR_HTTP2_SERVER_REFUSED_STREAM\" error returned from a resource access request?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Error-net__ERR_HTTP2_SERVER_REFUSED_STREAM-occurs-when-accessing-resources"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue description

Some resources on a requested webpage fail to load correctly, with the error `net::ERR_HTTP2_SERVER_REFUSED_STREAM` or `net::ERR_FAILED` displayed in the console.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis

The number of concurrent resource requests reaches the maximum HTTP2 stream limit.

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution


* (Recommended) Adjust the value of `http2-max-concurrent-streams` in the ConfigMap to a larger value as needed (default: 128). For details, see [http2-max-concurrent-streams](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/configmap/#http2-max-concurrent-streams).

* Disable HTTP2 support in the ConfigMap by setting `use-http2` to `false`. For details, see [use-http2](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/configmap/#use-http2).
