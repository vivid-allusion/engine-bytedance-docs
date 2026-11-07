---
title: "Best practices for migrating from JWT Token to API Key (without retaining JWT Token)"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Best_practices_for_migrating_from_JWT_Token_to_API_Key_without_retaining_JWT_Token"
---

The API gateway supports authentication and authorization using JWT and API Key. This article describes how to migrate from JWT authentication to API Key authentication on the machine learning platform without retaining the JWT token.

<span id="wNcg9Uqp"></span>
## Precautions


* The Key Auth Plugin can be enabled or disabled at the Service or Route level. Route\-level configuration takes precedence over Service\-level configuration.

* Key Auth is generated within the consumer, and a consumer supports up to 5 API Keys.

* After migrating from JWT authentication to API Key authentication, you must also update the authentication token on your client to ensure correct access to the Service.


<span id="UXozLUMm"></span>
## Prerequisites


* API gateway

   * An APIG instance has been created. For details, refer to [Create instance](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

   * The Service has been created. For specific operations, refer to [Create a service](https://docs.byteplus.com/en/docs/apig/Creating_a_service).

   * Route added. For more information, refer to [Creating a route](https://docs.byteplus.com/en/docs/apig/Creating_a_route).

* Machine learning platform

   * The online service has been created, and Service Token validation has been enabled. and use the API gateway's JWT token to authenticate and authorize.


<span id="68MN4l2E"></span>
## Procedure

<span id="N7al8AAv"></span>
### Step 1: Disable JWT authentication

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">It is not recommended to use JWT authentication and API\-Key authentication at the same time. Please disable JWT authentication first.</div>



* Disable JWT Token authentication in the machine learning platform

   * Log in to [Machine Learning Platform](https://console.byteplus.com/ml-platform).

   * In the left navigation bar, select **Online Services**, and in the service column, select the service for which you need to disable JWT Token authentication. Click the service name to enter the service details.

   * Select the **Invocation Guide** tab, then click to disable **Service Token validation**.

* Disable JWT Token authentication in the API Gateway.

   * Log in to the [API Gateway console](https://console.byteplus.com/veapig).

   * In the left navigation bar, select **Service list (Domain name)** . In the service list, select the target service. Click the service name to enter the service details.

   * Select the **authentication** tab. On the **JWT authentication** configuration page, disable JWT Token authentication.


<span id="N7al8AAv"></span>
### Step 2: Create a consumer


1. Log in to the [API Gateway console](https://console.byteplus.com/veapig).

2. In the top navigation bar, choose the target region.

3. In the left navigation bar, select **Consumer Management \> Consumer List**, and click **Create Consumer**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The consumer can be used to distinguish between different departments or business units.   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you only need to serve a single department or business unit, just create one consumer.   </div>
   

4. Click **OK** to complete the configuration.


<span id="s4SjPwrQ"></span>
### Step 3: Generate an API Key


1. In the left navigation bar, select **Consumer management \> Consumer list**.

2. In the consumer list, click the target consumer name to open the consumer details page.

3. In the API Key information section on the page, click **Generate API Key**.

4. In the pop\-up dialog box, select **Automatically create**. 

5. Click **Confirm** to generate API Key credential information.


<span id="4ugvXWLX"></span>
### Step 4: Enable Key Auth Plugin


1. Log in to the [API Gateway console](https://console.byteplus.com/veapig).

2. In the left navigation bar, select **Plugin Management \> Key Auth Plugin**, click **Create Plugin**, and configure Plugin parameters.

   * **Effect level**: select **route level** and configure the instance, Service, and route to which the Plugin belongs.

   * **Authentication configuration**: select **header** and enter the text  **"Authorization"**  in the textbox on the right side to indicate that API Key will be included in the Authorization header of requests.

   * **Consumer**: Select an existing consumer.

   * Other options can remain as default.

3. Click **Add** to complete the configuration.


<span id="NCFajO0D"></span>
## Result validation

<span id="vYc1kMCB"></span>
### View configurations

After completing the configuration, in the Plugin list, select the **Route Level** tab to view the configured Key Auth Plugin. If the Plugin status is **Enabled**, the Plugin is enabled.

<span id="UFExCixI"></span>
### Certification testing

After enabling the Key Auth Plugin in the APIG instance and generating the API Key credential using a consumer. Access requests carrying only this credential can reach the backend Upstream through the API gateway.


1. When accessing the service using the domain name configured in the APIG instance, while also providing the API Key credential.


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


<span id="ln3qDwv6"></span>
## Frequently asked questions

<span id="7ToVgb9k"></span>
### How to generate multiple API Keys


1. In the navigation bar on the left, select Consumer List, then click the name of the target consumer to go to the consumer details page **.** 

2. Click **Generate API Key** multiple times to add multiple API Keys to the current consumer.


<span id="3CjGa22O"></span>
### An error occurred during the call: JWT is not in the form of Header.Payload.Signature with two dots and 3 sections

Please disable JWT Token authentication in the machine learning platform or the API gateway.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After disabling JWT Token authentication, if errors still occur when making calls, try enabling and then disabling JWT Token authentication again.</div>



* Disable JWT Token authentication in the machine learning platform

   * Log in to the [machine learning platform](https://console.byteplus.com/ml-platform).

   * In the left navigation bar, select **Online Services**, then select the service in the service column for which you want to disable JWT Token authentication. Click the service name to enter the service details.

   * Select the **Invocation Guide** tab, click Close **Service Token Validation**.

* Disable JWT token authentication in the API gateway.

   * Log in to the [API Gateway console](https://console.byteplus.com/veapig).

   * In the left navigation bar, select **service list (Domain name)** . In the service list, select the target service. Click the service name to view the service details.

   * Select the **authentication** tab, and on the JWT authentication configuration page, disable JWT Token authentication.
