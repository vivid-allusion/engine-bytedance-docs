---
title: "PutBucketReplication"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Putbucketreplication"
---

<span id=".5Yqf6IO95o-P6L-w"></span>
## Feature description

This interface sets cross\-region or same\-region replication rules for a bucket. Using the PutBucketReplication interface, you can replicate newly created and modified objects from a source bucket to a destination bucket in the same or different region.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/docs/6349/1282866">HNS buckets</a> do not support the PutBucketReplication interface.</div>


<span id="12579cb4"></span>
## Prerequisites

If you set cross\-account cross\-region or cross\-account same\-region replication rules, you must grant TOS read permission on the source bucket and write permission on the destination bucket before setting the rules. For detailed operations, see [Permission configuration for cross-account replication](https://docs.byteplus.com/en/docs/tos/Permission-configuration-for-cross-account-replication).

<span id=".6K-35rGC5raI5oGv5qC35byP"></span>
## Request syntax

```JSON
PUT /?replication HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
Content-Length: 120
Content-MD5: XrY7u+Ae7tCTyyK7j1rNww==
{
  "Role": "ServiceRoleforReplicationAccessTOS",
  "Rules": [{
      "ID": "1",
      "Status": "Enabled",
      "PrefixSet": ["prefix_1", "prefix_2"],
      "Destination": {
        "Bucket": "Target Bucket Name",
        "Location": "ap-southeast-1",
        "StorageClass": "STANDARD"
      },
      "HistoricalObjectReplication": "Enabled",
      "DeleteMarkerReplication": "Enabled",
      "DeleteObjectReplication": "Disabled",
      "AccessControlTranslation": {
        "Owner": "BucketOwnerEntrusted"
      }
   }]
}
```


<span id=".6K-35rGC5Y-C5pWw5ZKM5raI5oGv5aS0"></span>
## Request parameters and headers

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This request uses public request headers. See <a href="https://docs.byteplus.com/docs/tos/reference-common-parameters">public parameters</a>.</div>



|**Name** |**Location** |**Type** |**Required** |**Sample value** |**Note** |
|---|---|---|---|---|---|
|replication |Query |String |Yes |\- |Represents a special identifier for the PutBucketReplication request. |


<span id=".6K-35rGC5YWD57Sg"></span>
## Request body elements


|**Name** |**Type** |**Required** |**Sample value** |**Note** |
|---|---|---|---|---|
|Role |String |Yes |ServiceRoleforReplicationAccessTOS |Role name. This role must have read and write permissions and service access permissions for TOS. You can also use the default TOS role `ServiceRoleforReplicationAccessTOS`. |
|Rules |Array |Yes |\- |Copy the replication rule information. |
|ID |String |No |1 |Unique identifier of the rule, fewer than 255 characters. |
|Status |String |Yes |Enabled |Specify whether to enable this rule; the values are explained as follows:<br><br><br>* `Enabled`: enable this rule.<br><br>* `Disabled`: do not enable this rule. |
|PrefixSet |Array |No |prefix_1 |Object name prefix applicable to this rule. |
|Tags |Array |No |\- |TOS can replicate objects with specific tags, supporting up to 10 tags. For more details on tags, see [Managing object tags](https://docs.byteplus.com/en/docs/tos/docs-managing-file-labels). |
|Key |String |No |key |The key of the object tag.<br><br>Parent node: Tags |
|Value |String |No |value |The value of the object tag.<br><br>Parent node: Tags |
|Destination |Object |Yes |\- |Target bucket information. |
|Bucket |String |Yes |Target Bucket Name |Target bucket name. |
|Location |String |Yes |cn\-beijing |Region of the target bucket. |
|StorageClass |String |No |STANDARD |Specify the storage class of the object copied to the destination bucket. The values are described as follows:<br><br><br>* `STANDARD`: Standard Storage.<br><br>* `STANDARD_IA`: Infrequent Access Storage.<br><br>* `INTELLIGENT_TIERING`: Intelligent Tiering Storage.<br><br>* `GLACIER_IR`: archive instant retrieval storage.<br><br>* `ARCHIVE`: archive storage.<br><br>* `COLD_ARCHIVE`: cold archive storage.<br><br>* `DEEP_COLD_ARCHIVE`: deep cold archive storage.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Cold Archive is only supported in China (Beijing), China (Shanghai), and China (Guangzhou).   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Deep Cold Archive is only supported in China (Beijing), China (Shanghai), and China (Guangzhou). Deep Cold Archive is currently in closed beta. Please contact your account manager for access.   </div><br>   <br><br><br>If both `StorageClass` and `StorageClassInheritDirective` parameters are set, the storage type is determined by the value specified in `StorageClass`. |
|StorageClassInheritDirective |String |No |DESTINATION_BUCKET |Set the storage class for objects copied to the destination bucket. The values are described as follows:<br><br><br>* `SOURCE_OBJECT`: inherit the storage class of the source bucket object.<br><br>* `DESTINATION_BUCKET`: inherit the default storage class of the destination bucket. |
|HistoricalObjectReplication |String |Yes |Enabled |Whether to enable replication of historical objects. If enabled, historical objects matching this rule will be replicated. The options are as follows:<br><br><br>* `Enabled`: Enable replication of historical objects.<br><br>* `Disabled`: Do not enable replication of historical objects. |
|DeleteMarkerReplication |String |No |Enabled |Whether to enable synchronizing deletion markers. If enabled, deletion markers matching this rule will be synchronized. The options are as follows:<br><br><br>* `Enabled`：Enable synchronizing deletion markers.<br><br>* `Disabled`：Do not enable synchronizing deletion markers.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Synchronizing deletion markers is only supported for buckets with version control enabled.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Synchronizing deletion markers is an invitation\-only feature. To try it, contact your account manager.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The tagging and synchronizing deletion markers functions can only be selected one at a time; simultaneous use of both functions is not supported.</div><br> |
|DeleteObjectReplication |String |No |Enabled |Whether to enable synchronizing object deletion. If enabled, after deleting an object in the source bucket, the object in the target bucket will be deleted synchronously. The options are as follows:<br><br><br>* `Enabled`：Enable synchronizing object deletion.<br><br>* `Disabled`：Do not enable synchronizing object deletion.<br><br><br><div data-tips="true" data-tips-type="warning">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Synchronizing object deletion will synchronize deletion operations from the source bucket to the target bucket. For example, when you delete a file on the source bucket or when an expired file deletion rule takes effect in its lifecycle, the target bucket will also synchronously delete the file. Please choose this option carefully.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Synchronizing object deletion is an invitation\-only feature. To try it, contact your account manager.</div><br> |
|TransferType |String |No<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is required for cross\-region replication scenarios between mainland China and regions outside mainland China.</div><br> |tos_acc |Specify the data transfer link used for cross\-region replication; the values are explained as follows:<br><br><br>* `internal`: TOS default transfer link. This link is only allowed for cross\-region replication data transfers within mainland China.<br><br>* `tos_acc`: transfer acceleration link. This link is only allowed for cross\-region replication data transfers between mainland China and regions outside mainland China.<br><br><br>The default value is `internal`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Before using the transfer acceleration link to transfer data, you must enable the transfer acceleration feature, which cannot be disabled once enabled. For details, see <a href="https://docs.byteplus.com/docs/6349/1262407#e67c338c">enable transfer acceleration</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Transfer acceleration is an invitation\-only feature. To try it, contact your account manager.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Transfer acceleration is billed separately. When using transfer acceleration, TOS charges both the cross\-region replication traffic fee for the source bucket and the transfer acceleration outbound traffic fee. For detailed information, see <a href="https://docs.byteplus.com/docs/6349/1262779">Transfer acceleration fees</a>.</div><br> |
|AccessControlTranslation |Object |No |\- |Object owner manages permissions.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When replicating objects across accounts only, set the <code>AccessControlTranslation</code> parameter.</div><br> |
|Owner |String |No |BucketOwnerEntrusted |Only supports setting to `BucketOwnerEntrusted`, which grants the destination bucket owner management permissions for the copied objects. This means the destination bucket owner can read the objects and grant other accounts permission to read the objects. By default, the destination bucket owner can overwrite and delete objects but cannot read the objects or grant other accounts permission to read the objects.<br><br>Parent node: AccessControlTranslation<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The <code>Owner</code> parameter must be set only when copying objects across accounts.</div><br> |


<span id=".5ZON5bqU5raI5oGv5aS0"></span>
## Response headers

This request returns public response headers. See [public parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id=".5ZON5bqU5YWD57Sg"></span>
## Response body elements

No elements are used.

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
PUT /?replication HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
Content-Length: 120
Content-MD5: XrY7u+Ae7tCTyyK7j1rNww==
{
  "Role": "ServiceRoleforReplicationAccessTOS",
  "Rules": [{
      "ID": "1",
      "Status": "Enabled",
      "PrefixSet": ["prefix_1", "prefix_2"],
      "Destination": {
        "Bucket": "Target Bucket Name",
        "Location": "ap-southeast-1",
        "StorageClass": "STANDARD"
      },
      "HistoricalObjectReplication": "Enabled",
      "DeleteMarkerReplication": "Enabled",
      "DeleteObjectReplication": "Disabled",
      "AccessControlTranslation": {
        "Owner": "BucketOwnerEntrusted"
      }
   }]
}
```


<span id=".5ZON5bqU56S65L6L"></span>
## Sample response

```JSON
HTTP/1.1 200 OK
x-tos-id-2: f91b0c03a01300c1-a444ed0        
x-tos-request-id: f91b0c03a01300c1-a444ed0            
Date: Fri, 30 Jul 2021 06:45:39 GMT
server: TosServer
```
