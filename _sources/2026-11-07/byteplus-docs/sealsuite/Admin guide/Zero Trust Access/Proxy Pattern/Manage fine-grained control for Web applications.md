---
title: "Manage fine-grained control for Web applications"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/management-fine-control-web-application"
---

In SealSuite proxy mode, to enforce fine\-grained control on Web applications, such as identifying and verifying specific URI paths and action APIs in HTTP/HTTPS requests, you must first define the application and its associated URL resource paths in the Admin Console.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip"><strong>Web applications (fine\-grained control)</strong>: Support URL\-level control and data protection based on URL paths. Configure this on the <strong>Zero Trust Access</strong> \> <strong>Application</strong> \> <strong>Web App</strong> page.</div>


* <div data-tips="true" data-tips-type="tip"><strong>Proxy applications</strong>: Support only transport\-layer access control based on IP addresses, ports, or domain names. Configure this on the <strong>Zero Trust Access</strong> \> <strong>Application</strong> \> <strong>Proxy App</strong> page. For details, see <a href="https://docs.byteplus.com/en/docs/sealsuite/management-agent-mode-application-resources">Manage proxy applications</a>.</div>



This article describes how to add and manage Web application resources for fine\-grained control policies in proxy mode.

 &nbsp;

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Ensure that you have deployed proxy gateway nodes and configured their clusters on the **Zero Trust Access** \> **Gateway Config** \> **Proxy Gateway** page by referring to [Access a proxy gateway](https://docs.byteplus.com/en/docs/sealsuite/access-proxy-gateway). At least one node in the target cluster must be running normally.

* Ensure that the target Web application is running normally on the enterprise intranet.

* Ensure that the SealSuite client has been upgraded to version **3.3.21** or later.


 &nbsp;

<span id=".5re75YqgLXdlYi3lupTnlKjotYTmupA="></span>
## Add Web application resources

Adding Web application resources includes two phases: creating an application and defining controlled resources.

 &nbsp;

<span id=".56ys5LiA5q2l77ya5Yib5bu6LXdlYi3lupTnlKg="></span>
### Step 1: Create a Web application


1. Log in to the SealSuite Admin Console.

2. In the left navigation pane, choose **Zero Trust Access** \> **Application** \> **Web App**.

3. At the top of the page, switch to the **Client Access** tab.

4. Click **Create an app** in the upper\-right corner of the page.

   <span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/2026-09-24/proxy-en-review/border-web-list.png) </span>

5. On the configuration page, complete the following key settings and click **Confirm**.

   <span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/2026-09-24/proxy-en-review/border-web-create.png) </span>

&nbsp;

   
   |**Configuration item** |**Description** |
   |---|---|
   |**Software name** |Enter a custom application name that is easy to identify. |
   |Application address |Configure the real service address of the target application in the intranet environment.<br><br><br>* **Protocol**: Select the service protocol of the application, http or https.<br><br>* **Address and port**: Enter the server IP address or domain name of the application and the corresponding service port number.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you select <strong>https</strong> as the protocol, the SealSuite gateway must decrypt encrypted traffic to identify the specific URL path. If no specific certificate is configured, the system uses the global "enterprise self\-signed root certificate" for decryption and verification by default. Ensure that a compliant SSL certificate is configured in <strong>Enterprise Settings</strong> \> <strong>Certificate Management</strong>, or ensure that all access endpoints have installed and trust the SealSuite global root certificate. Otherwise, employees will see a browser security alert during access.</div><br> |
   |**Application Description** |Optional. Briefly describe the business purpose of the application to facilitate future maintenance and identification. |
   |**Tag** |Associate logical grouping identifiers with the application. Tags allow you to grant permissions in batches across applications during policy configuration. |
   |**Effective access point** |Specify the target proxy gateway cluster where the application is published. You can select **All Clusters** or **Partial Clusters**. Selecting individual gateway nodes is not supported.<br><br><br>* **All Clusters**: Publish the application to all proxy gateway clusters.<br><br>* **Partial Clusters**: Publish the application to specified proxy gateway clusters.<br><br>* The effective cluster scope of a Web application must be included in the effective cluster scope of the corresponding [proxy application](https://docs.byteplus.com/en/docs/sealsuite/management-agent-mode-application-resources). If a cluster is outside the effective scope of the corresponding proxy application, fine\-grained control policies cannot take effect on that cluster.<br><br>* After the application is published to a cluster, the configuration is delivered to all nodes in the cluster. New nodes that join the cluster automatically inherit the applications published to that cluster. When a node leaves the cluster, its application publishing relationships inherited from that cluster are removed. |
   |**XFF Forwarding** |Controls how the gateway transparently forwards the real client IP address to the backend. The gateway processes the `X-Forwarded-For` HTTP header to forward the client IP address. Enable **XFF Forwarding** and select one of the following options. When the switch is disabled, the gateway appends the IP address of the client connected directly to it.<br><br><br>* **Pass\-through**: The gateway does not modify `X-Forwarded-For` and forwards the original request content to the backend. This applies when a trusted upstream proxy, such as a CDN or WAF, already writes XFF.<br><br>* **Add**: Append the client IP address directly connected to the gateway to the end of `X-Forwarded-For`. If the request does not contain this header, the gateway automatically creates it. This applies when you need to retain complete proxy chain information and meet audit and tracing requirements.<br><br>* **Cover**: Replace the entire content of `X-Forwarded-For` with the client IP address directly connected to the gateway. The original value is discarded. This applies when upstream XFF content is not trusted, such as preventing clients from forging XFF. |
   


<span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/2026-09-24/proxy-en-review/border-xff-options.png) </span>

 &nbsp;

