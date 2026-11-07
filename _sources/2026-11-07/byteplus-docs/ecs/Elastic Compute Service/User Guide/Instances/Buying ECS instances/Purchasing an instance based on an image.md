---
title: "Purchasing an instance based on an image"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Buying-ECS-instances-with-custom-images"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenarios

You can use a custom image you [created ](https://docs.byteplus.com/en/docs/ecs/Creating-custom-images-1)or [imported](https://docs.byteplus.com/en/docs/ecs/Importing-custom-images), or a [shared ](https://docs.byteplus.com/en/docs/ecs/Sharing-or-canceling-sharing-image)image, to quickly purchase an ECS instance.

<span id=".5pON5L2c6K-05piO"></span>
## Description


|**Limits** ||
|---|---|
|Image type |Only custom images and shared images in the **Available** state support this feature. |
|Instance type |Currently, when creating an instance with a Windows image, you cannot select 3rd\-generation instance types such as g3i, c3i, r3i that use the DPU architecture of the platform. For details of instance types, refer to [Instance types](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types). |
|**Notes** ||
|* After you create an instance with a Windows image, restart the new instance before logging in.<br><br>* When you create an instance of certain instance type with a Windows Server custom image, the platform automatically upgrades the Virtio driver. This improves the compatibility between the image and the instance and enhances system stability. ||


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


<Tabs>
<Tab zoneid="mBhikUUbyP" title="Use the system volume image to purchase an instance">
<TabTitle>Use the system volume image to purchase an instance</TabTitle>

1. Log in to the [Images console](https://console.byteplus.com/image/images). 

2. In the top menu bar, select the region and project of the target image.

3. On the Images page, click the "Custom Image" or "Shared Image" tab.

4. Click "Create Instances" in the "Actions" column to the right of the target image.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The platform uses the selected image as the instance image, and you cannot change it on the instance creation page.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the custom image belongs to a project, you need to use an account that has permission to operate the project to create instances from the image. The instances created from the image also belong to the project. For more information about how to authorize an account to operate a project, see <a href="https://docs.byteplus.com/en/docs/ecs/Managing-projects">Managing access to projects</a>.   </div>
   

5. On the instance creation page, refer to [Purchasing an ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) to create an instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you select a custom image created with an ESSD system volume for instance creation, the system volume type can only be specified as ESSD.   </div>
   


</Tab>
<Tab zoneid="NjhKderi3W" title="Use the whole image to purchase an instance">
<TabTitle>Use the whole image to purchase an instance</TabTitle>

1. Log in to the [Images console](https://console.byteplus.com/image/images). 

2. In the top menu bar, select the region and project of the target image.

3. On the Images page, click the "Custom Image" or "Shared Image" tab.

4. Click "Create Instances" in the "Actions" column to the right of the target whole image.

5. Refer to [Purchasing an ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) to create an instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">By default, the system uses the whole image as the instance image, and you cannot change it.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The system automatically creates the same number of data volumes based on the snapshot associated with the whole image. The capacity of each volume is the same as the corresponding snapshot. Note that:   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can only increase the capacity of system volumes and data volumes, but cannot decrease the capacity.   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can add new data volumes, but you cannot delete the data volumes contained in the whole image.   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">On the "Basic configuration" page and the "Confirm" page, you can view the data volume snapshot information of the whole image.   </div>
   


</Tab>
</Tabs>


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations

After you purchase an instance, refer to [Subsequent operations](https://docs.byteplus.com/en/docs/ecs/What-to-do-next) to learn how to use ECS instances.
