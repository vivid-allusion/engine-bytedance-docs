---
title: "Best practices for remote work scenarios"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/Best-practices-for-VPN-management"
---

This article aims to provide IT Administrators and cybersecurity experts with a diversified practical guide to applying VPNs in corporate network management. With SealSuite's flexible VPN configuration options, companies can develop a set of VPN network solutions tailored to specific needs.

<span id="fd8b7c2c"></span>
# Feature overview

SealSuite's VPN management module offers a range of functions, including VPN gateway configuration, permission management, ACL Policy, and Split Tunnel Mode settings. Companies can grant employee VPN access permissions through these features and manage ACL policy connecting to the VPN. SealSuite enhances the stability and speed of VPN tunnels, supports one\-click connection, and automatically selects the optimal VPN gateway, ensuring secure access to teleworking and cloud business systems.

<span id="0a1dfedd"></span>
# Scenario one: Configuring remote working practice for employees

<span id="c3deed24"></span>
## **Scenario introduction**

This scenario is designed for enterprise employees who often travel and need remote access to their corporate intranet systems. SealSuite VPN simplifies client operation with a click\-to\-connect feature, making it easy to establish a VPN connection and effectively solve this challenge. In addition, SealSuite VPN also enforces zero trust practices by enabling MFA verification for VPN connection.

Prerequisite is to deploy at least one VPN gateway and configure an ACL policy successfully for the gateway. Employees only need to log in to the SealSuite VPN client to connect to the corporate intranet with one click by connecting to the VPN gateway.


|**VPN gateway** |**Example Configuration** |**Final Effect** |
|---|---|---|
|Node A |* Enable Split Tunnel Mode<br><br>* Add domain A as a single node resource for Split Tunnel Mode |Employees can connect to VPN through node A using the SealSuite client, which allows them to access domain A via corporate intranet traffic. |
|Node B |* Activate Split Tunnel Mode<br><br>* Add domain B as a single node resource for Split Tunnel Mode |Employees can connect to VPN through node B using the SealSuite client, which allows them to access domain B via corporate intranet traffic. |


<span id="50291323"></span>
## **Procedure**


1. Log in to the SealSuite Admin Console.

2. In the left\-hand navigation bar, select **VPN** ＞ **VPN Gateway**.

