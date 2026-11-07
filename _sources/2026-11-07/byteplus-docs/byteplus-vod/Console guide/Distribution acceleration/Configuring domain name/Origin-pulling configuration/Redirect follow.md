---
title: "Redirect follow"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-redirect-follow"
---

To improve CDN response speed when your origin server uses 301 or 302 redirects, you can enable the redirect follow feature. This guide provides step\-by\-step instructions on how to enable this feature for **Playback**, **Image**, and **Custom\-origin** domain names within the BytePlus VOD console.

<span id="949e86a7"></span>
## Introduction

When a cache node retrieves content from the origin server, if the response status code from the origin server is 301 or 302, it means that the requested content has been redirected to another address. In this case, the cache node will return the response status code to the user's browser. The browser will then send a request to the redirected address. With redirect follow enabled, if the origin server returns a 301/302 status code, the cache node will not return the response code to the user, but will instead directly send a request to the redirected address. After obtaining the content, the cache node will cache it and return it to the user. In the scenario of content redirection, redirect follow can effectively improve the response speed of the CDN to user requests.

Therefore, it is recommended to enable redirect follow if there are 301/302 redirection scenarios on the origin server.

<span id="f536b306"></span>
## Example

Suppose the following scenario:


* The origin server https://www.example.com/image.png is redirected to https://www.test.com/image.png.

* User A and User B both request https://www.example.com/image.png.

* www.example.com is connected to the CDN.


Let's discuss the impact on the request results when redirect follow is disabled and enabled.

<span id="ab19e7f8"></span>
### **Redirect follow disabled**

The request process is as follows:


1. User A requests https://www.example.com/image.png.

2. The cache node requests the file from the origin server.

3. The origin server responds with a 301 or 302 status code, including the redirect address.

4. The cache node returns this status code to User A.

5. User A requests https://www.test.com/image.png.


Since www.test.com is not a domain name connected to the CDN, this request does not go through the CDN. User B will repeat the above steps during the request process.

As a result, the requests from both User A and User B cannot be accelerated.

<span id="55064f15"></span>
### **Redirect follow enabled**

The request process is as follows:


1. User A requests https://www.example.com/image.png.

2. The origin server responds with a 301 or 302 status code, including the redirect address.

3. The cache node requests https://www.test.com/image.png, caches the file, and returns it to User A.


At this point, User A will get the result faster. This is mainly due to the following reasons:


* The process avoids the cache node returning the status code to User A, which would require User A to make the request again.

* The CDN's request to https://www.test.com/image.png will be faster than User A's request to that address.


Then, User B requests https://www.example.com/image.png. Since the file is already cached, the request directly hits the cache. Therefore, the cache node returns the cached file to User B.

As a result, the requests from both User A and User B are accelerated.

<span id="bddeb789"></span>
## Enabling redirect follow


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and navigate to a specific space.

2. Click **Distribution acceleration \> Domain names** on the left navigation bar.

3. Depending on the type of your domain name, click the **Playback domain name**, **Image domain name**, or **Custom\-origin domain name** tab.

4. Find the domain name you want to configure and click the **Configure** button in the **Action** column.

5. Click the **Origin\-pulling configuration** tab.

6. Click the **Modify** button at the bottom of the page.

7. Under **Redirect follow**, switch the **Status** toggle.

8. Click **Save**.
