---
title: "EIP overview"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/EIP-overview"
---

<span id=".SVB2NOWFrOe9kQ=="></span>
## IPv4 public network

Elastic IP Address (EIP) and its internet egress bandwidth are IP connectivity services provided by BytePlus. This services can be purchased and held separately for cloud resources.

After an ECS instance is associated with an EIP, the ECS instance can communicate with the internet.

For more information about EIP, see [What is EIP?](https://docs.byteplus.com/en/docs/eip/What-is-EIP).

**Related documents:** 


* [Associating EIP](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP)

* [Disassociating EIP](https://docs.byteplus.com/en/docs/ecs/Disassociating-an-EIP)

* [Viewing EIP bandwidth](https://docs.byteplus.com/en/docs/ecs/Network-FAQs#.5aaC5L2V5p-l55yL5a6e5L6L55qE5YWs572RaXDluKblrr3vvJ8=)

* [Modifying EIP metering methods and its bandwidth upper limit](https://docs.byteplus.com/en/docs/ecs/Changing_EIP_configuration)


<span id=".SVB2NuWFrOe9kQ=="></span>
## IPv6 public network

After you enable the IPv6 gateway in a VPC, only communication within the VPC is supported. You can enable IPv6 Internet bandwidth for an IPv6 address based on your business requirements. This way, the IPv6 address can communicate with the Internet. With the IPv6 gateway, you can flexibly configure IPv6 Internet bandwidth and the egress\-only rule, and control the outbound and inbound IPv6 Internet traffic for the VPC.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The IPv6 gateway feature is currently in <strong>Beta</strong>. If you need a trial, contact your account manager.</div>


For more IPv6 gateway details, see [What is an IPv6 gateway?](https://docs.byteplus.com/en/docs/IPv6/What_is_IPv6_Gateway).

<span id=".55u45YWz5qaC5b-1"></span>
## Related concepts


|Concept |Description |
|---|---|
|Private network bandwidth |Private network refers to the access link between ECS instances and cloud databases, CLB instances, or TOS buckets that reside in the same region and belong to the same VPC. Private network bandwidth is consumed when communications occur over the private network. However, you are not charged for private network bandwidth. The private network bandwidth varies based on the instance type. For more information about bandwidth values, see [Instance type families](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types#.5a6e5L6L6KeE5qC85peP5YiX6KGo). |
|Internet bandwidth |Internet bandwidth refers to the network traffic generated when an ECS instance accesses the internet. Internet bandwidth is divided into outbound bandwidth and inbound bandwidth. You are charged only for outbound bandwidth.<br><br><br>* Outbound bandwidth refers to the Internet bandwidth for data flowing from an ECS instance.<br><br>* Inbound bandwidth refers to the Internet bandwidth for data flowing into an ECS instance. |
|Bandwidth upper limit |The bandwidth upper limit varies based on the billing method and metering method of the EIP you purchase. For more information, see [Billing overview](https://docs.byteplus.com/en/docs/eip/Billing-overview#.6K6h6LS55oC76KeI). |
|Billing method |Billing methods for EIP include pay\-as\-you\-go and subscription. For more information, refer to [Billing Overview](https://docs.byteplus.com/en/docs/eip/Billing-overview). |
|Standard modification of instance specification |After you create an EIP instance, you can modify the upper limit of the EIP bandwidth at any time based on your business requirements. For more information, refer to [Standard modification of instance specification](https://docs.byteplus.com/en/docs/eip/Bandwidth-modifications#.5bi46KeE5Y-Y6YWN).<br><br><br>* Upgrade: Increase the bandwidth upper limit.<br><br>* Downgrade: Decrease the bandwidth upper limit.<br><br>* Modification cycle: The billing cycle during which the modification is applied. |
|Temporary specification upgrade |A temporary upgrade is suitable when you want to increase the upper limit of EIP bandwidth temporarily within a specified period. When the specified period expires (that is, at the specified restoration time), the bandwidth upper limit is automatically restored to the value before the modification. Temporary Modify Instance Spec is applicable for businesses with significant fluctuations that can be predicted, such as during holidays and promotions. For more restrictions, refer to [Temporary specification upgrade](https://docs.byteplus.com/en/docs/eip/Bandwidth-modifications#.5Li05pe25Y2H6YWN). |
