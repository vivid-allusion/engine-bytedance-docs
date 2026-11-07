---
title: "DescribeResourcePackageSpec"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/DescribeResourcePackageSpec"
---

Call the DescribeResourcePackageSpec interface to query the specifications of the resource package.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|PackageType |String |Yes |StoragePackage |The type of the resource package. Currently, only the value `StoragePackage` is supported, which means a storage package. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|PackageSpecs |String[] |[ "100", "200", "300", "500", "1000", "2000", "5000", "10000" ] |The specification of the resource package. The unit is GiB. |
|PackagePriceDetails |Object[] |Please refer to the return example. |The deduction items of the resource package and the corresponding deduction factors for the deduction items. |
|DeductionItem |String |Regular backup space |Deduction items. The values can be `Regular Backup Space`, `Backup Space of Deleted Instances`, or `Cross-regional Backup Space`. |
|DeductionFactor |String |0.16 |Deduction factor. |

## Sample request

```json
POST /?Action=DescribeResourcePackageSpec&Version=2022-01-01
Host: open.ap-southeast-1.byteplusapi.com
Content-Type: application/json
X-Date: 20180614T114308Z
Authorization: HMAC-SHA256 Credential=AKIAIAGMBG4SXSQQ****/20180614/ap-southeast-1/rds_mysql/request, SignedHeaders=accept;content-type;host;x-date, Signature=6a593bf5f59e7c1109fb205c739d1cff4c672fe2d251963f4d48c8701d16****
{
    "PackageType": "StoragePackage"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202509222237438FA55B82971F2EDBA3D6-c76ee6",
        "Action": "DescribeResourcePackageSpec",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {
        "PackagePriceDetails": [
            {
                "DeductionFactor": "0.16",
                "DeductionItem": "常规备份空间"
            },
            {
                "DeductionFactor": "0.16",
                "DeductionItem": "已删除实例备份空间"
            },
            {
                "DeductionFactor": "0.64",
                "DeductionItem": "跨地域备份空间"
            }
        ],
        "PackageSpecs": [
            "100",
            "200",
            "300",
            "500",
            "1000",
            "2000",
            "5000",
            "10000"
        ]
    }
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
