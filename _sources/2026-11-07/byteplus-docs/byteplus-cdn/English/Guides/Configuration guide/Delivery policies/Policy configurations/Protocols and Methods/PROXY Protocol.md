---
title: "PROXY Protocol"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/proxy-protocol_en-us"
---

<span id="background"></span>
## Background

The PROXY protocol is a network protocol designed to address the issue of a server in a proxy environment being unable to obtain the client's real information. This information includes the client's IP address and port, as well as the destination IP address and port that the client needs to access. When establishing a TCP/UDP connection with the server, the proxy server sends a PROXY protocol header to transmit the client's real information.

<span id="feature-introduction"></span>
## Feature Introduction

The PROXY protocol feature on BytePlus CDN allows the CDN to identify the real client IP address when traffic is forwarded from an upstream proxy. By enabling this feature, which supports both v1 and v2 of the protocol, you can ensure that security policies, such as IP blocklists, are applied correctly based on the original user's IP.

<span id="usage-scenario"></span>
## Usage Scenario

This feature is useful if your architecture includes a proxy, such as BytePlus Global Accelerator (GA), that is deployed in front of the CDN and sends a PROXY protocol header. It allows you to use an IP blocklist/allowlist to control access to the CDN based on the client's real IP address.

<span id="steps"></span>
## Steps


1. Open the **PROXY Protocol** configuration page. For instructions, see [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Set **Status** to **Enabled**.

3. When you are finished, click **Save**.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_40b249edf6c0f1ce986691f08535aec1.png) </span>
