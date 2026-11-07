---
title: "Procedure"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/Procedure"
---

This topic introduces the usage process of Parallel File Storage, helping you quickly get started with Parallel File Storage.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite

Before using Parallel File Storage, please make sure you have completed the following steps:


1. Before using TOS, make sure that you have signed up for BytePlus. For more information, refer to [Signing up for BytePlus accounts](https://docs.byteplus.com/byteplus-platform/docs/signing-up-your-account).

2. The project to which the file system belongs has been created. For more details about the project and the specific steps to create a project, please refer to [Creating a project](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-project).

3. You have created VPC. If you have not created a VPC or wish to recreate a VPC, please refer to [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

4. You have created an ECS instance within the VPC. For specific steps, please refer to [Using the wizard to buy ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Both VPC and ECS need to be in the same region as the file system.   </div>
   

5. You have completed cross\-service authorization. For specific steps, please refer to [Cross-service authorization](https://docs.byteplus.com/docs/pfs/Cross-service-authorization).


<span id=".5L2_55So5rWB56iL"></span>
## Usage Process

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f23bb4cdf2594cdcaa427679b97d78c2~tplv-goo7wpa0wc-image.image) </span>


|**Steps** |**Description** |
|---|---|
|1. Choose file system specifications |Before using Parallel File Storage, please choose the appropriate product specifications according to your use case. For detailed instructions, please refer to [Product specifications](https://docs.byteplus.com/docs/pfs/Product-specifications). |
|2. Creating a file system |After selecting the file system specifications, you can create a file system through the console or API. For detailed instructions, please refer to the following documentation.<br><br><br>* [Creating a file system](https://docs.byteplus.com/docs/pfs/Creating-a-file-system)<br><br>* [CreateFileSystem](https://docs.byteplus.com/docs/pfs/CreateFileSystem) |
|3. Creating a mount service |The mount service is the entry point for ECS instances to access the file system. You need to create a mount service before you can mount the file system. For specific steps, please refer to the following document:<br><br><br>* [Creating a mount service](https://docs.byteplus.com/docs/pfs/Creating-a-mount-service)<br><br>* [CreateMountService](https://docs.byteplus.com/docs/pfs/CreateMountService) |
|4. Mounting a file system |The file system needs to be mounted to the ECS instance before it can be used. For the specific steps of mounting, please refer to [Mounting a file system](https://docs.byteplus.com/docs/pfs/Mounting-a-file-system). |


&nbsp;
