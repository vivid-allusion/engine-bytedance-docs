---
title: "Creating custom image based on instance (for Linux)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Creating-custom-images-from-a-Linux-instance"
---

This topic describes how to create a system volume image or whole image based on a Linux instance.

<span id=".5ZCN6K-N6Kej6YeK"></span>
## Terms


|Term |Notes |
|---|---|
|System volume image |A custom image that contains only system volume data. |
|Whole image |A custom image that contains data from the system volume and data volumes. During the image creation process, the platform creates a separate snapshot for each volume attached to the instance, including the system volume. The collection of these snapshots constitutes a whole image. |


<span id=".5pON5L2c6K-05piO"></span>
## Operation instructions


|**Preparations** ||
|---|---|
|Instance |You have purchased an ECS instance for creating a custom image. For more information, see [Purchasing ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances). |
|Dependent feature |The snapshot feature is enabled to store custom image data. For more information, see [Snapshot](https://docs.byteplus.com/en/docs/ecs/Overview-of-snapshots). |
|**Limits for different image types** ||
|System volume image |By default, only a custom image of your system volume is created. |
|Whole image |* The total amount of data on the system volume and data volumes must not exceed 32 TiB.<br><br>* You can create a whole image only based on the combination of the system volume and all data volumes of an instance.<br><br>* You cannot create a whole image for an instance equipped with a local disk or a PTSSD volume.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the specification details of the instance include local storage information, the instance is equipped with a local disk. For example, the <a href="https://docs.byteplus.com/en/docs/ecs/Local-SSD-based#8IH6RHiz">Local\-SSD i3s</a> instance type falls into this category.   </div><br>   <br><br>* You cannot export a whole image or use a whole image to change the operating system. |
|**Limits on various volume types** ||
|PTSSD volume |If the ECS instance for which you want to create a custom image is mounted with a PTSSD volume:<br><br><br>* Before you create an image, [stop the instance](https://docs.byteplus.com/en/docs/ecs/Stopping-instances) first. Otherwise, you cannot create an image.<br><br>* During the creation process, you cannot change the instance status. For example, you cannot start, stop, or restart the instance. Wait until the custom image is created before you perform operations on the instance. |
|ESSD volume |If the ECS instance for which you want to create a custom image is mounted with an ESSD volume:<br><br><br>* Before you create a custom image, you do not need to stop the instance. For volume performance metrics, refer to [Volume specifications](https://docs.byteplus.com/en/docs/ecs/Volume-specifications).<br><br>* During the creation process, you cannot change the instance status. For example, you cannot start, stop, or restart the instance. Wait until the custom image is created before you perform operations on the instance.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you create a custom image for a running instance, some real\-time data may not be saved to the image file. To ensure data integrity, we recommend that you stop the instance before you create an image.   </div><br>   <br><br>* During the creation process, the instance status does not change, and you can start, stop, or restart the instance. |


&nbsp;

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Do not modify the kernel. Otherwise, the custom image you create may not work as expected. </div>


* <div data-tips="true" data-tips-type="warning">If the available space of the system volume is insufficient, you may fail to create the custom image. </div>



<span id=".5q2l6aqk5LiA77ya5a6J6KOF5Liq5oCn5YyW6L2v5Lu277yI5Y-v6YCJ77yJ"></span>
## Step 1: Install software (optional)


1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance)

2. Install software on the target instance based on your business requirements. For example, you can install JDK or Oracle.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">When you create a non\-whole image, you can create a custom image only for your system volume. Therefore, data stored on the data volume is not contained in the image. Install software on the system volume.</div>


<span id=".5q2l6aqk5LqM77ya5riF6ZmkQ2xvdWQtSW5pdOmFjee9rg=="></span>
## Step 2: Clear the Cloud\-init configuration

Execute the following command to delete the /var/lib/cloud file. This way, the Cloud\-init configuration is cleared. If you do not delete the file, information such as the hostname and password cannot be injected into ECS instances created by using the custom image.

```Plain Text
rm -rf /var/lib/cloud
```


<span id=".5q2l6aqk5LiJ77ya5YGc5q2i5a6e5L6L"></span>
## Step 3: Stop the instance

Stop the target instance. For more information, see [Stopping instances](https://docs.byteplus.com/en/docs/ecs/Stopping-instances).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you use a custom image created based on an ESSD volume, you do not need to stop the instance and can skip this step.</div>


<span id=".5q2l6aqk5Zub77ya6YCa6L-H5a6e5L6L5Yib5bu66Ieq5a6a5LmJ6ZWc5YOP"></span>
## Step 4: Create a custom image based on the instance


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. On the left side of the top menu bar, select the project and region where the instance is located.

3. In the left\-side navigation pane, click "Instances & Images \> Instances". 

4. Click "... \> Volumes & Image \> Create custom image" in the "Actions" column on the right side of the target instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the snapshot feature is not enabled, click "... \> Volumes & Image \> Create custom image" in the "Actions" column on the right side of the target instance. In the pop\-up window, check the box next to "Click to activate, indicating that you are aware and agree Service\-Specific Terms for BytePlus Elastic Compute Service", and then click the "Activate" button.   </div>
   

5. In the pop\-up window, configure the following parameters.

   
   |Parameter​s |Description |Sample value |
   |---|---|---|
   |Image name |Specify the name of the custom image. |CentOS7.9\-P |
   |Project (optional) |Select the project to which the custom image belongs.<br><br><br>* After you select a project, the created custom image can be viewed and used only by users with permissions on the project.<br><br>* If no project is available in the drop\-down list, you can follow the guidelines to create a project. For more information, see [Creating projects](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Management#creating-project).<br><br>* If you want to change the project to which the image belongs after the image is created, refer to [Project resource management](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Resource_Management).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">A project is a collection of resources. You can add custom images to projects and classify and manage custom images by project. Additionally, you can control the permissions of users and roles within each project on custom images. <a href="https://docs.byteplus.com/en/docs/resourcemanagement/Project_Overview">Learn more</a>.</div><br> |projectA |
   |Image detection (optional) |Specifies whether to enable the image detection feature. This feature detects whether your custom image meets BytePlus image requirements. This helps ensure that the ECS instances created by using the custom image run as expected.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The image detection process starts after a custom image is created. Detection failures or failed detection does not block the creation or import process of the custom image. <a href="https://docs.byteplus.com/en/docs/ecs/Image_Detection_Overview">Learn more</a>.</div><br> |\- |
   |Tag (optional) |A tag is a key\-value pair used to identify cloud resources. Tags help you categorize cloud resources with similar attributes based on different dimensions, such as purpose, owner, or environment. This allows you to search and aggregate your cloud resources for easy management.<br><br>Click the  **+**  icon and enter the tag key and tag value to add tags to the image. For more information, refer to [Learn more](https://docs.byteplus.com/en/docs/resourcemanagement/Tag_Overview). |Key:Value |
   |Production scope (optional) |Select the "Creating Whole Images" option based on your business requirements to specify whether to create a custom image that contains data from the system volume and all data volumes.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the target instance is mounted with a data volume, a whole image is created by default. You can also clear the "Creating Whole Images" option to create a custom image that contains only system volume data.</div><br> |\- |
   

6. Click the "Create" button and wait until the custom image is created. The time required to create the custom image varies based on the actual amount of data in the volume.

7. You can view the progress of creating a custom image on the Custom Image page or the Executions page.

   * In the left\-side navigation pane, click "Instances & Images \> Images", and then select the "Custom Image" tab to view the creation progress.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2ccd7acd3d0702390d0e93e85010b742.png) </span>

   * In the left\-side navigation pane, click "Maintenance & Monitoring \> Executions", and view the creation progress on the Executions page.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e6eb217805d27452939e6cee2a654ead.png) </span>


<span id=".5pON5L2c57uT5p6c"></span>
## Operation results


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the top menu bar, select the region and project where the target custom image is located.

3. Select the "Custom Image" tab.

4. If the status of the target image is **Available** in the "State" column, the custom image is created.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_83918550ea1070b9cad433d85d72f081.png) </span>

5. You can also click the image name to go to the image details page, select the "Associative snapshot" tab, and view the IDs of the snapshots associated with the volumes in the image, the volume types, and the capacity of the volumes. For more information, see [Snapshot overview](https://docs.byteplus.com/en/docs/ecs/Overview-of-snapshots).


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [CreateImage - Creates images](https://docs.byteplus.com/en/docs/ecs/CreateImage)

* [DetectImage - Detects images](https://docs.byteplus.com/en/docs/ecs/DetectImage)
