---
title: "MSCreateInstanceOneStep"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/MSCreateInstanceOneStep"
---

Call MSCreateInstanceOneStep to create a Serverless instance in one step.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=MSCreateInstanceOneStep&groupName=Serverless-%E5%85%AC%E5%BC%80&serviceCode=milvus&version=2023-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters of this API and some common parameters are listed below. For more information, see [Public parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|pAenTt">必选</span> `Example value: MSCreateInstanceOneStep`

Action to execute, value: MSCreateInstanceOneStep.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|hv0YiM">必选</span>` Example value: 2023-01-01`

API version, value: 2023\-01\-01.



**InstanceName ** <span data-label="purple">string </span><span data-api-tag="require|tZANeC">必选</span> `example value: milvus-serverless-instance`

Instance name.



**InstanceVersion**<span data-label="purple"> string</span><span data-api-tag="require|gZgLJA">必选</span> ` Example value: V2_5`

Instance version



**NetworkConfig ** <span data-label="purple">object </span><span data-api-tag="require|TSz17b">必选</span> `Example value: -`

Network configuration.


**VpcInfo ** <span data-label="purple">object </span><span data-api-tag="require|XJfC1S">必选</span> `Example value: -`

VPC information.


**VpcId ** <span data-label="purple">string </span><span data-api-tag="require|LRtxiL">必选</span> `Example value: -`

VPC ID.



**VpcName ** <span data-label="purple">string </span><span data-api-tag="require|tZPLE0">必选</span> `Example value: -`

VPC name.




**SubnetInfo ** <span data-label="purple">object </span><span data-api-tag="require|Dh8hno">必选</span> `Example value: -`

Subnet information.


**SubnetId ** <span data-label="purple">string </span><span data-api-tag="require|sPQzyI">必选</span> `example value: -`

Subnet ID.



**Subnet name ** <span data-label="purple">string </span><span data-api-tag="require|UE1M7B">必选</span> `Example value: -`

Subnet name.




**InnerEndpointEnabled ** <span data-label="purple">boolean </span>`optional` `Example value: -`

Whether to turn on the internal network address.



**HttpsEnabled ** <span data-label="purple">boolean </span>`optional`

Whether to turn on HTTPS.



**IpVersion ** <span data-label="purple">string </span>`Optional`

IP address version.




**Password ** <span data-label="purple">string </span><span data-api-tag="require|tQ53JP">必选</span> `Example value: Milvus@12345`

Instance password.



**ProjectName ** <span data-label="purple">String </span>`Optional` `Example: default`

Project



**Tags ** <span data-label="purple">object[] </span>`optional` `Example value: -`

Instance tag.


**Key ** <span data-label="purple">string </span>`optional`

Tag key.



**Value ** <span data-label="purple">string </span>`optional`

Tag value.



**SystemTag ** <span data-label="purple">boolean </span>`optional`

Whether it is a system tag.




**DeleteProtectEnabled ** <span data-label="purple">boolean </span>`optional` `example value: false`

Turn on deletion protection or not.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters unique to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**OrderID ** <span data-label="purple">string </span>`Example value: -`

Order ID.



**OrderNO ** <span data-label="purple">string </span>`Example value: -`

Order number.



**InstanceId ** <span data-label="purple">string </span>`Example value: -`

Instance ID.



**TradeEnabled ** <span data-label="purple">boolean </span>`Example value: -`

Enable billing.



**TradeConfigId ** <span data-label="purple">string </span>`Example value: -`

Billing configuration ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
POST /?Action=MSCreateInstanceOneStep&Version=2023-01-01 HTTP/1.1
Host: /
Content-Type: application/json; charset=UTF-8
X-Date: 20260316T070104Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260316/cn-beijing/milvus/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "InstanceName": "milvus-serverless-instance",
  "InstanceVersion": "V2_5",
  "NetworkConfig": {
    "VpcInfo": {
      "VpcId": "i6EJ",
      "VpcName": "s3aJ"
    },
    "SubnetInfo": {
      "SubnetId": "HncnDShq",
      "SubnetName": "nRM3Zbk"
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
    "RequestId": "202603161501071271410960488DA724",
    "Action": "MSCreateInstanceOneStep",
    "Version": "2023-01-01",
    "Service": "milvus",
    "Region": "cn-beijing"
  },
  "Result": {
    "OrderID": "OMAoxtDnaFr",
    "OrderNO": "ACcR6Ri",
    "InstanceId": "S",
    "TradeEnabled": false,
    "TradeConfigId": "Nt8sKdjAfA"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists error codes related to this API and business logic. For more information, see [Public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|200 |CreateOrderFailed |CreateOrderFailed |Failed to create order. |
