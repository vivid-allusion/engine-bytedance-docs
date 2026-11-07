---
title: "Origin protocol"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-origin-protocol"
---

This article describes how to configure origin protocol in the BytePlus VOD console.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Configuring origin protocol applies to <strong>Custom\-origin domain</strong> <strong>name</strong>.</div>


<span id="cee4a502"></span>
## Introduction

When a user requests to access a resource, if the resource is not cached on the CDN node, the CDN will follow the protocol rules you have configured to fetch the resource from the origin server.

<span id="3fc19eaf"></span>
## Configuring origin protocol


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and enter a specific space.

2. Click **Distribution acceleration \> Domain names** on the left navigation bar.

3. Click the **Custom\-origin domain name** tab.

4. Find the domain name you want to configure and click the **Configure** button in the **Action** column.

5. Click the **Origin\-pulling configuration** tab.

6. Click the **Modify** button at the bottom of the page.

7. Under **Origin protocol**, switch the **Status** toggle and select the origin protocol type. The available values for this configuration are as follows:

   * **Same as user request protocol**: The cache node follows the protocol of the user's request for origin fetch.

   * **HTTP**: The cache node uses HTTP for origin fetch.

   * **HTTPS**: The cache node uses HTTPS for origin fetch.

8. Click **Save**.
