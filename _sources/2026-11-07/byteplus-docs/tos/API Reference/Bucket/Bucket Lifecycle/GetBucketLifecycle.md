---
title: "GetBucketLifecycle"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-getbucketlifecycle"
---

<span id="a3adda69"></span>
## **Description**

This API is used to get the lifecycle rules of a specified bucket.

<span id="8c92cf93"></span>
## **Request syntax**

```JSON
GET /?lifecycle HTTP/1.1
Host: bucket-name.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
```


<span id="0f57363e"></span>
## **Request parameters and headers**

For common request headers, see [Common parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|---|
|lifecycle |Query |String |Yes |\- |Identifies a GetBucketLifecycle request. |


<span id="f35f9372"></span>
## **Request body elements**

No elements are used.

<span id="fe2d9ab3"></span>
## **Response headers**

For common response headers, see [Common parameters](https://docs.byteplus.com/en/tos/docs/managing-file-labels).

<span id="e42bc015"></span>
## **Response body elements**

<span id="dc37bb5a"></span>
### Common elements


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Rules |Array |\- |The lifecycle rule information. |
|ID |String |id |The unique identifier of the rule. |
|Prefix |String |prefix1/ |Specifies the prefix to which the rule applies. Overlapping prefixes are disallowed.<br><br><br>* If a prefix is specified, the rule applies only to objects in the bucket that have a matching prefix.<br><br>* If no prefix is specified, the rule applies to all objects in the bucket. |
|Status |String |Enabled |Specifies whether the rule is enabled. Valid values:<br><br><br>* `Enabled`: The rule is enabled and executed by TOS regularly.<br><br>* `Disabled`: The rule is not enabled and is ignored by TOS. |
|Tags |Array |\- |You can configure lifecycle rules for objects with specific tags. You can configure up to 10 tags. For more information on tags, see [Managing object tags](https://docs.byteplus.com/en/tos/docs/managing-file-labels).<br><br>Child nodes: Key, Value |
|Key |String |tag |The key of the object tag.<br><br>Parent node: Tags |
|Value |String |value |The value of the object tag.<br><br>Parent node: Tags |
|Filter |Container |\- |The filtering conditions that specify when rules take effect currently only apply within a specified range of object sizes.<br><br>Child nodes: ObjectSizeGreaterThan, GreaterThanIncludeEqual, ObjectSizeLessThan, LessThanIncludeEqual |
|ObjectSizeGreaterThan |Integer |65536 |The rule applies to objects larger than the specified size, in bytes.<br><br>Parent node: Filter |
|GreaterThanIncludeEqual |String |Enabled |Whether to enable the equal condition. It can only be set to `Enabled` or `Disabled`. If not configured, it defaults to `Disabled`. The values are explained as follows:<br><br><br>* `Enabled`: Enable equal conditions, i.e. greater than or equal to.<br><br>* `Disabled`: Not enabling the equal condition, i.e., greater than.<br><br><br>Parent node: Filter |
|ObjectSizeLessThan |Integer |65536 |Set rules to apply to objects smaller than the specified size, in bytes.<br><br>Parent node: Filter |
|LessThanIncludeEqual |String |Enabled |Whether to enable the equal condition. The possible values are `Enabled` and `Disabled`, with `Disabled` being the default if not configured. The values are as follows:<br><br><br>* `Enabled`: Enable equal conditions, i.e. less than or equal to.<br><br>* `Disabled`: Indicate not to enable the equal condition, i.e. less than.<br><br><br>Parent node: Filter |
|Not |Array |\- |Set this lifecycle rule to ignore objects with the specified prefix and tags. |
|Prefix |String |prefix123 |Specify the object prefix to which Not applies instead of configuration.<br><br>Parent node: Not |
|Tags |Array |\- |Specify the object tag to which Not applies.<br><br>Child nodes: Key, Value |
|Key |String |key1 |Specify the tag key to which the Not configuration applies.<br><br>Parent node: Tags |
|Value |String |value1 |Specify the object tag value to which the Not configuration applies.<br><br>Parent node: Tags |


<span id="d1e69c94"></span>
### Elements related to lifecycle rules based on last modification time


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Expiration |Container | |Removes the expired properties of the latest version of the object from the lifecycle rule based on the last modification time. For Buckets with versioning enabled, the specified expiration time is only valid for the current version of the object.<br><br>Child nodes: Days, Date |
|Days |Integer |120 |The number of days the latest version of the object in the lifecycle rule expired and deleted based on the last modification time.<br><br>Parent Node: Expiration |
|Date |String |2024\-01\-31T00:00:00.000Z |The specific date on which the latest version of the object in the lifecycle rule expires and is deleted based on the last modification time. According to the ISO 8601 standard, it is the zero point of UTC.<br><br>Parent Node: Expiration |
|NoncurrentVersionExpiration |Container |\- |Removes the expired property of the historical version object from the lifecycle rule based on the last modification time. Effective only for buckets with version control turned on or suspended, and only for historical versions of objects.<br><br>Child nodes: NoncurrentDays, NonCurrentDate |
|NoncurrentDays |String |30 |The number of days in the lifecycle rule based on the last modification time for the historical version object to expire and be deleted.<br><br>Parent Node: NoncurrentVersionExpiration |
|NonCurrentDate |String |2024\-01\-31T00:00:00.000Z |The specific date on which the historical version object expired and was deleted in the lifecycle rule based on the last modification time. According to the ISO 8601 standard, it is the zero point of UTC.<br><br>Parent Node: NoncurrentVersionExpiration |
|AbortIncompleteMultipartUpload |Container |\- |Specifies the expired property of incomplete multipart uploads (parts).<br><br>Child nodes: DaysAfterInitiation |
|DaysAfterInitiation |Integer |30 |Specifies the lifecycle rule for incomplete multipart uploads (parts), the number of days after multipart uploads have been initialized.<br><br>Parent Node: AbortIncompleteMultipartUpload |
|Transitions |Array |\- |The expiration property of the latest version of the object is settled in the lifetime rule based on the last modification time. For Buckets with versioning enabled, the specified expiration time is only valid for the current version of the object.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If you set up auto\-transition to Infrequent Access Storage, Intelligent Tiering, Flashback Archive, Archive, Cold Archive, Deep Cold Archive and Delete Objects at the same time, the transition time must meet: Infrequent Access Storage < Intelligent Tiering < Flashback Archive < Archive  < Cold Archive < Deep Cold Archive < Delete Objects.</div><br><br><br>Child nodes: StorageClass, Days, Date |
|StorageClass |String |IA |The storage type of the latest version of the object settlement in the lifecycle rule based on the last modification time. The values are as follows:<br><br><br>* `IA`: Infrequent Access Storage.<br><br>* `INTELLIGENT_TIERING`: Intelligent Tiering.<br><br>* `ARCHIVE_FR`: Flashback Archive.<br><br>* `ARCHIVE`: Archive.<br><br>* `COLD_ARCHIVE`: Cold Archive.<br><br>* `DEEP_COLD_ARCHIVE`: Deep Cold Archive.<br><br><br>Parent Node: Transitions |
|Days |Integer |120 |The number of days in which the latest version of the object in the lifecycle rule based on the last modification time has expired and settled must be a positive integer.<br><br>Parent Node: Transitions |
|Date |String |2024\-01\-31T00:00:00.000Z |The specific date on which the latest version of the object in the lifecycle rule expired and settled based on the last modification time. According to the ISO 8601 standard, it is the zero point of UTC.<br><br>Parent Node: Transitions |
|NoncurrentVersionTransitions |Array |\- |The expiration property of a settled version history object in the lifetime rule based on the last modification time. Effective only for buckets with version control turned on or suspended, and only for historical versions of objects.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If you set up auto\-transition to Infrequent Access Storage, Intelligent Tiering, Flashback Archive, Archive, Cold Archive, Deep Cold Archive and Delete Objects at the same time, the transition time must meet: Infrequent Access Storage < Intelligent Tiering < Flashback Archive < Archive  < Cold Archive < Deep Cold Archive < Delete Objects.</div><br><br><br>Child nodes: StorageClass, NoncurrentDays, NonCurrentDate |
|StorageClass |String |IA |The storage type of the historical version object settlement in the lifetime rule based on the last modification time. The storage type of the settlement. The values are as follows:<br><br><br>* `IA`: Infrequent Access Storage.<br><br>* `INTELLIGENT_TIERING`: Intelligent Tiering.<br><br>* `ARCHIVE_FR`: Flashback Archive.<br><br>* `ARCHIVE`: Archive.<br><br>* `COLD_ARCHIVE`: Cold Archive.<br><br>* `DEEP_COLD_ARCHIVE`: Deep Cold Archive.<br><br><br>Parent Node: NoncurrentVersionTransitions |
|NoncurrentDays |Integer |120 |The number of days in which the historical object settled in the lifetime rule based on the last modification time must be a positive integer.<br><br>Parent Node: NoncurrentVersionTransitions |
|NoncurrentDate |String |2024\-01\-31T00:00:00.000Z |The specific date on which the historical version object settled in the lifetime rule based on the last modification time. According to the ISO 8601 standard, it is the zero point of UTC.<br><br>Parent Node: NoncurrentVersionTransitions |


<span id="018204e3"></span>
### Elements related to lifecycle rules based on last access time


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|AccessTimeTransitions |Array |\- |When configuring lifecycle rules based on last access time, the expiration attribute of the most recent version of the object.<br><br>Child nodes: StorageClass, Days |
|StorageClass |String |IA |When configuring lifecycle rules based on last access time, specify the storage class for the latest version objects that have been transitioned. Possible values include:<br><br><br>* `IA`: Infrequent Access Storage.<br><br>* `ARCHIVE_FR`: Flashback Archive.<br><br>* `ARCHIVE`: Archive.<br><br>* `COLD_ARCHIVE`: Cold Archive.<br><br>* `DEEP_COLD_ARCHIVE`: Deep Cold Archive.<br><br><br>Parent node: AccessTimeTransitions |
|Days |Integer |120 |When configuring lifecycle rules based on the last access time, specify the number of days for the latest version objects to expire and settle must be a positive integer.<br><br>Parent node: AccessTimeTransitions |
|NoncurrentVersionAccessTimeTransitions |Array |\- |In lifecycle rules based on last access time, the expiration attribute of historical version objects.<br><br>Child nodes: StorageClass, NoncurrentDays |
|StorageClass |String |IA |When configuring lifecycle rules based on last access time, specify the storage class for the sinking of historical versions objects. The possible values are as follows:<br><br><br>* `IA`: Infrequent Access Storage.<br><br>* `ARCHIVE_FR`: Flashback Archive.<br><br>* `ARCHIVE`: Archive.<br><br>* `COLD_ARCHIVE`: Cold Archive.<br><br>* `DEEP_COLD_ARCHIVE`: Deep Cold Archive.<br><br><br>Parent node: NoncurrentVersionAccessTimeTransitions |
|NoncurrentDays |Integer |60 |When configuring lifecycle rules based on last access time, the number of days specified for the expiration and transition of historical versions objects must be a positive integer.<br><br>Parent node: NoncurrentVersionAccessTimeTransitions |


<span id="48ee0cda"></span>
## **Sample request**

```JSON
GET /?lifecycle HTTP/1.1
Host: bucket-name.tos-ap-southeast-1.bytepluses.com
Date: Mon, 14 Apr 2021 01:17:29 GMT  
Authorization: authorization string
```


<span id="16e0fcde"></span>
## **Sample response**

<span id="826eaf1a"></span>
### **Sample response 1**

Lifecycle rules based on last modification time

```JSON
HTTP/1.1 200 OK
Date: Fri, 30 Jul 2021 13:53:55 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
Content-Length: ***
{
    "Rules": [
    {
      "ID": "id",
      "Prefix": "prefix1/",
      "Status": "Enabled",
      "Expiration": { "Days": 120 },
    },
    {
      "ID": "id",
      "Prefix": "prefix2/",
      "Status": "Enabled",
      "AbortIncompleteMultipartUpload": { "DaysAfterInitiation": 10 }
    }]
}
```


<span id="c687af55"></span>
### **Sample response 2**

Lifecycle rules based on last access time

```Bash
HTTP/1.1 200 OK
Date: Fri, 03 Jan 2025 13:53:55 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
Content-Length: ***
{
    "Rules": [
        {
            "ID": "aaa",
            "Prefix": "",
            "Status": "Enabled",
            "Tags": [
                {
                    "Key": "key",
                    "Value": "value"
                }
            ],
            "Filter": {
                "ObjectSizeGreaterThan": 1048576,
                "GreaterThanIncludeEqual": "Disabled",
                "ObjectSizeLessThan": 2072576,
                "LessThanIncludeEqual": "Disabled"
                "Not": [
                    {
                        "Prefix": "prefix123",
                        "Tags": [{
                            "Key": "key1",
                            "Value": "value1"
                        }]
                    }
                ]
            },
            "AccessTimeTransitions": [
                {
                    "StorageClass": "ARCHIVE",
                    "Days": 180
                }
            ],
            "NoncurrentVersionAccessTimeTransitions": [
                {
                    "StorageClass": "ARCHIVE",
                    "NoncurrentDays": 180
                }
            ]
        }
    ]
}
```


<span id="b3cdad2d"></span>
### **Sample response 3**

If no lifecycle rules are set, a sample response similar to the following example is returned.

```JSON
{
  "Error": {
    "Code": "NoSuchLifecycleConfiguration",
    "RequestId": "936901f5f9aa32d663f5f9aa-ac192267-1pUn7K-GBL-cq-tos_front",
    "HostId": "fWBVJIQESfYijNMMUzZkucybHUTgEyaF",
    "Message": "The bucket lifecycle configuration does not exist"
  }
}
```
