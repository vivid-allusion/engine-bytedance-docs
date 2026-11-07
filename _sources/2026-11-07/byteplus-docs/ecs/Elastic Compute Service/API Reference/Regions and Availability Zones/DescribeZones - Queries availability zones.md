---
title: "DescribeZones - Queries availability zones"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DescribeZones"
---

Call the DescribeZones operation to query the availability zones in a region.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeZones&groupName=%E5%9C%B0%E5%9F%9F&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|iT0fxq">必选</span> `Sample value: DescribeZones`

The operation that you want to perform. Value: DescribeZones.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|U0kipN">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**ZoneIds.N** <span data-label="purple">string[]</span> `Optional` `Sample value: ZoneIds.1=cn-beijing-a`

The availability zone ID. Up to 20 availability zone IDs are supported.


* Argument \- N: specifies the serial number of the availability zone ID.

* Separate multiple availability zone IDs with &.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Zones** <span data-label="purple">object[]</span> `Sample value: --`

The availability zone information.


**ZoneId** <span data-label="purple">string</span> `Sample value: cn-beijing-a`

The availability zone ID.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeZones&Version=2020-04-01 HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202106111445100102252431000052****",
        "Action": "DescribeZones",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "Zones": [
            {
                "ZoneId": "cn-beijing-a"
            },
            {
                "ZoneId": "cn-beijing-b"
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
|400 |InvalidArgument |The specified argument is invalid. |The specified parameter is invalid. |
|400 |LimitExceeded.MaximumZoneIds |You've reached the limit on the number of ZoneIds that you can set. |The number of specified zone IDs exceeds the upper limit. |
|404 |InvalidZone.NotFound |The specified zone does not exist. |The specified availability zone does not exist. |
|429 |FlowLimitExceeded |You've reached the limit on request rate of resources. |Resource request rate exceeds the limit. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
