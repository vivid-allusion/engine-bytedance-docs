---
title: "Manage proxy applications"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/management-agent-mode-application-resources"
---

A **proxy application** is the basic unit that defines internal network access targets in proxy mode. To let employees securely access internal business systems, such as code repositories, financial systems, and office automation platforms, through the SealSuite proxy gateway, you must first register the network addresses of these systems, such as IP addresses and domain names, as proxy applications. After creating proxy applications, you can select them in traffic routing policies and configure their access permissions in ACL policies.

This document describes how to manage proxy applications in SealSuite.

 &nbsp;

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Make sure you have successfully created a **gateway cluster** and added at least one associated node on the **Zero Trust Access** \> **Gateway Config** \> **Proxy Gateway** page, as described in [Connect a proxy gateway](https://docs.byteplus.com/en/docs/sealsuite/access-proxy-gateway).

 &nbsp;

<span id=".5re75Yqg5Luj55CG5bqU55So"></span>
## Add proxy applications


1. Log in to the SealSuite Admin Console.

2. In the left navigation pane, choose **Zero Trust Access** \> **Application**.

3. At the top of the page, switch to the **Proxy App** tab.

   <span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/2026-09-24/proxy-en-review/border-proxy-app-list.png) </span>

4. (Optional) To group proxy applications by business type, such as "R&D systems" and "financial systems", click **Create label** for the first tag or **Add label** for subsequent tags in the **Label** area on the left side of the page to define tags.

5. Click **Add Application** on the right side of the page.

6. On the Add Application page, configure the following basic information.

   * **Software name**: Enter an application name that is easy to identify. Multilingual configuration is supported.

   * **Description**: We recommend entering supporting information based on your needs, such as the application's business attributes, owners, or configuration background, to simplify later identification and maintenance.

   * **Tag**: Select a tag created in step 4 from the drop\-down list for the application. After you associate tags, you can select all applications in the category at once by using "Tag" when configuring an ACL policy or traffic routing policy. This simplifies large\-scale resource authorization.

   * **Effective access point**: Specify the gateway clusters to which the application is published. Applications are published and managed at the cluster level. If a proxy gateway node has not been added to a cluster, first create a cluster and associate the node as described in [Manage proxy gateway clusters](https://docs.byteplus.com/en/docs/sealsuite/access-proxy-gateway#74305092). This configuration mainly applies to multi\-region or multi\-data center network isolation scenarios. For example, if an internal application is reachable only within the LAN of the "Beijing data center", specify the "Beijing proxy gateway cluster" here to ensure that clients access the application through that specific cluster gateway.

      * **All Clusters**: The default option. The application takes effect in all created proxy gateway clusters.

      * **Partial Clusters**: Manually select specific gateway **clusters**. The application routes and permission policies are delivered only to the selected clusters and their member nodes.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Access inheritance and scheduling</strong>   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Node added to a cluster</strong>: The new node automatically inherits all application configurations published to the cluster. You do not need to publish the applications again.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Node removed from a cluster</strong>: The application publishing relationships inherited by the node from the original cluster are automatically removed. Before changing cluster members, make sure the cluster still has available nodes to handle application access.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Client cluster selection</strong>: SealSuite measures the latency of proxy gateway clusters and prioritizes low\-latency access paths for end users. Administrators can use <a href="https://docs.byteplus.com/en/docs/sealsuite/configure-proxy-mode-client-access-policy">Configure proxy mode client access policies</a> to allow or restrict manual cluster selection and specify which clusters employees can select.   </div>
   

   * **Application Address**: Click **Add address** on the right to add an address.

      * **Protocol**: Select a protocol based on the actual service protocol of the application. Options include **All**, **TCP**, and **UDP**. ICMP is not supported.

      * **Type**: Select the address type to enter: **Domain name** or **IP address**. For non\-TCP protocols, we generally recommend defining resources by IP address.

      * **Server address**: Based on the selected resource type, enter the corresponding domain name or IP information. Batch input is supported. Separate multiple records with line breaks.

         * **Domain name**: Applies to services accessed by URL, such as `git.corp.com`. Wildcards are supported. For example, entering `*.corp.com` matches all subdomains under that suffix.

         * **IP address**: Applies to services accessed by fixed IP address or CIDR block. IPv4 and IPv6 are supported. You can enter a single IP address, such as `10.1.1.1` or `2001:abcd:0:0:0:0:0:1`, an IP range, such as `10.1.1.1-10.1.1.10` or `2001:abcd::1-2001:abcd::10`, or a CIDR block, such as `10.1.1.0/24` or `2001:db8::/32`.

      * **Port list**: Enter the port numbers on which the application provides external services. A single port, such as `80`, and a port range, such as `1-65535`, are supported. For batch input, separate entries with commas or line breaks. Only traffic sent to the specified ports is proxied by the gateway. Requests to undefined ports are blocked, enabling minimum authorization at the service level. To allow all ports, enter `1-65535`.

   * **Quick Add**

      If you have maintained commonly used enterprise domain names or IP resource libraries in advance on the **System Settings** \> **Resource Management** \> [Address Management (Chinese)](https://help.feilian.cn/help-center/configuration-address-management) page, enable **Quick Add** to reference resources. Click **Select Application**, then select the address resources to reference from the resource library list.

7. After confirming that the configuration is correct, click **Confirm** at the bottom of the page to save the configuration.


 &nbsp;

<span id=".566h55CG5Luj55CG5bqU55So"></span>
## Manage proxy applications

Administrators can search, maintain, or clean up created application resources on the proxy application list page.


* **Quick search**

   * **Search by condition**: Supports keyword search by application name or application address (IP address or domain name), and quick filtering by gateway cluster or protocol type.

   * **Filter by tag**: Click a tag in the **Label** area on the left to view applications in that category.

* **Modify configuration**: Click **Edit** in the operation column on the right side of the target application to modify information such as the application name, tag, effective access point, or specific address and port. After changing the effective access point of an application, go to **Audit Logs** \> **Admin Log** to view the operation record and trace the operator, operation time, and configuration change details.

* **Delete resources**: Click **Delete** in the operation column on the right side of the target application to remove an application resource that is no longer used. Before deletion, make sure the application is not referenced by any **traffic routing policy** or **ACL policy**. Otherwise, legitimate access requests may be unexpectedly blocked, or sensitive traffic may not be diverted correctly.


 &nbsp;

<span id=".5ZCO57ut5pON5L2c"></span>
## Next steps

After a proxy application is created, it exists in the system only as a "resource". To enable actual network connectivity and permission control, you must also:


1. Go to **Proxy Policy** \> **ACL Policy** and configure authorization rules that allow specific groups to access the application. For more information, see [Configure proxy mode ACL policies](https://docs.byteplus.com/en/docs/sealsuite/configure-proxy-mode-acl-policy).

2. Go to **Proxy Policy** \> **Traffic Routing** and configure routing rules that direct target client traffic to the proxy gateway. For more information, see [Configure proxy mode traffic routing policies](https://docs.byteplus.com/en/docs/sealsuite/configuring-proxy-mode-traffic-diversion-strategy).
