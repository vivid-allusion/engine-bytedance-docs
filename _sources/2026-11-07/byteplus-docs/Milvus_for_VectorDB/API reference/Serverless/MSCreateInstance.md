---
title: "MSCreateInstance"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/MSCreateInstance"
---

Call MSCreateInstance to create a Serverless instance.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=MSCreateInstance&groupName=Serverless&serviceCode=milvus&version=2023-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters of this API and some common parameters are listed below. For more information, see [Public parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|5OTdTz">必选</span> `Example: MSCreateInstance`

Action to execute, value: MSCreateInstance.



**Version**<span data-label="purple"> string</span><span data-api-tag="require|duQDLW">必选</span> ` Example value: 2023-01-01`

API version, value: 2023\-01\-01.



**Name ** <span data-label="purple">string </span>`optional` `example value: milvus-serverless-instance`

Instance name.



**InstanceName ** <span data-label="purple">string </span><span data-api-tag="require|raXBhA">必选</span> `Example: milvus-serverless-instance`

Instance name.



**Remark ** <span data-label="purple">string </span>`optional` `Example: milvus serverless instance remark`

Instance remarks.



**InstanceVersion**<span data-label="purple"> string </span><span data-api-tag="require|y6ONd7">必选</span>` Example value: V2_5`

Instance version



**RegionId ** <span data-label="purple">string </span>`Optional` `Example: cn-beijing`

Instance region.



**ProjectName ** <span data-label="purple">String </span>`Optional` `Example: default`

Project



**MilvusVersion ** <span data-label="purple">string </span>`optional` `Example: V2_5`

Instance version



**NetworkConfig ** <span data-label="purple">object </span><span data-api-tag="require|icbrcJ">必选</span> `Example value: -`

Network configuration.


**VpcInfo ** <span data-label="purple">object </span><span data-api-tag="require|CPoMid">必选</span> `Example value: -`

VPC information.


**VpcId ** <span data-label="purple">string </span><span data-api-tag="require|Ogvz8c">必选</span> `Example: -`

VPC ID.



**VpcName ** <span data-label="purple">string </span><span data-api-tag="require|1arTEC">必选</span> `Example value: -`

VPC name.




**SubnetInfo ** <span data-label="purple">object </span><span data-api-tag="require|JBNeR8">必选</span> `Example: -`

Subnet information.


**SubnetId ** <span data-label="purple">string </span><span data-api-tag="require|RTJnwI">必选</span> `Example value: -`

Subnet ID.



**SubnetName ** <span data-label="purple">string </span><span data-api-tag="require|VB9mmM">必选</span> `example value: -`

Subnet name.




**InnerEndpointEnabled ** <span data-label="purple">boolean </span>`optional` `Example: -`

Whether to enable the internal network address.



**HttpsEnabled ** <span data-label="purple">boolean </span>`optional` `Example value: -`

Whether to turn on HTTPS.



**IpVersion ** <span data-label="purple">string </span>`optional` `Example value: -`

IP address version.




**Tags ** <span data-label="purple">object[] </span>`optional` `example value: -`

Instance tag.


**Key ** <span data-label="purple">string </span>`optional` `Example value: -`

Tag key.



**Value ** <span data-label="purple">string </span>`optional` `example: -`

Tag value.



**SystemTag ** <span data-label="purple">boolean </span>`optional` `example value: -`

Indicates if it is a system tag.




**DeleteProtectEnabled ** <span data-label="purple">boolean </span>`optional` `Example: false`

Turn on deletion protection or not.



**DeleteProtect ** <span data-label="purple">boolean </span>`Optional` `Example: false`

Turn on deletion protection or not.



**Password ** <span data-label="purple">string </span><span data-api-tag="require|zOj7Jy">必选</span> `Example: Milvus@12345`

Instance password.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters unique to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**OrderID ** <span data-label="purple">string </span>`Example: -`

Order ID.



**OrderNO ** <span data-label="purple">string </span>`Example value: -`

Order number.



**InstanceId ** <span data-label="purple">string </span>`Example value: -`

Instance ID.



**TradeEnabled ** <span data-label="purple">boolean </span>`Example: -`

Enable billing.



**TradeConfigId ** <span data-label="purple">string </span>`Example: -`

Billing configuration ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
POST /?Action=MSCreateInstance&Version=2023-01-01 HTTP/1.1
Host: /
Content-Type: application/json; charset=UTF-8
X-Date: 20260316T070027Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260316/cn-beijing/milvus/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "InstanceName": "milvus-serverless-instance",
  "InstanceVersion": "V2_5",
  "NetworkConfig": {
    "VpcInfo": {
      "VpcId": "OFrNZ9",
      "VpcName": "HpPO"
    },
    "SubnetInfo": {
      "SubnetId": "sJjdN",
      "SubnetName": "dcKVZ"
    }
  },
  "Password": "Milvus@12345"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "20260316150030190125217115B46BDA",
    "Action": "MSCreateInstance",
    "Version": "2023-01-01",
    "Service": "milvus",
    "Region": "cn-beijing"
  },
  "Result": {
    "OrderID": "H",
    "OrderNO": "yYf5vhK",
    "InstanceId": "dyGub0uzjBj",
    "TradeEnabled": false,
    "TradeConfigId": "W"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists error codes related to this API and business logic. For more information, see [Public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|200 |CreateOrderFailed |CreateOrderFailed |Failed to create order. |
