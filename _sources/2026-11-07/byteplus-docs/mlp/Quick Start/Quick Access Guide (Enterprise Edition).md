---
title: "Quick Access Guide (Enterprise Edition)"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Quick_Access_Guide_Enterprise_Edition"
---

BytePlus Machine Learning Platform is a platform for professional algorithm engineers to integrate cloud\-native tools + computing power (GPU, CPU Cloud as a Service) for one\-stop AI algorithm development and iteration. Here's how to access the Machine Learning Platform from scratch.

> MLP has a pre\-built training framework mirror, which supports one\-click submission of distributed training tasks, which can significantly reduce the project cycle from the POC to the formal production development environment. The first access requires data transfer, permission configuration, product function/performance POC and other tasks, and the cycle of AI development from POC to production environment is compressed to 1 to 2 weeks. Once again, resource capacity expansion and reduction, resource transfer only needs to be more allocated, and the hour level can be switched.


<span id="7a32e8f3"></span>
# 0. Preconfiguration

<span id="785d254a"></span>
## Register Account and Activate Service

Complete BytePlus account registration and enterprise certification, detailed guidance in the [document](https://arcosite.bytedance.net/sites/1689750851223/67dd0d78549d85051ff6a312/editor/67e2926dbafc26050d8f9fe0?docLang=en&bv=67dd0d7a549d85051ff6a324).


> * Please [log in to main account ](https://signin.byteplus.com/saml/sso)or have an [AdministratorAccess ](https://console.byteplus.com/iam/policymanage)sub account

> * Recommended storage, network resources, and Machine Learning Platform compute instances are kept in the same **region\-availability zone** for the best performance experience. Specifically, you can *communicate with the Machine Learning Platform product solution POC to confirm* . This document takes *Availability Zone B* as an example.


<span id="a20b8df6"></span>
## Activate related services

Activate associated services, including network, storage, Container Registry, and other resources, as detailed in [Register an account and open a service](https://docs.byteplus.com/docs/mlp/Register_an_account_and_open_a_service).

<span id="e3f83e03"></span>
## network configuration

<span id="cc5e2419"></span>
### **Private network VPC**

Open the [VPC console](https://console.byteplus.com/vpc/region:vpc+ap-southeast-1), Create/Multiuse, Private Network and Subnet.


* **Geography \- Availability Zones** are the same as Hashrate resources.

* Network segment planning on demand to avoid network segment conflicts in scenarios such as dedicated line/CEN.

* Please increase the number of available IPs in the subnet segment as needed (not less than the number of GPU cards is recommended), for example, CIDR = 20 Available IPs = 4093 or more.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b7e58e7ec8bb457f864d9d11199adc88~tplv-goo7wpa0wc-image.image) </span>

<span id="bc818fdc"></span>
### **SecurityGroup**

Open the [Private Network Console - SecurityGroup](https://console.byteplus.com/vpc/region:vpc+ap-southeast-1/securityGroup), under the aforementioned private network, the following connectivity needs to be guaranteed for the default SecurityGroup "Configuration Rule" or "Create SecurityGroup".


|access rules |strategy |protocol type |port range |Destination address |Description |
|---|---|---|---|---|---|
|out direction |allow |on demand |on demand |on demand |Select the traffic that needs to be released on demand |
|Incoming direction |allow | |2222 | |Dev boxes SSH login |
||| |10000 | |Dev boxes/custom tasks WebIDE |
||| |12222 | |Custom training framework communication |
||| |3389 | |RDP Remote Desktop |
||| |80 | |HTTP default port |
|||TCP |80 |apig\-sg\-xx |Limit network segment access or allow only API gateway access |
||| |443 | |HTTPS default port |
||| |5082 | |On\-demand, CloudFS dependencies |
||| |5092 | |On\-demand, CloudFS dependencies |
||| |ALL |SecurityGroup |interoperability |


<span id="486a7c7e"></span>
### Public IP (on demand)

> Guarantee the public network access experience, do not use the platform to share the network, and use the exclusive public network. Access to public networks and public login dependencies.


Open the [Private Network Console - Public IP ](https://console.byteplus.com/eip/region:eip+ap-southeast-1/eips), [Apply for Public IP], the **Region \- Availability Area** is the same as the computing power resources, and the line specifications are configured on demand.

<span id="49f08844"></span>
### Public NAT gateway (on demand)

> If you need to protect the public network access experience, use the exclusive public network, and do not use the platform to share the network, you need to [use the SNAT function to access the public network ](https://docs.byteplus.com/en/docs/natgateway/Accessing-the-internet-using-SNAT)and the public network login dependence.


1. Open the [Private Network Console - Public Network NAT gateway ](https://console.byteplus.com/nat/region:nat+ap-southeast-1/nats), [Create Public Network NAT gateway], the **Region \- Availability Area** is the same as the computing power resource, select the aforementioned Multiuse/Create Private Network and Subnet

2. Configure the public network IP for the public network NAT gateway.

3. [Configure SNAT Rules] \- [Create SNAT Rules] for the public network NAT gateway.

4. Open [Private Network Console - Routing Table ](https://console.byteplus.com/vpc/region:vpc+ap-southeast-1/routeTable), Add Route Entry, Add Public NAT gateway to routing table (the first public NAT gateway under private network will be automatically added to routing table)


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6f9e91dedfc642bc96b82d9dc67bb6e7~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/85e61f4c5e0a4216afca1f482f9ba5a2~tplv-goo7wpa0wc-image.image) </span>

<span id="5053d50c"></span>
### API gateway (on demand)

> If you need to ensure the public network access experience, you need to use the exclusive public network and not use the platform sharing network.


Access the [API gateway](https://console.byteplus.com/veapig/region:veapig+ap-southeast-1/gateway), select the public network for the network type, and select other configurations on demand.

<span id="8f85fc13"></span>
## Container Registry Configuration

Open the [Container Registry console ](https://console.byteplus.com/cr/region:cr+cn-beijing/instances?)and follow the prompts to activate BytePlus Container Registry service.


1. Create **Standard Edition** instance, the **region** and computing power resources are the same, wait for the instance status to change to [running] (may take 5~ 10 minutes).

2. Go to Instance\-Namespace\-Create namespace, Create a namespace for Dev boxes mirror archive.

3. Go to Instance \- Identity and Access Management \- Add VPC and select Multiplex/Create Private Network as described above.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/836c063969524e3e93668b9d9e658b16~tplv-goo7wpa0wc-image.image) </span>

Log in to the Machine Learning Platform with the registered BytePlus main accoun\*\*t [Machine Learning Platform with the registered BytePlus main account](https://console.byteplus.com/ml-platform), and the cross\-service authorization page will automatically pop up when entering the platform. After submitting the form, you can complete the cross\-service authorization of dependent services such as Torch Object Storage and Container Registry.

At this point, all the required services have been Activated. Next step, the main account will create the corresponding sub\-user account for the ordinary developer (optional).

<span id="5cd9815e"></span>
## Torch Log service configuration

Go to the [Torch Log Service](https://console.byteplus.com/tls/region:tls+ap-southeast-1/v2/?projectName=default) console and follow the on\-screen instructions to activate BytePlus Log Service.


1. Create a **log project**.

2. After the project is created successfully, go to the project and create a **log topic**. You can customize the log retention period and other configuration items as needed.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7caba68ae45e4c139ab292b133ad2ae0~tplv-goo7wpa0wc-image.image) </span>

<span id="19272246"></span>
## Monitoring configuration

Go to the [VMP](https://console.byteplus.com/prometheus/region:prometheus+cn-guangzhou/workspace?pageNumber=1) console and follow the on\-screen instructions to activate the BytePlus Managed Prometheus service. After the service is activated, create a workspace and select the specifications and storage duration according to your needs.

<span id="1adbbbac"></span>
## Storage Configuration

<span id="6baa3f8a"></span>
### **Torch Object Storage**

Open the [Torch Object Storage console](https://console.byteplus.com/tos) and follow the prompts to activate BytePlus Torch Object Storage service.

<span id="691a32a3"></span>
### **File storage PFS**

Open the [File storage PFS console ](https://console.byteplus.com/pfs/region:pfs+ap-southeast-1/instance?), the instance list \- Create file system (may take 10~ 20 minutes), and the mount service for the instance


1. **Geography \- Availability Zones** are the same as Hashrate resources.

2. Private Networks and Subnets, select Multiplex/Create Private Networks and Subnets as described above.

> PFS supports subpaths through filesets, providing fine grained data permission control.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e2aa778f32046949f4fefd755897246~tplv-goo7wpa0wc-image.image) </span>

<span id="8663519b"></span>
## Create sub account (optional, recommended)

Log in to [Identity and Access Management ](https://console.byteplus.com/iam/identitymanage/user)with the registered BytePlus main account, refer to the [help documentation ](https://docs.byteplus.com/en/docs/mlp/Create_appropriate_sub_accounts)Create sub account and configure permissions. If it is not a BytePlus main account, MLPlatformAdmin permission is required to add sub accounts.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8fda9b97b44741a2bf25c488523f2152~tplv-goo7wpa0wc-image.image) </span>

It is recommended to grant the following permissions on demand:


* BillingCenterFullAccess: all read and write permissions of expense center, required for resource group order placement, optional

* MLPlatformMemberAccess: Machine Learning Platform Developer Permissions \- Required

* AccessKeyFullAccess: User's own key management permissions \- required when using command\-line tools, tos, etc

* CRFullAccess: Permissions to use the BytePlus Container Registry

* TOSFullAccess: Permissions to use BytePlus Torch Object Storage

* vePFSFullAccess: Permissions to use BytePlus PFS

* APIGFullAccess: Permissions to use the BytePlus API gateway

* VPCFullAccess: Use BytePlus VPC full read\-write strategy

* CFSFullAccess: Permissions to use the BytePlus Cloud File System

* TLSFullAccess: Full administrative privileges with BytePlus Torch Log Service

* VmpFullAccess: Full administrative access to the BytePlus monitoring service


More Preset Permissions Reference: [Rights management](https://docs.byteplus.com/docs/mlp/rights_management).

<span id="2fe6a4be"></span>
## Machine learning global configuration

Log in with the registered BytePlus main account, open the [Machine Learning Platform console - global configuration ](https://console.byteplus.com/ml-platform/region:ml-platform+ap-southeast-1/globalConfig), and enter the pop\-up cross\-service authorization page for the first time to complete the cross\-service authorization of dependent services such as Torch Object Storage and Container Registry.

<span id="c0e37f0b"></span>
### VPC

In order to connect the private network environment, file systems such as Mount PFS and NAS between users and platforms, private network configuration is required. According to the availability area where the CPU/GPU computing power resources and PFS resources are located, configure the subnet of the same availability area. Supports associating multiple subnets directly with the default SecurityGroup.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After Associate VPC, you can choose two types of public network, exclusive network and shared network. The exclusive network requires the NAT gateway, EIP, and API gateway purchased by Associate to get a better public network experience. It is recommended to use it in the production environment.</div>


<div data-tips="true" data-tips-type="tip">The shared network shares bandwidth for all tenants of the platform. At present, the public network can be used for free, and the testing environment can be used. The formal generation environment is not recommended.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9078bd9db46747f29c3eb33e36dd56a7~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After completing all the above configuration, please contact the BytePlus Machine Learning Platform Product Solution POC to <strong>verify the configuration in the background</strong> for you. In the meantime, please continue with the subsequent configuration.</div>


<span id="4c13fc9b"></span>
### Container Registry

If you use the Container Registry Standard Edition instance, you need to perform a global configuration in the Machine Learning Platform, complete the authorization of the Standard Edition instance, and specify the mirror archive location.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/92ed8fd140fc479d9020d82878b3cd96~tplv-goo7wpa0wc-image.image) </span>

<span id="QZ5wc3Xe47"></span>
### Log service


1. On the **Global Setting** page of the Machine Learning Platform, find **Log Service (TLS)**  and click **Configure Rule**.

2. You can set log topics for online services, custom tasks, and dev boxes as needed. These logs can be stored in the same topic or in separate topics.

3. After you complete the configuration, click **OK**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ed2c2458d83f43ed98499fcc16e9290b~tplv-goo7wpa0wc-image.image) </span>

<span id="fhpzdMcPn9"></span>
### Monitoring service

Configure the monitoring service as follows:


1. Go to the **Global Settings** page of the Machine Learning Platform and find the **Monitoring \- Hosted Prometheus** section.

2. Click **Add Authorization**.

3. Turn on the **Monitoring Archive** switch. For **Archive Location**, select the workspace that you created.

4. Click **Confirm Add**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb2de3321e3c4e5f896dad67903af03e~tplv-goo7wpa0wc-image.image) </span>

<span id="69868f5d"></span>
### vePFS

File storage PFS requires global configuration in the Machine Learning Platform, Associate instance completion, and Add Mount permissions.


1. Associate instances: Associate PFS instances directly through the Machine Learning Platform, expect to wait 10\-20 minutes to complete Associate.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eac6e855e97c41168da3ef5eee65d474~tplv-goo7wpa0wc-image.image) </span>


2. Add Mount permission: Support setting by triplet of authorization directory × permission (read\-write/read\-only/none) × user. The authorization subdirectory needs to be set in the vepfs console fileset.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/89c1b727ccaa4e74b8460fc92b227d40~tplv-goo7wpa0wc-image.image) </span>

> Using the vepfs + Machine Learning Platform solution, when deleting the PFS in the scenario where the voucher expires/vepfs does not renew, you need to first Disassociate the vepfs instance in Machine Learning Platform \- global configuration \-vepfs.

> If you have two PFS instances mounted on the Machine Learning Platform, please note the following:

> * When mounting PFS via the CLI (command line) and SDK, you need to specify a PFS instance ID, otherwise you will not be able to commit the load task of mounting the PFS instance. For more information, please refer to

> * Using PFS to store TensorBoard logs similarly requires specifying the instance ID.


<span id="77434eed"></span>
# 1. Resource allocation

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After all the above configuration is completed and verified, contact the Machine Learning Platform product solution docking person to expand the compute node resources for you, and add the resource group to place an order for Quota. Depending on the size of the computing power, the time required varies. Please wait patiently for the notification before proceeding with the follow\-up operation.</div>


<span id="a7d99280"></span>
## Activated Quota

When you are notified that the resource activation was successful, you can start AI development by creating a resource through the resource group.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7e38da19f76c4180b8fdd8a4b05abe0b~tplv-goo7wpa0wc-image.image) </span>

<span id="18e90077"></span>
## Create Resource Group

Main account Log in to the Machine Learning Platform, select [Resource Group Management] \- [Resource Group] in the left navigation, and you can create a new resource group. Creating a resource group requires additional billFullAccess privileges if it is not the main account.


1. Select the computing configuration, for example, in the North China Availability Zone B, choose 128 A100 monthly prepaid high\-performance computing GPUs, 100GiB SSD cloud disks, and the configuration is as follows:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/352df96753dc4aeca6090b06204f5cac~tplv-goo7wpa0wc-image.image) </span>


2. Secondly, the storage & network configuration, directly select the global configuration has Associated private network, storage configuration. If not, you need to jump to the global configuration to complete the pre\-configuration operation first. It can diagnose network connectivity, verify VPC, APIG, mirror and other network configurations to ensure network access.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/528291fd0a8f4c158be1274d2c8c6a84~tplv-goo7wpa0wc-image.image) </span>


3. Confirm the configuration information and order. You can confirm the configuration information, select Duration, and whether to turn on Automatic renewal. Confirm order after confirming that the product agreement is correct.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/709208d1bd4e4a6198212f861635e8a9~tplv-goo7wpa0wc-image.image) </span>

<span id="ae817515"></span>
## Create Queue

The main account can further split the resource group resources into queues according to business needs and project requirements. You can [Create Queue] in the operation of the resource group on the [Resource Group] list page, or you can create a new queue in [Queue] in the left navigation.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1358c3ddc4fe4272a93f41cacf7be038~tplv-goo7wpa0wc-image.image) </span>

> When selecting [instance specifications] using Dev boxes, custom tasks, and inference services, please note that there are two specifications for high\-performance GPUs such as A100/A800:

> * High\-performance computing GPU type: e.g. A100, ml.hpcpni2.28xlarge, supports RDMA network communication, high performance. Usually, this specification is selected for multi\-instance calculation of the whole machine.

> * GPU type: such as A100, ml.pni2.28xlarge, support TCP network communication, normal performance, usually single card stand\-alone machine to choose this specification.


<span id="3af70ad2"></span>
# 2. Performance testing

For high\-performance GPUs that support RDMA networks, such as the A100, A800, H100, etc., you can follow the example test tasks.

The following provides typical example training tasks , which can be used to test the training throughput and communication performance of commonly used models.

<span id="33a96517"></span>
## Network: **NCCL Tests**

<span id="b9952163"></span>
### Mission statement

This task tests the performance and correctness of NCCL AllReduce operations based on [nccl-tests ](https://github.com/NVIDIA/nccl-tests).

<span id="275ba295"></span>
### Test method

Through the custom tasks function, you only need to fill in the basic information of the task, environment configuration, resource configuration, and then submit the NCCL Test task.

 **(1) Fill in the basic information**

By default, the task name and authorization visible range are automatically generated, and customers can also customize the modification.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/23766bfc762b46658daf479e3ea43850~tplv-goo7wpa0wc-image.image) </span>

 **(2) Fill in the environment configuration**

In the environment configuration, you can select the Preset mirror, Configure entry commands.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3efec1a2fa6545868b8f74add078d547~tplv-goo7wpa0wc-image.image" width="1702px" /></div>


The platform preset contains all tags of cuda and pytorch mirror. It is recommended to directly select the `pytorch: 2.6.0`in the preset mirror in the mirror entrance.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c784b2799b2e431e980199d53c040a77~tplv-goo7wpa0wc-image.image) </span>

There are two types of NCCL tasks, each of which selects a different entry command:

The first standard_nccl.sh standard incremental bandwidth test, test time is short, can verify the accuracy and bandwidth limit, entrance command:

`/opt/ml-platform/test/network/standard_nccl.sh`

The second high_bw_nccl.sh long\-term high\-bandwidth testing to verify the stability of machine communication:

`/opt/ml-platform/test/network/high_bw_nccl.sh`

 **(3) Fill in the resource allocation**

In the resource configuration, first select the queue that has been created, and then you can choose the MPI framework and the number of instance specifications.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3bed8959320b411b969a3c1277004a12~tplv-goo7wpa0wc-image.image) </span>

The instance specification of custom tasks supports all GPU models and any number of cards. Take 128 H100s as an example, select the MPI framework, select [128] for the number of instances, and select [ml.pni3h.5xlarge] for the instance specification.

<span id="786dd612"></span>
### expected outcome

Taking task type: `high_bw_nccl`as an example, NCCL version 2.13.4 + cuda11.7, the test found that A800 \* 8 has almost no difference in multi\-machine communication compared with A100 \* 8.


|**Node count** |**A100 \* 8** |**A800 \* 8** |
|---|---|---|
|1 |231.64±0.11 |155.90±0.10 |
|2 |97.06±0.86 |97.20±0.27 |
|4 |97.2 |97.21±0.25 |
|8 |97.15 |95.98±1.85 |
|16 |90±3 |94.57±0.51 |


<span id="9c4d6fb5"></span>
### Test Details

The test effect of each card under two A100\-80G:


1. standard_nccl.sh：


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/736cc1d9942f462ea3c27a3029fa75d5~tplv-goo7wpa0wc-image.image" width="1987px" /></div>



2. high_bw_nccl.sh


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2ba045b880214e61a154601c7de19abf~tplv-goo7wpa0wc-image.image" width="2015px" /></div>


<span id="9a3db4a6"></span>
## Model Training: ResNet

<span id="fa966a34"></span>
### Mission statement

Test the DDP distributed training speed of Pytorch's own ResNet model, mainly test the GPU computing performance, and the communication traffic is small.

<span id="5ab41d0a"></span>
### Test method

Through the custom tasks function, you only need to fill in the basic information, environment configuration, and resource configuration of the task to submit the NCCL Test task.

 **(1) Fill in the basic information**

By default, the task name and authorization visible range are automatically generated, and customers can also customize the modification.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/23766bfc762b46658daf479e3ea43850~tplv-goo7wpa0wc-image.image" width="2362px" /></div>


 **(2) Fill in the environment configuration**

In the environment configuration, you can select the Preset mirror, Configure entry commands.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3efec1a2fa6545868b8f74add078d547~tplv-goo7wpa0wc-image.image" width="1702px" /></div>


The platform preset contains all tags of cuda and pytorch mirror. It is recommended to directly select the `pytorch: 2.6.0`in the preset mirror in the mirror entrance.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b6784e3711244c419e987bb5a6a9d3b3~tplv-goo7wpa0wc-image.image) </span>

Entry command: `/opt/ml-platform/test/train/resnet/ddp.sh`

Optional parameters for the entry command:

```Plain
  --num-iters NUM_ITERS
                        number of benchmark iterations (default: 100)
  --batch-size BATCH_SIZE
                        input batch size (default: 32)
  --num-warmup-batches NUM_WARMUP_BATCHES
                        number of warm-up batches that don't count towards benchmark (default: 30)
  --num-batches-per-iter NUM_BATCHES_PER_ITER
                        number of batches per benchmark iteration (default: 10)
  --num-classes NUM_CLASSES
                        number of classes (default: 1000)
```


 **(3) Fill in the resource allocation**

In the resource configuration, first select the queue that has been created, and then you can choose the Pytorch DDP framework, the number of instance specifications.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3bed8959320b411b969a3c1277004a12~tplv-goo7wpa0wc-image.image" width="1468px" /></div>


The instance specification of custom tasks supports all GPU models and any number of cards. Take 128 A800s as an example, select the PytorchDDP framework, select [128] for the number of instances, and select [ml.hpcpni2l.28xlarge] for the instance specification.

<span id="0982c6c2"></span>
### expected outcome

The output is measured by the speed on each card, and testing found that the A800 \* 8 showed little difference in multi\-machine sample throughput compared to the A100 \* 8.


|Node configuration |A100 \* 8（ images/s） |A800 \* 8（ images/s） |
|---|---|---|
|2 |775.9±10.1 |774.7±11.0 |
|4 |778.6±12.7 |771.2±5.4 |
|8 |756.1±10.6 |762.2±4.6 |
|16 |737.3±17.9 |740.4±8.8 |


<span id="aa385314"></span>
### Test Details

The average speed on the 8\-card A100 is around 792 images/s.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e5ccab14a1d244999db238c0ae5a8e83~tplv-goo7wpa0wc-image.image" width="410px" /></div>


<span id="c932b241"></span>
## GPT (Megatron\-DeepSpeed)

<span id="143c7362"></span>
### Mission statement

Using Megatron\-DeepSpeed to train GPT of different sizes with Zero3 turned on, this task requires high computing and communication performance, and is mainly used to test the stability of large model training.

<span id="8261a48e"></span>
### Test method

Through the custom tasks function, you only need to fill in the basic information, environment configuration, and resource configuration of the task to submit the test task.

 **(1) Fill in the basic information**

By default, the task name and authorization visible range are automatically generated, and customers can also customize the modification.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/23766bfc762b46658daf479e3ea43850~tplv-goo7wpa0wc-image.image" width="2362px" /></div>


 **(2) Fill in the environment configuration**

In the environment configuration, you can select the Preset mirror, Configure entry commands.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3efec1a2fa6545868b8f74add078d547~tplv-goo7wpa0wc-image.image" width="1702px" /></div>


Platform preset 2.6.0 pytorch mirror, CUDA and Python versions are not limited, it is recommended to directly select the preset mirror in the mirror entrance `pytorch: 2.6.0`.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4289d44e4dfa4a0a89778eb086ea29ad~tplv-goo7wpa0wc-image.image) </span>

