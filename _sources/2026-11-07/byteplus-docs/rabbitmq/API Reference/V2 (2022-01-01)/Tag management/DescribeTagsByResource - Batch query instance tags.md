---
title: "DescribeTagsByResource - Batch query instance tags"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/DescribeTagsByResource_-_Batch_query_instance_tags"
---

Call the DescribeTagsByResource API to query resources with assigned tags.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* This API supports querying up to 10 tags per call.

* Each tag key supports querying up to 3 tag values simultaneously.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Note

Request frequency: This API limits requests to 100 times/second; the per\-user request frequency limit is 20 times/second.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeTagsByResource&groupName=%E6%A0%87%E7%AD%BE%E7%AE%A1%E7%90%86&serviceCode=RabbitMQ&version=2022-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters of this API and some common parameters are listed below. For more information, see [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|ew6F3N">必选</span> `Example: DescribeTagsByResource`

Action to perform, value: DescribeTagsByResource.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|skgu47">必选</span> `Example value: 2022-01-01`

API version, value: 2022\-01\-01.



**InstanceIds** <span data-label="purple">string[]</span> <span data-api-tag="require|tjAp5o">必选</span> `Example: ["rbtmq-xxxxxx:"]`

Instance IDs bound to tags.

Supports passing multiple instance IDs at once, up to 50 IDs simultaneously.



**TagFilters** <span data-label="purple">object[]</span> `Optional.` `Example value: [{\"Key\":\"test-key:\",\"Value\":\"test-val\"}]`

Filter by the specified tag key. Support filtering by tag key alone or by tag key and tag value together.

For filtering examples, see [Tag-Based Filtering Example](https://docs.byteplus.com/en/docs/kafka/filtering-instances-by-tag).


**Key** <span data-label="purple">string</span> <span data-api-tag="require|M3P2SN">必选</span> `Example value: owner`

Tag key.



**Value** <span data-label="purple">string</span> `Optional` `Example value: zhangsan`

Tag value.




**PageSize** <span data-label="purple">integer</span> <span data-api-tag="require|K7LywH">必选</span> `Example value: 1`

This parameter represents the number of data items per page when displaying paged query results. The value range is 1 to 100.



**PageNumber** <span data-label="purple">integer</span> <span data-api-tag="require|lMHNz9">必选</span> `Example value: 1`

This parameter indicates the page number when displaying paged query results. The minimum supported value is 1.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the unique response parameters of this API are listed below. For more details, see [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Total** <span data-label="purple">integer</span> `Example value: 10`

Total number of tags matching the query conditions.



**TagResources** <span data-label="purple">object[]</span> `Example: [ { "InstanceId": "rbtmq-xxxx", "Key": "test-key", "Value": "test-val", }, ]`

Tag details.


**InstanceId** <span data-label="purple">string</span> `Example: rbtmq-xxx`

Instance ID.



**Value** <span data-label="purple">string</span> `Example value: zhangsan`

Tag value.



**Key** <span data-label="purple">string</span> `Example value: owner`

Tag key.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
POST https://rabbitmq.byteplusapi.com/?Action=DescribeTagsByResource&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: rabbitmq.byteplusapi.com
X-Date: 20210328T100802Z
Authorization: HMAC-SHA256 Credential=AK********/20210328/cn-beijing/rabbitmq/request, SignedHeaders=x-date, Signature=********

{
   "InstanceIds":["rbtmq-xxxxxx:"],
   "TagFilters":[{"Key":"test-key:","Value":"test-val"}],
   "PageNumber":1,
   "PageSize":10,
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```text
{
    "ResponseMetadata": {
        "RequestId": "20230217175421E698024A11179196218F",
        "Action": "DescribeTagsByResource",
        "Version": "2022-01-01",
        "Service": "RabbitMQ",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "ToTal":1
        "TagResource": [
            {
                "InstanceId": "rbtmq-xxxx",
                "Key": "test-key",
                "Value": "test-val",
            },
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The following table lists error codes related to this interface and business logic. Refer to the [public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) section for common error codes.


|Status code |Error code |Error message |Specifications |
|---|---|---|---|
|403 |OperationDenied.InvalidInstanceStatus |The operation is not valid for the current status of the instance. |The current instance status does not allow this operation. |
|404 |InvalidInstanceId.NotFound |The specified Instance ID does not exist. |Instance does not exist. |
|500 |InternalError |The request failed due to some unknown error, exception or failure. |Internal error, please try again later. |
