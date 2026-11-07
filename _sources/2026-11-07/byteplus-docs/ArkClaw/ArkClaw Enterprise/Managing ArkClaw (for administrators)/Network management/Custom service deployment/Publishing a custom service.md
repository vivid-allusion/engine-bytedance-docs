---
title: "Publishing a custom service"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Publishing-a-custom-service"
---

This section describes how to configure a custom service.

<span id="m3SYEpW0"></span>
## Prerequisites

You need to activate the ArkClaw Enterprise Edition. For specific instructions, see [Activating ArkClaw Enterprise Edition service](https://docs.byteplus.com/en/docs/ArkClaw/Quick_start_guide).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">ALB features with ArkClaw capabilities are currently in invite\-only beta. If you wish to try them out, please contact your account manager.</div>


<span id="ODULX7Vv"></span>
## Create ALB


1. Log in to the [ALB console](https://console.byteplus.com/alb)

2. In the top menu bar, select the target project and region.

3. In the left navigation pane, select **Instance**.

4. On the instance management page, click "Create instance".

5. Configure parameters based on the table below.

   
   |Parameters |Notes |
   |---|---|
   |**Basic information** ||
   |Region |Select the Region where the ALB instance resides. The region cannot be changed after the instance is created. |
   |Name |Enter the name of the ALB instance. |
   |Instance edition |Select **Standard**. |
   |Enable ArkClaw |Select **Enable ArkClaw**. |
   |Description |Enter the description of the ALB instance. |
   |**Network Configuration** ||
   |IP type |Only IPv4 is supported. |
   |Network type |Select the network type for the ALB instance. The system will assign IP addresses to the ALB instance based on your selection.<br><br><br>* **Public**: A Public ALB can be accessed though both the public and private networks.<br><br>* **Private**: A private ALB only has the private IP address and can only be accessed via the private network. |
   |SpaceNetwork |Select SpaceNetwork from the dropdown. SpaceNetwork is the network of the ArkClaw Enterprise Edition space.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">For ArkClaw Enterprise Edition ArkClaw activated before May 13, 2026, its SpaceNetwork needs to be migrated by contacting the account manager.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When SpaceNetwork is selected, the system checks whether the user has completed cross\-service authorization. If not, the user is directed to the authorization page to grant the ServiceRoleForALB role access permissions to the SpaceNetwork and Claw APIs.</div><br> |
   |**EIP configuration (This parameter is only available when the ALB network type is set to public)**  ||
   |Security protection |Configure the security protection type for the EIP.<br><br><br>* **Default**: Elastic IP addresses (EIPs) of this type provide [basic DDoS protection](https://docs.byteplus.com/en/docs/6352/166081) capabilities.<br><br>* **Enhanced protection**: EIPs of this type not only provide basic DDoS protection but also support low\-latency, highly available Tbps\-level [native DDoS protection (enterprise edition)](https://docs.byteplus.com/en/docs/6352/196723) capabilities. Select **Safety package** for this EIP. If no package is available, click **Create safety package** to the right of the parameter field to create a new one. For parameter details, see [Purchasing an Anti-DDoS Origin (Enterprise Edition) instance](https://docs.byteplus.com/en/docs/6352/196723).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To use the enhanced protection feature, please contact your account manager or <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000645">Submit ticket</a>.</div><br> |
   |ISP |The ISP of the EIP. Only BGP (multi\-ISP) is supported by default. |
   |Metering method |Select the metering method for the EIP.<br><br><br>* **Pay\-by\-bandwidth**: Fees are calculated based on the duration of bandwidth usage, regardless of the actual traffic generated. This billing method is suitable for services with stable bandwidth requirements.<br><br>* **Pay\-by\-data\-transfer**: Fees are calculated based on the actual outbound internet traffic generated, regardless of the duration of bandwidth usage. This billing method is suitable for services with unstable or unpredictable bandwidth requirements.<br><br><br>For more billing details, see [Pay-as-you-go](https://docs.byteplus.com/docs/eip/Pay-as-you-go). |
   |Maximum bandwidth |Set the bandwidth cap of the EIP. Unit: Mbps. Value range:<br><br><br>* When the metering method is **Pay\-by\-bandwidth**, the bandwidth cap value ranges from 1 to 500 Mbps.<br><br>* When the metering method is **Pay\-by\-data\-transfer**, the bandwidth cap value ranges from 1 to 200 Mbps.<br><br><br>After creating a public network instance, you can adjust the EIP bandwidth cap as needed. |
   |Add EIP to BWP |Add EIP to [Bandwidth Package](https://docs.byteplus.com/en/docs/bandwidthpackage/What-is-Bandwidth-Package).<br><br><br>* To add an EIP to a Bandwidth Package, the following conditions must be met:<br><br>   * Both are in the same region.<br><br>   * Both use the same public network egress.​<br><br>   * Both have the same protection type.<br><br>   * The EIP uses pay\-as\-you\-go billing (i.e., Pay\-by\-bandwidth or Pay\-by\-data\-transfer as described in this document).<br><br>* After adding to a Bandwidth Package, the metering method and bandwidth cap configured here become ineffective. The EIP will share the bandwidth resources of the Bandwidth Package. If the EIP is later removed from the Bandwidth Package, the metering method and bandwidth cap configured here will be fully restored.<br><br>* If left unchecked, you can [Add to Bandwidth Package](https://docs.byteplus.com/en/docs/eip/Adding-an-EIP-to-a-Bandwidth-Package) as needed in the next step. |
   |**More configurations** ||
   |Delete protection |Specify whether to enable the **Delete protection** feature. Once enabled, the ALB instance cannot be deleted. To delete the ALB instance later, disable this feature first. |
   |Project |Select the project to which the ALB belongs. For more information, see [Project management](https://docs.byteplus.com/en/docs/clb/Projects-Overview). |
   |Tag |A tag consists of a key\-value pair and is used for categorizing and searching resources [Learn more](https://docs.byteplus.com/en/docs/clb/Tag-Overview)<br><br>Click the add icon, enter the tag key and tag value, and add tags to the ALB. |
   

6. Follow the console guidance to review and accept the legal terms.

7. Click **Submit** to complete the action.


<span id="sfQVQpVD"></span>
## Create a Claw backend server group

Only the "Server group type" parameter adds the "Claw type" option. All other parameters are the same as those of a standard ALB. For procedures, see [Creating a server group](https://docs.byteplus.com/en/docs/clb/Managing-server-groups).

<span id="WsZqPnEh"></span>
## Add Claw as backend server

Select Claw only when adding the backend server. All other parameters are the same as those of a standard ALB. For procedure, see [Adding a backend server](https://docs.byteplus.com/en/docs/clb/Managing-server-groups).

<span id="2TCawrHc"></span>
## Other actions


* [Creating an HTTP listener](https://docs.byteplus.com/en/docs/clb/Creating-HTTP-listener)

* [Creating forwarding rule (Standard edition)](https://docs.byteplus.com/en/docs/clb/Creating-a-forwarding-rule_Standard-edition)

* [Create endpoint service](https://docs.byteplus.com/en/docs/privatelink/Creating-endpoint-services)

* [Create interface endpoint](https://docs.byteplus.com/en/docs/privatelink/Endpoint-02)


[Learn more](https://docs.byteplus.com/en/docs/clb/Introduction)
