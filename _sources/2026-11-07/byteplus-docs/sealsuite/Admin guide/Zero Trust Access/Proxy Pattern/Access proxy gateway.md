---
title: "Access proxy gateway"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/access-proxy-gateway"
---

A **proxy gateway** forwards employee traffic to internal enterprise applications in proxy mode. SealSuite supports clustered gateway deployment. Gateway clusters provide centralized node management and automatic policy inheritance. They also support integration with third\-party load balancing (LB) to provide a high\-availability access entry point and simplify maintenance in large\-scale deployments.

This article describes how to add proxy gateway nodes and configure gateway clusters as needed.

<span id="51485509"></span>
## Prerequisites


* **License requirements**: You have purchased and obtained a **Zero Trust Network Access license**.

* **Server resource requirements**: Prepare a physical machine or virtual machine for gateway deployment. The machine must meet the following requirements:

   * **Operating system**: Debian 11, Ubuntu 20, CentOS 8, or later.

   * **Hardware configuration**:

      * Recommended configuration: 16\-core CPU, 32 GB memory, and 500 GB of disk space.

      * Minimum configuration: 8\-core CPU, 16 GB memory, and 200 GB of disk space.

* **Network allowlist requirements**: Before deployment, ensure that your enterprise network firewall or security group allows relevant traffic based on the following rules, and that correct DNS resolution is configured:

&nbsp;

   
   |**Source address** |**Destination address** |**Protocol and port** |**Description** |
   |---|---|---|---|
   |Proxy gateway |SealSuite Server |TCP 49900 |Used by the gateway to pull traffic routing policies and access control list (ACL) policies from the SealSuite server and report logs. |
   |Proxy gateway |Proxy application |Port of the proxy application |Used by the gateway to proxy access to applications that need to be published. |
   |SealSuite client |Proxy gateway |Custom TCP port (443 recommended)<br><br>All UDP ports |Used to establish traffic routing channels and transmit data. |
   |SealSuite client |SealSuite Server |TCP 10443<br><br>Use the actual port configured for your enterprise SealSuite Server |Used by the client to obtain traffic routing policies, gateway nodes, application lists, and more. |
   

* **DNS resolution**: The proxy gateway must be configured with a DNS server that can correctly resolve internal business domain names.


<span id="3cfd4bcc"></span>
## Add a proxy gateway node

Adding a gateway node involves three stages: **Basic Information**, **Deploy**, and **Connectivity Test**.


1. Log in to the SealSuite Admin Console.

2. In the left navigation pane, choose **Zero Trust Access** \> **Gateway Config**.

3. At the top of the page, switch to the **Proxy Gateway** tab.

4. In the lower\-left corner of the page, click **Create New Gateway**.

   <span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/2026-09-18/proxy-bordered/full-create-new-border.png) </span>

