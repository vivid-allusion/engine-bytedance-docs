---
title: "Copying custom images"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Copying_custom_images"
---

You can use the image replication feature to copy the system volume, data volume, and configuration of the specified custom image to other regions, enabling cross\-region ECS instance deployment and cross\-region data backup.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is in Beta. If you need a trial, please contact your account manager.</div>


<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes


| ||
|---|---|
|**Source image restrictions** ||
|Volume capacity |The volume capacity of each snapshot associated with the source custom image can not exceed 1 TiB. If the limit is exceeded, you can migrate data to the target region by using the SMC. [Learn more](https://docs.byteplus.com/en/docs/smc/Same-Account-or-Cross-Account-migration-of-ECS). |
|Management restrictions |During the replication process, you cannot delete the target image or source image, export or share the target image, or use the target image to create an instance. |
|**Target restrictions** ||
|Region |* The target region must be different from the source region.<br><br>* Supported regions for the Copy operation:<br><br>   * Regions in the Chinese mainland:<br><br>      * China (Beijing)(cn\-beijing)<br><br>      * China (Shanghai)(cn\-shanghai)<br><br>      * China (Guangzhou)(cn\-guangzhou)<br><br>   * Regions outside the Chinese mainland:<br><br>      * China (Hong Kong)(cn\-hongkong)<br><br>      * Asia Pacific (Johor)(ap\-southeast\-1)<br><br>      * Asia Pacific (Jakarta)(ap\-southeast\-3)<br><br>* Rules for copying:<br><br>   * Copying custom images is supported between Chinese mainland regions or between regions outside the Chinese mainland.<br><br>   * You can copy an image from a region in the Chinese mainland to the Asia Pacific (Johor) region. |
|Image quantity |The number of existing custom images in the target region must be less than 50. |
|License type |The license type of the target image must be consistent with that of the source image. |
|**Data replication restrictions** ||
|The project and shared attributes of the source image will not be copied to the target image. ||


&nbsp;

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Image console](https://console.byteplus.com/image/region:image+cn-beijing/images?projectName=default&tab=2). 

2. On the image list page, select the "Custom Image" tab.

3. In the top menu bar, select the project and region where the source image is located.

4. Select the image to be replicated and click "… \> Copy Image" in the "Actions" column.

5. Complete the following configuration in the "Copy Image" pop\-up window.

   
   |Parameter​ |Description |Sample value |
   |---|---|---|
   |Target region |Select the region for the copied image.<br><br>> Only cross\-region replication is supported. The source region must be different from the target region. |Asia Pacific (Johor) |
   |Custom image name |Enter the name of the custom image displayed in the target region. |copy_image |
   |Project (optional) |Select the project to which the custom image belongs.<br><br><br>* Once the project is selected, the replicated custom image can only be viewed and used by users with permissions on that project.<br><br>* If no project is available in the drop\-down list, you can follow the guidelines to create a project. For more information, see [Creating projects](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Management#creating-project).<br><br>* If you want to change the project to which the image belongs after the image is copied, refer to [Project resource management](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Resource_Management).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">A project is a collection of resources. You can add custom images to projects and classify and manage custom images by project. Additionally, you can control the permissions of users and roles within each project on custom images. For more details, refer to <a href="https://docs.byteplus.com/en/docs/resourcemanagement/Resource_Center_Overview">Resource center overview</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You can copy a custom image belonging to project A to project B, but the account performing the image copy action must have operational permissions on both project A and project B. For information about how to authorize an account to manage projects, refer to <a href="https://docs.byteplus.com/en/docs/resourcemanagement/Project_Permission_Management">Project permission management</a>.</div><br> |projectA |
   |Tag (optional) |The tags of the source image can be inherited. You can also specify custom tags.<br><br><br>* Inheritance tag: When you select "Inheritance tag", the target image inherits the existing tag information of the source image.<br><br>* Custom tag: You can configure new tags for the target image.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">A tag is a key\-value pair used to identify cloud resources. Tags help you categorize cloud resources with similar attributes based on different dimensions, such as purpose, owner, or environment. This allows you to search and aggregate your cloud resources for easy management. For more information, refer to <a href="https://docs.byteplus.com/en/docs/resourcemanagement/Tag_Overview">Tag overview</a>.</div><br> |\- |
   

6. Click "Copy" to replicate the image.

7. You can copy the image ID in the pop\-up window, go to the "Custom Image" tab in the target region, and view the replication progress.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When the replication task is in progress, the status of the target image is <strong>Creating</strong>. After replication is complete, the status of the target image turns to <strong>Available</strong>. In this case, an independent new image with a unique image ID is generated in the target region.   </div>
   

<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations

Upon completing replication, you will obtain a custom image with the same configuration but a different ID in the target region. In the target region, you can use the replicated image to [purchase instances](https://docs.byteplus.com/en/docs/ecs/Buying-ECS-instances-with-custom-images) or [change the instance operating system](https://docs.byteplus.com/en/docs/ecs/Changing-OS).

<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [CopyImage](https://docs.byteplus.com/en/docs/ecs/CopyImage)

* [DescribeTasks](https://docs.byteplus.com/en/docs/ecs/DescribeTasks)
