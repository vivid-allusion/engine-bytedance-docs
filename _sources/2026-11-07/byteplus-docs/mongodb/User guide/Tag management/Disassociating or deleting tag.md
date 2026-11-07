---
title: "Disassociating or deleting tag"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/disassociate-tag"
---

Document Database for MongoDB supports tag management. Tags can be used to identify resources. When instance no longer requires a certain tag, you can disassociate the instance from the tag. This topic describes how to disassociate tags from instances.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite

The instance status must be **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* You can disassociate up to 20 tags at a time.

* Repeatedly disassociating tags overwrites the original result, and the tag value will be updated.

* After tags are disassociated, if the number of resources associated with that tag is zero, it will be automatically deleted.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Disassociating tags has no impact on instance operation.</div>


<span id=".5Li65Y2V5Liq5a6e5L6L6Kej57uR5qCH562-"></span>
### Disassociate tags for individual instance


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, locate the target instance and click ** ** <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1f593c2f1753114728d247ea44bcbe09.png) </span> icon in the **Tag** column.

   You can click the target instance to enter the **Summary** page, and in the **Basic information** area, ** ** click <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1f593c2f1753114728d247ea44bcbe09.png) </span> icon in the **Tag** column.

5. In the pop\-up dialog box, confirm the instance information, find the tags to be disassociated, and click <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_780fa292e1f1e020b9db018da34cb501.jpg) </span> icon on the right of the tags.

6. click **OK**.


<span id=".5Li65aSa5Liq5a6e5L6L5om56YeP6Kej57uR5qCH562-"></span>
### Disassociate tag for multiple instances


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, select the target instances for which you want to disassociate tags, and click **Remove tag** in the lower\-left corner of the instance list.

5. In the pop\-up dialog box, confirm the instance information, and then enter or select the tags to be disassociated.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">You can click <strong>Add tag</strong> and enter multiple tag keys to batch disassociate tags. All tags containing these tag keys will be disassociated. Please proceed with caution.   </div>
   

6. Click **OK**.


<span id=".55u45YWzLWFwaQ=="></span>
## Relevant APIs


|API |Description |
|---|---|
|[RemoveTagsFromResource](https://docs.byteplus.com/en/docs/mongodb/removetagsfromresource) |Call the RemoveTagsFromResource API to disassociate tags from the target MongoDB instance. |