5. On the **Configure proxy gateway node** page, complete the following configuration.

   * **Basic Information**

   
   |Configuration item |Description |
   |---|---|
   |**Icon** |Use the default SealSuite icon, or click **Upload Icon** to upload a custom icon. |
   |**Name** |Enter a descriptive name for the gateway node. Names in multiple languages are supported. |
   |**Tag** |(Optional) Used to group and manage gateways. Select an existing tag from the drop\-down list. If no tag exists in the system, enter a tag name in the input box and click  **+ Add**. The system automatically creates the tag. |
   |**DNS server (primary)** <br><br>**DNS server (backup)**  |Enter the DNS address used by the gateway node to resolve intranet domain names. This ensures that the gateway can correctly locate intranet applications. |
   |**Internal IP** |Enter the actual IP address of the gateway node on the LAN. |
   |**External Address** |Set the address used by clients to connect to the gateway. For an intranet\-only office scenario, you can also enter the address used to access the gateway on the intranet. Select one of the following modes based on your network environment:<br><br><br>* **Public IP**: Enter the IPv4 address used to access the gateway from the public network or office network.<br><br>* **Domain**: Enter the fully qualified domain name (FQDN) of the gateway, such as `gw.corp.com`. Do not enter a protocol prefix, URL path, query parameters, or spaces.<br><br>   If this field is configured as a domain name, ensure that end users have upgraded their SealSuite client to **3.3.17 or later**. Otherwise, clients cannot connect. |
   |**Cluster** |**Optional when creating the node.**  You can select a cluster from the drop\-down list now or add the node to a cluster after creating it. **The node must belong to a cluster before it can handle client access requests.**  After joining a cluster, the node inherits the external address configuration of the cluster and participates in traffic distribution as part of the cluster resource pool.<br><br>If no cluster has been created, click **Cluster configuration** to quickly go to the cluster configuration page and create a cluster. For details, see [Manage proxy gateway clusters](https://docs.byteplus.com/en/docs/31/121782#74305092). You can also create a cluster after creating the proxy gateway, and then add the node to the cluster.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div><br><br><br><div data-tips="true" data-tips-type="warning">The SealSuite client implements application proxying by connecting to the cluster address. If a node is not added to a cluster, it cannot receive and process access requests from clients.</div><br> |
   |**Port** |Set the port on which the gateway listens, such as `8001`. Ensure that the server firewall allows inbound traffic on this port. |
   |**Enable encryption** |(Optional) **We strongly recommend that you enable this option**. After it is enabled, the proxy channel between the client and the proxy gateway is encrypted. If you disable it and the service accessed by employees uses a plaintext protocol, such as HTTP or Telnet, data transmitted over the public network faces an extremely high risk of packet capture and eavesdropping. Disable this option only in special test environments that are intranet\-only and fully trusted. |
   

   * **Deploy**

      Click **Next Step** to enter the deployment and installation phase. Log in to the Linux server and run the download and installation script provided on the page. The script automatically completes environment checks, software download, and service initialization.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Caution   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>For private deployments</strong>: The installation command for the proxy gateway component includes the communication address of the SealSuite Admin Console (Server), such as <code>sudo ./install.sh https://<Server_IP>:49900</code>. If your SealSuite Admin Console is deployed as a high\-availability (active/standby) cluster, manually replace the single IP address in the command with the virtual IP (VIP) of the cluster or the domain name used to access the cluster before you run the command. This prevents service interruption caused by the gateway losing connectivity during an active/standby switchover.   </div>
   

   * **Connectivity Test**

      After installation is complete, return to the SealSuite Admin Console and click **Next Step** to enter the connectivity test. Click **Start detection**. The system automatically checks the connectivity between the gateway node and the SealSuite Admin Console, and whether the gateway can access typical intranet resources.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Caution   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>For private deployments</strong>: Ensure that the SealSuite Server Portal is configured with a certificate issued by a trusted certificate authority (CA). If a self\-signed certificate is used, the gateway cannot pass the underlying HTTPS certificate verification. This causes the "connectivity test" to fail and the gateway to go offline.   </div>
   

After the test succeeds, click **Done**.

<span id="74305092"></span>
## Manage proxy gateway clusters

Gateway clusters are the core solution for enterprise\-grade access and high availability. By aggregating multiple discrete gateway nodes into a logical cluster, you can configure a unified third\-party load balancing (LB) entry point. The availability of the entry point depends on the load balancer and gateway deployment.

A proxy gateway cluster can contain one or more nodes. You can create a cluster that contains only one node to host an independent access entry point. After an application is published to a cluster, it takes effect on all nodes in the cluster. When a new node joins the cluster, it automatically inherits the applications published to the cluster, and no republishing is required. When a node is removed from the cluster, the application associations inherited from the original cluster are automatically removed.


1. Log in to the SealSuite Admin Console.

2. In the left navigation pane, choose **Zero Trust Access** \> **Gateway Config**.

3. At the top of the page, switch to the **Proxy Gateway** tab.

4. In the upper\-right corner of the **Proxy Gateway** tab, click **Cluster configuration**.

   <span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/2026-09-18/proxy-bordered/full-cluster-new-border.png) </span>

5. In the **Cluster configuration** dialog box, click **Create Cluster** and configure the following information:

&nbsp;

   
   |Configuration item |Description |
   |---|---|
   |**Cluster Name** |Enter an easy\-to\-identify cluster name. |
   |**Cluster Address** |Set the unified entry point used by clients to access the cluster. Enter the address based on your networking plan.<br><br><br>* **Load balancing mode (recommended)** : If you have deployed a third\-party LB, enter the unified domain name or virtual IP (VIP) of the LB. The client connects to this address, and the LB distributes traffic to provide high availability.<br><br>* **Single\-gateway/direct connection mode**: If you have not deployed an LB and only want to use a cluster for logical management and policy inheritance, directly enter the public domain name or IP of the primary gateway node in the cluster.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div><br><br><br><div data-tips="true" data-tips-type="warning"><strong>Version requirement</strong>: If the cluster address is configured as a <strong>domain name</strong>, ensure that end users have upgraded their SealSuite client to <strong>3.3.17 or later</strong>. Earlier client versions cannot recognize access points in domain name format. As a result, they cannot access proxy applications associated with the cluster.</div><br> |
   |**Port** |Set the port used by the cluster to provide external services. Ensure that the firewall allows inbound traffic on this port at the access entry point, such as a third\-party load balancer or the gateway node itself. |
   |**Enable encryption** |Specify whether to encrypt cluster traffic during transmission. |
   |**Select Proxy Gateway** |Select gateway nodes to add to the cluster from the currently created gateway nodes.<br><br>After joining the cluster, these nodes form a "resource pool". If a third\-party load balancing (LB) service is also integrated, traffic is distributed by the LB to healthy nodes in the pool when clients access the cluster address.<br><br>The cluster must contain at least one node in the "Running" state to handle client access requests. |
   

