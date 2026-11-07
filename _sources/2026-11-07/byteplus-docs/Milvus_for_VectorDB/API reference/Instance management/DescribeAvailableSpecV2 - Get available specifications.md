---
title: "DescribeAvailableSpecV2 - Get available specifications"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/DescribeAvailableSpecV2_-_Get_available_specifications"
---

Call DescribeAvailableSpecV2 to get available specifications.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeAvailableSpecV2&groupName=%E5%AE%9E%E4%BE%8B%E7%AE%A1%E7%90%86&serviceCode=milvus&version=2023-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters of this API and some common parameters are listed below. For more information, see [Public parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|vL7HKg">必选</span> `Example value: DescribeAvailableSpecV2`

Action to execute, value: DescribeAvailableSpecV2.



**Version**<span data-label="purple"> string </span><span data-api-tag="require|r72rnW">必选</span>`Example: 2023-01-01`

API version, value: 2023\-01\-01.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters unique to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**SpecList ** <span data-label="purple">object[] </span>`Example value: -`

Specification list.


**SpecType ** <span data-label="purple">string </span>`Example value: -`

Specification resource type.



**DisplayName ** <span data-label="purple">string </span>`Example value: 4 cores 8 G`

Display name.



**SpecName ** <span data-label="purple">string </span>`Example value: -`

Specification name.



**Cpu ** <span data-label="purple">long </span>`Example value: -`

CPU core count.



**Memory ** <span data-label="purple">long </span>`Example value: -`

Memory size in GB.



**ItemType ** <span data-label="purple">string </span>`example value: -`

Resource type.

\-PERFORMANCE: Performance.

\-CAPACITY: Capacity.




**NodeSupportSpecList ** <span data-label="purple">object[] </span>`Example value: -`

Specification list supported by each node type.


**NodeType ** <span data-label="purple">string </span>`Example value: QUERY_NODE`

Node type.



**MaxNodeNum ** <span data-label="purple">integer </span>`Example value: -`

Maximum number of nodes supported under the current type.



**SpecName ** <span data-label="purple">string[] </span>`Example value: -`

Specification list supported under the current node type.




**ZoneSupportSpecList ** <span data-label="purple">object[] </span>`Example value: -`

List of specifications supported by the availability zone.


**SpecName ** <span data-label="purple">string[] </span>`Example value: -`

Specification list supported in the current availability zone.



**SoldOutSpecName ** <span data-label="purple">string[] </span>`Example value: -`

List of sold\-out specification names in the current Availability Zone.



**ZoneId ** <span data-label="purple">string </span>`Example value: -`

Availability zone ID.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
{}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```text
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeAvailableSpecV2",
        "Version": "2023-01-01",
        "Service": "***",
        "Region": "cn-north-1"
    },
    "Result": {
        "SpecList": [
            {
                "SpecType": "CU",
                "SpecName": "通用型-4核8G",
                "TradeCode": "cu.general.4c8g",
                "Cpu": 0,
                "Memory": 0,
                "DisplayName": ""
            }
        ],
        "NodeSupportSpecList": [
            {
                "NodeType": "QUERY_NODE",
                "SpecName": [
                    ""
                ],
                "MaxNodeNum": 0
            }
        ],
        "ZoneSupportSpecList": [
            {
                "ZoneId": "cn-beijing-a",
                "SpecName": [
                    ""
                ]
            }
        ],
        "NodeCuTypeSupportSpecList": [
            {
                "SpecName": [
                    ""
                ],
                "NodeCUType": "QUERY_NODE",
                "MaxNodeNum": 0
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists error codes related to this API and business logic. For more information, see [Public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|200 |InternalServerError |InternalServerError |Internal server exception. |
