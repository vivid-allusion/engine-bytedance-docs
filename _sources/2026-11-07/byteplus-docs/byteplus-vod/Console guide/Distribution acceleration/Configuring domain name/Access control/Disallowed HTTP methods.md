---
title: "Disallowed HTTP methods"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-disallowed-http-methods"
---

This article describes how to configure disallowed HTTP methods in the BytePlus VOD console.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The disallowed HTTP methods apply to <strong>Custom\-origin domain</strong> <strong>name</strong>.</div>


<span id="14e87438"></span>
## Introduction

The HTTP request method specifies how the resource is requested. Different request methods have specific usage scenarios. By default, BytePlus VOD allows requests to access accelerated domain names using the following methods.


* GET

* POST

* DELETE

* PUT

* HEAD


You can configure disallowed HTTP request methods according to your needs. If a user request uses a disallowed HTTP request method, BytePlus VOD rejects the request and returns a 405 response status code.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">It is not recommended that you disallow GET, HEAD, and POST. These are the commonly used request methods. If GET and POST are disallowed, you will not be able to use OpenAPI to access the BytePlus VOD service.</div>


<span id="82569462"></span>
## Configuring disallowed HTTP methods


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and enter a specific space.

2. Click **Distribution acceleration \> Domain names** on the left navigation bar.

3. Click the **Custom\-origin domain name** tab.

4. Find the domain name you want to configure and click the **Configure** button in the **Action** column.

5. Click the **Access control** tab.

6. Click the **Modify** button at the bottom of the page.

7. Under **Disallowed HTTP methods**, switch the **Status** toggle and select the HTTP request methods that you want to disallow.

8. Click **Save**.
