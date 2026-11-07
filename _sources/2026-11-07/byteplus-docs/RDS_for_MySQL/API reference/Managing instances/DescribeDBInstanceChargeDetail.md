---
title: "DescribeDBInstanceChargeDetail"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/DescribeDBInstanceChargeDetail"
---

Call the DescribeDBInstanceChargeDetail API to query the billing information of the instance.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-f83edc2e\*\*\*\* |Instance ID. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|ChargeDetail |Object |Please refer to the return example. |Billing information for the instance. |
|ChargeType |String |PostPaid |Payment type. Values:<br><br><br>* `PostPaid`: Pay\-as\-you\-go (post\-payment).<br><br>* `PrePaid`: Annual and monthly subscription (pre\-payment). |
|AutoRenew |Boolean |true |Whether to automatically renew in the prepaid scenario.<br><br><br>* `true`: Automatically renew upon expiration.<br><br>* `false`: Do not automatically renew upon expiration. |
|PeriodUnit |String |Month |The purchase cycle in the prepaid scenario.<br><br><br>* `Month`: The purchase cycle is monthly.<br><br>* `Year`: The purchase cycle is yearly.<br><br><br>tip<br><br>When this parameter is used as a request parameter, the default value is `Month`. |
|Period |Integer |1 |The purchase duration in the prepaid scenario.<br><br>tip<br><br><br>* When this parameter is used as a request parameter, the default value is `1`.<br><br>* When the value of PeriodUnit is `Year`, the value range of Period is 1~3.<br><br>* When the value of PeriodUnit is `Month`, the value range of Period is 1~9. |
|ChargeStatus |String |Normal |Billing status of the instance. Values:<br><br><br>* `Normal`: Normal.<br><br>* `Overdue`: Arrears.<br><br>* `Unpaid`: Waiting for payment. |
|ChargeStartTime |String |2025\-07\-22T13:10:15.000Z |The billing start time of the instance (UTC time). The format is `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|ChargeEndTime |String |2025\-08\-22T15:59:59.000Z |The billing end time (UTC time) of the yearly and monthly subscribed instances. The format is `yyyy-MM-ddTHH:mm:ss.sssZ`.<br><br>tip<br><br>If the queried instance is a pay\-as\-you\-go instance, this field will be returned as empty. |
|OverdueTime |String |2025\-08\-23T04:00:00.000Z |The time (UTC time) when the instance is shut down due to arrears (pay\-as\-you\-go) or expiration (yearly/monthly subscription). The format is `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|OverdueReclaimTime |String |2025\-08\-29T15:59:59.000Z |The expected release time (UTC time) after the instance is shut down due to arrears (pay\-as\-you\-go) or expiration (yearly or monthly subscription). The format is `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|TempModifyStartTime |String |2022\-01\-01T10:10:10.000Z |The start time of the temporary upgrade (UTC time). The format is `yyyy-MM-ddTHH:mm:ss.sssZ`.<br><br>tip<br><br>For instances that are not in the temporary upgrade period, this field will not be returned. |
|TempModifyEndTime |String |2022\-01\-01T10:10:09.000Z |The restoration time (UTC time) of the temporary upgrade. The format is `yyyy-MM-ddTHH:mm:ss.sssZ`.<br><br>tip<br><br>For instances not in the temporary upgrade period, this field is not returned. |

## Sample request

```json
POST /?Action=DescribeDBInstanceChargeDetail&Version=2022-01-01
Host: open.ap-southeast-1.byteplusapi.com
Content-Type: application/json
X-Date: 20180614T114308Z
Authorization: HMAC-SHA256 Credential=AKIAIAGMBG4SXSQQ****/20180614/ap-southeast-1/rds_mysql/request, SignedHeaders=accept;content-type;host;x-date, Signature=6a593bf5f59e7c1109fb205c739d1cff4c672fe2d251963f4d48c8701d16****
{
    "InstanceId": "mysql-f83edc2e****"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2025072414470358C0C64BFA4C2A01A242-870b4a",
        "Action": "DescribeDBInstanceChargeDetail",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "ChargeDetail": {
            "AutoRenew": true,
            "ChargeEndTime": "2025-08-22T15:59:59.000Z",
            "ChargeStartTime": "2025-07-22T13:10:15.000Z",
            "ChargeStatus": "Normal",
            "ChargeType": "PrePaid",
            "OverdueReclaimTime": "2025-08-29T15:59:59.000Z",
            "OverdueTime": "2025-08-23T04:00:00.000Z",
            "Period": 1,
            "PeriodUnit": "Month"
        }
    }
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
