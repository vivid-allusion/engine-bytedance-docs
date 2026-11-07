---
title: "Bucket policy templates and parameters"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-templates-and-parameters"
---

This topic describes authorized operations, authorization templates, and authorization parameters supported by bucket policies.

<span id="WhABJky8"></span>
## Supported actions

<span id="bpY36gpC"></span>
### General actions


|**Action** |**Description** |
|---|---|
|\* |The wildcard, which indicates all operations that can be performed on the resource. |
|Get\* |Indicates all GET operations that can be performed on the resource. |
|Put\* |Indicates all PUT operations that can be performed on the resource.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This operation is risky. Proceed with caution.</div><br> |
|List\* |Indicates all LIST operations that can be performed on the resource. |


<span id="DrUYnkFa"></span>
### Bucket actions


|**Category** |**Action** |**Description** |
|---|---|---|
|Bucket operation |ListBucket |Lists objects in a bucket. |
||HeadBucket |Checks whether a bucket exists and obtains its metadata. |
||DeleteBucket |Deletes the bucket.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This operation is risky. Proceed with caution.</div><br> |
|Bucket ACL |GetBucketACL |Obtains bucket ACL information. |
||PutBucketACL |Sets the bucket ACL.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This operation is risky. Proceed with caution.</div><br> |
|Bucket policy |GetBucketPolicy |Gets the bucket policy. |
||PutBucketPolicy |Sets the bucket policy. This permission allows users to change the bucket policy and obtain other permissions.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This action is risky. Proceed with caution.</div><br> |
||DeleteBucketPolicy |Deletes the bucket policy.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This operation is risky. Proceed with caution.</div><br> |
|Bucket tags |GetBucketTagging |Retrieve bucket tags. |
||PutBucketTagging |Set bucket tags. |
|Lifecycle rules |GetLifecycleConfiguration |Obtains the bucket lifecycle rule. |
||PutLifecycleConfiguration |Sets the bucket lifecycle rule. |
|Object locking |PutBucketObjectLockConfiguration |Set object lock feature. |
||GetBucketObjectLockConfiguration |Gets the object lock configuration. |
|RenameObject |PutBucketRename |Sets the bucket's RenameObject feature. |
||GetBucketRename |Obtains the bucket's RenameObject feature information. |
|Access monitor |PutBucketAccessMonitor |Enable or disable access tracking. |
||GetBucketAccessMonitor |Retrieve access tracking information. |
|Bucket inventory |PutBucketInventory |Create Bucket inventory. |
||GetBucketInventory |Obtain information about the specified bucket inventory rule. |
||ListBucketInventory |Get bucket inventory rule list. |
||DeleteBucketInventory |Delete bucket inventory.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This operation is risky; please configure with caution.</div><br> |


<span id="F0AF7OcM"></span>
### Object actions


|**Category** |**Action** |**Description** |
|---|---|---|
|Object operation |GetObject |Obtains the content and metadata of an object. |
||PutObject |Performs PUT upload, part upload, part upload initialization, or part merging. |
||DeleteObject |Deletes an object.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This operation is risky. Proceed with caution.</div><br> |
||SetObjectExpires |Set object expiration time.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This action is a risky operation; please configure with caution.</div><br> |
|Object ACL |GetObjectAcl |Obtains the object ACL information. |
||PutObjectAcl |Sets the object ACL.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This operation is risky. Proceed with caution.</div><br> |
|Object tag |GetObjectTagging |Obtains an object tag. |
||PutObjectTagging |Sets object tags. |
||DeleteObjectTagging |Deletes object tags.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This operation is risky. Proceed with caution.</div><br> |
|Object retention period |PutObjectRetention |Set object retention policy. |
||GetObjectRetention |Get object retention policy. |
|RenameObject |RenameObject |Rename object.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">For flat namespaces (FNS), enable the RenameObject feature before using RenameObject. For details, see <a href="https://docs.byteplus.com/docs/tos/Use-renameobject">Using RenameObject</a> or <a href="https://docs.byteplus.com/docs/tos/Putbucketrename">PutBucketRename</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For hierarchical namespaces (HNS), the RenameObject feature is supported by default and does not require additional activation.</div><br> |
|Others |AbortMultipartUpload |Cancels a multi\-part upload task. |
||ListMultipartUploadParts |Lists uploaded parts. |


