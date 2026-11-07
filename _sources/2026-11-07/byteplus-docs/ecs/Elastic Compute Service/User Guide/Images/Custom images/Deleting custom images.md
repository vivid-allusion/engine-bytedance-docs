---
title: "Deleting custom images"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Deleting-custom-images"
---

This topic describes how to delete a custom image that you create.

<span id=".5pON5L2c6K-05piO"></span>
## Usage notes


|Item |Description |
|---|---|
|Restrictions |* You cannot delete a shared image. You need to cancel all sharing relationships for the image before you can delete the image. [Learn more](https://docs.byteplus.com/en/docs/ecs/Sharing-or-canceling-sharing-image#.5Y-W5raI5YWx5Lqr6ZWc5YOP).<br><br>* You cannot delete a custom image that is being copied, created, or exported. You need to wait until the copy, creation, or export process is complete before you can delete the image. |
|Impact |After you delete an image:<br><br><br>* You can no longer use the image to purchase an instance or change the operating system of an instance.<br><br>* When you change the operating system of an instance created by using the image, you can only select other images.<br><br>* Instances created by using the image can still be used as expected. You are charged for using the instances. |


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Image console](https://console.byteplus.com/image/region:image+cn-beijing/images?projectName=default&tab=2). 

2. In the top menu bar, select the project and region to which the target image belongs.

3. Select the "Custom Image" tab.

4. Click "... \> Delete" in the "Actions" column to the right of the target image.

5. In the pop\-up window, select "Whether to delete the corresponding snapshot" based on your business requirements, and then click the "Delete" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0cbe707e18bfe391a12de47be44bc15f.png) </span>


<span id=".55u45YWz5paH5qGj"></span>
## Related document

[DeleteImages](https://docs.byteplus.com/en/docs/ecs/DeleteImages)
