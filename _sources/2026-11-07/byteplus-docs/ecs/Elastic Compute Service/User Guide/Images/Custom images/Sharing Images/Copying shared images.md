---
title: "Copying shared images"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Copy_shared_image"
---

If you want to modify an image shared with your account or use the shared image across regions, you can copy the image as a custom image and perform operations on the custom image.

<span id="89VranSx"></span>
## Usage notes


|**Shared image** ||
|---|---|
|Management restrictions |Image sharing cannot be canceled while the shared image is being copied. |
|**Target image** ||
|Region |You can copy a shared image only to the region in which the shared image is located. |
|Image quantity |The number of existing custom images in the target region must be less than 50. |
|License types |The license type of the target image must be consistent with that of the shared image. |
|System volume |If the system volume capacity of the shared image is less than 20 GiB, the  platform automatically adjusts the system volume capacity of the target image to 20 GiB. |
|**Data replication** ||
|The project and tag attributes of the shared image will not be copied to the target image. ||


<span id="sHXxT4H0"></span>
## Procedure


1. Log in to the [Image console](https://console.byteplus.com/image/region:image+cn-beijing/images?projectName=default&tab=2).

2. On the image list page, select the "Shared Image" tab.

3. In the top menu bar, select the project and region to which the source image belongs.

4. Click "Copy Image" in the "Actions" column to the right of the shared image to be copied.

5. In the "Copy Shared Image" pop\-up window, complete the following configuration.

   
   |Parameter​ |Description |Sample value |
   |---|---|---|
   |Custom image name |Enter the name of the custom image displayed in the target region. |copy_image |
   |Project (optional) |Select the project to which the custom image belongs.<br><br><br>* Once the project is selected, the replicated custom image can only be viewed and used by users with permissions on that project.<br><br>* If no project is available in the drop\-down list, you can follow the guidelines to create a project. For more information, see [Creating projects](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Management#creating-project).<br><br>* If you want to change the project to which the image belongs after the image is copied, refer to [Project resource management](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Resource_Management).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">A project is a collection of resources. You can add custom images to projects and classify and manage custom images by project. Additionally, you can control the permissions of users and roles within each project on custom images. For more details, refer to <a href="https://docs.byteplus.com/en/docs/resourcemanagement/Resource_Center_Overview">Resource center overview</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You can copy a custom image belonging to project A to project B, but the account performing the image copy action must have operational permissions on both project A and project B. For information about how to authorize an account to manage projects, refer to <a href="https://docs.byteplus.com/en/docs/resourcemanagement/Project_Permission_Management">Project permission management</a>.</div><br> |projectA |
   |Tag (optional) |Configure the tag information of the target image.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">A tag is a key\-value pair used to identify cloud resources. Tags help you categorize cloud resources with similar attributes based on different dimensions, such as purpose, owner, or environment. This allows you to search and aggregate your cloud resources for easy management. For more information, refer to <a href="https://docs.byteplus.com/en/docs/resourcemanagement/Tag_Overview">Tag overview</a>.</div><br> |\- |
   

6. Click "Copy" to replicate the shared image.

7. You can copy the image ID in the pop\-up window, go to the "Custom Image" tab in the target region, and view the replication progress.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When the replication task is in progress, the status of the target image is <strong>Creating</strong>. After replication is complete, the status of the target image turns to <strong>Available</strong>. In this case, an independent new image with a unique image ID and a snapshot is generated in the target region. For snapshot billing details, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Overview-of-snapshots">Snapshot overview</a>.   </div>
   

<span id="h559oVt8"></span>
## Subsequent operations

You can use the replicated image to [purchase instances](https://docs.byteplus.com/en/docs/ecs/Buying-ECS-instances-with-custom-images) or [change the instance operating system](https://docs.byteplus.com/en/docs/ecs/Changing-OS). You can also deploy an image across regions by using the [custom image replication](https://docs.byteplus.com/en/docs/ecs/Copying_custom_images) feature.

<span id="KZtCXizB"></span>
## Related documents


* [CopyImage](https://docs.byteplus.com/en/docs/ecs/CopyImage)

* [DescribeTasks](https://docs.byteplus.com/en/docs/ecs/DescribeTasks)
