---
title: "Configuring app advanced settings"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-configuring-application-strategy"
---

The SealSuite Application Gateway provides a comprehensive suite of advanced policies to enhance your application's security, performance, and compatibility. You can use these settings to implement fine\-grained controls such as authentication\-free access, cross\-domain resource sharing, high\-availability health checks, and custom request/response rewriting. This guide details each policy and provides instructions for configuration.

<span id="0b551e2b"></span>
# Prerequisites

You have added a new application and associated it with an application gateway. For specific operations, please refer to [Adding SSO application](https://docs.byteplus.com/docs/sealsuite/docs-add-application).

<span id="3f8a206b"></span>
# Procedure


1. Log in to the SealSuite Admin Console.

2. From the left navigation bar, go to **Zero Trust Access** \> **Application**.

3. In the **Web App** tab, select the app that needs to configure advanced policies and go to the app details page.

4. In the **Advanced Settings** area of the **Application Gateway** tab, enable and configure the appropriate policy based on the actual security requirements.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/88a82118a1db4424bede527b884a2b52~tplv-goo7wpa0wc-image.image) </span>

   For each policy configuration description, see [Advanced settings configuration instructions](https://docs.byteplus.com/docs/sealsuite/docs-configuring-application-strategy#ea0f4b7d).


<span id="ea0f4b7d"></span>
# Advanced settings configuration instructions

<span id="a684f842"></span>
## Authentication\-Free Access

With this policy enabled, apps that access the gateway proxy do not require MFA authentication for quick access.

For example, when authentication\-free access is enabled in wildcard domain applications, every domain within the application will facilitate quick access via the application gateway proxy, bypassing MFA Authentication.

<span id="509d178c"></span>
## Cross\-Domain Access

Cross\-domain access refers to the ability to request resources from a different domain. Commonly, cross\-domain access is needed when accessing different domain names, the same domain name with different ports, or different subdomains. For example, the following cross\-domain access scenario:


* Web applications need access to API services from different sources.

* Web pages need to load resources from different sources. For example, loading CSS, JavaScript, and other resources from another domain under the source domain name.

* Web applications need to interact with third\-party services. For example, social media platforms, payment gateways, map services, and other interactions.


To protect browser security and prevent cross\-site attacks, browsers enforce a same\-origin policy, which by default only allows a web page to access resources from the same domain it was loaded from. Therefore, you can enable the cross\-domain access policy and configure the detailed parameters of the cross\-domain access policy to achieve cross\-domain access for your application.


1. Enable the **Cross\-Domain Access** policy.

2. Click **Configure** to configure cross\-domain access policy parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |Request Domain |The request domain is the originating website for a cross\-domain request. To permit its access, the request domain must be included in the configuration settings. You can use a wildcard (\*) to indicate that all request domain access is allowed, or you can specify a specific request domain name. |
   |Request Method |The request method refers to the HTTP method used for cross\-domain requests, and you must add the allowed request methods to the configuration, such as GET, POST, etc. |
   |Mandatory Request Header |The mandatory request header refers to the HTTP header information that needs to be added to the cross\-origin request, and the name of the mandatory request header needs to be added to the configuration. Click on **Add New** to add multiple mandatory request headers. |
   |Path |The path refers to the path of the cross\-domain request, and a forwarding rule must be added to the configuration to specify the path of the cross\-domain request and the target server address. Click on **Add New** to add multiple paths. |
   

   At the top of the form, click **Add** to add multiple cross\-domain configurations. Except for the first cross\-domain configuration, all other new cross\-domain configurations support deletion.

3. Click **Confirm** to complete configuration.


<span id="aefb3bf2"></span>
## Domain Name Rewriting

This policy is used to replace nested resource addresses when multiple intranet resources are nested.


1. Enable the **Domain Name Rewriting** policy.

2. Click **Configure** to configure the site rewrite policy.

   When configuring the site rewrite policy, you need to specify **Address before domain name rewrite**, which is the address requested by the front end, which can be the domain name. Click **Add New** to add multiple addresses before domain name rewrite. When configuring a pre\-rewrite address, it is necessary to ensure the correctness and security of the address.

3. Click **Confirm** to complete configuration.


<span id="0dd88d10"></span>
## Gateway Request Rewriting

This policy applies to parameters included in the custom request URL, such as request header parameters and query parameters. It supports configuring multiple rewrite operations which enable access to the server address for the business site.


1. Enable **Gateway Request Rewriting** policy.

2. Click **Configure** to configure the gateway request rewriting policy parameters based on the provided information.

   
   |**Region** |**Field** |**Description** |
   |---|---|---|
   |Headers Rewriting |Header type |Options include **request header** and **response header**. |
   ||Rewrite operation |Select **update**, **regular substitution**, **add** or **delete**. |
   ||Parameter name |Specifies the parameter name. |
   ||Regular expression |If you selected **regular substitution** as a rewrite operation, you need to specify a matching regular expression. |
   ||Parameter Value |Specifies the parameter value. Click **Add New** below the **Headers Rewriting** area to add multiple parameters. |
   |Query Parameter Rewriting |Rewrite operation |Select **update**, **regular substitution**, **add** or **delete**. |
   ||Parameter name |Specifies the query parameter name. |
   ||Regular expression |If you selected **regular substitution** as a rewrite operation, you need to specify a matching regular expression. |
   ||Parameter Value |Specifies the query parameter value. Click **Add New** below the **Query Parameter Rewriting** area to add multiple query parameters. |
   

3. Click **Confirm** to complete configuration.


<span id="e9c0a416"></span>
## Traffic Hijacking

When this policy is enabled, the VPN DNS server will automatically intercept user requests for the third\-party app and reroute them to the appropriate application gateway. This policy grants users access to the application through the application gateway proxy. This policy is enabled by default.

<span id="9ecd0eb0"></span>
## Custom Script Configuration

This policy provides administrators with maximum flexibility. By injecting custom scripts (such as JavaScript), you can extend or modify the functionality of an existing site—such as customizing frontend styles, enhancing user interaction, or integrating third\-party analytics tools—without needing to modify the application's backend source code.


1. Enable the **Custom Script Configuration** toggle.

2. Click **Configure** and paste your prepared script code into the configuration box.


<span id="5537d76d"></span>
## Restricting Access to the Feishu Client Only

This enhanced security policy deeply integrates your application with the Feishu/Lark ecosystem. When enabled, the SealSuite Application Gateway verifies whether an access request originates from an official Feishu/Lark client (Desktop or Mobile). Any requests initiated from external browsers will be automatically denied.


1. **Prerequisite: Configure Feishu/Lark Authentication Source**

   Before activating this policy, ensure you have successfully configured and enabled the **Feishu/Lark Authentication Source** within the SealSuite Identity module.

2. **Activation and URL Generation**

   In the Advanced Settings, toggle the **Only allow app access in Feishu** switch. A dialog box will appear containing a dedicated **Redirect URL**. This URL serves as the bridge for the security authentication handshake between the SealSuite application and the Feishu/Lark application.

3. **Feishu/Lark Open Platform Configuration**

   1. Click **Copy** to save the provided Redirect URL.

   2. Log in to the **Feishu/Lark Open Platform** developer console.

   3. Select the application corresponding to this integration and enter the **App Details** page.

   4. Navigate to **Security Settings** and paste the copied address into the **Redirect URL** field, then save your changes.

4. **Enabling the Policy**

   After completing the configuration on the Feishu/Lark Open Platform, return to the SealSuite Admin Console and click **Enable** to activate the policy.


<span id="ef91026c"></span>
## Health Check

This policy ensures the **high availability** of your backend services. The Application Gateway sends periodic **probes** to backend servers based on your defined rules (frequency, path, and expected response codes). If a server fails these probes consecutively, the gateway automatically removes it from the **load balancing pool**, preventing traffic from being routed to a failing instance. The server is automatically reintegrated once it returns to a healthy state, effectively preventing application downtime caused by a single point of failure.


1. Toggle on the **Health Check** switch.

2. Click **Configure**, define your health check rules in the dialog box, and click **Confirm**.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Health Detection Port** |Defines which port on the backend server receives the probe requests.<br><br><br>* **Use the backend server's default business port**: Probes are sent to the standard port configured in your Backend Server Group.<br><br>* **Specify Custom Port**: If your application uses a dedicated port for health monitoring (separate from business traffic), select this and enter the port number. |
   |**Health Detection Path** |The specific URL path the gateway will query (e.g., `/health-check`). Must start with a forward slash `/` and be between 1–80 characters. |
   |**Detection Interval (seconds)**  |The number of seconds between each health probe sent to a backend server. (Range: 1–50s). |
   |**Timeout (seconds)**  |The maximum time to wait for a response from the server before considering the probe a failure. (Range: 1–50s). |
   |**Health Check Return Code** |The HTTP status code(s) that indicate a "Healthy" status. Only responses matching this configuration are considered successful.<br><br>Typically, `200` is used for standard health. You can also specify ranges like `2XX` (any 200\-level success) or `2XX-5XX`. |
   


<span id="da357d2f"></span>
## Obtaining Client IP

The Application Gateway includes this built\-in core capability to ensure that backend applications receive the authentic source IP address of the visitor. This feature is permanently active and cannot be disabled to ensure consistent logging and security auditing across your systems.

<span id="117aad49"></span>
## Trusted Proxy Configuration

In complex network architectures, traffic often passes through multiple intermediate layers—such as CDNs or front\-end WAFs—before reaching the SealSuite Application Gateway. This policy allows you to define a list of **Trusted Proxy** IP addresses.

When a request originates from one of these trusted IPs, the gateway intelligently parses the `X-Forwarded-For` header to identify the original upstream client IP. This prevents the gateway from misidentifying the proxy’s IP as the visitor’s IP, ensuring accurate identity auditing and security logs even in multi\-layered proxy environments.


1. Enable the **Trusted Agent Configuration** toggle.

2. Click **Configure** and enter the IP addresses or CIDR ranges of the proxy servers (e.g., WAFs, load balancers, or CDNs) situated in front of the SealSuite Application Gateway.

3. Separate multiple IPs or network segments using commas or spaces.


<span id="6c19bee1"></span>
## Advanced settings

To meet specific requirements for access performance, security validation, and protocol compatibility, you can customize advanced gateway parameters for each integrated application.


1. Navigate to the **Advanced settings** card and click **Configure**.

2. Adjust the following parameters in the configuration dialog based on your technical requirements:

   
   |**Parameter** |**Description** |**Example** |
   |---|---|---|
   |**1. Location Redirect Rewrite** |Used to correct HTTP 301 or 302 redirect URLs returned by backend systems. If a backend server returns a `Location` header containing an internal IP (e.g., `http://192.168.x.x/home`), the gateway replaces it with the corresponding public URL. |**Example**: A finance system uses `http://10.0.0.5` internally but is mapped to `https://finance.corp.com` via SealSuite.<br><br><br>* **Key**: `http://10.0.0.5`<br><br>* **Value**: `https://finance.corp.com`<br><br><br>**Result**: A redirect to `/login` on the internal IP is automatically rewritten to the public URL. |
   |**2. Cookie Domain Custom Mapping** |Manually specifies rewriting rules for the `Domain` attribute in `Set-Cookie` headers. This ensures that the browser correctly stores and attaches cookies when accessing the app externally. |**Example**: Assume the backend returns the header `Set-Cookie: session_id=123; Domain=oa.internal;`, while the public access URL is `https://oa.xyz.com`.<br><br><br>* **Key**: `oa.internal`<br><br>* **Value**: `oa.xyz.com`<br><br><br>**Result**: The gateway rewrites the header so the employee’s browser receives `Domain=oa.xyz.com`. This ensures the login session is correctly stored and remains persistent when the application is accessed over the public network. |
   |**3. Token Cookie Domain** |Defines the domain scope for the identity token cookie issued by the gateway. This controls which domains the browser will automatically include the login credential for. |**SSO Experience**: By setting this to your root domain (e.g., `.corp.com`), a user logged into `git.corp.com` can access `wiki.corp.com` without being prompted to log in again. |
   |**4. Special Access URL Mapping** |Handles non\-standard or complex authentication redirection logic (e.g., OAuth 2.0 or SAML). It ensures query parameters and anchors are fully preserved during redirects. |**Example**: Consider a legacy ERP system that requires a specific query parameter, such as `?source=legacy`, to successfully initialize a session.<br><br><br>* **Key**: `/erp/login`<br><br>* **Value**: `https://gateway.corp.com/erp/login`<br><br><br>**Result**: When a user request is redirected to the login page, the gateway enforces this mapping to ensure that `source=legacy` and all subsequent parameters are passed to the client completely intact. |
   |**5. Response Rewrite Blacklist** |Defines a list of URL paths (supporting wildcards like `/api/*`) where the gateway should **not** modify any content. The gateway will transparently pass through the backend response. |* **Scenario 1**: If your application’s API endpoints are consolidated under the `/v1/api/` directory:<br><br>   * **Input**: `/v1/api/*`<br><br>* **Scenario 2**: If specific frontend scripts are encountering errors due to gateway rewriting:<br><br>   * **Input**: `/static/js/*.js` |
   |**6. Response Rewrite Extensions** |A whitelist of file extensions (e.g., `.html`, `.jsp`) that the gateway is allowed to parse and modify (e.g., for IP replacement or script injection). |**Performance**: Scanning large binary files like images (`.jpg`) or installers (`.exe`) is resource\-intensive and can cause latency. Limiting rewriting to text\-based files optimizes gateway CPU/Memory usage. |
   |**7. Disable Cookie Domain Rewrite** |When enabled, the gateway stops automatically modifying the `Domain` attribute in the `Set-Cookie` header, passing the backend's original value to the browser. |**Advice**: Keep this **Disabled** unless your backend already provides the correct public domain or you are using **Parameter 2** to manage domains manually. |
   |**8. Hashtag (#) Preserve Paths** |Captures URL anchors (fragments) that browsers typically do not send to the server. The gateway injects a script into the response for these paths to capture the fragment and pass it to the backend. |**Example**: Suppose your application performs login verification using a URL structure like `https://oa.com/login#token=123`.<br><br><br>* **Input**: `/login` or `/login*`<br><br><br>**Result**: When a user accesses this path, the SealSuite gateway uses an injected script to "capture" the `token=123` fragment—which is normally restricted to the browser—and ensures the backend system can receive and process the parameter as intended. |
   |**9. Disable Iframe Auto Rewrite** |Stops the gateway from injecting scripts designed to fix internal IP addresses within `<iframe>` tags. |**Advice**: Enable this only if the auto\-fix logic causes JavaScript errors or if your backend already correctly handles relative paths for nested windows. |
   |**10. Security Policy Priority Injection** |Moves SealSuite security scripts (e.g., watermarks, anti\-copy logic) to the very top of the `<body>` tag in the HTML document. |**Security**: On slow networks, page content might load before security scripts. Moving the injection point ensures "immediate" protection (watermarks appear instantly) before sensitive data is displayed. |
   |**11.**  **Disable Hashtag Accept Header Check** |Relaxes the gateway's performance check that only injects hashtag\-preservation scripts when a `Accept: text/html` header is present. |**Use Case**: Fixes issues for legacy clients, mobile apps, or embedded devices that do not send standard HTTP headers but still rely on hashtag parameters for login. |
