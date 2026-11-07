---
title: "RemoveTagsFromResource - Unbind instance tags"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/RemoveTagsFromResource_-_Unbind_instance_tags"
---

Call the RemoveTagsFromResource API to unbind tags from one or more instances.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Note

Request frequency: This API limits requests to 40 times per second. The per\-user request frequency limit is 8 times per second.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=RemoveTagsFromResource&groupName=%E6%A0%87%E7%AD%BE%E7%AE%A1%E7%90%86&serviceCode=RabbitMQ&version=2022-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters of this API and some common parameters are listed below. For more information, see [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|gvsAjN">必选</span> `Example value: RemoveTagsFromResource`

Action to perform, value: RemoveTagsFromResource.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|iAKrnN">必选</span> `Example value: 2022-01-01`

API version, value: 2022\-01\-01.



**InstanceIds** <span data-label="purple">string[]</span> <span data-api-tag="require|GF0Vfb">必选</span> `Example values: ["rbtmq-sdgsxxxx","rbtmq-fgerfxxx"]`

The instance ID for unbinding tags.

Supports importing multiple instance IDs at once, up to 50 instance IDs simultaneously.



**TagKeys** <span data-label="purple">string[]</span> `Optional` `Example value: ["key1", "key2"]`

Tags to delete.

Supports importing multiple tag keys at once, up to 20 tag keys simultaneously.



**All** <span data-label="purple">boolean</span> `Optional` `Example value: true`

Whether to unbind all tags from the specified instance The value range is as follows:


* true: unbind all tags from the specified instance

* false: (default) do not unbind all tags from the specified instance

   The All parameter only takes effect when TagKeys is empty



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API has no unique response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
POST https://rabbitmq.byteplusapi.com/?Action=RemoveTagsFromResource&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: rabbitmq.byteplusapi.com
X-Date: 20210328T100802Z
Authorization: HMAC-SHA256 Credential=AK********/20210328/cn-beijing/rabbitmq/request, SignedHeaders=x-date, Signature=********

{
   "InstanceIds":["rbtmq-xxxxxx:"],
   "TagKeys":["instancetype","chargetype"],
   "All":false
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```text
{
    "ResponseMetadata": {
        "RequestId": "20230217175421E698024A11179196218F",
        "Action": "RemoveTagsFromResource",
        "Version": "2022-01-01",
        "Service": "RabbitMQ",
        "Region": "cn-guangzhou"
    },
    "Result": null
}

```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The following table lists error codes related to this interface and business logic. Refer to the [public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) section for common error codes.


|Status code |Error code |Error message |Specifications |
|---|---|---|---|
|403 |OperationDenied.AccountNotAuthorized |You are not authorized to perform this operation. |You do not have the required permissions. Authorize or switch accounts and try again. |
|403 |OperationDenied.InvalidInstanceStatus |The operation is not valid for the current status of the instance. |The operation is not allowed for the current instance status. |
|404 |InvalidInstanceId.NotFound |The specified Instance ID does not exist. |Instance does not exist. |
|500 |InternalError |The request failed due to some unknown error, exception or failure. |Internal error, please try again later. |
