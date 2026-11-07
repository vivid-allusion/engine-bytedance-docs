---
title: "How do I fix the \"SSL_ERROR_RX_RECORD_TOO_LONG\" error for HTTPS access?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/HTTPS-access-error-SSL_ERROR_RX_RECORD_TOO_LONG"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue description

The error "SSL_ERROR_RX_RECORD_TOO_LONG" or "routines:CONNECT_CR_SRVR_HELLO:wrong version number" is returned for an HTTPS request.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis

The HTTPS request was sent to a non\-HTTPS port, for example, an HTTP port.

Common cases are as follows:


* Port 443 of the CLB instance is bound to port 80 of the Ingress Pod.

* Port 443 of the Ingress Controller Service is mapped to port 80 of the Ingress Pod.


<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution

Check the access port and modify the CLB or Service configuration accordingly to ensure that HTTPS requests are routed to the correct port.
