---
title: "AddTagsToResource - Add instance tags"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/AddTagsToResource_-_Add_instance_tags"
---

Call the AddTagsToResource API to bind tags to a specified instance.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* When setting tags, the tag key (Key) and tag value (Value) must meet certain rules. For details, see [Tag setting rules](https://docs.byteplus.com/en/docs/rabbitmq/Bind_tags#.5qCH562-6K6-572u6KeE5YiZ).

* Tag keys can not repeat multiple tags under the same instance, and each tag key can have only one tag value.

* If the newly bound tag key overlaps with an existing tag key on the instance, the new tag value will overwrite the original tag value. Proceed with caution.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Note

Request frequency: This API limits requests to 40 times per second. The per\-user request frequency limit is 8 times per second.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=AddTagsToResource&groupName=%E6%A0%87%E7%AD%BE%E7%AE%A1%E7%90%86&serviceCode=RabbitMQ&version=2022-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters of this API and some common parameters are listed below. For more information, see [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|Zt9xgn">必选</span> `Example value: AddTagsToResource`

The action to perform, value: AddTagsToResource.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|OExssp">必选</span> `Example value: 2022-01-01`

API version, value: 2022\-01\-01.



**InstanceIds** <span data-label="purple">string[]</span> <span data-api-tag="require|E9eXxa">必选</span> `Example value: [\"rbtmq-xxxxxx\"]`

The instance ID to bind tags to.

Supports importing multiple instance IDs at once, up to 50 instance IDs simultaneously.



**Tags** <span data-label="purple">object[]</span> <span data-api-tag="require|AMNYl8">必选</span> `Example value: [{\"Key\":\"testKey\",\"Value\":\"testVal\"}]`

The array object of tag keys and tag values that need to be bound."


* Supports importing multiple sets of tag key\-value pairs at once, up to 20 sets simultaneously.

* The tag key value must meet the setting rules. See [tag setting rules](https://docs.byteplus.com/en/docs/rabbitmq/Bind_tags#.5qCH562-6K6-572u6KeE5YiZ) for details.



**Key** <span data-label="purple">string</span> <span data-api-tag="require|pVDPbP">必选</span> `Example value: owner`

Key of the tag.



**Value** <span data-label="purple">string</span> `Optional` `Example value: zhangsan`

Tag value.




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API has no unique response parameters. For more information, see [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
POST https://rabbitmq.byteplusapi.com/?Action=AddTagsToResource&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: rabbitmq.byteplusapi.com
X-Date: 20210328T100802Z
Authorization: HMAC-SHA256 Credential=AK********/20210328/cn-beijing/rabbitmq/request, SignedHeaders=x-date, Signature=********

{
   "InstanceIds":["rbtmq-xxxxxx"],
   "Tags":[{"Key":"test","Value":"test"}]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```text
{
    "ResponseMetadata": {
        "RequestId": "20230217175421E698024A11179196218F",
        "Action": "AddTagsToResource",
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
|403 |OperationDenied.InvalidInstanceStatus |The operation is not valid for the current status of the instance. |The current instance status does not allow this action. |
|404 |InvalidInstanceId.NotFound |The specified Instance ID does not exist. |The instance does not exist. |
|500 |InternalError |The request failed due to some unknown error, exception or failure. |Internal error, please try again later. |
