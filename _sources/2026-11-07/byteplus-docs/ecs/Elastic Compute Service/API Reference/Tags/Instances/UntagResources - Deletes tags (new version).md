---
title: "UntagResources - Deletes tags (new version)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/UntagResources"
---

Call the UntagResources operation to delete tags from one or multiple resources.

<span id=".5L2_55So6K-05piO"></span>
## Usage notes

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>



* <div data-tips="true" data-tips-type="warning">This page describes the tag\-targeted operation of the new version, which is strongly recommended for new users. </div>


* <div data-tips="true" data-tips-type="warning">Tag\-targeted operations of the earlier version may no longer be maintained in the future. If you still need to use them, refer to:</div>


   * <div data-tips="true" data-tips-type="warning"><a href="https://docs.byteplus.com/en/docs/ecs/CreateTags">CreateTags \- Creates tags (earlier version)</a></div>


   * <div data-tips="true" data-tips-type="warning"><a href="https://docs.byteplus.com/en/docs/ecs/DeleteTags">DeleteTags \- Deletes tags (earlier version)</a></div>


   * <div data-tips="true" data-tips-type="warning"><a href="https://docs.byteplus.com/en/docs/ecs/DescribeTags">DescribeTags \- Queries tagged resources (earlier version)</a></div>



<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes


* This operation supports deleting a maximum of 20 tags per query.

* Repeatedly disassociating a tag overrides the original result and updates the tag value.


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=UntagResources&groupName=%E6%A0%87%E7%AD%BE&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|5PulWO">必选</span> `Sample value: UntagResources`

The action that you want to perform. Value: UntagResources.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|UlOB7l">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**ResourceIds.N** <span data-label="purple">string[]</span> <span data-api-tag="require|oMYjd2">必选</span> `Sample value: ResourceIds.1=i-l8u0p77yseabkpak****&ResourceIds.2=i-l8u0p7xyseabkbak****`

The resource ID.


* Argument \- N: indicates the serial number of the resource. Valid range: 1\-50.

* Separate resources with &.



**ResourceType** <span data-label="purple">string</span> <span data-api-tag="require|egeXBd">必选</span> `Sample value: instance`

The resource type. Valid values:


* instance: instance

* image: image

* reservedinstance: Reserved Instances (RI)

* scheduledinstance: Elastic Scheduled Instances (ESI)

* key pair: key pair



**TagKeys.N** <span data-label="purple">string[]</span> <span data-api-tag="require|rGxrK2">必选</span> `Sample value: TagKeys.1=k1`

The key of the custom tag to be deleted from the resource.


* Argument \- N: specifies the serial number of the tag key. Valid range: 1–20.

* Separate multiple tag keys with &.


Naming rules:


* Cannot start with `volc:` or `sys:` in any case form.

> Tags that start with `volc:` or `sys:` are reserved for the system. You cannot create tags starting with them.


* It can contain only language characters, digits, spaces, and English symbols of " _", ".", ":", "/", "=", "+", "\-", and "@".

* It must be 1 to 128 characters in length.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId** <span data-label="purple">string</span> `Sample value: 202308101209161A3FE8E1FC09E29F****`

The request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=UntagResources&Version=2020-04-01&ResourceType=instance&ResourceIds.1=i-l8u0p77yseabkpak****&ResourceIds.2=i-l8u0p7xyseabkbak****&TagKeys.1=k1 HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
ServiceName: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
"ResponseMetadata": {
        "RequestId": "202308101209161A3FE8E1FC09E29F****",
        "Action": "UntagResources",
        "Version": "2020-01-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20230810120154605002C8D8D494A3****"
    }
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |IdempotentParameterMismatch |The request uses the same client token as a previous, but non\-identical request. Do not reuse a client token with different requests, unless the requests are identical. |The idempotent parameters are inconsistent. |
|400 |InvalidArgument |The specified argument is invalid. |The specified parameter is invalid. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken is invalid. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified tag key is invalid. |
|400 |LimitExceeded.MaximumResourceIds |You've reached the limit on the number of ResourceIds that you can set. |The specified number of resource IDs exceeds the limit. |
|400 |LimitExceeded.MaximumTagKeys |You've reached the limit on the number of TagKeys that you can set. |The specified tag key is out of range. |
|404 |InvalidResourceId.NotFound |The specified ResourceId does not exist. |The specified resource does not exist. |
|404 |InvalidResourceType.NotFound |The specified ResourceType does not exist. |The specified resource type does not exist. |
|404 |InvalidTagKey.NotFound |The specified TagKey does not exist. |The specified tag key does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The previous idempotent request is still being processed. Please try again later. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
