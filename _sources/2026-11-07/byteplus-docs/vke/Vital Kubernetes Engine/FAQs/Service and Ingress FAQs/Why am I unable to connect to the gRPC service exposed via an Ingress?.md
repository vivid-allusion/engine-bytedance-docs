---
title: "Why am I unable to connect to the gRPC service exposed via an Ingress?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Cannot-connect-to-a-gRPC-Service-exposed-through-an-Ingress"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue description

The gRPC service exposed by an Ingress is inaccessible.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis


* A valid back\-end protocol was not specified in the Ingress Annotation.

* The gRPC service can be accessed only by using a TLS port.


<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution


* In the corresponding Ingress, add `nginx.ingress.kubernetes.io/backend-protocol:"GRPC"` Annotation.

* Confirm that the client sends requests over the TLS port and that the traffic is encrypted.
