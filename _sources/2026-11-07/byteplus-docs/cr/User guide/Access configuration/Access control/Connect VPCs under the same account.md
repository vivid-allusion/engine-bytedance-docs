---
title: "Connect VPCs under the same account"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/connect-vpcs-under-the-same-account"
---

CR supports connecting instances with private network VPCs under the same account, enabling resources within the VPC (cloud servers, container services, and more) to access instances via the internal network. This enables high\-speed and stable image push and pull, while avoiding public network bandwidth costs.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This action applies only to Standard Edition instances.</div>


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To establish the connectivity between a CR instance and a VPC, the private domain name of the instance needs to be resolved to an IP address within that VPC. Therefore, for each VPC you associate with an instance, one <strong>private domain name (PrivateZone) record</strong> and one <strong>Elastic network interface (ENI)</strong> are automatically created for resolution. </div>


<span id="LTVt7Hpw"></span>
## Background

VPC connectivity under this account includes the following two scenarios. Both require the VPC and CR instance to be under **the same account and region**:


|**Scenario** |**Description** |**Typical usage scenarios** |
|---|---|---|
|**Connect this account's VPC** (User VPC) |Connect the VPC subnet created by the user in this account with the CR instance. After configuration, resources within the selected subnet can access the CR instance via the private network address to push and pull images. |Resources such as ECS and self\-built Kubernetes require pulling images via the internal network. |
|**Connect cross\-product VPC** (Service VPC) |Connect other cloud products under this account (such as Container Service VKE) that automatically create or use VPCs with CR instances. These VPCs are managed by the cloud product service and can only be selected after cross\-service authorization. |Other cloud products, such as VKE clusters, require password\-free pulling of images via the internal network. |


<span id="DuYZCrDJ"></span>
## Usage limits


* Only VPCs under the same account and region are supported for connectivity.

* The total number of VPCs under this account and cross\-service VPCs cannot exceed 5. If you have reached this quota, delete any unnecessary VPC associations or request a quota increase. For instructions, see [VPC access quota](https://docs.byteplus.com/en/docs/cr/vpc-quota).

* Currently, only some products support cross\-product VPC connectivity, including [Machine Learning Platform](https://docs.byteplus.com/en/docs/mlp/Overview2), [FaaS](https://docs.byteplus.com/en/docs/faas/Release_notes), [ByteHouse Cloud Data Warehouse Edition](https://docs.byteplus.com/en/docs/bytehouse/docs-bytehouse-overview), and more.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A Standard Edition instance has been created. For instructions, see [Create standard instance ](https://docs.byteplus.com/en/docs/cr/create-a-container-registry-enterprise-edition-instance).

* Connect VPCs under this account: A VPC and subnet have been created in the same region. For instructions, see [Create VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC?_vtm_=a106466.b106468.0_0.0_0.0.735_7610249723459077638) and [Create subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet).

* Connect cross\-product VPCs: Cross\-service authorization for CR has been activated in the target product. When using CR\-related features in the target product for the first time, the system will automatically display the **cross\-service access request** page. After confirming the access role and associated policy information, click **Authorize now** to complete.


<span id=".5pON5L2c5q2l6aqk"></span>
## **Connecting to the VPC of the current account**


1. Log in to the target instance.

   1. Log in to the [CR console](https://console.byteplus.com/cr).

   2. Select the target region in the top navigation bar.

   3. In the left navigation bar, click **List of instances**, find the target instance, and click **Enter instance**.

2. In the left navigation bar, click **Access control**. On the Access control page, click **Add VPC**.

3. Configure the VPC to be added.

   
   |Parameter |Description |
   |---|---|
   |Account |Select **This account**. |
   |Associated project |The associated target project. After association, members in the project will obtain the corresponding permissions for the CR according to the project authorization. For details, see [Project management](https://docs.byteplus.com/en/docs/organization/OrganizationSetup). |
   |VPC |Select an existing VPC. After the VPC is added, internal network push and pull of images and Helm charts are enabled among clusters in this VPC. |
   |Subnet |Select the private network subnet to connect. After configuration, resources within the selected subnet can access the instance via the private network to push or pull images. |
   

4. Click **Confirm** to complete the configuration.


<span id="iiywyIhC"></span>
## **Connecting VPCs across products**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Currently, only VPCs associated with the <strong>default security group</strong> named <code>Default</code> are supported. If the <strong>default security group</strong> name has been modified, change it back to <code>Default</code> before proceeding. To view the default security group of a VPC, see <a href="https://docs.byteplus.com/en/docs/vpc/Viewing-details-of-a-VPC">Viewing VPC details</a>.</div>



1. Log in to the target instance.

   1. Log in to the [CR console](https://console.byteplus.com/cr).

   2. Select the target region in the top navigation bar.

   3. In the left navigation bar, click **List of instances**, find the target instance, and click **Enter instance**.

2. In the left navigation bar, click **Access control**. On the Access control page, click **Add VPC**.

3. Configure the VPC to be added.

   
   |Parameter |Description |
   |---|---|
   |Account |Select **Cross\-service,**  and select the authorized BytePlus account. |
   |Tier |Select **New version**, and select the VPC associated with another product. |
   

4. Click **Confirm** to complete the configuration.