<span id="q6Rw9Wjw"></span>
## Bucket policy templates

The TOS console provides seven preset bucket policy templates to cater to common scenarios. You can use one of them to quickly configure a policy.

In some templates, you need to specify the authorized user or resource; in other templates, you can change the authorized user, resource, action, and condition.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Buckets set with public\-read\-only or public\-read\-write permission are exposed over the public network. Files in these buckets can be read and written by anyone, which incurs traffic fees and may cause property loss and data leakage.</div>



|**Template** |**Authorized User** |**Resource Scope** |**Operation** |
|---|---|---|---|
|Bucket Read\-Only |To be specified: you need to specify the authorized user |The current bucket and all its objects |Allows the specified user to perform the following operations on the current bucket and all its objects:<br><br><br>* Get\*: all GET operations.<br><br>* List\*: all LIST operations.<br><br>* HeadBucket: Checks whether the bucket exists and obtains its metadata. |
|Bucket Read and Write |To be specified: you need to specify the authorized user. |The current bucket and all its objects |Allows the specified user to perform the following operations on the current bucket and all its objects:<br><br><br>* Get\*: all GET operations.<br><br>* List\*: all LIST operations.<br><br>* HeadBucket: Checks whether the bucket exists and obtains its metadata.<br><br>* PutLifecycleConfiguration: Sets the bucket lifecycle rule.<br><br>* PutBucketVersioning: Sets the multiversion status.<br><br>* PutBucketCORS: Sets the bucket CORS.<br><br>* PutObject: Performs PUT upload, POST upload, part upload, initializes part upload tasks, or merges parts.<br><br>* DeleteObject: Deletes an object.<br><br>* PutObjectAcl: Sets the object ACL.<br><br>* DeleteObjectVersion: Deletes an object of a specified version.<br><br>* AbortMultipartUpload: Cancels a multi\-part upload task. |
|Folder Read\-Only |To be specified: you need to specify the authorized user. |To be specified: you need to specify the object prefix |Allows the specified user to perform the following operations on the current bucket and specified objects in it:<br><br><br>* ListBucket: Lists objects in the bucket.<br><br>* HeadBucket: Determines whether the bucket exists and gets its metadata.<br><br>* ListBucketVersions: Lists multiversion objects in the bucket.<br><br>* GetObject: Obtains the content and metadata of an object.<br><br>* GetObjectAcl: Obtains the object ACL.<br><br>* GetObjectVersion: Obtains the content and metadata of an object of a specified version. |
|Folder Read and Write |To be specified: you need to specify the authorized user. |To be specified: you need to specify the object prefix. |Allows the specified user to perform the following operations on the current bucket and specified objects in it:<br><br><br>* ListBucket: Lists objects in the bucket.<br><br>* HeadBucket: Checks whether the bucket exists and obtains its metadata.<br><br>* ListBucketVersions: Lists multiversion objects in a bucket.<br><br>* ListBucketMultipartUploads: Lists multi\-part upload tasks.<br><br>* GetObject: Obtains the content and metadata of an object.<br><br>* PutObject: Performs PUT upload, POST upload, part upload, part upload initialization, or part merging.<br><br>* GetObjectAcl: Obtains the object ACL.<br><br>* PutObjectAcl: Sets the object ACL.<br><br>* GetObjectVersion: Obtains the content and metadata of an object of a specified version.<br><br>* AbortMultipartUpload: Cancels a multi\-part upload task.<br><br>* ListMultipartUploadParts: Lists uploaded parts. |
|Public Read\-Only (including ListBucket operations) |All users: all internet users |The current bucket and all its objects |Allows all users to perform the following operations on the current bucket and all its objects:<br><br><br>* ListBucket: Lists objects in the bucket.<br><br>* HeadBucket: Determines whether the bucket exists and gets its metadata.<br><br>* ListBucketVersions: Lists multiversion objects in a bucket.<br><br>* GetObject: Obtains the content and metadata of an object.<br><br>* GetObjectVersion: Obtains the content and metadata of an object of a specified version. |
|Public Read\-Only (excluding ListBucket operations) |All users: all internet users. |The current bucket and all its objects |Allows all users to perform the following operations on the current bucket and all its objects:<br><br><br>* HeadBucket: Determines whether the bucket exists and gets its metadata.<br><br>* GetObject: Obtains the content and metadata of an object.<br><br>* GetObjectVersion: Obtains the content and metadata of an object of a specified version. |
|Public\-read\-write |All users: all internet users. |The current bucket and all its objects |Allows all users to perform the following operations on the current bucket and all its objects:<br><br><br>* ListBucket: Lists objects in the bucket.<br><br>* HeadBucket: Determines whether the bucket exists and gets its metadata.<br><br>* ListBucketVersions: Lists multiversion objects in the bucket.<br><br>* GetObject: Obtains the content and metadata of an object.<br><br>* PutObject: Performs PUT upload, POST upload, part upload, part upload initialization, or part merging.<br><br>* GetObjectAcl: Obtains the object ACL.<br><br>* PutObjectAcl: Sets the object ACL.<br><br>* GetObjectVersion: Obtains the content and metadata of an object of a specified version.<br><br>* AbortMultipartUpload: Cancels a multi\-part upload task.<br><br>* ListMultipartUploadParts: Lists uploaded parts. |


