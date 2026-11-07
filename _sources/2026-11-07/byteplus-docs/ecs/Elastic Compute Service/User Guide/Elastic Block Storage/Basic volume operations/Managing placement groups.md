---
title: "Managing placement groups"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Manage-placement-group"
---

A storage placement group is a policy that controls how volumes are distributed. Creating a placement group allows you to deploy volumes across different underlying storage clusters. This achieves physical isolation of volumes, improving disaster recovery and high availability for your business. This topic describes how to create placement groups and anti\-affinity volumes, as well as the necessary procedures.

<span id="K5U6DfME"></span>
## Background information

To improve data availability and disaster recovery, highly available databases and critical business systems require data to be stored in isolated and independent clusters. This prevents a single cluster failure from affecting all business operations. EBS provides the placement group feature to address this scenario. You can designate an availability zone and create multiple sub\-placement groups for a placement group. When creating a volume, you can then select the placement group and its sub\-placement groups. Based on metrics such as cluster health and load, the system deploys volumes with different sub\-placement group numbers to different clusters, thereby achieving data isolation and protection.


* Placement group: A placement group manages multiple sub\-placement groups.

* Sub\-placement group: A sub\-placement group maps to one or more clusters. Based on the placement group and sub\-placement group numbers, EBS creates volumes in the corresponding clusters. This ensures that volumes with different sub\-placement group numbers are deployed in different clusters. If there are fewer sub\-placement groups than clusters, and if a particular cluster is heavily loaded, the system will schedule volume creation in other clusters. In this case, a single sub\-placement group maps to multiple clusters.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e7ff71f7af9f7ce820773ab7454e6341.png) </span>

&nbsp;

<span id="hq0v9T9r"></span>
## Notes

The number of clusters in the availability zone where a placement group resides may decrease when online resources are scaled down or during machine maintenance. When the number of sub\-placement groups exceeds the number of clusters, and there are insufficient cluster resources, EBS prioritizes successfully creating the volume. Consequently, the volume may be created without anti\-affinity.

<span id="rwXUhTxM"></span>
## Step 1: Create a placement group


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left navigation pane, select "Storage \> Placement group".

3. In the top menu bar, select the project and region in which you want to create a placement group.

4. On the "Placement group" page, click "Create placement group".

5. In the "Create placement group" dialog, set the following parameters.

   
   |Parameter |Required |Description |
   |---|---|---|
   |Name |Yes |Enter a name for your placement group. The placement group name must:<br><br><br>* Start with a Chinese character, a letter (case‑sensitive) or an underscore (_).<br><br>* Contain only Chinese characters, letters (case‑sensitive), numbers, periods (.), underscores (_), or hyphens (\-).<br><br>* Be between 1 and 128 characters long. |
   |Description |No |Provide additional information for your placement group. |
   |Availability zone |Yes |Select the available zone for your placement group. |
   |Sub placement groups quantity |Yes |Specify the number of sub\-placement groups you want to create. The valid range is 2 to 10. After the number of sub\-placement groups is specified, the system automatically assigns sequential numbers to them, starting at 1 and ending with the total number of groups. |
   |Auto assign sub placement groups |No |Specify whether to enable the automatic assignment of a sub\-placement group to volumes. When this option is enabled, you only need to specify the placement group when creating a volume. The system will then automatically assign a sub\-placement group.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If auto\-assignment is enabled and you specify a sub\-placement group number when creating a volume, the system will automatically assign a sub\-placement group. The specified number will be ignored.</div><br> |
   

6. Once you have finished configuring, click "Create".


<span id="j7EIepov"></span>
## Step 2: Create an volume with anti\-affinity enabled


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left navigation pane, select "Storage \> Volumes".

3. In the top menu bar, select the project and region in which you want to create a volume.

4. On the "Volumes" tab, click "Create volume".

5. On the "Create Volume" page, configure basic information, storage specifications, placement group, and other parameters for the volume.

   The following describes only the parameters related to placement groups. For more information about other parameters, see [Creating a Volume](https://docs.byteplus.com/en/docs/ecs/Create-a-volume).

   
   |Parameter |Description |
   |---|---|
   |Region and availability zone |Select the region and availability zone for your volume.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">A placement group is limited to the availability zone in which it was created and does not support cross\-zone resource management. When creating a volume and associating it with a placement group, select the same region and availability zone as the group.</div><br> |
   |Placement group |Select a storage placement group. |
   |Child placement group |Select a sub\-placement group number. The system deploys volumes with different sub\-placement group numbers across different clusters, depending on metrics such as cluster health and load.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Each sub\-placement group can host up to 200 volumes.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Once a volume is bound to a sub\-placement group, the binding cannot be changed.</div><br> |
   

5. After you have finished configuring, click "Confirm order".

6. After confirming that the volume configuration and number of volumes are correct, as well as the associated costs, check the box that says, "I have read and agree to the Elastic Compute Service Terms of Service". Then, click "Create volume" to submit your order.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can also create a volume on the "Placement group" page. Steps:</div>


<div data-tips="true" data-tips-type="default">Log in to the <a href="https://console.byteplus.com/ecs/instance">ECS console</a>. In the left navigation pane, select "Storage \> Placement group". On the "Placement group" page, click "Create volume" in the "Actions" column of a placement group. Follow the prompts to create the volume.</div>


<span id="JS6YcgmU"></span>
## Related operations


<Tabs>
<Tab zoneid="fe60mHBESd" title="View basic information about a placement group">
<TabTitle>View basic information about a placement group</TabTitle>

1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left navigation pane, select "Storage \> Placement group".

3. In the top menu bar, select the project and region where the placement group resides.

4. On the "Placement group" page, click the name of the placement group you want to manage.

5. On the "Overview" tab, view details such as the number of sub\-placement groups and auto\-assigned sub\-placement groups.


</Tab>
<Tab zoneid="R1G7NB90tw" title="View volumes associated with a placement group">
<TabTitle>View volumes associated with a placement group</TabTitle>

1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left navigation pane, select "Storage \> Placement group".

3. In the top menu bar, select the project and region where the placement group resides.

4. On the "Placement group" page, click the name of the placement group you want to manage.

5. On the placement group details page, click the "Associated Volumes" tab to view information about volumes associated with the placement group.


</Tab>
<Tab zoneid="TtQtwPEPyC" title="Delete a placement group">
<TabTitle>Delete a placement group</TabTitle>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">You cannot delete a placement group if it is associated with a volume. If your placement group is associated with volumes, you must delete those volumes first before deleting the placement group.</div>



1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left navigation pane, select "Storage \> Placement group".

3. In the top menu bar, select the project and region where the placement group resides.

4. On the "Placement group" page, click "... \> Delete" in the "Actions" column of the placement group.

5. In the box that appears, click "Delete".


</Tab>
</Tabs>
