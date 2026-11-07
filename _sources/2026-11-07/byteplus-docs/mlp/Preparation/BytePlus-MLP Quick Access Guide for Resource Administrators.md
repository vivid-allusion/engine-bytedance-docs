---
title: "BytePlus-MLP Quick Access Guide for Resource Administrators"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/BytePlus-MLP_Quick_Access_Guide_for_Resource_Administrators"
---

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Provide <strong>thousands of large\-scale, high\-performance, high\-stability, cost\-optimized AI</strong> infrastructure solutions, providing customers with hundreds of hours of large\-scale model task engineering stability guarantee, PD separation inference computing power cluster up to 5 times throughput.</div>


<span id="0d0ad43d"></span>
# Overview

BytePlus MLP is a platform for professional algorithm engineers to integrate cloud\-native tools + computing power (GPU, CPU Cloud as a Service) for one\-stop AI algorithm development and iteration.


|Product name |MLP, Machine Learning Platform |
|---|---|
|Description |Machine Learning Platform |
|official website |https://console.byteplus.com/ml\-platform/region:ml\-platform+ap\-southeast\-1/dashboard?guideTab=mlDevelopment |
|Geographies and Availability Zones |Asia Pacific (Johor)/Southeast Asia Pacific (Johor) |
|Open country and region |`Hong Kong (HKG)`, `Singapore (SGP)`, `Japan (JPN)`, `Korea (KOR)` |


<span id="e6c69a99"></span>
# Platform configuration

<span id="89b85555"></span>
## Open related services [required]


|product |purpose |necessity |
|---|---|---|
|Virtual Private Cloud |private network |must |
|Subnet |subnet |must |
|Security Group |SecurityGroup |must |
|EIP |Public IP |To configure a dedicated network, you must |
|NAT Gateway |NAT gateway, providing access to the public network<br><br>> You can use the platform provided. |To configure a dedicated network, you must |
|API Gateway |API gateway to provide WebIDE domain access<br><br>> If you don't use inference services, you can use the platform's public |To configure a dedicated network, you must<br><br>Inference service, required |
|Container Registry |mirror vault<br><br>> If you don't need a custom mirror, you can leave it unconfigured. |Custom mirror storage and build, required |
|PFS |Parallel File System |on demand |
|TLS（Torch Log Service） |log service |must |
|VMP（Vital Managed Service for Prometheus） |monitoring service |must |


<span id="c35b0d09"></span>
### Network Configuration

<span id="8e2b6362"></span>
#### **Virtual Private Cloud (Required)** 


