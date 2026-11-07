---
title: "External authentication and authorization"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Custom_authentication_and_authorization"
---

API Gateway supports connecting to user\-built external authentication and authorization services, making it easier for users to unify their authentication methods. This article describes how to configure external authentication and authorization in API Gateway.

<span id="ddeDwTYn"></span>
## Background

Businesses deployed in the cloud typically protect the communication security of externally exposed interfaces based on the credential information (that is, Token) carried in client requests. When the Token uses a user\-defined format, the business server must additionally access the authentication service after receiving the request to complete the authentication process, ensuring the legitimacy of client access. To meet this scenario, API Gateway supports authentication based on user\-built authentication and authorization services. 


1. The client initiates an authentication request to the gateway.

2. The gateway directly forwards the authentication request to the user\-built authentication service. The authentication service supports deployment in Vital Kubernetes Engine cluster, ECS instance, veFaaS, or by specifying a fixed IP address.

3. The authentication service reads the verification information in the request for validation. After successful validation, it returns credential information (Token) to the gateway, which then passes it back to the client.

4. The client initiates a business request to the gateway, carrying the Token issued after successful authentication in the previous step.

5. The gateway forms a new request message by extracting the original business request's path (including query parameters), HTTP method (GET, POST, and so on), and Token, and initiates an authorization request to the integrated user\-built authorization service. You can configure the HTTP header location of the authentication Token in the API Gateway console ( Authorization, Cookie, or custom), and you can also specify authorization request headers and response headers as needed.

6. After receiving the authorization request, the authentication service completes a validity check based on the Token and returns `2xx` or an error status code.

   * If the authentication service returns a status code of `2xx`, it indicates that the Token is valid and has permission to access the specified backend resources. The gateway continues to forward the original business request to the protected Backend service, and after receiving the business response, forwards it to the client again, completing access to the protected business Service.

   * If the authentication Service returns an abnormal HTTP status code, this indicates that the Token is invalid or the Token does not have permission to access the specified Backend Resources. The gateway directly returns the response from the authentication Service to the client, resulting in access failure.


<span id="ddeDwTYn"></span>
## Prerequisites


