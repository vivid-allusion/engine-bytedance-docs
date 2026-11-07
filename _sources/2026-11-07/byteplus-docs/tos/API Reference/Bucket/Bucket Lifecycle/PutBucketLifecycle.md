---
title: "PutBucketLifecycle"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-putbucketlifecycle"
---

<span id="615fec68"></span>
## **Introduction**

This API is used to set lifecycle rules for a bucket. After lifecycle rules are enabled, TOS automatically changes the storage type of files (objects) or deletes them on the expiration date specified in the rules.

<span id="hLjWoCRt"></span>
## **Notes**


* The JSON\-serialized lifecycle rules for a bucket cannot exceed 20 KB in size.

* This API must be called by the bucket owner or subaccounts of the bucket owner with the PutBucketLifecycle permission for the bucket. For detailed instructions on how to achieve access control using bucket policies, see [Bucket policy management](https://docs.byteplus.com/en/tos/docs/overview_5).

* If you have not set lifecycle rules, calling this API creates them. If you have done so, calling this API overwrites the existing rules.

* PutBucketLifecycle operates in an overwriting manner. To introduce additional lifecycle rules, call the GetBucketLifecycle API to get the current lifecycle rules, append the new rules, and then update the old configuration using the PutBucketLifecycle API.


<span id="58e99814"></span>
## **Request syntax**

```JSON
PUT /?lifecycle HTTP/1.1
Host: bucket-name.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
Content-Length: ContentLength
Content-MD5: MD5
{
    "Rules": [{
      "ID": "id",
      "Prefix": "prefix",
      "Status": "Enabled",
      "Tags": [
                {
                    "Key": "key",
                    "Value": "value"
                }
            ],
            "Filter": {
                "ObjectSizeGreaterThan": 65536,
                "GreaterThanIncludeEqual": "Enabled",
                "ObjectSizeLessThan": 10485760,
                "LessThanIncludeEqual": "Disabled",
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
      "Expiration": { "Days": 120 },
      "NoncurrentVersionExpiration": { "NoncurrentDays": 120 },
      "AbortIncompleteMultipartUpload": { "DaysAfterInitiation": 10 },
      "Transitions": [
        {
          "StorageClass": "IA",
          "Days": 30
        },
        {
          "StorageClass": "COLD_ARCHIVE",
          "Days": 60
        }
      ],
      "NoncurrentVersionTransitions": [
        {
          "StorageClass": "IA",
          "NoncurrentDays": 30
        },
        {
          "StorageClass": "COLD_ARCHIVE",
          "NoncurrentDays": 60
        }
      ]
    }]
}
```


<span id="91b57ba8"></span>
## **Request parameters and headers**

For common request headers, see [Common parameters](https://docs.byteplus.com/en/tos/reference/overview).


|**Name** |**Location** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|---|
|lifecycle |Query |String |Yes |\- |Identifies a PutBucketLifecycle request. |


<span id="88baf21d"></span>
## **Request body elements**

<span id="9992e6b5"></span>
### Common elements


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Rules |Array |Yes |\- |The lifecycle rule information. |
|ID |String |No |id |The unique identifier of the rule. |
|Prefix |String |No |prefix |Specifies the prefix to which the rule applies. Overlapping prefixes are disallowed.<br><br><br>* If a prefix is specified, the rule applies only to objects in the bucket that have a matching prefix.<br><br>* If no prefix is specified, the rule applies to all objects in the bucket. |
|Status |String |Yes |Enabled |Specifies whether the rule is enabled. Valid values:<br><br><br>* `Enabled`: The rule is enabled and executed by TOS regularly.<br><br>* `Disabled`: The rule is not enabled and is ignored by TOS. |
|Tags |Array |No |\- |You can configure lifecycle rules for objects with specific tags. You can configure up to 10 tags. For more information on tags, see [Managing file tags](https://docs.byteplus.com/en/tos/docs/managing-file-labels).<br><br>Child nodes: Key, Value |
|Key |String |No |tag |The key of the object tag.<br><br>Parent node: Tags |
|Value |String |No |value |The value of the object tag.<br><br>Parent node: Tags |
|Filter |Container |No |\- |The filtering conditions that specify when rules take effect currently only apply within a specified range of object sizes.<br><br>Child nodes: ObjectSizeGreaterThan,GreaterThanIncludeEqual,ObjectSizeLessThan,LessThanIncludeEqual |
|ObjectSizeGreaterThan |Integer |No |65536 |The rule applies to objects larger than the specified size, in bytes.<br><br>Parent node: Filter |
|GreaterThanIncludeEqual |String |No |Enabled |Whether to enable the equal condition. It can only be set to `Enabled`or `Disabled`. If not configured, it defaults to `Disabled`. The values are explained as follows:<br><br><br>* `Enabled`: Enable equal conditions, i.e., greater than or equal to.<br><br>* `Disabled`: Not enabling the equal condition, i.e., greater than.<br><br><br>Parent node:Filter |
|ObjectSizeLessThan |Integer |No |65536 |Set rules to apply to objects smaller than the specified size, in bytes.<br><br>Parent node: Filter |
|LessThanIncludeEqual |String |No |Enabled |Whether to enable the equal condition. Can only take values `Enabled` or `Disabled`, default is `Disabled`if not configured. The values are as follows:<br><br><br>* `Enabled`: Enable equal conditions, i.e., less than or equal to.<br><br>* `Disabled`: Indicate not to enable the equal condition, i.e., less than.<br><br><br>Parent node: Filter |
|Not |Array |No |\- |Set this lifecycle rule to ignore objects with the specified prefix and tags.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">After enabling, this lifecycle rule does not support fragment cleanup.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Only one Not configuration can be added to a lifecycle rule.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The Not configuration must specify at least one prefix or tag.</div><br> |
|Prefix |String |No |prefix123 |Specify the object prefix to which Not applies instead of configuration.<br><br><br>* Only one prefix can be set at most, and its length cannot exceed 1,023.<br><br>* The prefix specified by Not must begin with the rule\-defined prefix. For example, if the rule defines the prefix as `prefix`, the Not prefix must be `prefix1`, `prefix2`, `prefix123`, etc.<br><br><br>Parent node: Not |
|Tags |Array |No |\- |Specify the object tag to which Not applies.<br><br><br>* Only one tag can be set at most, and the valid character set includes uppercase and lowercase letters, numbers, spaces, and symbols `: + - = .` `_ : /`.<br><br>* The Not specified tag key must differ from the tag key specified by the rule. For example, if the rule specifies the tag as `"key1":"value1"`, Not cannot specify the tag as `"key1":"value1"` or `"key1":"value2"`.<br><br><br>Child nodes: Key, Value |
|Key |String |No |key1 |Specify the tag key to which the Not configuration applies.<br><br>Parent node: Tags |
|Value |String |No |value1 |Specify the object tag value to which the Not configuration applies.<br><br>Parent node: Tags |


<span id="5227b475"></span>
### Elements related to lifecycle rules based on last modification time


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Expiration |Container |No | |When configuring lifecycle rules based on the last modified time, specify the expiration property to delete the latest version of the object. For buckets that have versioning enabled, the specified expiration time only applies to the current version of the object.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The expiration deletion time of the object must be greater than the time it is converted to another storage type.</div><br><br><br>Child nodes:Days, Date |
|Days |Integer |No |120 |When configuring lifecycle rules based on the last modification time, the number of days specified for expiring and deleting the latest version objects must be a positive integer.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Days and Date parameters are mutually exclusive.</div><br><br><br>Parent node:Expiration |
|Date |String |No |2024\-01\-31T00:00:00.000Z |When configuring a lifecycle rule based on the last modification time, specify a specific date on which the latest version of the object will expire and be deleted.<br><br>The date must be expressed in UTC according to the ISO 8601 standard and must be zero of UTC.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Days and Date parameters are mutually exclusive.</div><br><br><br>Parent node: Expiration |
|NoncurrentVersionExpiration |Container |No |\- |When configuring a lifecycle rule based on the last modification time, remove the expiration property of the historical version object. Effective only for buckets with version control turned on or suspended, and only for historical versions of objects.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The historical version of the object must expire longer than the conversion to another storage type.</div><br><br><br>Child nodes: NoncurrentDays, NonCurrentDate |
|NoncurrentDays |String |No |30 |When configuring a lifecycle rule based on the last modification time, specify the number of days before the historical object is deleted.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">NoncurrentDays and NonCurrentDate parameters mutual exclusion.</div><br><br><br>Parent node: NoncurrentVersionExpiration |
|NonCurrentDate |String |No |2024\-01\-31T00:00:00.000Z |When configuring a lifecycle rule based on the last modification time, specify a specific date on which the historical object will expire and be deleted.<br><br>The date must be expressed in UTC according to the ISO 8601 standard and must be zero of UTC.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">NoncurrentDays and NonCurrentDate parameters mutual exclusion.</div><br><br><br>Parent node: NoncurrentVersionExpiration |
|AbortIncompleteMultipartUpload |Container |No |\- |Specifies the expired property of incomplete multipart uploads (parts).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">AbortIncompleteMultipartUpload does not support filtering based on object tags.</div><br><br><br>Child nodes: DaysAfterInitiation |
|DaysAfterInitiation |Integer |No |30 |Specifies the lifecycle rule for incomplete multipart uploads (parts), the number of days after the multipart upload task has been initialized.<br><br>Parent node: AbortIncompleteMultipartUpload |
|Transitions |Array |No |\- |When configuring a lifecycle rule based on last modified time, the expiration property of the latest version object storage type is sunk. For Buckets with versioning enabled, the specified expiration time is only valid for the current version of the object.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If you set up auto\-transition to Infrequent Access Storage, Intelligent Tiering Storage, Flashback Archive, Archive Storage, and Delete Objects at the same time, the settlement time must meet: Infrequent Access Storage < Intelligent Tiering Storage < Flashback Archive < Archive Storage < Cold Archive Storage< Deep Cold Archive Storage < Delete Objects.</div><br><br><br>Child nodes: StorageClass, Days, Date |
|StorageClass |String |No |IA |When configuring a lifecycle rule based on last modified time, specify the storage type for the latest version of the object to settle. The values are as follows:<br><br><br>* `IA`: Infrequent Access Storage<br><br>* `INTELLIGENT_TIERING`: Intelligent Tiering Storage<br><br>* `ARCHIVE_FR`: Flashback Archive<br><br>* `ARCHIVE`: Archive Storage<br><br>* `COLD_ARCHIVE`: Cold Archive Storage<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Cold Archive Storage is supported only in China (Beijing), China (Shanghai), and China (Guangzhou).   </div><br>   <br><br>* `DEEP_COLD_ARCHIVE`: Deep Cold Archive Storage<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Deep Cold Archive Storage is only supported in China (Beijing), China (Shanghai), and China (Guangzhou), and all are in the invitation\-only testing phase. If you need to use this storage type, please contact your account manager.   </div><br>   <br><br>Parent node: Transitions |
|Days |Integer |No |120 |When configuring a lifecycle rule based on the last modification time, specify the number of days the latest version of the object has expired and settled, which must be a positive integer.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The Days and Date parameters are mutual exclusions.</div><br><br><br>Parent node: Transitions |
|Date |String |No |2024\-01\-31T00:00:00.000Z |When configuring a lifecycle rule based on the last modification time, specify a specific date when the latest version will expire and settle.<br><br>The date must be expressed in UTC according to the ISO 8601 standard and must be zero of UTC.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The Days and Date parameters are mutual exclusions.</div><br><br><br>Parent node: Transitions |
|NoncurrentVersionTransitions |Array |No |\- |Settles the expiration property of the historical version object when configuring a lifecycle rule based on the last modification time. Effective only for buckets with version control turned on or suspended, and only for historical versions of objects.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If you set up auto\-transition to Infrequent Access Storage, Intelligent Tiering Storage, Flashback Archive, Archive Storage, and Delete Objects at the same time, the settlement time must meet: Fall to Infrequent Access Storage < Intelligent Tiering Storage < Flashback Archive < Archive Storage < Cold Archive Storage< Deep Cold Archive Storage < Delete Objects.</div><br><br><br>Child nodes: StorageClass, NoncurrentDays, NonCurrentDate |
|StorageClass |String |No |IA |When configuring a lifecycle rule based on last modified time, specify the type of storage for historical object fallout. The values are as follows:<br><br><br>* `IA`: Infrequent Access Storage<br><br>* `INTELLIGENT_TIERING`: Intelligent Tiering Storage<br><br>* `ARCHIVE_FR`: Flashback Archive<br><br>* `ARCHIVE`: Archive Storage<br><br>* `COLD_ARCHIVE`: Cold Archive Storage<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Cold Archive Storage is supported only in China (Beijing), China (Shanghai), and China (Guangzhou).   </div><br>   <br><br>* `DEEP_COLD_ARCHIVE`: Deep Cold Archive Storage<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Deep Cold Archive Storage is only supported in China (Beijing), China (Shanghai), and China (Guangzhou), and all are in the invitation\-only testing phase. If you need to use this storage type, please contact your account manager.   </div><br>   <br><br>Parent node: NoncurrentVersionTransitions |
|NoncurrentDays |Integer |No |120 |When configuring a lifecycle rule based on the last modification time, specify the number of days that the historical object has expired and settled, which must be a positive integer.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">NoncurrentDays and Noncurrent Date parameters mutual exclusion.</div><br><br><br>Parent node: NoncurrentVersionTransitions |
|NoncurrentDate |String |No |2024\-01\-31T00:00:00.000Z |When configuring a lifecycle rule based on the last modification time, specify a specific date on which the historical object will expire and settle.<br><br>The date must be expressed in UTC according to the ISO 8601 standard and must be the zero of UTC.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">NoncurrentDays and Noncurrent Date parameters mutual exclusion.</div><br><br><br>Parent node: NoncurrentVersionTransitions |


<span id="5163b8cf"></span>
### Elements related to lifecycle rules based on last access time


|**Name** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|AccessTimeTransitions |Array |No |\- |When configuring lifecycle rules based on last access time, the expiration attribute of the most recent version of the object.<br><br>Child nodes: StorageClass,Days |
|StorageClass |String |No |IA |When configuring lifecycle rules based on last access time, specify the storage class for the latest version objects that have been transitioned. Possible values include:<br><br><br>* `IA`: Infrequent Access Storage<br><br>* `ARCHIVE_FR`: Flashback Archive<br><br>* `ARCHIVE`: Archive Storage<br><br>* `COLD_ARCHIVE`: Cold Archive Storage<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Cold Archive Storage is supported only in China (Beijing), China (Shanghai), and China (Guangzhou).   </div><br>   <br><br>* `DEEP_COLD_ARCHIVE`: Deep Cold Archive Storage<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Deep Cold Archive Storage is only supported in China (Beijing), China (Shanghai), and China (Guangzhou), and all are in the invitation\-only testing phase. If you need to use this storage type, please contact your account manager.   </div><br>   <br><br>Parent node: AccessTimeTransitions |
|Days |Integer |No |120 |When configuring lifecycle rules based on the last access time, specify the number of days for the latest version objects to expire and settle must be a positive integer.<br><br>Parent node: AccessTimeTransitions |
|NoncurrentVersionAccessTimeTransitions |Array |No |\- |In lifecycle rules based on last access time, the expiration attribute of historical version objects.<br><br>Child nodes: StorageClass, NoncurrentDays |
|StorageClass |String |No |IA |When configuring lifecycle rules based on last access time, specify the storage class for the sinking of historical versions objects. The possible values are as follows:<br><br><br>* `IA`: Infrequent Access Storage<br><br>* `ARCHIVE_FR`: Flashback Archive<br><br>* `ARCHIVE`: Archive Storage<br><br>* `COLD_ARCHIVE`: Cold Archive Storage<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Cold Archive Storage is supported only in China (Beijing), China (Shanghai), and China (Guangzhou).   </div><br>   <br><br>* `DEEP_COLD_ARCHIVE`: Deep Cold Archive Storage<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Deep Cold Archive Storage is only supported in China (Beijing), China (Shanghai), and China (Guangzhou), and all are in the invitation\-only testing phase. If you need to use this storage type, please contact your account manager.   </div><br>   <br><br>Parent node: NoncurrentVersionAccessTimeTransitions |
|NoncurrentDays |Integer |No |60 |When configuring lifecycle rules based on last access time, the number of days specified for the expiration and transition of historical versions objects must be a positive integer.<br><br>Parent node: NoncurrentVersionAccessTimeTransitions |


<span id="9b07f1f9"></span>
## **Response headers**

For common response headers, see [Common parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).

<span id="0190b917"></span>
## **Response body elements**

No elements are used.

<span id="cb137c43"></span>
## **Sample request 1**

Configure the expiration deletion of the latest object versions based on the last modification time.

```JSON
PUT /?lifecycle HTTP/1.1
Host: bucket-name.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
Content-Length: ContentLength
Content-MD5: MD5
{
    "Rules": [{
      "ID": "id",
      "Prefix": "prefix",
      "Status": "Enabled",
      "Expiration": { "Days": 120 }
    }]
}
```


<span id="3587a7c0"></span>
## **Sample request 2**

Configure the expiration deletion of the latest object versions in versioning\-enabled buckets based on the last modification time, including deletion of historical object versions and incomplete multipart uploads.

```JSON
PUT /?lifecycle HTTP/1.1
Host: bucket-name.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
Content-Length: ContentLength
Content-MD5: MD5
{
    "Rules": [{
      "ID": "id",
      "Prefix": "prefix",
      "Status": "Enabled",
      "Expiration": { "Days": 120 },
      "NoncurrentVersionExpiration": { "NoncurrentDays": 120 },
      "AbortIncompleteMultipartUpload": { "DaysAfterInitiation": 10 }
    }]
}
```


<span id="251d1671"></span>
## **Sample request 3**

Perform storage type transitions and expiration deletions on objects in a bucket based on their last modification time.

```JSON
PUT /?lifecycle HTTP/1.1
Host: bucket-name.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
Content-Length: ContentLength
Content-MD5: MD5
{
    "Rules": [{
      "ID": "id",
      "Prefix": "prefix",
      "Status": "Enabled",
      "Expiration": { "Days": 120 },
      "NoncurrentVersionExpiration": { "NoncurrentDays": 120 },
      "Transitions": [
        {
          "StorageClass": "IA",
          "Days": 30
        },
        {
          "StorageClass": "COLD_ARCHIVE",
          "Days": 60
        }
      ]
    }]
}
```


<span id="08ff198a"></span>
## **Sample request 4**

Perform storage type conversion and expiration deletion operations on objects with specified prefixes and tags in a bucket based on the last modification time configuration.

```JSON
PUT /?lifecycle HTTP/1.1
Host: bucket-name.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
Content-Length: ContentLength
Content-MD5: MD5
{
    "Rules": [{
      "ID": "id",
      "Prefix": "prefix",
      "Status": "Enabled",
      "Expiration": { "Days": 120 },
      "NoncurrentVersionExpiration": { "NoncurrentDays": 120 },
      "Transitions": [
        {
          "StorageClass": "IA",
          "Days": 30
        },
        {
          "StorageClass": "COLD_ARCHIVE",
          "Days": 60
        }
      ],
        "Tags": [
        {
          "Key": "aa",
          "Value": "bb"
        },
        {
          "Key": "cc",
          "Value": "dd"
        }
      ]
    }]
}
```


<span id="d9a496a3"></span>
## **Sample request 5**

Perform storage type transitions and expiration deletions on objects in a bucket based on their last access time.

```Bash
PUT /?lifecycle HTTP/1.1
Host: bucket-name.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
Content-Length: ContentLength
Content-MD5: MD5
{
    "Rules": [
        {
            "ID": "1",
            "Prefix": "aa",
            "Status": "Enabled",
            "AccessTimeTransitions": [
                {
                    "StorageClass":"IA",
                    "Days": 30
                },
                {
                    "StorageClass":"ARCHIVE_FR",
                    "Days": 60
                }
            ]
        },
        {
            "ID": "2",
            "Prefix": "vvv",
            "Status": "Enabled",
            "NoncurrentVersionAccessTimeTransitions": [
                {
                    "StorageClass":"IA",
                    "NoncurrentDays":4
                }
            ]
        }
    ]
}
```


<span id="d3553058"></span>
## **Sample request 6**

This sample request configures multiple lifecycle rules for objects with different prefixes in the bucket.

```JSON
PUT /?lifecycle HTTP/1.1
Host: bucket-name.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
Content-Length: ContentLength
Content-MD5: MD5
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


<span id="c0627708"></span>
## **Sample response**

```JSON
HTTP/1.1 200 OK
x-tos-id-2: f91b0c03a01300c1-a444cd0        
x-tos-request-id: f91b0c03a01300c1-a444cd0            
Date: Fri, 30 Jul 2021 06:45:39 GMT
server: TosServer
Content-Length: 0
```