* Open the [VPC console ](https://console.byteplus.com/vpc/region:vpc+ap-southeast-1/vpc/create)and create a VPC

   * **Geography \- Availability Zones** are the same as Hashrate Resources

   * Network segment planning on demand to avoid network segment conflicts in scenarios such as dedicated line/CEN

   * Please increase the number of available IPs in the network segment as needed (not less than the number of GPU cards is recommended), CIDR < 20


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c5d26297c67640849cb9ed290ee42e7a~tplv-goo7wpa0wc-image.image" width="2688px" /></div>


<span id="53c951dd"></span>
#### **Subnet (required)** 


* Open the [subnet console ](https://console.byteplus.com/vpc/region:vpc+ap-southeast-1/subnet/create)and create a subnet

   * Subnet Availability Zones need to be aligned with Resource Availability Zones

   * Please increase the number of IPs in the subnet segment on demand, CIDR ≤ 20 or the number of available IPs ≥ 4093


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d2b59381828c41259024634304df1ef8~tplv-goo7wpa0wc-image.image" width="2658px" /></div>


<span id="8ab06c67"></span>
#### Security Group  **(required)** 


* Open the [SecurityGroup console ](https://console.byteplus.com/vpc/region:vpc+ap-southeast-1/securityGroup/create), under the aforementioned private network, for the default SecurityGroup "Configuration Rule" or "Create SecurityGroup", the following connectivity needs to be guaranteed



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


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0db0aa68b4af49d48b507e5cf26894f3~tplv-goo7wpa0wc-image.image" width="2828px" /></div>


<span id="15d0c2a7"></span>
#### E**IP (on demand, if you need to protect the public network access experience, use the exclusive public network, do not use the platform to share the network, you need to access the public network and public network login, rely on)** 


* Open the [public IP console ](https://console.byteplus.com/eip/region:eip+ap-southeast-1/eips/create), [Apply for public IP], the **region\-availability area** is the same as the computing power resource, and the line specification is on demand


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cdaf7ae0d89f4215a0aff69460061f74~tplv-goo7wpa0wc-image.image" width="2644px" /></div>


<span id="bf98657e"></span>
#### NAT Gateway  **(on demand, if you need to protect the public network access experience, use the exclusive public network, do not use the platform to share the network, you need to** [use the SNAT function to access the public network ](https://docs.byteplus.com/en/docs/natgateway/Accessing-the-internet-using-SNAT)**and public network login dependence).** 


* Open the [public network NAT gateway console ](https://console.byteplus.com/nat/region:nat+ap-southeast-1/nats/create), [Create a public network NAT gateway], the **region\-availability area** is the same as the computing power resource, select the private network and subnet multiplexed/created above

   * It is the public network NAT gateway [Configure the public network IP]

   * [Configure SNAT rules] \- [Create SNAT rules] for the public network NAT gateway

   * Open the [routing table console ](https://console.byteplus.com/vpc/region:vpc+ap-southeast-1/routeTable), add a route entry, and add the public NAT gateway to the routing table (the first public NAT gateway under the private network will be automatically added to the routing table).


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5bd6cc21f94346928a1437859a3473a1~tplv-goo7wpa0wc-image.image" width="2570px" /></div>


<span id="1cbdf7e8"></span>
#### **API Gateway (on demand, if you need to protect the public network access experience, use the exclusive public network, and do not use the platform to share the network)**  , select the public network for the network type, and other configurations are on demand


* Open the [API Gateway console ](https://console.byteplus.com/veapig/region:veapig+ap-southeast-1/gateway)and click Create Instance

   * The gateway type is: standard gateway

   * The private network and subnet are the VPC created above.

   * Check **Public Network** Type


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0317c2b679de4cd6957865c98e4a8063~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/207145fbb15a429db76efe34c7d6a17c~tplv-goo7wpa0wc-image.image) </span>

<span id="078c6c3e"></span>
### Container Registry CR [On demand, if you need to customize the mirror, you can choose to open it]


* Open the[ Container Registry console](https://console.byteplus.com/cr/region:cr+ap-southeast-1/instances?) and follow the prompts to open the BytePlus mirror vault service

   * Create a **standard version** instance, the **region** and computing power resources are the same, wait for the instance status to change to [running] (may take 5~ 10 minutes)

   * Go to Instance \- Namespace \- Create a namespace, create a namespace for Dev boxes mirror archive

   * Go to Instance \- Identity and Access Management \- Add VPC, select Multiplex/Create, Private Network


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6fc3a396067542f7860b0ef8e6ba4d35~tplv-goo7wpa0wc-image.image" width="1626px" /></div>


<span id="ef0dadb9"></span>
### Storage Resources

<span id="ffb0d6ee"></span>
#### **Torch Object Storage TOS [Required]** 


* Open the [Torch Object Storage console ](https://console.byteplus.com/tos)and follow the prompts to open the BytePlus Torch Object Storage service


<span id="9ea0f3bd"></span>
#### Parallel **File Storage PFS [Optional]** 

Open the [parallel File Storage PFS console ](https://console.byteplus.com/pfs/region:pfs+ap-southeast-1/create?), instance list \- create file system (may take 10~ 20 minutes) and mount the instance


* **Geography \- Availability Zones** are the same as Hashrate Resources

* Private Networks and Subnets, select Private Networks and Subnets for Multiuse/Create, as described above


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0ed9d55398a448ebb2ad1c21c48be4ba~tplv-goo7wpa0wc-image.image" width="2558px" /></div>



* [On\-demand] Create Fileset, Fileset can better manage storage data permissions


<span id="3412eb9e"></span>
#### File Storage FileNAS [Optional]


* Open the File Storage FileNAS console and create a NAS instance

   * The VPC of the instance uses the VPC created above.

   * After the creation is completed, you need to create a mount point before you can use it.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/25639b8322d346fe941ee34df6ed18c2~tplv-goo7wpa0wc-image.image" width="2444px" /></div>


<span id="e760cf41"></span>
### Create sub account (optional)


* Log in to [IAM ](https://console.byteplus.com/iam/create_user/name)with your registered BytePlus main account, create a sub account and configure permissions. If it is not a BytePlus main account, MLPlatformAdmin permission is required to add sub accounts.

* It is recommended to grant the following permissions on demand:

   * BillingCenterFullAccess: all read and write permissions of expense center, required for resource group order placement, optional

   * MLPlatformMemberAccess: MLP Developer Permissions \- Required

   * AccessKeyFullAccess: User's own key management permissions \- required when using command\-line tools, tos, etc

   * CRFullAccess: Permissions to use BytePlus mirror vault

   * TOSFullAccess: Permissions to use BytePlus Torch Object Storage

   * vePFSFullAccess: Permissions to use BytePlusvePFS

   * APIGFullAccess: Permissions to use the BytePlusAPI gateway

   * VPCFullAccess: Use BytePlusVPC full read\-write strategy

   * CFSFullAccess: Permissions to use the BytePlus Cloud File System

   * TLSFullAccess: Full administrative privileges to use the BytePlus logging service

   * VmpFullAccess: Full administrative access to the BytePlus monitoring service


More Preset Permissions Reference: [Preset Policy](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-policies)

<span id="51515292"></span>
## Go to MLP to complete the global configuration [Required]

<span id="4946d7d6"></span>
#### Video crash version

<div style="text-align: center">
<img src="data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIiB2aWV3Qm94PSIwLDAsMjAlLDEwMCUiIHZlcnNpb249IjEuMSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB4bWxuczp4bGluaz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94bGluayI+CiAgPGRlZnM+CiAgICA8bGluZWFyR3JhZGllbnQgaWQ9ImciPgogICAgICA8c3RvcCBzdG9wLWNvbG9yPSIjRjJGM0Y1IiBvZmZzZXQ9IjI1JSIgLz4KICAgICAgPHN0b3Agc3RvcC1jb2xvcj0iI0U1RTZFQiIgb2Zmc2V0PSIzNyUiIC8+CiAgICAgIDxzdG9wIHN0b3AtY29sb3I9IiNGMkYzRjUiIG9mZnNldD0iNjMlIiAvPgogICAgPC9saW5lYXJHcmFkaWVudD4KICA8L2RlZnM+CiAgPHJlY3QgaWQ9InIiIHdpZHRoPSI0MDAlIiBoZWlnaHQ9IjEwMCUiIGZpbGw9InVybCgjZykiIC8+CiAgPGFuaW1hdGUgeGxpbms6aHJlZj0iI3IiIGF0dHJpYnV0ZU5hbWU9IngiIGZyb209Ii0zMDAlIiB0bz0iMCUiIGR1cj0iMS41cyIgcmVwZWF0Q291bnQ9ImluZGVmaW5pdGUiICAvPgo8L3N2Zz4=" width="2030px" /></div>


Log in with the registered BytePlus sub account, open the [MLP console - global configuration ](https://console.byteplus.com/ml-platform/region:ml-platform+ap-southeast-1/globalConfig), and enter the pop\-up cross\-service authorization page for the first time to complete the cross\-service authorization of dependent services such as Torch Object Storage and mirror vault.

<span id="02fa2da9"></span>
#### Private network VPC


* In order to connect the private network environment, mount PFS, NAS and other file systems between users and platforms, private network configuration is required. According to the availability area where the CPU/GPU computing power resources and PFS resources are located, configure the subnet of the same availability area. Supports associating multiple subnets directly with the default SecurityGroup.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After binding the VPC, you can choose two types of public network, exclusive network and shared network.</div>



1. <div data-tips="true" data-tips-type="tip">The exclusive network needs to bind the NAT gateway, EIP and API gateway purchased by yourself to get a better public network experience. It is recommended to use it in the production environment.</div>


2. <div data-tips="true" data-tips-type="tip">The shared network shares bandwidth for all tenants of the platform. At present, the public network can be used for free, and the testing environment can be used. The formal generation environment is not recommended.</div>



<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/51d979ca036d42768a3521c93e7f0b5f~tplv-goo7wpa0wc-image.image" width="2530px" /></div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a72e3082b0cd4e32af396cd26159ed70~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d317f91989f4df1bf2c1127e9b7c245~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After completing all the above configuration, please contact the BytePlus Machine Learning Platform Product Solution POC to <strong>verify the configuration in the background</strong> for you. In the meantime, please continue with the subsequent configuration.</div>


<span id="74eb0b9d"></span>
#### Container Registry CR


* If you use the Container Registry Standard Edition instance, you need to perform a global configuration in the Machine Learning Platform, complete the authorization of the Standard Edition instance, and specify the mirror archive location.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2219560e6664469e82f4b5af5728a759~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ee835929061e4da0b7ec1b21d9682a28~tplv-goo7wpa0wc-image.image) </span>

<span id="e35fa2a5"></span>
#### Parallel File Storage PFS


* If you use File storage PFS, you need to do global configuration in the Machine Learning Platform, **complete a) bind instance b) add mount permission**

   * **Binding instances** : Binding PFS instances directly through the Machine Learning Platform, expect to wait 10\-20 minutes to complete the binding.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e9991e615e554fc792b15fca195d55ca~tplv-goo7wpa0wc-image.image" width="2198px" /></div>



* **Add mount permission** : support setting by triplet of authorized directory × permission (read/write/read only/none) × user, the authorized subdirectory needs to be set in the vepfs console fileset


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ce447359df794a918b98778b31bcc9ff~tplv-goo7wpa0wc-image.image" width="1986px" /></div>


> Using the vepfs + Machine Learning Platform solution, when deleting PFS in the scenario where the voucher expires/vepfs does not renew, you need to unbind the vepfs instance in Machine Learning Platform \- global configuration \-vepfs first.

> If you have two PFS instances mounted on the Machine Learning Platform, please note the following:

> 1. When mounting a PFS via the CLI (command line) and SDK, you need to specify a PFS instance ID, otherwise you cannot commit the load task of mounting a PFS instance.

> 2. Using PFS to store TensorBoard logs similarly requires specifying the instance ID.


<span id="12fb1c0d"></span>
#### Torch Log Service TLS


* Add TLS authorization, support for selecting Dev boxes, custom tasks, and inference services

   * The log data will be pushed to the TLS platform, and users can use the TLS API to obtain the data; the MLP platform will also embed some log modules, allowing users to query real\-time logs


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cf3a81d8600746d78d498ad85ba3e28c~tplv-goo7wpa0wc-image.image" width="2074px" /></div>


<span id="4883a9e9"></span>
#### Monitor VMP


* Add VMP authorization, support for selecting Dev boxes, custom tasks and inference services

   * The monitoring data will be pushed to the VMP platform, and users can use the VMP API to obtain data; the MLP platform will also embed some monitoring boards, allowing users to query indicators such as utilization and usage


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2a47b595a3014b3cbac42b48d541b624~tplv-goo7wpa0wc-image.image" width="2078px" /></div>


<span id="8d2c9277"></span>
# resource opening

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After all the above configuration is completed and verified, the Machine Learning Platform product solution POC will expand the compute node resources for you and add resource groups to place orders for Quota. Depending on the size of the computing power, the time required varies. Please wait patiently for the notification before proceeding with the follow\-up operation.</div>


<span id="5e981438"></span>
## Create a resource group

Main account Log in to the Machine Learning Platform, select [Resource Group Management] \- [Resource Group] in the left navigation, and you can create a new resource group. If it is not the main account, additional billFullAccess privileges are required to create a resource group.

(1) First select the computing configuration, for example, in Johor Availability Zone B, choose 128 H20 monthly prepaid high\-performance computing GPUs, 100GiB SSD cloud disks, and the configuration is as follows:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/91ffe6c2682443539096633416e79d86~tplv-goo7wpa0wc-image.image" width="2890px" /></div>


(2) Secondly, carry out storage & network configuration, and directly select the private network and storage configuration that have been bound in the global configuration. If not, you need to jump to the global configuration to complete the pre\-configuration operation first. It can diagnose network connectivity, verify VPC, APIG, mirror and other network configurations to ensure network access.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3a49e7f2c01b4346849db8e236e720ba~tplv-goo7wpa0wc-image.image" width="2810px" /></div>


(3) Finally confirm the configuration information and submit the order. You can confirm the configuration information, select the purchase time, whether to turn on automatic renewal, and submit the order after confirming that the product agreement is correct.

<span id="5fcbc251"></span>
## Create queue

The main account can further split the resource group resources into queues according to business needs and project requirements. You can create a queue in the operation of the resource group on the [Resource Group] list page, or you can create a new queue in the [Queue] in the left navigation.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d1fd3076a3bf4c32ba2f8a20a31cfdad~tplv-goo7wpa0wc-image.image) </span>

> Tips: Please note that when algorithm engineers use Dev boxes, custom tasks, and inference services to select [instance specifications], there are two specifications for high\-performance GPUs such as A100/A800:

> High\-performance computing GPU type: e.g. A100, ml.hpcpni2.28xlarge, supports RDMA network communication, high performance. Usually, choose this specification for multi\-instance calculation of the whole machine.

> GPU type: such as A100, ml.pni2.28xlarge, supports TCP network communication, ordinary performance, usually single card stand\-alone machine Select this specification
