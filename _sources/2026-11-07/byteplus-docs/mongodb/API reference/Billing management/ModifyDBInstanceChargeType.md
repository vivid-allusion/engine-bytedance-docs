---
title: "ModifyDBInstanceChargeType"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/modifydbinstancechargetype"
---

Call the ModifyDBInstanceChargeType API to modify the billing method of the target instance.

## Request type

Asynchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceIds |String[] |Yes |["mongo\-replica\-a1f25ba5\*\*\*\*"] |Instance ID.<br><br>tip<br><br><br>* You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) API to query the basic information about all the MongoDB instances in the target region, including the instance IDs.<br><br>* Multiple instance IDs can be input at the same time to switch multiple instances to Yearly or monthly subscription at once. The instance IDs are separated by commas (,).<br><br>* A maximum of 10 instances can be input at the same time, and each ID must be unique. |
|ChargeType |String |Yes |Prepaid |The modified billing method of the instance. The value range is as follows:<br><br><br>* `PostPaid`: Pay\-as\-you\-go (also known as post\-paid).<br><br>* `Prepaid`: Yearly or monthly subscription (also known as pre\-paid).<br><br><br>tip<br><br>For more information about the billing method, see [Billing methods](https://docs.byteplus.com/en/docs/mongodb/billing-method). |
|PeriodUnit |String |No |Year |Specify the yearly or monthly subscription instance as the yearly or monthly type. The values are as follows:<br><br><br>* `Year`: Yearly subscription.<br><br>* `Month`: Monthly subscription.<br><br><br>tip<br><br>When the value of `ChargeType` is `Prepaid`, this parameter is required. |
|Period |Integer |No |1 |The purchased term of the yearly or monthly subscription instance, where:<br><br><br>* When `PeriodUnit` is `Year`, the value of `Period` is from 1 to 3.<br><br>* When `PeriodUnit` is `Month`, the value of `Period` is from 1 to 9.<br><br><br>tip<br><br>When the value of `ChargeType` is `Prepaid`, this parameter is required. |
|AutoRenew |Boolean |No |false |Whether to enable auto\-renewal for the yearly/monthly subscription instance. The value range is as follows:<br><br><br>* `false` (default): Auto\-renewal is not enabled.<br><br>* `true`: Auto\-renewal is enabled.<br><br><br>tip<br><br>This parameter takes effect only when the value of `ChargeType` is `Prepaid`. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|InstanceIds |String[] |["mongo\-replica\-a1f25ba5\*\*\*\*"] |Instance ID. |
|OrderNO |String |Order707596823497132\*\*\*\* |Order ID. |

## Sample request

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=ModifyDBInstanceChargeType&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/ap-southeast-1/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceIds": [
        "mongo-replica-a1f25ba5****"
    ],
    "ChargeType": "Prepaid",
    "PeriodUnit": "Year",
    "Period": 1,
    "AutoRenew": false
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202202211539050101742350380678****",
        "Action": "ModifyDBInstanceChargeType",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "InstanceIds": [
            "mongo-replica-a1f25ba5****"
        ],
        "OrderNO": "Order707596823497132****"
    }
}
```

## Error codes

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/mongodb/error-code).
