---
title: "DescribePriceV2 - Query Instance Price V2"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/DescribePriceV2_-_Query_Instance_Price_V2"
---

Call DescribePriceV2 to query the instance price.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribePriceV2&groupName=%E5%AE%9E%E4%BE%8B%E7%AE%A1%E7%90%86&serviceCode=milvus&version=2023-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters of this API and some common parameters are listed below. For more information, see [Public parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|3tQ4tN">必选</span> `Example value: DescribePriceV2`

Operation to execute, value: DescribePriceV2.



**Version**<span data-label="purple"> string</span><span data-api-tag="require|iB0KOc">必选</span>` Example: 2023-01-01`

API version, value: 2023\-01\-01.



**ChargeConfig ** <span data-label="purple">object </span><span data-api-tag="require|FLkUPI">必选</span> `Example value: -`

Billing information.


**ChargeType**<span data-label="purple"> string</span><span data-api-tag="require|suJyui">必选</span>`  Example value: PRE`

Payment type.

\-POST: pay\-as\-you\-go.

PRE: Subscription.



**Period ** <span data-label="purple">integer </span>`optional` `Example value: 1`

Purchase duration.



**AutoRenew ** <span data-label="purple">boolean </span>`optional` `Example value: true`

Automatic renewal status.




**ComponentSpecList**<span data-label="purple"> object[] </span><span data-api-tag="require|tZKCw6">必选</span> `example value: -`

Specification list.


**NodeType ** <span data-label="purple">string </span><span data-api-tag="require|w8JKIP">必选</span>`Example value: PROXY_NODE: proxy node.`

Node type.

META_NODE: Mix Coordinator.

PROXY_NODE: proxy node.

INDEX_NODE: Index node.

DATA_NODE: Data node.

QUERY_NODE: Query node.

STREAMING_NODE: Streaming node.



**ResourceSpecName**<span data-label="purple"> string </span><span data-api-tag="require|AflmPm">必选</span>` example value: -`

Resource specification name (obtained from the specification list).



**NodeNum**<span data-label="purple"> integer </span><span data-api-tag="require|D52mD3">必选</span> `Example value: -`

Number of nodes.




**InstanceId ** <span data-label="purple">string </span>`optional` `Example value: -`

Instance ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters unique to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**OriginalAmount ** <span data-label="purple">string </span>`Example value: -`

Original amount.



**DiscountAmount ** <span data-label="purple">string </span>`Example value: -`

Discount amount.



**PayableAmount ** <span data-label="purple">string </span>`Example value: -`

Amount due.



**Currency ** <span data-label="purple">string </span>`example: USD`

Currency.



**NodePriceList ** <span data-label="purple">object[] </span>`Example value: -`

Price details for each node type.


**ChargeItemCode ** <span data-label="purple">string </span>`Example value: -`

Billable item.



**OriginalAmount ** <span data-label="purple">string </span>`example: -`

Original amount.



**PayableAmount ** <span data-label="purple">string </span>`Example value: -`

Amount due.



**NodeNum ** <span data-label="purple">integer </span>`Example value: -`

Number of nodes.



**Node type ** <span data-label="purple">string </span>`Example value: -`

Node type.



**ChargeItemNum ** <span data-label="purple">integer </span>`example: -`

Quantity corresponding to the billable item.



**DiscountAmount ** <span data-label="purple">string </span>`Example value: -`

Discount amount.



**NodeCUType ** <span data-label="purple">string </span>`Example value: -`

Resource type.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
POST /?Action=DescribePriceV2&Version=2023-01-01 HTTP/1.1
Host: /
Content-Type: application/json; charset=UTF-8
X-Date: 20260126T065514Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260126/cn-beijing/milvus_dev/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "ChargeConfig": {
    "ChargeType": "PRE"
  },
  "ComponentSpecList": [
    {
      "NodeType": "Excepteur anim non irure",
      "ResourceSpecName": "规格代号"
    }
  ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "20260126145517082003254123108686",
    "Action": "DescribePriceV2",
    "Version": "2023-01-01",
    "Service": "milvus_dev",
    "Region": "cn-beijing"
  },
  "Result": {
    "OriginalAmount": "99822",
    "DiscountAmount": "dzJThtB",
    "PayableAmount": "O9gP24",
    "Currency": "eu do adipisicing",
    "NodePriceList": [
      {
        "ChargeItemCode": "non sit eiusmod fugiat est",
        "OriginalAmount": "7u8Sx26",
        "DiscountAmount": "76pSpcFmw",
        "PayableAmount": "Yh",
        "ChargeItemNum": 70261165.91912973,
        "NodeType": "labore commodo aute in quis",
        "NodeNum": 87213450.0837586,
        "NodeCUType": "minim quis commodo aliqua"
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
|200 |ComponentSpecNotSupported |Component spec not supported |Not supported to input specifications. |
|200 |InternalServerError |InternalServerError |Internal service exception. |
|200 |ComponentSpecMissing |Component spec missing |Specification missing. |