<span id="4eZxSoDw"></span>
## Bucket policy parameters

A statement contains main policy parameters. A policy can contain multiple statements, and each statement can contain the following parameters.


|Parameter |Required |Description |Example |
|---|---|---|---|
|**Sid** |Optional |Specifies the policy name for differentiation.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The policy name must be unique in a bucket.</div><br> |```json```<br>```"Sid": "test"```<br> |
|**Effect** |Yes |Specifies whether to allow or deny access. Valid values:<br><br><br>* **Allow**: allow<br><br>* **Deny**: deny |```json```<br>```"Effect": "Allow"```<br> |
|**Principal** |No<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When <code>Effect</code> is <code>Allow</code>, the <code>Principal</code> parameter is required.</div><br> |Specifies the authorized user.<br><br><br>* Specified user: Set the account ID to be authorized. Use / to authorize IAM users under this account.`/`.<br><br>* All users: Use wildcard \*`*`. |* Specified User<br><br><br>```json```<br>```"Principal":["200000****/IAMUserName"]```<br><br><br><br>* All users<br><br><br>```json```<br>```"Principal":["*"]```<br> |
|**NotPrincipal** |No |This parameter must be used together with `"Effect":"Deny"`. When used with `"Effect":"Deny"`, access is denied to all users except those specified by `NotPrincipal`. For typical authorization scenarios of `NotPrincipal`, please see [Using NotPrincipal, NotResource, and NotAction](https://docs.byteplus.com/docs/tos/Typical-authorization-scenarios-for-notprincipal-notresource-and-notaction).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Wildcard cannot be used alone<code>*</code>Denies all users; using <code>"NotPrincipal":["*"]</code> is not supported.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you need to authorize IAM users under this account, you can use<code>/</code>.</div><br> |```json```<br>```"NotPrincipal":["200000****/IAMUserName"]```<br> |
|**Action** |No<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The <code>Action</code> parameter is required when <code>Effect</code> is set to <code>Allow</code>.</div><br> |The list of operations allowed or denied by the specified policy. For supported operations in TOS, see [Action Description](https://docs.byteplus.com/docs/tos/docs-templates-and-parameters#WhABJky8).<br><br><br>* Represented as a string, the action format is `tos:ActionName`, case insensitive.<br><br>* Supports wildcards`*`, indicating all operations allowed on this resource. For example: `"Action":["tos:List*"]`. |```json```<br>```"Action": [```<br>```        "tos:Get*",```<br>```        "tos:List*",```<br>```        "tos:HeadBucket"```<br>```      ]```<br> |
|**NotAction** |No |This parameter can be used with `"Effect":"Deny"` and `"Effect":"Allow"`, explained as follows:<br><br><br>* Used with `"Effect":"Deny"`, it indicates that all actions except those specified by `NotAction` will be denied.<br><br>* Used with `"Effect":"Allow"`, it means all actions except those specified by `NotAction` are allowed.<br><br><br>This parameter value is expressed as a string, with action format `tos:ActionName`, case\-insensitive. For typical authorization scenarios involving `NotAction`, refer to  [Using NotPrincipal, NotResource, and NotAction](https://docs.byteplus.com/docs/tos/Typical-authorization-scenarios-for-notprincipal-notresource-and-notaction).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Using wildcards alone is not supported.<code>*</code>Denying all actions is not supported, meaning <code>"NotAction":["*"]</code> cannot be used.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For the list of operations supported by TOS, see <a href="https://docs.byteplus.com/docs/tos/docs-templates-and-parameters#WhABJky8">Action Description</a>.</div><br> |```json```<br>```"NotAction": [```<br>```        "tos:Get*",```<br>```        "tos:List*",```<br>```        "tos:HeadBucket"```<br>```      ]```<br> |
|**Resource** |No<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When <code>Effect</code> is <code>Allow</code>, the <code>Resource</code> parameter is required.</div><br> |specifies the resource scope of the policy based on the following rules:<br><br><br>* if you only need to perform operations on the bucket, set the resource as the bucket name, for example `trn:tos:::bucketname`.<br><br>* if you only need to perform operations on objects within the bucket, set the resource as the object inside the bucket, for example `trn:tos:::bucketname/objectname`. |```json```<br>``` "Resource": [```<br>```        "trn:tos:::bucketname",```<br>```        "trn:tos:::bucketname/*"```<br>```      ]```<br> |
|**NotResource** |No |This parameter must be used together with `"Effect":"Deny"`. When used with `"Effect":"Deny"`, access to all resources except those specified by `NotResource` will be denied. The rule settings are as follows:<br><br><br>* If you only need to perform operations on the bucket, set the resource as the bucket name only, for example, `trn:tos:::bucketname`.<br><br>* If you only need to perform operations on objects within the bucket, set the resource within the bucket, such as `trn:tos:::bucketname/objectname`. Objects within the bucket support wildcards`*`, representing all resources within the bucket.<br><br>   For an introduction to typical authorization scenarios for `NotResource`, see  [Using NotPrincipal, NotResource, and NotAction](https://docs.byteplus.com/docs/tos/Typical-authorization-scenarios-for-notprincipal-notresource-and-notaction).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Using wildcards alone is not supported<code>*</code>Reject all resources, which does not support using <code>"NotResource":["*"]</code>.</div><br> |```json```<br>```"NotResource": "trn:tos:::bucketname/*"```<br> |
|**Condition** |No |Specifies the authorization condition. For detailed information about conditions, see [Condition Details](https://docs.byteplus.com/docs/tos/docs-templates-and-parameters#nk9G2rUC). |```json```<br>```"Condition": {```<br>```        "IpAddress": {```<br>```                "SourceIp": [```<br>```                        "192.168.0.1",```<br>```                        "192.168.0.3"```<br>```                ]```<br>```        }```<br>```}```<br> |


<span id="hoPGzraU"></span>
### Example

```json
{
  "Statement": [
    {
      "Sid": "IPtest",
      "Effect": "Allow",
      "Principal":["*"],
      "Action": [
        "tos:Get*",
        "tos:List*",
        "tos:HeadBucket"
      ],
      "Resource":[
        "trn:tos:::bucketname",
        "trn:tos:::bucketname/*"
      ],
      "Condition": {
         "IpAddress": {
           "SourceIp": [ 
            "192.168.0.1",
            "192.168.0.3"
          ]
        }
      } 
    } 
  ]
}
```


<span id="nk9G2rUC"></span>
## Conditions

<span id="QvBSD9c9"></span>
### Supported conditions

Conditions determine when the bucket policy applies; the bucket policy only takes effect if the request information meets the conditions. Conditions consist of a key, a condition operator, and a value. There are interdependencies between condition operators, keys, and supported actions.


|**Key** |**Type** |**General** |**Key Description** |**Value description** |
|---|---|---|---|---|
|prefix |String |No |When listing objects, use to specify a prefix; only the following actions support this setting:<br><br><br>* List\*<br><br>* ListBucket<br><br>* ListBucketVersions |Enter specific prefixes and wildcards (\*).<br><br>For example, if the condition is set to `prefix not equal to dr1/`, then when the account granted bucket policy lists objects, the `prefix` parameter in the Query must be set to values other than `dr1/`, or the bucket policy will not take effect. |
|delimiter |String |No |When listing objects, the character for grouping Object names is only supported by the following actions:<br><br><br>* List\*<br><br>* ListBucket<br><br>* ListBucketVersions |Enter common delimiters.<br><br>For example, if the condition is set as `delimiter equals /`, the account granted the bucket policy must set the `delimiter` parameter in the Query when listing objects;`/`otherwise, the bucket policy will not take effect. |
|max\-keys |String |No |When listing objects, returns the maximum number of objects. Only the following operations support this setting:<br><br><br>* List\*<br><br>* ListBucket<br><br>* ListBucketVersions |Enter a number within the range [1\-1000].<br><br>For example, if the condition is set to `max-keys equals 10`, the account granted the bucket policy must set the `max-keys` parameter to `10` in the Query when listing objects; otherwise, the bucket policy will not take effect. |
|x\-tos\-acl |String |No |When uploading an object or setting an ACL, it declares the object's ACL in the header field. Only the following operations support this setting:<br><br><br>* Put\*<br><br>* PutBucketAcl<br><br>* PutObject<br><br>* PutObjectAcl |Enter a valid ACL with a range of values:<br><br><br>* private<br><br>* public\-read<br><br>* public\-read\-write<br><br>* bucket\-owner\-read<br><br>* bucket\-owner\-full\-control<br><br>* authenticated\-read<br><br>* bucket\-owner\-entrusted<br><br><br>For example, if the condition is set to `x-tos-acl equals public-read`, the account granted the bucket policy must set the `x-tos-acl` parameter to `public-read` in the header when uploading objects or setting ACL; otherwise, the bucket policy will not take effect. |
|x\-tos\-copy\-source |String |No |When copying objects, these specify the source bucket and object names; setting them is only supported for the following actions:<br><br><br>* Put\*<br><br>* PutObject |Enter the valid source object's path.<br><br>For example, if the condition is set to `x-tos-copy-source equals /bucket/object`, then when the account granted by the bucket policy calls the CopyObject API, it must set the `x-tos-copy-source` parameter in the Header to `/bucket/object`, otherwise the bucket policy will not take effect. |
|x\-tos\-metadata\-directive |String |No |Specify whether to copy metadata from the source object or replace metadata with the one provided in the request; only the following operations support this setting:<br><br><br>* Put\*<br><br>* PutObject |Enter the metadata copy policy with values `COPY` or `REPLACE` as described below:<br><br><br>* COPY: Copy metadata from the source object.<br><br>* REPLACE: Replace the object's metadata with the metadata provided in the request.<br><br><br>For example, if the condition is set to `x-tos-metadata-directive equals COPY`, then when the account granted by the bucket policy calls the CopyObject interface, it must set the `x-tos-metadata-directive` parameter to `COPY` in the header; otherwise, the bucket policy will not take effect. |
|CurrentTime |Date |Yes |The server receives the request time in UTC, formatted as ISO 8601, with the basic format yyyy\-MM\-ddTHH:mmZ (UTC time). |Enter the date in ISO 8601 format.<br><br>For example, set the condition to `CurrentTime greater than 2023-10-13T15:00:00Z`. When the account granted the bucket policy performs the corresponding action, the request time must be later than 2023\-10\-13T15:00:00Z; otherwise, the bucket policy will not take effect. |
|EpochTime |Numeric |Yes |Seconds elapsed since January 1, 1970 (UTC/GMT midnight), excluding leap seconds. |Enter the number of seconds.<br><br>For example, if the condition is set to `EpochTime greater than 1697187692`, the request time must be greater than 1697187692 when the account granted the bucket policy performs the corresponding action; otherwise, the bucket policy will not take effect. |
|SecureTransport |Boolean |Yes |Whether the request uses SSL encryption. |Enter `true` or `false`. The values are described as follows:<br><br><br>* true: yes.<br><br>* false: no.<br><br><br>For example, if you set the condition to `SecureTransport bool true`, requests must use SSL encryption when the account granted the bucket policy performs the corresponding action; otherwise, the bucket policy will not take effect. |
|SourceIp |String |Yes |Source IP of the request. |Enter an IP address or IP range. For multiple IPs, separate them with commas.<br><br>For example, if the condition is set to `SourceIp equals 192.168.0.1`, then when an account granted the bucket policy executes the corresponding action, the source IP of the request must be 192.168.0.1; otherwise, the bucket policy will not take effect. |
|UserAgent |String |Yes |the user agent of the request. |Enter Agent details and wildcards (\*).<br><br>For example, if the condition is set as `UserAgent equals tos go sdk v2.6.0`, the account granted the bucket policy must use the client agent tos go sdk v2.6.0 in the request when performing the corresponding action; otherwise, the bucket policy will not take effect. |
|Referer |String |Yes |The request URL. |Enter URL.<br><br>For example, if the condition is set as `Referer equals http://console.volcengine.com`, when the account granted the bucket policy performs the corresponding action, the request header must be `http://console.volcengine.com`; otherwise, the bucket policy will not take effect. |
|rolename |String |Yes |role name, used to specify other cloud services or internal requests within TOS. |Enter the role name.<br><br>For example, set the condition to `rolename equals ServiceRoleforReplicationAccessTOS`. When accessing TOS, the role name must be ServiceRoleforReplicationAccessTOS; otherwise, the bucket policy will not take effect. |
|NetPlane |String |Yes |Network plane of request origin. |Only supports configuring `public`, indicating the request originates from the public network.<br><br>For example, if you set the condition to `NetPlane equals public`, the request source must be public network when the account granted the bucket policy performs the corresponding action; otherwise, the bucket policy will not take effect. |
|volc:ViaConsole |String |Yes |Is the request from the console |Enter `true` or `false`. The values mean the following:<br><br><br>* true: log in to the console to access.<br><br>* false: programmatically request API access.<br><br><br>For example, if the condition is set to `volc:ViaConsole equals true`, the account granted the bucket policy must access TOS through the console; otherwise, the bucket policy will not take effect. |
|volc:ResourceTag/$ |String |Yes |The tag value of the tag key `tag_key` in the requested bucket's tags. |Enter the storage bucket's tag value.<br><br>If you set the condition as `volc:ResourceTag/project equals short video business`, the account granted in the bucket policy can only access buckets with the tag key `project` and tag value `short video business`. |
|volc:RequestTag/$ |String |No |The tag value of the tag key `tag_key` passed in the request. |Input the tag value transmitted in the request.<br><br>For example, if the condition is set as `volc:RequestTag/project equals short video business`, the account granted the bucket policy must carry the tag key project with the value short video business when performing the corresponding action; otherwise, the bucket policy will not take effect. |
|volc:RequestTagKeys |String |No |Request all forwarded tag keys. |Enter the tag key to pass in the request.<br><br>For example, if the condition is set as `volc:RequestTagKeys equals short video business`, the account granted the bucket policy must include the tag key "short video business" in the request when performing the corresponding action; otherwise, the bucket policy will not take effect. |
|volc:SourceIp |String |Yes |Source IP initiating the request. |Enter an IP address or range. Separate multiple IPs with commas.<br><br>For example, if the condition is set to `volc:SourceIp equals 192.168.0.1`, the source IP of the request from the account granted the bucket policy must be 192.168.0.1 when performing the corresponding action; otherwise, the bucket policy will not take effect. |
|volc:UserName |String |Yes |The name of the requested IAM user. |Enter the IAM user name.<br><br>For example, if the condition is set as `volc:UserName equals sso-`, the IAM user name prefix must be sso\- when accessing TOS; otherwise, the bucket policy will not take effect. |
|volc:RequestedRegion |String |Yes |Requested Region. |Enter the specific Region.<br><br>For example, if the condition is set to `volc:RequestedRegion equals cn-beijing`, access to TOS is restricted to the North China 2 (Beijing) bucket; otherwise, the bucket policy does not take effect. |
|volc:CurrentTime |String |Yes |The server receives the request time in UTC, formatted as ISO 8601, with the basic format yyyy\-MM\-ddTHH:mmZ (UTC time). |Enter the date in ISO 8601 format.<br><br>For example, if the condition is set to `volc:CurrentTime greater than 2023-10-13T15:00:00Z`, when an account granted the bucket policy performs the corresponding action, the request time must be later than 2023\-10\-13T15:00:00Z; otherwise, the bucket policy will not take effect. |
|volc:PrincipalTrn |String |Yes |TRN of the request identity. |Enter TRN, as explained below:<br><br><br>* User identity access (including user SSO): trn:iam::${AccountId}:user/$<br><br>* Temporary credential access after role assumption (including role SSO): trn:iam::${AccountId}:role/$<br><br>* Root user access (must be the root account/root user; sub\-users or roles within the root account are not included): trn:iam::${AccountId}:root<br><br><br>For example, to set the following condition, the access identity must be<br><br>`trn:iam::2100*****4:user/tos_user`<br><br>when accessing TOS; otherwise, the bucket policy will not take effect.<br><br>```Python```<br>```"Condition":{```<br>```    "StringEquals":{```<br>```            "volc:PrincipalTrn":"trn:iam::2100*****4:user/tos_user"```<br>```    }```<br>``` }```<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Using the <code>volc:PrincipalTrn</code> condition is supported only when creating bucket policies in JSON view.</div><br> |


<span id="jucDSGPx"></span>
### Operator explanation

In an authorization policy, conditions and operators are matched as follows.


|**Condition** |**Operators** |
|---|---|
|* prefix<br><br>* delimiter<br><br>* x\-tos\-acl<br><br>* x\-tos\-copy\-source<br><br>* x\-tos\-metadata\-directive<br><br>* UserAgent<br><br>* Referer<br><br>* rolename<br><br>* volc:ResourceTag/$<br><br>* volc:RequestTag/$<br><br>* volc:RequestTagKeys<br><br>* volc:UserName<br><br>* volc:RequestedRegion |* **Equals**: exactly matches the set condition value.<br><br>* **Not equals**: does not match the set condition value.<br><br>* **Equals (case\-insensitive)** : matches the set condition value exactly, ignoring case.<br><br>* **Not equals (case\-insensitive)** : does not match the set condition value exactly, ignoring case.<br><br>* **Like**: supports wildcard (\*) regular matching; for example, `like abc*` matches all characters starting with `abc`, case\-sensitive.<br><br>* **Not Like**: supports wildcard (\*) regular matching; for example, `Not like abc*` matches all characters except those starting with `abc`, case\-sensitive. |
|* max\-keys<br><br>* CurrentTime<br><br>* EpochTime<br><br>* volc:CurrentTime |* **equals**: equals the set condition value.<br><br>* **not equals**: does not equal the set condition value.<br><br>* **less than**: less than the set condition value.<br><br>* **less than or equal**: less than or equal to the set condition value.<br><br>* **Greater than**: greater than the set condition value.<br><br>* **Greater than or equal to**: greater than or equal to the set condition value. |
|* SourceIp<br><br>* NetPlane<br><br>* volc:SourceIp |* **equals**: specified IP or IP range.<br><br>* **not equals**: all IPs except the specified IP or IP range. |
|* SecureTransport<br><br>* volc:ViaConsole |Boolean value with only two options: `true` and `false`. |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">After you configure prefix, delimiter, or max\-keys, you need to carry the corresponding key\-value pair when performing List operations. Otherwise, the bucket policy will not take effect.</div>


* <div data-tips="true" data-tips-type="warning">Separate multiple values with commas (,).</div>


* <div data-tips="true" data-tips-type="warning">If your value contains commas (,), you can use<code>/</code>escape characters.</div>
