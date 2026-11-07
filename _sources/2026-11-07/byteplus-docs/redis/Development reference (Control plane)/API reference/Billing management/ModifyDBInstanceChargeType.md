---
title: "ModifyDBInstanceChargeType"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/modifydbinstancechargetype"
---

Call the ModifyDBInstanceChargeType API to modify the billing method of the target instance.

## Request type

Asynchronous request.

## Precautions

* The instance is in the **Running** status.

* Pay\-as\-you\-go instances incur fees by the second, with an hourly billing cycle. The system settles fees hourly (based on UTC+8 time). Ensure that you have an adequate account balance to avoid instance shutdown due to arrears. For more information, refer to [Switching to pay-as-you-go](https://docs.byteplus.com/en/docs/redis/switch-to-pay-as-you-go).

* When switching to pay\-as\-you\-go for an instance, the system will first calculate the residual value of the instance according to the refund rules of non\-seven day unconditional unsubscription (the remaining amount will be refunded based on the payment method used). After switching, the instance will immediately be billed according to pay\-as\-you\-go. For more details on the non\-seven day no\-reason refund rules, refer to [Non-seven Day No-reason Refund Rules](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management#2a09ed89).

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyDBInstanceChargeType&serviceCode=Redis&version=2020-12-07&groupName=计费管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceIds |Array of String |Yes |["redis\-cn02he8bhzsji\*\*\*\*","redis\-cn02j292it8lc\*\*\*\*"] |Instance ID.<br><br>> **tip**<br><br><br><br>* > Supports batch converting multiple instance IDs to subscription.<br><br><br>* > You can pass up to 100 instances at a time. Instance IDs must be unique.<br><br><br>* > Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query basic information about all Redis instances in the target region, including their instance IDs.<br> |
|ChargeType |String |Yes |PrePaid |The modified instance billing type. Valid values are as follows:<br><br><br>* `PrePaid`: Subscription (also known as prepaid).<br><br>* `PostPaid`: Pay\-as\-you\-go (also known as postpaid). For more information about billing methods, see [Billing method](https://docs.byteplus.com/en/docs/redis/billing-method). |
|PurchaseMonths |Integer |No |1 |Purchase duration. The unit is month. Valid values:<br><br><br>* Monthly purchase: `1`, `2`, `3`, `4`, `5`, `6`, `7`, `8`, `9`.<br><br>* Annual purchase: `12`, `24`, `36`.<br><br><br>> **tip**<br><br><br><br>* > If this parameter is left blank, the default purchase duration is 1 month.<br><br><br>* > This parameter is valid only when `ChargeType` is set to `PrePaid`.<br> |
|AutoRenew |Boolean |No |false |Whether to enable automatic renewal, the value range is as follows:<br><br><br>* `false` (default value): do not enable automatic renewal.<br><br>* `true`: Enable automatic renewal.<br><br><br>> **tip**<br><br><br><br>* > This parameter is valid only when `ChargeType` is set to `PrePaid`.<br><br><br>* > After selecting `true` to enable automatic renewal, the system defaults to a renewal period of 1 month.<br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |To ensure the idempotence of requests and prevent duplicate submission of requests. The client generates the parameter values to ensure the uniqueness among different requests. Values are case\-sensitive, no more than 127 ASCII characters. |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|OrderNO |String |Order702856788643751\*\*\*\* |Order ID. |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=ModifyDBInstanceChargeType&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
        "InstanceIds": ["redis-cn02he8bhzsji****", "redis-cn02j292it8lc****"],
        "ChargeType": "PrePaid",
        "PurchaseMonths": 1,
        "AutoRenew": false
}
```

## Response example

```JSON
{
     "ResponseMetadata": {
          "RequestId": "2022061517350601022524311806521111",
          "Action": "ModifyDBInstanceChargeType",
          "Version": "2020-12-07",
          "Service": "Redis",
          "Region": "cn-beijing"
     },
     "Result": {
          "OrderNO": "Order702856788643751****"
     }
}
```

## Error code

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/redis/error-code).
