---
title: "Sharing or unsharing custom images"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Sharing-or-canceling-sharing-image"
---

You can share custom images that you create with other accounts on the platform. This allows you to deploy ECS instances across accounts. You can unshare an image when you no longer want to share the image with other accounts.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes


|**Sharing account** ||
|---|---|
|Number of platform accounts with which an image can be shared |Each image can be shared with up to 50 platform accounts. |
|Target region |You can share an image with an account that resides in the same region as the image. Cross\-region image sharing is not supported. |
|Source image management |* Shared images that are shared with other platform accounts cannot be directly deleted. You must remove all sharing relationships of the image before deletion.<br><br>* Only custom images with the "Available" status can be shared. |
|**Receiving account** ||
|Limits |* You can use a shared image to [create instances](https://docs.byteplus.com/en/docs/ecs/Buying-ECS-instances-with-custom-images) and [change operating systems](https://docs.byteplus.com/en/docs/ecs/Changing-OS). You cannot delete or modify a shared image.<br><br>* Both receiving accounts and their IAM users can use the shared images. However, the account using the image must have permission to perform the target actions. Examples:<br><br>   * When IAM user A uses a shared image to create an instance, IAM user A must have the permission to create instances (RunInstances).<br><br>   * When IAM user B uses a shared image to change the operating system, IAM user B must have the permission to change the operating system (ReplaceSystemVolume).<br><br>* You are not allowed to share images with other platform accounts if the images are shared with your account by other users.<br><br>* Shared images are user\-owned private images. The platform cannot guarantee their security and integrity. Confirm that the images are shared by trusted accounts before you use the shared images. |
|Billing rules |If the source image is chargeable, when the receiving account uses the shared image, the account is also charged. The billing rules are the same as those of the source chargeable image. |
|License types |The license type of the shared image must be consistent with that of the source image. |


<span id=".5YWx5Lqr6ZWc5YOP"></span>
## Share an image

You can use the ECS console or the resource management console to share your custom images with other accounts.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">You can share custom images with other BytePlus accounts in either the ECS console or the resource management console. Additionally, you can directly share resources with the entire enterprise organization, departments, and member accounts by using the resource management feature.</div>


* <div data-tips="true" data-tips-type="warning">Sharing custom images within an enterprise organization by using the Resource Sharing (RS) feature is currently in Beta. To request a trial, <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> or contact your account manager. For more information, see <a href="https://docs.byteplus.com/en/docs/resourcemanagement/Resource_Share_Overview">Resource Share Overview</a>.</div>



<span id="VeNKi2ih"></span>
### Share custom images in the image console


1. Log in to the [Image console](https://console.byteplus.com/image/region:image+cn-beijing/images?projectName=default&tab=2). 

2. Select the "Custom Image" tab.

3. In the top menu bar, select the region where the target image is located.

4. Click "Shared Image" in the "Actions" column of the custom image to be shared.

5. In the pop\-up window, enter the ID of the receiving account and click "Share".

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Separate multiple account IDs with Enter keys. For information about how to view the account ID, see <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview">Managing account information</a>.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">To share images within an organization, click the "sharing within the organization" button to go to the resource sharing console and perform sharing operations. <a href="https://docs.byteplus.com/en/docs/ecs/Sharing-or-canceling-sharing-image#6ChABlDg">Learn more</a>.   </div>
   

6. After you share an image with other accounts, you can view the shared image in the custom image list. The shared image has the "Shared" tag. Click the name of the shared custom image to view the information of the receiving account on the "Shared object" tab of the details page.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The shared image is a non\-project resource. Even if the source image is a project resource, the shared image will not be added to the project.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The receiving accounts and their IAM users with permission to perform operations on shared images can view the accessible shared images by clicking "Image \> Shared Image". For more project details, see <a href="https://docs.byteplus.com/en/docs/resourcemanagement/Project_Management">Project management</a>.   </div>
   


<span id="6ChABlDg"></span>
### Share custom images in the resource sharing console


1. Log in to the [resource sharing](https://console.byteplus.com/resourcemanager/region:resource-manager+cn-beijing/resource_share/owned?menuKey=rs) console.

2. In the directory tree on the left, select "Resource sharing \> Shared by me".

3. In the top menu bar, select the region where the relevant resources are located.

4. Select the "Shared by me" tab, click the "Create shared unit" button, and configure the following information in sequence.

   1. **Configure basic information and associate resources**

      
      |Parameter​ |Description |
      |---|---|
      |Unit name |Specify a name for the shared unit. |
      |Resource select |Specify the resource type and select the resources to be shared.<br><br><br>* Region: The region where the resources to be shared are located. To change the region, select the new region in the top menu bar.<br><br>* Product: Select "ecs \- image" and select the custom images to be shared. |
      

   2. **Associate sharing permissions**

      The system automatically associates the preset policy library based on the resource type. You can click to view the details of the shared policies.

   3. **Associate shared users**

      
      |Parameter​ |Description |
      |---|---|
      |Resource user |Select the scope of resource users. Supported:<br><br><br>* Allow sharing with any account: The resource owner can share resources with any root user. If the resource owner belongs to an enterprise organization, resources can also be shared with the entire enterprise organization, its departments, and member accounts.<br><br>* Only allow sharing with enterprises and organizations: The resource owner must belong to an enterprise organization, and resources can only be shared with the organization itself, its subordinate Organizational Units (OUs), and member accounts. This option is unavailable to non\-administrators of the enterprise organization. |
      ||Select the method for adding resource users. Supported:<br><br><br>* Add by business organization: Only the enterprise organization administrator can enable this option and select the entire organization, organizational units (OUs), or member accounts directly from the enterprise organization tree directory.<br><br>* Select the user type and specify the user ID to add a resource user: Select the intended user type first and then specify the root user ID, enterprise organization ID, or enterprise organization OUID to add a resource user. |
      |Shared users added |View information about shared accounts that have already been added. |
      

   4. **Confirm and submit the request**

      After you confirm that the current configuration of shared resources, shared users, and other information is correct, click the "Confirm" button to create the shared unit.

   5. When the new shared unit is in the **Enabled** status, the shared unit is created as expected.

6. After you share an image with other accounts, you can view the shared image in the custom image list. The shared image has the "Shared" tag.

   1. Click the name of the shared custom image to view the information of the receiving account on the "Shared object" tab of the details page.

   2. You can also click the "Resource Sharing Console" button to view and manage shared account information in the resource sharing console.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The shared image is a non\-project resource. Even if the source image is a project resource, the shared image will not be added to the project.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The receiving accounts and their IAM users with permission to perform operations on shared images can view the accessible shared images by clicking "Image \> Shared Image". For more project details, see <a href="https://docs.byteplus.com/en/docs/resourcemanagement/Project_Management">Project Management</a>.   </div>
   


<span id=".5Y-W5raI5YWx5Lqr6ZWc5YOP"></span>
## Unshare images

After you unshare an image, the instances that are created or reinstalled by the receiving accounts based on the image are not affected. However, the receiving accounts cannot query the shared image or use the image to create an instance or change the operating system.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Image sharing cannot be canceled while the shared image is being copied by the receiving account. <a href="https://docs.byteplus.com/en/docs/ecs/Copy_shared_image">Learn more</a>.</div>


<span id="dhS7hYmB"></span>
### Unshare images in the image console

When your custom image is shared with other BytePlus accounts in the image console, you can refer to this section to unshare the image.


1. Log in to the [Image console](https://console.byteplus.com/image/region:image+cn-beijing/images?projectName=default&tab=2). 

2. Select the "Custom Image" tab.

3. In the top menu bar, select the region where the target image is located.

4. Click the name of the shared custom image.

5. On the image details page, select the "Shared object" tab, and click "Cancel sharing" next to the ID of the receiving account.

6. In the pop\-up window, click "OK" to confirm the unsharing.

7. After you unshare a custom image, go to the details page of the custom image and view that the information of the receiving account has been removed from the "Shared object" tab.


<span id="M5XOS9ff"></span>
### Unshare images in the resource sharing console

When your custom image is shared with other BytePlus accounts in the resource sharing console, you can refer to this section to unshare the image.


1. Log in to the [resource sharing console](https://console.byteplus.com/resourcemanager/region:resource-manager+cn-beijing/resource_share/owned?menuKey=rs).

2. In the directory tree on the left, select "Resource sharing \> Shared by me".

3. In the top menu bar, select the region where the relevant resources are located.

4. Select the "Shared by me" tab, and click the "View details" button in the "Actions" column to the right of the target shared unit.

   1. Click the "Edit shared unit" button.

   2. Select "ecs \- image" in the product column.

   3. Clear the image that you no longer want to share.

   4. Click the "Next" button.

   5. After you confirm the sharing permissions and shared user, click the "Confirm" button to complete the operation.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [ModifyImageSharePermission](https://docs.byteplus.com/en/docs/ecs/ModifyImageSharePermission)

* [DescribeImageSharePermission](https://docs.byteplus.com/en/docs/ecs/DescribeImageSharePermission)
