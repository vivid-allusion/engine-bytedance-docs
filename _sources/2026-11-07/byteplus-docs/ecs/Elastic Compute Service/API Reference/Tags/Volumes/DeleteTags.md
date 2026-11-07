---
title: "DeleteTags"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DeleteTags-02"
---

Call DeleteTags to delete user tags from one or more resources.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You are allowed to call this API action to delete up to 20 tags at a time.</div>


* <div data-tips="true" data-tips-type="tip">Deleting a tag repeatedly will overwrite the existing result and update the tag value.</div>



<span id="request-parameters"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Action |String |Yes |DeleteTags |The action that you want to perform. Value: DeleteTags. |
|ResourceType |String |Yes |volume |The resource type. Valid values:<br><br><br>* volume |
|ResourceIds.N |String |Yes |ResourceIds.1=vol\-76pwr6rilv8lzwxv\*\*\*\*&ResourceIds.2=vol\-76pwr6rilv8lzwxv\*\*\*\* |The resource ID.<br><br><br>* Parameter \- N specifies the serial number of the resource. Valid values: 1–50.<br><br>* Separate resources with ampersands ( & ). |
|TagKeys.N |String |Yes |TagKeys.1=k1 |The tag key of the user tag you want to delete from the resource.<br><br><br>* Parameter \- N specifies the serial number of the tag key. Valid values: 1–20.<br><br>* Separate tag keys with ampersands ( & ).<br><br><br>Name the tag key as follows:<br><br><br>* Do not start with `volc:` or `sys:` in any uppercase or lowercase form.`volc:` or `sys:` is the start of the system reserved tag keys that cannot be created.<br><br>* The value can contain only letters, digits, spaces, and the following special characters: _ . : / = + \- @<br><br>* The value can be 1 to 128 characters in length. |


<span id="response-parameters"></span>
## Response parameters

null

<span id="sample-request"></span>
## Sample request

```Plain Text
GET /?Action=DeleteTags&Version=2020-04-01&ResourceType=volume&ResourceIds.1=vol-76pwr6rilv8lzwxv*****&ResourceIds.2=vol-76pwr6rilv8lzwxv****&TagKeys.1=tag HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
ServiceName: storage_ebs
```


<span id="sample-response"></span>
## Sample response

```Plain Text
{
    "ResponseMetadata": {
        "RequestId": "202303031134568758D54369753EAEA42A",
        "Action": "DeleteTags",
        "Version": "2020-04-01",
        "Service": "storage_ebs",
        "Region": "ap-southeast-1"
    },
    "Result": {}
}
```


<span id="error-codes"></span>
## Error codes


|**HttpCode** |**Error Code** |**Error Message** |
|---|---|---|
|400 |ErrTagServiceUnavailable |tag service unavailable |
|400 |ErrTagNotFound |tag not found in request |
|400 |InvalidTagKeyConflict |tag key conflict |
|400 |ErrInvalidTagKey |tag key invalid |
|400 |ErrInvalidTagValue |tag value invalid |
|400 |ErrTagKeyNotFound |tag key not found |
|400 |ErrMaximumResourceIds |too many resource ids |
|400 |ErrResourceTypeNotFound |resource type not found |
|400 |ErrResourceTypeUnknown |resource type unknown |
|400 |ErrInvalidAccountId |account id invalid |
|400 |ErrCallTagPlatform |failed to call tag platform |
|400 |ErrQueryTagDB |db error |
