---
title: "Best practices for global network management through SD-WAN"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/best-practices-for-global-network-management-through-sd-wan"
---

This article aims to provide IT administrators with customized network solutions, simplifying corporate network deployment and management. It covers both domestic and international networking and routing policy configuration, helping enterprises achieve network performance optimization and compliant cross\-border access.

<span id="4605ee88"></span>
# Feature overview

As enterprises increasingly demand enhanced network performance and flexibility, SD\-WAN (Software\-Defined Wide Area Network) technology has become a key component of modern IT infrastructure. SealSuite SD\-WAN offers an innovative network solution that helps businesses simplify configurations, reduce costs, and improve network performance. Based on the global SD\-WAN network of SealSuite, SealSuite SD\-WAN network supports the following key features through hardware CPE, software CPE, and cloud VPN components:


* **Network interconnectivity and interoperability**: Connects dispersed workplaces and data centers to achieve comprehensive network integration.

* **Compliant cross\-border access**: Provides access to international resources while ensuring compliance.

* **Resource\-intelligent route selection**: Automatically selects the best path based on real\-time network conditions, reducing latency.


<span id="9d6edde3"></span>
# Scenario 1: Connecting domestic office networks

<span id="7bd20da3"></span>
## **Scenario introduction**

In traditional networking, domestic workplace/branch network connections often face complex configurations, high maintenance costs, and long deployment cycles. SealSuite SD\-WAN offers an efficient domestic branch networking solution by simplifying configurations and reducing costs.

<span id="fcba5d5e"></span>
## **Procedure**


* **Deploy software CPE**: Launch software CPE at each branch office.

   1. Log in to the SealSuite Admin Console.

   2. In the left navigation bar, select **SD\-WAN** \> **Branch Gateway**.

   3. In the upper right corner of the **Gateway** page, select **Add Branch** \> **Software**.

   4. On the **Add Branch** page, complete the following configurations.

      1. On the **Basic configuration** interface, complete the following configuration items and click **Next Step**.

         
         |**Configuration Item** |**Description** |
         |---|---|
         |**Branch Name** |Customize the Chinese and English names for the branch gateway, used to identify the specific gateway. |
         |**Branch Gateway Type** |Used to identify the enterprise institution corresponding to the branch gateway:<br><br><br>* **Office Branch**: Indicates a gateway associated with an enterprise's branch office.<br><br>* **Headquarter**: Indicates a gateway associated with the enterprise's headquarter.<br><br>* **Data Center**: Indicates a gateway related to the Internet Data Center (IDC) room.<br><br>* **Public Cloud**: Indicates a gateway associated with a public cloud service provider.<br><br>* **Other**: This is a generic option for identifying other types of enterprise institutions or network locations. |
         |**Source network address translation (SNAT)**  |SNAT is used to obscure internal network addresses and resolve private network address conflicts.<br><br><br>* **Enable**: It is recommended to enable the SNAT configuration. Select **Enable** when the branch network segment of the current branch gateway conflicts with other branch network segments. After enabling SNAT, SealSuite will automatically generate a branch network segment for the branch gateway and use this segment to communicate with the SealSuite public cloud.<br><br>* **Not applicable**: If SNAT is not enabled, you need to manually set up the branch network segment for the branch gateway. Once setup is completed, SealSuite will automatically distribute the corresponding branch network segment to each SealSuite entry point (POP node) to facilitate network communication between the branch gateway and the SealSuite public cloud. |
         |**DNS proxy** |DNS proxy is a network service for proxying client DNS query requests:<br><br><br>* **Enable**: It is recommended to enable the DNS proxy. After enabling, if the internal network PC points the DNS server address to the LAN port of the branch gateway, the branch gateway will use the primary and secondary DNS server addresses configured here for DNS proxy resolution.<br><br>* **Not applicable**: If the DNS proxy feature is disabled, internal network PCs cannot point the DNS server address to the LAN port of the branch gateway. |
         |**High Availability** |Enabling high availability on devices increases the system's redundancy and reliability. If one node fails or is interrupted, another node can take over the work, ensuring the continuity and availability of the branch.<br><br><br>* **Enable**: It is recommended to enable the High Availability option. After enabling high availability, the branch will automatically generate two branch nodes. The two CPE nodes can use floating IP to achieve high reliability, which currently only supports AWS.<br><br>* **Not applicable**: Not enabling high availability means that the system will not automatically generate additional branch nodes, nor does it support floating IP for high reliability. In this case, if a node fails, it may lead to branch interruption or unavailability. |
         

   5. On the **Deploy** interface, follow the component installation command provided by the interface to install the SealSuite branch gateway component on the corresponding Linux system server address, and click **Next**.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If you choose to enable the High Availability feature, then during the deployment process, you will need to complete the deployment steps for both nodes separately.      </div>
      

   6. On the **Connectivity Test** interface, complete the connectivity test according to the information provided by the interface to ensure the server where the branch gateway component is located is interconnected with the SealSuite network, and then click **Confirm**.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If you choose to enable the High Availability feature, then when conducting connectivity testing, you need to ensure that both nodes pass the connectivity test to complete the addition of the branch gateway.      </div>
      

