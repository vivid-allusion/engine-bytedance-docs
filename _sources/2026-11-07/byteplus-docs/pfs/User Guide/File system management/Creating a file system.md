---
title: "Creating a file system"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/Creating-a-file-system"
---

This topic introduces the preparation work and operation steps for creating a file system on the PFS console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite

Before using Parallel File Storage, please make sure you have completed the following steps:


1. Before using PFS, make sure that you have signed up for BytePlus. For more information, refer to [Signing up for BytePlus accounts](https://docs.byteplus.com/byteplus-platform/docs/signing-up-your-account).

2. The project to which the file system belongs has been created. For more details about the project and the specific steps to create a project, please refer to [Creating a project](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-project).

3. You have created VPC . If you have not created a VPC or wish to recreate a VPC, please refer to [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

4. You have created mounting nodes within the VPC, including ECS and GPU servers. For specific purchasing steps, please refer to [Using the wizard to buy ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">For optimal performance, it is recommended to deploy PFS and the nodes that need to be mounted in the same availability zone.   </div>
   

5. You have completed cross\-service authorization. For specific steps, please refer to [Cross-service authorization](https://docs.byteplus.com/docs/pfs/Cross-service-authorization).


<span id=".5pON5L2c5q2l6aqk"></span>
## **Procedure**


1. Log on to the [PFS console](https://console.byteplus.com/pfs).

2. In the top menu bar, select the region where you want to create the file system.

3. Select **File System** \> **Instances** List in the left navigation bar . On the Instance List page, click **Create File System** in the top left corner.

4. On the **Create File System** page, set the following parameters.

   
   |**Parameters** |**Description** |
   |---|---|
   |Name |Set the name of the file system. The naming convention is as follows:<br><br><br>* Only Chinese and English are allowed at the beginning.<br><br>* Can only contain Chinese characters, letters, numbers, underscores (_) and hyphens (\-).<br><br>* The length needs to be within 1 to 128 characters. |
   |Description |Set the description information of the file system for easy differentiation. This is an optional field with a length of 0 to 120 characters. |
   |Availability Zone |Choose the available zone for the file system.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For optimal performance, it is recommended to deploy PFS and the nodes that need to be mounted in the same availability zone.</div><br> |
   |Specifications |Choose the specifications of the file system. For detailed information about the specifications, please refer to [Product specifications](https://docs.byteplus.com/docs/pfs/Product-specifications). |
   |Capacity |Select the capacity of the file system. For more information, please refer to [Product specifications](https://docs.byteplus.com/docs/pfs/Product-specifications). |
   |Tag |Click **Add tags**, enter the tag key and tag value to add tags to the file system. For detailed rules on setting tag key values, please refer to [Binding or adding tags](https://docs.byteplus.com/docs/pfs/Binding-or-adding-tags).<br><br>Tags consist of key\-value pairs and are used to identify cloud resources. They can help you categorize cloud resources with similar characteristics from different perspectives, such as usage, owner, or environment, making it easier to filter and aggregate them for efficient cloud resource management. For more information, please refer to [Overview](https://docs.byteplus.com/docs/pfs/Overview). |
   |Virtual private cloud |Select the private network where the instance is located. It is recommended that the file system and the ECS instance to be mounted are in the same private network. Otherwise, they will not be able to achieve optimal performance through internal network communication.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After the file system is successfully created, the private network cannot be modified.</div><br> |
   |Subnet |Select the subnets available in the virtual private network (VPC). Subnets are blocks of IP addresses within a private network. All cloud resources in the VPC must be deployed within a subnet, which allocates private IP addresses to the resources. For more details, please refer to [Creating a subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet). |
   |Project |Select the project to create a file system.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="tip">A project is a virtual concept that includes a group of resources, users, and roles. Through a project, a unified view and management of a group of resources can be achieved, and the permissions of users and roles within the project to access these resources can be controlled.</div><br> |
   |Billing type |Current PFS only supports pay\-as\-you\-go billing. For billing details, please refer to [Billing overview](https://docs.byteplus.com/docs/pfs/Billing-overview). |
   

5. After setting the parameters, click **Confirm order** to enter the order details page.

6. On the **Details** page, confirm the file system parameters, read and check the **Storage Products and Services Terms**, and click **Buy now**.

7. After confirming that the information is correct, click **Next step**.

   After the purchase is completed, you can click **Go to Product Console** to view the file system in the file list.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Creating a file system takes some time. Please be patient and wait.   </div>
