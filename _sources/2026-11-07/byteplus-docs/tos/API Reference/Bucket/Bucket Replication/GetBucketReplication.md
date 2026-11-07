---
title: "GetBucketReplication"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Getbucketreplication"
---

<span id="oSFm97u4"></span>
## Feature description

This interface retrieves the current data replication progress, cross\-region replication rules, or same\-region replication rules for the specified bucket (Bucket).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/docs/tos/Bucket-type">HNS buckets</a> do not support the GetBucketReplication interface.</div>


<span id=".6K-35rGC5raI5oGv5qC35byP"></span>
## Request syntax

```JSON
GET /?replication&progress&rule-id=1 HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id=".6K-35rGC5Y-C5pWw5ZKM5raI5oGv5aS0"></span>
## Request parameters and headers

This request uses public request headers. See [Public Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|---|
|replication |Query |String |Yes |\- |Represents the special identifier for the GetBucketReplication request. |
|progress |Query |String |No |progress |Indicates whether to query the bucket’s data replication progress; must be used with the `rule-id` parameter. |
|rule\-id |Query |String |No |1 |Query the rule number for copying progress. Use it with the `progress` parameter. |


<span id=".6K-35rGC5YWD57Sg"></span>
## Request body elements

No elements are used.

<span id=".5ZON5bqU5raI5oGv5aS0"></span>
## Response headers

This request returns public response headers. See [Public Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id=".5ZON5bqU5YWD57Sg"></span>
## Response body elements


|**Name** |**Type** |**Sample value** |**Note** |
|---|---|---|---|
|Role |String |ServiceRoleforReplicationAccessTOS |role name. |
|Rules |Array |\- |Copy rules. |
|ID |String |1 |The unique identifier of the rule. |
|Status |String |Enabled |Specify whether to enable this rule. The values are as follows:<br><br><br>* `Enabled`: Enable this rule.<br><br>* `Disabled`: Disable this rule. |
|PrefixSet |Array |prefix_1 |The object name prefix to which this rule applies. |
|Tags |Array |\- |TOS can copy Objects with specific tags, allowing up to 10 tags to be configured. For detailed information about tags, refer to [File Tag Management](https://docs.byteplus.com/en/docs/tos/docs-managing-file-labels). |
|Key |String |key |The key of the object tag.<br><br>Parent node: `Tags` |
|Value |String |value |The value of the object tag.<br><br>Parent node: `Tags` |
|Destination |Object |\- |save the target bucket information. |
|Bucket |String |Target Bucket Name |Name of the bucket storing copies of objects identified by the rule. |
|Location |String |cn\-beijing |the region where the target bucket is located. |
|StorageClass |String |STANDARD |Specify the storage class of the objects copied to the destination bucket. The values are as follows:<br><br><br>* `STANDARD`: Standard storage.<br><br>* `STANDARD_IA`: Infrequent Access storage.<br><br>* `GLACIER_IR`: Glacier Instant Retrieval storage.<br><br>* `INTELLIGENT_TIERING`: Intelligent Tiering storage.<br><br>* `ARCHIVE`: Archive storage.<br><br>* `COLD_ARCHIVE`: Cold Archive storage.<br><br>* `DEEP_COLD_ARCHIVE`: Deep Cold Archive storage<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If both <code>StorageClass</code> and <code>StorageClassInheritDirective</code> parameters are set, the object's storage type is assigned based on the value specified in <code>StorageClass</code>.</div><br> |
|StorageClassInheritDirective |String |DESTINATION_BUCKET |Set the storage class for objects replicated to the destination bucket. The options are as follows:<br><br><br>* `SOURCE_OBJECT`: inherit the storage class of the source bucket's object.<br><br>* `DESTINATION_BUCKET`: inherit the default storage class of the destination bucket. |
|HistoricalObjectReplication |String |Enabled |Enable or disable copying historical objects. When enabled, it copies historical objects that meet this rule. The value descriptions are as follows:<br><br><br>* `Enabled`: Enable copying historical objects.<br><br>* `Disabled`: Disable copying historical objects. |
|DeleteMarkerReplication |String |Enabled |Whether to enable synchronizing deletion markers. If enabled, deletion markers matching this rule will be synchronized. The options are as follows:<br><br><br>* `Enabled`: Enable synchronizing deletion markers.<br><br>* `Disabled`: Do not enable synchronizing deletion markers.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Synchronizing deletion markers is an invitation\-only feature. To try it, contact your account manager.</div><br> |
|DeleteObjectReplication |String |Enabled |Whether to enable synchronizing object deletion. If enabled, after deleting an object in the source bucket, the object in the target bucket will be deleted synchronously. The options are as follows:<br><br><br>* `Enabled`: Enable synchronizing object deletion.<br><br>* `Disabled`: Do not enable synchronizing object deletion.<br><br><br><div data-tips="true" data-tips-type="warning">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Synchronizing object deletion is an invitation\-only feature. To try it, contact your account manager.</div><br> |
|TransferType |String |tos_acc |Data transmission links used during data replication. The values are as follows:<br><br><br>* `internal`: The default TOS transmission link. This link is only allowed for cross\-region data replication within mainland China.<br><br>* `tos_acc`: Transmission acceleration link. This link is only allowed for cross\-region data replication between mainland China and regions outside mainland China. |
|AccessControlTranslation |Object |\- |Owner management permissions for the object.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The <code>AccessControlTranslation</code> parameter is only returned when copying objects across accounts. If a bucket uses cross\-account copying but the <code>AccessControlTranslation</code> parameter is not returned, it means the destination bucket has not been granted owner management permissions for the copied object. Specifically, the owner of the destination bucket can overwrite and delete the object but cannot read it or grant other accounts permission to read the object.</div><br> |
|Owner |String |BucketOwnerEntrusted |The destination bucket has been granted owner management permissions for replicated objects, allowing it to read objects and grant read access to other accounts. |
|Progress |Object |\- |Save the copying progress. |
|NewObject |String |2015\-09\-24T15:28:14.000Z |Show the time when data was replicated to the target bucket. |
|HistoricalObject |float64 |0.99 |Displays the percentage of copied historical data. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
GET /?replication&progress&rule-id=1 HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id=".5ZON5bqU56S65L6L"></span>
## Sample response

```JSON
HTTP/1.1 200 OK
Date: Fri, 30 Jul 2021 13:53:55 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
Content-Length: 643

{
    "Role": "ServiceRoleforReplicationAccessTOS",
    "Rules":[{
        "ID": "1",
        "Status": "Enabled",
        "PrefixSet": ["prefix_1", "prefix_2"],
        "Destination":{
            "Bucket":"Target Bucket Name",
            "Location": "Target Bucket Location",
            "StorageClass": "STANDARD"
        },
        "HistoricalObjectReplication": "Enabled",
        "DeleteMarkerReplication": "Enabled",
        "DeleteObjectReplication": "Disabled",
        "AccessControlTranslation": {
                "Owner": "BucketOwnerEntrusted"
        },
        "Progress":{
            "NewObject": "2015-09-24T15:28:14.000Z",
            "NewObject": "0.99"
        }
    }]
}
```
