---
title: "Creating custom images by using snapshots or snapshot consistency groups"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Create_Custom_Image_from_Snapshot_or_Snapshot_Group"
---

This topic describes how to create a custom image by using a snapshot or a snapshot consistency group.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The [snapshot](https://docs.byteplus.com/en/docs/ecs/Overview-of-snapshots) feature is enabled.

* The [system volume snapshot](https://docs.byteplus.com/en/docs/ecs/Create-a-snapshot) or the [snapshot consistency group is created](https://docs.byteplus.com/en/docs/ecs/Create-a-snapshot-consistency-group), and neither the snapshot nor the snapshot consistency group is associated with an image ID.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id="wr4uHZUf"></span>
### Create a custom image by using a snapshot

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">You can create a custom image by using a snapshot created exclusively for a system volume.</div>



1. Log in to the [ECS console](https://console.byteplus.com/ecs/region:ecs+ap-southeast-1/instance?).

2. In the left\-side navigation pane, click "Storage \> Snapshots".

3. In the top menu bar, select the project and region where the target snapshot is located.

4. Select the "Snapshots" tab.

5. Click "... \> Create custom image" in the "Actions" column of the target snapshot.

6. On the "Create custom image" page, check the snapshot information and configure the following parameters.

   
   |**Parameter​**  |**Description** |**Sample value** |
   |---|---|---|
   |Image name |Specify the name of the custom image. |CentOS7\-FromSnapshot |
   |Project (optional) |Select the project to which the custom image belongs.<br><br><br>* After you select a project, the created custom image can be viewed and used only by users with permissions on the project.<br><br>* If no project is available in the drop\-down list, you can follow the guidelines to create a project. For more information, see [Creating projects](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Management#creating-project).<br><br>* If you want to change the project to which the image belongs after the image is created, refer to [Project resource management](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Resource_Management).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">A project is a collection of resources. You can add custom images to projects and classify and manage custom images by project. Additionally, you can control the permissions of users and roles within each project on custom images. <a href="https://docs.byteplus.com/en/docs/resourcemanagement/Project_Overview">Learn more</a>.</div><br> |projectA |
   |Image detection (optional) |Specify whether to enable the image detection feature. This feature checks whether your custom image meets the image requirements of the platform. This helps ensure that the ECS instances created by using the custom image run as expected.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The image detection process starts after a custom image is created. Interrupted checks or failed checks do not block the creation or import process of the custom image. <a href="https://docs.byteplus.com/en/docs/ecs/Image_Detection_Overview">Learn more</a>.</div><br> |\- |
   |Tag (optional) |Click the  **+**  icon and enter the tag key and tag value to add tags to the image.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">A tag is a key\-value pair used to identify cloud resources. Tags help you categorize cloud resources with similar attributes based on different dimensions, such as purpose, owner, or environment. This allows you to search and aggregate your cloud resources for easy management. <a href="https://docs.byteplus.com/en/docs/resourcemanagement/Tag_Overview">Learn more</a>.</div><br> |Key:Value |
   

7. After you configure the parameters, click "Create custom image" to submit the image creation request.

8. You can view the progress of creating a custom image on the "Custom Image" tab or the "Executions" page.

   * In the left\-side navigation pane, click "Instances & Images \> Images", and then select the "Custom Image" tab to view the creation progress.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4824dcd926047ca3dc9887a19883ec3b.png) </span>

   * In the left\-side navigation pane, click "Maintenance & Monitoring \> Executions", and view the creation progress on the "Executions" page.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_65077a7973f6c2a09b060ea4a47f41e9.png) </span>


<span id="MrzgNM1H"></span>
### Create a custom image by using a snapshot consistency group


1. Log in to the [ECS console](https://console.byteplus.com/ecs/region:ecs+ap-southeast-1/instance?).

2. In the left\-side navigation pane, click "Storage \> Snapshots".

3. In the top menu bar, select the project and region where the target snapshot is located.

4. Select the "Snapshot Groups" tab.

5. Click the "Create custom image" button in the "Actions" column of the target snapshot consistency group.

6. On the "Create custom image" page, check the snapshot consistency group information and configure the following parameters.

   
   |**Parameter** |**Description** |**Sample value** |
   |---|---|---|
   |Image name |Specify the name of the custom image. |CentOS7\-FromSnapshotConsistencyGroup |
   |Project (optional) |Select the project to which the custom image belongs.<br><br><br>* After you select a project, the created custom image can be viewed and used only by users with permissions on the project.<br><br>* If no project is available in the drop\-down list, you can follow the guidelines to create a project. For more information, see [Creating projects](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Management#creating-project).<br><br>* If you want to change the project to which the image belongs after the image is created, refer to [Project resource management](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Resource_Management).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">A project is a collection of resources. You can add custom images to projects and classify and manage custom images by project. Additionally, you can control the permissions of users and roles within each project on custom images. <a href="https://docs.byteplus.com/en/docs/resourcemanagement/Project_Overview">Learn more</a>.</div><br> |projectA |
   |Image detection (optional) |Specifies whether to enable the image detection feature. This feature checks whether your custom image meets the image requirements of the platform. This helps ensure that the ECS instances created by using the custom image run as expected.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The image detection process starts after a custom image is created. Interrupted checks or failed checks do not block the creation or import process of the custom image. <a href="https://docs.byteplus.com/en/docs/ecs/Image_Detection_Overview">Learn more</a>.</div><br> |\- |
   |Tag (optional) |Click the  **+**  icon and enter the tag key and tag value to add tags to the image.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">A tag is a key\-value pair used to identify cloud resources. Tags help you categorize cloud resources with similar attributes based on different dimensions, such as purpose, owner, or environment. This allows you to search and aggregate your cloud resources for easy management. <a href="https://docs.byteplus.com/en/docs/resourcemanagement/Tag_Overview">Learn more</a>.</div><br> |Key:Value |
   |System volume only |Specify whether to use only the system volume snapshot in the snapshot consistency group to create the custom image. |\- |
   

7. After you configure the parameters, click "Create custom image" to submit the image creation request.

8. You can view the progress of creating a custom image on the "Custom Image" tab or the "Executions" page.

   * In the left\-side navigation pane, click "Instances & Images \> Images", and then select the "Custom Image" tab to view the creation progress.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5c47683c4d507cd1ec99c6a973baa142.png) </span>

   * In the left\-side navigation pane, click "Maintenance & Monitoring \> Executions", and view the creation progress on the Executions page.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_de1d9b0e0d971affa0ee78b24e02538d.png) </span>


<span id=".5pON5L2c57uT5p6c"></span>
## Operation results


1. Log in to the [ECS console](https://console.byteplus.com/ecs/region:ecs+ap-southeast-1/instance).

2. In the top menu bar, select the region and project where the target custom image is located.

3. Select the "Custom Image" tab.

4. If the status of the target image is **Available** in the "State" column, the custom image is created.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_83918550ea1070b9cad433d85d72f081.png) </span>

5. You can also click the image name to go to the image details page, select the "Associative snapshot" tab, and view the IDs of the snapshots associated with the volumes in the image, the volume types, and the capacity of the volumes. For information about the snapshot feature, see [Snapshot overview](https://docs.byteplus.com/en/docs/ecs/Overview-of-snapshots).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c2d28c91a18e288b3c6c3a75c589cf61.png) </span>