<span id=".56ys5LqM5q2l77ya5a6a5LmJ5Y-X5o6n6LWE5rqQ77yIdXJsLei3r-W-hC_mjqXlj6PvvIk="></span>
### Step 2: Define controlled resources (URL paths/APIs)

After the application is created, go to the application details page to define the specific resource scope for control.


1. On the **Client Access** tab of the **Web App** list page, click the target application name to open the details page.

2. In the **Resource Management** section at the bottom of the page, click  **+ Add Resource** on the right.

   <span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/2026-09-24/proxy-en-review/border-web-resource-detail.png) </span>

3. In the **Add Resource** window, define the application resources that require fine\-grained access control under this application.

   * **Resource name**: Define a name for this group of paths, such as "core management APIs".

   * **Resource Path**: Enter a specific URL or URI path.

      * Supports **exact paths**, such as `/admin/login`.

      * Supports **wildcard paths**. Use `*` to match all resources in a directory, such as `/api/v1/*`.

   * **Continue adding**: To define multiple resource paths, click **Add New**.

   * **Delete**: Click **Delete** on the right of a path to remove the corresponding configuration row.

4. Click **Confirm** to finish defining application resources.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Tip: How do I obtain application paths?</strong></div>


<div data-tips="true" data-tips-type="tip">If you do not know the specific URL paths of the target application, especially the API paths behind pages, use the following methods:</div>



* <div data-tips="true" data-tips-type="tip"><strong>Reverse lookup from logs (recommended)</strong>: First configure a policy that allows access to all paths (<code>/*</code>). Then observe employees' actual access records in <strong>Audit Logs</strong>. The gateway automatically reconstructs all request traces behind the pages. You can extract the real action API paths for precise configuration.</div>


* <div data-tips="true" data-tips-type="tip"><strong>Provided by developers</strong>: Request the Admin Console path, such as <code>/admin</code>, or a list of sensitive APIs, such as <code>/api/export</code>, from the developers of the target application.</div>



 &nbsp;

<span id=".566h55CGLXdlYi3lupTnlKg="></span>
## Manage Web applications

On the **Client Access** tab of the **Web App** list page, you can maintain defined resources.


* **Edit**: Open the target application details page and modify basic application information, effective access points, resource paths, and more. When modifying effective access points, you can select only proxy gateway clusters. The selected cluster scope must be included in the effective cluster scope of the corresponding proxy application.

* **Delete**: Remove Web application resources that are no longer used. Before deletion, ensure that the resource is not referenced by any fine\-grained control policy.


You can view configuration change records for applications published to clusters in **Admin Log** under **Audit Logs**.

 &nbsp;

<span id=".5ZCO57ut5pON5L2c"></span>
## Next steps

After defining Web application resources, go to the **Zero Trust Access** \> **Proxy Policy** \> **Fine\-Grained Control** policy tab to configure specific authorization rules. For details, see [Configure fine-grained control policies in proxy mode](https://docs.byteplus.com/en/docs/sealsuite/configure-proxy-mode-fine-control-strategy).
