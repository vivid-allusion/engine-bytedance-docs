---
title: "Creating object groups"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Creating_object_groups"
---

An object group is a collection of resources, which can include instances of multiple services across multiple regions. The object group is used to define the range of resources.

<span id="04wrRs5W"></span>
## Limits


* A root user can create up to 100 object groups.

* Up to 100 resource types can be added to an object group.

* Up to 1,000 resources of the same type and up to 5,000 resources of all types can be added to an object group.

* When you select resources by resource name, project and tag, up to 1,000 resources can be matched.


<span id="39D2zCHk"></span>
## Procedure


1. Log in to the [Observability Platform console](https://console.byteplus.com/observe).

2. In the left navigation pane, click **Alert Center \> Alert Configuration** to go to the Alert Configuration page.

3. In the alert configuration section on the left, select **Cloud Monitor** and click the **Object Grouping** tab.

4. Click **Create object group**. Configure the object group parameters as described, and then click **Create**.

   
   |Parameter |Description |
   |---|---|
   |Object group name |Specify a custom name for the object group.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Using certain characters in the name may cause alert SMS delivery failures. </div><br> |
   |Resource type |Specify the resource types included in the object group. Click **Add** in the lower\-left corner to add multiple resource types.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Up to 100 resource types can be added to an object group.</div><br> |
   |Selection method |The method of selecting resources. You can manually select resources or select multiple resources at a time by resource name, project, or tag. |
   ||You need to specify the following parameters when you set the Selection method parameter to **Manually select**:<br><br><br>* **Region**: The region to which the resource belongs.<br><br>* **Select resource**: Manually select target resources from the resource list and add them to the object group. This is static. Newly added resources cannot be automatically matched and need to be manually added to the object group. This is applicable to scenarios where fixed resources are specified. |
   ||You need to specify the following parameters when you set the Selection method parameter to **Resource name**:<br><br><br>* **Region**: The region to which the resource belongs.<br><br>* **Resource name**: Select resources by resource name\-matching rules. Resources that match the rules are automatically added to the object group. Resources are selected dynamically. New resources that match the rules are automatically added to the object group.<br><br>   You can select all resources, or select some resources based on resource name matching rules. When selecting some resources, you can configure multiple matching rules. The logical relationships between multiple matching rules include "Anyone is met" and "All are met".<br><br>   * **Anyone is met**: OR logic relationship. This means resources that meets any matching rule are selected.<br><br>   * **All are met**: AND logic relationship. This means only resources that meet all matching rules are selected.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The filter conditions provided by matching rules include Prefix matches, Suffix matches, Contain, Not contain, Equal to, and Not equal to.   </div><br>    |
   ||For products that allow you to select alert objects by project, see [Limits](https://docs.byteplus.com/en/docs/314/120394#04wrRs5W). You need to specify the following parameters when you set the Selection method parameter to **Project**:<br><br><br>* **Region**: The region to which the resource belongs.<br><br>* **Project**: Select target resources in batches by project and add them to the object group. Resources are selected dynamically. New resources added to the project are automatically added to the object group. |
   ||For products that allow you to select alert objects by tag, see [Limits](https://docs.byteplus.com/en/docs/314/120394#04wrRs5W). You need to specify the following parameters when you set the Selection method parameter to **Tag**:<br><br><br>* **Region**: The region to which the resource belongs.<br><br>* **Tag**: Select target resources in batches by tag and add them to the object group. Resources are selected dynamically. Resources that match the tag rules will be automatically added to the object group.<br><br>   When selecting resources by tag, you can configure multiple tag\-matching rules. The logical relationships between multiple matching rules include "Anyone is met" and "All are met".<br><br>   * **Anyone is met**: Uses OR logic. Resources that match any of the matching rules are selected.<br><br>   * **All are met**: Uses AND logic. Only resources that match all matching rules are selected.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The filter conditions provided by matching rules include "Exists, and the value prefix matches", "Exists, and the value suffix matches", "Exists, and the value prefix does not match", "Exists, and the value suffix does not match", "Exists, and the value contains", "Exists, and the value does not contain", "Exists, and the value is equal to", "Exists, and the value is not equal to", "Exist", and "Does not exist".   </div><br>    |
   

5. After the object group is created, click its name to view its details. The details include basic information, associated alert templates, cloud products, matching rules and resource lists for different cloud products, and associated alert rules.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You need to apply an alert template to the object group before you can associate alert templates, alert rules, as well as matching rules and resource lists for different cloud services. For instructions, see <a href="https://docs.byteplus.com/en/docs/Observability_Platform/Applying_alert_templates_to_object_groups">Applying alert templates to object groups</a>.   </div>
