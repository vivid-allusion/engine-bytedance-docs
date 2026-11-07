---
title: "DeleteTags - Deletes tags (earlier version)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DeleteTags"
---

Call the DeleteTags operation to delete tags from one or multiple resources.

<span id=".5L2_55So6K-05piO"></span>
## Usage notes

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">This page describes the tag\-targeted operation of the earlier version, which may be ​discontinued in the future. Tag\-targeted interfaces of the new version support a wider range of scenarios. We recommend that new users use tag\-targeted interfaces of the following new versions.</div>



* <div data-tips="true" data-tips-type="warning"><a href="https://docs.byteplus.com/en/docs/ecs/TagResources">TagResources \- Creates tags (new version)</a></div>


* <div data-tips="true" data-tips-type="warning"><a href="https://docs.byteplus.com/en/docs/ecs/UntagResources">UntagResources \- Deletes tags (new version)</a></div>


* <div data-tips="true" data-tips-type="warning"><a href="https://docs.byteplus.com/en/docs/ecs/ListTagsForResources">ListTagsForResources \- Queries tagged resources (new version)</a></div>



<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes


* This operation supports deleting a maximum of 20 tags per query.

* Repeatedly disassociating a tag overrides the original result and updates the tag value.


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DeleteTags&groupName=%E6%A0%87%E7%AD%BE&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|T7cZ6F">必选</span> `Sample value: DeleteTags`

The operation that you want to perform. Value: DeleteTags.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|qFdy2k">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**ClientToken** <span data-label="purple">string</span> `Optional` `Sample value: 333456899ff****`

The ClientToken is used to ensure the request idempotency. You can use the client to automatically generate a token, but you must make sure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

Value: Only ASCII characters are supported. The length is no more than 64 ASCII characters.



**ResourceIds.N** <span data-label="purple">string[]</span> <span data-api-tag="require|HgO4tw">必选</span> `Sample value: ResourceIds.1=i-l8u0p77yseabkpak****&ResourceIds.2=i-l8u0p7xyseabkbak****`

The resource ID.


* Argument \- N: indicates the serial number of the resource. Valid range: 1\-50.

* Separate resources with &.



**ResourceType** <span data-label="purple">string</span> <span data-api-tag="require|kouec2">必选</span> `Sample value: instance`

The resource type. Valid values:


* instance: instance

* image: image

* reservedinstance: Reserved Instances (RI)

* scheduledinstance: Elastic Scheduled Instances (ESI)

* keypair: key pair



**TagKeys.N** <span data-label="purple">string[]</span> <span data-api-tag="require|0HGPWe">必选</span> `Sample value: TagKeys.1=k1`

The tag key of the tag to be deleted from the resource.


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

Only the response parameters specific to this operation are listed below. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following <a href="https://docs.byteplus.com/en/docs/49/12884#.6ZSZ6K-v56CB">error codes</a> for the operation are returned only when invalid values are specified for request parameters. If valid values are specified for the request parameters, no error code is displayed, and a status code of 200 is returned. However, this does not mean that the operation on all resources is successful. To view the operation result on a single resource, see the information in the following response parameters.</div>




**OperationDetails** <span data-label="purple">object[]</span> `Sample value: --`

The operation details.


**Error** <span data-label="purple">object</span> `Sample value: --`

The error message for the resource being operated on.


**Code** <span data-label="purple">string</span> `Sample value: InvalidInstance.NotFound`

The error code for the failure of a specific individual request during batch operations. Valid values:


* InvalidResourceId.NotFound: The specified resource does not exist.

* InternalError: An internal error occurred. Try again. If multiple attempts fail, submit a ticket.

* FlowLimitExceeded: You have exceeded the rate limit for resource requests.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Each <code>Code</code> corresponds to a <code>Message</code> in sequence.</div>




**Message** <span data-label="purple">string</span> `Sample value: The specified instance does not exist.`

The error information for the failure of a specific individual request during batch operations. Valid values:


* The specified ResourceId does not exist.

* An internal error has occurred.

* You've reached the limit on request rate of resources.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Each <code>Code</code> corresponds to a <code>Message</code> in sequence.</div>





**ResourceId** <span data-label="purple">string</span> `Sample value: i-l8u0p77yseabkpak****`

The ID of the target resource.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DeleteTags&Version=2020-04-01&ResourceType=instance&ResourceIds.1=i-l8u0p77yseabkpak****&ResourceIds.2=i-l8u0p7xyseabkbak****&TagKeys.1=k1 HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
ServiceName: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "DeleteTags",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "OperationDetails": [
            {
                "Error": null,
                "ResourceId": "i-l8u0p77yseabkpak****"
            },
            {
                "Error": {
                    "Code": "InvalidResourceId.NotFound",
                    "Message": "The specified ResourceId does not exist."
                },
                "ResourceId": "i-l8u0p7xyseabkbak****"
            }
        ]
    }
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
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The previous idempotent request is still in process. Please try again later. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
