---
title: "Image import overview"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Import_image_overview"
---

You can create an image file for a local server or an ECS instance from other cloud vendors, and import the image file into the BytePlus platform as a custom image.

This topic describes how to import an image, helping you understand how to migrate an image file to the cloud by uploading the image.

<span id="uFO8K4gu"></span>
## Import a Linux image

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3cfb40866aff060ddc77605772bfb555.png) </span>


1. Learn about the requirements and limits for importing Linux images. For more information, see [Image import requirements](https://docs.byteplus.com/en/docs/ecs/Requirements).

2. Configure an image.

   1. Modify the /etc/fstab file of the image to comment out or delete the data volume directory information. [Learn more](https://docs.byteplus.com/en/docs/ecs/Creating-Linux-images#.56ys5LiJ5q2l77ya5L-u5pS56Jma5ouf5py65paH5Lu2).

   2. Install and configure Cloud\-init. [Learn more](https://docs.byteplus.com/en/docs/ecs/Creating-Linux-images#.56ys5Zub5q2l77ya5Zyo6Jma5ouf5py65LiK5a6J6KOFQ2xvdWQtaW5pdA==).

   3. Install the Virtio driver. [Learn more](https://docs.byteplus.com/en/docs/ecs/Creating-Linux-images#5VeObo5n).

   4. Install the password reset plugin and the blk\-none tool. [Learn more](https://docs.byteplus.com/en/docs/ecs/Creating-Linux-images#.56ys5YWt5q2l77ya5Zyo6Jma5ouf5py65Lit5a6J6KOF5o-S5Lu2).

   5. Check whether the image complies with the BytePlus image specifications. [Learn more](https://docs.byteplus.com/en/docs/ecs/Creating-Linux-images#.56ys5YWr5q2l77ya5qOA5rWL6ZWc5YOP6KeE6IyD).

   6. Obtain the image file and convert the format of the image file. [Learn more](https://docs.byteplus.com/en/docs/ecs/Creating-Linux-images#.56ys5Lmd5q2l77ya5a-85Ye66ZWc5YOP).

3. Import the image file to generate a custom image. [Learn more](https://docs.byteplus.com/en/docs/ecs/Importing-custom-images-1).

4. Subsequently, you can [use the image to purchase an ECS instance](https://docs.byteplus.com/en/docs/ecs/Buying-ECS-instances-with-custom-images) or [change the operating system of an ECS instance](https://docs.byteplus.com/en/docs/ecs/Changing-OS).


<span id="O1oCSjTk"></span>
## Import a Windows image

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cd6e1f4ef610df8c638caf1149c1c744.png) </span>


1. Learn about the requirements and limits for importing Windows images. For more information, see [Image import requirements](https://docs.byteplus.com/en/docs/6522/82025#windows-server%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F%E9%95%9C%E5%83%8F).

2. Configure an image.

   1. Install and configure Cloudbase\-init in the image. [Learn more.](https://docs.byteplus.com/en/docs/ecs/Creating-Windows-images#.56ys5LiJ5q2l77ya5Zyo6Jma5ouf5py65LiK5a6J6KOFQ2xvdWRiYXNlLWluaXQ=)

   2. Install the Virtio\-Win driver. [Learn more.](https://docs.byteplus.com/en/docs/ecs/Creating-Windows-images#.56ys5LqU5q2l77ya5Zyo6Jma5ouf5py65LiK5a6J6KOFVmlydGlv6amx5Yqo)

   3. Install the password reset plugin. [Learn more.](https://docs.byteplus.com/en/docs/ecs/Creating-Windows-images#.56ys5YWt5q2l77ya5a6J6KOF5o-S5Lu2)

   4. Obtain the script for activating the operating system. [Learn more](https://docs.byteplus.com/en/docs/ecs/Creating-Windows-images#.56ys5LiD5q2l77ya6I635Y-W5r-A5rS76ISa5pys).

   5. Run Sysprep to delete specific content from the image. [Learn more.](https://docs.byteplus.com/en/docs/ecs/Creating-Windows-images#.56ys5Zub5q2l77ya5omn6KGMU3lzcHJlcA==)

   6. Obtain the image file and convert the format of the image file. [Learn more.](https://docs.byteplus.com/en/docs/ecs/Creating-Windows-images#.56ys5Lmd5q2l77ya5a-85Ye66ZWc5YOP)

3. Import the image file to generate a custom image. [Learn more.](https://docs.byteplus.com/en/docs/ecs/Importing-custom-images-1)

4. Subsequently, you can [use the image to purchase an ECS instance](https://docs.byteplus.com/en/docs/ecs/Buying-ECS-instances-with-custom-images) or [change the operating system of an ECS instance](https://docs.byteplus.com/en/docs/ecs/Changing-OS).
