---
title: "Enable public network for Resource Group VPC"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/enable_public_network_for_resource_group"
---

A virtual private cloud (VPC) is a private network in the cloud used to achieve private network isolation and to provide a secure, isolated environment for resources such as cloud servers.

A cloud server is an instance running within a VPC. It can be used together with a public IP or NAT gateway service, allowing cloud resources to communicate with the public Internet. This article will explain how to enable public network capability for VPC.

<span id="958b3ee2"></span>
## 1 Use cases

When multiple cloud servers, such as those in a dedicated integrated resource group, need to provide services to the public internet and each cloud server offers different services, you can create a public NAT gateway within the VPC and create DNAT and SNAT rules to enable network connectivity between the cloud servers and the public internet.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/169fbc7fe38e436eb4745131999dad24~tplv-goo7wpa0wc-image.image) </span>

<span id="166b444b"></span>
## 2 Prerequisites


* VPC network resources have been created. For detailed instructions, see [Create a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

* Create a dedicated integration resource group that has already been bound to a VPC network. For detailed instructions, see [Exclusive Integrated Resource Group Management](https://docs.byteplus.com/docs/dataleap/exclusive_integrated_resource_group).


<span id="_1-查看资源组绑定的vpc"></span>
## 3 View resource group\-bound VPCs


1. Log in to the [DataLeap Tenant Console](https://console.byteplus.com/dataleap/console/region:dataleap-console+ap-southeast-1/project/list?administrator=mine&current=1&isMine=true&pageSize=20&projectName=&projectOrOwnerName=&sortColumn=createTime&sortOrder=desc).

2. In the left navigation bar, click **Resource group management** to enter the dedicated resource group management interface.

3. Click the resource group name. The resource group details will appear on the right. You can view the bound private network name from the **configuration information** section.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6d5b29b137644f5e94c4c4e8b04b7bad~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-创建nat网关"></span>
## 4 Create a NAT gateway


1. In the upper left corner, go to **Products and Services**, search for the **Private Network** product, and click to open the **Private Network** management interface.

2. In the left navigation bar, click **Public NAT Gateway** to access the management interface.

3. Click **Create NAT Gateway** to enter the creation page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3e724213b9774ec0817f12d4a2ba8827~tplv-goo7wpa0wc-image.image) </span>

4. On the Create Public NAT Gateway page, enter the corresponding parameters.



|Parameters |Description |
|---|---|
|Billing method |* Pay\-as\-you\-go: A postpaid model suitable for scenarios where there is significant business growth in the short term.<br><br>* Subscription: A prepaid model suitable for long\-term, stable business operations.<br><br>   For details, see [NAT Gateway Billing Overview](https://docs.byteplus.com/en/docs/natgateway/Billing-overview). |
|Region |The service currently supports Asia Pacific (Johor), with internal network isolation between different regions. It is recommended to select a region closer to your business to reduce network latency and improve access speed. |
|Name |Enter the NAT gateway name. It must meet the following requirements:<br><br><br>* Start with a Chinese character, a letter, or a number<br><br>* Only Chinese characters, letters, numbers, the period ".", the underscore "_", and the hyphen "\-" are allowed.<br><br>* Must be 1–128 characters in length |
|Description |Enter a description for the NAT gateway to facilitate future management. |
|Specifications |Choose the NAT gateway specifications Specifications are divided into small, medium, and large, each supporting a different maximum number of connections. |
|VPC |Use the dropdown to add the private network associated with the NAT gateway. |
|Subnet |Select a subnet under the private network. Assign a private IP address from this subnet to the automatically generated network interface card for the NAT gateway. |
|Project |Select the project for the public NAT gateway. For more information, see [Managing projects](https://docs.byteplus.com/en/docs/natgateway/Managing-projects).<br><br><br>* If you select All resources for the account in the top navigation bar before entering the creation page, you can then select an existing project from the dropdown.<br><br>* If you select the target project in the top navigation bar before entering the creation page, you can only select the target project.<br><br><br>After the Public NAT gateway is created, if you need to switch projects, refer to [Project Resource Management](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Resource_Management). When a public NAT gateway is moved into or out of a project, its sub\-resources—including SNAT rules, DNAT rules, public NAT gateway auxiliary NICs, and public NAT gateway security groups—are also moved into or out of the project accordingly. |


For more information about creation operations, see [Create NAT Gateway](https://docs.byteplus.com/en/docs/natgateway/Creating-an-Internet-NAT-gateway).

After entering the required information, click **Confirm Order**. On the redirected page, check to agree to the **Agreement**, and click **Buy Now**.

<span id="_3-配置公网ip"></span>
## 5 Configure EIP


1. After creating the public NAT gateway, on the NAT list page, in the right\-side action bar, click **Configure EIP**.

2. Click **Associate EIP**. In the drop\-down list, select an available public IP. If no public IP is available, go to the Apply for Public IP page to request one. For detailed instructions on application operations, see [https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP](https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP)


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f72d11c116f54def9f4212ef2d6465a6~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-配置snat规则"></span>
## 6 Configure SNAT rules

After binding the public IP, switch to **SNAT rules** in the top toolbar, and click **Create SNAT rule**.

See: [https://docs.byteplus.com/en/docs/natgateway/Managing-SNAT-rules](https://docs.byteplus.com/en/docs/natgateway/Managing-SNAT-rules)

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aeb28a9eadda4bdcaf3e71d6f0b1125d~tplv-goo7wpa0wc-image.image) </span>


|Parameters |Description |
|---|---|
|Name |Enter the SNAT rule name, which must meet the following conditions:<br><br><br>* Start with Chinese characters, letters, or numbers<br><br>* It can only contain Chinese characters, letters, numbers, period '.', underscore '_', and hyphen '\-'.<br><br>* Must be 1–128 characters long |
|Granularity |You can select granularity such as **VPC, subnet, cloud server, or custom network segment**. Since network connectivity for data integration tasks is currently established at the private network level, you need to select **private** **network** as granularity when creating SNAT rules. |
|EIP |Select the public IP address bound to the NAT rule from the dropdown. |


Click the **Create** button, and the rule will be created successfully. The created SNAT rule will be displayed in the rule list, where you can **Edit, Delete**, and perform other operations on the rule.

Afterwards, the subnets of this VPC will be able to access the public Internet.
