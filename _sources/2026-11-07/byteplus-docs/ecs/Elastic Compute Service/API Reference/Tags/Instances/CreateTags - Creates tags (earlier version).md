---
title: "CreateTags - Creates tags (earlier version)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/CreateTags"
---

Call the CreateTags operation to associate tags with one or multiple resources.

<span id=".5L2_55So6K-05piO"></span>
## Usage notes

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This page describes the tag\-targeted operation of the earlier version, which may no longer be maintained in the future. Tag\-targeted interfaces of the new version support a wider range of scenarios. We recommend that new users use tag\-targeted interfaces of the following new versions. </div>



* <div data-tips="true" data-tips-type="warning"><a href="https://docs.byteplus.com/en/docs/ecs/TagResources">TagResources \- Creates tags (new version)</a></div>


* <div data-tips="true" data-tips-type="warning"><a href="https://docs.byteplus.com/en/docs/ecs/UntagResources">UntagResources \- Deletes tags (new version)</a></div>


* <div data-tips="true" data-tips-type="warning"><a href="https://docs.byteplus.com/en/docs/ecs/ListTagsForResources">ListTagsForResources \- Queries tag resources (new version)</a></div>



<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes


* For more tag details, refer to [Tag overview](https://docs.byteplus.com/en/docs/ecs/Tag-overview).

* One resource can be associated with up to 50 tags, and up to 20 tags can be associated per interface call.

* For the same resource, if you add a tag with an existing tag key, the new tag value automatically overrides the original one.

* Tags cannot be associated with resources in the "Deleting" status.


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=CreateTags&groupName=%E6%A0%87%E7%AD%BE&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|tsSg7e">必选</span> `Sample value: CreateTags`

The action that you want to perform. Value: CreateTags.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|SiWvZx">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**ClientToken** <span data-label="purple">string</span> `Optional` `Sample value: 333456899ff****`

The ClientToken is used to ensure the request idempotency. You can use the client to automatically generate a token, but you must make sure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

Value: Only ASCII characters are supported. The length is no more than 64 ASCII characters.



**ResourceIds.N** <span data-label="purple">string[]</span> `Optional` `Sample value: ResourceIds.1=i-l8u0p77yseabkpak****&ResourceIds.2=i-l8u0p7xyseabkbak****`

The resource ID.


* Argument \- N: indicates the serial number of the resource. Valid range: 1\-50.

* Separate resources with &.



**ResourceType** <span data-label="purple">string</span> <span data-api-tag="require|OOAPvh">必选</span> `Sample value: instance`

The resource type. Valid values:


* instance: instance

* image: image

* reservedinstance: RI

* scheduledinstance: ESI

* keypair: key pair



**Tags.N.Key** <span data-label="purple">string[]</span> <span data-api-tag="require|k4SKNi">必选</span> `Sample value: Tags.1.Key=k1`

The key of the tag associated with the resource.


* Argument \- N: specifies the serial number of the tag key. Valid range: 1–20.

* Separate multiple tag keys with &.


Naming rules:


* Cannot start with `volc:` or `sys:` in any case form.

> Tags that start with `volc:` or `sys:` are reserved for the system. You cannot create tags starting with them.


* Only language characters, digits, spaces, and English symbols of "_", ".", ":", "/", "=", "+", "\-", and "@" are allowed.

* It must be 1 to 128 characters in length.



**Tags.N.Value** <span data-label="purple">string[]</span> `Optional` `Sample value: Tags.1.Value=v1`

The value of the tag associated with the resource.


* Argument \- N: specifies the serial number of the tag value. Valid range: 1–20.

* Separate multiple tag values with ampersands (&).


Naming rules:


* Only language characters, digits, spaces, and English symbols of " _", ".", ":", "/", "=", "+", "\-", and "@" are allowed.

* It must be 0 to 256 characters in length.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following<a href="https://docs.byteplus.com/en/docs/49/12883#.6ZSZ6K-v56CB"> error codes </a>for the operation are returned only when invalid values are specified for request parameters. If valid values are specified for the request parameters, no error code is displayed, and a status code of 200 is returned. However, this does not mean that the operation on all resources is successful. To view the operation result on a single resource, see the information in the following response parameters.</div>




**OperationDetails** <span data-label="purple">object[]</span> `Sample value: --`

The operation details.


**Error** <span data-label="purple">object</span> `Sample value: --`

The error message for the resource being operated on.


**Code** <span data-label="purple">string</span> `Sample value: InvalidInstance.NotFound`

The error code for the failure of a specific individual request during batch operations. Valid values:


* InvalidResourceId.NotFound: The specified resource does not exist.

* InvalidResourceStatus: The current status of the resource does not support this operation.

* OperationDenied.ResourceLocked: The specified operation is rejected because your resource has been locked by another operation.

* InternalError: An internal error occurred. Try again. If multiple attempts fail, submit a ticket.

* FlowLimitExceeded: You have exceeded the rate limit for resource requests.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Each <code>Code</code> corresponds to a <code>Message</code> in sequence.</div>




**Message** <span data-label="purple">string</span> `Sample value: The specified instance does not exist.`

The error information for the failure of a specific individual request during batch operations. Valid values:


* The specified ResourceId does not exist.

* The status of the specified resource does not support this request.

* The specified operation is denied as your resource is locked for another operation.

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
GET /?Action=CreateTags&Version=2020-04-01&ResourceType=instance&ResourceIds.1=i-l8u0p77yseabkpak****&ResourceIds.2=i-l8u0p7xyseabkbak****&Tags.1.Key=k1&Tags.1.Value=v1 HTTP/1.1
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
        "Action": "CreateTags",
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
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken is invalid. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified tag key is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified tag value is invalid. |
|400 |LimitExceeded.MaximumResourceIds |You've reached the limit on the number of ResourceIds that you can set. |The specified number of resource IDs exceeds the limit. |
|400 |LimitExceeded.MaximumTags |You've reached the limit on the number of tags that you can create. |The specified tag number exceeds the maximum limit. |
|400 |MissingParameter.ResourceType |The required parameter ResourceType is not supplied. |The ResourceType parameter cannot be left empty. |
|400 |QuotaExceeded.MaximumTags |You've reached the limit on the number of Tags that you can create. |The upper limit of tags that can be created for a resource has been reached. |
|404 |InvalidResourceId.NotFound |The specified ResourceId does not exist. |The specified resource does not exist. |
|404 |InvalidResourceType.NotFound |The specified ResourceType does not exist. |The specified resource type does not exist. |
|404 |InvalidTag.NotFound |The specified tag does not exist. |The specified key value does not exist. |
|409 |InvalidTagKey.Conflict |The specified TagKey already exists. |The specified tag key already exists. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The previous idempotent request is still being processed. Please try again later. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again. If multiple attempts fail, submit a ticket. |