* **Deploy hardware CPE**: if hardware CPE is purchased, deploy hardware CPE at each branch office.

   **Step one**: Add hardware\-based branch gateway in the SealSuite Admin Console.

   1. Log in to the SealSuite Admin Console.

   2. In the left navigation bar, select **SD\-WAN** \> **Branch Gateway**.

   3. In the upper right corner of the **Gateway** page, select **Add Branch** \> **Hardware**.

   4. In the **Add Branch Gateway** interface, complete the following settings in **Basic configuration**, and click **Next Step**.

      
      |**Configuration Item** |**Description** |
      |---|---|
      |**Branch Name** |Customize the Chinese and English names for the branch gateway, used to identify the specific gateway. |
      |**Device model** |Choose **FLG\-X1** or **FLG\-X2** according to the actual device model. |
      |**Branch Gateway Type** |Used to identify the enterprise institution corresponding to the branch gateway:<br><br><br>* **Office Branch**: Indicates a gateway associated with an enterprise's branch office.<br><br>* **Headquarter**: Indicates a gateway associated with the enterprise's headquarter.<br><br>* **Data Center**: Indicates a gateway related to the Internet Data Center (IDC) room.<br><br>* **Public Cloud**: Indicates a gateway associated with a public cloud service provider.<br><br>* **Other**: This is a generic option for identifying other types of enterprise institutions or network locations. |
      |**Source network address translation (SNAT)**  |SNAT is used to obscure internal network addresses and resolve private network address conflicts.<br><br><br>* **Enable**: It is recommended to enable the SNAT configuration. Select **Enable** when the branch network segment of the current branch gateway conflicts with other branch network segments. After enabling SNAT, SealSuite will automatically generate a branch network segment for the branch gateway and use this segment to communicate with the SealSuite public cloud.<br><br>* **Not applicable**: If SNAT is not enabled, you need to manually set up the branch network segment for the branch gateway. Once setup is completed, SealSuite will automatically distribute the corresponding branch network segment to each SealSuite entry point (POP node) to facilitate network communication between the branch gateway and the SealSuite public cloud. |
      |**DNS proxy** |DNS proxy is a network service for proxying client DNS query requests:<br><br><br>* **Enable**: It is recommended to enable the DNS proxy. After enabling, if the internal network PC points the DNS server address to the LAN port of the branch gateway, the branch gateway will use the primary and secondary DNS server addresses configured here for DNS proxy resolution.<br><br>* **Not applicable**: If the DNS proxy feature is disabled, internal network PCs cannot point the DNS server address to the LAN port of the branch gateway. |
      |**High Availability** |Enabling high availability on devices increases the system's redundancy and reliability. If one node fails or is interrupted, another node can take over the work, ensuring the continuity and availability of the branch.<br><br><br>* **Enable**: It is recommended to enable the High Availability option. After enabling high availability, the branch will automatically generate two branch nodes. The two CPE nodes can use floating IP to achieve high reliability, which currently only supports AWS.<br><br>* **Not applicable**: Not enabling high availability means that the system will not automatically generate additional branch nodes, nor does it support floating IP for high reliability. In this case, if a node fails, it may lead to branch interruption or unavailability. |
      

   5. In the **Add Branch Gateway** interface, configure the FLG according to the information provided in the **Device Provisioning** section.

      * For guidance on **Device Preparation** and **Device Provision**, please see step two below. Ensure you save the **Authentication URL**, **ID**, and **Secret** for the upcoming provisioning steps of the FLG.

      * By default, the physical WAN port of the FLG is set to DHCP. If you need to access the internet via a static IP, you can click **Configure** to remotely configure the static IP, for detailed operation, please refer to [Managing devices and networks for hardware-based branch gateways](https://docs.byteplus.com/docs/sealsuite/docs-managing-devices-and-networks-for-branch-gateway-hardware-version).

      * If you exit the branch gateway hardware configuration page midway, you can find the added node that is to be activated in the gateway list, click **View Device Provisioning Info**, and you can retry to get the **Authentication URL**, **ID**, **Secret** and other configuration information.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ef42b580e86c45e9985fdf200ae52f3c~tplv-goo7wpa0wc-image.image) </span>

         **Step two**: Local configuration of SealSuite to access the network gateway FLG.

   6. Power on the FLG and start the device with a network cable connected to the WAN port, ensuring the equipment is normal and connected to the internet.

   7. Use an Ethernet cable to connect the device LAN port to your PC for device provisioning.

   8. On your PC, access the local device console at `192.168.168.1` and log in using the SealSuite administrator account credentials.

   9. On the **WAN Configure** page of the console, complete the WAN port settings as required.

      
      |**Configuration Item** |**Description** |
      |---|---|
      |**Connection Type** |Choose **Static IP** or **DHCP** according to actual needs.<br><br><br>* If **Static IP** is selected, it is necessary to configure the WAN port's **IP Address**, **Subnet Mask**, and **Default Gateway**, where the WAN port's IP address must be on the same network segment as the IP Address of the connected counterpart port.<br><br>* If **DHCP** is selected, it indicates dynamic IP address acquisition, negating the need for manual configuration of other parameters. |
      |**Advanced Settings** |Select whether to enable **SNAT**. Once enabled, the private network packet's source IP address will automatically be converted to a public network address, realizing intercommunication between the local network and the internet. |
      

   10. On the **Device Provisioning** page of the console, finish the **Device Provisioning Configuration**, and click to initiate provisioning.

      * **Authentication URL**: Corresponds to the **Authentication URL** of the hardware\-based branch gateway saved in the SealSuite Admin Console.

      * **ID**: Corresponds to the **ID** of the hardware\-based branch gateway saved in the SealSuite Admin Console.

      * **Secret**: Corresponds to the **Secret** of the hardware\-based branch gateway saved in the SealSuite Admin Console.

   11. Wait for activation to complete, ensuring the provisioning is successful and the hardware\-based branch gateway instance is bound to the device.

      Subsequently, you can view and control the device in the SealSuite Admin Console.

   12. (Optional) At the bottom of the left navigation bar of the local console, click **Reset Password** to change the password of the login account.


