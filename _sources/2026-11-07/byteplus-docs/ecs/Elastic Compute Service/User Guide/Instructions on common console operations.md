---
title: "Instructions on common console operations"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Using-the-console"
---

During the use of Elastic Compute Service (ECS), you might have questions about ECS operations, such as buying instances, remote connections, changing operating systems, changing instance types, expanding volumes, using snapshots and images. This topic describes some common operations on ECS instances to help you use ECS in a secure, reliable, flexible, and efficient manner.

<span id=".5L2_55So6aG755-l"></span>
## Usage notes


* For more information on the usage notes and limits on ECS instances, refer to [Usage notes](https://docs.byteplus.com/en/docs/ecs/Usage-notes) and [Constraints](https://docs.byteplus.com/en/docs/ecs/Limits).

* If you need to know more before you purchase an ECS instance, refer to [Quick start](https://docs.byteplus.com/en/docs/ecs/Quick-start).


<span id=".5a6e5L6L"></span>
## Instance 

<span id=".6YCJ5oup5a6e5L6L6K6h6LS55pa55byP"></span>
### Selecting instance billing method


|Metering method |Applicable scenario |Actions guide |
|---|---|---|
|Pay\-as\-you\-go. |A billing method that allows you to use resources first and pay for them afterward. Without paying for a large amount of resources in advance, you can activate and release resources on\-demand at any time. |* For the impact of account arrears on pay\-as\-you\-go instances and related resources, and how to handle it, see [Arrears](https://docs.byteplus.com/en/docs/ecs/Arrears).<br><br>* You can enable Economical Mode for pay\-as\-you\-go instances to save costs while retaining instance data. For more information, refer to [Instruction on Economical Mode](https://docs.byteplus.com/en/docs/ecs/Economical-mode-for-pay-as-you-go-instances) |
|Yearly/monthly subscription |A billing method that requires you to pay first and use later. It helps you save expenses. You can benefit from an annual discount provided by the platform. For long\-term stable businesses, a subscription\-based ECS instance is your first choice. |For information about the impact of subscription\-based instance expiration on the instance and associated resources and how to handle it, please refer to [Instruction on renewal and unsubscription](https://docs.byteplus.com/en/docs/ecs/Renewal-and-unsubscription) |
|Spot Instance |A type of on\-demand instance with performance same as regular pay\-as\-you\-go instances. This billing method offers a certain discount on the basis of the prices of pay\-as\-you\-go instances. This helps you lower the cost of instance usage in certain scenarios. |* [Overview of spot instance ](https://docs.byteplus.com/en/docs/ecs/Spot_instance)<br><br>* [Purchasing spot instances](https://docs.byteplus.com/en/docs/ecs/Buying_spot_instance) |
|RI |A voucher with deduction and reservation capabilities. It can be used to deduct the bills for compute resources (vCPU, GPU, and memory) required by Pay\-as\-you\-go instances (excluding spot instances). You can also use it to reserve resources to ensure a stable supply. |* [Overview of Reserved Instances](https://docs.byteplus.com/en/docs/ecs/Reserved-instances-overview)<br><br>* [Purchasing RI](https://docs.byteplus.com/en/docs/ecs/Buying-Reserved-instances) |
|Elastic Scheduled Instances (ESIs) |Pay\-as\-you\-go instances that support advance reservation. They are applicable for scenarios that require flexibility and ensure stable supply of resources. After you reserve an ESI, the system automatically creates a pay\-as\-you\-go instance within the resource delivery period. |* [ESI overview](https://docs.byteplus.com/en/docs/ecs/Elastic_Scheduled_Instances_Overview)<br><br>* [Purchasing Elastic Scheduled Instances (ESI)](https://docs.byteplus.com/en/docs/ecs/Creating_ESIs) |


<span id=".6L2s5o2i5a6e5L6L6K6h6LS55pa55byP"></span>
### Changing instance billing method


* [Changing billing method from Pay-as-you-go to Subscription](https://docs.byteplus.com/en/docs/ecs/Converting-from-pay-as-you-go-to-subscription)

* [Changing billing method from Subscription to Pay-as-you-go](https://docs.byteplus.com/en/docs/ecs/Converting-from-subscription-to-pay-as-you-go)


<span id=".6LSt5Lmw5a6e5L6L"></span>
### Purchasing instances

<span id=".5aaC5L2V6YCJ5oup5a6e5L6L57G75Z6L"></span>
#### How to choose an instance type

Before you purchase an instance, refer to [ECS instance types](https://docs.byteplus.com/en/docs/ecs/Instance-types) and [Best practices for instance type selection](https://docs.byteplus.com/en/docs/ecs/Instance-type-selection-best-practice) for more information on ECS instance types and use scenarios.

Before you purchase an instance, refer to ECS instance types and Best practices for instance type selection for more information on ECS instance types and use scenarios.

<span id=".6LSt5Lmw5pa55byP5LuL57uN"></span>
#### How to purchase an ECS instance

In any scenario, you can purchase an instance at any time. In addition, you can purchase two or more instances with the same configuration at a time.


|Purchase method |Applicable scenario |
|---|---|
|[Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) |Purchase an instance with custom configurations. This method allows you to select the billing method, image, instance type, storage capacity, network, and security group based on your needs in different scenarios. |
|[Purchase an ECS instance with the same configuration](https://docs.byteplus.com/en/docs/ecs/Buying-ECS-instances-that-use-the-same-configuration) |If you need a new instance with the same configuration as the current instance, you can use this method to quickly create a new instance. |
|[Purchasing an instance based on an instance launch template](https://docs.byteplus.com/en/docs/ecs/Buying-ECS-instances-with-a-launch-template-or-version) |You can create an instance startup template and purchase an instance based on it with one click. This method simplifies the configuration process and reduces the configuration duration. |
|[Purchasing an instance based on a custom image](https://docs.byteplus.com/en/docs/ecs/Buying-ECS-instances-with-custom-images) |If you have preferred operating system, applications, or other configurations, you can create a custom image. When you create an instance, you can use this custom image to improve configuration efficiency. |


<span id=".6YOo572y5a6e5L6L"></span>
### Deploying instance

When purchasing instances, you can make dispersed deployments across different underlying hardware, deploy instances for exclusive access to underlying physical resources, or configure automatic elastic deployment based on business situations.


|Functionality |Applicable scenario |Actions guide |
|---|---|---|
|Deployment Set |A policy to control the distribution of instances across underlying hardware (physical machines/switches/racks) for achieving physical security isolation. This policy is applicable for scenarios with high requirements for underlying disaster recovery and availability. |1. [Creating deployment set](https://docs.byteplus.com/en/docs/ecs/Deployment-set-overview#M9aiS8dq)<br><br>2. [Creating instance in deployment set](https://docs.byteplus.com/en/docs/ecs/Deployment-set-overview#VmkUxq5V) |
|Auto scaling |An on\-demand scalable pool of ECS resources is provided. The number and type of instances within the scaling group are automatically identified and adjusted in real time. |[Procedure for creating a scaling task](https://docs.byteplus.com/en/docs/as/Building-a-scaling-task-process) |


<span id=".6L-B56e75a6e5L6L"></span>
### Migrating instance


|Functionality |Applicable scenario |Actions guide |
|---|---|---|
|Server Migration Center (SMC) |With SMC, you can migrate your own local servers, virtual machines, cloud hosts on other cloud platforms, or other types of servers to BytePlus. This helps you address issues like limited existing resources and low scalability. |1. [Importing migration source](https://docs.byteplus.com/en/docs/smc/Step-1-Import-Migration-Sources)<br><br>2. [Creating and starting migration job](https://docs.byteplus.com/en/docs/smc/Server-Migration-Task) |


<span id=".566h55CG5a6e5L6L"></span>
### Managing instance


|Applicable scenario |Actions guide |
|---|---|
|To manage the lifecycle of an instance |* [Logging in to instance](https://docs.byteplus.com/en/docs/ecs/Overview-1)<br><br>* [Starting instance](https://docs.byteplus.com/en/docs/ecs/Starting-instances)<br><br>* [Stop instance](https://docs.byteplus.com/en/docs/ecs/Stopping-instances)<br><br>* [Restarting instance](https://docs.byteplus.com/en/docs/ecs/Restarting-instances)<br><br>* [Instance deletion protection](https://docs.byteplus.com/docs/ecs/Instance_delete_protection)<br><br>* [Delete instance](https://docs.byteplus.com/en/docs/ecs/Deleting-ECS-instances) |
|When you require fine\-grained control and management of instances |* [Setting custom data of instance](https://docs.byteplus.com/en/docs/ecs/Configuring-custom-data): Use custom data when you create an instance or modify the custom data of an existing instance. This allows the instance to automatically obtain software packages, install web servers, or pass in data at the initial startup.<br><br>* [Viewing instance metadata](https://docs.byteplus.com/en/docs/ecs/Viewing-instance-metadata): The metadata refers to the basic information of an ECS instance on the cloud platform, such as hostname, instance ID, IP address, network information, etc. You can access the metadata from the instance and perform system configuration to initialize information. |
|The login passwords or key of an instance are forgotten or lost |* [Resetting passwords](https://docs.byteplus.com/en/docs/ecs/Resetting-passwords)<br><br>* [Creating key pair](https://docs.byteplus.com/en/docs/ecs/Creating-key-pairs) and [associating key pair with ECS instance](https://docs.byteplus.com/en/docs/ecs/Binding-key-pairs-to-instances) |
|The current instance type or network configuration can not meet business needs. |[Changing instance type](https://docs.byteplus.com/en/docs/ecs/Modifying-instance-types) |
|The current operating system cannot meet your requirements |[Changing operating system](https://docs.byteplus.com/en/docs/ecs/Changing-OS) |


<span id=".6Ieq5a6a5LmJ6ZWc5YOP"></span>
## Custom image

BytePlus provides you with a wide variety of [public images](https://docs.byteplus.com/en/docs/ecs/Public-image-overview) with legitimate copyrights, ensuring high security and stability. However, if you need to redeploy a complex initialization system or deploy multiple servers with the same configuration, we recommend that you use a custom image. You can create a private image based on an instance or snapshot, or upload an image from the local volume. In addition to the operating system, an image allows you to pre\-install public applications or private applications for higher customization.


|Applicable scenarios |Actions guide |
|---|---|
|Creating custom image |* [Creating custom image based on instance (for Linux)](https://docs.byteplus.com/en/docs/ecs/Creating-custom-images-from-a-Linux-instance)<br><br>* [Creating custom image based on instance (for Windows)](https://docs.byteplus.com/en/docs/ecs/Creating-custom-images-from-a-Windows-instance) |
|Importing custom image |[Importing custom image](https://docs.byteplus.com/en/docs/ecs/Importing-custom-images-1): After you import an image, you can use it to create an instance. |
|To check the validity of a custom image |[Image detection](https://docs.byteplus.com/en/docs/ecs/Image_Detection_Overview) |
|To use an image across accounts |[Sharing or cancelling sharing of custom image](https://docs.byteplus.com/en/docs/ecs/Sharing-or-canceling-sharing-image) |
|To use an image across regions |[Replicating custom image](https://docs.byteplus.com/en/docs/ecs/Copying_custom_images) |
|To export an image and download it to local volume for use |[Exporting custom image](https://docs.byteplus.com/en/docs/ecs/Exporting-custom-images) |
|To manage the progress and details of custom image tasks |[Managing custom image tasks](https://docs.byteplus.com/en/docs/ecs/Managing-custom-image-tasks) |


&nbsp;

<span id=".5LqR55uY5ZKM5b-r54Wn"></span>
## Volume and snapshot


|Functionality |Applicable scenario |Actions guide |
|---|---|---|
|Volume |A highly available, highly reliable, high\-performance, elastic, and scalable block storage device. You can use it as scalable disk storage for ECS and Vital Kubernetes Engine services. |1. [Creating volume](https://docs.byteplus.com/en/docs/ecs/Create-a-volume)<br><br>2. [Attaching volume](https://docs.byteplus.com/en/docs/ecs/Attach-a-volume)<br><br>3. [Partitioning and formatting volume](https://docs.byteplus.com/en/docs/ecs/Partition-and-initialize-a-volume) |
|Snapshot |A backup method where each snapshot is a backup file of volume data at a specific point in time. When data is lost or system fails, you can roll back volume data by using the snapshot feature to recover the lost data. |* [Creating snapshot](https://docs.byteplus.com/en/docs/ecs/Create-a-snapshot): You can create a snapshot as a data backup of a volume at a specific point in time.<br><br>* [Using snapshot to roll back volume](https://docs.byteplus.com/en/docs/ecs/Rollback-volume-through-snapshot): If there is an error in the volume data, you can roll back the volume by using a volume snapshot taken at a specific point in time.<br><br>* If the volume capacity can not meet your business needs, refer to the following topics:<br><br>   * [Expanding volumes for a Linux ECS instance](https://docs.byteplus.com/en/docs/ecs/Extend-volume-linux)<br><br>   * [Expanding volumes for a Windows ECS instance](https://docs.byteplus.com/en/docs/ecs/Extend-volume-windows) |


<span id=".572R57uc"></span>
## Network


|Functionality |Applicable scenario |Actions guide |
|---|---|---|
|Virtual Private Cloud   |An isolated and self\-configured virtual network environment that provides high security for the ECS instance. You can fully manage your VPC and the resources in it. |[Changing VPC or subnet](https://docs.byteplus.com/en/docs/ecs/Changing-the-VPC-or-subnet-of-an-ECS-instance) |
|Network Interface |It is a virtual hardware device that the ECS relies on for network communication, and it also carries the IP address. |* [Mounting/unmounting secondary network interface for instance](https://docs.byteplus.com/en/docs/ecs/Attaching-and-detaching-secondary-network-interfaces)<br><br>* [Assigning IPv6 addresses to primary/secondary network interfaces associated with instance](https://docs.byteplus.com/en/docs/ecs/Assigning-or-releasing-a-private-IPv6-address) |
|Security group  |This feature is designed based on the allowlist principle to control the outbound and inbound traffic at each network interface of the ECS instance. You can add security group rules to allow the required traffic at the network interface based on your needs. |* [How to make a security group plan](https://docs.byteplus.com/en/docs/ecs/How-to-plan-security-groups)<br><br>* [Changing the security group for an ECS network interface](https://docs.byteplus.com/en/docs/ecs/Changing-security-groups) |
|Elastic IP (EIP) |If you associate an EIP with your ECS instance, the ECS instance can communicate with the Internet and other on\-cloud/off\-cloud resources associated with the EIP. This makes communication flexible and easy. |* [Associate EIP](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP)<br><br>* [Disassociate EIP](https://docs.byteplus.com/en/docs/ecs/Disassociating-an-EIP)<br><br>* [Changing EIP configuration](https://docs.byteplus.com/en/docs/ecs/Changing_EIP_configuration) |


<span id=".5a6J5YWo6Ziy5oqk"></span>
## Security

<span id=".5a6e5L6L5YaF6YOo6Ziy5oqk"></span>
### Internal protection for instance

Weak passwords, IP addresses and ports imprecisely opened are potential security risks for the instance. To fundamentally increase the security level of the instance, we recommend that you first enhance the internal protection capability of the instance.


|Protection method |Note |Actions guide |
|---|---|---|
|Password |It is recommended to improve the password complexity such as adding uppercase letters, symbols, and numbers or using a long password. |[Resetting passwords](https://docs.byteplus.com/en/docs/ecs/Resetting-passwords) |
|Key pairs |Compared to "Password", we recommend that you use "Key Pair", which is based on an encryption algorithm and is applicable for scenarios that require higher security. |[Overview of key pair](https://docs.byteplus.com/en/docs/ecs/Key-pair-overview) |
|Security group  |The security group is used to control the inbound and outbound network traffic of each network interface of the ECS instance. It is an important isolation manner for ensuring network security. The security group feature helps you to control access to or from the ECS instance.<br><br>To ensure resource security within the security group, we recommend that you follow the principle of least privilege and cautiously and precisely allow IP addresses and ports. |* [Security group overview](https://docs.byteplus.com/en/docs/ecs/Security-group-overview)<br><br>* [Common ports for ECS instances](https://docs.byteplus.com/en/docs/ecs/Common_ports_for_ECS_instances) |


<span id=".5a6e5L6L5aSW6YOo6Ziy5oqk"></span>
### External protection for instance

Internal protection prevents access from unknown sources, but external security issues such as DDoS traffic attacks, anomalous intrusions, and brute force cracking also occur from time to time. You are recommended to select protection methods based on the business situation.


|Protection method |Note |Actions guide |
|---|---|---|
|Security Enhancement |If you enable this feature enabled, the system dynamics will be monitored and analyzed in real time. In addition, file monitoring, process monitoring, and alerting for exceptions like unauthorized logins are also enabled, lowering the risk of host intrusion. |[Enabling security enhancement for instance](https://docs.byteplus.com/en/docs/ecs/Security-enhancement) |
|DDoS Protection |Relying on massive protective bandwidth, multidimensional protection algorithms, and efficient cleaning systems, we provide professional protection services for gaming, Internet+, finance, and other businesses susceptible to DDoS attacks. This service effectively avoids business interruptions caused by DDoS attacks. |Configuring DDoS protection for instance |


<span id=".55uR5o6n"></span>
## Monitoring

Comprehensive monitoring metrics, event\-based monitoring, and visual data displays help you track the operating status of the resources you have created. You can customize the alert feature to be promptly notified when exceptions occur on your instance.


|Functionality |Applicable scenario |Actions guide |
|---|---|---|
|Metric monitoring |This feature allows you to view various monitoring data of an instance, such as data of basic monitoring, operating system monitoring, TCP monitoring, process monitoring, GPU monitoring, and RDMA monitor. |[Viewing instance GPU/RDMA monitoring data](https://docs.byteplus.com/en/docs/ecs/Viewing-instance-monitoring-data) |
|Event monitoring |This feature is used to record and notify ECS information. When an instance or task triggers a system event (such as a system failure that leads to instance redeployment), you can promptly view the event details and take action. |[Querying and handling ECS events](https://docs.byteplus.com/en/docs/ecs/Querying-and-handling-events) |
|Instance monitoring and status monitoring |To automatically detect software and hardware operating information of the instance and calculate the health status of the instance, helping you quickly understand the health condition of the instance. |[View instance health status](https://docs.byteplus.com/en/docs/ecs/Viewing-instance-health-status) |


<span id=".6L-Q57u0"></span>
## O&M

The following O&M functions help you quickly address instance exceptions and ensure service stability.


|Functionality |Applicable scenario |Actions guide |
|---|---|---|
|Accessing instance system logs and screenshots |When an instance encounters a failure, you need to identify the cause based on system logs and screen information. However, the failed instance can not be accessed remotely in most failure cases. |[Accessing instance system logs and screenshots](https://docs.byteplus.com/en/docs/ecs/Obtaining-instance-system-logs-and-screenshots) |
|Cloud assistant |A native automated O&M tool. With Cloud Assistant, you can perform operation commands on one or multiple objects. You do not need to input passwords, log in, or use a jump server. |[Use procedure](https://docs.byteplus.com/en/docs/ecs/Overview-of-cloud-assistant#.5L2_55So5rWB56iL) |
|Operations orchestration |An automated O&M service for cloud products. You can orchestrate task flows based on your needs and execute them automatically. You can also centrally manage orchestrated tasks and view the execution progress and results. |[Use procedure](https://docs.byteplus.com/en/docs/ecs/Overview_of_Process_Orchestration#.5L2_55So5rWB56iL) |
|Instance Diagnosis |This feature is used to check instance performance, status of network, volumes, and other items. This helps you timely identify and understand common issues with ECS instances to ensure normal operation of your instance. |[Overview of instance diagnosis](https://docs.byteplus.com/en/docs/ecs/Instance_diagnosis_overview) |


<span id=".5qCH562-5LiO6aG555uu"></span>
## Tags and projects


|Functionality |Applicable scenario |Actions guide |
|---|---|---|
|tag |Resources with similar characteristics can be tagged and categorized for unified management and accounting. |[Associate a tag](https://docs.byteplus.com/en/docs/ecs/Tag-overview#.5Yib5bu65bm257uR5a6a5qCH562-) |
|project |With Identity and Access Management (IAM), you can grant permissions to users by project (i.e., a group of resources) to ensure resource isolation and data security. You can also view resource bills by project to facilitate the calculation of cloud resource costs. |[Project management process](https://docs.byteplus.com/en/docs/ecs/Managing-projects#.6aG555uu566h55CG5L2_55So5rWB56iL) |
