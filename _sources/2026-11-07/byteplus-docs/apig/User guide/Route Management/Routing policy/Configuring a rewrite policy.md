---
title: "Configuring a rewrite policy"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Configuring_a_rewrite_policy"
---

The API Gateway supports specifying a route to turn on URL rewriting policy. This document explains how to configure a rewrite policy for a route.

<span id="vCYHd62Z"></span>
## Background information

In some application scenarios, the URL provided by the backend service differs from the path configured in the API Gateway rules. By default, the API Gateway directly forwards the access path to the same path on the backend service. If the URL rewriting rules are not configured, due to the difference between the access path and service path, the access will return `404`. At this time, it is necessary to use the URL rewriting rules to rewrite the URL accessed by the service so that it can reach the real path of the backend service.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A route has been created. For details, please refer to [Creating a route](https://docs.byteplus.com/en/docs/apig/Creating_a_route).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [APIG console](https://console.byteplus.com/veapig).

2. In the top navigation bar, select the target region.

3. In the left navigation bar select **Route Management \> Route List**.

4. In the Route List, select the target route, click **Edit** in the **Actions** column.

5. In the **advanced configuration** area of the edit route page, check **Enable** for **URL rewriting** and configure the URL rewriting policy.

   
   |Parameter |Description |
   |---|---|
   |URL rewriting |URL rewriting can rewrite the Path of requests sent by the client to the API gateway, enabling the API gateway to forward a different Path to the backend Service than the one received from the client.<br><br><br>* **Match Path**: Displays the current routing match type and match Path. The match types include equal to, prefix, and regular expression matching.<br><br>* **Rewrite Path**: Enter the target rewrite Path as needed. |
   

   Examples of URL rewriting, as shown in the table below.

   
   |Method |Meaning |Example |
   |---|---|---|
   |Equal to + URL rewriting |Completely modify the original request path. |* Equal to path:`/app/test`<br><br>* URL rewriting path:`/`<br><br><br>The original request Path is`/app/test`, but the Path forwarded to the backend Service is`/`. |
   |Prefix matching + URL rewriting |Modify the original request's path prefix. |* Prefix matching path: `/app/`<br><br>* URL rewriting path:`/`<br><br>   If the original request's Path is `/app/test`, then the Path forwarded to the backend Service is `/test`. |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the matching method uses prefix matching and the path after rewriting the URL ends with<code>/</code>If it ends with, the prefix matching path also needs to be modified to end with<code>/</code>Ends with.   </div>
   

6. Click **Confirm** to complete the configuration.


<span id="UBhMBBV8"></span>
## Result validation

In the back\-end Service of the APIG instance, deploy an Nginx server and specify the path as`/`when the path configured in the route policy is `/demo`, and URL rewriting rules are not configured, due to the inconsistent paths, directly accessing the Service through the API gateway will return `404`.

```Bash
curl -H "Host: apig-example.com" http://180.xxx.xxx.xxx/demo
```


The expected response result is as follows:

```HTML
<html>
<head><title>404 Not Found</title></head>
<body>
<center><h1>404 Not Found</h1></center>
<hr><center>nginx</center>
</body>
</html>
```


After activating and configuring URL rewriting rules in the routing policy of the API gateway, use the following command to access the Service.

```Bash
curl -H "Host: apig-example.com" http://180.xxx.xxx.xxx/demo
```


The expected output is as follows, the rewriting policy has changed the path `/demo` in the request to`/`, allowing correct access to the backend Service.

```HTML
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>html { color-scheme: light dark; }
body { width: 35em; margin:0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```


&nbsp;

&nbsp;

&nbsp;

&nbsp;
