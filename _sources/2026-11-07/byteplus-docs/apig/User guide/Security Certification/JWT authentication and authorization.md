---
title: "JWT authentication and authorization"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Enabling_JWT_Authentication"
---

Authenticating the identity information of end users accessing the API gateway. After authentication is enabled, only requests carrying a credential can access the services published by the API Gateway, resulting in a higher level of security. This article introduces how to configure JWT authentication and authorization.

<span id="CwbGOOAU"></span>
## Background Information


* JWT authentication: JSON Web Token (JWT) is a lightweight authentication standard that allows us to use JWT to transmit secure and reliable information between users and servers. Essentially, it is a Token—a compact, URL\-safe method used for transmission between two parties in network communication. For details, refer to [Official documentation](https://jwt.io/introduction).

* The API gateway's credential is currently bound to the service. After JWT authentication is enabled for a service, only requests that carry a JWT token can successfully access resources under the domain name corresponding to the service.


<span id="RUVdKvaI"></span>
## Prerequisites


* An instance has been created. For details, refer to [Create an instance](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

* The service has been created. For details, refer to [Create Service](https://docs.byteplus.com/en/docs/apig/Creating_a_service).


<span id="Ux5p8YiU"></span>
## Procedure

<span id="4yp0unWd"></span>
### Step 1: Enable JWT authentication


1. Log in to the [API Gateway console](https://console.byteplus.com/veapig).

2. In the top navigation bar, choose the target region.

3. In the left navigation bar, select **Route Management \> Service List (Domain name)** . In the service list, click the target service name to enter the service overview page.

4. Click the **authentication** tab.<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_bed24a276e15f775188e757f9efc1ef1.png) </span>Click the icon to open the **Authentication** dialog box.

5. Enable the **credential** switch.

6. Click **Confirm** to complete the configuration.


<span id=".5pON5L2c5q2l6aqk"></span>
### Step 2: Generate a JWT Token

<div data-tips="true" data-tips-type="warning">Caution</div>


<div data-tips="true" data-tips-type="warning">The JWT Token is valid for 7 days from the time it is issued. Please obtain a new JWT Token promptly before it expires to prevent business disruption.</div>



1. In the left navigation bar, select **Route management \> Service list**. In the service list, click the target service name to go to the service overview page.

2. Click **authentication**, and switch to the **authentication** tab.

3. On the **JWT credential** page, click **Generate authentication token** to obtain a JWT Token. You can also view invocation examples in the **Invocation Examples** region.


<span id="FV5WUUIN"></span>
## Result validation

After enabling JWT authentication in the API gateway service and generating the JWT credential. Only access requests carrying this credential can reach the backend Upstream through the API gateway.


1. When you access the Service using the domain name configured in the APIG instance without providing the JWT credential, [consequence].


```Bash
curl -H "Host: apig-example.com" http://14.xxx.xxx.xxx
```


The expected result is as follows: it indicates authentication failure, and you cannot access the backend Service through the API gateway.

```Bash
RBAC: access denied.
```



2. Access the service using the domain name configured in the APIG instance when carrying the JWT credential.


```Bash
curl -H "Host: apig-example.com" http://14.xxx.xxx.xxx -H "Authorization: Bearer eyJhbGciOiJSUzI***"
```


The expected result is as follows, indicating that the backend service can be accessed through the API gateway.

```HTML
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
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


<span id="uG6wVDi1"></span>
## Related Documentation


* [Implement gateway authentication and authorization using API Key](https://docs.byteplus.com/en/docs/apig/Using_API_Key_to_Implement_Gateway_Authentication_and_Authorization)

* [Best practices for migrating from JWT Token to API Key without retaining JWT Token](https://docs.byteplus.com/en/docs/apig/Best_practices_for_migrating_from_JWT_Token_to_API_Key_without_retaining_JWT_Token)

* [Best practices for migrating JWT Token to API Key (retain JWT Token)](https://docs.byteplus.com/en/docs/apig/Best_practices_for_migrating_from_JWT_Token_to_API_Key_retain_JWT_Token)
