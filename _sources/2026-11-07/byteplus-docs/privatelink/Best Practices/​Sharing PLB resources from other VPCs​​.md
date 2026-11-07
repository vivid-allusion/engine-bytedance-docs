---
title: "​Sharing PLB resources from other VPCs​​"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/Sharing-PLB-resources-in-a-VPC-with-another-VPC"
---

This topic explains how to share the Private Load Balancer (PLB) service within a VPC with other VPCs using PrivateLink.

<span id=".5Zy65pmv5LuL57uN"></span>
## Scenarios

Through PrivateLink, the PLB service resources associated with the endpoint service are shared with the endpoint, enabling resources within the VPC to access the backend servers of the PLB service deployed in the public service zone.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The billing features for PLB\-type service resources and endpoint services via PrivateLink are currently in beta stage. Please contact your account manager for more information.</div>


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_13b288de17d864434bca536941d93148.png) </span>

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Create a VPC, subnet, and Elastic Compute Service (ECS) instances. For detailed actions, see [Creating a Virtual Private Cloud](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC) and [Purchasing an Elastic Compute Service instance](https://vsop-online.bytedance.net/docs/6522/104245).

* The PLB service configuration has been completed.


<span id=".6YWN572u5q2l6aqk"></span>
## Configuration steps

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following steps only describe the parameters required for the configuration in this document. For parameters not mentioned, keep the default values.</div>


<span id=".5q2l6aqk5LiA77ya5Yib5bu657uI56uv6IqC54K55pyN5Yqh"></span>
### Step 1: Create endpoint service


1. Log in to [Endpoint service console](https://console.byteplus.com/pl/endpointServices) using the service provider's account.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If cross\-service role authorization has not been performed, please complete the authorization first according to the prompts on the page.   </div>
   

2. In the top menu bar, select the target project and region.

3. Click **Create endpoint service** and see the table below to configure the relevant parameters.

   
   |Parameter |Notes |Example value |
   |---|---|---|
   |**Basic information** |||
   |Region |Select the region to which the endpoint service belongs.<br><br>After you select a region, the created endpoint service can only associate endpoints within its selected region and cannot be migrated. |China (Beijing) |
   |Name |The name of the endpoint service does not need to be filled in manually. Once the endpoint service is created successfully, the system automatically generates it in the format of com.volces.privatelink.<Region ID\>.<endpoint service ID\>. |\-\- |
   |Description |Add a description for the endpoint service to distinguish it from other endpoint services. |eps\-01 |
   |Payer account |Select the payer account for the PrivateLink service. |Endpoint |
   |**Service resources** |||
   |Type |Select the type of service resource provided by the endpoint service. In this topic, select PLB. |PLB |
   |Service resources |Select the PLB instance(s) to be used as service resources and choose the Availability Zone(s) where this PLB instance provides service. |\- |
   |**Advanced options** |||
   |Auto accept connection |Select whether this endpoint service automatically accepts connection requests from endpoints. |Yes |
   

4. Click **Buy now** to complete the action.


<span id=".5q2l6aqk5LqM77ya5re75Yqg57uI56uv6IqC54K55pyN5Yqh55m95ZCN5Y2V"></span>
### Step 2: Add allowlist for endpoint service

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the endpoint and the endpoint service belong to the same account, please skip this step.</div>



1. Click the ID of the target endpoint service and select the **Allowlist** tab.

2. Click **Add allowlist**, and configure the allowlist according to the table below.

   
   |Parameter |Notes |Example value |
   |---|---|---|
   |Allowlist range |Select the allowlist range of endpoint service. |Designated account number |
   |Account ID |Enter the account ID to which the endpoint belongs. |210234\*\*\*\* |
   

3. Click **Buy now** to complete the action.


<span id=".5q2l6aqk5LiJ77ya5Yib5bu65o6l5Y-j57uI56uv6IqC54K5"></span>
### Step 3: Create interface endpoint


1. Log in to [Endpoint console](https://console.byteplus.com/pl/endpoints) using the BytePlus Account of the service consumer.

2. Follow the steps below to complete cross\-service role authorization. Only accounts that have not completed cross\-service role authorization need to perform this. If already authorized, ignore this step.

   1. On the **Cross\-service access request** page, click **Authorize**.

      1. The authorized role is displayed in the role list of the Identity and Access Management (IAM) platform. Deleting the authorized role may cause cross\-service access failures. Proceed with caution.

      2. If the authorization role is deleted and you need to continue using the PrivateLink service, you must re\-authorize the role.

   2. In the left\-side navigation pane, click **Endpoint** again.

3. On the **Interface Endpoint** tab, click **Create Endpoint**, and configure the relevant parameters as per the table below.

   
   |Parameter |Notes |Example value |
   |---|---|---|
   |**Basic information** |||
   |Region |Select the region of endpoint. |China (Beijing) |
   |Name |Enter the name of endpoint. |ep\-01 |
   |Type |Select the type of endpoint. |Interface |
   |**Endpoint Service** |||
   |Add method |Select the method for associating an endpoint service. |Select available service |
   |Endpoint Service |Select the endpoint service that was created in [Creating endpoint service](https://docs.byteplus.com/en/docs/privatelink/Sharing-PLB-resources-in-a-VPC-with-another-VPC#.5q2l6aqk5LiA77ya5Yib5bu657uI56uv6IqC54K55pyN5Yqh). |com.volces.privatelink.cn\-beijing.epsvc\-2fe630gurkl37k5gfuy33\*\*\*\* |
   |Payer account |The billing account for the PrivateLink service, specified by the endpoint service creator, cannot be modified. |Endpoint |
   |**Network configuration** |||
   |VPC |Select the VPC to which the endpoint belongs. The VPC selected here must be different from the VPC to which the endpoint service's associated service resource belongs. |VPC1 |
   |Availability Zone and Subnet |Check the box for the Availability Zones of the endpoint service where you need to establish connections and select the corresponding subnet for each.<br><br>After a subnet is selected, the system will automatically create an endpoint network interface for you. |Availability Zone A, subnet01, Auto\-assign IP |
   |Security Group |Select the security group(s) to be associated with the endpoint's network interface. |Default\-sg |
   

4. Click **Confirm order** according to the console instructions to review and confirm the Legal.

5. Click **Buy now** to check whether the creation is successful.

   Locate and record the name of the successfully created endpoint service. In this example, the endpoint domain name is ep\-2fegvybuk2yv459gp68nb\*\*\*\*.epsvc\-2fegvxu3a2h3459gp67rd\*\*\*\*.cn\-beijing.privatelink.volces.com.


<span id=".5q2l6aqk5Zub77ya5rWL6K-V6IGU6YCa5oCn"></span>
### Step 4: Test connectivity


1. Remotely log in to the ECS within VPC1. For specific actions, see [Logging in to Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the `curl http://endpoint domain:PLB listener port` command to test network connectivity.

   This topic runs the `curl http://ep-2fegvybuk2yv459gp68nb****.epsvc-2fegvxu3a2h3459gp67rd****.cn-beijing.privatelink.volces.com:80` command.

   If the returned result displays the content of the Web service page configured on the backend server, it indicates successful network connectivity.
