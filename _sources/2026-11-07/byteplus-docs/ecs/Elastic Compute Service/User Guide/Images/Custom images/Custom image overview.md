---
title: "Custom image overview"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Custom_image_overview"
---

A custom image is an image that you create yourself by using an instance or a snapshot, or an image uploaded from your local device. A custom image is your private image. In addition to the operating system, you can pre\-install public applications or private applications in the image based on your business requirements. Custom images are applicable to scenarios where you need to redeploy systems with complex initialization or deploy servers with the same configuration multiple times.

This topic describes how to create and use a custom image.

<span id=".5rWB56iL5qaC6KeI"></span>
## Process overview

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cf113d8006ecf80a9c34b0ed30a46832.png) </span>

<span id=".55u45YWz5pON5L2c"></span>
## Related operations


|Operation |Description |Related documents |
|---|---|---|
|Importing custom images |You can create an image file based on a local server or an ECS instance from other cloud vendors, and import the image file into BytePlus as your custom image. |[Importing custom images](https://docs.byteplus.com/en/docs/ecs/Importing-custom-images) |
|Creating custom images |You can create a custom image based on an existing ECS instance or snapshot in the BytePlus console. |* [Creating custom images based on instances](https://docs.byteplus.com/en/docs/ecs/Creating-custom-images-from-a-Linux-instance)<br><br>* [Creating custom images based on snapshots or snapshot consistency groups](https://docs.byteplus.com/en/docs/ecs/Create_Custom_Image_from_Snapshot_or_Snapshot_Group) |
||You can use Tailor to create a BytePlus custom image based on the system volume of a local server or an ECS instance from other cloud vendors. |* [Using Tailor to create custom images](https://docs.byteplus.com/en/docs/ecs/Creating-custom-images-with-Tailor) |
|Copying custom images |You can copy a custom image in your account to another region. This allows you to deploy ECS instances **across regions**. |[Copying custom images](https://docs.byteplus.com/en/docs/ecs/Copying_custom_images) |
|Sharing images |You can share custom images that you create with other BytePlus accounts. This allows you to deploy ECS instances **across accounts**. |[Sharing or unsharing images](https://docs.byteplus.com/en/docs/ecs/Sharing-or-canceling-sharing-image) |
|Exporting custom images |After you create a custom image, you can export the image to a TOS bucket in the same region and download the image to a local device. |[Exporting custom images](https://docs.byteplus.com/en/docs/ecs/Exporting-custom-images) |
|Modifying custom image information |After you create a custom image, you can modify the name, description, tags, and boot mode of the custom image. |[Modifying custom image information](https://docs.byteplus.com/en/docs/ecs/Modifying-custom-image-information) |
|Deleting custom images |You can delete custom images that are no longer required. |[Deleting custom images](https://docs.byteplus.com/en/docs/ecs/Deleting-custom-images) |
|Viewing task information |You can view the progress and details of custom image creation, replication, import, and export tasks. |[Managing custom image tasks](https://docs.byteplus.com/en/docs/ecs/Managing-custom-image-tasks) |
