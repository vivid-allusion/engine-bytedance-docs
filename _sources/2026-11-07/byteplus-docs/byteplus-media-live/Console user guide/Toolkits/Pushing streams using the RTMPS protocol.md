---
title: "Pushing streams using the RTMPS protocol"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/pushrtmps"
---

This document describes how to push streaming using RTMPS protocol.

<span id="94235e21"></span>
## Context

Real Time Message Protocol (RTMP) is a network protocol that transmits streaming audio and video between Flash players and servers. RTMP works on top of TCP and uses port 1935 by default. It is a standard, unencrypted real\-time messaging protocol.

RTMPS is a variant of RTMP. It is RTMP that works on top of TLS/SSL. It uses SSL to encrypt network connections at the transport layer. The default port is 443. RTMPS solves the security issues of RTMP very well.

<span id="4faa2200"></span>
## Procedure

<span id="efb9779b"></span>
### **Configure the RTMPS function**

By default, BytePlus MediaLive enables the RTMPS function for the push\-stream domain name. However, if you want the RTMPS function to take effect, you must configure the certificate and HTTPS for the push\-stream domain name first. For how to configure the certificate, refer to [Managing SSL certificate](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-managing-certificates). For how to configure HTTPS, refer to [HTTPS configuration](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-https).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/71d9f2ce91014b28949f804b853d0d89~tplv-goo7wpa0wc-image.image) </span>

<span id="72b61063"></span>
### Push Streaming using RTMPS protocol

You can modify the RTMP address to obtain the RTMPS address and push streaming.


1. Use the **Address generator** to obtain the RTMP push stream address.

2. Change the generated RTMP push stream address protocol header to **RTMPS**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/963694262ccc4a95b165175e5a43d3fc~tplv-goo7wpa0wc-image.image) </span>

3. Enter the RTMPS push stream address into the OBS software to start streaming. The player can follow the normal pull streaming playback process. RTMP, FLV, HLS, and RTM protocols are supported.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/52462e79c96d4196a2ce6aa3a9d8906d~tplv-goo7wpa0wc-image.image) </span>
