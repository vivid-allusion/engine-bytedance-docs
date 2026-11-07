---
title: "IDC shared cloud Torch Object Storage service"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/Sharing-on-cloud-TOS-with-a-data-center"
---

This topic explains how to share the BytePlus Torch Object Storage (TOS) with an on\-premises IDC via the PrivateLink service.

<span id=".5Zy65pmv5LuL57uN"></span>
## Scenarios

Whether from a Virtual Private Cloud (VPC) or an on\-premises IDC, you can use PrivateLink to securely access Torch Object Storage (TOS) while avoiding public endpoint conflicts common in multi\-cloud environments.

> Cloud as a Service refers to public cloud services provided by cloud vendors. BytePlus's cloud services are deployed in the 100.64.0.0/10 CIDR block, such as the TOS service.


This topic provides configuration guidance for different scenarios when using PrivateLink to access TOS services.​​


* The default domain names for Endpoint Services and Interface Endpoints only contain the instance ID and region information, and do not identify the specific cloud service type.​​ To differentiate between cloud service types and bucket objects via PrivateLink, use the wildcard domain name feature of Interface Endpoints.​​

* When accessing TOS through an Interface Endpoint, PrivateLink allows all traffic from the target VPC to TOS by default.​​ To control bucket access scope via PrivateLink, use a Gateway Endpoint.

* PrivateLink natively supports HTTP protocol access. If you need to use the HTTPS protocol, see [Accessing Torch Object Storage through a custom domain name](https://docs.byteplus.com/en/docs/privatelink/Accessing-TOS-through-private-DNS).


The specific network architecture is shown in the following diagram.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_63e8cbc864e081f92aff79b35512d662.png) </span>

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A VPC, subnet, and Elastic Compute Service (ECS) have been created. For detailed operations, see [Creating a Virtual Private Cloud](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC) and [Purchasing an ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* For on\-premises IDC access to TOS via PrivateLink, first establish connectivity between your IDC and the VPC. Please choose the appropriate configuration steps based on your cloud connectivity service.

   * **Using Direct Connect and Cloud Enterprise Network (CEN)** : see [Direct Connect Getting started](https://docs.byteplus.com/en/docs/directconnect/Quick-start).

   * **Using Virtual Private Network (VPN) connection**: see [Virtual Private Network connection getting started](https://docs.byteplus.com/en/docs/vpn/Quick-start).

* When using Gateway Endpoints, ensure you have the target private bucket name.


<span id=".6YWN572u5q2l6aqk"></span>
## Configuration procedures

<span id=".5q2l6aqk5LiA77ya6I635Y-W57uI56uv6IqC54K55pyN5Yqh5ZCN56ew"></span>
### Step 1: Obtain endpoint service name

The endpoint service is created by the business party integrated with PrivateLink. Contact your account manager to authorize the corresponding BytePlus service to your account, then obtain the endpoint service name as shown in the table below.


|BytePlus Cloud Services |Service name |
|---|---|
|Torch Object Storage (TOS) |com.volces.privatelink.*regionID*.tos\-s3 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Replace the <em>Region ID</em> in the service names listed in the table above as needed. This topic uses the service name <code>com.volces.privatelink.cn-beijing.tos-s3</code> as an example.</div>


<span id=".5q2l6aqk5LqM77ya5Yib5bu657uI56uv6IqC54K5"></span>
### Step 2: Create Endpoint

Select the appropriate endpoint type based on your specific use case.

<span id=".5Yib5bu65o6l5Y-j57uI56uv6IqC54K5"></span>
#### Create an interface endpoint

For detailed steps, see [Creating an interface endpoint](https://docs.byteplus.com/en/docs/privatelink/Endpoint-02). Key parameters include:


* Select interface as the **Type**.

* **Endpoint Service**:​​ Select the name obtained in [Step 1](https://docs.byteplus.com/en/docs/privatelink/Sharing-on-cloud-TOS-with-a-data-center#.5q2l6aqk5LiA77ya6I635Y-W57uI56uv6IqC54K55pyN5Yqh5ZCN56ew).


After the interface endpoint is successfully created, you can view the endpoint domain name on the endpoint list page.


* The default endpoint domain format is: *Endpoint ID*.*Endpoint Service ID*.*region ID*.privatelink.volces.com.

* The wildcard domain format is: \*.*Endpoint ID*.*Endpoint Service ID*.*region ID*.privatelink.volces.com.


<span id=".5Yib5bu6572R5YWz57uI56uv6IqC54K5"></span>
#### Creating a gateway endpoint

For detailed steps, see [Creating a gateway endpoint](https://docs.byteplus.com/en/docs/privatelink/Endpoint-03). Key parameters include:


* Type: Select gateway.

* Endpoint Service:​​ Select the name obtained in [Step 1](https://docs.byteplus.com/en/docs/privatelink/Sharing-on-cloud-TOS-with-a-data-center#.5q2l6aqk5LiA77ya6I635Y-W57uI56uv6IqC54K55pyN5Yqh5ZCN56ew).

* Configure access policies according to your specific requirements.​​ For example, ​to grant read\-only access to a specific private bucket and all its objects via PrivateLink, configure the access policy as follows:​​

   ```Plain Text
           { 
              "Statement" : [
               {
                  "Effect": "Allow",
                  "Principal": [
                    "trn:iam::210005****:user/test",  # 指定允许主账号210005****下的用户test访问相应的存储桶
                    "trn:iam::210006****:root"   # 指定允许主账号210006****下的所有用户访问相应的存储桶
                  ],
                  "Action":[            # 指定可执行的操作
                    "tos:ListBuckets",
                    "tos:ListObject*"
                  ],
                  "Resource":[
                    "trn:tos:::bucketname/*"  # 指定私有存储桶的名称
                  ]
                }
              ]
     }
   ```
   


<span id=".5q2l6aqk5LiJ77ya57uT5p6c6aqM6K-B"></span>
### Step 3: Result verification


1. Log in to a server within your on\-premises IDC or VPC.​​

2. For Interface Endpoints, execute the `ping` command targeting the Endpoint Domain name to test network connectivity. For Gateway Endpoints, skip this step.​​

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the interface endpoint has the wildcard domain name enabled, please note during validation that the \* in the endpoint domain name must be replaced with any string, or you can directly use the root domain name.   </div>
   

3. Access TOS by calling APIs or SDKs to validate functionality.​​

   For example, to list all objects in a specific bucket via PrivateLink, the request parameters are described as follows:​​

   * Interface Endpoint

      * When making API calls, set the **Host** header to the endpoint's domain name.​​

         ​Taking the example of calling the API to list objects, a sample request is shown below.

         ```Plain Text
         GET / HTTP/1.1 
         Host: ep-3rf21wq2bsh6o5zsk2ipt****.tos-s3.cn-beijing.privatelink.volces.com  ## 传入终端节点域名
         Date: Fri, 30 Jul 2021 08:05:36 GMT 
         Authorization: authorization string
         ```
         

      * When accessing via SDK, using Go SDK as an example: Pass in the **accessKey** and **secretKey** as the AK and SK of the account to which the endpoint belongs, pass in the **endpoint** as the endpoint domain, pass in the **region** as the region ID to which the endpoint belongs, pass in the **bucketName** as the name of the bucket to be accessed.

   * Gateway Endpoint

      When accessing via API or SDK, configure all parameters with your TOS information. Access to authorized buckets and operations will succeed, while attempts to access unauthorized buckets will return a permission error.​​
