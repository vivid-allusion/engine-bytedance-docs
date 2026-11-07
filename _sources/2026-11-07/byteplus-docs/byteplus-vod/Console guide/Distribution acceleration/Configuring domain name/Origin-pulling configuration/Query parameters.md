---
title: "Query parameters"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-query-parameters"
---

To control how the CDN handles URL parameters when fetching content from your origin server, you can configure the query parameter settings for your accelerated domain names.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Configuring HTTP request headers applies to <strong>Custom\-origin domain name</strong>.</div>


<span id="b288ad25"></span>
## Introduction

By default, when the CDN retrieves content from the origin server, the parameters in the origin request URL are the same as those in the user's request URL. For example, if the user requests a file with the URL `http://www.example.com/image.png?version=1`, the URL includes the `version` parameter. When the CDN retrieves the file from the origin server, it also includes this parameter.

If the parameters on both sides are not consistent in your business scenario, you can configure query parameters for the origin.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, BytePlus VOD only supports two settings for query parameters during origin requests: "Include All" and "Include None". These settings apply to all files on the origin server.</div>


<span id="3d52b4c5"></span>
## Configuring query parameters


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and enter a specific space.

2. Click **Distribution acceleration \> Domain names** on the left navigation bar.

3. Click the **Custom\-origin domain name** tab.

4. Find the domain name you want to configure and click the **Configure** button in the **Action** column.

5. Click the **Origin\-pulling configuration** tab.

6. Click the **Modify** button at the bottom of the page.

7. Under **Query parameters**, switch the **Status** toggle and select the **Action**.

   * Keep all parameters

   * Delete all parameters


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You cannot currently modify the default <strong>Rule type</strong> and <strong>Rule</strong> settings. The default settings apply to all files.</div>
