---
title: "Origin Keep-Alive"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/origin-preconnection_en-us"
---

This document describes how to configure Origin Keep\-Alive in BytePlus CDN.

<span id="overview"></span>
## Overview

By default, CDN edge nodes do not reuse TCP connections to your origin. Each origin request therefore requires a new TCP connection; HTTPS origin requests also require a new TLS handshake.

When enabled, Origin Keep\-Alive allows a CDN edge node to keep a TCP connection to the origin open after completing an origin request. Later origin requests can reuse that connection, eliminating the need to establish a new TCP connection. For HTTPS origin requests, reuse also avoids an additional TLS handshake and reduces connection\-setup latency.

<span id="keep-alive-timeout"></span>
## Keep\-Alive Timeout

The default keep\-alive timeout is `3600` seconds. You cannot change this value in the BytePlus CDN console. To request a different timeout, [submit a support ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000735).

CDN edge nodes reuse the connection for subsequent origin requests as long as it remains open and its idle time does not exceed the keep\-alive timeout. The keep\-alive timer resets whenever the connection is reused. If the connection times out, is closed by the origin, or encounters an error, the CDN edge node establishes a new connection for the next origin request.

<span id="use-cases"></span>
## Use Cases

Origin Keep\-Alive is recommended for the following scenarios:


* CDN edge nodes frequently send origin requests to your origin, and you want to reduce the overhead of repeatedly establishing TCP connections and, for HTTPS, performing TLS handshakes. This feature is particularly effective when origin requests arrive in intermittent batches and the interval between batches falls within the keep\-alive timeout. For example, when retrieving files from an object storage origin, connections established for one batch can be reused by a later batch.

* Your origin is geographically distant from CDN edge nodes, resulting in high TCP or TLS connection\-setup latency.

* You serve dynamic content or API responses that cannot be fully cached at the edge and are sensitive to origin latency.


For domains with infrequent origin requests, the benefit of connection reuse may be limited.

<span id="notes"></span>
## Notes


* When multiple CDN edge nodes send origin requests to the same origin, each node may maintain persistent TCP connections for up to the keep\-alive timeout. This can increase the number of concurrent connections at the origin. Ensure that your origin has sufficient connection capacity.

* Set the idle connection timeout on your origin to at least `3600` seconds. Otherwise, the origin might close an idle connection before the CDN keep\-alive timeout expires, requiring the CDN edge node to establish a new connection for a subsequent origin request.

* This feature optimizes connection establishment between CDN edge nodes and the origin. It does not affect connections between clients and CDN edge nodes.


<span id="steps"></span>
## Steps


1. Open the **Origin Keep\-Alive** configuration page. For the steps, see [Domain Management](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Set **Status** to Enabled.


After the configuration takes effect, a CDN edge node establishes a persistent TCP connection to the origin when it first sends an origin request. Subsequent origin requests reuse the connection while it remains open and its idle time has not exceeded the keep\-alive timeout.

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260814035749-541726008379.png) </span>
