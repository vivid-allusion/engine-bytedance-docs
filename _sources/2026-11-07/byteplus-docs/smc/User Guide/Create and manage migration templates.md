---
title: "Create and manage migration templates"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/Create_and_manage_migration_templates"
---

You can use migration templates to plan target instances in advance. The Server Migration Center (SMC) creates target instances automatically based on your specified migration templates during the migration process, reducing resource wastage caused by manually creating target instances beforehand.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The migration template feature is currently in Beta. If you need a trial, please contact your account manager.</div>


<span id="7QfSZUWi"></span>
## Create a new migration template

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">A maximum of 50 migration templates are supported per account.</div>


* <div data-tips="true" data-tips-type="default">The instances planned in the migration template must meet <a href="https://docs.byteplus.com/en/docs/smc/Preparations#.5YeG5aSH55uu5qCH5a6e5L6L">target instance specifications</a>.</div>



<span id="7QfSZUWi"></span>
### Create a migration template

You can create a migration template from scratch, configuring details such as target instance specifications, OS type, Volumes, and network information within the template.


1. Log in to the [ECS console](https://console.byteplus.com/auth/login?redirectURI=%2Fecs%2Fregion%3Aecs%2Bap-southeast-1%2Finstance).

2. In the left directory tree under any region, select "Server Migration Center \> Migration Template".

3. In the top menu bar, select the project to which the target migration template belongs.

4. Click the "Create Migration Template" button and fill in the following arguments.

   
   |Parameter​ |Description |Sample value |
   |---|---|---|
   |**Basic information** |||
   |Name |Specify the name of the migration template. |bj\-g3il |
   |Project |Specify the project to which the migration template belongs. A project is a set of resources. You can add the migration template created this time to the project for project\-based management. This helps maintain resource isolation and ensure data security. For more information on projects, refer to [Managing projects](https://docs.byteplus.com/en/docs/ecs/Managing-projects).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">By default, the project is <code>default</code>. Each resource can only belong to one project.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Once a project is selected, the created migration template can only be used by users with permission for that project.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When accessing the creation page, if you have already selected a specific project via the top menu bar, the newly created migration template can only be associated with that project. If you want to associate it with another project, change the top menu bar project to "All Resources" or the target project.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If no project is available, click "New project" to <a href="https://docs.byteplus.com/en/docs/resourcemanagement/Project_Management#creating-project">create a project</a> in the IAM console. After you create the project, return to the creation page and select the created project.</div><br> |default |
   |Region and AZ |Specify the Region and AZ where the target instance created using the designated migration template is located. [Learn more](https://docs.byteplus.com/en/docs/ecs/Regions-and-Availability-Zones). |China (Beijing) Availability Zone A |
   |Billing method |Select the target instance and Volume's metering methods. Value:<br><br><br>* [Pay-as-you-go](https://docs.byteplus.com/en/docs/ecs/Pay-as-you-go): You are charged based on the usage duration, which is calculated in hours. This option allows you to create and delete ECS instances as needed.<br><br>* [Subscription](https://docs.byteplus.com/en/docs/ecs/Subscription): You are charged a subscription fee based on the subscription duration. |Pay\-as\-you\-go |
   |Instance type |Specify the target instance's specification.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">ECS instances of different types offer different network and storage rate limiting capabilities. You can choose an instance type based on your business requirements. <a href="https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types">Learn more</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Instance types available for sale may vary in different regions and availability zones. You can view the availability zones and regions available in the "Availability zone" column of the target instance type.</div><br> |ecs.g3il.xlarge |
   |Operating systems |Specify the target OS type, which must be consistent with the source server's operating system. Value:<br><br><br>* Linux<br><br>* Windows |Linux |
   |**Storage configuration** |||
   |Type |Specify the specification of the Volume to be mounted on the target instance. [Learn more](https://docs.byteplus.com/en/docs/ecs/Volume-specifications). |ESSD |
   |Performance level |Specify the Volume performance level. The selectable performance levels for different Volume specifications can be viewed in [Volume specifications](https://docs.byteplus.com/en/docs/ecs/Volume-specifications). |PL0 |
   |**Network configuration** |||
   |Virtual Private Cloud |Select the Virtual Private Cloud (VPC) where the target instance is located. Virtual Private Cloud (VPC) provides private network isolation features for your cloud environment, and private networks in different VPCs cannot communicate with each other.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If no VPC is available, you can click the “Create VPC” button to manually <a href="https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC">create a VPC</a>. After creation, you can select it on this page.</div><br> |vpc01 |
   |Subnet |Select a subnet to allocate the primary private IP address of the primary network interface for the instance. After selecting a subnet, you can choose the private IP address allocation method, which supports:<br><br><br>* Automatically allocated IP: Select to have the platform automatically allocate an available IPv4 address from the subnet.<br><br>* Maintain the IP: Keep consistent with the primary private IP address of the primary network interface of the source server.<br><br>* Fill in during creation: When you create the target instance, you manually specify an available IPv4 address from the subnet.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If no subnet is available, you can click the "Create Subnet" button to manually <a href="https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet">create a subnet</a>. After creation, you can select it on this page.</div><br> |subnet01 auto\-assign IP |
   |Security group |The security group controls the outbound and inbound traffic of the Elastic Compute Service (ECS) network interface, and the ECS must attach a security group. [Learn more](https://docs.byteplus.com/en/docs/ecs/Security-group-overview).<br><br><br>* Security groups are designed based on the allowlist principle. By default, security groups deny the inbound and outbound traffic of network interfaces. You can add security group rules based on your needs to allow traffic.<br><br>* Each network interface can be associated with up to 5 security groups.<br><br>* After creating an ECS instance, you can also change the [security group](https://docs.byteplus.com/en/docs/ecs/Changing-security-groups) of its network interface based on your needs. |Default |
   |**EIP** |||
   |EIP |When you create an ECS instance, an EIP is automatically assigned by default. The EIP is associated with the primary private IP of the primary network interface. This enables the instance to be accessed via Internet. After creating the instance, you can also [associate an EIP](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP) with the instance based on your needs. |\- |
   |ISP | BGP (Multi\-ISP) is supported. |BGP (Multi\-ISP) |
   |Billing method |EIPs support pay\-as\-you\-go and subscription billing methods. For more information, refer to [Billing overview](https://docs.byteplus.com/en/docs/eip/Billing-overview).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the billing method of the ECS instance is pay\-as\-you\-go, you can not select the subscription billing method for the EIP on this page. If you need to associate a subscription\-based EIP with a pay\-as\-you\-go instance, manually <a href="https://docs.byteplus.com/en/docs/ecs/associating-an-EIP">associate an EIP</a> after you create the instance.</div><br> |Pay\-as\-you\-go |
   |Billing method |After choosing pay\-as\-you\-go as the billing method for the instance, you need to select a metering method for the EIP. [Pay-by-bandwidth](https://docs.byteplus.com/en/docs/eip/Pay-as-you-go#pay-by-bandwidth) and [Pay-by-data-transfer](https://docs.byteplus.com/en/docs/eip/Pay-as-you-go#pay-by-data-transfer) are supported. |Pay\-by\-data\-transfer |
   |Maximum bandwidth |Default: 50 Mbps |50 |
   

5. Click the "Confirm" button to submit the template creation request.


<span id="h44dYVCy"></span>
### Copy migration template

You can create a new migration template based on an existing one through the copy feature.


1. Log in to the [ECS console](https://console.byteplus.com/auth/login?redirectURI=%2Fecs%2Fregion%3Aecs%2Bap-southeast-1%2Finstance).

2. In the left directory tree under any region, select "Server Migration Center \> Migration Template".

3. In the top menu bar, select the project to which the target migration template belongs.

4. Click the “target migration template” on the right<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_92a57b0547f038c32e59d8048035f1b9.png) </span>\> Copy Template button.

5. Modify the template configuration as needed; the parameters supported by the migration template can be viewed in [Create Migration Template](https://docs.byteplus.com/en/docs/smc/Create_and_manage_migration_templates#7QfSZUWi).

6. Click the “Confirm” button to submit the copy template request.


<span id="CuQuUhDz"></span>
## Manage migration templates

After successful creation, you can manage migration templates using the following feature.


|Operation |Description |
|---|---|
|view migration template |You can view the configuration of migration templates, including target instance type, OS type, Volume, network, and other information.<br><br><br>1. Log in to the [ECS console](https://console.byteplus.com/auth/login?redirectURI=%2Fecs%2Fregion%3Aecs%2Bap-southeast-1%2Finstance).<br><br>2. Select "Server Migration Center \> Migration Template" from the directory tree on the left.<br><br>3. Click the target template name to view the template and its instance configuration details on the right. |
|modify migration template |You can modify the name and description of an existing migration template.<br><br><br>1. Log in to the [ECS console](https://console.byteplus.com/auth/login?redirectURI=%2Fecs%2Fregion%3Aecs%2Bap-southeast-1%2Finstance).<br><br>2. Click the target template name.<br><br>3. Click the right side of "Template Name" or "Template Description".<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_86804c1fae8a6fd03433b13c83275062.png) </span>Click the button to update template information.<br><br>4. Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2e0d66ad52aac940b724cfafce87514c.png) </span> button to save changes. |
|Delete migration template |You can delete unused migration templates to avoid invalid templates occupying the quota.<br><br><br>1. Log in to the [ECS console](https://console.byteplus.com/auth/login?redirectURI=%2Fecs%2Fregion%3Aecs%2Bap-southeast-1%2Finstance).<br><br>2. Select "Server Migration Center \> Migration Template" from the left directory tree.<br><br>3. Click the "<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c64be9eb6bb04d1a8c9f63fd810f105b.png) </span>\> Delete Template" button on the right side of the migration template name.<br><br>4. In the pop\-up window, confirm the template information and click the "Delete" button. |
