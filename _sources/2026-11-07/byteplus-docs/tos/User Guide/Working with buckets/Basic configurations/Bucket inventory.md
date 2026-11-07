---
title: "Bucket inventory"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Bucket-inventory"
---

You can use the bucket inventory feature to regularly obtain information about specified objects in your bucket and save it to a designated bucket. This topic introduces the use cases and steps involved in using the feature.

<span id=".5L2_55So5Zy65pmv"></span>
## Use cases

You can use this feature to create inventory lists on a schedule that you define, for either a given bucket, or objects that share a prefix. Inventory lists include object size, storage type, last update date, ETag, shard upload status, and encrypted state.

If you need to list a large number of objects, we recommend using the bucket inventory feature.

<span id="76ae9212"></span>
## Permissions required


* By default, the owner of an account has full permissions. Identity and Access Management (IAM) users have no permissions by default. If an IAM user needs to perform any of the following operations, the account owner must grant the user the appropriate permissions using an [IAM](https://docs.byteplus.com/en/docs/tos/docs-overview_6) or [Bucket policy](https://docs.byteplus.com/en/docs/tos/docs-overview_5).

   * Create bucket inventory rules: `tos:PutBucketInventory`

   * View bucket inventory configurations: `tos:GetBucketInventory`

   * Delete bucket inventory rules: `tos:DeleteBucketInventory`

* Before configuring a bucket inventory rule for the first time, you must use Identity and Access Management (IAM) to grant TOS permission to read all objects from the source bucket and write objects to the destination bucket. We recommend granting these permissions via the console. After successful authorization, IAM will automatically generate the `TosArchiveTOSInventory` role. You can log in to the [IAM console](https://console.byteplus.com/iam/identitymanage/role)I to view this role.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you have configured bucket or IAM policies for your business, make sure that the following actions relating to the generation of bucket inventory lists are not explicitly denied, since doing so may cause the generation to fail:   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">PutObject   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">CreateMultipartUpload   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">UploadPart   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">CompleteMultipartUpload   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">HeadObject   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">ListObjects   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">SetObjectMeta   </div>
   

* By default, the `TosArchiveTOSInventory` role does not have permission to access Key Management Service (KMS) keys. If your bucket is encrypted with SSE\-KMS, you must authorize the `KMSCryptoUserAccess` role before creating a bucket inventory rule. Otherwise, the generation will fail.


<span id=".5riF5Y2V5paH5Lu26K-05piO"></span>
## Inventory files

<span id=".5paH5Lu25qC85byP"></span>
### File format

Once a bucket inventory rule has been created, TOS will generate inventory list files based on the configured parameters. The following example illustrates the path structure of the inventory list files.

```Plain Text
destinationPrefix/sourceBucketName/inventoryId/YYYY-MM-DDTHH-MMZ/files/UUID.csv.gz

dest_bucket
 └──destinationPrefix/
     └──sourceBucketName/
         └──inventoryId/
             ├──YYYY-MM-DDTHH-MMZ/
                  ├──files/
                       ├──7fd76a1c421391260a481a3405c6****_0.csv.gz
                       ├──7fd76a1c421391260a481a3405c6****_1.csv.gz
                       ├──8s5sda632dwa89s2das3dw9dsa2s****_0.csv.gz
                        ....
                  ├──manifest.json
                  ├──manifest.checksum
```


The parameters are described below:


|**Parameter** |**Description** |
|---|---|
|destinationPrefix/ |Specifies the path prefix for storing inventory reports in the destination bucket. If no prefix is defined, the default prefix `tos_bucket_inventory` will be used. |
|sourceBucketName/ |Specifies the bucket from which the inventory file was generated. |
|inventoryId/ |Specifies the name of the bucket inventory rule. |
|YYYY\-MM\-DDTHH\-MMZ/ |Specifies the time when scanning of the stored objects began during the generation of the inventory file, in UTC time and formatted as `YYYY-MM-DDTHH-MMZ`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Objects uploaded after this time will not be recorded in the inventory file.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For bucket inventory rules created before July 15, 2025 and left unchanged, the timestamp format is YYYY\-MM\-DDTHH:MMZ. </div><br> |
|files/ |Specifies the directory in which the inventory file is stored. The default is `files/`. Inventory files are formatted as `UUID.csv.gz`, with the default format being `.csv.gz`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">For more information, see <a href="https://docs.byteplus.com/docs/tos/Bucket-inventory#fileschema">Inventory file parameters</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If a substantial amount of data is exported, TOS automatically splits the inventory file into smaller segments to make processing easier. These files are named in sequential order, for example <code>UUID_0</code>, <code>UUID_1</code> and so on.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The <code>files</code> directory may contain non\-unique UUIDs. For example, multiple files such as <code>UUIDA_0</code>, <code>UUIDB_0</code> and <code>UUIDB_1</code> may coexist.</div><br> |
|manifest.json |A file that stores the metadata and other information of the inventory file. For more information, see [manifest.json](https://docs.byteplus.com/docs/tos/Bucket-inventory#manifest-json). |
|manifest.checksum |Specifies the MD5 checksum of the manifest.json file, for example `79b1e0cbe3af7fdf127b91af601b****`. |


<span id="manifest-json"></span>
### manifest.json

The following example illustrates a `manifest.json` file, together with its description.

```json
{    "creationTimestamp":"1672682400",
     "sourceBucket":"srctest",
     "destinationBucket":"destest",
     "fileFormat":"CSV",
     "fileSchema":"BucketName,ObjKey,Size,ETag,StorageClass,LastModifiedDate,IsMultipartUploaded,EncryptionStatus",
     "version":"2022-11-14",
     "files":[{
         "Key":"tos_bucket_inventory/destest/srctest/2023-01-03T02-00Z/files/7fd76a1c421391260a481a3405c6****_0.csv.gz",
         "Size":619,
         "MD5checksum":"79b1e0cbe3af7fdf127b91af601b****",
         "InventoriedRecord":17
         }]
}
```



|**Parameter** ||**Description** |
|---|---|---|
|creationTimestamp ||A Unix timestamp in seconds showing when scanning of the source bucket began. |
|sourceBucket ||Specifies the bucket from which the inventory file was generated. |
|destinationBucket ||Specifies the bucket in which the inventory file is stored. |
|fileFormat ||Specifies the format of the inventory file. The default is `CSV`. |
|fileSchema ||Specifies the object details included in the inventory file. For more information, see [fileSchema](https://docs.byteplus.com/docs/tos/Bucket-inventory#fileschema). |
|version ||Specifies the version number of the inventory file. |
|files |Key |Specifies the full path and filename of the inventory file. |
||Size |Specifies the size of the inventory file in bytes. |
||MD5checksum |Specifies the MD5 checksum of the inventory file. |
||InventoriedRecord |Specifies the number of records in the inventory file. |


<span id="fileschema"></span>
### fileSchema

Here is a screenshot of a fileSchema file.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bc9969dadb104eaca0c3d5fca2bb4792~tplv-goo7wpa0wc-image.image) </span>

FileSchema files do not include parameter names. The parameter names shown in the screenshot are for reference purposes only. The detailed descriptions of the parameters are as follows:


|**Parameter** |**Required** |**Description** |
|---|---|---|
|BucketName |Yes |Specifies the name of the source bucket. |
|ObjKey |Yes |Specifies the name of the object.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Object names are URL\-encoded and must be decoded before use.</div><br> |
|VersionId |Yes |Specifies the version ID of the object.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter only appears when versioning is enabled for the bucket and the Object version is set to All versions.</div><br> |
|IsLatest |Yes |Specifies whether the object version is the latest version. The fields are described as follows:<br><br><br>* **TRUE**: The object is the latest version.<br><br>* **FALSE**: The object is a historical version.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter only appears when versioning is enabled for the bucket and the Object version is set to All versions.</div><br> |
|IsDeleteMarker |Yes |Specifies whether the object version is a deletion mark. The fields are described as follows:<br><br><br>* **TRUE**: The object version is a deletion mark.<br><br>* **FALSE**: The object version is not a deletion mark.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter only appears when versioning is enabled for the bucket and the Object version is set to All versions.</div><br> |
|Size |No |Specifies the size of the object in bytes. |
|ETag |No |Specifies the ETag of the object. |
|StorageClass |No |Specifies the storage type of the object. The fields are described as follows:<br><br><br>* **STANDARD**: Standard Storage.<br><br>* **IA**: Infrequent Access Storage.<br><br>* **INTELLIGENT_TIERING**: Intelligent Tiering Storage.<br><br>* **ARCHIVE_FR**: Flashback Archive.<br><br>* **ARCHIVE**: Archive.<br><br>* **COLD_ARCHIVE**: Cold Archive.<br><br>* **DEEP_COLD_ARCHIVE**: Deep Cold Archive. |
|IntelligentTieringAccessTier |No |Specifies the Intelligent Tiering access tier in which the object is stored. The fields are described as follows:<br><br><br>* **Frequent access tier**: FREQUENT<br><br>* **Infrequent access tier**: INFREQUENT<br><br>* **Flashback archive tier**: ARCHIVEFR |
|LastModifiedDate |No |Specifies the date on which the object was last modified. This is written in Unix timestamp format and is measured in seconds. |
|IsMultipartUploaded |No |Specifies whether the object was uploaded via multipart upload. The fields are described as follows:<br><br><br>* **TRUE**: The object was uploaded via multipart upload.<br><br>* **FALSE**: The object was not uploaded via multipart upload. |
|EncryptionStatus |No |Specifies whether the object is encrypted. The fields are described as follows:<br><br><br>* **TRUE**: The object is encrypted.<br><br>* **FALSE**: The object is not encrypted. |
|CRC64 |No |Specifies the CRC64 value of the object, which is commonly used to verify data integrity. For more information, see [Checking data integrity](https://docs.byteplus.com/docs/tos/Overview10). |
|ReplicationStatus |No |Specifies the cross\-region or same\-region replication status of the object:<br><br><br>* If the object is the source for cross\-region or same\-region replication, the replication status values are:<br><br>   * **COMPLETE**: Replication completed.<br><br>   * **PENDING**: Replication in progress.<br><br>   * **FAILED**: Replication failed.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The feature that allows you to view the replication status of source objects is currently in closed beta. Contact your account manager for access.</div><br><br><br><br>* If the object is a target for cross\-region or same\-region replication, the value **REPLICA** is displayed to indicate that it is a replicated object.<br><br>* If the object is neither a source nor a target for replication, this field will be empty. |
|Tag |No |Specifies the tag(s) assigned to the object. The format is `key1#value1;key2#value2;`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Object tag keys and values are URL\-encoded and must be decoded before use.</div><br> |
|RetentionMode |No |Specifies the retention policy mode of the object. The fields are described as follows:<br><br><br>* **COMPLIANCE**: Compliance mode.<br><br>* **NONE**: No retention policy is set for the object. |
|RetainUntilTimestamp |No |Specifies the time at which the object's retention period expires. This is written in Unix timestamp format and is measured in seconds. |
|LastAccessTime |No |Specifies when the object was last accessed.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The LastAccessTime parameter is currently in closed beta. Please contact your account manager for access.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The last access time of objects is updated only when the <strong>Access monitor</strong> feature is enabled. To view the <strong>last access time</strong>, enable the <strong>Access monitor</strong> option on the <strong>Lifecycle</strong> page. For instructions, see <a href="https://docs.byteplus.com/en/docs/tos/Lifecycle-rules-based-on-last-accesstime#cebe8b4c">Enable access monitor</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">TOS calculates the last access time of objects from the day access monitor is enabled. The access time of an object is updated only when at least 24 hours have passed since the last access request for that object. For example, downloading an object at 8:00 a.m. on January 1 records the access time as 8:00 a.m. on January 1. Any download requests made before 8:00 a.m. on January 2 will not update the access time. The access time will update only if you download the object again after 8:00 a.m. on January 2. For more information, see <a href="https://docs.byteplus.com/en/docs/tos/Which-operations-update-the-lastaccesstime">Which operations update an object's last access time?</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The last access time of an object may not always be accurate. For example, if the server is busy, the last access time of some objects may not update after they are accessed. Therefore, do not rely on this information for data cleanup.</div><br> |


<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


|**Category** |**Description** |
|---|---|
|Billing |Using the bucket inventory feature incurs costs for storing inventory files. For billing details, see [Billing overview](https://docs.byteplus.com/docs/tos/docs-billing-overview). |
|Number of bucket inventory rules |You can configure each bucket with up to ten bucket inventory rules. |
|Configuring bucket inventory rules |* The inventory files can be generated and stored in different buckets, but these buckets must be in the same region and under the same account.<br><br>* Currently, the bucket inventory feature only supports creating lists of all objects or objects with a shared prefix within a given bucket.<br><br>* If you have created multiple inventory rules within a single bucket, the filtering scope of each rule must not overlap with that of any other rule. TOS automatically validates the filtering scope. If any overlaps are detected, the filtering scope of any existing rules must first be deleted or modified. Otherwise, creation of a new rule will fail. |
|Generation time |The first time you configure a bucket inventory rule, TOS will load the rules within 24 hours for FNS buckets and within 48 hours for HNS buckets. If there are fewer than 10 billion objects in a bucket, an inventory report is usually generated within 24 hours of the rule being loaded. If the number exceeds 10 billion, the generation time increases accordingly.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If you need to execute an inventory rule for an FNS bucket immediately, see <strong>Execute a bucket inventory rule immediately</strong> under <a href="https://docs.byteplus.com/en/docs/tos/Bucket-inventory?lang=zh&TagIDs=2,348#.5YW25LuW5pON5L2c">Other operations</a>.</div><br> |
|Object quantity |TOS supports **daily** or **weekly** exports of inventory files. We recommend setting the export frequency according to the number of objects.<br><br><br>* Number of objects < 10 billion: Daily or weekly exports are acceptable.<br><br>* Number of objects between 10 billion and 50 billion: Weekly exports are recommended.<br><br>* Number of objects \> 50 billion: We recommend specifying object prefixes and exporting files in batches. |
|Editing a bucket inventory rule |If you edit a bucket inventory rule while it is being executed, the changes may appear in inventory files generated on or after the day the rule was edited. For this reason, we recommend using inventory files generated one day after the rule was modified. |
|Deleting a bucket inventory rule |If you delete a bucket inventory rule while it is being executed, some inventory files may remain in the directory and the generation of new files may stop. |
|Others |* Exporting inventory files uses bandwidth. If your bucket has limited bandwidth, you can choose a different one to store your inventory files and avoid using the source bucket's bandwidth.<br><br>* No inventory file will be generated if the source bucket contains no files or if the configured inventory rules do not match any objects.<br><br>* During the export process, if objects are written to or updated in the bucket, the corresponding information may not be captured in the inventory file.<br><br>* To reduce storage costs, delete any unnecessary inventory files. Similarly, if you no longer require periodic inventory reports, you can delete the configured bucket inventory rules. |


<span id=".5pON5L2c5q2l6aqk"></span>
## Steps


1. Log in to the [TOS console](https://console.byteplus.com/tos) .

2. In the left navigation pane, click **Buckets**.

3. In the top menu bar, select the project of the bucket you want to manage.

4. On the **Buckets** page, click the name of the bucket.

5. In the left navigation pane, select **Basic configurations \> Bucket inventory**.

6. On the **Create bucket inventory** page, click **Create inventory**.

7. On the **Create bucket inventory** page, set the following parameters:

   
   |**Parameter** |**Description** |
   |---|---|
   |Status |Select whether to activate the bucket inventory rule. The options are **Enabled** and **Disabled**. |
   |Rule name |Specify the name of the bucket inventory rule. Rule names must:<br><br><br>* Be between 1 and 64 characters.<br><br>* Contain only numbers, hyphens (\-), letters, underscores (_) and periods (.).<br><br>* Start and end with a number or letter. |
   |Target bucket |Select the bucket in which the inventory file will be stored.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If you have given all users permission to read and write the bucket, there is a risk of inventory files being leaked.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The bucket must be in the same region as the source bucket.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">You cannot store inventory files in a bucket whose storage type is Archive, Cold Archive, or Deep Cold Archive.</div><br> |
   |Inventory report prefix |Specify the path prefix for storing inventory files in the destination bucket. If no prefix is defined, the default prefix `tos_bucket_inventory` will be used. Naming rules:<br><br><br>* Prefixes can contain Chinese characters, letters, numbers, and common symbols.<br><br>* Prefixes cannot start with a forward slash (/) or backslash (\). Consecutive forward slashes (/) are not allowed.<br><br>* `..` cannot be used as a directory name.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For more information, refer to the file format section above.</div><br> |
   |Report output format |Use the following options to configure the inventory report output format:<br><br><br>* **Compressed**: The inventory report is compressed and stored in the destination bucket in csv.gz format.<br><br>* **Uncompressed**: The inventory report is stored in the destination bucket in csv format.<br><br><br>The default **Report output format** is **Compressed**, which can reduce storage costs. |
   |Report export cycle |Select a cycle for report export. You can choose **weekly**, **daily**, or **one\-off**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">One\-off report exports run only once.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you need to include a large number of objects, we recommend exporting the reports on a weekly basis.</div><br> |
   |Object version |Select the object versions to be exported. You can choose either **Current version** or **All versions**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter only applies to buckets that have versioning enabled.</div><br> |
   |Filter settings |Configure the scope of objects and information to be included in inventory reports:<br><br><br>* **Match by prefix**: Use a prefix to filter objects. If no prefix is specified, inventory reports will include all objects in the bucket.<br><br>* **Conditional filtering**: Set conditions to filter objects. Supported conditions include **Object size**, **Creation time**, **Modification time**, **Filter tag**, **Storage type**, and **Object type**.<br><br>* **List content information**: Select the information to be included in inventory reports. The following options are available: **Object size**, **Storage type**, **Intelligent Tiering: Access Layer**, **Last update date**, **ETag**, **Shard upload status**, **Encrypted state**, **CRC64**, **Replication state**, **Tag**, ** Retention mode**, **Retention expiration time and last access time**. For more information, see [fileSchema](https://docs.byteplus.com/docs/tos/Bucket-inventory#fileschema).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Exporting <strong>last access time</strong> is currently in closed beta. Please contact your account manager for access.</div><br> |
   

8. Once you have finished configuring, click **Create**.


<span id=".5YW25LuW5pON5L2c"></span>
## Other operations


* **Edit a bucket inventory rule**: Click **Edit** in the **Actions** column of the rule you want to modify.

* **Delete a bucket inventory rule**: Click **Delete** in the **Actions** column of the rule you want to remove, and confirm the deletion by clicking **Delete** in the box that appears.

* **Execute a bucket inventory rule immediately**: Click **Execute immediately** in the **Actions** column of the rule you want to execute. Then, click **OK** in the box that appears to Create Instant Inventory.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">This operation is only available for FNS buckets.   </div>
   

* **Preview a bucket inventory rule**: Click **Preview List** in the **Actions** column of the rule you want to check. Then, view the list directory names and list results in the box that appears. You can filter the list results by date. To view list results, click **View List Results**. The following information is available: **Source bucket**, **Target bucket**, **Total number of objects**, **Total object size**, **Manifest file format**, **The version number of the manifest file**, **Inventory file**, and **Size**. To download list results, click **Download** in the Actions column.


<span id="7ea76b59"></span>
## Troubleshooting


* [The inventory file has not yet been generated – why is that?](https://docs.byteplus.com/docs/tos/Bucket-inventory2#2ca51210)

* [What factors might affect the speed at which the inventory file is exported?](https://docs.byteplus.com/docs/tos/Bucket-inventory2#8fbc3ce4)
