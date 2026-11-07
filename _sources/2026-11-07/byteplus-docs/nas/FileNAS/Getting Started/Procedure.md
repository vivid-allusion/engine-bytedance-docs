---
title: "Procedure"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Manual"
---

This topic introduces the usage process of FileNAS, helping you quickly get started with FileNAS.

<span id="ee17ba35"></span>
## Prerequisite

Before using FileNAS, please make sure you have completed the following steps:


1. Before using FileNAS, make sure that you have signed up for BytePlus. For more information, refer to [Signing up for BytePlus accounts](https://docs.byteplus.com/byteplus-platform/docs/signing-up-your-account).

2. The project to which the file system belongs has been created. For more details about the project and the specific steps to create a project, please refer to [Creating a project](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-project).

3. You have created VPC. If you have not created a VPC or wish to recreate a VPC, please refer to [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

4. You have created an ECS instance within the VPC. For specific steps, please refer to [Using the wizard to buy ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Both VPC and ECS need to be in the same region as the file system.   </div>
   

5. You have completed cross\-service authorization. For specific steps, please refer to [Cross-Service Authorization](https://docs.byteplus.com/docs/nas/Cross-Service-authorization).


<span id="2cb2b78b"></span>
## Usage process


|**Steps** |**Description** |
|---|---|
|1. Choose file system specifications |Before using FileNAS, please choose the appropriate product specifications according to your use case. For detailed instructions, please refer to [Product specifications](https://docs.byteplus.com/docs/nas/Product-specifications). |
|2. Creating a file system |After selecting the file system specifications, you can create a file system through the console or API. For detailed instructions, please refer to the following documentation.<br><br><br>* Console:<br><br>   * Extreme FileNAS: [Creating a file system](https://docs.byteplus.com/docs/nas/Creating-a-file-system)<br><br>   * Cache FileNAS: [Creating file systems](https://docs.byteplus.com/en/docs/nas/Creating_file_systems)<br><br>* API: [CreateFileSystem](https://docs.byteplus.com/en/docs/nas/CreateFileSystem) |
|3. Creating a mount pount |The mount point is the entry point for ECS instances to access the file system. You need to create a mount point before you can mount the file system. For specific steps, please refer to the following document:<br><br><br>* Console:<br><br>   * Extreme FileNAS: [Managing mount targets](https://docs.byteplus.com/docs/nas/Managing-mount-points)<br><br>   * Cache FileNAS: [Managing mount targets](https://docs.byteplus.com/en/docs/nas/Managing_mount_targets)<br><br>* API: [CreateMountPoint](https://docs.byteplus.com/en/docs/nas/CreateMountPoint) |
|4. Mounting a file system |The file system needs to be mounted to the ECS instance before it can be used. For the specific steps of mounting, please refer to<br><br><br>* Extreme FileNAS: [Mounting a file system](https://docs.byteplus.com/docs/nas/Mounting-a-file-system)<br><br>* Cache FileNAS: [Mounting file systems](https://docs.byteplus.com/en/docs/nas/Mounting_file_systems) |


&nbsp;
