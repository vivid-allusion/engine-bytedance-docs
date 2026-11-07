---
title: "Tag management"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Managing-tags"
---

<span id=".5qaC6L-w"></span>
## Overview

As your business scale expands, the variety and quantity of cloud resource instances you use also gradually increase. When you have a large number of cloud resource instances, by adding different tags to cloud resources of different types and purposes, you can label and categorize them. This helps you search for instances with target characteristics more quickly.

<span id=".5bqU55So5Zy65pmv"></span>
## Scenario


* **Group management**

   You can associate different tags to different environments (such as the production environment and test environment), different operating systems (such as Windows and Linux), or different client platforms (such as iOS and Android). For example, you can associate a tag, such as the key\-value pair of Test:Server\-Windows, with all instances involved in a test environment. During routine maintenance, you can filter a group of instances with this tag from all instances and then take actions.

* **Tag\-based bill splitting**

   In team or project management, you can add tags based on group, project, or department (such as CostCenter:Project) to categorize resources. Then, use these tags in the Billing Center for cost allocation management. If you want to use tags for bill splitting, you need to enable Billing tag in the Billing Center console by the path of [Bill management-Billing tag](https://console.byteplus.com/finance/bill/tag/), and apply related tags to detailed bills. For specific actions, refer to [Billing tags](https://docs.byteplus.com/en/docs/byteplus-platform/bill_tags).


<span id=".5qCH562-57G75Z6L"></span>
## Tag type


* System tag: Tags that are automatically associated with scaling groups and instances when scaling groups are created or when instances are managed via the scaling group feature. System tags typically start with `volc:` or `sys:`, and can only be viewed, not edited.

* Custom Tags: Tags manually added by you are called custom tags. You can not create custom tags that start with `volc:` or `sys:`  in any letter case.

* For more information on tag design principles, please refer to [Tag design principles](https://docs.byteplus.com/en/docs/ecs/Tag-design-principles).


<span id=".5qCH562-5L2_55So6K-05piO"></span>
## Tag usage instructions


* A tag consists of a tag key (Key) and a tag value (Value), both of which are case\-sensitive. The tag value can be empty.

* Keys of multiple tags for the same instance must be unique, and each Key can have only one Value.

* Currently, only scaling groups and instances within scaling groups support the tag feature.

* Scaling groups in the **Creating** and **Deleting** states do not support modifying tags.

* A maximum of 50 tags can be added per operation, and each scaling group can be associated with a maximum of 50 tags.

* Tags that have been associated with resources such as ECS instances within a scaling group do not change as the scaling group is tagged.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".57uR5a6a5qCH562-"></span>
### Associate a tag

<span id=".5Yib5bu65Ly457yp57uE5pe257uR5a6a5qCH562-"></span>
#### Associate tags during scaling group creation

When you [create a scaling group](https://docs.byteplus.com/en/docs/as/Creating-a-scaling-group), click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1d3e137a7fd2eeff405adbc924499ba3.png) </span> icon of the tag parameter, and enter the tag key and value.

<span id=".5Yib5bu65Ly457yp57uE5ZCO57uR5a6a5qCH562-"></span>
#### Associate tags for a created scaling group


1. Log in to the [Scaling Group console](https://console.byteplus.com/as/group). 

2. In the top menu bar, select the project and region of the target resource.

3. Select any of the following methods to access the tag editing page:

   * In the "Tag" column of the target scaling group, hover the mouse over the edit icon <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3e6273c62a7babdd248e78c7aebc2c25.png) </span> .

   * Click the name of the target scaling group to enter the details page. Next to "Tag" in the "Basic Information" section, click the edit icon <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3e6273c62a7babdd248e78c7aebc2c25.png) </span> .

4. Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1d3e137a7fd2eeff405adbc924499ba3.png) </span> icon to associate a new tag with the scaling group.

5. Click the "OK" button to complete the operation. 


<span id=".57yW6L6R5qCH562-"></span>
### Edit a tag


1. Log in to the [Scaling Group console](https://console.byteplus.com/as/group). 

2. In the top menu bar, select the project and region of the target resource.

3. Select any of the following methods to access the tag editing page:

   * In the "Tag" column of the target scaling group, hover the mouse over the edit icon <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3e6273c62a7babdd248e78c7aebc2c25.png) </span> .

   * Click the name of the target scaling group to enter the details page. Next to "Tag" in the "Basic Information" section, click the edit icon <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3e6273c62a7babdd248e78c7aebc2c25.png) </span> .

4. Edit tags.

   * **Add tag**: In the pop\-up "Edit tag" dialog box, add new tag keys and values.

   * **Edit tag**: In the pop\-up "Edit tag" dialog box, directly edit the target key or value.

   * **Delete tag**: In the pop\-up "Edit tag" dialog box, next to the tag that you want to delete, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c873e2bedec7b7d5c5784111d2d50192.png) </span> icon.

5. Click the "OK" button to complete the operation.


<span id=".6YCa6L-H5qCH562-5pCc57Si5Ly457yp57uE"></span>
### Search scaling groups by tag


1. Log in to the [Scaling Group console](https://console.byteplus.com/as/group). 

2. In the top menu bar, select the project and region of the target resource.

3. To the right of the "Tag" column in the instance list, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d8b9c7d0e5cba19d5da69f4de6efbe32.png) </span> icon.

4. In the window that pops up below, enter the tag key and value that you want to query.

5. Click the "Confirm" button to search the target scaling group.


<span id=".6YCa6L-H5qCH562-6L-b6KGM5YiG6LSm"></span>
### Splitting bills by tags

For detailed operations, refer to [Billing tags](https://docs.byteplus.com/en/docs/byteplus-platform/bill_tags).
