---
title: "DescribeInstanceTypeFamilies - Queries instance type families"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DescribeInstanceTypeFamilies"
---

Call the DescribeInstanceTypeFamilies operation to query information about instance type families provided by ECS.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeInstanceTypeFamilies&groupName=%E5%AE%9E%E4%BE%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The table below lists only the request parameters specific to this operation and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|RAo7ie">必选</span> `Sample value: DescribeInstanceTypeFamilies`

The operation that you want to perform. Valid value: DescribeInstanceTypeFamilies.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|ymHVA9">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**Generation** <span data-label="purple">string</span> `Optional` `Sample value: ecs-1`

The generation of instance type families. Valid values:


* ecs\-1: The 1st\-generation instance type.

* ecs\-2: The 2nd\-generation instance type.

* ecs\-3: The 3rd\-generation instance type.


For more information, see [Best practices of instance selection](https://docs.byteplus.com/en/docs/ecs/Instance-type-selection-best-practice) and [Instance types](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types).



**ZoneId** <span data-label="purple">string</span> `Optional` `Sample value: cn-beijing-a`

The ID of the availability zone where the instance is located.

You can call the [DescribeZones](https://docs.byteplus.com/en/docs/ecs/DescribeZones) operation to query the availability zones in the same region.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**InstanceTypeFamilies** <span data-label="purple">object[]</span> `Sample value: --`

The information about instance type families.


**Generation** <span data-label="purple">string</span> `Sample value: ecs-2`

The generation of instance type families.



**InstanceTypeFamily** <span data-label="purple">string</span> `Sample value: ecs.g2i`

The instance type family.



**ZoneIds** <span data-label="purple">string[]</span> `Sample value: cn-beijing-a`

The availability zone ID where the instance type families are located.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeInstanceTypeFamilies&Version=2020-04-01&ZoneId=cn-beijing-a HTTP/1.1
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
        "Action": "DescribeInstanceTypeFamilies",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstanceTypeFamilies": [
            {
                "InstanceTypeFamily": "ecs.c1ie",
                "ZoneIds": [
                    "cn-beijing-a"
                ],
                "Generation": "ecs-1"
            },
            {
                "InstanceTypeFamily": "ecs.g2i",
                "ZoneIds": [
                    "cn-beijing-a"
                ],
                "Generation": "ecs-2"
            }
          ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|404 |InvalidZone.NotFound |The specified zone does not exist. |The specified availability zone does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
