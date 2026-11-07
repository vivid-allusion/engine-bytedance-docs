---
title: "Create Resource Pool"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Create_Resource_Pool"
---

The Flink resource pool in the project is used to manage computational resources, which are isolated and independent from each other within the pool. Computational resources are consumed by task operations and debugging, and a Flink resource pool must be created before developing the task.

<span id="eb75e3b4"></span>
## Prerequisites


* After the primary account adds project members, the project administrator (Project_Admin) is generally responsible for creating the Flink resource pool. Please ensure that project members have been added.

* The private network, subnet, security group, and other resources used when creating the resource pool must be created in advance. For related documents, please refer to [Create a VPC](https://docs.byteplus.com/zh-CN/docs/vpc/Creating-a-VPC).


<span id="96617747"></span>
## Create a Universal Resource in VCI Mode


1. Login to [BytePlus Flink Console](https://console.byteplus.com/flink).

2. Select the target region from the top menu bar.

3. Select **Project Management** from the left navigation bar, then search for and click on the project block to enter the project.

4. In the project’s left navigation bar, select **Resource Management**, then click on the **Resource Pool** tab, followed by clicking on **Create Resource Pool**.

5. On the **Create General Resource Pool** page, set the basic information, network information, storage information, and other parameters of the resource pool, then click **Next: Confirm Order**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/72cc7835ad6149219546d917b4807931~tplv-goo7wpa0wc-image.image) </span>


|**Primary Configuration Item** |**Secondary Configuration Item** |**Description** |
|---|---|---|
|Basic Information |Resource Type |Default is **general resources**. |
||Resource Mode |Default is **VCI mode**, which deploys BytePlus Flink resource pools on general resources\-VCI resource domain. |
||Billing Type |Deploying BytePlus Flink resource pools in the general resources\-VCI resource domain supports **pay\-as\-you\-go** and **annual and monthly subscriptions** billing types, please choose as needed.<br><br>For billing details, please see [Pay-As-You-Go](https://docs.byteplus.com/docs/flink/Pay-As-You-Go) and [Annual and Monthly Subscription](https://docs.byteplus.com/docs/flink/Annual_and_Monthly_Subscription).<br><br>If you choose the annual and monthly subscriptions billing type, you also need to choose **purchase duration** and confirm whether **automatic renewal** is required.<br><br>It is advised to use pay\-as\-you\-go resource pools during the testing phase to prevent inaccurate resource estimation; after clear usage is determined, you can switch to annual and monthly subscriptions billing. |
||Resource Pool Name |Enter the name of the resource pool to be created.<br><br><br>* Must be globally unique and cannot be an empty string.<br><br>* Length must be between 1 to 63 characters.<br><br>* Supports lowercase English letters, numbers, and hyphens (\-); the name must start and end with a letter or number. |
||Regions and Availability Zones |* The region is fixed and cannot be changed.<br><br>* Select an appropriate availability zone based on business needs such as network latency and high availability. For more information, please see [Regions and Availability Zones](https://docs.byteplus.com/docs/flink/Regions_and_Availability_Zones). |
||Associated Project |Select the project to which the resource pool belongs from the dropdown menu. |
|Resource configuration |Compute specifications |If a **subscription** billing type is created, you will need to manually configure resources for the BytePlus Flink resource pool. The basic unit of resource is CU, where 1 CU means: 1 CPU core and 4 GB of memory.<br><br>Set the amount of resources according to actual needs. If uncertain initially, you can start by setting it to 5 CU. |
|Network information |Private network |To ensure smooth internal network access, it is recommended to choose a VPC in the same region as your existing cloud services. Within the same VPC, subnets in different availability zones are interconnected.<br><br>If you have not yet created a private network, please refer to [Create a VPC](https://docs.byteplus.com/zh-CN/docs/vpc/Creating-a-VPC). |
||Subnet |Select a subnet from the dropdown list.<br><br>The system will automatically filter available subnets based on your selected region, availability zone, and private network. |
||Security Group |Select a security group from the dropdown list. |
|Storage Information |TOS Object Storage |By default, the TOS associated with product initialization is used, and modifications are not supported. |



6. On the **Details** page, review the resource pool configuration details, read and agree to the BytePlus Flink\-related agreements, then click **Purchase Now**.

7. Check the progress of the resource pool creation.

   Click **Go to Console** to return to the resource pool list page and check the creation progress. The purchased resource pool is displayed as **Initializing** and after completion, it is displayed as **Running**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7446e68cdf304fd2890e519c73c09275~tplv-goo7wpa0wc-image.image) </span>
