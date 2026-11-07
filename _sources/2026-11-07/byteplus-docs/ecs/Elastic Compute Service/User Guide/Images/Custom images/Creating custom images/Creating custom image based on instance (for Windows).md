---
title: "Creating custom image based on instance (for Windows)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Creating-custom-images-from-a-Windows-instance"
---

This topic describes how to create a system volume image or whole image based on a Windows instance.

<span id=".5ZCN6K-N6Kej6YeK"></span>
## Terms


|Term |Description |
|---|---|
|System volume image |A custom image that contains only system volume data. |
|Whole image |A custom image that contains data from the system volume and data volumes. During the image creation process, the platform creates a separate snapshot for each volume attached to the instance, including the system volume. The collection of these snapshots constitutes a whole image. |


<span id=".5pON5L2c6K-05piO"></span>
## Operation instructions


|**Preparations** ||
|---|---|
|Instance |You have purchased an ECS instance for creating a custom image. For more information, see [Purchasing ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances). |
|Dependent feature |The snapshot feature is enabled to store custom image data. For more information, see [Snapshot](https://docs.byteplus.com/en/docs/ecs/Overview-of-snapshots). |
|**License type** ||
|If the license type of the operating system on your instance is Bring Your Own License (BYOL), the license type of any custom image created from the instance is also BYOL. You need to use your own license to activate the operating system. ||
|**Limits for different image types** ||
|System volume image |By default, only a custom image of your system volume is created. |
|Whole image |* The total amount of data on the system volume and data volumes must not exceed 32 TiB.<br><br>* You can create a whole image only based on the combination of the system volume and all data volumes of an instance.<br><br>* You cannot create a whole image for an instance equipped with a local disk or a PTSSD volume.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the specification details of the instance include local storage information, the instance is equipped with a local disk. For example, the <a href="https://docs.byteplus.com/en/docs/ecs/Local-SSD-based#8IH6RHiz">Local\-SSD i3s</a> instance type falls into this category. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types">Instance type overview</a>.   </div><br>   <br><br>* You cannot export a whole image or use a whole image to change the operating system. |
|**Limits on various volume types** ||
|PTSSD volume |If the ECS instance for which you want to create a custom image is mounted with a PTSSD volume:<br><br><br>* Before you create an image, [stop the instance](https://docs.byteplus.com/en/docs/ecs/Stopping-instances) first. Otherwise, you cannot create an image.<br><br>* During the creation process, you cannot change the instance status. For example, you cannot start, stop, or restart the instance. Wait until the custom image is created before you perform operations on the instance. |
|ESSD volume |If the ECS instance for which you want to create a custom image is mounted with an ESSD volume:<br><br><br>* Before you create a custom image, you do not need to stop the instance. For volume performance metrics, refer to [Volume specifications](https://docs.byteplus.com/en/docs/ecs/Volume-specifications).<br><br>* During the creation process, you cannot change the instance status. For example, you cannot start, stop, or restart the instance. Wait until the custom image is created before you perform operations on the instance.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you create a custom image for a running instance, some real\-time data may not be saved to the image file. To ensure data integrity, we recommend that you stop the instance before you create an image.   </div><br>   <br><br>* During the creation process, the instance status does not change, and you can start, stop, or restart the instance. |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Do not modify the kernel. Otherwise, the custom image you create may not work as expected.</div>


* <div data-tips="true" data-tips-type="warning">If the available space of the system volume is insufficient, you may fail to create the custom image.</div>



<span id=".5q2l6aqk5LiA77ya5a6J6KOF5Liq5oCn5YyW6L2v5Lu277yI5Y-v6YCJ77yJ"></span>
## Step 1: Install software (optional)


1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance)

2. Install software on the target instance based on your business requirements. For example, you can install JDK or a Linux graphical desktop.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When you create a non\-whole image, you can create a custom image only for your system volume. Therefore, data stored on the data volume is not contained in the image. Install software on the system volume.</div>


<span id="cIjCcrGS"></span>
## Step 2: Install plugins

To reset, associate, and disassociate passwords, you must install the password plugin for the custom image you create. Otherwise, the image may not work as expected. For more information, see [Installing the password plugin](https://docs.byteplus.com/en/docs/ecs/Installing-the-password-plug-in).

You can also install the CloudMonitor plugin for custom images. This allows you to monitor an instance from within the instance and obtain deeper, more accurate information about the running status of the instance. For more information, see [Installing the plugin](https://docs.byteplus.com/en/docs/cloudmonitor/Installing-an-agent).

<span id=".5q2l6aqk5LqM77ya5riF55CG572R5Y2h5L-h5oGv"></span>
## Step 3: Clear the network interface information

You need to clear the existing network interface information. Otherwise, information such as the hostname and password cannot be injected into ECS instances created by using the custom image.


1. Click the Windows icon and click "Windows System \> Run".

2. Enter `cmd` and click the "OK" button to open the command line.

3. Execute the `ipconfig /release` command to release the existing IP address.


<span id=".5q2l6aqk5Zub77ya6L-Q6KGMU3lzcHJlcA=="></span>
## Step 4: Run Sysprep

You need to use Sysprep to delete specific information from the image so that the image can be used on different devices. For more information, see [Sysprep (system preparation) overview](https://learn.microsoft.com/zh-cn/windows-hardware/manufacture/desktop/sysprep--system-preparation--overview?view=windows-11).


* If you use the public image provided by the platform to create a custom image, execute the following command in the CMD command prompt. For information about the public image versions, see [Image release notes](https://docs.byteplus.com/en/docs/ecs/Image-release-notes) .

   ```Plain Text
   reg delete "HKLM\SOFTWARE\Cloudbase Solutions"
   net stop wuauserv
   C:\Windows\System32\Sysprep\sysprep.exe /shutdown /generalize /quiet /oobe /unattend:C:\Windows\sysprep-unattend.xml
   ```
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After you execute the command, the instance enters the generalization process:   </div>
   

      1. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Delete information specific to the instance, including but not limited to the Security Identifier (SID), hostname, and password. Applications and related data are retained.   </div>
   

      2. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Uninstall (but do not delete) drivers specific to the instance.   </div>
   

      3. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Specify that the content in the unattended answer file can be added to the existing installation.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After generalization is complete, the instance automatically shuts down.   </div>
   

* If you use the public image not provided by the platform to create a custom image, execute the following command in the CMD command prompt.

   ```Plain Text
   %WINDIR%\system32\sysprep\sysprep.exe /generalize /shutdown /oobe
   ```
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After you execute the command, the instance enters the generalization process:   </div>
   

      1. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Delete information specific to the instance, including but not limited to the Security Identifier (SID), hostname, and password. Applications and related data are retained.   </div>
   

      2. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Uninstall (but do not delete) drivers specific to the instance.   </div>
   

      3. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Specify that the instance starts in Out\-of\-Box Experience (OOBE) mode.   </div>
   

      4. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Specify that the content in the unattended answer file can be added to the existing installation.   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After generalization is complete, the instance automatically shuts down.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Cloudbase\-init runs after the OOBE process is complete, the password you create during the OOBE process is overwritten by the login password specified in the configuration file. After you create an ECS instance by using the image, use the login password you create during instance creation, rather than the password created during the OOBE process.   </div>
   


<span id=".5q2l6aqk5LqU77ya5YGc5q2i5a6e5L6L"></span>
## Step 5: Stop the instance

Stop the target instance. For more information, see [Stopping instances](https://docs.byteplus.com/en/docs/ecs/Stopping-instances).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you use a custom image created based on an ESSD volume or you have run Sysprep, you do not need to stop the instance and can skip this step.</div>


<span id=".5q2l6aqk5YWt77ya6YCa6L-H5a6e5L6L5Yib5bu66Ieq5a6a5LmJ6ZWc5YOP"></span>
## Step 6: Create a custom image based on the instance


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. On the left side of the top menu bar, select the project and region where the instance is located.

3. In the left\-side navigation pane, click "Instances & Images \> Instances". In the left\-side navigation pane, select "Elastic Compute Service (ECS) \> Instances".

4. Click "... \> Volumes & Image \> Create custom image" in the "Actions" column on the right side of the target instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the snapshot feature is not enabled, click "... \> Volumes & Image \> Create custom image" in the "Actions" column on the right side of the target instance. In the pop\-up window, check the box next to "Click to activate, indicating that you are aware and agree Service\-Specific Terms for BytePlus Elastic Compute Service", and then click the "Activate" button.   </div>
   

5. In the pop\-up window, configure the following parameters.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Image name |Specify the name of the custom image. |CentOS7.9\-P |
   |Project (optional) |Select the project to which the custom image belongs.<br><br><br>* After you select a project, the created custom image can be viewed and used only by users with permissions on the project.<br><br>* If no project is available in the drop\-down list, you can follow the guidelines to create a project. For more information, see [Creating projects](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Management#creating-project).<br><br>* If you want to change the project to which the image belongs after the image is created, refer to [Project resource management](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Resource_Management).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">A project is a collection of resources. You can add custom images to projects and classify and manage custom images by project. Additionally, you can control the permissions of users and roles within each project on custom images. <a href="https://docs.byteplus.com/en/docs/resourcemanagement/Project_Overview">Learn more</a>.</div><br> |projectA |
   |Tag (optional) |A tag is a key\-value pair used to identify cloud resources. Tags help you categorize cloud resources with similar attributes based on different dimensions, such as purpose, owner, or environment. This allows you to search and aggregate your cloud resources for easy management.<br><br>Click the  **+**  icon and enter the tag key and tag value to add tags to the image. For more information, see [Learn more](https://docs.byteplus.com/en/docs/resourcemanagement/Tag_Overview). |Key:Value |
   |Production scope (optional) |Select the "Creating Whole Images" option based on your business requirements to specify whether to create a custom image that contains data from the system volume and all data volumes.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the target instance is mounted with a data volume, a whole image is created by default. You can also unselect the "Creating Whole Images" option to create a custom image that contains only system volume data.</div><br> |\- |
   

7. Click the "Create" button and wait until the custom image is created. The time required to create the custom image varies based on the actual amount of data in the volume.

8. You can view the progress of creating a custom image on the Custom Image tab or the Executions page.

   * In the left\-side navigation pane, click "Instances & Images \> Images", and then select the "Custom Image" tab to view the creation progress.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_851ccd6abc81b12e2efa3566960e6691.png) </span>

   * In the left\-side navigation pane, click "Maintenance & Monitoring \> Executions", and view the creation progress on the Executions page.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_30f7d4a4dae7d6fd140aaeefa8edf4b0.png) </span>


<span id=".5pON5L2c57uT5p6c"></span>
## Operation results


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the top menu bar, select the region and project where the target custom image is located.

3. Select the "Custom Image" tab.

4. If the status of the target image is **Available** in the "State" column, the custom image is created.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b4a520f28f1efa876efd12ac4f0d154c.png) </span>

5. You can also click the image name to go to the image details page, select the "Associative snapshot" tab, and view the IDs of the snapshots associated with the volumes in the image, the volume types, and the capacity of the volumes. For more information, see [Snapshot overview](https://docs.byteplus.com/en/docs/ecs/Overview-of-snapshots).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e673725038e4a50a63a4e17f8ef05872.png) </span>


<span id="CmLZMWCm"></span>
## Related documents


* [CreateImage - Creates images](https://docs.byteplus.com/en/docs/ecs/CreateImage)

* [DetectImage - Detects images](https://docs.byteplus.com/en/docs/ecs/DetectImage)
