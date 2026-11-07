---
title: "UntagResources - Untags resources"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/UntagResources"
---

Remove user tags from a scaling group.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=UntagResources&groupName=%E6%A0%87%E7%AD%BE&serviceCode=auto_scaling&version=2020-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|iSdyC5">必选</span> `Sample value: UntagResources`

The action that you want to perform. Value: UntagResources.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|5YTHTG">必选</span> `Sample value: 2020-01-01`

The version of the API. Value: 2020\-01\-01.



**ResourceIds.N ** <span data-label="purple">string[] </span><span data-api-tag="require|Kzq2JE">必选</span> `Sample value: scg-ybmssdnnhn5pkgyd****`

Resource ID. You can call [DescribeScalingGroups](https://docs.byteplus.com/en/docs/as/DescribeScalingGroups) to query the scaling group ID.


* Argument \- N: Specifies the serial number of the resource. Valid value: 1\-20.



**ResourceType ** <span data-label="purple">string </span><span data-api-tag="require|5OKozO">必选</span> `Sample value: scalinggroup`

Resource type. Valid values:


* scalinggroup: The scaling group.



**TagKeys.N ** <span data-label="purple">string[] </span><span data-api-tag="require|x7lNJj">必选</span> `Sample value: k1`

The key of the tag.


* Parameter \- N: Specifies the serial number of the tag key. Value: 1–50.

* Separate multiple tag keys with &.


Naming rules:


* It cannot start with `volc:` or `sys:` in any combination of uppercase and lowercase letters.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Tags that start with <code>volc:</code> or <code>sys:</code> are reserved for the system. You cannot create tags starting with them.   </div>
   

* Only letters, digits, spaces, and the following symbols are allowed: "_", ".", ":", "/", "=", "+", "\-", and "@".

* It must be 1 to 128 characters in length.

> Keys of the same resource must be unique.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**OperationDetails ** <span data-label="purple">object[] </span>`Sample value: --`

The operation details. If an empty array is returned, this indicates the operation succeeded.


**ResourceId ** <span data-label="purple">string </span>`Sample value: scg-ybmssdnnhn5pkgyd****`

Resource ID.



**Error ** <span data-label="purple">object </span>`Sample value: --`

The error details about the resource operation.


**Code ** <span data-label="purple">string </span>`Sample value: OperationDenied.ResourceLocked`

Error code.



**Message ** <span data-label="purple">string </span>`Sample value: The specified operation is denied as your resource is locked for another operation.`

The error details.





&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=UntagResources&ResourceIds.1=scg-ybmssdnnhn5pkgyd****&ResourceType=scalinggroup&TagKeys.1=k1&Version=2020-01-01 HTTP/1.1
Host: auto-scaling.cn-beijing.byteplusapi.com.cn
X-Date: 20240507T113257Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240507/cn-beijing/auto_scaling/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "2024050719330708921214609005A3D7",
    "Version": "2020-01-01",
    "Service": "auto_scaling",
    "Region": "cn-beijing"
  },
  "Result": {
    "OperationDetails": [
      {
        "ResourceId": "scg-ybmssdnnhn5pkgyd****",
        "Error": {
          "Code": "OperationDenied.ResourceLocked",
          "Message": "The specified operation is denied as your resource is locked for another operation."
        }
      }
    ]
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/as/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified tag value is invalid. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified tag key is invalid. |
|400 |MissingParameter.ResourceIds |The required parameter ResourceIds are not supplied. |The resource ID cannot be empty. |
|400 |LimitExceeded.ResourceIds |You've reached the limit on the number of ResourceIds that you can set. |The upper limit of the number of resource IDs that can be set is reached. |
|400 |LimitExceeded.TagKeys |You've reached the limit on the number of tag keys that you can delete. |The upper limit of the number of tag keys that can be deleted is reached. |
|404 |InvalidResourceType.NotFound |The specified ResourceType does not exist. |The specified resource type does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
