---
title: "Set expiration times"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Set-expiration-times"
---

You can use APIs to instruct TOS to delete objects when they reach the end of their lifecycle. This topic explains how to set, modify, and view the expiration times for objects.

<span id="c34f55be"></span>
## Notes


|**Category** |**Notes** |
|---|---|
|Start time |The expiration time of an object is calculated from the Last‑Modified time, in days. |
|Execution time |After setting the object expiration time, TOS starts the deletion task at midnight after the expiration time is reached. For example, if the object's Last‑Modified time is 2024\-09\-26 12:00 and the expiration time is 3 days, the object expires at 2024\-09\-30 00:00. |
|Priority |Expiring objects via APIs takes precedence over lifecycle deletion rules. For instance, if an object's expiration time is set to five days and a lifecycle rule specifies deletion after three days, the object will be deleted after five days based on its expiration time.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can set both object expiration times and lifecycle rules simultaneously. For instance, if you configure a rule to transition objects with a specified prefix to Infrequent Access Storage three days after their last modified time, and you set the expiration time for an object with the specified prefix to five days, the object will transition to Infrequent Access Storage after three days and be deleted after five days.</div><br> |
|Versioning |The process of expiring objects with multiple versions has two steps:<br><br><br>* At the first expiration: The object becomes a historical version with a deletion mark added.<br><br>* On subsequent expiration: The historical version follows the original object's expiration policy and the data is permanently deleted. |
|Usage limits |You cannot set an expiration time for symlink objects. |


<span id="cce0d641"></span>
## Steps


<Tabs>
<Tab zoneid="hsW8CfbKYM" title="Set expiration times">
<TabTitle>Set expiration times</TabTitle>

**Add an expiration time when uploading an object**

You can use the `x-tos-object-expires` parameter in the following APIs to add an expiration time to an object. This parameter supports setting a positive integer in days, indicating the object will expire after the specified time. The calculation starts from the object's Last‑Modified time, and the deletion task executes at midnight after the expiration time. For example, if you set the `x-tos-object-expires` parameter to `3`, and the object's last modified time is 2024\-09\-26 12:00, the object will expire at 2024\-09\-30 00:00. The corresponding API descriptions are as follows:


* Add an expiration time when uploading an object

   * [PutObject](https://docs.byteplus.com/docs/tos/reference-putobject)

   * [PostObject](https://docs.byteplus.com/docs/tos/reference-postobject)

   * [CreateMultipartUpload](https://docs.byteplus.com/docs/tos/reference-createmultipartupload)

* Add an expiration time when appending an object

   * [AppendObject](https://docs.byteplus.com/docs/tos/reference-appendobject)

* Set an expiration time when copying an object

   * [CopyObject](https://docs.byteplus.com/docs/tos/reference-copyobject)


**Add an expiration time to an uploaded object**

You can add an expiration time to an uploaded object by using the SetObjectExpires API's `ObjectExpires` parameter. This parameter supports setting a positive integer or 0, with the unit in days. The value definitions are as follows:


* Positive integer: The object expires after the specified time, calculated from the object's Last‑Modified time. The deletion task begins at midnight following the expiration time. For example, if the `ObjectExpires` parameter value is set to `3` and the object's last modified time is 2024\-09\-26 12:00, the object will expire at 2024\-09\-30 00:00.

* 0: The object will remain in the bucket until you manually delete it or lifecycle rules remove it.


For details, see [SetObjectExpires](https://docs.byteplus.com/docs/tos/SetObjectExpires).


</Tab>
<Tab zoneid="KJ7NLdTEqz" title="Modify expiration times">
<TabTitle>Modify expiration times</TabTitle>

You can modify the object's expiration time through the `ObjectExpires` parameter of the SetObjectExpires interface. This parameter supports positive integers or 0, in days. The values are explained below:


* Positive integer: the object expires after the specified time, calculated from the object's last modified time, and deletion starts at midnight after the expiration time. For example, setting the `ObjectExpires` parameter value to `3` and the object's last modified time is 2024\-09\-26 12:00, then the object expires at 2024\-09\-30 00:00.

* Objects will be retained in the bucket until you delete them manually or lifecycle rules delete them.


For details, see [SetObjectExpires](https://docs.byteplus.com/docs/tos/SetObjectExpires).


</Tab>
<Tab zoneid="WIZ7sYLgx4" title="View expiration times">
<TabTitle>View expiration times</TabTitle>

* You can check an object’s expiration time using the `X-Tos-Expiration` parameter in GetObject and HeadObject. For details, see [GetObject](https://docs.byteplus.com/docs/tos/reference--getobject) and [HeadObject](https://docs.byteplus.com/docs/tos/reference-headobject).

* To view the expiration time of an object in the console:

   1. Log in to the [TOS console](https://console.volcengine.com/tos).

   2. In the left navigation pane, click **Buckets**. In the **Buckets** list, click the bucket you want to manage.

   3. On the **Objects** page, click **Details** in the **Actions** column of the object you want to check. The **expiration time** is displayed under **Basic information**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The expiration time is only displayed when a lifecycle rule is configured with an automatic deletion policy in the <strong>Policy configuration</strong> section.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If there are multiple lifecycle rules and the first rule does not include an automatic deletion policy, but subsequent rules do, the expiration time will not be displayed.   </div>
   


</Tab>
</Tabs>