6. Click **Confirm** to create the cluster.


<span id="a02cc630"></span>
## Maintenance and status monitoring

<span id="hBgmzGwn6"></span>
### Gateway nodes

On the proxy gateway list page, you can monitor gateway running status in real time and perform maintenance tasks.


* **Quick search and filtering**: In the search area above the list on the left, search by keyword or filter by **Tag**, **Name**, **Status**, or **Cluster Name** to quickly locate the target gateway in large\-scale deployments.

* **Monitor running status**: In the node list on the left, quickly evaluate gateway health based on the status indicator in the lower\-right corner of each node.

* **Maintenance tasks**:

   * **View details**: Click a node name in the list. The right pane displays the gateway details and component ID and secret used for manual installation or troubleshooting.

   * **Edit configuration**: Click the **Edit** button in the upper\-right corner to modify basic information such as the IP address, port, and DNS of the gateway.

   * **Delete Gateway**: If the gateway server has been retired, click **Delete Gateway** to remove it from the backend. Before deleting a gateway, ensure that no "proxy application" uses this gateway as its only access point. Otherwise, associated applications become inaccessible.


<span id="hnYol28EF"></span>
### Clusters

In the upper\-right corner of the **Proxy Gateway** tab, click **Cluster configuration** to view and manage created proxy gateway clusters.


* **Search clusters**: Enter a cluster name in the search box above the list to find the target cluster.

* **View cluster information**: View the cluster name, cluster address, port, whether encryption is enabled, and the proxy gateway nodes included in the cluster. Click the refresh button to update the list.

* **Create a cluster**: Click **Create Cluster**, configure cluster information, and add proxy gateway nodes. A cluster can contain one or more nodes. A cluster with no nodes does not appear in the cluster selection list on the client.

* **Edit a cluster**: In the **Action** column of the target cluster, click **Edit** to adjust cluster configuration. A node can belong to only one cluster at a time. After a node joins a cluster, it automatically inherits the applications published to the cluster. After the node is removed from the cluster, the application associations inherited from the original cluster are automatically removed. Before adjusting proxy gateway nodes in an online cluster, confirm that the cluster still has available nodes to handle application access.

* **Delete a cluster**: In the **Action** column of the target cluster, click **Delete** to delete a cluster that is no longer used. A cluster cannot be deleted while applications are associated with it. Deleting a cluster unbinds its nodes without deleting them. Historical audit logs and connection logs are retained.


<span id="227f5d9e"></span>
## Next steps

After the proxy gateway node is deployed successfully and its status is "Running", complete the following configuration to enable zero trust access in proxy mode:


1. Go to **Zero Trust Access** \> **Application** \> **Proxy App** to publish internal business resources to a proxy gateway cluster. For details, see [Manage proxy applications](https://docs.byteplus.com/en/docs/sealsuite/management-agent-mode-application-resources).

2. Go to **Zero Trust Access** \> **Proxy Policy** to configure traffic routing and access permissions.

   * **Traffic routing policy**: Delivers the address range of an application to clients and steers traffic to the proxy gateway. For details, see [Configure a proxy mode traffic routing policy](https://docs.byteplus.com/en/docs/sealsuite/configuring-proxy-mode-traffic-diversion-strategy).

   * **ACL policy**: Grants access to specific applications based on employee identity or device attributes. For details, see [Configure ACL policies for proxy mode](https://docs.byteplus.com/en/docs/sealsuite/configure-proxy-mode-acl-policy).

3. (Optional) If your enterprise requires additional authentication, go to **Identity** \> **Account Setup** \> **MFA Setup** to enable secondary authentication for the **Employee Proxy** scenario. This strengthens access security. For details, see [Configuring multi-factor authentication (MFA)](https://docs.byteplus.com/en/docs/sealsuite/docs-configuring-multi-factor-authentication-mfa-).
