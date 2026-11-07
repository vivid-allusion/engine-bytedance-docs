---
title: "Tag management"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Tag-overview"
---

As your business grows, both the number and types of cloud resources continue to increase, which makes management more difficult. At this point, you can add different tags to mark and classify cloud resources of different types and purposes. This allows you to quickly find cloud resources with specific attributes and improve management efficiency.

<span id=".5bqU55So5Zy65pmv"></span>
## Applicable scenarios

**Group management**

You can associate different tags with different environments (such as the production environment and test environment), different operating systems (such as Windows and Linux), or different client platforms (such as iOS and Android). For example, you can associate a tag, such as the key\-value pair of Test:Server\-Windows, with all instances involved in a test environment. During routine maintenance, you can filter a group of instances with this tag from all instances and then take actions.

**Tag\-based bill splitting**

In team or project management, you can add tags based on group, project, or department (such as CostCenter:Project) to categorize resources. Then, use these tags in the Billing Center for cost allocation management. If you want to use tags for bill splitting, enable Billing tag in the Billing Center consoleapply related tags to detailed bills. For specific actions, refer to [Billing tags](https://docs.byteplus.com/en/docs/byteplus-platform/bill_tags).

<span id=".5qCH562-57G75Z6L"></span>
## Tag type


* System tag: Tags that are automatically added to resources when they are created are system tags. System tags usually start with `volc:` or `sys:`, can only be viewed and cannot be edited.

* Custom Tags: Tags manually added by you are called custom tags. You can not create custom tags that start with `volc:` or `sys:` in any case variation (uppercase or lowercase).

* For design principles and common examples of tags, see [Tag design principles](https://docs.byteplus.com/en/docs/ecs/Tag-design-principles).


<span id=".5L2_55So6K-05piO"></span>
## Usage notes


* ECS\-related resources that support the tag feature include: instances, custom images, volumes, RIs, ESIs, launch templates, key pairs, and cloud assistants.

* A tag consists of a tag\-key (Key) and a tag\-value (Value), both of which are case\-sensitive. Value can be empty.

* Keys of multiple tags for the same resource must be unique, and each Key can have only one Value.


<span id=".566h55CG5qCH562-"></span>
## Manage tags

This topic, with instances used as an example, describes the procedure to associate tags with resources. If you need to associate tags with other resources, such as volumes and RIs, select the target resource in the left\-side navigation pane in the product console.

<span id=".5Yib5bu65bm257uR5a6a5qCH562-"></span>
### Create and associate tags

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You can associate up to 20 tags per request, and associate up to 50 tags with one resource.</div>


* <div data-tips="true" data-tips-type="tip">If the tag key to be associated with the instance overlaps with an existing one, the new tag value will override the original. Please proceed with caution.</div>




<Tabs>
<Tab zoneid="f3fyeTRNXH" title="Associate tags with created instances">
<TabTitle>Associate tags with created instances</TabTitle>

1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Instances & Images \> Instances". In the top menu bar, select the region and project of the target instance.

3. On the Instances page, associate tags with instances.

   * Associate tags with multiple instances at the same time: Select one or more instances with tags to be associated with, and click the "··· \> Add tags" button at the bottom of the page.

   * Associate tags with one instance: Click the "··· \> Instance settings \> Edit tag" button in the "Actions" column to the right of the target instance.

4. In the pop\-up dialog box, confirm the instance name and click the "Add tags" button to associate one or more new tags with the instance.

5. Click "Reset" to complete the operation.

6. You can view the associated tags of instances through the following methods:

   * In the "tag" column of the target instance on the Instances page.

   * On the Instances page, click the target instance to enter the instance Overview page. In the "Basic information" section, you can view associated tags of the instance.


</Tab>
<Tab zoneid="CnsYUAuWt4" title="Associate tags with instances that are being created">
<TabTitle>Associate tags with instances that are being created</TabTitle>

[When creating instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) on the **Custom configuration** page, you can click the "Add tags" button to associate tags with instances.

If you associate tags when creating an instance, network resources created at the same time (such as EIPs) are also associated with the same tags. If an EIP is associated with an instance after the instance is created, the tags of that instance are not synchronized to the EIP.


</Tab>
</Tabs>


<span id=".6Kej57uR5qCH562-"></span>
### Disassociate tags

If a tag can no longer be applied to manage and retrieve resources, refer to the following methods to disassociate the tag from target resources.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You can disassociate a maximum of 20 tags at one time.</div>


* <div data-tips="true" data-tips-type="tip">Repeatedly disassociating a tag overrides the original result and updates the tag value.</div>


* <div data-tips="true" data-tips-type="tip">After a tag is disassociated, if not associated with any resource, it will be automatically deleted.</div>


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Instances & Images \> Instances". In the top menu bar, select the region and project of the target instance.

3. On the Instances page, disassociate tags from instances. After you disassociate tag keys, all associated tags with them will be disassociated. Please proceed with caution when you select or enter tag keys to disassociate.

   * Disassociate tags from multiple instances at the same time: Select one or more instances with tags to be disassociated, and click the "··· \> Remove tags" button at the bottom of the page.

   * Disassociate tags from one instance: Click the "··· \> Instance settings \> Edit tag" button in the "Actions" column to the right of the target instance.

5. Click "Confirm" to complete the operation.


<span id=".5L2_55So5qCH562-5pCc57Si6LWE5rqQ"></span>
### Search resources by tag

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When you search resources by tag, the limits on entered tags are as follows:</div>



* <div data-tips="true" data-tips-type="tip">You can enter a maximum of 10 tag keys at one time.</div>


* <div data-tips="true" data-tips-type="tip">When you search by tag in the search bar above the instance list, a maximum of three tag values can be filtered at the same time for the same tag key.</div>


* <div data-tips="true" data-tips-type="tip">Tag values can be left blank or empty:</div>


   * <div data-tips="true" data-tips-type="tip">Left blank: This defaults to no limit on the tag values, which means any value can be used.</div>


   * <div data-tips="true" data-tips-type="tip">Left empty: Filter tags with an empty value, which refers to tags added without an entered value.</div>


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Instances & Images \> Instances". In the top menu bar, select the region and project of the target instance.

4. On the Instances page, you can quickly search for instances by tag as follows.

   * Method 1: Search in the header of the instance list

      1. In the header, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fdf17bac02d997d043069ddeb7057e68.png) </span>icon next to "Tag". Then, select or enter the tag key and tag value.

      2. Click the "Confirm" button to view all instances associated with the specified tag.

   * Method 2: Search in the search bar above the instance list

      Specify the search method in the search bar. Available search methods include "Tag", "Tag key", and "Tag value".


**Sample search**

Assume the search condition is:

Tag key 1: key1; Tag value: value1, value2;

Tag key 2: key2, tag value: left blank.

Resources associated with the following tags are filtered out:


* key1, value1

* key1, value2

* The tag whose key is key2 and whose value can be any value


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* In addition to tags, you can also use [projects](https://docs.byteplus.com/en/docs/ecs/Managing-projects) to group your resources based on dimensions such as resource usage, permission, and ownership. This helps achieve hierarchical resource management for multiple users and multiple projects. 

* If you need to call the interface to manage tag resources, refer to [OpenAPI - Tags](https://docs.byteplus.com/en/docs/ecs/Tags).
