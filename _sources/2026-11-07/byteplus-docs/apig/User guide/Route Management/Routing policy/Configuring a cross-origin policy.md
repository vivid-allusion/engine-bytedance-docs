---
title: "Configuring a cross-origin policy"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Configuring_a_cross-origin_policy"
---

API Gateway supports cross\-origin policy configuration for routes, and you can enable cross\-origin for specific routes. This article describes how to configure a cross\-origin policy for a route.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Background Information

In the HTTP protocol, Cross\-Origin refers to a restriction mechanism implemented by browsers for security reasons, restricting resource access between different origins (Origin). You can enable Cross\-Origin Resource Sharing (CORS) in the routes of the API Gateway, allowing cross\-origin access, thereby enabling secure cross\-origin data transmission.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A route has been created. For more details, please refer to [Creating a route](https://docs.byteplus.com/en/docs/apig/Creating_a_route).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [API Gateway console](https://console.byteplus.com/veapig).

2. In the top navigation bar, select the target region.

3. In the left navigation bar select **Route Management \> Route List**.

4. In the Route List, select the target route, click **Edit** in the **Actions** column.

5. In the **Advanced Configuration** region of the edit route page, check **Enable** after **cross\-origin** to enable the cross\-origin access policy.

6. Click **Confirm** to complete the configuration.


<span id="wcGPvyU6"></span>
## Result validation

After the configuration, you can use the following command to verify whether the cross\-origin policy is effective.

```Bash
curl -I -H "Origin: http://test.com" -H 'Host: apig-example.com' -X OPTIONS http://180.xxx.xxx.xxx
```


The expected response result is as follows. You can see that the `access-control-allow-origin` field has been added to the response header.

```HTML
HTTP/1.1 200 OK
server: istio-envoy
date: Fri, 28 Feb 2025 03:57:34 GMT
content-type: text/html
content-length: 615
last-modified: Tue, 02 Nov 2021 14:49:22 GMT
etag: "61814ff2-267"
accept-ranges: bytes
x-envoy-upstream-service-time: 1
access-control-allow-origin: http://test.com
```


&nbsp;