Entry command:

`/opt/ml-platform/test/train/megatron/deepspeed-175b.sh`, or

`/opt/ml-platform/test/train/megatron/deepspeed-13b.sh`

Entry command for custom parameters

```Bash
export MP_SIZE=2
export PP_SIZE=2
export NUM_LAYER=12
export HIDDEN_SIZE=768
export NUM_ATTN_HEAD=12
export SEQ_LEN=1024
/opt/ml-platform/test/train/megatron/deepspeed.sh
```


 **(3) Fill in the resource allocation**

In the resource configuration, first select the queue that has been created, and then you can choose the Pytorch DDP framework, the number of instance specifications.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3bed8959320b411b969a3c1277004a12~tplv-goo7wpa0wc-image.image" width="1468px" /></div>


175B at least A100/A800 6 machines, 13b at least A100/A800 2 cards, or A30 8 cards. Take 128 A800s as an example, select the PytorchDDP framework, select [128] for the number of instances, and [ml.hpcpni2l.28xlarge] for the instance specification.

<span id="c676a6c0"></span>
### expected outcome

This task is a torture testing task, the parameters have not been tuned, and the training speed has no practical reference value. The corresponding machine can maintain a high load and run for a long time.

<span id="d9af397c"></span>
# 3. Resource cleanup (critical)

After use, if the test is over and the resource is no longer used, please unsubscribe the resource in time to avoid unnecessary expenses.

Please note that you de\-authorized each associated cloud product in the Machine Learning Platform global configuration and went to the console of each cloud product to delete the instance.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6954411cc5b941ce8b3fd31d310b94b9~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/996f0d29caa14ba5af0acd9fb0e22221~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0232d4636a194ba28d93e37eec1b52f2~tplv-goo7wpa0wc-image.image) </span>
