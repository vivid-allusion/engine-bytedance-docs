---
title: "How do I handle missing HTTP headers in requests?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Header-loss-in-HTTP-requests"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue description

HTTP headers are missing from requests.

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution


* Scenario 1: All headers containing "_" are missing from HTTP requests


Add `underscores_in_headers on` in the configuration file of the nginx container.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">We recommend avoiding <code>_</code> in headers and using <code>-</code> instead.</div>



* Scenario 2: The missing HTTP headers are HTTP\-incompatible ones (for example, Mobile Version)


Add `enable-underscores-in-headers: true` in the ConfigMap for nginx.
