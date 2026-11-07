---
title: "[New Feature] Pay by the volume"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/New_Feature_Pay_by_the_volume"
---

When you want to pay as much as you want, you can use BytePlus Machine Learning Platform's pay\-per\-use approach to configure and use your resources. Creating a pay\-per\-use type of resource group is not charged, and is only billed for how long the resource is used after the load is successfully committed.

<span id="bb5f50fc"></span>
## pre\-preparation

<span id="d747e360"></span>
### 1. Register Account and Activate Service

Refer to [Register an account and open a service](https://docs.byteplus.com/docs/mlp/53985)[ ](https://www.volcengine.com/docs/6459/76345)to complete BytePlus [account registration ](https://console.byteplus.com/ml-platform/region:ml-platform+ap-southeast-1/dashboard)and enterprise certification.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To do the following, log in to the <a href="https://console.byteplus.com/home">main account </a>or a sub account with global <a href="https://console.byteplus.com/iam/policymanage">AdministratorAccess </a>privileges.</div>


<span id="68d5668c"></span>
### 2. Activate related services

Refer to the official website help document to Activate associated services, including network, storage, Container Registry and other resources.

<span id="eddc242d"></span>
### 3. Network configuration

<span id="e8fdcdb6"></span>
#### **Private networks** `are required`

Open the [Private Networks Console - Private Networks ](https://console.byteplus.com/vpc/region:vpc+ap-southeast-1/vpc?)to reuse existing private networks and subnets; or Create new private networks and subnets.


1. **Geography \- Availability Zones** are the same as Hashrate resources.

2. Network segment planning on demand to avoid network segment conflicts in scenarios such as dedicated line/CEN.

3. Please increase the number of available IPs in the subnet segment as needed (not less than the number of GPU cards is recommended), for example, CIDR = 20 Available IPs = 4093 or more.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5e0989d0b80643738564e7e621b39982~tplv-goo7wpa0wc-image.image) </span>

<span id="b58ea8fd"></span>
#### **SecurityGroup** `must`

Open the [Private Network Console - SecurityGroup ](https://console.byteplus.com/vpc/region:vpc+ap-southeast-1/securityGroup), under the aforementioned private network, the following connectivity needs to be guaranteed for the default SecurityGroup "Configuration Rule" or "Create SecurityGroup".


|access rules |strategy |protocol type |port range |Destination address |Description |
|---|---|---|---|---|---|
|out direction |allow |on demand |on demand |on demand |Select the traffic that needs to be released on demand |
|Incoming direction |allow | |2222 | |Dev boxes SSH login |
||| |10000 | |Dev boxes/custom tasks WebIDE |
||| |12222 | |Custom training framework communication |
||| |3389 | |RDP Remote Desktop |
||| |80 | |HTTP default port |
||| |443 | |HTTPS default port |
||| |5082 | |On\-demand, CloudFS dependencies |
||| |5092 | |On\-demand, CloudFS dependencies |
||| |ALL |SecurityGroup |interoperability |


<span id="858b2b2e"></span>
### 4. Container Registry Configuration

Open the [Container Registry console ](https://console.byteplus.com/cr/region:cr+ap-southeast-1/instances?tab=enterprise)and follow the prompts to activate BytePlus Container Registry service.


1. Create **standard version** instance, the **region** and computing power resources are the same, wait for the instance status to change to [running] (may take 5~ 10 minutes)

2. Go to Instance \- Namespace \- Create namespace, Create a namespace for Dev boxes mirror archive

3. Go to Instance \- Identity and Access Management \- Add VPC and select Multiplex/Create Private Network


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/235fce3e4fd4437ba54b4e829e2120aa~tplv-goo7wpa0wc-image.image) </span>

After activating the whitelist, log in to the Machine Learning Platform with the registered BytePlus main accoun\*\*t [Machine Learning Platform with the registered BytePlus main account](https://console.byteplus.com/ml-platform/region:ml-platform+ap-southeast-1/dashboard), and the cross\-service authorization page will automatically pop up when entering the platform. After submitting the form, you can complete the cross\-service authorization of dependent services such as Torch Object Storage and Container Registry.

At this point, all the required services have been Activated. Next step, the main account will create the corresponding sub\-user account for the ordinary developer (optional).

<span id="4ce7f2b7"></span>
### 5. Create sub account (optional)

Log in to [Identity and Access Management ](https://console.byteplus.com/iam/identitymanage/user)with the registered BytePlus main account, create sub account and configure permissions. If it is not a BytePlus main account, [MLPlatformAdmin ](https://console.byteplus.com/iam/policymanage)permission is required to add sub accounts.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/922b59412c464d3685ddb43ccbaaee57~tplv-goo7wpa0wc-image.image) </span>

It is recommended to grant the following permissions on demand:


* [MLPlatformDeveloperAccess ](https://console.byteplus.com/iam/policymanage)Machine Learning Platform Developer Permissions Required

* [AccessKeyFullAccess ](https://console.byteplus.com/iam/policymanage): permissions for your key management \- required when using command line tools, tos, etc


More Preset Permissions Reference: [Preset Policies](https://arcosite.bytedance.net/sites/1689750851223/67dd0d78549d85051ff6a312/editor/685a62d80079c10520f88eb6?docLang=en&bv=67dd0d7a549d85051ff6a324).

<span id="985cd780"></span>
## Create Resource Group

Recommended as the main account.

Open the [Create Resource Group ](https://console.byteplus.com/ml-platform/region:ml-platform+ap-southeast-1/resourceGroup/create?from=%2Fml-platform%2Fregion%3Aml-platform%2Bap-southeast-1%2FresourceGroup&chargeType=PrePaid)page (entrance: Console \> Resource Group \> Pay\-per\-Volume), follow the console guidelines, and create a pay\-per\-Volume resource group. The following describes the core configuration involved.

<span id="a77ffd94"></span>
### 1. Load network configuration


* If the load network is not associated with a private network VPC/SecurityGroup to complete configuration.

* In the pay\-per\-volume model, inventory changes in real time. When configuring a subnet, it is recommended to override all availability zones.

* When you commit a load with pay\-per\-use resources, the allocation of resources is determined based on the subnet availability of the load network.

> For example, when only configuring [Availability Area B], only the resources of [Availability Area B] are supported when submitting the load. If there is no stock in Area B, Create will not be supported; if there are resources in the same specification [Availability Area C] at this time, Create can be directly successful.


* If the required Availability Zone is not bound to a subnet, please go to the global configuration to complete the authorization before going to the console to Create a resource group.

* It is recommended to carry out network connectivity diagnosis, verify VPC, APIG, mirror and other network configurations to ensure network access.


<span id="e17d23a3"></span>
### 2. Storage network configuration instructions (optional)

If you need to use NAS storage products on pay\-per\-use loads, you can associate storage networks here.


* Storage Private network VPC: Default selection of global configuration authorized VPC, storage VPC Associate does not support modification.

* Subnet: By default, select the global configuration authorized subnet, and the storage subnet needs to be consistent with the availability zone of the load subnet.


<span id="a689e5cc"></span>
## Create Queue

The main account can further split the resource group resources into queues according to business needs and project requirements.

Operation entrance:


* Create Queue in the actions column of the resource group on the [Resource Groups ](https://console.byteplus.com/ml-platform/region:ml-platform+ap-southeast-1/resourceGroup?current=1&pageSize=10)list page.

* You can also create a new queue in Queue Managcreate a new queue in Queue Management in the left navigation.

> Note that at the top of the menu bar, switch to the region where your resource group is located to see/select the corresponding resource group.


The core configuration is described below.

<span id="6c09d55e"></span>
### Configuration Management Instructions


* At least 1vCPU and above quotas should be allocated. The CPU quota is recommended to be greater than 16vCPU, and the cloud disk quota is recommended to be at least greater than 20GiB. If it is lower than this value or not configured, Dev boxes cannot be created normally.

* The quota unit of a GPU is the number of cards.

* You, the administrator, can authorize queues for users, see [Manage users in a queue](https://docs.byteplus.com/docs/mlp/Manage_users_in_a_queue).

> For more queue management operations, see [Manage users in a queue](https://docs.byteplus.com/docs/mlp/Manage_users_in_a_queue).


<span id="075e1173"></span>
## Create pay\-per\-use payload

When you Create a workload, select the Pay\-per\-Volume Queue type to Create a Pay\-per\-Volume payload. Take Create Dev boxes as an example to know how to configure it.

Open the [Dev boxes ](https://console.byteplus.com/ml-platform/region:ml-platform+ap-southeast-1/devinstance/create)Create page, the top menu bar toggles the region for your pay\-per\-use queue region, and follows the console guidelines to configure. The following describes the pay\-per\-use core parameters, see the full configuration instructions [Create Dev boxes](https://docs.byteplus.com/docs/mlp/Create_Dev_boxes).

<span id="aacbc181"></span>
### 1. Queue configuration

When selecting a queue, please select the [Pay Per Volume] type


* After selecting the queues, you can see the remaining available quotas for each queue.

* During the load submission process, the maximum specification set cannot exceed the quota limit of the queue, otherwise the load will not be successfully committed.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e8078c1157034a86b31265c323185afe~tplv-goo7wpa0wc-image.image) </span>

<span id="01f70f0a"></span>
### 2. Calculation specifications


* The platform supports instance specifications of [high\-performance computing GPU type], [GPU computing type], [general\-purpose type], [memory type] and [computing type].

* saleable health

   * When the health of an instance is [sufficient], it means that the specification is fully resourced in the current availability zone.

   * When the health level is [tight], it means that the resource is about to be sold out. If you need a lot of resources, it is recommended to replace it with another specification with sufficient health.

   * When Health is [Out], the resource is sold out and you cannot select the instance Create.

* When the resources are sufficient, but the resource group does not configure the subnet of the availability zone, the instance specification of the availability zone cannot be selected. Please contact the resource administrator [Change Load Network] before Create.


<span id="08b70bf9"></span>
### 3. Storage Mount


* When using a pay\-per\-use queue, Mount [TOS] and [NAS] types of storage are supported.

* When mounting [NAS], you need to first associate the storage network in the resource group. The subnet of the storage network on the resource group needs to be consistent with the subnet availability zone of the load network.


<span id="28fece70"></span>
### 4. Create the result description


* When the resources are sufficient, the load will be created in a very short time, please be patient.

* When the load status is "Running", billing starts.

   * Dev boxes: When the development machine is shut down, the cloud disk will continue to be billed; only when the Dev boxes are deleted, the cloud disk will stop billing.

   * Custom tasks: Billing ends when a task fails or completes.

   * Inference services: billed only on the fly.

* When resources are insufficient, the load will enter a queued state; you can replace other instances with sufficient resources or bind subnets in all available areas where resources are available.