* The Instance has been created. For details, see [Create instance](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

* A self\-built authentication and authorization server has been deployed, and the authentication server is configured as Upstream in the API Gateway. For details, see [Upstream Management](https://docs.byteplus.com/en/docs/apig/Upstream_Management).


<span id="AyamhzTh"></span>
## Usage limits


* Self\-built authentication and authorization currently only take effect at the Instance level.

* The cloud resources where the self\-built authentication and authorization Service resides (for example, VKE cluster, ECS Instance, and more) must be in the same VPC as the API Gateway Instance.


<span id="hFSwy7SA"></span>
## Procedure


1. Log in to [APIG console](https://console.byteplus.com/veapig).

2. Select the target region in the top navigation bar.

3. In the left navigation bar, choose **add\-on center,**  select **external authentication add\-on** from the add\-on list, click **Create add\-on**, and configure authentication and authorization information.

   
   |Parameter |Description |
   |---|---|
   |Effective level |Choose the effectiveness level of the external authentication add\-on. Currently, only **instance level** is supported. |
   |Instance |Choose the APIG instance where the external authentication feature will take effect. |
   |Description |Supports choosing whether to edit notes content based on business needs, such as specifying the purpose of the add\-on, for easier identification in the future. |
   |Authentication location |Configure the request header that contains the credential, for example, `Authorization`. |
   |Authentication service address |Configure the authentication server address and authentication method, including:<br><br><br>* **Upstream type**: Choose the backend type of the authentication server. Support **VKE**, **cloud server**, **veFaaS**, and **fixed IP**.<br><br>* **Upstream**: Choose the specific Upstream where the authentication server is located.<br><br>* **Authentication address**: Configure the path used for authentication, for example `/`.<br><br>* **Authentication method**: Configure the HTTP Method used for authentication. Support **GET** or **POST**.<br><br>* **Timeout time**: Configure the maximum wait time for the authentication Service to return the response result, unit: s. If this time is exceeded and the authentication Service has not returned, authentication will fail.<br><br>* **Authentication method**: Configure the authentication method, including:<br><br>   * **Disable**: Disable authentication.<br><br>   * **API Key**: Use API Key for authentication. When this option is selected, you need to specify the location of the API Key (**request header** or **request parameter**) and the value of the API Key.<br><br>   * **Signature**: Use signature for authentication. When this option is selected, you need to configure the signature's **Service**, **Access Key**, and **Secret Key**. |
   |Forward request header |Configure additional client request headers to be carried in the authentication request message. The authentication request message will carry this header and send it to the authentication service.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The client's <code>Host</code>, <code>Method</code>, <code>Path</code>, and <code>Content-Length</code> request headers are added to the authentication request message by default, so you do not need to add them manually.</div><br> |
   |Add request header |In the configuration, you need to extract request headers from the response headers returned by the authentication service and forward them to Upstream. |
   |Ignore preflight requests |Configure whether to ignore preflight requests (Options).<br><br><br>* **Enable**: The gateway will ignore preflight requests (Options), will not perform authentication, and will allow them through directly.<br><br>* **Disable**: The gateway will not ignore preflight requests and will perform external authentication as usual. |
   |Allow anonymous access |Configure whether to allow anonymous access, that is, whether to allow requests that do not include credential.<br><br><br>* **Enable**: Allow anonymous access. The Gateway will directly allow requests without credential.<br><br>* **Disable**: Prohibit anonymous access. The Gateway will intercept and block requests without credential. |
   |Hide credential |Configure whether to hide the credential passed from the frontend when the gateway forwards requests to the backend service (Upstream).<br><br><br>* **Enable**: Hide the credential from the backend. The gateway will remove the relevant credential (such as the Authorization header) before forwarding the request.<br><br>* **Disable**: Do not hide the credential. The gateway will directly pass the original credential to the backend service. |
   |Re\-routing |Whether to reroute according to the authentication response header added in the client request.<br><br><br>* **Enable**: Requests are re\-routed according to the Method, Path, request headers, request parameters, and added authentication response headers in the original client request.<br><br>* **Disable**: Routing is performed only based on the Method, Path, request headers, and request parameters in the original client request. |
   |Downgrade mode |Whether to use authentication downgrade mode.<br><br><br>* **Enable**: When the authentication Service server is not available, the system will automatically skip the authentication process. At this time, the client can access the backend business without authentication.<br><br>* **Disable**: When the authentication Service server is not available, the system will not skip the authentication process. At this time, since authentication cannot be completed, the client cannot access the corresponding backend business. |
   |Matching rules |Configure authentication matching rules, including:<br><br><br>* **blocklist**: Domain names and paths matched in the blocklist do not require authentication. All other domain names or paths require authentication.<br><br>* **allowlist**: Domain names and paths matched in the allowlist require authentication. All other domain names or paths do not require authentication.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Click <strong>Add</strong> to configure multiple matching rules.</div><br><br><br><br>* **Domain name**: Configure the domain name information in the matching rules.<br><br>* **path**: Configure the path information in the matching rules. Supports **prefix match** or **exact matching**. |
   

4. Click **Confirm**.


<span id="crEZAagP"></span>
## Validating results

<span id="a3YqrwlK"></span>
### Viewing settings

After the configuration is complete, a new add\-on record will be generated in the external authentication add\-on list. The add\-on status is **Enabled**, indicating that the add\-on feature is effective.

<span id="5zCWNWus"></span>
### Authentication test

When the external authentication add\-on is configured in the APIG instance, and an access request matches the configured Domain name and path, only requests carrying the credential can pass through the API Gateway to access the Backend upstream.


1. When using the Domain name configured in the APIG instance to access the Service without carrying the credential.

   ```Bash
   curl -H "Host: apig-example.com" http://14.xxx.xxx.xxx
   ```
   

   The expected result is as follows, indicating authentication failure and inability to pass through the API Gateway to access the Backend Service.

   ```Bash
   ext_auth:missing_credential
   ```
   

2. When using the Domain name configured in the APIG instance to access the Service while carrying the credential.

   ```Bash
   curl -H "Host: apig-example.com" http://14.xxx.xxx.xxx -H "Authorization: Bearer e8cc8b4f-***"
   ```
   

   The expected result is as follows, indicating that access to the Backend Service through the API Gateway is possible.

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