<span id="c3a47fad"></span>
## Results

After deployment, inter\-branch access will enter the SealSuite SD\-WAN through the nearest Point of Presence (PoP), and intelligently select the optimal path, choosing to exit at the optimal Point of Presence (PoP) closest to the access target, reducing access latency and improving the inter\-visit experience.

<span id="d32904c3"></span>
# Scenario 2: Cross\-border resource access for enterprises

<span id="8f281e0c"></span>
## **Scenario introduction**

For enterprises with overseas access needs, traditional network devices often cannot provide legal cross\-border access methods. SealSuite facilitates compliant cross\-border office app access for users by deploying POP nodes worldwide.

<span id="23c4662a"></span>
## **Procedure**


1. Log in to the SealSuite Admin Console.

2. In the left navigation bar, select **SD\-WANateway**.

3. In the top right corner of the **Branch Gateway** page, click **Remote Working**.

4. On the pop\-up page on the right side of the screen, click **Get Started**.

   After clicking the button, the page will automatically redirect to the **Remote Working** page, and the **Remote Working** feature switch is on by default.

   After enabling the remote working feature, SealSuite will automatically generate the following resources:

   * In the **VPN** \> **VPN Gateway** section of the SealSuite Admin Console, it will automatically generate an offline cloud VPN gateway (VPN cloud node).

   * In the **Application** \> **Gateway Management** section of the SealSuite Admin Console, it will automatically generate an offline cloud application gateway.

