---
title: "Limits"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Limits"
---

This topic describes the default quota limits for ECS\-related resources.

<span id=".5a6e5L6L"></span>
## Instance


|Limit item |Upper limit |Changeable |
|---|---|---|
|Max. ECS instances that can be created at one time |100 |No |
|Max. vCPUs or GPUs available for an instance type family configured with a specified billing method within a single availability zone for each account<br><br>> For information about quota items associated with instance type families, see [Description of ECS instance type quota items](https://docs.byteplus.com/en/docs/ecs/ECS-resource-quota-management#.ZWNz6KeE5qC86YWN6aKd6aG56K-05piO). |Please go to the  [Quota center](https://console.byteplus.com/quota/productList/ParameterList?ProviderCode=ecs) to view. |Yes. To increase the vCPU quota, please apply at the [Quota Center](https://console.byteplus.com/quota/productList/ParameterList?ProviderCode=ecs). |
|Does an ECS instance with a local volume support custom mounting of a new volume? |No. Local volumes are created and destroyed along with the ECS instance. |\- |


<span id=".6aKE55WZ5a6e5L6L5Yi4"></span>
## RI


|Limit item |Upper limit |Changeable |
|---|---|---|
|Max. vCPUs available for all regional RIs held by an account in a region |200 |Yes, the product is currently in Beta. If you need to increase the vCPU quota, please contact your account manager to apply. |
|Max. vCPUs available for all Zonal RIs held by an account in an availability zone |200 |Yes. To increase the vCPU quota, please apply at the [Quota Center](https://console.byteplus.com/quota/productList/ParameterList?ProviderCode=ecs). |
|Instance types supported by Reserved Instances (RI) |Refer to [Purchase Reserved Instances (RI)](https://docs.byteplus.com/en/docs/ecs/Buying-Reserved-instances#.5rOo5oSP5LqL6aG5). |\- |
|Reserved Instances (RI) that do not support changing instance type |Refer to [Changing Reserved Instances](https://docs.byteplus.com/en/docs/ecs/Change-Reserved-instances#.5rOo5oSP5LqL6aG5), and this type only supports purchasing Zonal RI. |\- |


<span id=".5by55oCn6aKE57qm5a6e5L6L"></span>
## Elastic Scheduled Instances


|Limit item |Upper limit |Changeable |
|---|---|---|
|Instance types available for reservation |Please refer to [Elastic Scheduled Instances (ESI) overview](https://docs.byteplus.com/en/docs/ecs/Elastic_Scheduled_Instances_Overview#.5L2_55So6ZmQ5Yi2). |\- |
|Max. vCPUs an account can use in an availability zone |300 |Yes. To increase the vCPU quota, please apply at the [Quota Center](https://console.byteplus.com/quota/ProductList/inParameterList?ProviderCode=ecs). |
|The maximum number of instances that can be reserved and purchased at one time |500 |\- |


<span id=".6ZWc5YOP"></span>
## Image


|Limit item |Description of Limit |Changeable |
|---|---|---|
|Maximum size of an image file that can be imported |2 TiB |No |
|Image format |QCOW2, RAW, VHD, VMDK |No |
|Maximum number of BytePlus accounts that a single custom image can be shared with |50 |No |
|Number of custom images that a single account can create in a single region |50 |Yes. If you want to increase your custom image quota, go to [Quota Center](https://console.byteplus.com/quota/productList/ParameterList?ProviderCode=ecs) and submit a quota increase application. |


<span id=".5LqR55uY"></span>
## Volume


|Limit item |Upper limit |Changeable |
|---|---|---|
|Max. volumes that can be attached per ECS instance |The number of volumes that can be attached to instances of different instance types varies. For more information, refer to [Instance types](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types).<br><br>> If you have created an ECS instance by using a CentOS 6.x image, a maximum of 8 volumes can be attached (including 1 system volume). |No |
|Capacity of a single system volume |* PTSSD: 40 GiB to 500 GiB<br><br>* ESSD: 40 GiB to 2,048 GiB |No |
|Capacity of a single data volume |* PTSSD: 20 GiB to 8,192 GiB<br><br>* ESSD: 20 GiB to 32,768 GiB |No |
|Maximum usage per volume type |* ESSD PL0: Maximum usage of 64TiB for each root user in a region.<br><br>* ESSD FlexPL: Maximum usage of 10TiB for each root user in a region. |Yes. To increase the quota for volume capacity, please apply at the [Quota Center](https://console.byteplus.com/quota/productList/ParameterList?ProviderCode=EBS). |


<span id=".5b-r54Wn"></span>
## Snapshot


|Limit item |Upper limit |Changeable |
|---|---|---|
|Maximum number of manual snapshots that can be created per volume |Up to 256 manual snapshots can be created for each volume. |No |
|Max. automatic snapshots that can be created per volume |Up to 1024 automatic snapshots can be created for each volume. |No |


<span id=".572R5Y2h"></span>
## Network interface


|Limit item |Upper limit |Changeable |
|---|---|---|
|Max. primary ENIs that can be attached per ECS instance |1 |No |
|Max. ENIs (primary and secondary) that can be attached per instance |The number of network interfaces that can be mounted to an ECS instance varies based on the instance type. For more information, see [Instance type overview](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types). |No |
|Number of private IP addresses and EIPs for a single network interface |* Primary private IP addresses: 1<br><br>* Secondary private IP addresses:<br><br>   * Up to 9 secondary private IP addresses are supported for an ENI that is not attached to an ECS instance.<br><br>   * The number of secondary private IP addresses that can be attached to an ENI depends on the instance types. For more information, refer to [Instance types](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types).<br><br>* EIP: The number of EIPs depends on the number of private IP addresses (primary and secondary) on the ENI. Each private IP address can be attached to an EIP. |No |


<span id=".5a6J5YWo57uE"></span>
## Security group


|Limit item |Upper limit |Changeable |
|---|---|---|
|The maximum number for an ECS instance |Each ENI can be associated with up to 5 security groups. |No |


<span id=".5a-G6ZKl5a-5"></span>
## Key pair


|Limit item |Upper limit |Changeable |
|---|---|---|
|Operating systems |Only the Linux operating system is supported. |\- |
|Max. key pairs for an account in a region |500 |No |
|The maximum number for an ECS instance |Only one key pair can be associated on the console.<br><br>If you need multiple key pairs, manually modify the `~/.ssh/authorized_keys` file inside the instance to add multiple key pairs. |\- |


<span id=".6YOo572y6ZuG"></span>
## Deployment set


|Limit item |Description of Limit |Changeable |
|---|---|---|
|Maximum number of instances in a single deployment set |The number of instances that can be created within a deployment set varies based on the deployment policy:<br><br><br>* Availability<br><br>   * Limit for an availability zone: 5 instances.<br><br>   * Limit for a region: 5 instances \* Number of availability zones in the region.<br><br>* Availability Group policy:<br><br>   * Limit for an availability zone: A deployment set can be divided into a maximum of 7 groups, with the total number of instances created in these 7 groups not exceeding 60.<br><br>   * Limit for a region: 60 instances x Number of availability zones in the region. |Yes. If you need to change the quota, please contact your account manager. |
|Types of instances that can be created within the deployment set |You can call the [DescribeDeploymentSetSupportedInstanceTypeFamily](https://docs.byteplus.com/en/docs/ecs/DescribeDeploymentSetSupportedInstanceTypeFamily) operation to query the instance type families that support deployment set. |\- |


<span id=".5YWs572RSVA="></span>
## EIP


|Limit item |Description of Limit |Changeable |
|---|---|---|
|Max. EIPs that can be applied for an account in a region |20 |Yes. To increase the EIP quota, please apply at the[ Quota Center](https://console.byteplus.com/quota/productList/ParameterList?ProviderCode=EIP). |
|ISPs |BGP (Multi\-ISP) |\- |
|Bandwidth upper limit |Apply for an EIP:<br><br><br>* Pay\-as\-you\-go (pay\-by\-bandwidth): 500 Mbps<br><br>* Pay\-as\-you\-go (pay\-by\-data\-transfer): 200 Mbps<br><br>* Subscription: 500 Mbps<br><br><br>Modify an EIP:<br><br><br>* Pay\-as\-you\-go (pay\-by\-bandwidth): 1,000 Mbps<br><br>* Pay\-as\-you\-go (pay\-by\-data\-transfer): 200 Mbps<br><br>* Subscription: 1,000 Mbps |No |
|Number of EIPs that can be associated |The number of EIPs that can be associated with an instance depends on the number of attachable ENIs and the number of private IP addresses (primary and secondary) on the ENIs. |No |
|Number of EIPs that can be added to a single bandwidth package |100 |Yes. If you need to increase the quota of EIPs that can be added to a Shared Bandwidth Package, please apply at the [Quota Center](https://console.byteplus.com/quota/productList/ParameterList?ProviderCode=EIP). |


<span id=".5qCH562-"></span>
## Tag


|Limit item |Upper limit |Changeable |
|---|---|---|
|The maximum number for an ECS instance |50 |No |
