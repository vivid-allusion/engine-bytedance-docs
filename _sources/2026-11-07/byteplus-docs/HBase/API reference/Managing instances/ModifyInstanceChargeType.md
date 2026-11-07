---
title: "ModifyInstanceChargeType"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/ModifyInstanceChargeType"
---

Call the ModifyInstanceChargeType interface to convert the instance billing type from pay\-as\-you\-go to yearly or monthly subscription.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |hb\-cn01762cf4d6\*\*\*\* |Instance ID. |
|ChargeType |String |Yes |PostPaid |Billing type. The valid values are:<br><br><br>* `PostPaid`: Pay\-as\-you\-go.<br><br>* `PrePaid`: Yearly or monthly subscription. |
|PurchaseMonths |Integer |No |1 |Purchase duration. The unit is month. Valid values: `1` (default), `2`, `3`, `4`, `5`, `6`, `7`, `8`, `9`, `12`, `24`, and `36`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is valid only when <code>ChargeType</code> is set to <code>PrePaid</code>.</div><br> |
|AutoRenew |Boolean |No |false |Specifies whether to enable auto\-renewal. Valid values are:<br><br><br>* `false`: Disables auto\-renewal(Default).<br><br>* `true`: Enables auto\-renewal.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is valid only when <code>ChargeType</code> is set to <code>PrePaid</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When you select <code>true</code> to enable auto\-renewal, the default renewal duration is one month.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|Name |Type |Example value |Description |
|---|---|---|---|
|OrderNo |String |Order730602621667020\*\*\*\* |Order ID. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```json
POST /?Action=ModifyInstanceChargeType&Version=2018-01-01 HTTP/1.1
Host: hbase.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/hbase/request,SignedHeaders=content-type;host;x-date,  Signature=****
{
    "InstanceId": "hb-cncqf0aa02a0****",
    "ChargeType": "Prepaid",
    "PurchaseMonths": 1,
    "AutoRenew": false
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20231127143346F031F701FDB9A48F1F44",
        "Action": "ModifyInstanceChargeType",
        "Version": "2018-01-01",
        "Service": "hbase",
        "Region": "cn-beijing"
    },
    "Result": {
        "OrderNo": "Order730602621667020****"
    }
}
```
