---
title: "Origin request timeout"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-origin-request-time-out"
---

To balance content delivery performance with your origin server's stability, you can customize the origin request timeout in BytePlus VOD.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Origin request time\-out applies to <strong>Custom\-origin domain name</strong>.</div>


<span id="2364fcee"></span>
## Introduction

In BytePlus VOD, the default timeout configuration is as follows:


* When the CDN sends a TCP request to establish a connection with the origin server, the TCP request timeout is 2 seconds.

* When the CDN sends an HTTP request to retrieve content from the origin server, the HTTP request timeout is 60 seconds.


In some cases, you may need to set a reasonable timeout based on the network conditions and the origin server's data processing capability. Before setting the timeout, please note the following:


* If you set the timeout too short, origin requests may fail frequently. This may be due to poor network quality.

* If you set the timeout too long, origin requests will continue to occupy the origin server's connections, affecting the server's service capacity.


<span id="3b8d8fbf"></span>
## Configuring the origin request timeout


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and enter a specific space.

2. Click **Distribution acceleration \> Domain names** on the left navigation bar.

3. Click the **Custom\-origin domain name** tab.

4. Find the domain name you want to configure and click the **Configure** button in the **Action** column.

5. Click the **Origin\-pulling configuration** tab.

6. Click the **Modify** button at the bottom of the page.

7. Under Origin request time\-out, enable the Status toggle and set the timeouts for TCP and HTTP respectively. The unit of timeout is seconds.

   * For TCP timeout, you can set a time range of 2\-60 seconds.

   * For HTTP timeout, you can set a time range of 5\-60 seconds.

8. Click **Save**.
