---
title: "Traffic path description"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Product-Overview-04"
---

The following figure displays the traffic path for Classic Load Balancer (CLB) access traffic.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bea16cf532e483a41cd56dcb93fd15a6.png) </span>

CLB access request processing flow:


* Layer\-4 protocol (TCP/UDP) access requests from users are directly forwarded to backend servers by servers in the Layer\-4 cluster based on routing algorithms.

* The Layer\-7 (HTTP/HTTPS) access requests from users are first distributed by servers in the Layer\-4 cluster to servers in the Layer\-7 CLB cluster, and then forwarded to backend servers based on forwarding policies.

* HTTPS access requests require certificate verification and packet decryption within the Layer\-7 cluster before being finally distributed to backend servers via the HTTP protocol.

* Layer\-7 (HTTP/HTTPS) access requests use TCP protocol for traffic forwarding in the Layer\-4 cluster.
