---
title: "ListResourcePackages"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/ListResourcePackages"
---

Call the ListResourcePackages API to query resource plans.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListResourcePackages&serviceCode=rds_mysql&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|EffectiveTime |Object of [TimeFilter](https://docs.byteplus.com/en/docs/40/66091#timefilter) |No |{<br><br>"EndTime":"2025\-08\-20T08:00:00.000Z",<br><br>"StartTime":"2025\-08\-20T08:00:00.000Z"<br><br>} |Query by the effective time period of the resource plan. |
|ExpirationTime |Object of [TimeFilter](https://docs.byteplus.com/en/docs/40/66091#timefilter) |No |{<br><br>"EndTime":"2029\-08\-20T08:00:00.000Z",<br><br>"StartTime":"2026\-08\-20T08:00:00.000Z"<br><br>} |Query by the due time period of the resource plan. |
|PackageStatus |String |No |NotEffective |The state of the resource plan. Values:<br><br><br>* `NotEffective`: not effective.<br><br>* `InUse`: in use.<br><br>* `Expire`: expired. |
|PackageType |String |No |StoragePackage |The deduction item of the resource plan. Currently, only `StoragePackage` is supported, which is a storage plan. |
|PackageSpec |String |No |100 |Resource plan specifications. If PackageType is StoragePackage, the value range for PackageSpec is:<br><br><br>* `100`: 100 GiB.<br><br>* `200`: 200 GiB.<br><br>* `300`: 300 GiB.<br><br>* `500`: 500 GiB.<br><br>* `1000`: 1000 GiB.<br><br>* `2000`: 2000 GiB.<br><br>* `5000`: 5000 GiB.<br><br>* `10000`: 10000 GiB. |
|PurchaseDuration |Integer |No |1 |Purchase duration for the resource plan. |
|PageNumber |Integer |No |1 |Current page number. The minimum value is 1. Default value: 1. |
|PageSize |Integer |No |20 |Number of records per page. The minimum value is 1, and the maximum value is 100. The default value is 10. |
|OrderType |String |No |asc |The sorting order for the query results. Values:<br><br><br>* `asc`: sort in ascending order.<br><br>* `desc`: sort in descending order. Default value. |
|OrderBy |String |No |ExpirationTime |The field to sort by. Values:<br><br><br>* `EffectiveTime`: the effective time of the resource plan.<br><br>* `ExpirationTime`: the due time of the resource plan.<br><br>* `CreateTime`: the create time of the resource plan. |


<span id="timefilter"></span>
### TimeFilter


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|EndTime |String |No |2027\-08\-20T08:00:00.000Z |The end time (UTC) of the time period for querying resource plans by expiration date. Format: `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|StartTime |String |No |2026\-08\-19T08:00:00.000Z |The start time (UTC) of the time period for querying resource plans by expiration date. Format: `yyyy-MM-ddTHH:mm:ss.sssZ`. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Total |Integer |21 |The quantity of results that meet the query conditions. |
|ResourcePackages |Array of [ResourcePackage](https://docs.byteplus.com/en/docs/40/66091#resourcepackage) |Refer to the Sample response. |Details of the resource plan. |


<span id="resourcepackage"></span>
### ResourcePackage


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|CreateTime |String |2025\-08\-26T06:51:19.000Z |The creation time (UTC) of the resource plan. Format: `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|EffectiveTime |String |2025\-09\-30T14:00:00.000Z |The effective time of the resource plan (UTC time). Format: `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|ExpirationTime |String |2025\-10\-30T15:59:59.000Z |The expiration time of the resource plan (UTC time). Format: `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|PackageId |String |rds\-pkg\-210000\*\*\*\*\-ec95 |Resource plan ID. |
|PackageSpec |String |100 |Resource plan specifications. |
|PackageStatus |String |NotEffective |The state of the resource plan. Values:<br><br><br>* `NotEffective`: not effective.<br><br>* `InUse`: in use.<br><br>* `Expire`: expired. |
|PackageType |String |StoragePackage |The deduction item of the resource plan. Currently, only `StoragePackage` is supported, which is a storage plan. |
|PurchaseDuration |Integer |1 |Purchase duration for the resource plan. The unit is month. |
|Region |String |cn\-beijign |The region where the resource plan is located. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=ListResourcePackages&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "ExpirationTime": {
        "EndTime": "2029-08-20T08:00:00.000Z",
        "StartTime": "2026-08-20T08:00:00.000Z"
    }
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20250922223137889D767ED5A0B1FEB66D-35b4e1",
        "Action": "ListResourcePackages",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {
        "ResourcePackages": [
            {
                "CreateTime": "2025-08-19T08:22:15.000Z",
                "EffectiveTime": "2025-08-20T08:00:00.000Z",
                "ExpirationTime": "2028-08-20T15:59:59.000Z",
                "PackageId": "rds-pkg-210000****-4e1f",
                "PackageSpec": "100",
                "PackageStatus": "InUse",
                "PackageType": "StoragePackage",
                "PurchaseDuration": 36,
                "Region": "cn-beijing"
            },
            {
                "CreateTime": "2025-08-19T08:22:15.000Z",
                "EffectiveTime": "2025-08-20T08:00:00.000Z",
                "ExpirationTime": "2028-08-20T15:59:59.000Z",
                "PackageId": "rds-pkg-210000****-24f5",
                "PackageSpec": "100",
                "PackageStatus": "InUse",
                "PackageType": "StoragePackage",
                "PurchaseDuration": 36,
                "Region": "cn-beijing"
            }
        ],
        "Total": 2
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
