---
title: "ModifyDBInstanceChargeType"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/modifydbinstancechargetype"
---

Call the ModifyDBInstanceChargeType API to modify the billing type of an instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-21a3333b\*\*\*\* |Instance ID. |
|ChargeType |String |Yes |PrePaid |Billing method. The value is `PrePaid` (subscription).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Only pay\-as\-you\-go instances can be converted to subscription instances.</div><br> |
|AutoRenew |Boolean |No |true |Is automatic renewal enabled for the prepaid scenario?<br><br><br>* `true`: automatic renewal.<br><br>* `false`: no automatic renewal (Default value). |
|PeriodUnit |String |No |Month |Purchase period for prepaid scenarios.<br><br><br>* `Month`: monthly (default).<br><br>* `Year`: subscription. |
|Period |Integer |No |1 |Subscription duration in a prepaid scenario. default value: 1. Range:<br><br><br>* When PeriodUnit is `Month`, Period ranges from 1 to 9.<br><br>* When PeriodUnit is `Year`, Period ranges from 1 to 3. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|InstanceId |String |postgres\-21a3333b\*\*\*\* |Instance ID. |
|OrderNO |String |Order709899242175681\*\*\*\* |Order ID. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=ModifyDBInstanceChargeType&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-ca7b7019****",
    "ChargeType": "PrePaid",
    "PeriodUnit": "Month",
    "AutoRenew": false
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230802104119518A5717C82679D86E18",
        "Action": "ModifyDBInstanceChargeType",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstanceId": "postgres-ca7b7019****",
        "OrderNO": "Order726254891288237****"
    }
}
```
