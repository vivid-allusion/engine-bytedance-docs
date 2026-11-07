---
title: "Creating a mount service"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/Creating-a-mount-service"
---

The mounting service is the connection point of the file system in a network environment. The file system needs to be mounted on a computing node in order to access and store data. This topic introduces the steps for creating a mounting service.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* Mounting the VPC where the service is located requires using the default routing rules for the 100.64.0.0/10 network segment.If you have modified the routing table rules of this VPC, please submit a ticket before creating the mounting service.

* After the mount service is created, the system will automatically create 3 ECS instances to manage the client cluster. Please make sure your account meets the requirements for purchasing corresponding ECS instance specifications.

   * Currently supported ECS instance types include ecs.g2i.large, ecs.g2i.xlarge, and ecs.g2i.2xlarge. Please refer to the console for the specific available instance types.

   * After creating an ECS instance, this instance will incur ECS product fees. For details on the billing of ECS instances, please refer to [Billing overview](https://docs.byteplus.com/en/docs/ecs/Billing-overview).

   * After creation, you can log in to the[ ECS console](https://console.byteplus.com/auth/login?redirectURI=%2Fecs%2Finstance) to view the created instances.

   * Please do not directly delete the automatically created instances in the ECS console.

* The mount service name is unique for each region and each account, and cannot be duplicated.

* Please do not modify the configuration files in `/etc/hosts` and `/root/.ssh` of the PFS management node.


<span id=".5pON5L2c5q2l6aqk"></span>
## **Procedure**


1. Log on to the [PFS console](https://console.byteplus.com/pfs).

2. In the top menu bar, select the region where the target file system is located.

3. Select **File System** \> **Mount Service** in the left navigation bar , and click **Create Mount Service**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When creating a mount service for the first time, you need to complete the authorization according to the prompts on the interface.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you have already authorized before, there is no need to authorize again.   </div>
   

4. Set the following parameters in the pop\-up dialog box.

   
   |**Parameters** |**Description** |
   |---|---|
   |Mount Service Name |Set the name of the mount service. The naming convention is as follows:<br><br><br>* Cannot start with numbers, hyphens (\-), or underscores (_).<br><br>* Only Chinese characters, letters, numbers, underscores (_) and hyphens (\-) are allowed.<br><br>* The length needs to be within 1 to 128 characters.<br><br>* The service name for each account in each region must be unique and cannot be duplicated. |
   |Availability Zone |Choose the availability zone where you want to create the mount service. |
   |Virtual private cloud |Select the same VPC network as the file system and ECS. |
   |Subnet |Select a subnet under the VPC network.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="tip">In order to achieve optimal performance experience, the file system, ECS instances, and subnets need to be in the same availability zone.</div><br> |
   |Project |Select the project to which the mounting service needs to belong. |
   |Node specification |Choose the specifications for creating three ECS management nodes. Please refer to the specifications displayed on the console for supported specifications. |
   

5. After setting up, click **Create**.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Creating a mounting service may take approximately 10 minutes. Please be patient and wait. After creation, you will need to refresh the mounting service list page to check the creation status.   </div>
