---
title: "Restoring objects"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-restoring-files"
---

Objects in Archive, Cold Archive, or Deep Cold Archive storage types need to be restored before they can be accessed. This document explains how to restore objects from Archive, Cold Archive, or Deep Cold Archive.

<span id="77e0703f"></span>
## Restoration instructions

Objects in Archive, Cold Archive, or Deep Cold Archive must be restored before they can be accessed. The restoration process is as follows:


1. Perform a restoration operation on the target object. Archive objects require setting a copy expiration period; Cold Archive and Deep Cold Archive types require setting both a copy expiration period and a restoration mode; the restoration time details are as follows:

   
   |**Storage type** |**Restoration time** |
   |---|---|
   |Archive |Restoration time for Archive objects is within 1 minute. |
   |Cold Archive |The restoration time for Cold Archive objects depends on the restoration mode you select. The retrieval times and charges of different restoration modes vary; the faster the retrieval, the higher the price. Please choose the appropriate restoration mode according to your actual needs. Description of restoration modes is as follows:<br><br><br>* **Quick retrieval**: Generally completes restoration within 1 to 5 minutes. Suitable for scenarios where urgent object retrieval is needed.<br><br>* **Standard retrieval**: Generally completes restoration within 2 to 5 hours.<br><br>* **Batch retrieval**: Generally completes restoration within 5 to 12 hours.<br><br><br>Each BytePlus account's retrieval capacity reference value: an average of 500 objects per second, with a total retrieval volume of 100–150 TiB per day across three restoration modes. |
   |Deep Cold Archive |The restoration time for Deep Cold Archive objects depends on the restoration mode you choose. Different restoration modes have different retrieval times and billing; the faster the retrieval, the higher the price. Please choose the appropriate restoration mode based on your actual needs. Description as follows:<br><br><br>* **Standard retrieval**: Generally completes restoration within 12 hours.<br><br>* **Batch retrieval**: Generally completes restoration within 48 hours.<br><br><br>Each BytePlus account has a reference retrieval rate: On average, 100 objects per second, and the total retrieval volume for both restoration modes is 10–15 TiB per day. |
   

2. After object restoration, TOS will generate a temporary copy of Standard Storage type for your access and operations. The copy will be automatically deleted after the expiration period you set.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Any modifications to storage type, metadata edits, or tag editing for restored objects will directly affect the original data.   </div>
   

3. After the copy is automatically deleted at the end of the expiration period, the object will revert back to its archived, cold archived, or deep cold archived state and will not be accessible. Reading the object again requires restoration.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The copy will expire at 00:00:00 UTC after the validity period ends. For example, if you generated a copy for an object on October 10, 2023, at 10:00:00 with a validity period of 5 days, the object will be frozen again on October 16, 2023, at 00:00:00.   </div>
   

<span id="f2aa0d3e"></span>
## Billing notes


