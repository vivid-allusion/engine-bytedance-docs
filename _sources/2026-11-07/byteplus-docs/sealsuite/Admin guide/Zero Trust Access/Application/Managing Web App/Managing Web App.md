---
title: "Managing Web App"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/managing-web-app"
---

This guide explains how to securely publish your internal web applications to the internet using SealSuite's **App Gateway**. This feature allows authorized users to access internal apps directly from their web browser—without needing to install a client or connect to a VPN. It's a key component for achieving Zero Trust Access and enabling secure external collaboration.

<span id="2bb54d81"></span>
# **Add a New Web Application**

The goal of this step is to create a secure reverse proxy that connects your public\-facing domain to your internal application server. You'll start by choosing the publishing method that best matches your application's domain structure.


1. Log in to the Admin Console.

2. From the left navigation bar, go to **Zero Trust Access** \> **Application**.

3. Click the **Web App** tab.

4. In the top\-right corner, click the  **+ Create an App** button.

5. In the **Add** dialog, select an application type:

   * [Standard Proxy Application](https://docs.byteplus.com/en/docs/sealsuite/managing-web-app?_vtm_=a78999.b69280.0_0.0_0.0.2_undefined#configuring-a-standard-proxy-application): The most common choice, ideal for publishing a single application with its own dedicated domain.

   * [Wildcard Domain Application](https://docs.byteplus.com/en/docs/sealsuite/managing-web-app?_vtm_=a78999.b69280.0_0.0_0.0.3_undefined#configuring-a-wildcard-domain-application): Use this to publish multiple sub\-applications that share a common parent domain (e.g., `*.yourcompany.com`).

6. Configure the basic information and application functions based on the selected application type, then click **Confirm**.

7. The system redirects you to the **Authorization** tab. You can configure the application's basic visibility on the **Single application authorization** page.

   * **Full**: The application is available to all enterprise users without requiring an access request.

   * **Restricted**: Follows the principle of least privilege. The application is only available to specific users. After selecting this option, click  **+ Add Department**,  **+ Add Employee**, or  **+ Add Role** to assign access permissions.

      * **Apply for application access**: When **Restricted** is selected, you can also enable **Request to access application** and associate a workflow (If no workflow exists, contact the enterprise super administrator to create one. For details, see [Creating workflows](https://docs.byteplus.com/docs/sealsuite/creating-workflows)). Once enabled, unauthorized employees can request access via the client or Portal, and automatically gain permissions upon approval.


<span id="84e12fd5"></span>
## **Configuring a Standard Proxy Application**

If you chose **Standard Proxy Application**, complete the following settings:


* **Basic Information**

   
   |**Parameter** |**Description** |
   |---|---|
   |**Application Icon** |Upload an icon for your application. It will appear in the user's application portal. |
   |**Application Name** |A user\-friendly name to identify this web application. |
   |**Application address** |The **public URL** that users will enter in their browser to access the application (e.g., `https://oa.yourcompany.com`). |
   |**Application Description** |A brief description of the application's purpose. |
   

* **Application Functionality**

   
   |**Parameter** |**Description** |
   |---|---|
   |**Application Gateway** |Enabled by default. This is the core feature that allows clientless, VPN\-less remote access to internal web apps. |
   |**Publishing Method** |Choose how your application will be exposed to the internet.<br><br><br>* **Own Domain Name:**  Publish the application using a domain you own and manage. You will need access to your DNS provider to complete the setup.<br><br>   * **App Domain Name:**  The full public domain name for your application.<br><br>   * **Forwarding Mode:**  How traffic is sent to your backend servers.<br><br>      * **Single Server:**  For applications running on a single backend server.<br><br>      * **Load Balance:**  For applications running on a cluster of backend servers.<br><br>   * **Backend Server Group:**  The **internal address** of your application server(s).<br><br>   * **DNS Parameters:**  Click  **+ Add Gateway** and select the gateway that will handle traffic for this app. When a user accesses the app, their request is first routed to this gateway for identity verification before being forwarded. If you haven't added a gateway yet, you'll need to do so first. See [Managing application gateway](https://docs.byteplus.com/docs/sealsuite/docs-application-gateway-management).<br><br>      <div data-tips="true" data-tips-type="danger" data-tips-is-title="true" data-wrapper-indent="2">danger      </div><br>      <br><br>      <div data-tips="true" data-tips-type="danger" data-wrapper-indent="2">After configuring the gateway, you must create a DNS record with your provider to point your application domain to the gateway's address. See <a href="https://docs.byteplus.com/docs/sealsuite/managing-web-app#1c1abdc8">Configure DNS for Your Application</a> for an example.      </div><br>      <br><br>* **Hosted Domain Names:**  Publish the application using a SealSuite\-provided domain. This is useful for quick testing or if you don't have your own domain.<br><br>   * **App Domain Name:**  Enter a unique prefix, and the system will generate a full public domain name for you.<br><br>   * **Application Access Path:**  If you're enabling SSO, enter the application's login path here.<br><br>   * **Backend Server Group:**  The **internal address** of your application server(s). |
   


<span id="329c4ed5"></span>
## **Configuring a Wildcard Domain Application**

If you chose **Wildcard Domain Application**, complete the following settings:


* **Basic Information**

   
   |**Parameter** |**Description** |
   |---|---|
   |**Application Icon** |Upload an icon for your application. It will appear in the user's application portal. |
   |**Application Name** |A user\-friendly name to identify this web application. |
   |**Application Address** |The **public URL** that users will enter in their browser to access the application (e.g., `https://oa.yourcompany.com`). |
   |**Application Description** |A brief description of the application's purpose. |
   

* **Application Functionality**

   
   |**Parameter** |**Description** |
   |---|---|
   |**Application Gateway** |Enabled by default. This is the core feature that allows clientless, VPN\-less remote access to internal web apps. |
   |**App Domain Name** |Enter your **wildcard domain**, such as `*.example.com`. |
   |**Certificate** |To secure HTTPS traffic for a wildcard domain, you must select or upload a matching SSL certificate. See [Managing SSL certificates](https://docs.byteplus.com/docs/sealsuite/docs-application-gateway-management#9c4ab401). |
   |**Backend Forwarding Method** |Defines the logic for how the gateway locates the actual backend server.<br><br><br>* **Resolve by accessed domain name**: Default option. The gateway transparently passes the subdomain accessed by the user (e.g., `a.example.com`) to the internal DNS for dynamic resolution. Suitable for scenarios where internal DNS records are complete and can be updated in real time.<br><br>* **Specify backend address**: The gateway forwards all requests hitting the wildcard domain directly to a preset server group, bypassing DNS resolution. Suitable for scenarios where internal DNS maintenance costs are high, subdomains have no resolution records, or traffic needs to be unified for distribution by backend Nginx/Ingress. When selected, you must configure the **Forwarding Mode** and **Forward Host**. |
   |**Forwarding Mode** |Configured only when **Backend Forwarding Mode** is set to **Specify Backend Address**. Defines how traffic is forwarded to backend servers.<br><br><br>* **Single Server**: Suitable for scenarios with only one backend application server.<br><br>* **Load Balance**: Suitable for cluster scenarios with multiple backend application servers. When selected, the **Allocation Policy Type** must be configured. |
   |**Allocation Policy Type** |Configured only when **Forwarding Mode** is set to **Load Balance**. Defines how the gateway distributes requests to backend server groups.<br><br><br>* **Weighted Rotation Algorithm**: Distributes requests based on the weight proportions set in the **Backend Server Group**. Suitable for scenarios where backend server performance is uneven. Note that if all backend servers are set to the same weight, the weight attribute will not take effect, and the system will distribute requests using a simple round\-robin strategy.<br><br>* **Least Connections**: Distributes requests to the backend server with the fewest current connections. Suitable for business scenarios with significant differences in request processing duration, effectively preventing overload on a single server.<br><br>* **Source IP Algorithm**: Directs requests from the same client IP address to the same backend server within a period. Note that in this mode, the weight attribute of backend servers will no longer take effect. |
   |**Session Hold** |Optional only when **Forwarding Mode** is set to **Load Balance** and the strategy is **Weighted Rotation Algorithm** or **Least Connections**.<br><br>When enabled, requests from the same user are locked to the same backend server for a set duration to ensure business logic continuity (e.g., login status). SealSuite supports Layer 4 (based on Source IP) and Layer 7 (based on Cookie) session persistence.<br><br>**Configuration Suggestion**: In network environments such as **dedicated lines, VPNs, or cloud connections**, intermediate links may strip or tamper with identity markers, leading to connection instability. In such scenarios, it is recommended to use the **Source IP Algorithm** allocation strategy for more stable session locking. |
   |**Forward Host** |Configured only when **Backend Forwarding Mode** is set to **Specify Backend Address**. Determines the `Host` request header content sent to the backend server.<br><br><br>* **App Domain Name**: Preserves the original domain accessed by the client. Suitable for scenarios where the backend server needs to distribute different services based on the domain (e.g., Nginx multiple Virtual Hosts).<br><br>* **Backend Service Address**: Uses the IP or domain configured in the **Backend Server Group** list. Suitable for scenarios where the backend only recognizes its own IP or specific internal hostnames.<br><br><br>**Note**: If only one server is configured in the **Backend Server Group**, the `Host` will be fixed to the **Backend Server Address** regardless of the selection here. |
   |**Backend Server Group** |Visible only when **Backend Forwarding Mode** is set to **Specify Backend Address**. Used to configure the **actual service address** of the application within the corporate internal network.<br><br>**Note**: When the allocation strategy is **Weighted Rotation Algorithm**, you can set a **Weight** for each server. Administrators can set different weight proportions (range 1\-100) based on server performance, where higher values allocate more traffic. |
   |**DNS Parameters** |Click  **+ Add Gateway** and select the appropriate gateway. You must then configure a wildcard DNS record with your provider to point your domain to the gateway's address. See [Configure DNS for Your Application](https://docs.byteplus.com/docs/sealsuite/managing-web-app#1c1abdc8) for an example. |
   


<span id="1c1abdc8"></span>
# **Configure DNS for Your Application**

You must create a DNS record with your domain provider (e.g., Alibaba Cloud, GoDaddy) that points your application's public domain to the SealSuite gateway address.

This section uses **Alibaba Cloud** as an example, but the core principles apply to any DNS provider.


1. **Copy the Gateway Address from SealSuite.** 

   * **During app creation:**  Find the correct gateway in the list and click the copy icon in the **Domain name resolution gateway address** column.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24935e3ef9014ab3b3a0669a81301f16~tplv-goo7wpa0wc-image.image) </span>

   * **For an existing app:**  Go to the app's details page, click the **Application Gateway** tab, and copy the address from the **CNAME Address/Domain name resolution gateway address** column.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7fb7481aa0d7466da779b2b9473e454e~tplv-goo7wpa0wc-image.image) </span>

2. **Add a DNS Record with Your Provider.** 

   1. Log in to your Alibaba Cloud DNS Console.

   2. Find your domain and click **Configure Resolution**.

   3. Click **Add DNS Record**.

   4. Fill in the fields and click **OK**.

   
   |**Field** |**Example Value** |**Description** |
   |---|---|---|
   |**Record Type** |A |An A record maps a domain to an IPv4 address. |
   |**Host** |oa |The subdomain prefix. Use `oa` for `oa.yourcompany.com`. Use `@` for the root domain (`yourcompany.com`). |
   |**Resolution Line** |Default |Keep the default setting. |
   |**Value** |47.100.x.x |Paste the **gateway IP address** you copied from the SealSuite Admin Console. |
   |**TTL** |10 minutes |The cache time for the DNS record. |
   

3. **Verify Your Configuration.** 

   After waiting for the DNS changes to propagate, you can verify that the setup is working:

   * **Use command\-line tools:** 

      * `ping your-app-url.com` should return the gateway's IP address.

      * `nslookup your-app-url.com` should show the correct resolution.

   * **Test in your browser:**  Navigate to your application's URL. You should be redirected to the SealSuite authentication page.


<span id="60a35865"></span>
# **Manage Your Web Applications**

<span id="25254362"></span>
## **Viewing the Application List**


1. Log in to the Admin Console.

2. Go to **Zero Trust Access** \> **Application** and select the **Web App** tab.

3. From this page, you can:

   * Filter the list by **Status**, **Application name**, or **Scope**.

   * View basic information like name, URL, and enabled features.

   * Click an application name to go to its details page.

   * Click a URL to quickly access the application.

   * Use the **Actions** column to **Disable** or **Delete** an application.

      * **Disable:**  Temporarily makes the application unavailable. You can reactivate it later.

      * **Delete:**  Permanently removes the application and its configuration. **This action cannot be undone.** 


<span id="56ed9fd8"></span>
## **Viewing and Configuring Application Details**


1. Log in to the Admin Console.

2. Go to **Zero Trust Access** \> **Application** and select the **Web App** tab.

3. Click the name of the application you want to manage.

4. The details page has several tabs:

   
   |**Tab** |**Description** |
   |---|---|
   |**General** |View and edit the app's core details, security settings, and portal navigation options.<br><br><br>* **General:**  Edit the icon, name, description, group, and access URL.<br><br>* **Security Setup:**  Enable or disable **Multi\-Factor Authentication (MFA)**  and set the re\-authentication interval.<br><br>* **Portal Quick Access:**  Configure how the application appears in the SealSuite portal and other third\-party platforms. See [Configuring portal quick access](https://docs.byteplus.com/docs/sealsuite/docs-application-management_1#d2d03e7a). |
   |**Application Gateway** |Review and manage the gateway configuration for this app.<br><br><br>* For details on these settings, refer to the "Add a New Web Application" section above.<br><br>* Once the gateway is enabled, you can also configure security and advanced policies. See [Configuring app advanced settings](https://docs.byteplus.com/docs/sealsuite/docs-configuring-application-strategy) and [Configuring application security rules](https://docs.byteplus.com/docs/sealsuite/docs-configuring-application-security-rules). |
   |**API Access Control** |View, add, and manage API resources protected by the gateway.<br><br><br>* **View:**  The list shows existing API resource groups, sorted by creation date. Use the search bar to find resources by name or path.<br><br>* **Add:**  Click  **+ Add Resource** to define a new API resource.<br><br>   * **Resource Name:**  A descriptive name. Supports Chinese and English characters, up to 60 characters long.<br><br>   * **Resource Path:**  The URL path that the gateway will match (e.g., `/admin/*` or a specific path like `/image/logo.gif`).<br><br>   * **Request Method:**  Select the allowed HTTP methods (GET, POST, etc.).<br><br>      Once you've added an API resource, you can create access control policies for it under **Dynamic Decision**. See [Configuring dynamic policies](https://docs.byteplus.com/docs/sealsuite/docs-dynamic-policies).<br><br>   * **Manage:**  Use the **Edit** and **Delete** actions in the list, or select multiple resources to **Batch Delete**. |
   |**Authorization** |* **Single application authorization**: Adjust the application's basic visibility and enable/disable the **Request to access application** entry.<br><br>* **Authorized objects** View a list of personnel, departments, and roles authorized to access the application.<br><br>* **Authorization group**: View all authorization groups (batch authorization rules) associated with the application. Click **Go to Page** to adjust them, or return to the **Web App** list and click **Batch authorization** for unified management. For details, see [Managing batch authorization](https://docs.byteplus.com/docs/sealsuite/managing-web-app#1391549c). |
   


<span id="1391549c"></span>
# **Managing batch authorization**

Configuring permissions individually for numerous enterprise applications significantly increases maintenance costs and the risk of omissions during personnel changes. "Authorization groups" provide a batch authorization capability to improve efficiency and security. Create an authorization group to bind "**specified crowds (employees/departments/roles)** " to "**multiple applications (or application tags)** " and uniformly set them to "**Allow access**" or "**Deny access**". This handles complex scenarios such as:


* **Scenario 1: Cross\-application batch permission activation**

   When establishing a new business department or onboarding new employees, you do not need to add personnel to each application manually. Create an authorization group with an "Allow" action, associate the target crowd (e.g., "Business Department A") with the relevant business applications (or application tags), and activate permissions across all applications with a single click.

* **Scenario 2: High\-risk isolation and control of specific personnel (blacklist)** 

   If an employee exhibits abnormal behavior or poses security risks, create an authorization group with a "Deny" action to associate them with core, highly sensitive applications. The "Deny rules first" principle ensures the employee immediately loses access to these applications, achieving cross\-application blocking.


<span id="2b9b3432"></span>
## Create an authorization group


1. Log in to the Admin Console.

2. In the left navigation bar, select **Zero Trust Access** \> **Application**.

3. On the **Application** page, click the **Web App** tab, then click **Batch authorization** in the upper\-right corner of the list.

4. In the upper\-right corner of the batch authorization drawer, click  **+ Create authorization group**.

5. In the configuration dialog box, complete the following settings:

   * **General**

      * **Authorization group name**: Required. Enter a custom name (up to 60 characters), such as "Innovation Department Exclusive Application Authorization".

      * **Authorization group description**: Optional. Describe the group's purpose (up to 100 characters).

      * **Status**: Enabled by default. Can be disabled.

   * **Action**

      * **Action type**: Select **Allow** to grant access or **Deny** to block access.

      * **Scope** : Click edit to specify the authorized personnel. You can add users by **user**, **department**, or **role**. You can also configure **Exclude objects** to remove specific personnel from the scope.

      * **Application**: Click edit to select one or more applications added to the application gateway, or associate them via **Application tags**.

6. Click **Confirm**. A secondary confirmation dialog box appears. Since batch authorization may affect many employees' access, you must manually type `Confirm batch authorization` in the input box to verify the action.


<span id="792d4f94"></span>
## Manage and maintain authorization groups

On the **Batch authorization** page, use the top filter bar (by name, employee, department, application, or tag) to locate authorization groups and perform the following operations:


* **Enable/Disable authorization groups**: Toggle the status switch in the list to enable or disable groups.

* **Edit authorization groups**: Click **Edit** in the operation column to modify the effective objects, application scope, or action type.

* **Delete authorization groups**: Click **Delete** in the operation column. This permanently clears the group's configurations. You must type `Delete authorization group` to confirm.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><strong>Conflict and priority rule description</strong>:</div>



* <div data-tips="true" data-tips-type="warning"><strong>Internal conflict in authorization groups</strong>: If a user or department triggers both an "Allow" and a "Deny" authorization group for the same application, SealSuite strictly follows the "<strong>Deny rules first</strong>" principle and blocks access.</div>


* <div data-tips="true" data-tips-type="warning"><strong>Priority determination order with other policies</strong>: When determining a user's final access to a web application, SealSuite evaluates multiple security policies. The blocking priority is: <strong>Dynamic Control Deny</strong> \> <strong>Authorization Group Deny</strong> \> <strong>Advanced Authentication Deny</strong> \> <strong>Authorization Group Allow</strong>. This means that even if an authorization group explicitly allows access, the user will be blocked if their device triggers a Dynamic Control interception rule or they fail advanced secondary authentication.</div>
