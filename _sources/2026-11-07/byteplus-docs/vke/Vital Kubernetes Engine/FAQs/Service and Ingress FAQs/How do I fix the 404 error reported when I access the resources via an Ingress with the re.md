---
title: "How do I fix the 404 error reported when I access the resources via an Ingress with the rewrite-target setting?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/A-404-error-occurs-when-accessing-resources-after-rewrite-target-is-configured"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue description

After path rewriting is configured by using the `rewrite-target` annotation in the Ingress, some resources on the page fail to load or a white screen appears.

<span id=".6Zeu6aKY5Y6f5Zug"></span>
## Cause

The possible reasons are as follows:


* The `rewrite-target` annotation does not use a regular expression.

* The resource path in the application is hardcoded to the root directory.


<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution


* Check whether `rewrite-target` is used together with a regular expression and capture groups. For details, see [Rewrite](https://kubernetes.github.io/ingress-nginx/examples/rewrite/).

* Check whether the front\-end request accesses the correct path.
