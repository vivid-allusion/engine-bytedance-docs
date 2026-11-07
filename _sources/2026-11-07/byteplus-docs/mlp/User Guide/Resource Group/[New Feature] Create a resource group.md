---
title: "[New Feature] Create a resource group"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/NewFeature_Create_a_resource_group"
---

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">V2.0 function summary:</div>



1. <div data-tips="true" data-tips-type="tip">[Need to be opened] <strong>The VPC associated with PFS can be inconsistent with the VPC bound to the global configuration</strong> , and supports binding multiple VPC networks</div>


   1. <div data-tips="true" data-tips-type="tip">If your resources have multiple VPC environment isolation requirements, you can bind multiple VPC networks in the global configuration and associate them with the corresponding resource group when placing an order to achieve network isolation of machines and loads</div>


   2. <div data-tips="true" data-tips-type="tip">If you have multiple requests for PFS instances, and the VPCs associated with PFS instances are inconsistent, you can create two PFS mount service implementations in the global configuration</div>


2. <div data-tips="true" data-tips-type="tip"><strong>Support dynamic mounting and unbinding of PFS instances in resource groups, that is, you can decide whether to mount PFS instances when purchasing machines</strong></div>



<span id="如何使用"></span>
## How to use

> **Global configuration** completes the authorization and binding of all dependent services, and completes the configuration at each load.


<span id="全局配置"></span>
### global configuration

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">New features:</div>



1. <div data-tips="true" data-tips-type="tip">PFS VPCs are no longer strongly associated with global configuration VPCs</div>


2. <div data-tips="true" data-tips-type="tip">Support for configuring and binding multiple VPCs</div>


3. <div data-tips="true" data-tips-type="tip">Supports binding multiple PFS mount services (VPCs to which PFS instances belong are inconsistent)</div>


1. Log in to the Machine Learning Platform console and click [global configuration] to enter the corresponding page

2. Select the **VPC module** and click [Configure Private Network]

   **Please note that when binding a VPC, try to choose a VPC with a larger network segment to ensure that the number of available IPs meets your business scenarios.** 

> It is recommended that the network segment size of the private network be between/8~/16\-bit network masks, and the availability area subnet network segment mask is less than or equal to /20, so as to meet the subsequent creation of subnets in other availability areas, and to avoid IP exhaustion caused by too small subnet network segments, such as:

