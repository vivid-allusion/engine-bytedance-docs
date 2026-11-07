---
title: "Create VCI resource pool"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Create_VCI_resource_pool"
---

Support users in creating Flink resource pools on VCI common resources, where the computing resources in different pools are isolated and independent.

<span id="add99808"></span>
## Prerequisites


* The private network, subnet, and security group used to create the resource pool need to be established beforehand.

* By default, only the main account, project leader, and administrator (Project_Admin) have the authority to manage Flink resource pools. Please ensure that project members are added and associated with their roles, see [成员管理](https://docs.byteplus.com/docs/undefined/655468147c29cc0301edef1f).


<span id="1b5d8030"></span>
## Create common resources in VCI mode


1. Login to [BytePlus Flink console](https://console.volcengine.com/flink).

2. Select the target region from the top menu bar.

3. In the left navigation bar, select **Project Management**, then search for and click on the project block to enter the project.

4. In the project's left navigation bar, select **Resource Management**, then click the **Resource Pool** tab, followed by clicking **Create Resource Pool**.

5. On the **Create Universal Resource Pool** page, set parameters for the resource pool such as basic information, network data, and storage data, then click **Next: Confirm Order**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6fcd4cdcd05048449ae8b8d3df271428~tplv-goo7wpa0wc-image.image) </span>

   
   |**Primary Configuration Item** |**Secondary Configuration Item** |**Description** |
   |---|---|---|
   |Basic Information |Resource Type |The default is set to **Common Resources**. |
   ||Resource Mode |The default is **VCI Mode**, which deploys a BytePlus Flink resource pool on the Common Resources\-VCI resource domain. |
   ||Billing Type |Deploying a BytePlus Flink resource pool in the Common Resources\-VCI resource domain supports **pay\-as\-you\-go** and **subscription** billing types, please choose as needed.<br><br>For billing details, please refer to [Pay-As-You-Go](https://docs.byteplus.com/docs/flink/45695)and[Annual and Monthly Subscription](https://docs.byteplus.com/docs/flink/45824).<br><br>If you choose the subscription billing type, you also need to select **purchase duration**, and confirm if **auto\-renewal** is needed. |
   ||Resource Pool Name |Enter the name of the resource pool to be created.<br><br><br>* Must be globally unique and cannot be an empty string.<br><br>* Length of 1 to 63 characters.<br><br>* Supports lowercase English letters, numbers, and hyphens (\-); and the name must start and end with a letter or number. |
   ||Regions and availability zones |* Region has been selected and cannot be changed.<br><br>* Select an appropriate availability zone based on the network latency and high availability requirements of the business. For more information, please see[Regions and Availability Zones](https://docs.byteplus.com/docs/flink/45821). |
   ||Associated project |The current resource pool's associated project cannot be changed. |
   ||Tags |Supports adding tags to resource pools for easier identification and management. A maximum of 20 tags can be added.<br><br>Tags are in key\-value pair format. Pay attention to the following when setting:<br><br><br>* Only supports uppercase and lowercase letters, numbers, Chinese characters, and special characters `.:/=+-_@`; key\-value case is sensitive.<br><br>* Keys must not start with any case variation of `volc:`, such as `volc:`, `Volc:`, `vOlc:`, `volc:`... (16 combinations).<br><br>* Key length must be 1~128 characters; Value length must be 0~256 characters. |
   |Resource configuration |Compute specifications |If you create a **subscription\-based** billing type, you will need to manually configure resources for the BytePlus Flink resource pool. The basic unit of resources is CU, with 1 CU representing: 1 CPU core and 4 GB memory.<br><br>Please set the resource amount according to actual needs. |
   |Network information |Private network |To ensure smooth intra\-network access, it is advisable to choose a VPC located in the same region as your existing cloud services. Within the same VPC, subnets of different availability zones are interconnected.<br><br>If you have not yet created a private network, please refer to [creating a private network](https://www.volcengine.com/docs/6401/69467). |
   ||Subnet |Select a subnet from the drop\-down list.<br><br>The system will automatically filter available subnets based on the region, availability zone, and private network you select. |
   ||Security Group |Select a security group from the dropdown list. |
   |Storage Information |TOS Object Storage |The default is the TOS associated with the product at initialization and cannot be modified. |
   

6. On the **Details** page, view the configuration details of the resource pool, read and agree by ticking the BytePlus Flink related agreement, then click **Purchase Now**.

7. Check the progress of the resource pool creation.

   Click **Go to Console** to return to the resource pool list page and check on the creation progress. The purchased resource pool is displayed as **In Initialization**, and upon completion, it's displayed as **Running**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f68faef6601e4dd0921ad6358a985626~tplv-goo7wpa0wc-image.image) </span>
