---
title: "OAuth2 single sign-on add-on"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/OAuth2_single_sign-on_add-on"
---

The OAuth2 single sign\-on add\-on supports validation of the token or authorization credential in user requests, completes identity validation, and forwards the request after validation to ensure API access security. This document describes how to create the OAuth2 single sign\-on add\-on.

<span id="5sSuDNn3"></span>
## Background information

The OAuth2 single sign\-on add\-on for API Gateway combines the OAuth protocol with single sign\-on (SSO), providing a solution for unified identity authentication across multiple applications through API Gateway, simplifying the login process and ensuring API access security.

<span id="pGbeaN2f"></span>
## Prerequisites


* An API Gateway instance has been created. For operation details, see [Create instance](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

* A service has been created. For operation details, see [Create service](https://docs.byteplus.com/en/docs/apig/Creating_a_service#.5Yib5bu65pyN5Yqh).

* A route has been created. For operation details, see [Create route](https://docs.byteplus.com/en/docs/apig/Creating_a_route).

* (Optional) If you do not obtain the OAuth authentication service address through **OIDC Discovery ** , you need to obtain the authentication server and token server addresses in advance.


<span id="hZMkik0a"></span>
## Procedure


1. Log in to [APIG console](https://console.byteplus.com/veapig).

2. In **Instance management**, select the target instance.

3. In the left navigation bar, click **Add\-on center **  \> **OAuth2 single sign\-on add\-on** \> **Create add\-on**.

4. Configure add\-on rules.

   
   |Parameter |Description |
   |---|---|
   |Scope of effect |Select the scope of effect for the add\-on, including:<br><br><br>* **Service level**: The add\-on takes effect within the service. You need to specify the target instance and target service for it to take effect.<br><br>* **Route level**: The add\-on takes effect within the route. You need to specify the target instance, target service, and target route for it to take effect. |
   |Service |Select the service to which the add\-on belongs. |
   |Associated route |Select the route to which the add\-on belongs. |
   |OAuth authentication |Configure the authentication service address using the following methods.<br><br><br>* Select from Identity:<br><br>* **Obtain via OIDC Discovery address**: Click **Automatically obtain address** to automatically obtain the Discovery URL.<br><br>* **Custom configuration**: Enter the predefined authentication server address and token server address. |
   |Redirect URL |When entering the redirect address after authentication, it must be consistent with the registered address to ensure that the authentication result is securely returned to the client and to prevent the credential from being obtained by an unauthorized address. For example, if the domain name of the gateway is example.com and the redirect path is /callback, you need to enter the complete address https://example.com/callback in the identity authentication platform. |
   |Token validity period |Enter the token validity duration. When the token expires, it must be obtained again to reduce the risk of credential leakage. |
   |Hide credential |After enabling, when API requests are forwarded to the backend, authentication\-related headers will be hidden to avoid plain\-text transmission or display of sensitive data such as keys and tokens during authentication, reducing the risk of information leakage. This feature is disabled by default. |
   |Allow anonymous access |After enabling, supports specifying some interfaces for direct access without OAuth authentication, meeting the direct access needs for public resources (such as the login page). This feature is disabled by default. |
   |Ignore OPTIONS requests |After turning on this feature, OAuth authentication validation for preflight requests (OPTIONS) will be skipped, preventing preflight requests from being blocked in cross\-origin scenarios and ensuring normal cross\-origin processes. This feature is turned off by default. |
   

4. Click **Confirm**.


<span id="uXwdJpex"></span>
## 

&nbsp;
