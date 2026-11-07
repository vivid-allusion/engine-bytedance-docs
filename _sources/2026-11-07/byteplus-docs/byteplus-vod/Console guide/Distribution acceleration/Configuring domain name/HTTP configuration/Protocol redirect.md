---
title: "Protocol redirect"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-force-redirect"
---

This article describes how to configure protocol redirect for a domain name in the BytePlus VOD console.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Protocol redirect applies to <strong>Playback domain name</strong>, <strong>Image domain name</strong>, and <strong>Custom\-origin domain name</strong>.</div>


<span id="cee4a502"></span>
## Introduction

Protocol redirect, also known as a protocol\-level redirect or a protocol\-based redirect, refers to the process of redirecting a user's request from one network protocol to another. It involves changing the protocol scheme in the URL that the user has requested.

<span id="3fc19eaf"></span>
## Configuring protocol redirect


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and enter a specific space.

2. Click **Distribution acceleration \> Domain names** on the left navigation bar.

3. Depending on the type of your domain name, click the **Playback domain name**, **Image domain name**, or **Custom\-origin domain name** tab.

4. Find the domain name you want to configure and click the **Configure** button in the **Action** column.

5. Click the **HTTP configuration** tab.

6. Click the **Modify** button at the bottom of the page.

7. Under **Force redirect**, enable the **Status** toggle and configure protocol redirect.

   
   |**Configuration** |**Description** |
   |---|---|
   |Policy |Sets the type of protocol redirect. The possible values for this configuration are:<br><br><br>* **No redirect**: Does not redirect the request.<br><br>* **HTTP to HTTPS**: Redirects the user's HTTP request to HTTPS.<br><br>* **HTTPS to HTTP**: Redirects the user's HTTPS request to HTTP. |
   |Redirect style |Sets the method of redirection. This configuration appears when the **Policy** is **HTTP to HTTPS** or **HTTPS to HTTP**. The possible values for this configuration are:<br><br><br>* **301**: The CDN returns a 301 status code for redirection.<br><br>* **302**: The CDN returns a 302 status code for redirection. |
   

8. Click **Save**.
