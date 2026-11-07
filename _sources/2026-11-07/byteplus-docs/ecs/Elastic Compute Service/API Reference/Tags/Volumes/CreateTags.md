---
title: "CreateTags"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/CreateTags-01"
---

Call CreateTags to add user tags to one or more resources.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For more information on tags, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Tag-overview">Tag overview</a>.</div>


* <div data-tips="true" data-tips-type="tip">Up to 50 tags can be added to a resource. You are allowed to call this API action to add up to 20 tags at a time.</div>


* <div data-tips="true" data-tips-type="tip">If you add a tag with the same tag key as an existing tag to a resource, the new tag value overwrites the original tag value.</div>


* <div data-tips="true" data-tips-type="tip">You cannot add tags to resources in the <strong>Deleting</strong> state.</div>



<span id="request-parameters"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Action |String |Yes |CreateTags |The action that you want to perform. Value: CreateTags. |
|ResourceType |String |Yes |instance |The resource type. Valid values:<br><br><br>* volume |
|ResourceIds.N |String |Yes |ResourceIds.1=vol\-76pwr6rilv8lzwxv\*\*\*\*&ResourceIds.2=vol\-76pwr6rilv8lzwxv\*\*\*\* |The resource ID.<br><br><br>* Parameter \- N specifies the serial number of the resource. Valid values: 1–50.<br><br>* Separate resources with ampersands ( & ). |
|Tags.N.Key |String |Yes |Tags.1.Key=k1 |The tag key of the user tag you want to add to the resource.<br><br><br>* Parameter \- N specifies the serial number of the tag key. Valid values: 1–20.<br><br>* Separate tag keys with ampersands ( & ).<br><br><br>Name the tag key as follows:<br><br><br>* Do not start with `volc:` or `sys:` in any uppercase or lowercase form.`volc:` or `sys:` is the start of the system reserved tag keys that cannot be created.<br><br>* The value can contain only letters, digits, spaces, and the following special characters: _ . : / = + \- @<br><br>* The value can be 1 to 128 characters in length. |
|Tags.N.Value |String |No |Tags.1.Value=v1 |The tag value of the user tag you want to add to the resource.<br><br><br>* Parameter \- N specifies the serial number of the tag value. Valid values: 1–20.<br><br>* Separate tag values with ampersands ( & ).<br><br><br>Name the tag key as follows:<br><br><br>* The value can contain only letters, digits, spaces, and the following special characters: _ . : / = + \- @<br><br>* This parameter can be 0–256 characters in length. |


<span id="response-parameters"></span>
## Response parameters


|Name |Type |Example |Description |
|---|---|---|---|
|OperationDetails |Array of Struct |N/A |The operation details. If the details are empty, it indicates a successful creation. |


<span id="sample-request"></span>
## Sample request

```Plain Text
GET /?Action=CreateTags&Version=2020-04-01&ResourceType=volume&ResourceIds.1=vol-76pwr6rilv8lzwxv*****&ResourceIds.2=vol-76pwr6rilv8lzwxv****&Tags.1.Key=tag&Tags.1.Value=test HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
ServiceName: storage_ebs
```


<span id="sample-response"></span>
## Sample response


* Successful response


```Plain Text
{
    "ResponseMetadata": {
        "RequestId": "202303031059488DC8442420A69FB06C4E",
        "Action": "CreateTags",
        "Version": "2020-04-01",
        "Service": "storage_ebs",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "OperationDetails": []
    }
}
```



* Failed response


```Plain Text
{
    "ResponseMetadata": {
        "RequestId": "20230303112058C237F8584025A6A60F6C",
        "Action": "CreateTags",
        "Version": "2020-04-01",
        "Service": "storage_ebs",
        "Region": "ap-southeast-1",
        "Error": {
            "Code": "ErrPartTagFailed",
            "Message": "part tag failed"
        }
    },
    "Result": null
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
|400 |ErrSystemTagExceedQuota |system tag exceed quota |
|400 |ErrCustomTagExceedQuota |custom tag exceed quota |
|400 |ErrResourceExcluded |resource excluded |
|400 |ErrResourceNotFound |resource not found |
|400 |ErrPartTagFailed |part tag failed |
|400 |ErrCallTagPlatform |failed to call tag platform |
|400 |ErrQueryTagDB |db error |
