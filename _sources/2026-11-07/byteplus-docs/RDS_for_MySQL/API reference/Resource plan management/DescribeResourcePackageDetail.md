---
title: "DescribeResourcePackageDetail"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/DescribeResourcePackageDetail"
---

Call the DescribeResourcePackageDetail API to query the detailed usage information of the resource plan.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeResourcePackageDetail&serviceCode=rds_mysql&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|PackageId |String |Yes |rds\-pkg\-210000\*\*\*\*\-4e1f |Resource plan ID. |
|QueryStartTime |String |Yes |2025\-09\-21T16:00:00Z |The start time of the specific time period (UTC time). The format is `yyyy-MM-ddTHH:mm:ssZ`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The start time of the task cannot be earlier than seven days before the current date.</div><br> |
|QueryEndTime |String |Yes |2025\-09\-28T15:59:59Z |The end time of the specific time period (UTC time). The format is `yyyy-MM-ddTHH:mm:ssZ`. |
|PageNumber |Integer |No |1 |Current page number. The minimum value is 1. Default value: 1. |
|PageSize |Integer |No |10 |Number of records per page. The minimum value is 1, and the maximum value cannot exceed 1,000. The default value is 10. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|ResourcePackage |Object of [ResourcePackage](https://docs.byteplus.com/en/docs/40/66088#resourcepackage) |Refer to the Sample response. |Details of the resource plan. |
|Total |Integer |3 |The quantity of usage details for the resource plan. |
|UsageProgress |Integer |89 |The usage progress of the resource plan. The unit is percentage. |


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
POST /?Action=DescribeResourcePackageDetail&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "PackageId": "rds-pkg-210000****-4e1f",
    "QueryStartTime": "2025-09-21T16:00:00Z",
    "QueryEndTime": "2025-09-28T15:59:59Z",
    "PageNumber": 1,
    "PageSize": 10
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20250923112134D0FDC5B835A79FF44B47-2f9056",
        "Action": "DescribeResourcePackageDetail",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {
        "ResourcePackage": {
            "CreateTime": "2025-08-26T06:51:19.000Z",
            "EffectiveTime": "2025-08-26T06:00:00.000Z",
            "ExpirationTime": "2025-09-26T15:59:59.000Z",
            "PackageId": "rds-pkg-2100000746-b4e7",
            "PackageSpec": "100",
            "PackageStatus": "InUse",
            "PackageType": "StoragePackage",
            "PurchaseDuration": 1,
            "Region": "cn-beijing"
        },
        "Total": 0,
        "UsageItems": null,
        "UsageProgress": 89
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
