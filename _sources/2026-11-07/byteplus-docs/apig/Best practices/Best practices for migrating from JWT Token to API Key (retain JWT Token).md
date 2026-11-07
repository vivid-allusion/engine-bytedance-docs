---
title: "Best practices for migrating from JWT Token to API Key (retain JWT Token)"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Best_practices_for_migrating_from_JWT_Token_to_API_Key_retain_JWT_Token"
---

The API gateway supports authentication and authorization using JWT and API Key. This article explains how to migrate from JWT authentication to API Key authentication on the machine learning platform while retaining the JWT token.

<span id="22gvKr72"></span>
## Precautions


* The Key Auth Plugin can be enabled or disabled at the Service or route resource level. Route\-level Plugin configuration takes precedence over Service\-level configuration.

* Key Auth is generated for the consumer, and each consumer can have up to 5 API Keys.


<span id="9CwS5EwL"></span>
## Prerequisites


* API gateway

   * An APIG instance has been created. For details, refer to [Create an instance](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

   * The Service has been created. For specific operations, refer to [Creating a service](https://docs.byteplus.com/en/docs/apig/Creating_a_service).

   * A route has been added. For details, refer to [Creating a route](https://docs.byteplus.com/en/docs/apig/Creating_a_route).

* Machine learning platform

   * The online Service has already been created, and Service Token validation has been enabled. and use the JWT token from the API gateway for authentication and authorization.


<span id="rzkGOpXj"></span>
## Procedure

<span id="Vcjk1Jd2"></span>
### Step 1: Create a consumer


1. Log in to the [API Gateway console](https://console.byteplus.com/veapig).

2. In the top navigation bar, choose the target region.

3. In the left navigation bar, select **Consumer management \> consumer list**, then click **Create consumers**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">A consumer can be used to distinguish between different departments or business parties.   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you do not need to support multiple departments or business units, just create a consumer.   </div>
   

4. Click **Add** to complete the configuration.


<span id="MGGxJ3rk"></span>
### Step 2: Generate an API Key


1. In the left navigation bar, select **Consumer Management \> Consumer List**.

2. In the consumer list, click the name of the target consumer to view the consumer details page.

3. In the API Key information section on the page, click **Generate API Key**.

4. In the pop\-up dialog, select **Uploaded**, and in the **API Key information** text box, enter the original Token.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Do not include 'Bearer' in the uploaded token information.   </div>
   

5. Click **OK** to generate API Key credential information.


<span id="mMM4KWjS"></span>
### Step 3: Enable Key Auth Plugin


1. Log in to the [API Gateway console](https://console.byteplus.com/veapig).

2. In the left navigation bar, select **Plugin Management \> Key Auth**, click **Create Plugin**, and configure the Plugin parameters.

   * **Effect level**: select **Routing level** and configure the instance, Service, and route to which the Plugin belongs.

   * **Authentication configuration**: select **header** and enter the text  **"Authorization"**  in the textbox on the right side to indicate that API Key will be included in the Authorization header of requests.

   * **Consumer**: Select an existing consumer.

   * Other options can remain as default.

3. Click **Add** to complete the configuration.


<span id="lEDG6shk"></span>
### Step 4: Disable JWT authentication


* Disable JWT Token authentication in the machine learning platform

   * Log in to [the machine learning platform](https://console.byteplus.com/ml-platform).

   * In the left navigation bar, select **Online Services**. In the Service column, select the service for which you want to disable JWT Token authentication. Click the service name to view service details.

   * Select the **API Guide** tab, and click to disable **Service Token Verification**.

* Disable JWT token authentication in the API gateway

   * Log in to the [API Gateway console](https://console.byteplus.com/veapig).

   * In the left navigation bar, select **Service list (Domain name)** . In the service list, select the target service. Click the service name to enter the service details.

   * Select the **Authentication management** tab, go to the **JWT authentication** configuration page, and disable JWT Token authentication.


<span id="5zdZrV1I"></span>
## Result validation

<span id="kg2CUijf"></span>
### View configuration

After configuration is complete, in the Plugin list, select the **Route Level** tab to view the configured Key Auth Plugin. If the Plugin status is **Enabled**, the Plugin is in effect.

<span id="0q3Wl6Jw"></span>
### Certification tests

After enabling the Key Auth Plugin in the APIG instance and generating the API Key credential by using the consumer, you can authenticate API requests using the generated API Key. Only access requests carrying this credential can access the upstream backend through the API gateway.


1. When accessing the Service using the domain name configured in the APIG instance and providing API Key credential information.


```Bash
curl http://scv4***.volceapi.com/doubao -H "Content-Type: application/json" \
-H "Authorization: Bearer 52b06***" \
-d '{
   "stream": true, "stream_options": {"include_usage": true},
   "model": "vemlp-deepseek-r1-enc",
   "messages": [
      {"role":"system","content":"You are Doubao, an AI artificial intelligence assistant developed by ByteDance."},
      {"role":"user","content":"What are the common cruciferous plants?"}
    ]
 }'
```


<span id="EKyrhMub"></span>
## Frequently asked questions

<span id="9ZCxNjjj"></span>
### How to generate multiple API keys


1. In the left navigation bar, select **Consumer Management**, click the target consumer name, and enter the consumer details page.

2. Click **Generate API Key** multiple times to add multiple API Keys to the current consumer.


<span id="cBCgmw2S"></span>
### Invocation error: The JWT is not in the format of Header.Payload.Signature with two dots and three sections.

Please disable JWT Token authentication in the machine learning platform or API gateway.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After disabling JWT Token, if errors still occur when making calls, try enabling and then disabling JWT Token authentication again.</div>



* Disable JWT Token authentication in the machine learning platform

   * Log in to [Machine Learning Platform](https://console.byteplus.com/ml-platform).

   * In the left navigation bar, select **Online Services**, and in the Service column, select the Service for which you want to disable JWT Token authentication. Click the service name to go to the service details.

   * Select the **Call guide** tab, and click to disable **Service Token validation**.

* Disable JWT Token authentication in the API gateway

   * Log in to the [API Gateway console](https://console.byteplus.com/veapig).

   * In the left navigation bar, select **Service list (Domain name)** . In the service list, select the target service, click the service name, and enter the service details.

   * Select the **authentication** tab, and on the JWT authentication configuration page, disable JWT token authentication.
