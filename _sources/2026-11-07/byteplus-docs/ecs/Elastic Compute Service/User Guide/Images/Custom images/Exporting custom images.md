---
title: "Exporting custom images"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Exporting-custom-images"
---

After you create a custom image, you can export the image to a TOS bucket in the same region and download the image to a local device. This topic describes how to export custom images and the related usage notes.

<span id=".5pON5L2c6K-05piO"></span>
## Usage notes


|**Preparations** ||
|---|---|
|Dependent features |TOS is required to export custom images. Make sure that:<br><br><br>* You have activated TOS. [What is TOS?](https://docs.byteplus.com/en/docs/tos/docs-what-is-tos).<br><br>* A bucket is available in the region where the custom image is located. Otherwise, create a bucket in the region. For more information, see [Creating buckets](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket). |
|Permission |The first time you export a custom image to a TOS bucket, you must authorize ECS to access your TOS object. For more information, see [Confirming authorization](https://console.byteplus.com/iam/service/attach_role/?ServiceName=ecs). |
|**Export restrictions** ||
|Source image |* You cannot export commercial images, such as commercial images for Windows Server and Red Hat Enterprise Linux.<br><br>* When you export a system volume image, the system volume capacity can not exceed 1 TiB. When you export a whole image, there are no capacity restrictions on system volume and data volume.<br><br>* During the export process, the image status remains **Available**. Under such circumstances, you can still use the image to create instances, share the image, and change the operating system. However, you cannot delete the image. After the export task is completed, you can delete the image. |
|Image file export |* The exported image file is in QCOW2 format. Other formats are not supported.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">You may fail to start the image file on other platforms.   </div><br>   <br><br>* The image file will be saved in the selected TOS bucket.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If a file with the same name already exists in the bucket, the file is overwritten by the exported file.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Naming rules for image files generated in the TOS bucket:   </div><br>   <br><br>      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">System volume image: <code>Custom prefix_Image ID_system.qcow2</code>   </div><br>   <br><br>      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Data volume image: <code>Custom prefix_Image ID_data.qcow2</code>   </div><br>    |
|Export task |* After you start an export task, you cannot cancel the task. You cannot initiate multiple tasks to export the same image at the same time.<br><br>* The time required to export an image depends on the size of the custom image file and the number of concurrent export tasks. |


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Image console](https://console.byteplus.com/image/images). 

2. In the top menu bar, select the region and project where the target custom image is located.

3. On the image list page, select the "Custom Image" tab.

4. Click the "..." button in the "Actions" column on the right of the target image and select "Export Image."

5. In the "Export Image" pop\-up window, confirm the image information and configure the parameters described in the following table.

   
   |**Parameter​**  |**Description** |
   |---|---|
   |TOS Bucket Address |Select a TOS Bucket in the same region as the custom image. |
   |Image File Name Prefix |The custom prefix for the name of the exported file. Naming rules:<br><br><br>* Composed of digits or letters.<br><br>* The prefix must be 1 to 30 characters in length. |
   

6. Click the "Export" button to submit the export task.


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations

<span id="82EETdlx"></span>
### View export details


1. Log in to the [ECS console](https://console.byteplus.com/ecs/).

2. In the left\-side navigation pane, click "Maintenance & Monitoring \> Executions".

3. In the top menu bar, select the region and project where the target custom image is located.

4. Search for the target task by "Execution ID" or "Resource ID," and click the target task name to view the basic information of the task, including the task ID, name, status, progress, and start and end time.


<span id="dM3ASdK0"></span>
### Download image files

After an image is exported to the TOS bucket you specified, an image file is generated in the bucket. You can download the image file to the default download path of your browser and use the downloaded image file. For details, refer to [Downloading files](https://docs.byteplus.com/en/docs/tos/docs-downloading-a-file).

<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [ExportImage](https://docs.byteplus.com/en/docs/ecs/ExportImage)

* [DescribeTasks](https://docs.byteplus.com/en/docs/ecs/DescribeTasks)
