---
title: "Lifecycle Rules Overview"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Lifecycle-rules-overview"
---

This topic describes how to implement automatic deletion of objects upon expiration through the lifecycle management feature of TOS, thereby saving your storage costs.

<span id="be7a17e6"></span>
## **Scenarios**

Lifecycle management is suitable for the following typical scenarios:


* Log files are uploaded periodically but only need to be retained for one week or one month, after which they need to be deleted.

* Some files are accessed frequently within a period of time, after which they may not be accessed andneed to be transitioned to Infrequent Access Storage or Archive Storage or deleted.

* A large number of files need to be batch deleted from a bucket. Manually deleting them is both time\-consuming and subject to a quantity limit. If lifecycle rules are configured for the bucket, all files can be deleted as scheduled.


For the objects in the above scenarios, you can define lifecycle rules to identify them and manage their lifecycle.

<span id="540c6569"></span>
## **Transition process**

Objects are transitioned between different storage types as follows.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d1fb6b4e66b843e292fc4be42f7805a0~tplv-goo7wpa0wc-image.image) </span>

Below are the rules for object transition.


|**Rule** |**Description** |
|---|---|
|Object transition |Objects can be transitioned only in a one\-way manner, that is, in the order of Standard Storage \> Infrequent Access Storage \> Intelligent Tiering Storage \> Flashback Archive \> Archive Storage . Cross\-level transition is allowed (for example, Standard Storage \> Archive), but reversed transition is not allowed (for example, Flashback Archive \> Standard Storage). |
|Intelligent Tiering Storage |TOS supports transitioning files from Standard Storage or Infrequent Access Storage to Intelligent Tiering Storage based on the following lifecycle rules:<br><br><br>* Files stored in Standard Storage and Infrequent Access Storage can be transitioned to Intelligent Tiering Storage.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Objects smaller than 64 KiB cannot be transitioned to Intelligent Tiering Storage.   </div><br>   <br><br>* Files stored in Intelligent Tiering Storage can only be transitioned to Flashback Archive, Archive Storage.<br><br>* Files transitioned from Standard Storage to Intelligent Tiering Storage will be stored in the frequent access tier of the latter, while those from Infrequent Access Storage will be in the infrequent access tier. |
|Archive Storage |Data in Archive Storage needs to be restored before they can be accessed. For detailed instructions, see [Restoring Files](https://docs.byteplus.com/en/tos/docs/restoring-files?version=1.0.0). |
|Cold Archive Storage |Cold Archive storage is supported only in China (Beijing), China (Shanghai), and China (Guangzhou). |
|Deep Cold Archive Storage |Deep Cold Archive is only supported in China (Beijing), China (Shanghai), and China (Guangzhou), and all are in the invitation\-only testing phase. If you need to use this storage type, please contact your account manager. |


<span id="53f94ece"></span>
### Operation

The lifecycle management function supports setting rules for deleting objects and converting storage types for the latest and historical versions of objects. The specific operations for deleting objects and converting storage types vary depending on the version control state. The instructions are as follows:


|**operation** |**Version control is not enabled** |**Enable version control** |**Pause version control** |
|---|---|---|---|
|Delete the latest version of the object |Permanently delete the object. |Add a delete tag for the latest version object and convert it to a historical version object. |* If it is a null version of an object, it is permanently deleted.<br><br>* If it is not a null version of the object, the object is marked for deletion and converted to a historical version. |
|Delete historical object |No. |Permanently delete the historical version object. |No matter whether it is a null version of the object, the historical version object is permanently deleted. |
|Converts the storage type of the latest version of the object |Converts the storage type of an object |Converts the storage type of the latest version object. |Converts the storage type of the latest version object. |
|Converting the storage type of a historical object |No. |Converts the storage type of the historical object. |Converts the storage type of the historical object. |


<span id="9b5efde9"></span>
## Effective time of rules

After creating a lifecycle rule, it will not take effect immediately on all objects in the bucket, and there will be a certain delay. That is, within 24 hours after the life cycle rule is created, the TOS will load the rule. After the rule is loaded, the TOS will start execution within 24 hours. The following limitations also exist:


|Category ||Description |
|---|---|---|
|A single storage bucket configuration lifecycle rule under one account. |Versioning not enabled. |The TOS supports completing 100 million lifecycle\-related operations (including storage type conversion, object expiration deletion, shard expiration deletion, and object\-level lifecycle expiration deletion) within 24 hours. If the number of lifecycle\-related operations exceeds 100 million, the execution time may exceed 24 hours. |
||Versioning Enabled |TOS supports completing 50 million lifecycle\-related operations (including storage type conversion, object expiration deletion, shard expiration deletion, and object\-level lifecycle expiration deletion) within 24 hours. If the number of lifecycle\-related operations exceeds 50 million, the execution time may exceed 24 hours.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If versioning is enabled on the bucket, each operation on an object's version is recorded as a lifecycle operation.</div><br> |
|Multiple storage buckets configuration lifecycle rules under one account. ||The TOS supports completing 200 million lifecycle\-related operations (including storage type conversion, object expiration deletion, shard expiration deletion, and object\-level lifecycle expiration deletion) within 24 hours. If the number of lifecycle\-related operations exceeds 200 million, the execution time may exceed 24 hours. |
|Modify or delete lifecycle rules ||The TOS will stop the execution of the original rules after a short delay (usually a few minutes), so it is recommended not to update lifecycle rules frequently. |


<span id="f65aa113"></span>
## Rule execution priority

Different prefix overlapping states have different priorities for lifecycle rule execution, as follows:


* unopened prefix overlap

   When setting lifecycle rules, conversion times vary for different storage types. For the same object, there is no case where an expiration policy is in effect at the same time, so there is no need to determine the priority of lifecycle rule execution.

* Opened prefix overlap

   If an object matches multiple lifecycle rules, the rule with a short expiration date will take effect first. If the rule expires in the same number of days, the lifecycle rule will be executed according to the principle of lower cost. The priority is as follows:

   Delete Object \> Convert to Deep Cold Archive \> Convert to Cold Archive \> Convert to Archive \> Convert to Archive Flashback \> Convert to Low Frequency \> Add Remove Marker to Object


<span id="0a0be877"></span>
## Precautions


|**Restriction** |**Description** |
|---|---|
|Quantity |The number of lifecycle rules for a bucket cannot exceed 1,000, and the total size of JSON descriptions for these rules cannot exceed 20 KB. |
|Effective time |Before executing the lifecycle rule, TOS will retrieve a file inventory, including prefixes and tags, and will only retrieve the file inventory once every 24 hours. If you modify the file prefixes and tags after retrieving the file inventory, you will need to wait for the next cycle for the changes to take effect. |
|Default expiration date |The default expiration date is calculated based on the date when you create or edit a rule and the number of days before expiration, specifically:<br><br><br>* Files sink to Infrequent Access Storage 30 days after upload.<br><br>* Files sink to Intelligent Tiering Storage 60 days after upload.<br><br>* Files sink to Flashback Archive 90 days after upload.<br><br>* Files sink to Archive Storage 180 days after upload.<br><br>* Files sink to Cold Archive Storage 270 days after upload.<br><br>* Files sink to Deep Cold Archive Storage 450 days after upload.<br><br>* Files are deleted 630 days after upload. |
| |* Objects in a single\-AZ bucket support transitioning to the following storage classes: Infrequent Access, Intelligent\-Tiered, Flashback Archive, Archive, Cold Archive, and Deep Cold Archive.<br><br>* Objects in a multi\-AZ bucket support transitioning to the following storage classes: Infrequent Access (multi\-AZ), Intelligent\-Tiered (multi\-AZ), and Flashback Archive (multi\-AZ). For more detailed information about multi\-AZ, see [Multi-AZ Redundancy](https://docs.byteplus.com/docs/tos/Multi-az-redundancy).<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Only the Asia Pacific (Johor) regions support the multi\-AZ redundancy feature.</div><br> |


<span id="f9e5bb73"></span>
## Related Documentation


* [Life Cycle Cost Description](https://docs.byteplus.com/docs/tos/Lifecycle-rules-cost-description)

* [Configure Lifecycle Rules based on Last Modified Time](https://docs.byteplus.com/docs/tos/docs-setting-lifecycle-rules)

* [Configure lifecycle rules based on last access time](https://docs.byteplus.com/docs/tos/Lifecycle-rules-based-on-last-accesstime)

* [Seting prefix overlap](https://docs.byteplus.com/docs/tos/Set-prefix-overlap)
