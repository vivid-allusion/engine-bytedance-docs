---
title: "Implementing private access between VPCs across accounts"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/Getting-Started-03"
---

<span id=".5Zy65pmv56S65L6L"></span>
## Scenario examples

This topic describes the detailed configuration for enabling Elastic Compute Services (ECSs) in the endpoint's VPC to access service resources in the endpoint service across different accounts.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_02239e60edd81f7b566d5bc1f2b7afd4.png) </span>

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Ensure you have completed the preparatory steps outlined in the [Quick start](https://docs.byteplus.com/en/docs/privatelink/Getting-Started-01).

<span id=".6YWN572u5q2l6aqk"></span>
## Configuration procedures

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following steps only describe the parameters required for the configuration in this document. For parameters not mentioned, keep the default values.</div>


<span id=".5q2l6aqk5LiA77ya5Yib5bu657uI56uv6IqC54K55pyN5Yqh"></span>
### Step 1: Create endpoint service


1. Log in to the [Endpoint Service console](https://console.byteplus.com/pl/endpointServices) using account B.

2. Only accounts that have not completed cross\-service role authorization need to perform this. If already authorized, ignore this step.

   1. On the **Cross\-service access request** page, click **Authorize**.

      * The authorized role will be displayed in the role list of the Identity and Access Management (IAM) platform. Deleting the authorized role may cause cross\-service access failures. Proceed with caution.

      * If the authorization role is deleted and you need to continue using the PrivateLink service, you must re\-authorize the role.

   2. In the left\-side navigation pane, click **Endpoint Service** again.

3. In the top menu bar, select the target project and region.

4. Click **Create Endpoint Service** and see the table below to configure the relevant parameters.

   
   |Parameter |Explanation |Example |
   |---|---|---|
   |**Basic information** |||
   |Regions |Select the region to which the endpoint service belongs. |China (Guangzhou) |
   |Name |The name of the endpoint service does not need to be filled in manually. Once the endpoint service is created successfully, the system automatically generates it in the format of `com.volces.privatelink.<regionID>.<endpointserviceID>`. |\-\- |
   |**Service Resource** |||
   |Topic |Select the service resource type provided by the endpoint service. |CLB |
   |Service Resource |Select the CLB instance(s) to be used as the service resource(s). |CLB01 |
   |**Advanced option** |||
   |Auto accept connection |Auto\-accept endpoint connection<br><br><br>* **Yes:**  Automatically accept connection requests from endpoints.<br><br>* **No**: If No is selected, after the endpoint is created, you must manually accept the connection request from the endpoint. For the procedure, see [Accepting an endpoint connection](https://docs.byteplus.com/en/docs/privatelink/Accepting-Rejecting-endpoint-connection). |Yes |
   

5. Click **Create** to complete the action.

   Locate and record the Name of the successfully created endpoint service, as you will need it in [Step 3: Create endpoint](https://docs.byteplus.com/en/docs/privatelink/Getting-Started-03#.5q2l6aqk5LiJ77ya5Yib5bu657uI56uv6IqC54K5).


<span id=".5q2l6aqk5LqM77ya5re75Yqg5pyN5Yqh55m95ZCN5Y2V"></span>
### Step 2: Add allowlist


1. Click the target endpoint service, and select **Allowlist** tab.

2. Click **Add allowlist**, and configure the allowlist according to the table below.

   
   |Parameter |Explanation |Example |
   |---|---|---|
   |Allowlist range |Select the allowlist range of endpoint service. |Specified Account |
   |Account ID |Enter the ID of account A. |210000\*\*\*\* |
   

3. Click **Add** to complete the action.


<span id=".5q2l6aqk5LiJ77ya5Yib5bu657uI56uv6IqC54K5"></span>
### Step 3: Create endpoint


1. Log in to the [Endpoint console](https://console.byteplus.com/pl/endpoints) using account A.

2. Follow the steps below to complete cross\-service role authorization.

   Only accounts that have not completed cross\-service role authorization need to perform this. If already authorized, ignore this step.

   1. On the **Cross\-service access request** page, click **Authorize**.

      * The authorized role will be displayed in the role list of the Identity and Access Management (IAM) platform. Deleting the authorized role may cause cross\-service access failures. Proceed with caution.

      * If the authorization role is deleted and you need to continue using the PrivateLink service, you must re\-authorize the role.

   2. In the left\-side navigation pane, click **Endpoint** again.

3. On the **Interface Endpoint** tab, click **Create Endpoint**, and configure the relevant parameters as per the table below.

   
   |Parameter |Explanation |Example |
   |---|---|---|
   |**Basic information** |||
   |Regions |Select the region of endpoint. |China (Guangzhou) |
   |Name |Enter the name of endpoint. |endpoint01 |
   |Topic |Select the type of endpoint. |Interface |
   |**Endpoint Service** |||
   |Add method |Select the method for associating an endpoint service. It supports two methods: Add by Service Name and Select available service. |Select available service |
   |Endpoint Service |Select the endpoint service created in [Step 1](https://docs.byteplus.com/en/docs/privatelink/Getting-Started-03#.5q2l6aqk5LiA77ya5Yib5bu657uI56uv6IqC54K55pyN5Yqh). |com.volces.privatelink.cn\-guangzhou.epsvc\-2fe630gurkl37k5gfuy33\*\*\*\* |
   |**Network Configuration** |||
   |VPC |Select the VPC to which the endpoint belongs. The VPC selected here must be different from the VPC to which the endpoint service's associated service resource belongs. |VPC01 |
   |AZs and Subnets |Check the box for the Availability Zones of the endpoint service where you need to establish connections and select the corresponding subnet for each.<br><br>After a subnet is selected, the system will automatically create an endpoint network interface for you. |Availability zone A, subnet01, Auto\-assign IP |
   |Security group |Select the security group(s) to be associated with the endpoint's network interface. |Default\-sg |
   

4. Click **Buy now**. Follow the console guidance to review and accept the Legal.

5. Click **Buy now** to check whether the creation is successful.

6. view and record the created Endpoint Domain. This will be needed in [Step 4: Test connectivity](https://docs.byteplus.com/en/docs/privatelink/Getting-Started-03#.5q2l6aqk5Zub77ya5rWL6K-V6L-e6YCa5oCn).


<span id=".5q2l6aqk5Zub77ya5rWL6K-V6L-e6YCa5oCn"></span>
### Step 4: Test connectivity

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before performing the following verification, ensure that the backend server for the CLB instance of the service resource is configured with the backend service. The procedure can be found in <a href="https://docs.byteplus.com/en/docs/clb/Creating-an-HTTP-static-page#.5q2l6aqk5LqM77ya5pCt5bu65ZCO56uv5pyN5Yqh">Configuring the backend service</a>.</div>



1. Remotely log in to the Elastic Compute Service (ECS) in VPC01. For specific actions, see [Logging in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the `curl http://endpoint domain:listener port` command to test network connectivity.

   For example, if the endpoint domain is ep\-2fegvybuk2yv459gp68nbk2e7.epsvc\-2fegvxu3a2h3459gp67rdzvhe.cn\-guangzhou.privatelink.volces.com and the service resource CLB instance's listener port is 80, then execute: `curl http://ep-2fegvybuk2yv459gp68nbk2e7.epsvc-2fegvxu3a2h3459gp67rdzvhe.cn-guangzhou.privatelink.volces.com:80`.

   If the returned result displays the content of the backend service page configured on the backend server, it indicates successful network connectivity.
