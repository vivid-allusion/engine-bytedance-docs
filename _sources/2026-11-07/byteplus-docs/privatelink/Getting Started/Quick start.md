---
title: "Quick start"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/Getting-Started-01"
---

<span id=".6KeE5YiS5Zyw5Z-f5Y-K6LSm5Y-3"></span>
## Plan the Region and Account


* To reduce latency and improve download speed, it is recommended that the deployment regions of the endpoint service and endpoint be as geographically close as possible to the access source customers.

* Please ensure the endpoint service and endpoint are located in the same Region.

* Please confirm whether the accounts to which the endpoint service and endpoint belong are the same or different.


<span id=".6LWE5rqQ5YeG5aSH"></span>
## Resource Preparation


* Prepare a BytePlus Account: Determine the number of accounts based on whether the endpoint service and endpoint belong to the same account.

   * Same account scenario: Register one BytePlus account and complete real\-name authentication.

   * Cross\-account scenario: Register two BytePlus accounts and complete real\-name authentication for each.

* Prepare a private network environment in the cloud: Prepare two VPCs to provide a private network environment for the endpoint service and endpoint. When creating a VPC, ensure the Region you select matches the Region planned for PrivateLink, and choose the Account for the VPC based on actual planning. To create a VPC, refer to [Creating an IPv4 VPC](https://docs.byteplus.com/en/docs/vpc/Building-an-IPv4-VPC).

* Prepare service resource: Create a CLB instance as a service resource in the VPC providing the PrivateLink environment for the endpoint service, and complete the related configuration. You can refer to [Building layer-4 CLB](https://docs.byteplus.com/en/docs/clb/Layer-4-CLB) to configure a new Cloud Load Balancer.

* Prepare an Elastic Compute Service (ECS) instance: Create an ECS instance in the VPC to which the endpoint belongs, for connectivity verification.


<span id=".5YWl6Zeo5Zy65pmv5LuL57uN"></span>
## Introduction to entry\-level scenarios

The PrivateLink service supports private network access between VPCs under the same Account and across different Accounts. You can refer to appropriate actions to quickly use the PrivateLink Product according to actual scenarios.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b422a7a4a9475f00245b8b77e21bae3b.png) </span>


* [Private network access between VPCs under the same Account](https://docs.byteplus.com/en/docs/privatelink/Getting-Started-02)

   1. [Create an endpoint service](https://docs.byteplus.com/en/docs/privatelink/Getting-Started-02#.5q2l6aqk5LiA77ya5Yib5bu657uI56uv6IqC54K55pyN5Yqh): Create an endpoint service and allow automatic establishment of endpoint connections.

   2. [Create an endpoint](https://docs.byteplus.com/en/docs/privatelink/Getting-Started-02#.5q2l6aqk5LqM77ya5Yib5bu657uI56uv6IqC54K5): Create an endpoint.

   3. [Test connectivity](https://docs.byteplus.com/en/docs/privatelink/Getting-Started-02#.5q2l6aqk5LiJ77ya5rWL6K-V6L-e6YCa5oCn): To verify that the Elastic Compute Service (ECS) in the VPC where the endpoint resides can access the service resource.

* [Private network access between cross-Account VPCs](https://docs.byteplus.com/en/docs/privatelink/Getting-Started-03)

   1. [Create an endpoint service](https://docs.byteplus.com/en/docs/privatelink/Getting-Started-03#.5q2l6aqk5LiA77ya5Yib5bu657uI56uv6IqC54K55pyN5Yqh): Create an endpoint service and allow automatic establishment of endpoint connections.

   2. [Add service allowlist](https://docs.byteplus.com/en/docs/privatelink/Getting-Started-03#.5q2l6aqk5LqM77ya5re75Yqg5pyN5Yqh55m95ZCN5Y2V): Add the Account where the endpoint belongs to the endpoint service allowlist.

   3. [Create an endpoint](https://docs.byteplus.com/en/docs/privatelink/Getting-Started-03#.5q2l6aqk5LiJ77ya5Yib5bu657uI56uv6IqC54K5): Create an endpoint.

   4. [Test connectivity](https://docs.byteplus.com/en/docs/privatelink/Getting-Started-03#.5q2l6aqk5Zub77ya5rWL6K-V6L-e6YCa5oCn): To verify that the Elastic Compute Service (ECS) in the VPC where the endpoint resides can access the service resource.
