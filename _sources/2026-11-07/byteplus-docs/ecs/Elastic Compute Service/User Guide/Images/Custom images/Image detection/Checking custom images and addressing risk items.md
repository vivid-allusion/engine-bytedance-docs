---
title: "Checking custom images and addressing risk items"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Detect_Custom_Images"
---

This topic describes how to check custom images and address risk items based on the check report.

<span id=".5qOA5rWL6ZWc5YOP"></span>
## Check images

<span id=".5a-85YWl6ZWc5YOP5pe25qOA5rWL"></span>
### Check images during image import

When you import an image in the console, you can select "Execute detection after creation" to enable the image detection feature. For more information, see [Importing custom images](https://docs.byteplus.com/en/docs/ecs/Importing-custom-images-1).

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8d8a9553e4df3577a8eb080f54933bb1.png) </span>

<span id=".5Yib5bu66ZWc5YOP5pe25qOA5rWL"></span>
### Check images during image creation

When you create a custom image for an ECS instance in the console, you can select "Execute detection after creation" to enable the image detection feature. For more information, see [Creating custom images for instances](https://docs.byteplus.com/en/docs/ecs/Creating-custom-images-from-a-Linux-instance).

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ec587173b20da69c2be4d0c0d6ff4744.png) </span>

<span id=".6Ieq6KGM5byA5ZCv5qOA5rWL"></span>
### Manually enable image detection

For existing custom images, you can manually perform image detection based on your business requirements.


1. Log in to the [Image console](https://console.byteplus.com/image/images).

2. Select the "Custom Image" tab and locate the target image.

3. Click the "... \> Image detection" button in the "Actions" column on the right side of the target image.

4. In the pop\-up window, click "OK" to start image detection.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_84b1b57b5756fe48a06e82b74c3a3c4f.png) </span>

5. The custom image list page is automatically displayed and image detection starts.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1991b731ca1d46f7a5773f42f8dc8db.png) </span>

6. After the image detection is complete, you can click "View details" in the "Inspection results" column of the target image, and select the "Image detection result" tab to view the detailed report.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_47ee78beffd0a1848f1a471a58d83653.png) </span>


<span id=".5p-l55yL5qOA5rWL5oql5ZGK"></span>
## View a check report


1. Log in to the [Image console](https://console.byteplus.com/image/images).

2. Select the "Custom Image" tab.

3. You can hover the mouse over "Inspection completed" in the "Inspection results" column of the target image to view the result summary.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8c26d95d6bf8898005add85110035605.png) </span>

4. You can click "View details" in the "Inspection results" column of the target image, and select the "Image detection result" tab to view the detailed report.

   
   |Check result |Description |
   |---|---|
   |Risk item not found |No exceptions are found. |
   |Suggested optimization item |Issues that may affect instance running are found. We recommend that you optimize the image based on the instructions. |
   |Strongly recommend fixing item |Issues that affect instance running are found. You need to address the risk items based on the instructions to ensure that the instances work as expected. |
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2fc39c8d358fa7ddb1b8c48b7f4be6a6.png) </span>

5. For details of check items and description of risk severities, refer to [Check item description](https://docs.byteplus.com/en/docs/ecs/Detect_item_description).


<span id="4rVNzkOf"></span>
## Address risk items

If risk items that may affect the running of your instance are detected for your image, you can address the risk items of your image based on the check report.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">The One\-click repair feature is in Beta. If you need a trial, <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> or contact your account manager.</div>


* <div data-tips="true" data-tips-type="default">Currently, only some image issues can be addressed through one\-click repair. For issues of other severities, you need to manually address them. <a href="https://docs.byteplus.com/en/docs/ecs/Detect_item_description">Learn more</a>.</div>




<Tabs>
<Tab zoneid="AWgtj1LMxf" title="One-click repair">
<TabTitle>One-click repair</TabTitle>

1. Log in to the [Image console](https://console.byteplus.com/image/images).

2. Select the "Custom Image" tab.

3. Click the name of the target image to go to the image details page.

4. Select the "Image detection result" tab, and click the "one\-click repair" button.

5. In the pop\-up window, select the risk items that need to be addressed, and click "OK" to submit the repair request.

6. You can click "Task management" in the pop\-up window to view the repair progress.

7. After the repair task is complete, you can [initiate image detection](https://docs.byteplus.com/en/docs/ecs/Detect_Custom_Images#.6Ieq6KGM5byA5ZCv5qOA5rWL) again to confirm the repair result.


</Tab>
<Tab zoneid="HRJjAeW9v5" title="Manual repair">
<TabTitle>Manual repair</TabTitle>

1. In the custom image source, address the risk items according to the instructions in the check report. [Learn more](https://docs.byteplus.com/en/docs/ecs/Detect_Custom_Images#.5p-l55yL5qOA5rWL5oql5ZGK).

2. Create or import the custom image again and initiate image detection to verify whether the risk items are addressed. [Learn more](https://docs.byteplus.com/en/docs/ecs/Detect_Custom_Images#.5qOA5rWL6ZWc5YOP).


</Tab>
</Tabs>


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [CreateImage](https://docs.byteplus.com/en/docs/ecs/CreateImage)

* [ImportImage](https://docs.byteplus.com/en/docs/ecs/ImportImage)

* [DescribeImages](https://docs.byteplus.com/en/docs/ecs/DescribeImages)

* [DetectImage](https://docs.byteplus.com/en/docs/ecs/DetectImage)
