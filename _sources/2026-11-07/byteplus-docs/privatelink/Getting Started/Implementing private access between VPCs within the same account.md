---
title: "Implementing private access between VPCs within the same account"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/Getting-Started-02"
---

<span id=".5Zy65pmv56S65L6L"></span>
## Scenario examples

When the service provider and service consumer belong to the same account, the service provider deploys the service, and one or multiple service consumers access the provider's service through PrivateLink.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1c5de2a96cec378e8234917c5f8e302.png) </span>

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Ensure you have completed the preparatory steps outlined in the [Quick start](https://docs.byteplus.com/en/docs/privatelink/Getting-Started-01).

<span id=".6YWN572u5q2l6aqk"></span>
## Configuration procedures

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following steps only describe the parameters required for the configuration in this document. For parameters not mentioned, keep the default values.</div>


<span id=".5q2l6aqk5LiA77ya5Yib5bu657uI56uv6IqC54K55pyN5Yqh"></span>
### Step 1: Create endpoint service


1. Log in to the [Endpoint Service console](https://console.byteplus.com/pl/endpointServices) using account A.

2. Only accounts that have not completed cross\-service role authorization need to perform this. If already authorized, ignore this step.

   1. On the **Cross\-service access request** page, click **Authorize**.

      * The authorized role will be displayed in the role list of the Identity and Access Management (IAM) platform. Deleting the authorized role may cause cross\-service access failures. Proceed with caution.

      * If the authorization role is deleted and you need to continue using the PrivateLink service, you must re\-authorize the role.

   2. In the left navigation tree, click **Endpoint Service** again.

3. In the top menu bar, select the target project and region.

4. Click **Create Endpoint Service** and configure the parameters according to the table below.

   
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

   View the endpoint service name and record it; [Step 2: Create Endpoint](https://docs.byteplus.com/en/docs/privatelink/Getting-Started-02#.5q2l6aqk5LqM77ya5Yib5bu657uI56uv6IqC54K5) requires it.


<span id=".5q2l6aqk5LqM77ya5Yib5bu657uI56uv6IqC54K5"></span>
### Step 2: Create Endpoint


1. Log in to the [Endpoint console](https://console.byteplus.com/pl/endpoints) using account A.

2. Refer to the steps below to complete the cross\-service role authorization.

   Only accounts that have not completed cross\-service role authorization need to perform this. If already authorized, ignore this step.

   1. On the **Cross\-service access request** page, click **Authorize**.

      * The authorized role will be displayed in the role list of the Identity and Access Management (IAM) platform. Deleting the authorized role may cause cross\-service access failures. Proceed with caution.

      * If the authorization role is deleted and you need to continue using the PrivateLink service, you must re\-authorize the role.

   2. In the left\-side navigation pane, click **Endpoint** again.

3. Click **Create Endpoint** and configure the parameters according to the table below.

   
   |Parameter |Explanation |Example |
   |---|---|---|
   |**Basic information** |||
   |Regions |Select the region of endpoint. |China (Guangzhou) |
   |Name |Enter the name of endpoint. |endpoint01 |
   |Topic |Select the type of endpoint. |Interface |
   |**Endpoint Service** |||
   |Add method |Select the method for associating an endpoint service. It supports two methods: Add by Service Name and Select available service. |Select available service |
   |Endpoint Service |Select the endpoint service created in [Step 1](https://docs.byteplus.com/en/docs/privatelink/Getting-Started-02#.5q2l6aqk5LiA77ya5Yib5bu657uI56uv6IqC54K55pyN5Yqh). |com.volces.privatelink.cn\-guangzhou.epsvc\-2fe630gurkl37k5gfuy33\*\*\*\* |
   |**Network Configuration** |||
   |VPC |Select the VPC to which the endpoint belongs. |VPC01 |
   |AZs and Subnets |Check the box for the Availability Zones of the endpoint service where you need to establish connections and select the corresponding subnet for each.<br><br>After a subnet is selected, the system will automatically create an endpoint network interface for you. |Availability zone A, subnet01, Auto\-assign IP |
   |Security group |Select the security group(s) to be associated with the endpoint's network interface. |Default\-sg |
   

4. Click **Buy now**. Follow the console guidance to review and accept the Legal.

5. Click **Buy now** to check whether the creation is successful.

6. Click Go to product console, view and record the domain name of the successfully created endpoint, as it is needed in Step 3: Test connectivity.


<span id=".5q2l6aqk5LiJ77ya5rWL6K-V6L-e6YCa5oCn"></span>
### Step 3: Test connectivity

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before verification, ensure that the backend servers of the CLB instance have backend services configured. For the procedure, see <a href="https://docs.byteplus.com/en/docs/clb/Creating-an-HTTP-static-page#.5q2l6aqk5LqM77ya5pCt5bu65ZCO56uv5pyN5Yqh">Configuring the backend service</a>.</div>



1. Remotely log in to the Elastic Compute Service (ECS) in VPC01. For specific actions, see [Logging in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the `curl http://endpoint domain:listener port` command to test network connectivity.

   For example, if the endpoint domain is `ep-2fegvybuk2yv459gp68nbk2e7.epsvc-2fegvxu3a2h3459gp67rdzvhe.cn-guangzhou.privatelink.volces.com` and the service resource CLB instance's listener port is 80, then execute: `curl http://ep-2fegvybuk2yv459gp68nbk2e7.epsvc-2fegvxu3a2h3459gp67rdzvhe.cn-guangzhou.privatelink.volces.com:80`.

   If the returned result displays the content of the backend service page configured on the backend server, it indicates successful network connectivity.
