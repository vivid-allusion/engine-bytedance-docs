---
title: "Associating or adding tag"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Associating_or_adding_tag"
---

Table Storage for HBase supports tag management. After associating tags, you can quickly filter instances by specifying tag keys and tag values. This topic contains instructions on how to associate tags with an instance.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Each tag key must be unique for instance, and can have only one tag value.

* If the new tag key for an instance is the same as an associated one, the new tag value will override that of the associated one. Exercise caution when performing this operation.

* A maximum of 100 instances can be selected simultaneously for batch tag associating.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5Li65Y2V5Liq5a6e5L6L5re75Yqg5qCH562-"></span>
### Associate tags for individual instances

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can directly associate tags for instances when <a href="https://docs.byteplus.com/en/docs/HBase/Creating_an_instance_1">creating instances</a>, or you can associate tags for instances after instance creation is completed.</div>



1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the ** ** <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1f593c2f1753114728d247ea44bcbe09.png)<sub> </sub></span> icon after the Tag.

   You can also click the target instance to enter the **Summary** page. In the **Basic information** area, click the ** ** <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1f593c2f1753114728d247ea44bcbe09.png)<sub> </sub></span> icon after the Tag.

4. In the pop\-up dialog box, select the existing tag key and tag value from the drop\-down list according to business needs, or enter a new tag key and tag value.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you use sub\-account management instances, you need to add a globally <code>TagFullAccess</code> permission policy for sub\-account, so that all existing tags under the main account can be viewed in the drop\-down list, otherwise the drop\-down list is empty. Whether a sub\-account has <code>TagFullAccess</code> does not affect adding new tags to the instance. Add permissions for sub\-accounts see <a href="https://docs.byteplus.com/en/docs/HBase/Using_HBase_with_sub-accounts">Using HBase with sub\-accounts</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The tag key value must meet certain setting rules. For details, please refer to the <a href="https://docs.byteplus.com/en/docs/HBase/Tag_overview#.5qCH562-6K6-572u6KeE5YiZ">Tag setting rules</a>.   </div>
   

5. Click **OK**.


<span id=".5Li65aSa5Liq5a6e5L6L5ZCM5pe25re75Yqg5qCH562-"></span>
### Associate tags from multiple instances at once


1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, select multiple target instances and click the **Add tab** in the lower left corner of the instance list.

4. In the pop\-up dialog box, select the existing tag key and tag value from the drop\-down list according to business needs, or enter a new tag key and tag value.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you use sub\-account management instances, you need to add a globally <code>TagFullAccess</code> permission policy for sub\-account, so that all existing tags under the main account can be viewed in the drop\-down list, otherwise the drop\-down list is empty. Whether a sub\-account has <code>TagFullAccess</code> does not affect adding new tags to the instance. Add permissions for sub\-accounts see <a href="https://docs.byteplus.com/en/docs/HBase/Using_HBase_with_sub-accounts">Using HBase with sub\-accounts</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The tag key value must meet certain setting rules. For details, please refer to the <a href="https://docs.byteplus.com/en/docs/HBase/Tag_overview#.5qCH562-6K6-572u6KeE5YiZ">Tag setting rules</a>.   </div>
   

5. Click **OK**.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[AddTagsToResource](https://docs.byteplus.com/en/docs/HBase/AddTagsToResource) |Call the AddTagsToResource to associate tags to one or more instances. |
