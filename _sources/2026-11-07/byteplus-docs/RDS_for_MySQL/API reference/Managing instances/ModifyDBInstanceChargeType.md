---
title: "ModifyDBInstanceChargeType"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbinstancechargetype"
---

Call the ModifyDBInstanceChargeType API to modify the billing method of an instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyDBInstanceChargeType&serviceCode=rds_mysql&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-538e563b\*\*\*\*,mysql\-2122c54c\*\*\*\* |Instance ID. You can enter up to 20 instance IDs. Separate the IDs with a comma (,). |
|ChargeType |String |Yes |PrePaid |Billing method. Values are:<br><br><br>* `PrePaid`: subscription.<br><br>* `PostPaid`: pay\-as\-you\-go. |
|AutoRenew |Boolean |No |false |Is automatic renewal enabled for the prepaid scenario? Values:<br><br><br>* `yes`: automatic renewal.<br><br>* `false`: no automatic renewal.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Required when ChargeType is <code>PrePaid</code>.</div><br> |
|PeriodUnit |String |No |Month |Purchase period for prepaid scenarios.<br><br><br>* `Month`: The purchase cycle is by month. Default.<br><br>* `Year`: the purchase cycle is by year.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Required when ChargeType is <code>PrePaid</code>.</div><br> |
|Period |Integer |No |1 |Subscription duration in a prepaid scenario.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Required when ChargeType is <code>PrePaid</code>.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|InstanceId |String |mysql\-7e662621\*\*\*\* |Instance ID. |
|OrderNO |String |Order7098992421756812175 |Order ID. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=ModifyDBInstanceChargeType&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-538e563b****,mysql-2122c54c****",
    "ChargeType": "PrePaid",
    "AutoRenew": false,
    "PeriodUnit": "Month",
    "Period": 1
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202307041643413D011E46886A48732386",
        "Action": "ModifyDBInstanceChargeType",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstanceId": "mysql-538e563b****,mysql-2122c54c****",
        "OrderNO": "Order7343129081879630116"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
