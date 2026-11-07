---
title: "Associating or adding tag"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/associate-tag"
---

Document Database for MongoDB supports tag management. Tags can be used to identify cloud resources, helping you label and classify similar instances based on different criteria (such as usage, type, owner and environment), making it easier to filter and manage the tags. This topic describes how to associate tags with instances.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite

The instance status must be **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).

<span id=".5qCH562-6K6-572u6KeE5YiZ"></span>
## Tag setting rules

The tag setting rules in Document Database for MongoDB service are specified in the table below.


|Limits |Description |
|---|---|
|Tag key |* Supports any language letters or characters (such as Chinese, English letters), digits, spaces, and the following special characters: `_.:/=+-@`.<br><br>* The tag key must be 1 to 128 characters in length.<br><br>* Tag keys are case\-sensitive. For example, `Type` and `type` are two different tag keys.<br><br>* `volc:` and `sys:` are system\-reserved tag keys. When adding tags, you cannot set a tag key to start with `volc:` or `sys:` (in any case). |
|Tag value |* Supports any language letters or characters (such as Chinese, English letters), digits, spaces, and the following special characters: `_.:/=+-@`.<br><br>* Tag values are case\-sensitive. For example, `Shard` and `shard` are two different tag values.<br><br>* The tag value should be 0 to 256 characters in length, meaning that tag values can be empty. |
|Quantity |* The total number of tags is unlimited, but each MongoDB instance can associate up to 50 tags.<br><br>* You can add up to 20 tags at a time. |


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Each tag key must be unique for instance, and can have only one tag value.

* If the key of a newly added tag is the same as a tag key already associated with instance, the new tag value will overwrite the original one. Proceed with caution.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Associating tags has no impact on instance operation.</div>


<span id=".5Li65Y2V5Liq5a6e5L6L57uR5a6a5qCH562-"></span>
### Associate tags for individual instance


* **Method 1**

   Associate tags directly when creating instance. For specific procedures, refer to [Creating instance](https://docs.byteplus.com/en/docs/mongodb/creating_an_instance).

* **Method 2**

   1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

   2. In the upper\-left corner of the top menu bar, select the project and region for instance.

   3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

   4. On the target instance type list page, locate the target instance and click ** ** <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1f593c2f1753114728d247ea44bcbe09.png) </span> icon in the **Tag** column.

      You can click the target instance to enter the **Summary** page, and in the **Basic information** area, ** ** click <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1f593c2f1753114728d247ea44bcbe09.png) </span> icon in the **Tag** column.

   5. In the pop\-up dialog box, confirm the instance information and select existing tag keys and values from the drop\-down list according to business needs, or enter new tag keys and values.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If IAM users use tag resources in MongoDB instances, the root account needs to add the <code>TagFullAccess</code> permission policy for IAM users globally first. Only then can the existing tags under the root account be seen in the drop\-down list. Otherwise, the drop\-down list will be empty. However, even if IAM users do not have <code>TagFullAccess</code> permission, they can still add new tags to instances. For more details, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/using_mongodb_services_with_subusers">Using MongoDB with IAM users</a>.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The tag keys and values must comply with certain setting rules. For mode details, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/associate-tag#.5qCH562-6K6-572u6KeE5YiZ">Tag setting rules</a>.      </div>
      

   6. click **OK**.


<span id=".5Li65aSa5Liq5a6e5L6L5om56YeP57uR5a6a5qCH562-"></span>
### Associate tag for multiple instances


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, select the target instances for which you want to disassociate tags, and click **Add tag** in the lower\-left corner of the instance list.

5. In the pop\-up dialog box, confirm the instance information and select existing tag keys and values from the drop\-down list according to business needs, or enter new tag keys and values.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If IAM users use tag resources in MongoDB instances, the root account needs to add the <code>TagFullAccess</code> permission policy for IAM users globally first. Only then can the existing tags under the root account be seen in the drop\-down list. Otherwise, the drop\-down list will be empty. However, even if IAM users do not have <code>TagFullAccess</code> permission, they can still add new tags to instances. For more details, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/using_mongodb_services_with_subusers">Using MongoDB with IAM users</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The tag keys and values must comply with certain setting rules. For mode details, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/associate-tag#.5qCH562-6K6-572u6KeE5YiZ">Tag setting rules</a>.   </div>
   

6. Click **OK**.


<span id=".55u45YWzLWFwaQ=="></span>
## Relevant APIs


|API |Description |
|---|---|
|[AddTagsToResource](https://docs.byteplus.com/en/docs/mongodb/addtagstoresource) |Call the AddTagsToResource API to associate tags with the target MongoDB instance. |
