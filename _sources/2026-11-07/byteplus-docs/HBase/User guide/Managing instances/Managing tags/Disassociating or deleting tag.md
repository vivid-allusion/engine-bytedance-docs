---
title: "Disassociating or deleting tag"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Disassociating_or_deleting_tag"
---

When an instance no longer requires a certain tag, you can disassociate the instance from the tag. This topic contains instructions on how to disassociate tags from an instance.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* You can disassociate up to 20 tags at a time.

* A maximum of 100 instances can be selected simultaneously for batch tag disassociating.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5Li65Y2V5Liq5a6e5L6L6Kej57uR5qCH562-"></span>
### Disassociate tags for individual instances


1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the ** ** <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1f593c2f1753114728d247ea44bcbe09.png)<sub> </sub></span> icon for the Tag column.

   You can also click the target instance to enter the **Summary** page. In the **Basic information** area, click the ** ** <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1f593c2f1753114728d247ea44bcbe09.png)<sub> </sub></span> icon after the Tag.

4. In the dialog box that pops up, confirm the instance information, find the tag that needs to be unbound, and click the <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_780fa292e1f1e020b9db018da34cb501.jpg)<sub> </sub></span> icon.

5. Click **OK**.


<span id=".5Li65aSa5Liq5a6e5L6L5ZCM5pe26Kej57uR5qCH562-"></span>
### Disassociate tags from multiple instances at once


1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, select multiple target instances and click the **Remove tab** in the lower left corner of the instance list.

4. In the dialog box that pops up, confirm the instance information and select the tag key to be disassociated.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When disassociate the tag, all instances containing the tag key will be disassociated, please be cautious.   </div>
   

5. Click **OK**.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[RemoveTagsFromResource](https://docs.byteplus.com/en/docs/HBase/RemoveTagsFromResource) |Call the RemoveTagsFromResource to disassociate tags from one or more instances. |
