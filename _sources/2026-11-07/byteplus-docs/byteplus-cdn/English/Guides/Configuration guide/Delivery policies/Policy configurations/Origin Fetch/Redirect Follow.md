---
title: "Redirect Follow"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-redirect-follow"
---

To improve content delivery speed when your origin server uses 301 or 302 redirects, you can enable the Redirect Follow feature in BytePlus CDN. This feature instructs the CDN to directly follow the redirect, fetch the content from the new URL, cache it, and return it to the user. This process eliminates an extra round trip for the browser, significantly accelerating content delivery for redirected resources.

<span id="feature-introduction"></span>
## Feature Introduction

When the CDN requests content from the origin server, if the origin server's response status code is 301 or 302, it indicates that the requested content has been redirected to another URL. At this point, the CDN will return the response status code to the user's browser for processing. The browser will then make a request to the redirected URL. After enabling this configuration, if the origin server returns a 301/302 status code, the CDN does not return the response code but instead directly requests the content from the redirected URL. After obtaining the content, the CDN caches it and returns it to the user. In the scenario of content redirection, Redirect Follow can effectively decrease the CDN's response time to user requests.

Therefore, we recommend enabling Redirect Follow if there are 301/302 redirection scenarios on the origin server.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is only effective for user requests using the GET or HEAD methods.</div>


<span id="example"></span>
### Example

Assume the following scenario:


* The origin server redirects requests for `https://www.example.com/image.png` to `https://www.test.com/image.png`.

* User A and User B request `https://www.example.com/image.png` one after another.

* `www.example.com` is integrated with CDN.


The following discusses the impact on the request results when Redirect Follow is disabled and enabled.

**Redirect Follow Disabled**

The request process is as follows:


1. User A requests `https://www.example.com/image.png`.

2. CDN requests the file from the origin.

3. The origin responds with a 301 or 302 status code, including the redirect URL.

4. CDN returns this status code to User A.

5. User A requests `https://www.test.com/image.png`.


Since `www.test.com` is not integrated with CDN, this request does not go through CDN. User B repeats the above steps.

As a result, neither User A nor User B's requests benefit from data transfer acceleration.

**Redirect Follow Enabled**

The request process is as follows:


1. User A requests `https://www.example.com/image.png`.

2. The origin responds with a 301 or 302 status code, including the redirect URL.

3. CDN requests `https://www.test.com/image.png`, caches the file, and returns the file to User A.

   At this point, User A will receive the requested file faster, mainly due to the following reasons:

   * This process avoids the need for the CDN to return a status code and for User A to make a new request.

   * CDN requests `https://www.test.com/image.png` faster than User A can request the URL.


Then, User B requests `https://www.example.com/image.png`. Since the file has been cached, the request hits the cache. Therefore, CDN returns the cached file to User B.

As a result, both User A and User B's requests benefit from data transfer acceleration.

<span id="steps"></span>
## Steps


1. Open the **Redirect Follow** configuration page. For instructions, see [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Set **Status** to **On**.

3. Click **Save** to apply the configuration.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/617abede067f43dd844b1e854f257107~tplv-goo7wpa0wc-image.image) </span>
