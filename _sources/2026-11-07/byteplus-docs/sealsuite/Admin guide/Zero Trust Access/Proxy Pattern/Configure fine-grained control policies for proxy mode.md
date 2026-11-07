---
title: "Configure fine-grained control policies for proxy mode"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/configure-proxy-mode-fine-control-strategy"
---

Fine\-grained control policies are the application\-layer (L7) permission control engine in SealSuite proxy mode. Unlike ACL policies, which primarily determine whether users can access an application, fine\-grained control policies identify specific access paths (URLs) over HTTP/HTTPS. This lets administrators control which pages and APIs users can access within an application.

By configuring fine\-grained control policies, administrators can follow the principle of least privilege. They can strictly limit the resource scope available to different roles in the same application, effectively prevent lateral privilege escalation within applications, and provide in\-depth audit support for sensitive business operations.

This article describes how to configure fine\-grained control policies in proxy mode.

 &nbsp;

<span id=".57K-57uG566h5o6n562W55WlLXZzLWFjbC3nrZbnlaU="></span>
## Fine\-grained control policies vs. ACL policies

&nbsp;


|Dimension |ACL policy (L4) |Fine\-grained control policy (L7) |
|---|---|---|
|**Control granularity** |**Application level**. Controls only whether employees can access the IP address, port, or domain name of the target application. |**Page/API level**. Identifies and authorizes specific URL paths, such as `/admin` and `/api/delete`. |
|**Defense objective** |**Prevent unauthorized access**. Blocks unauthorized users or non\-compliant devices from accessing internal business systems. |**Prevent lateral privilege escalation**. Restricts unauthorized operations by admitted users within an application, such as a regular employee attempting to access the Admin Console. |
|**Data protection** |**None**. Controls only network connectivity. |**Page\-level hardening**. Supports advanced protection such as dynamic screen watermarks, copy prevention, and developer tool blocking. |


 &nbsp;

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Make sure you have configured the corresponding "Allow" Access Policy for the target application by referring to [Configure a proxy-mode ACL policy](https://docs.byteplus.com/en/docs/sealsuite/configure-proxy-mode-acl-policy). Fine\-grained control policies and ACL policies use chained execution logic. Access requests must first pass admission checks before traffic can enter the application layer for in\-depth evaluation.

* Make sure the target application resource has been defined on the **Client Access** tab of the **Zero Trust Access** \> **Application** \> **Web App** page. For details, see [Manage fine-grained control web applications](https://docs.byteplus.com/en/docs/sealsuite/management-fine-control-web-application).

* Make sure the SealSuite client has been upgraded to **3.3.18** or later.


 &nbsp;

<span id=".5re75Yqg57K-57uG566h5o6n562W55Wl"></span>
## Add a fine\-grained control policy


1. Log in to the SealSuite Admin Console.

2. In the left\-side navigation pane, choose **Zero Trust Access** \> **Proxy Policy**.

3. Switch to the **Fine\-Grained Control** tab, and click **Add Access Rule** on the right side of the page.

   <span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/2026-09-24/proxy-en-review/fine-list-ready.png) </span>

4. On the policy configuration page that appears, complete the following settings as needed, and click **Confirm**.


 &nbsp;

<span id=".5Z-65pys5L-h5oGv"></span>
### General

<span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/2026-09-24/proxy-en-review/fine-general-ready.png) </span>


* **Policy name**: Enter a custom policy name. We recommend that the name indicate the control scope, such as "Finance system \- query only".

* **Strategy status**: Select the initial status of the new policy, either enabled or disabled.

* **Priority**: The priority of the current policy. Valid values are 0 to 100. A larger value indicates a higher priority. The system matches policies in descending order of priority and stops matching after a policy is hit. If two policies with the same priority are hit, the policy modified most recently takes precedence.

* **Strategy effective duration**: Configure the time range during which the policy takes effect. Custom durations in days are supported.


 &nbsp;

<span id=".5Yqo5L2c"></span>
### Action

Define the processing logic that the gateway executes when an access request matches the policy.

<span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/2026-09-24/proxy-en-review/fine-action-ready.png) </span>


* **Action Type**

   * **Allow**: Allows access requests that meet the conditions.

   * **Reject**: Blocks access requests. You can configure **Blocked Message** to determine what end users see when they are blocked. Options include **No notifications** (directly returns 403), **Use built\-in information** (displays the default SealSuite block page with customizable text), and **Use custom redirect pages** (redirects to an internal permission request page, for example).

* **Data Protection (Control Type)** : After this option is enabled, the control granularity extends from basic "access admission" to "behavior control". SealSuite not only verifies whether employees can access the target page, but also applies page\-level security hardening to matched Layer 7 traffic. This effectively reduces the risk of sensitive data leakage through user interactions.

   * **Do not copy content**: Prevents employees from copying text data on application pages.

   * **Disable Mouse Right Click**: Disables the browser right\-click menu to block attempts to obtain page resources through "Save as" or "View source".

   * **Disable Developer Tool**: Detects and blocks browser developer tools (F12) from opening. This prevents technical personnel from capturing API data or bypassing front\-end logic through the debugging environment.

   * **Turn on screen watermark**: Overlays a dynamic watermark on application pages. Click **Configure** on the right to customize the watermark content and style for traceability audits of non\-compliant screenshots.


 &nbsp;

<span id=".5a6i5L2T"></span>
### Object

Define the "people" and "resource" scopes to which this policy applies.

<span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/2026-09-24/proxy-en-review/fine-object-ready.png) </span>


* **Scope**: Select the employee scope to which this policy applies. Select **All** for all employees or **Part** to specify a subset. When you select **Part**, you can filter by **Employee** (department, role, or specific member) or **Device** (name or group).

* **Resources**: Define the specific application resources controlled by this policy. You can select all applications or a custom resource scope.

   * **Custom resource scope**: Under **Resources**, select **Part**, click **Edit**, and select target resources by **Application name** or **Application tag** in the window that appears. The resource data comes from **Zero Trust Access** \> **Application** \> **Web App**. To add and maintain resources, go to the **Web App** page and switch to the **Client Access** tab. Resources on the **gratuitous access** tab (clientless access) apply only to application gateway mode.


 &nbsp;

<span id=".566h55CG57K-57uG566h5o6n562W55Wl"></span>
## Manage fine\-grained control policies

On the **Fine\-Grained Control** list page, you can maintain existing policies as follows:


* **Status switching**: Quickly enable or disable a policy by using the status switch in the **Action** column.

* **Priority adjustment**: Click the **Priority** of a target policy to quickly modify the policy matching order based on business changes.

* **Edit/Delete**: Click the corresponding button to modify the configuration or remove policies that are no longer needed.


 &nbsp;

<span id=".5ZCO57ut5pON5L2c77ya5p-l55yL6K6_6Zeu5a6h6K6h"></span>
## Next step: View access audit logs

After a policy takes effect, all matched access activities are recorded in detail. Go to **Audit Logs** \> **Proxy Layer 7 Access Log** to view detailed access paths, matched policies, and executed actions.
