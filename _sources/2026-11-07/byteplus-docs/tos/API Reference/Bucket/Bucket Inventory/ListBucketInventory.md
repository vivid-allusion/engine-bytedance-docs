---
title: "ListBucketInventory"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/ListBucketInventory"
---

<span id=".5Yqf6IO95o-P6L-w"></span>
## Description

This interface is used to batch retrieve all inventory rules in the bucket.

<span id=".6K-35rGC5raI5oGv5rSL5byP"></span>
## Request syntax

```JSON
GET /?inventory HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 13:59:18 GMT
Authorization: authorization string
```


<span id=".6K-35rGC5Y-C5pWw5ZKM5raI5oGv5aS0"></span>
## Request parameters and headers

This request uses the common request headers; see [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |**Type** |**Required** | ** Sample value** |**Note** |
|---|---|---|---|---|---|
|inventory |Query |String |Yes |\- |Special identifier representing the ListBucketInventory request. |
|continuation\-token |Query |String |No |next_inventory_id |Set the continuation\-token to continue listing the bucket inventory from the last returned list instead of starting over. |


<span id=".6K-35rGC5YWD57Sg"></span>
## Request body elements

No elements are used.

<span id=".5ZON5bqU5raI5oGv5aS0"></span>
## Response headers

This request returns the common response headers; see [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id=".5ZON5bqU5YWD57Sg"></span>
## Response body elements


|**Name** |**Type** |**Sample value** |**Note** |
|---|---|---|---|
|ListInventoryConfigurationsResult |Array |\- |List the results of the bucket inventory rules. |
|InventoryConfiguration |Array |\- |Bucket inventory rules. |
|IsTruncated |Bool |true |Whether to list all inventory tasks. The options are as follows:<br><br><br>* `true`: Not all inventory tasks in the bucket are listed. You can use the value of the `NextContinuationToken` field as the `continuation-token` parameter for the next request to get the next page of inventory configurations.<br><br>* `false`: All inventory tasks in the bucket are fully listed. |
|NextContinuationToken |String |next_inventory_id |This field is returned when the inventory tasks in the bucket are not listed completely. You can use this field as the `continuation-token` parameter for the next request to retrieve the next page of the bucket inventory configuration list. |
|Id |String |report |Bucket inventory name. |
|IsEnabled |Bool |true |Enable the bucket inventory feature. Valid values:<br><br><br>* `true`: Enable the bucket inventory feature.<br><br>* `false`: Disable the bucket inventory feature. |
|Destination |Array |\- |Information related to the inventory file. |
|TOSBucketDestination |Array |\- |Bucket\-related information of the inventory file.<br><br>Parent node: Destination |
|Role |String |TosArchiveTOSInventory |Role name used to grant permission to read all files from the source bucket and write files to the target bucket in object storage. This role must have read and write permissions for TOS and service access rights. You can also use the default TOS role `TosArchiveTOSInventory`. |
|Format |String |CSV |Format of the inventory file. Value `CSV` means the inventory file format is CSV compressed with GZIP.<br><br>Parent node: TOSBucketDestination |
|AccountId |String |200000\*\*\*\* |The account ID of the bucket owner.<br><br>Parent node: TOSBucketDestination |
|Bucket |String |bucket_0001 |The bucket to save the manifest file.<br><br>Parent node: TOSBucketDestination |
|Prefix |String |prefix1 |Storage path prefix of the inventory file.<br><br>Parent node: TOSBucketDestination |
|Schedule |Array |\- |Bucket list export cycle information. |
|Frequency |String |Daily |Inventory file export cycle. Valid values:<br><br><br>* `Daily`: Export the inventory file daily.<br><br>* `Weekly`: Export the inventory file weekly.<br><br><br>Parent node: Schedule |
|IncludedObjectVersions |String |All |Exported object versions. Valid values:<br><br><br>* `All`: Export object information for all versions.<br><br>* `Current`: Export object information for the current version. |
|Filter |Array |\- |Prefix for bucket list filtering. After specifying the prefix, the bucket list will export objects matching the prefix setting. |
|Prefix |String |Pics/ |Export file prefix matching information. If not set, the manifest will include all objects in the bucket by default.<br><br>Parent node: Filter |
|OptionalFields |Array |\- |Information exported from the inventory file. |
|Field |String |Size |Information to be exported in the inventory file. Supports multiple selections, with the following options:<br><br><br>* `Size`: The size of the object.<br><br>* `LastModifiedDate`: The last modification date of the object.<br><br>* `ETag`: The ETag value of the object, used to identify the object's content.<br><br>* `StorageClass`: The storage type of the object.<br><br>* `IsMultipartUploaded`: Whether the object was uploaded via multipart upload.<br><br>* `EncryptionStatus`: Whether the object is encrypted.<br><br>* `CRC64`: The CRC64 value of the object.<br><br>* `ReplicationStatus`: The cross\-region or same\-region replication status of the object.<br><br>* `Tag`: The object tag.<br><br>* `RetentionMode`: The retention mode.<br><br>* `RetainUntilTimestamp`: Retention expiration time.<br><br><br>Parent node: OptionalFields |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
GET /?inventory HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 13:59:18 GMT
Authorization: authorization string
```


<span id=".5ZON5bqU56S65L6L"></span>
## Sample response

```JSON
HTTP/1.1 200 OK
x-tos-id-2: 4fac130beeb50032-a444ed0
x-tos-request-id: 4fac130beeb50032-a444ed0
Date: Fri, 30 Jul 2021 13:59:18 GMT
server: TosServer
Content-Length: 1429

{
  "ListInventoryConfigurationsResult": {
    "InventoryConfiguration": [
      {
        "Id": "report",
        "IsEnabled": "true",
        "Filter": { "Prefix": "Pics/" },
        "Destination": {
          "TOSBucketDestination": {
            "Format": "CSV",
            "AccountId": "200000****",
            "Role": "TosArchiveTOSInventory",
            "Bucket": "test23",
            "Prefix": "prefix1"
          }
        },
        "Schedule": { "Frequency": "Daily" },
        "IncludedObjectVersions": "Current",
        "OptionalFields": {
          "Field": [
            "Size",
            "StorageClass"
          ]
        }
      },
      {
        "Id": "report1",
        "IsEnabled": "true",
        "Filter": { "Prefix": "fast" },
        "Destination": {
          "TOSBucketDestination": {
            "Format": "CSV",
            "AccountId": "200000****",
            "Role": "TosArchiveTOSInventory",
            "Bucket": "test12",
            "Prefix": "tos_bucket_inventory"
          }
        },
        "Schedule": { "Frequency": "Weekly" },
        "IncludedObjectVersions": "Current",
        "OptionalFields": {
          "Field": [
            "IsMultipartUploaded",
            "EncryptionStatus",
            "CRC64",
            "Size",
            "StorageClass",
            "LastModifiedDate",
            "ETag"
          ]
        }
      }
    ],
    "IsTruncated": "false"
  }
}
```