* Restoring objects from Archive will incur data retrieval costs. Restoring objects from Cold Archive or Deep Cold Archive will incur data retrieval costs and request charges. For detailed information, please see [Data retrievals](https://docs.byteplus.com/docs/tos/docs-data-retrieval-fee) and [Requests](https://docs.byteplus.com/docs/tos/docs-request-fee).

* After the restoration of Archive, Cold Archive, or Deep Cold Archive objects is complete, a temporary copy will be created for your access. The copy is of Standard Storage and will be billed as such during its validity. For more details, please see [Temporary storage](https://docs.byteplus.com/docs/tos/docs-temporary-storage-fee).

* If you delete an object in Archive, Cold Archive, or Deep Cold Archive before the copy expires, the copy will also be deleted. Storage capacity fees will then be calculated based on the actual storage duration of the copy, rather than the validity period. For detailed information, please see [Storage](https://docs.byteplus.com/docs/tos/docs-storage-fee).


<span id="56ae80b7"></span>
## Restore a single object


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. On the navigation pane on the left, click **Buckets**. In the **Buckets** list, click the bucket you want to manage.

3. On the **Objects** page, click on the **Actions** column's **Restore** for the target object.

4. In the **Restore Object** dialog, set the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |Current Status |Default to **not restored**. |
   |Copy Validity Period |Set the validity period of the copy. The validity period must be a positive integer, ranging from 1 to 365, measured in days.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Copies will be charged according to the Standard Storage type during their validity period until they are automatically deleted upon expiration. For detailed instructions, see <a href="https://docs.byteplus.com/docs/tos/docs-temporary-storage-fee">Temporary storage</a>.</div><br> |
   |Restoration Mode |Restoration modes for Cold Archive or Deep Cold Archive objects need to be set only during restoration. The shorter the restoration time, the higher the unit price. Description as follows:<br><br><br>* Restoration modes for Cold Archive objects<br><br>   * **Quick retrieval**: Typically completes restoration within 1 to 5 minutes.<br><br>   * **Standard retrieval**: Typically completes restoration within 2 to 5 hours.<br><br>   * **Batch retrieval**: Typically completes restoration within 5 to 12 hours.<br><br>* Restoration modes for Deep Cold Archive objects<br><br>   * **Standard retrieval**: Typically completes restoration within 12 hours.<br><br>   * **Batch retrieval**: Typically completes restoration within 48 hours. |
   

5. After setting the parameters, click **Restore**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">During the object restoration process, you can click on the <strong>Restore</strong> option in the operation column of the target object to view the restoration status of the object.   </div>
   

<span id="d71eaa99"></span>
## Batch object restoration

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The restoration modes supported by objects in archive storage, cold archive, and deep cold archive types vary. If you select multiple types of storage objects during a batch restoration operation, only the objects that support the selected restoration mode will be restored; other objects that do not support this mode will result in an error.</div>



1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. On the navigation pane on the left, click **Buckets**. In the **Buckets** list, click the bucket you want to manage.

3. On the **Objects** page, select the objects or folders you want to batch restore, and then click **Restore** at the bottom left of the object list.

4. In the **Restore Object** dialog, set the following parameters.

   
   |**Parameters** |**Description** |
   |---|---|
   |Restoration Mode |When restoring objects, you need to set the restoration mode. The shorter the restoration time, the higher the price. Supports three restoration modes:<br><br><br>* **Quick retrieval**: Supports the restoration of archive storage and cold archive objects. The restoration times for objects of each storage type in this mode are as follows:<br><br>   * Archive: Restoration is generally completed within 1 minute.<br><br>   * Cold Archive: Restoration is generally completed within 1 to 5 minutes.<br><br>* **Standard retrieval**: Supports the restoration of archive storage, cold archive, and deep cold archive objects. The restoration times for objects of each storage type in this mode are as follows:<br><br>   * Archive: Restoration is generally completed within 1 minute.<br><br>   * Cold Archive: Restoration is generally completed within 2 to 5 hours.<br><br>   * Deep Cold Archive: Restoration is generally completed within 12 hours.<br><br>* **Batch retrieval**: Supports the restoration of Cold Archive and Deep Cold Archive objects. The restoration times for objects in different storage types are described as follows:<br><br>   * Cold archive: Generally restored within 5 to 12 hours.<br><br>   * Deep cold archive: Generally restored within 48 hours. |
   |Copy Validity Period |Set **Copy Validity Period**. The validity period must be a positive integer, ranging from 1 to 365, measured in days.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Copies will be charged according to the Standard Storage type during their validity period until they are automatically deleted upon expiration. For detailed instructions, see <a href="https://docs.byteplus.com/docs/tos/docs-temporary-storage-fee">Temporary storage</a>.</div><br> |
   

5. After setting the parameters, click **Restore**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">During the object restoration process, you can click the <strong>Restore </strong>button in the operation column of the target object to check the restoration status of the object.   </div>
   

<span id="b9f763e2"></span>
## Modify the validity period of the copy

Once a copy has expired and been deleted automatically, the related object reverts to its original state (Archive, Cold Archive, or Deep Cold Archive) and becomes unreadable. Restore it to regain access. To extend the validity period of a copy, follow the steps below before the copy expires. Otherwise, you will have to pay for data retrieval again.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, only extensions of the copy validity period are supported, not reductions.</div>



1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. On the navigation pane on the left, click **Buckets**. In the **Buckets** list, click the bucket you want to manage.

3. On the **Objects** page, click on the **Actions** column's **Restore** for the target object.

4. In the **Restore Object** dialog, set the validity period for the copies, then click **Restore**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The validity period of the copy should be a positive integer, ranging from 1 to 365 days.   </div>
   

<span id="7516ae3d"></span>
## API documentation


|**API** |**Description** |
|---|---|
|[RestoreObject](https://docs.byteplus.com/docs/tos/reference-restoreobject) |Invoke the RestoreObject interface to restore objects from archive, cold archive, and deep cold archive storage types. |
