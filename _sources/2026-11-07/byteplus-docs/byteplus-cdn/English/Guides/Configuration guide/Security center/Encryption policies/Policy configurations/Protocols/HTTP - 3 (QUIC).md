---
title: "HTTP/3 (QUIC)"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-quic_1"
---

This document introduces BytePlus CDN's support for HTTP/3 and QUIC protocols.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Due to conflicting mechanisms, HTTP/3 (QUIC) and WebSocket cannot be enabled simultaneously.</div>


<span id="overview"></span>
## Overview

The HTTP/3 (QUIC) feature from BytePlus CDN enables your services to handle requests using the next\-generation HTTP/3 and QUIC protocols. The QUIC protocols supported by CDN include the following:


* Google QUIC (gQUIC): The supported gQUIC versions are Q043, Q046, and Q050.

* IETF QUIC: IETF QUIC is the transport layer protocol used by HTTP/3.


In summary, CDN supports HTTP/3 and specific versions of gQUIC.

Enabling the HTTP/3 (QUIC) feature allows the CDN to handle user requests using these protocols.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">CDN supports connection reuse for QUIC requests. When a CDN node receives a QUIC request for a domain with HTTPS enabled, it can reuse existing connections from other QUIC requests on that node, provided they use the same certificate.</div>


<span id="introduction-to-http-3"></span>
## Introduction to HTTP/3

HTTP/3, based on IETF QUIC, is the latest version of the HTTP protocol and offers the following advantages:


* **Low Latency**: QUIC integrates key exchange and supported protocols into the initial handshake process. When the server responds to a client connection, the response packet contains data needed for data encryption. The client can use this data to generate keys to encrypt packets that need to be sent. With HTTPS connections, a TCP handshake is required first between the client and the server, followed by a TLS handshake to establish a secure connection.

* **Improved Performance in Network Switching**: QUIC includes a unique connection identifier, which uniquely identifies the connection between the client and the server. Even if the client's IP address changes, the client only needs to send a packet with this ID to resume the connection with the server. For TCP, if the client's IP address changes, the existing TCP connection will time out, and the client must undergo a time\-consuming process to re\-establish the connection.

* **Robust Performance in Weak Network Conditions**: QUIC is based on UDP. Even in cases of packet loss and significant network latency, QUIC can still ensure service availability.


<span id="prerequisites"></span>
### Prerequisites

To enable this configuration, your domain must have HTTPS Encryption Service enabled.

<span id="steps"></span>
### Steps


1. Open the **HTTP/3 (QUIC)**  configuration page. For instructions, see [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Set **Status** to **Enabled**.

3. After completing the configuration, click **Save**.


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260806105134-641939731487.png) </span>
