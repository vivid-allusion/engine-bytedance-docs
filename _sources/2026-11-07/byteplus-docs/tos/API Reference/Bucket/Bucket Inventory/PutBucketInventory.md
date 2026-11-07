---
title: "PutBucketInventory"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/PutBucketInventory"
---

<span id="be7e050e"></span>
## Description

This interface is used to create bucket inventory. After creating the bucket inventory, TOS will output various types of information about the objects by day or week, including the number, size, storage type, and so on.

<span id="d5952e46"></span>
## Precautions


* Only the owner of the bucket and a user with PutBucketInventory privileges can create a bucket inventory.

* You can configure up to 10 bucket inventory rules per bucket.

* The source bucket in which the bucket manifest is created does not need to be the same as the destination bucket in which the manifest file is kept, but it must be in the same region.


<span id="e1635e8f"></span>
## **Request syntax**

```JSON
PUT /?inventory&id=report HTTP/1.1
Host: BucketName.tos-ap-southeast-1.bytepluses.com
Date: Mon, 31 Oct 2016 12:00:00 GMT
Authorization: authorization string
Content-Length: length

{
 "InventoryConfiguration": {
   "Id": "id",
   "IsEnabled": "true",
   "Filter": {
     "Prefix": "Pics/"
   },
   "Destination": {
     "TOSBucketDestination": {
       "Format": "CSV",
       "AccountId": "200000****", 
       "Role": "TosArchiveTOSInventory",
       "Bucket": "destination-bucket",
       "Prefix": "prefix1"
     }
   },
   "Schedule": { "Frequency": "Daily" },
   "IncludedObjectVersions": "All",
   "OptionalFields": {
     "Field": [
       "Size",
       "LastModifiedDate",
       "ETag",
       "StorageClass",
       "IsMultipartUploaded",
       "EncryptionStatus",
       "CRC64",
       "ReplicationStatus"
     ]
   }
 }
}
```


<span id="995cd931"></span>
## Request parameters and headers

For common request headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|inventory |Query |String |Yes |\- |A special identifier representing a PutBucketInventory request. |
|id |Query |String |Yes |report |The name of the bucket inventory, which must remain globally unique under the current bucket. The instructions are as follows:<br><br><br>* The length is 0 to 64 characters.<br><br>* Contains only lowercase letters a\-z, uppercase letters A\-Z, numbers 0\-9, an underscore (\-), an underscore (_), and a period (.).<br><br>* The beginning and end can only be lowercase letters a\-z, uppercase letters A\-Z, and numbers 0\-9.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The <code>id</code>in the header must match the <code>Id</code>of the request element.</div><br> |


<span id="458d0f91"></span>
## **Request body elements**