5. Based on actual business needs, select and configure one or more of the following remote working methods.

   * Build a client\-based remote working environment, see [Building a client-based remote working environment](https://docs.byteplus.com/docs/sealsuite/docs-enabling-telecommuting-on-the-cloud#d41be92a).

   * Build a clientless remote working environment, see [Building a clientless remote working environment](https://docs.byteplus.com/docs/sealsuite/docs-enabling-telecommuting-on-the-cloud#3bf4c989).


<span id="5cc2a2c0"></span>
## Results

Users can access globally with secured and compliant access points, allowing companies to connect to global resources securely and efficiently.

<span id="c0a34967"></span>
# Scenario 3: Setting up smart routing policy based on employee groups

<span id="8161295c"></span>
## **Scenario introduction**

In a multiple entry points and multi\-destination environment, SealSuite SD\-WAN supports fine control over paths from a user's perspective to meet different access needs, achieving better management and an improved access experience.

Different users have different access needs for domain name resources. For example, software development department staff may need to frequently visit gaming news/technology\-related sites hosted in other countries. To ensure users from different locations accessing contents with optimal speed, an user\-based routing policy can be configured.For more information, please refer to [Application Routing: Intelligent Traffic Steering](https://docs.byteplus.com/docs/sealsuite/docs-application-scheduling).

<span id="58cfd1c6"></span>
## **Procedure**


1. **Add application resource**

   1. In the left navigation bar, select **System Settings** \> **Resource** \> **Address Management**.

   2. Fill in the following information and click on **Confirm**.

      
      |**Configuration Item** |**Required** |**Description** |
      |---|---|---|
      |Domain resource name |Yes |Enter the name of the resource for identification. |
      |Domain resource tag |No |Add one or multiple tags that the resource belongs to. You can select existing tags, modify and delete existing ones, or **Add Group**.<br><br>Tags can be used for resource classification, which facilitates system settings. |
      |Domain address |Yes |Add one or more domain names, support for adding domain names and wildcard domains.<br><br>You can batch copy and paste content, the system will automatically deduplicate and you can clear content with a single click. |
      

2. **Configure routing policy**: Specify certain resources and employees.

   1. Log in to the SealSuite Admin Console.

   2. In the left navigation bar, click on **SD\-WAN** \> **Routing Policy**.

   3. On the **Configure** **routing policy** page, click on **Employee**.

   4. Click on **Add New Policy**, fill in the content following the instructions below, and click on **Confirm**.

      
      |**Configuration Item** |**Required** |**Description** |
      |---|---|---|
      |Policy name |Yes |Enter the name of the policy for identification. It is recommended to name using keywords of departments or roles. |
      |Priority |Yes |Set the priority of this policy. If the same employee has multiple routing policies, the policies are effective according to priority. The higher the number, the higher the priority; when strategies with the same priority are triggered, the most recently created or updated routing policy is executed. |
      |Select resource |Yes |Choose one or more resources to configure the routing policy based on the **Resource Name** or **Resource Group**. |
      |Scope |Yes |Select one or more members based on **Department** or **Role**, specifying the scope of members for which the policy is effective. |
      |Destination Branch Gateway |Yes |Set one or more destination branch gateways as the configured resource's destination branch gateway.<br><br>To ensure that routing policies take effect, it is necessary to ensure that the destination branch gateway is in the Running status, that is, to ensure that the branch gateway has been deployed and activated. For specific configuration methods, please refer to [Adding a software-based branch gateway](https://docs.byteplus.com/docs/sealsuite/docs-adding-a-branch-gateway-software-version-) and [Adding a hardware-based branch gateway](https://docs.byteplus.com/docs/sealsuite/docs-adding-a-branch-gateway-hardware-version-). |
      |Default client destination |Yes |Set a default destination for employee routing policy clients. When employees connect to cloud nodes or select auto\-routing to connect to cloud nodes from the client, if no destination is specified, resources will use this default destination. |
      


<span id="afc056f8"></span>
## Results

Through configuring routing policy, enterprises can achieve a better access experience and more refined network management according to the specific needs of employees.

<span id="d3b15159"></span>
# Scenario 4: Scheduling applications intelligently by branch

<span id="233cac6b"></span>
## Understanding branch\-level scheduling

In environments with multiple entry and exit points, SealSuite SD\-WAN enforces fine\-grained control over access paths at the branch level. This ensures specific access requirements are met, management is centralized, and the overall user experience is optimized.

Branch\-level scheduling restricts the ingress branch gateway when users access target applications via domain names. For example, access to sensitive enterprise resources can be restricted to traffic originating from specific work areas or branch offices. For more details, see [Application Routing: Intelligent Traffic Steering](https://docs.byteplus.com/docs/sealsuite/docs-application-scheduling).

<span id="6cd94022"></span>
## Configure branch\-level routing

<span id="31aeeff4"></span>
### 1. Add application addresses

Add domain or IP address resources within the application scheduling module.


1. In the left navigation bar of the Admin Console, select **System Settings** \> **Resources** \> **Address Management**.

2. Click  **+ Add Domain Name**, configure the following parameters, and click **Confirm**.

   
   |**Configuration Item** |**Required** |**Description** |
   |---|---|---|
   |Domain Resource Name |Yes |Enter a unique identifier for the application. |
   |Domain Resource Tag |No |Assign tags to classify and manage resources. Select existing tags or create new ones. |
   |Domain Address |Yes |Specify one or more domains or wildcard domains.<br><br>Batch copy\-pasting is supported; the system automatically removes duplicates. |
   


<span id="5836db4f"></span>
### 2. Configure routing policies

Select branch routing and define the ingress branch gateway constraints.


1. Log in to the SealSuite Admin Console.

2. In the left navigation bar, click **SD\-WAN** \> **Routing Policy**.

3. Under the **Routing Policy** tab, click **Branch Policy**.

4. Click  **+ Add Policy**, configure the parameters as described below, and click **Confirm**.

   
   |**Configuration Item** |**Required** |**Description** |
   |---|---|---|
   |Policy Name |Yes |Enter a descriptive name. Including branch gateway keywords is recommended. |
   |Priority |Yes |Set a priority value (1–100). If multiple policies target the same application, the highest value takes precedence. For IP resources, high\-priority policies override lower ones even if address segments overlap. |
   |Select Application |Yes |Choose one or more applications by name or tag to include in the policy. |
   |Destination Branch Gateway |No |Specify the egress branch gateway for the policy. Each policy supports only one egress point.<br><br>The gateway must be in **Running** status (deployed and activated) for the policy to take effect. See [Adding a software-based branch gateway](https://docs.byteplus.com/docs/sealsuite/docs-adding-a-branch-gateway-software-version-) and [Adding a hardware-based branch gateway](https://docs.byteplus.com/docs/sealsuite/docs-adding-a-branch-gateway-hardware-version-). |
   |Source Branch Gateway |No |Define the ingress gateway constraint. By default, resources are accessible from any gateway. Specify an ingress gateway to restrict access to a specific branch.<br><br>The gateway must be in **Running** status for the policy to take effect. See [Adding a software-based branch gateway](https://docs.byteplus.com/docs/sealsuite/docs-adding-a-branch-gateway-software-version-) and [Adding a hardware-based branch gateway](https://docs.byteplus.com/docs/sealsuite/docs-adding-a-branch-gateway-hardware-version-).<br><br>If no ingress gateway is specified, this policy serves as a fallback for employee routing policies. |
   


<span id="e53a91a3"></span>
## Expected outcome

Application scheduling allows enterprises to optimize access performance and enforce granular network controls based on specific branch requirements.