> VPC CIDR: [172.24.0.0/16 ](http://172.24.0.0/16)number of IPv4 available 65533

> * Availability Zone A subnet CIDR: [172.24.0.0/20 ](http://172.24.0.0/20)number of IPv4 available 4093

> * Availability Zone B subnet CIDR: [172.24.16.0/20 ](http://172.24.16.0/20)number of IPv4 available 4093

> * Availability Zone C subnet CIDR: [172.24.32.0/20 ](http://172.24.32.0/20)number of IPv4 available 4093

   > You can reasonably plan the size of private networks and subnets according to the future demand for the number of IPs, and **it is not recommended** :

> * A single subnet fully occupies the entire private network segment.

> * The subnet segment is too small, for example, the mask bit is greater than or equal to /24.

3. Private network:

   1. Select the private network and subnet you need to license to the MLP

   2. The subnet supports multiple selection, and the selected subnet availability area must be consistent with the availability area where the machine resources are located

4. Public network: (If this part is not set, please contact Volcano oncall Kaibai)

   1. When allowing public network access, Dev boxes can log in and access in the public network environment, and also need to configure the NAT gateway and public network IP required for public network login.

   2. When public network access is disabled, Dev boxes can only be logged in and accessed through private networks (WebIDE and SSH remote access).

> Each workload container of the Machine Learning Platform consumes 1 ENI and 1 VPC subnet IP. The number of targets required is the sum of the following three parts:

> ```Plain Text
  * Sum (number of Dev boxes created), both on and off Dev boxes are required
  * Sum (the number of custom tasks instances in the Running state), for example: 2 12 machine x card training tasks, 24 required
  * Sum (the number of inference service instances in the Running state), for example: 2 30 machine x card training tasks, 60 required
```



<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/65d00e44931440978e8b4ae0c7b5113a~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/569561f2a0974463852a2c05bb81bc61~tplv-goo7wpa0wc-image.image) </span>


3. [Optional] Select the **PFS module** and click [Bind PFS]

   1. Please select the PFS instance you want to use

      1. If you have bound a PFS instance 1, and the VPC associated with the PFS instance 2 to be bound is inconsistent with the VPC associated with the PFS instance 1, a new mount service will be created; if the VPCs are consistent, a new PFS mount instance will be added under the mount service

   2. After binding the PFS instance, you can configure the mount permission for the instance

      1. For example, set the "/" root directory, only user group xx1 has read permission, and user group xx2 in the "/mlptest" directory has read permission

   3. When there is no bound PFS mount instance under the mount service, it will be automatically deleted and unrecoverable.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/185858e9f75e4762aea5c2f21fcf5b29~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d3caf7d58dfa4a73aaafa253793f21c1~tplv-goo7wpa0wc-image.image) </span>

<span id="资源组"></span>
### Resource Group

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">New features:</div>



1. <div data-tips="true" data-tips-type="tip">Supports configuration in the resource group dimension, private network VPC, subnet, and SecurityGroup</div>


2. <div data-tips="true" data-tips-type="tip">Support binding PFS instances by resource group dimension</div>


3. <div data-tips="true" data-tips-type="tip">Support for configuring different networks for load and storage (load refers to Dev boxes, custom tasks, and inference services; storage refers to PFS and NAS)</div>


   <div data-tips="true" data-tips-type="tip">:::To create a resource group, you need to complete the following configuration items:   </div>
   

   <div data-tips="true" data-tips-type="tip">    </div>
   


<div data-tips="true" data-tips-type="tip"></div>


<div data-tips="true" data-tips-type="tip">
|step |Parameter |Note |Demo |
|---|---|---|---|
|Computing configuration |<strong>Concept</strong> |* <strong>Required field</strong><br><br>* Supports 1 to 200 visible characters, and only includes uppercase and lowercase letters, Chinese, numbers, dashes, and underscores |<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5745fe52c20a42b6a9239500b5089857~tplv-goo7wpa0wc-image.image" width="2656px" /><br><br><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/78adb6013e9a4202b79cdf979caf0d11~tplv-goo7wpa0wc-image.image" width="2602px" /> |
||<strong>Description</strong> |* Optional field<br><br>* Supports 1 to 500 characters ||
||<strong>Billing Method</strong> |* <strong>Required field</strong><br><br>* Prepaid: monthly purchase and renewal, suitable for medium and long\-term stable business<br><br>* Post\-paid: use first and then pay, suitable for short\-term elastic needs, charged when using resources, no charge for creating resource groups ||
||<strong>Region</strong> |* <strong>Required field</strong><br><br>* The intranets in different regions are isolated from each other. It is recommended to choose an area closer to your business to reduce network latency and improve access speed.<br><br><blockquote data-wrapper-indent="0">Support,</blockquote><br><br><blockquote data-wrapper-indent="0">Hong Kong, China (HKG)</blockquote><br><br><blockquote data-wrapper-indent="0">Singapore (SGP)</blockquote><br><br><blockquote data-wrapper-indent="0">Japan (JPN)</blockquote><br><br><blockquote data-wrapper-indent="0">Korea (KOR)</blockquote><br><br><blockquote data-wrapper-indent="0">Cayman Islands (CYM)</blockquote><br><br><blockquote data-wrapper-indent="0">Türkiye (TUR)</blockquote><br><br><blockquote data-wrapper-indent="0">Indonesia (IDN)</blockquote><br><br><blockquote data-wrapper-indent="0">Brunei (BRN)</blockquote><br><br><blockquote data-wrapper-indent="0">Sri Lanka (LKA)</blockquote><br><br><blockquote data-wrapper-indent="0">Vietnam (VNM)</blockquote><br><br><blockquote data-wrapper-indent="0">Thailand (THA)</blockquote><br><br><blockquote data-wrapper-indent="0">Malaysia (MYS)</blockquote><br><br><blockquote data-wrapper-indent="0">Philippines (PHL)</blockquote><br><br><blockquote data-wrapper-indent="0">Qatar (QAT)</blockquote><br><br><blockquote data-wrapper-indent="0">Saudi Arabia (SAU)</blockquote><br><br><blockquote data-wrapper-indent="0">British Virgin Islands (VGB)</blockquote> ||
||<strong>Availability Zone</strong> |* <strong>Required field</strong><br><br>* Availability zone refers to the physical area where power and network are isolated in the same area. Within the same private network, availability zones communicate with each other.<br><br><blockquote data-wrapper-indent="0">The availability zone to which the resource belongs needs to be consistent with the availability zone to which the load network/storage network belongs</blockquote> ||
||<strong>calculation specification</strong> |* <strong>Required field</strong><br><br>* Support for selection, pure CPU specs, GPU specs, and high\-performance GPU specs for RDMA networks<br><br>* If you encounter insufficient resources, please contact BytePlus customer service students to increase the sample quota. ||
||<strong>Cloud disk</strong> |* Optional field<br><br>* If you need to use Dev boxes, you must purchase a cloud disk with a certain capacity. A single Dev box requires at least 20GiB.<br><br><blockquote data-wrapper-indent="0">The cloud disk will be mounted as persistent storage in the root directory/, and the data in this directory will be preserved after shutdown or restart</blockquote><br><br>* Supports the choice of two specifications: Extremely Fast SSD PL0 and Extremely Fast SSD FlexPL, the latter has the best single disk maximum IOPS and maximum throughput. If you have higher throughput requirements when using Dev boxes, you can choose the FlexPL specification. ||
|Storage and network configuration |<strong>Load network configuration</strong> |* <strong>Required field</strong><br><br>* When creating workloads for the Machine Learning Platform (Dev boxes, custom tasks, and inference services), private network VPCs, subnets, and SecurityGroups are required<br><br>* The selected VPC must be bound in the global configuration, and the availability zone of the selected subnet needs to be consistent with the availability zone where the instance resource is located |<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ea6f333128ab4af99346e76888de3f6a~tplv-goo7wpa0wc-image.image" width="1976px" /> |
||<strong>Storage Network Configuration</strong> |* <strong>Required field</strong><br><br>* When creating workloads for the Machine Learning Platform (Dev boxes, custom tasks, and inference services), private network VPCs, subnets, and SecurityGroups are required<br><br>* The selected VPC must be bound in the global configuration, and the availability zone of the selected subnet needs to be consistent with the availability zone where the instance resource is located ||
||<strong>PFS configuration</strong> |* File storage PFS is a high\-throughput, low\-latency, and scalable parallel file system service introduced by BytePlus, which meets the data reading and writing requirements of high\-throughput and low\-latency in high\-performance computing scenarios.<br><br>* Make sure the binding of the global configuration PFS instance is complete<br><br>* After binding the PFS instance, you can mount the PFS shared file system on the training/service/development machine<br><br>* The VPC network and storage network where the PFS instance is located must be consistent, otherwise it cannot be created<br><br><blockquote data-wrapper-indent="0">After the resource group is successfully purchased, the PFS instance will be mounted on the purchased machine. You can check the mount progress on the resource group list page.</blockquote> ||
||<strong>SFCS configuration</strong> |* The local disk on the GPU node is used as a data cache service, which has the characteristics of high performance, ease of use and multi\-compatibility<br><br><blockquote data-wrapper-indent="0">This function requires clarification</blockquote> ||
|Confirm the order |<strong>\-</strong> |* Select the purchase time, and the prepaid support is 7 days, 1 month, 1 year, etc.<br><br>* tick agreement |<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/33ae8e5a89c5486fb4e7a75855f3be7b~tplv-goo7wpa0wc-image.image" width="2542px" /> |
</div>


<div data-tips="true" data-tips-type="tip">FAQs</div>


<span id="怎么感知vepfs绑定的进度？"></span>
### <div data-tips="true" data-tips-type="tip">How to sense the progress of PFS binding?</div>



* <div data-tips="true" data-tips-type="tip">If you need to use the file system PFS in the Machine Learning Platform, select the global configuration bound PFS instance when creating the resource group.</div>


* <div data-tips="true" data-tips-type="tip">The PFS instance is bound asynchronously after the resource group order is placed. You can check the binding progress on the resource group list page [PFS Instance]</div>



<span id="资源组绑定的负载网络是否可以变更？"></span>
### <div data-tips="true" data-tips-type="tip">Can the load network bound to a resource group be changed?</div>



* <div data-tips="true" data-tips-type="tip">Supports changing the load network configuration after creating a resource group, and supports replacing VPC, subnet, and SecurityGroup.</div>


* <div data-tips="true" data-tips-type="tip">If you will use products such as NAT gateway/Internet Express/Container Registry/load balance on the Machine Learning Platform, you also need to update synchronously when changing the VPC</div>


* <div data-tips="true" data-tips-type="tip">After replacing a VPC, the existing load does not change; only newly committed loads will use the new VPC.</div>


   * <div data-tips="true" data-tips-type="tip">Dev boxes replacement VPC will not take effect</div>


   * <div data-tips="true" data-tips-type="tip">If you add a new SecurityGroup, it will not take effect on the existing Dev boxes; if you need to take effect on the existing Dev boxes, please change the inbound and outbound configuration of the existing bound SecurityGroup</div>
