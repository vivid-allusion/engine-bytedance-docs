---
title: "CreateResourcePackage"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/CreateResourcePackage"
---

Call the CreateResourcePackage API to create a resource plan.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Storage plans are available by subscription only.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateResourcePackage&serviceCode=rds_mysql&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Is it required? |Example |Description |
|---|---|---|---|---|
|PackageType |String |Yes |StoragePackage |The deduction item of the resource plan. Currently, only `StoragePackage` is supported, which is a storage plan. |
|PackageSpec |String |Yes |100 |Resource plan specifications. If PackageType is `StoragePackage`, the value range for PackageSpec is:<br><br><br>* `100`: 100 GiB.<br><br>* `200`: 200 GiB.<br><br>* `300`: 300 GiB.<br><br>* `500`: 500 GiB.<br><br>* `1000`: 1000 GiB.<br><br>* `2000`: 2000 GiB.<br><br>* `5000`: 5000 GiB.<br><br>* `10000`: 10000 GiB. |
|EffectiveTimeType |String |Yes |Specified |Effective time type. Values:<br><br><br>* `Immediate`: Takes effect immediately.<br><br>* `Specified`: Takes effect at the specific time. |
|EffectiveTime |String |No |2025\-08\-30T09:00:00Z |This parameter is required when the effective time of the resource plan is `Specific time`, that is, when EffectiveTimeType is set to `Specified`. The time format is `yyyy-MM-ddTHH:mm:ssZ` (UTC time).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the specified effective time is earlier than the current time, the current time is rounded up to the next hour to be the effective time for the resource plan.</div><br> |
|ChargeInfo |Object of [ChargeInfoObject](https://docs.byteplus.com/en/docs/40/66090#chargeinfoobject) |Yes |See the request example. |Purchase duration for the resource plan. |


<span id="chargeinfoobject"></span>
### ChargeInfoObject


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|PeriodUnit |String |Yes |Month |Purchase period for prepaid scenarios. Range:<br><br><br>* `Month`: the purchase cycle is by month.<br><br>* `Year`: the purchase cycle is by year. |
|Period |Integer |Yes |1 |Subscription duration in a prepaid scenario. The value range of this parameter depends on the value of PeriodUnit:<br><br><br>* When PeriodUnit is `Month`, Period ranges from 1 to 11.<br><br>* When PeriodUnit is `Year`, Period ranges from 1 to 5. |
|Number |Integer |No |1 |The purchase quantity of the resource plan. Value range: 1~50. Default value: 1. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|OrderId |String |Order2002000011757122272 |The configuration order number. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=CreateResourcePackage&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "PackageType": "StoragePackage",
    "PackageSpec": "100",
    "EffectiveTimeType": "Specified",
    "EffectiveTime": "2025-09-30T09:00:00Z",
    "ChargeInfo": {
        "Number": 1,
        "Period": 1,
        "PeriodUnit": "Month"
    }
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2025092223045219098175CFF5A8A0299E-ddbddb",
        "Action": "CreateResourcePackage",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {
        "OrderId": "Order2002000011757122272"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
