---
title: "Importing custom images"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Importing-custom-images-1"
---

This topic describes how to import a custom image. After you import a custom image, you can use the custom image to create instances.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


|Item |Description |
|---|---|
|Dependent features |TOS and the snapshot feature are required to import a custom image. Make sure that [Torch Object Storage](https://docs.byteplus.com/en/docs/tos/docs-what-is-tos) is activated and the [snapshot](https://docs.byteplus.com/en/docs/ecs/Overview-of-snapshots) feature is enabled. |
|Permission |The first time you export a custom image to a TOS bucket, you must authorize ECS to access your TOS object. [Confirm authorization](https://console.byteplus.com/iam/service/attach_role/?ServiceName=ecs). |
|Image file |You must create an image file that meets the requirements on your local device. For more information, see [Creating Linux images](https://docs.byteplus.com/en/docs/ecs/Creating-Linux-images) and [Creating Windows images](https://docs.byteplus.com/en/docs/ecs/Creating-Windows-images). Image files must meet the following requirements:<br><br><br>* The file format for image files must be QCOW2, RAW, VHD, or VMDK.<br><br>* Image file size:<br><br>   * The size of a single image file must not exceed 2 TiB.<br><br>   * The total size of the system volume image file and data volume image file included in the whole image must not exceed 32 TiB.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If the limit is exceeded, you can migrate data to a custom image by using the <a href="https://docs.byteplus.com/en/docs/smc/What-is-Server-Migration-Center">SMC</a>.</div><br> |


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5LiK5Lyg6ZWc5YOP5paH5Lu2"></span>
### Step 1: Upload an image file

Before you import an image, upload the image file to TOS and authorize the backend service to access the object address in TOS. 

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To import a whole image containing the system volume and data volume, follow the instructions in this step to separately upload the image file for the system volume and data volume to TOS.</div>



1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the top menu bar, select the project where the target bucket is located.

3. Click the name of the target bucket where you want to store the image file to go to the bucket details page.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The region of the target bucket must be the same as the region where you want to import the image. You can also create a new bucket based on your business requirements. For more information, see <a href="https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket">Creating buckets</a>.   </div>
   

4. Upload the image file.

   1. In the left\-side navigation pane, click "Objects".

   2. Click the "Upload file" button to go to the configuration page for uploading a file.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f20b63bd4e6e3e4c3950b43858d35526.png) </span>

   4. According to the [file upload](https://docs.byteplus.com/en/docs/tos/docs-uploading-a-file) guide, select the image file to be uploaded and click the "Upload" button to start the upload process.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_225d95cc281e23b8f361e53f1a783960.png) </span>

5. Obtain the image file URL.

   1. After the upload is complete, click the "Details" button in the "Actions" column to the right of the uploaded file to go to the file details page.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2ed427b76513147b8b1e2bdaf13d43ce.png) </span>

   2. Click the copy button to the right of the URL to obtain the URL of the file. URL format: `https://{bucket name}.{TOS domain name}/{object path}`.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_78393cc10caaaeb775dc94215893974b.png) </span>


<span id="XmPj31e3"></span>
### Step 2: Import the image


1. Log in to the [Image console](https://console.byteplus.com/image/images).

1. In the top menu bar, select the region where you want to import the generated custom image.

2. Select the "Custom Image" tab.

3.  **(Optional)**  Click to activate, indicating that you are aware and agree BytePlus Customer Agreement, Service Specific Terms and SLA for ECS.

4. After you enable the snapshot service, click the "Import image" button and configure the parameters in the following table.

   
   |Parameter​ |Description |Sample value |
   |---|---|---|
   |Region |The region where the image will be located after being imported.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">After you select the region, the image can be used only for resources within this region and cannot be migrated.</div><br><br><br>* <div data-tips="true" data-tips-type="default">To change the region, select the desired region in the top menu bar.</div><br> |Asia Pacific (Johor) |
   |Image file URL |Enter the URL of the system volume image you obtained from the [image file upload](https://docs.byteplus.com/en/docs/ecs/Importing-custom-images-1#.5q2l6aqk5LiA77ya5LiK5Lyg6ZWc5YOP5paH5Lu2) step. |https://test\-test.tos\-ap\-southeast\-1.bytepluses.com/ubuntu.qcow2 |
   |Image name |Specify the name of the image. |image\-1 |
   |Operating systems |Select the platform and version of the image to upload. |CentOS\-8.3 |
   |Volume configuration (optional) |When you import an image that contains a data volume, you must enable this option and configure the data volume information.<br><br><br>1. Select "Configuration Volumes attribute".<br><br>   > The parameters of the system volume are automatically configured and the system volume is automatically mounted to the `/vda` directory. You do not need to modify the configurations.   <br>   <br><br>2. Click the "Add Storage Volume" button and enter the URL of the data volume image obtained from the [image file upload](https://docs.byteplus.com/en/docs/ecs/Importing-custom-images-1#.5q2l6aqk5LiA77ya5LiK5Lyg6ZWc5YOP5paH5Lu2) step.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">A maximum of 15 data volumes can be added.   </div><br>    |\- |
   |Architecture |Select the image architecture. `x86_64` and `arm64` are supported. |x86_64 |
   |Boot mode |Select the boot mode for the image. `BIOS` and `UEFI` are supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Make sure that the selected boot mode matches the boot mode supported by the image. Otherwise, the ECS instance created by using the image cannot start as expected.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Elastic Bare Metal (EBM)\-type ECS instances only support the <code>UEFI</code> boot mode. The default boot mode of the image that you use to create ECS instances of types other than the EBM type is <code>UEFI</code>.</div><br> |UEFI |
   |License types |Select the license type to activate the operating system. Value:<br><br><br>* BytePlus official license: Activate the operating system by using the license officially provided by the platform.<br><br>* BYOL: Activate the operating system by using the license included in your image.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When you import Red Hat Enterprise Linux or SUSE Linux Enterprise Server images, only "BYOL" is supported.</div><br> |BytePlus official license |
   |Image detection (optional) |Specify whether to enable the image check feature. This feature checks whether your custom image meets the image requirements of the platform. This helps ensure that the ECS instances created by using the custom image run as expected. [Learn more](https://docs.byteplus.com/en/docs/ecs/Image_Detection_Overview).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The image detection process starts after a custom image is created. Interrupted checks or failed checks do not block the creation or import process of the custom image.</div><br> |\- |
   |Project (optional) |Select the project to which the custom image belongs.<br><br><br>* After you select a project, the imported custom image can be viewed and used only by users with permissions on the project.<br><br>* If no project is available in the drop\-down list, you can follow the guidelines to create a project. For more information, see [Creating projects](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Management#creating-project).<br><br>* If you want to change the project to which the image belongs after the image is imported, refer to [Project resource management](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Resource_Management).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">A project is a collection of resources. You can add custom images to projects and classify and manage custom images by project. Additionally, you can control the permissions of users and roles within each project on custom images. <a href="https://docs.byteplus.com/en/docs/resourcemanagement/Project_Overview">Project overview</a>.</div><br> |projectA |
   |Tag (optional) |A tag is a key\-value pair used to identify cloud resources. Tags help you categorize cloud resources with similar attributes based on different dimensions, such as purpose, owner, or environment. This allows you to search and aggregate your cloud resources for easy management.<br><br>Click the " **+** " icon and enter the tag key and tag value to add a tag to the image. For more information, refer to [Managing tags](https://docs.byteplus.com/en/docs/ecs/Tag-overview). |Key:Value |
   

6. Click the "Import" button to create an image import task. The image status will change to **Creating**, and you can view the import progress below the status.


<span id=".5q2l6aqk5LiJ77ya5p-l55yL5a-85YWl57uT5p6c"></span>
### Step 3: View the import result


1. Log in to the [Image console](https://console.byteplus.com/image/images). 

2. In the top menu bar, select the region where the image that you imported is located.

3. Select the "Custom Image" tab.

4. View the status of the imported image.

   
   |Status |Description |
   |---|---|
   |Creating |The image is being created. Wait until the image is created. |
   |Available |The image has been successfully created and no exceptions are found. The image can be used as expected. |
   |Error |An error occurred on the image. The image cannot be used as expected. |
   


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [ImportImage](https://docs.byteplus.com/en/docs/ecs/ImportImage)

* [ModifyImageAttribute](https://docs.byteplus.com/en/docs/ecs/ModifyImageAttribute)
