---
title: "Using API Key to implement gateway authentication"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Using_API_Key_to_Implement_Gateway_Authentication_and_Authorization"
---

The API Gateway uses the Key Auth plugin to implement authentication based on the API Key. This document describes how to configure API Key authentication for the API Gateway.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The Key Auth plugin supports enabling and disabling at the Service and Route levels, with the effective priority of configuration being Route \> Service.

* Once Key Auth is enabled, only accesses with valid consumer credentials pass the authentication.

* Key Auth is generated within the consumer, and a consumer can have at most 5 API Key.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An APIG instance has been created. For details, please refer to [Creating an instance](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

* A service has been created. For details, please refer to [Creating a service](https://docs.byteplus.com/en/docs/apig/Creating_a_service#.5Yib5bu65pyN5Yqh).

* A upstream has been created, this document uses the Vital Kubernetes Engine type as an example. For more details, please refer to [Creating a Vital Kubernetes Engine type upstream](https://docs.byteplus.com/en/docs/apig/Creating_a_Vital_Kubernetes_Engine_type_Upstream).

* A route has been created. For details, please refer to [Creating a route](https://docs.byteplus.com/en/docs/apig/Creating_a_route).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id="2mUJrRxr"></span>
### Step 1: Create a consumer


1. Log in to the [API Gateway console](https://console.byteplus.com/veapig).

2. In the top navigation bar, select the target region.

3. In the left navigation bar, select **Consumer Management \> Consumer List**, then click **Create a consumer**.

4. Click **Confirm** to complete the configuration.


<span id="KqRccmHu"></span>
### Step 2: Generate API Key


1. In the left navigation bar select **consumer management \> consumer list ** .

2. In the consumer list, click the target consumer name to go to the consumer details page.

3. In the credential area, click **Generate API Key**.

4. In the pop\-up dialog, select **Automatically create** API Key credential.

5. Click **Confirm** to generate API Key credential.


<span id="B5mOdJbI"></span>
### Step 3: Enable the Key Auth plugin


1. Log in to the [API Gateway console](https://console.byteplus.com/veapig).

2. In the left navigation bar, select **Plugin management \> Key Auth plugin**, click **Create plugin**, and configure the plugin parameters.

   * **Effectiveness level**: Select **Route level** and configure the plugin instance, Service, and route.

   * **Authentication configuration**: Select **Header**, and set the source to **Authorization**, indicating that the Authorization in the request header carries the API Key credential.

   * **Consumer**: select one of the created consumers.

   * Other configurations remain as default.

3. Click **Confirm** to complete the configuration.


<span id="K4r390HF"></span>
## Result validation

<span id="1GcktZ5b"></span>
### View configuration

After the configuration is complete, in the add\-on list, select **Route Level** tab to view the configured Key Auth add\-on; if the status of the add\-on is **enabled**, it indicates that the add\-on is effective.

<span id="fuh0XulP"></span>
### Credential test

Enable the Key Auth plugin in the APIG instance and generate the API Key credential using the consumer. Only access requests carrying this credential can access the backend Upstream through the APIG.


1. Access the service using the Domain name configured in the APIG instance, when the API Key credential is not carried.


```Bash
curl -H "Host: apig-example.com" http://14.xxx.xxx.xxx
```


The expected result is as follows, indicating that authentication has failed and access to the backend service through the API gateway cannot be achieved.

```Bash
Consumer authentication failed.
```



2. Access the service using the domain name configured in the API gateway instance, when carrying API key credential information.


```Bash
curl -H "Host: apig-example.com" http://14.xxx.xxx.xxx -H "Authorization: Bearer e8cc8b4f-***"
```


The expected result is as follows, indicating that access to the backend service through the API gateway is possible.

```HTML
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
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
