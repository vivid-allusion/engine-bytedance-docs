---
title: "CreateInstanceOneStep - Create instance"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/CreateInstanceOneStep"
---

Call CreateInstanceOneStep to create an instance in one step.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=CreateInstanceOneStep&groupName=%E5%AE%9E%E4%BE%8B%E7%AE%A1%E7%90%86&serviceCode=milvus&version=2023-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters of this API and some common parameters are listed below. For more information, see [Public parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action**<span data-label="purple"> string</span><span data-api-tag="require|IC5QQh">必选</span> ` Example value: CreateInstanceOneStep`

The action to execute, value: CreateInstanceOneStep.



**Version ** <span data-label="purple">string</span><span data-api-tag="require|mXZGb3">必选</span>` Example: 2023-01-01`

API version, value: 2023\-01\-01.



**InstanceConfiguration**<span data-label="purple"> object </span><span data-api-tag="require|7AMrzR">必选</span>` Example value: {}`

Instance basic configuration.


**InstanceName ** <span data-label="purple">string</span><span data-api-tag="require|z8uOsb">必选</span>  `Example value: milvus-instance-01`

Instance name.



**InstanceVersion ** <span data-label="purple">string</span><span data-api-tag="require|KGBmNb">必选</span> ` Example value: V2_5`

Milvus version.


* V2_5: corresponds to Milvus 2.5.x version.

* V2_6: corresponds to Milvus 2.6.x version



**HaEnabled ** <span data-label="purple">boolean </span>`optional` `example value: true`

Whether to enable high availability (Deprecated).



**ComponentSpecList ** <span data-label="purple">object[] </span><span data-api-tag="require|N3YXm6">必选</span>` example value: -`

Component specification list.


**NodeNum**<span data-label="purple"> integer </span><span data-api-tag="require|bdjE6i">必选</span>` Example value: -`

Number of nodes.



**CpuNum ** <span data-label="purple">integer </span>`optional` `Example value: -`

CPU core count (Deprecated).



**MemSize ** <span data-label="purple">integer </span>`optional` `Example value: -`

Memory size (Deprecated).



**NodeType ** <span data-label="purple">string</span><span data-api-tag="require|hEqBwg">必选</span> ` example: -`

Node type.



**NodeCUType ** <span data-label="purple">string </span>`optional` `example value: -`

node CU type (deprecated).


* CAPACITY: capacity.

* PERFORMANCE: performance.



**ResourceSpecName**<span data-label="purple"> string </span><span data-api-tag="require|bXYLfb">必选</span> `example value: -`

Specification name (obtained from the supported specification types of the node in the specification list interface).




**AdminPassword ** <span data-label="purple">string</span><span data-api-tag="require|XZZXzO">必选</span>  `Example value: SecurePassword123!`

Administrator password.




**NetworkConfig**<span data-label="purple"> object</span><span data-api-tag="require|6iPOFT">必选</span>`  example value: {}`

Network configuration.


**VpcInfo**<span data-label="purple"> object</span><span data-api-tag="require|N7Q9rg">必选</span>  `Example value: -`

Private network information.


**VpcId ** <span data-label="purple">string </span><span data-api-tag="require|FVP4UU">必选</span> `example: vpc-12345678`

Private network ID.



**VpcName ** <span data-label="purple">string </span>`optional` `example: milvus-vpc`

Private network name.




**SubnetInfo ** <span data-label="purple">object</span><span data-api-tag="require|oJDVWX">必选</span> ` Example value: -`

Subnet information.


**SubnetId ** <span data-label="purple">string</span><span data-api-tag="require|cofCH1">必选</span> ` example: subnet-12345678`

Subnet ID.



**Subnet name** <span data-label="purple">string</span> `optional` `example: milvus-subnet`

Subnet name.





**ChargeConfig**<span data-label="purple"> object</span><span data-api-tag="require|ckxCct">必选</span>`  Example value: {}`

Billing configuration.


**ChargeType**<span data-label="purple"> string</span><span data-api-tag="require|tdgbiw">必选</span> ` Example value: PRE`

Billing type.

PostPaid: Pay\-as\-you\-go.

PrePaid: Subscription.



**Period ** <span data-label="purple">integer </span>`optional` `Example value: 12`

Subscription duration. Unit: month.

Required for subscription.



**AutoRenew ** <span data-label="purple">boolean </span>`optional` `Example value: true`

Whether to enable automatic renewal.

Subscription is required for yearly or monthly plans.



**ExpireDate ** <span data-label="purple">string </span>`optional` `example: 2025-12-31 12:00:00`

Expiration time (Deprecated).




**Region ** <span data-label="purple">string </span>`optional` `example value: ap-beijing`

region (Deprecated).



**Zones**<span data-label="purple"> string[]</span><span data-api-tag="require|O767wi">必选</span> ` Example: []`

Availability zone.



**Tags ** <span data-label="purple">object[] </span>`optional` `example value: []`

Tag.


**Key ** <span data-label="purple">string</span><span data-api-tag="require|nkGrZc">必选</span> ` Example value: environment`

Tag key.



**Value**<span data-label="purple"> string </span><span data-api-tag="require|jMj3Vv">必选</span>` example value: production`

Tag value.




**ProjectName ** <span data-label="purple">string </span>`optional` `Example value: ai-platform`

Project name.

Default is default.



**DeleteProtectEnabled ** <span data-label="purple">boolean </span>`optional` `Example value: true`

Deletion protection enabled.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters unique to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**OrderID ** <span data-label="purple">string </span>`Example value: B00`

Order ID.



**OrderNO ** <span data-label="purple">string </span>`Example value: B00`

Order number.



**InstanceId ** <span data-label="purple">string </span>`Example: milvus-xxx`

Instance ID.



**TradeEnabled ** <span data-label="purple">boolean </span>`Example: true`

Whether to enable trading; currently only true is supported.



**TradeConfigId ** <span data-label="purple">string </span>`Example: B00`

Transaction configuration ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
POST /?Action=CreateInstanceOneStep&Version=2023-01-01 HTTP/1.1
Host: milvus.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=UTF-8
X-Date: 20251027T125731Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251027/cn-beijing/milvus/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "InstanceConfiguration": {
    "InstanceName": "milvus-instance-01",
    "InstanceVersion": "V2_5",
    "HaEnabled": true,
    "ComponentSpecList": [
      {
        "NodeType": "D3",
        "CpuNum": 1.3280476287606415,
        "MemSize": 828.0444265105901,
        "NodeNum": 575.031725645527,
        "NodeCUType": "XKLcmV2Bz",
        "ResourceSpecName": "yfR"
      }
    ],
    "AdminPassword": "SecurePassword123!"
  },
  "NetworkConfig": {
    "VpcInfo": {
      "VpcId": "vpc-12345678",
      "VpcName": "milvus-vpc"
    },
    "SubnetInfo": {
      "SubnetId": "subnet-12345678",
      "SubnetName": "milvus-subnet"
    },
    "InnerEndpointEnabled": true
  },
  "ChargeConfig": {
    "ChargeType": "PRE",
    "Period": 12,
    "AutoRenew": true,
    "ExpireDate": "2025-12-31 12:00:00"
  },
  "Region": "ap-beijing",
  "Zones": [
    "skReWqLyG"
  ],
  "Tags": [
    {
      "Key": "environment",
      "Value": "production"
    }
  ],
  "ProjectName": "default",
  "DeleteProtectEnabled": true
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "20251027205734191076210077AEC70D",
    "Action": "CreateInstanceOneStep",
    "Version": "2023-01-01",
    "Service": "milvus",
    "Region": "cn-beijing"
  },
  "Result": {
    "OrderID": "uGk",
    "OrderNO": "JVUMP6Hh",
    "InstanceId": "t7O",
    "TradeEnabled": false,
    "TradeConfigId": "JUfJgXG"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists error codes related to this API and business logic. For more information, see [Public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|200 |BadRequestParameterEmpty |Parameter can not be empty. |Parameter cannot be empty. |
|200 |ComponentSpecMissing |Component spec missing |Specification missing. |
|200 |NodeNumTooSmall |Node number too small |Insufficient number of nodes. |
|200 |NodeCpuNotValid |Node cpu not valid |CPU specifications are incorrect. |
|200 |NodeMemNotValid |Node mem not valid |Memory specification is incorrect. |
|200 |ComponentSpecNotSupported |Component spec not supported |Not supported to input specifications. |
|200 |NodeNumTooBig |Node number too big |Number of nodes too large. |
|200 |CreateOrderFailed |CreateOrderFailed |Failed to create order. |
|200 |InternalServerError |InternalServerError |Internal server exception. |
