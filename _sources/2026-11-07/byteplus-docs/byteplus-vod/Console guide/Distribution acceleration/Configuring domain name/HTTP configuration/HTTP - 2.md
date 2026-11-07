---
title: "HTTP/2"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-http-2"
---

To improve your content delivery performance, you can enable the HTTP/2 protocol for your domain names in the BytePlus VOD console.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Enabling HTTP/2 applies to <strong>Playback domain name</strong>, <strong>Image domain name</strong>, and <strong>Custom\-origin domain name</strong>.</div>


<span id="0eaa4974"></span>
## Introduction

HTTP/2, originally named HTTP/2.0, is another revision of the HTTP network protocol. It is a binary protocol that supports multiplexed streams, header compression, and stream prioritization. HTTP/2 changes are designed to maintain interoperability and compatibility with HTTP1.1.

HTTP/2 inherently requires the latest and most secure TLS version. The websites that use HTTP/2 usually use HTTPS by default.

<span id="31595572"></span>
## Prerequisite

You have enabled HTTPS for the domain name.

<span id="0ccc74ca"></span>
## Enabling HTTP/2


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and enter a specific space.

2. Click **Distribution acceleration \> Domain names** on the left navigation bar.

3. Depending on the type of your domain name, click the **Playback domain name**, **Image domain name**, or **Custom\-origin domain name** tab.

4. Find the domain name you want to configure and click the **Configure** button in the **Action** column.

5. Click the **HTTP configuration** tab.

6. Click the **Modify** button at the bottom of the page.

7. Under **HTTP/2**, turn on the **Status** toggle.

8. Click **Save**.
