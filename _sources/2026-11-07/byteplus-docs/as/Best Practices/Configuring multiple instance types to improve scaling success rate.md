---
title: "Configuring multiple instance types to improve scaling success rate"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Configuring-multiple-instance-types-for-a-scaling-group"
---

Within the same scaling group, you can select multiple instance types with similar performance, specification, or price as the scaling configuration source. When a higher\-priority instance type cannot be used to create an instance, the next\-priority instance type is automatically used. This enhances the fault tolerance and high availability of scale\-out operations, and applies to scenarios requiring business continuity without reliance on a single instance type.

<span id=".6YWN572u5YmN6K-05piO"></span>
## Configuration note

Scaling groups support two types of scaling configuration sources: scaling configuration and instance launch template:


* The creation methods, multi\-instance type configuration methods, usage process, and limits of the two types differ slightly. You can refer to [Scaling configuration sources](https://docs.byteplus.com/en/docs/as/Overview-of-scaling-configuration-sources#.5Ly457yp6YWN572u5p2l5rqQ57G75Z6L) to select the appropriate scaling configuration source type.

* Only one scaling configuration source can be associated with a scaling group.


This topic describes how to configure a scaling group with multiple instance types by using a scaling configuration and an instance launch template.

<span id=".6YCa6L-H4oCc5Ly457yp6YWN572u4oCd6YWN572u5Ly457yp57uE"></span>
## Configure a scaling group by using a scaling configuration

After you create a scaling group, you can create a scaling configuration and associate it with the scaling group. The procedure is as follows:


1. Create a scaling group: When you configure the scaling configuration source, select "Not set now". For information about other parameters, see [Creating scaling groups](https://docs.byteplus.com/en/docs/as/Creating-a-scaling-group).

2. Create a scaling configuration: The following only lists parameters related to multiple instance types. For information about other parameters, see [Creating scaling configurations](https://docs.byteplus.com/en/docs/as/Managing_a_scaling_configuration).

   1. In the "Instance Type" section, select the instance type. The selected type here is the preferred type for scale\-out, which is the highest\-priority type.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">We recommend that you select an instance type with "Normal stock" to improve the success rate of scaling out.      </div>
      

            2. In the "Multi\-type" section, select "Enable multi\-type selection", select multiple instance types, and drag to sort the types in the list below. The preferred type has the highest priority and cannot be adjusted. To modify the preferred instance type, clear "Enable multi\-type selection" before you proceed.

   3. In the "Status After Creation" section, select "Associate scaling group".

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_83141a244ffbe862451ff30c58ffd280.png) </span>

3. At this point, you have successfully created a scaling group with multiple instance types. You can go to the scaling group details page and view the selected instance types on the "Scaling Configuration Sources \> Scaling configurations" tab.

   To modify the instance types, click the "Change scaling configuration" button on the right side of the scaling configuration.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_360ec90265bfb4e54e213ade807acedf.png) </span>

4. Subsequently, you can [enable the scaling group](https://docs.byteplus.com/en/docs/as/Enabling-a-scaling-group) and [create scaling rules](https://docs.byteplus.com/en/docs/as/Creating-a-scheduled-scaling-policy) to trigger scaling operations for the scaling group.


<span id=".6YCa6L-H4oCc5a6e5L6L5ZCv5Yqo5qih54mI4oCd6YWN572u5Ly457yp57uE"></span>
## Configure a scaling group by using an instance launch template

After you create an instance launch template, you can select the template to create a scaling group. You can also create a scaling group first and then [select an instance launch template](https://docs.byteplus.com/en/docs/as/Associating-a-scaling-configuration-source-with-a-scaling-group#.6YCJ5oup5ZCv5Yqo5qih5p2_). This section describes how to select an instance launch template to create a scaling group. The procedure is as follows:


1. Create an instance launch template: You can create an instance launch template by using various methods. For example, you can create an instance launch template from an existing instance or recreate an instance launch template by following the console wizard. For more information, see [Creating instance launch templates](https://docs.byteplus.com/en/docs/ecs/Creating-launch-templates).

2. Create a scaling group: The following only lists parameters related to multiple instance types. For information about other parameters, see [Creating scaling groups](https://docs.byteplus.com/en/docs/as/Creating-a-scaling-group).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_22be1d5e30387cfb4a5b1fa1f39af7db.png) </span>

   
   |Parameter​ |Description |Sample value |
   |---|---|---|
   |Select Launch Template/Select template version |You can select any version of the template. |\- |
   |Extended Launch Template Configuration |After you click "Enable", you can select multiple instance types. You can click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_89caf61ce74414d0b3b5dd0ca874cada.png) </span> icon to the left side of "Selected instance types" and drag to sort the instance types.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is currently in Beta. To apply for a trial, contact your account manager.</div><br> |Enable |
   

3. At this point, you have successfully created a scaling group with multiple instance types. You can view the associated launch template on the "Scaling Configuration Sources \> Launch Templates" tab of the scaling group details page.

   To modify the instance types, click the "Modify the Launch Template" button on the right side of the launch template.

4. Subsequently, you can [enable the scaling group](https://docs.byteplus.com/en/docs/as/Enabling-a-scaling-group) and [create scaling rules](https://docs.byteplus.com/en/docs/as/Creating-a-scheduled-scaling-policy) to trigger scaling operations for the scaling group.