|**Name** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|InventoryConfiguration |Array |Yes |\- |Bucket inventory rule. |
|Id |String |Yes |report |The name of the bucket inventory, which must remain globally unique under the current bucket. The instructions are as follows:<br><br><br>* The length is 0 to 64 characters.<br><br>* Contains only lowercase letters a\-z, uppercase letters A\-Z, numbers 0\-9, an underscore (\-), an underscore (_), and a period (.).<br><br>* The beginning and end can only be lowercase letters a\-z, uppercase letters A\-Z, and numbers 0\-9.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The <code>id</code>of the request element must match the <code>id</code>in the header.</div><br> |
|IsEnabled |Bool |Yes |true |Whether to enable the bucket inventory feature. The values are as follows:<br><br><br>* `True`: Enable the bucket inventory feature.<br><br>* `False`: The bucket inventory feature is not enabled. |
|Destination |Array |Yes |\- |Information about the manifest file. |
|TOSBucketDestination |Array |Yes |\- |Bucket\-related information for the manifest file.<br><br>Parent Node: Destination |
|Format |String |Yes |CSV |The format of the manifest file. The value is `CSV`, that is, the format of the manifest file is CSV format compressed using GZIP.<br><br>Parent Node: TOSBucketDestination |
|AccountId |String |Yes |200000\*\*\*\* |The account ID of the bucket owner.<br><br>Parent Node: TOSBucketDestination |
|Role |String |Yes |TosArchiveTOSInventory |Role name that grants the object store permission to read all files in the source bucket and write files to the target bucket. This role must have TOS read and write permissions and service access, or you can use the TOS default role `TosArchiveTOSInventory`.<br><br>Parent Node: TOSBucketDestination |
|Bucket |String |Yes |bucket_0001 |Specifies the bucket in which to save the manifest file.<br><br>Parent Node: TOSBucketDestination |
|Prefix |String |No |prefix1 |The storage path prefix for the manifest file.<br><br>Default saved in the target bucket `tos_bucket_inventory/sourceBucketName/inventoryId/YYYY-MM-DDTHH-MMZ/files`path.<br><br>Parent Node: TOSBucketDestination |
|Schedule |Array |Yes |\- |Bucket inventory export cycle information. |
|Frequency |String |Yes |Daily |Cycle of the manifest file export. The values are as follows:<br><br><br>* `Daily`: Export manifest files by day.<br><br>* `Weekly`: Export manifest files by week.<br><br>* `Once`：Export manifest files all at once.<br><br><br>Parent Node: Scheduled |
|Instant |Bool |Yes |true |Whether to enable the instant inventory feature. The values are as follows:<br><br><br>* `true`：Enable the instant inventory feature.<br><br>* `false`：The instant inventory feature is not enabled.<br><br><br>Parent Node: Schedule |
|IncludedObjectVersions |String |Yes |All |The exported object version with the following values:<br><br><br>* `All`: Export all versions of object information.<br><br>* `Current`: Exports the current version of the object information. |
|Filter |Array |No |\- |Prefix for bucket list filtering. After specifying the prefix, the bucket manifest will export only objects that match the prefix setting. |
|Prefix |String |No |Pics/ |Export file prefix matching information, if not set, a manifest of all objects in the bucket is generated by default.<br><br>Parent Node: Filter |
|OptionalFields |Array |No |\- |Information exported from the manifest file. |
|Field |String |No |Size |The manifest file needs to export the information. Multiple selection is supported, and the values are as follows:<br><br><br>* `Size`: The size of the object.<br><br>* `LastModifiedDate`: The last modification time of the object.<br><br>* `ETag`: The ETag value of the object, used to identify the content of the object.<br><br>* `StorageClass`: The storage type of the object.<br><br>* `IsMultipartUploaded`: Whether it is an object uploaded by sharding.<br><br>* `EncryptionStatus`: Whether the object is encrypted.<br><br>* `ReplicationStatus`: Cross\-region replication or co\-region replication status of the object.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The ability to view the replication status of cross\-region replication and co\-region replication of source objects is currently available for beta testing. If you need to use this feature, please contact your account manager.</div><br><br><br>All information is exported by default.<br><br>Parent Node: OptionalFields |


<span id="f4ac8d89"></span>
## **Response headers**

For common response headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).

<span id="fc0fd4e2"></span>
## **Response body elements**

No elements are used.

<span id="344f9462"></span>
## **Sample request**

```JSON
PUT /?inventory&id=report HTTP/1.1
Host: BucketName.tos-ap-southeast-1.bytepluses.com
Date: Sat, 07 Oct 2023 09:02:23 GMT
Authorization: authorization string

{
 "InventoryConfiguration": {
   "Id": "report",
   "IsEnabled": "true",
   "Filter": {
     "Prefix": "Pics/"
   },
   "Destination": {
     "TOSBucketDestination": {
       "Format": "CSV",
       "AccountId": "200000****", 
       "Role": "TosArchiveTOSInventory",
       "Bucket": "destination-bucket",
       "Prefix": "prefix1"
     }
   },
   "Schedule": { "Frequency": "Daily" },
   "IncludedObjectVersions": "All",
   "OptionalFields": {
     "Field": [
       "Size",
       "LastModifiedDate",
       "ETag",
       "StorageClass",
       "IsMultipartUploaded",
       "EncryptionStatus",
       "CRC64",         
       "ReplicationStatus"
     ]
   }
 }
}
```


<span id="a1eb3cf3"></span>
## **Sample response**

```JSON
HTTP/1.1 200 OK
Date: Sat, 07 Oct 2023 09:02:23 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
Content-Length: 0
```
