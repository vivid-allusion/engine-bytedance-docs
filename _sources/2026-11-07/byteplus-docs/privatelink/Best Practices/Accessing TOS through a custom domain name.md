---
title: "Accessing TOS through a custom domain name"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/Accessing-TOS-through-private-DNS"
---

This topic describes how to configure PrivateLink to access BytePlus Torch Object Storage (TOS) service using a custom domain name.

<span id=".5Zy65pmv5LuL57uN"></span>
## Scenarios

By default, accessing TOS through PrivateLink uses the HTTP protocol and Endpoint Domain. If you wish to access via the original TOS domain name or want to use the HTTPS protocol through PrivateLink, you need to configure a private DNS name.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">When accessing TOS via PrivateLink using the HTTPS protocol, you must use the Private DNS Name you configured.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Ensure the endpoint service has Private DNS Name enabled and verified. If unable to enable the private DNS name for the interface endpoint, please contact the service provider and refer to [Verifying the private DNS name](https://docs.byteplus.com/en/docs/privatelink/Modifying-Verifying-private-DNS-names#.6aqM6K-B56eB5pyJRE5T5ZCN56ew) to complete the configuration.

* The Virtual Private Cloud (VPC) and its Elastic Compute Service (ECS) have been created. For detailed actions, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC) and [Purchasing an ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).


<span id=".6YWN572u5q2l6aqk"></span>
## Configuration steps

<span id=".5q2l6aqk5LiA77ya6I635Y-W57uI56uv6IqC54K55pyN5Yqh5ZCN56ew"></span>
### Step 1: Obtain endpoint service name

The endpoint service is created by the service provider; you need to obtain the Endpoint Service Name.


|BytePlus Cloud Services |Service name |
|---|---|
|Torch Object Storage (TOS) |com.volces.privatelink.*regionID*.tos\-s3 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Replace the <em>Region ID</em> in the service names listed in the table above as needed. This topic uses the service name com.volces.privatelink.cn\-beijing.tos\-s3 as an example.</div>


* <div data-tips="true" data-tips-type="tip">Confirm that the endpoint service has Private DNS Name enabled.</div>



<span id=".5q2l6aqk5LqM77ya5Yib5bu65o6l5Y-j57uI56uv6IqC54K5"></span>
### Step 2: Create interface endpoint

For detailed steps, see [Creating interface endpoint](https://docs.byteplus.com/en/docs/privatelink/Endpoint-02). The parameters to note are as follows:


* **Region** should match the region where the endpoint service is located.

* Select interface as the **Type**.

* **Endpoint service** selects the name obtained in step 1.

* Select Enable for the **Private DNS name**. The private DNS name defaults to the private DNS name configured for the endpoint service.


<span id=".57uT5p6c6aqM6K-B"></span>
### Result verification


1. Remotely log in to the Elastic Compute Service (ECS) in VPC. For specific actions, see [Logging in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the `ping` command targeting the Private DNS Name to test network connectivity.