3. On the **VPN Gateway** management page, at the top right corner, click **Add New Gateway**.

   In SealSuite's Admin Console, you should add VPN gateway according to your enterprise's specific needs. For specific operations, please refer to [Adding VPN gateway](https://docs.byteplus.com/docs/sealsuite/docs-adding-a-vpn-gateway). If you have already added VPN gateway, you can skip this step.

4. Configure global resources for **Split Tunnel Mode**.

   Configuring split tunnel mode is to ensure only selected network resources will route through the gateway, while the rest will route through public network. This ensures the optimal user experience and least network connection issue.

   1. In the left navigation bar, select **VPN Gateway** ＞ **Advanced Settings**.

   2. On the **Advanced Settings** page of the VPN, in the **Split Tunnel Mode** section, click **Add New Resource**.

   3. In the **Add Resource** interface, configure the network resources to be routed through the VPN tunnel according to your needs and click **Confirm**.

      You can choose to configure either \*\*Domain \*\*or, **IP address**, or both. For example, if you only need the internal websites`www.example.com` to go through the VPN tunnel, then you add `www.example.com` to the **Static domain name list** and set the corresponding IP list for that domain.

5. On the **VPN Gateway** page, find the VPN gateway that has been enabled, and click on the node card to enter the gateway details.

6. In the gateway details page, click on the **Network mode** tab, click **Edit** on the right side of the page, and complete the following configurations, and click **Save**.

   
   |**Configuration Item** |**Description** |
   |---|---|
   |Network mode |You can choose between **Full Tunnel Mode** and **Split Tunnel Mode**.<br><br>Selecting both when you allow users to use the gateway under both mode. Please configure the split mode resource as described above. |
   |Enable single gateway routing under split tunnel mode |Toggle on the **Enable single gateway routing under split tunnel mode** switch.<br><br>Only if we have resources that are dedicated to specific gateway and should not route to other gateway.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After toggling this switch on, the current VPN node will use only the single node resources under Split Tunnel Mode, and will not utilize all resources under <strong>Split Tunnel Mode</strong> from the <strong>Advanced Settings</strong>.</div><br> |
   |Add New Resource |Click **Add New Resource**, add the specified single gateway resource in the **Add Resource** panel on the right, and click **Confirm**.<br><br>You can choose to configure either \*\*Domain \*\*or, **IP address**, or both. For example, if you only need the domain `www.example.com` to go through the VPN tunnel, then you add `www.example.com` to the **Static domain name list** and set the corresponding IP list for that domain. |
   

7. In the left navigation pane, select **VPN** ＞ **Access Permission** to manage who have access to the VPN function on the client.

8. In the upper right corner of the **Access Permission** tab, click **Add Permissions**.

   You need to manage VPN permissions in the SealSuite Admin Console based on the actual situation of the enterprise. For specific operations, please refer to [Adding VPN access permissions](https://docs.byteplus.com/docs/sealsuite/docs-adding-vpn-access-permissions_2).

9. In the left navigation pane, select **VPN** ＞ **ACL Policy** to manage the access policies.

   You need to manage VPN permissions in the SealSuite Admin Console based on the actual situation of the enterprise. For specific operations, please refer to [Managing access control rules](https://docs.byteplus.com/docs/sealsuite/docs-managing-access-control-rules_2).

10. Set the VPN ACL Policy to **Open Access Mode**.

   Choose Open Access Mode if you are only managing a small sets of restricted resources. Choose Closed Network Mode only if you want to implement stringent network control in your network environment with whitelisted websites. We recommend the Open Access Mode to ensure best end\-user convenience.

11. In the left navigation pane, select **VPN** ＞ **ACL Policy**.

12. On the **VPN Access** page, select **Open Access Mode**.

   * If you are setting this up for the first time, you need to click on **Open Access Mode**, and then click on **Next**.

      On the create a network resource page, click on **Jump out of the process**. Subsequently, you can add network resources and access rules on your own.

   * If you have previously created network resources and access rules, you need to click on **Switch** in the upper left corner of the page, and select **Open Access Mode** in the pop\-up dialog.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f0552387d7f74237a256f39090c06fe8~tplv-goo7wpa0wc-image.image) </span>


<span id="834ea64a"></span>
## **Results**

When company employees log in to the SealSuite VPN client through their personal devices and successfully establish a connection, they will be able to access the company's internal network resources and implement remote work. By connecting to either split tunnel mode or full tunnel mode under the selected VPN gateway after MFA verification.

<span id="e74e3329"></span>
# Scenario two: Allow designated departments to access specified resources

<span id="ad4987c1"></span>
## **Scenario introduction**

In this scenario, we choose to set the VPN Access mode to **Closed Network Mode**, and through the access rules, we ensure that employees can only access specific network resources they need for their work after connecting to the VPN. In this mode, unauthorized access is automatically blocked, thus significantly reducing potential security risks. At the same time, this strategy also helps to simplify network management, as the administrator only needs to define the resources allowed for access, instead of restricting each resource's access one by one.

<span id="5d5bfbdc"></span>
## **Procedure**


1. Log in to the SealSuite Admin Console.

2. In the left\-hand navigation bar, select **VPN** ＞ **VPN Gateway**.

3. On the **VPN Gateway** management page, at the top right corner, click **Add New Gateway**.

   In SealSuite's Admin Console, you should add VPN gateway according to your enterprise's specific needs. For specific operations, please refer to [Adding VPN gateway](https://docs.byteplus.com/docs/sealsuite/docs-adding-a-vpn-gateway). If you have already added VPN gateway, you can skip this step.

4. Configure allow access policies for the main and backup DNS ports 53 for the VPN.

   Before setting up the **Closed Network Mode**, you need to first add an access rule to allow traffic on the main and backup DNS ports 53 of the VPN. Otherwise, setting to **Closed Network Mode** will result in the services being inaccessible.

   1. In the left\-hand navigation bar, select **VPN** ＞ **ACL Policy**.

   2. Click on the **Network Resources** tab and click **Add New Resource**.

   3. In the **Add Resource** dialog, complete the configurations and click **Confirm**.

      
      |**Configuration Item** |**Description** |
      |---|---|
      |Resource name |Enter a custom name used to identify the network resource. |
      |Resource group |Network resources support categorization through tags, and these tags can later be used in bulk settings for network resources when configuring access rules. |
      |Resource Type |Select **IP Address**. |
      |Protocols |Select the corresponding protocol for **Domain**, supporting the selection of **All**, **https,**  or **http**, or the protocol followed by the **IP Address**, supporting the selection of **all**, **tcp**, **udp** or **icmp**, with support for multiple selections. |
      |Domain name list |Add the IP addresses of the DNS primary and secondary servers under the VPN gateway to the IP List. |
      |Port list |Add port 53 to the Port list. |
      

5. On the **VPN Access** page, click **Switch**.

6. In the **Switch default mode** dialog, click **Closed Network Mode**, and then click **Confirm**.

7. Set up access policy under Closed Network Mode.

   When the VPN access mode is switched to **Closed Network Mode**, by default employees will not be able to access any network resources, and you will need to add access rules to allow access to specific network resources based on the actual needs of the corporation. Subsequently, employees connected to the corporate intranet via VPN will be able to access network resources within the effective scope of the rule.

   1. On the **VPN Access** page, click the **Network Resources** tab, and within the tab click **Add New Resource**.

   2. In the **Add Resource** dialog, configure network resources, and click **Confirm**.

      
      |**Configuration Item** |**Description** |
      |---|---|
      |Resource name |Enter a custom name used to identify the Network Resource. |
      |Resource group |Network resources support categorization through tags, and these tags can later be used in bulk settings for network resources when configuring access rules. |
      |Resource Type |Select to configure **Domain** or **IP address**. For example, if you need to add `www.example.com` as a network resource, select **Domain** as resource type, and add `www.example.com` to the **Domain Name List**. |
      |Protocols |Select the corresponding protocol for **Domain**, supporting the selection of **All**, **https,**  or **http**, or the protocol followed by the **IP Address**, supporting the selection of **all**, **tcp**, **udp** or **icmp**, with support for multiple selections. |
      |Domain Name List |* Set the domain names included in the network resources, required to include port information (80 and 443 ports are added by default), format example: `www.example.com:80`. When adding multiple domain names, use commas or spaces to separate them.<br><br>* Set the necessary port list for network resources, supporting single ports (for example, 80), or port ranges (for example, 0\-65535). When adding multiple ports, use commas or spaces to separate them. |
      |Port list |Set the necessary port list for network resources, supporting single ports (for example, 80) or port ranges (for example, 0\-65535). When adding multiple ports, use commas or spaces to separate them. |
      

   3. On the **VPN Access** page, click the **Access Rule** tab, and within the tab, click **New Policy**.

   4. In the **Add Access Rule** dialog, complete the following configurations, and click **Confirm**.

      
      |**Configuration Item** |**Description** |
      |---|---|
      |Toggle permission |Click **Change** to set up **Grant employee access to the selected resources**. |
      |Policy Name |Enter a custom name used to identify the policy. |
      |Select resource |In the **Select resource** configuration item, choose the already created `www.example.com` network resources. |
      |Priority |Set to 100. The higher the value, the higher the priority of policy implementation. |
      |User Scope |Select **Department**, and choose the specified department range (for example, select Department A). Members within the department range will be the scope of the current policy. |
      |Expiration |Set to **Permanent**. |
      


<span id="a1469b51"></span>
## **Results**

After logging into the SealSuite client and connecting to the VPN, all employees from Department A can access `www.example.com`. Employees from other departments cannot access network resources after logging into the SealSuite client and connecting to VPN.

<span id="becac1a5"></span>
# Scenario three: Configure a dedicated Split Tunnel Mode resource for a single VPN node

<span id="c2c590ba"></span>
## **Scenario introduction**

This scenario is primarily to demonstrate how to configure a dedicated Split Tunnel Mode resource for a specific VPN node within SealSuite VPN management. This configuration allows a specific VPN node to access particular network resources, rather than global resources, thus achieving more refined network resource management and optimization.

In this scenario, we will detail how to configure a dedicated Split Tunnel Mode resource for a VPN node. By following the steps in this scenario, you can configure similar settings for multiple VPN gateway to achieve optimal performance and resource access for each node. For instance, if you have two VPN gateway, you can configure each of them as shown in the example below to achieve access to specific network resources for each node. Here is an example configuration for two VPN gateway and an explanation of the final effect:


|**VPN gateway** |**Example Configuration** |**Final Effect** |
|---|---|---|
|Node A |* Enable Split Tunnel Mode<br><br>* Add domain A as a single node resource for Split Tunnel Mode |Employees can connect to VPN through node A using the SealSuite client, which allows them to access domain A via corporate intranet traffic. |
|Node B |* Activate Split Tunnel Mode<br><br>* Add domain B as a single node resource for Split Tunnel Mode |Employees can connect to VPN through node B using the SealSuite client, which allows them to access domain B via corporate intranet traffic. |


<span id="2fc222ee"></span>
## **Procedure**


1. Log in to the SealSuite Admin Console.

2. In the left\-hand navigation bar, select **VPN** ＞ **VPN Gateway**.

3. On the **VPN Gateway** management page, at the top right corner, click **Add New Gateway**.

   In SealSuite's Admin Console, you should add VPN gateway according to your enterprise's specific needs. For specific operations, please refer to [Adding VPN gateway](https://docs.byteplus.com/docs/sealsuite/docs-adding-a-vpn-gateway). If you have already added VPN gateway, you can skip this step.

4. In the left\-hand navigation bar, select **VPN** ＞ **VPN Gateway**.

5. On the **VPN Gateway** page, find the enabled VPN gateway, click on the node card to enter the gateway details page.

6. On the gateway details page, click the **Network mode** tab, click **Edit** on the right side of the page, complete the following configurations, and click **Save**.

   
   |**Configuration Item** |**Description** |
   |---|---|
   |Network mode |Select only **Split Tunnel Mode**. |
   |Enable single gateway routing under split tunnel mode |Toggle on the **Enable single gateway routing under split tunnel mode** switch.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After toggling this switch on, the current VPN node will use only the single node resources under Split Tunnel Mode, and will not utilize all resources under <strong>Split Tunnel Mode</strong> from the <strong>Advanced Settings</strong>.</div><br> |
   |Add New Resource |Click **Add New Resource**, add the specified single gateway resource in the **Add Resource** panel on the right, and click **Confirm**.<br><br>You can choose to configure either \*\*Domain \*\*or, **IP address**, or both. For example, if you only need the domain `www.example.com` to go through the VPN tunnel, then you add `www.example.com` to the **Static domain name list** and set the corresponding IP list for that domain. |
   


<span id="4458d8e8"></span>
## **Results**

Employees must connect to the specified VPN node through the SealSuite client to access the resources at `www.example.com` via the VPN\-encrypted tunnel. If connected to a non\-specified VPN node, they will not be able to access the resource.
