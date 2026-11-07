---
title: "DescribeInstanceDasSnapShotCollectionStatus"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/DescribeInstanceDasSnapShotCollectionStatus"
---

Call the DescribeInstanceDasSnapShotCollectionStatus API to query the session snapshot collection state and backoff strategy state of the specified database instance.

<span id="CiY29aTv"></span>
## Request type

Synchronous request

<span id="phsH8PXp"></span>
## Request parameters


|**Name** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-f3b91\*\*\*\*\*\*\*\*\*<br><br> |Database instance ID<br><br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances) API to query the instance ID of RDS for MySQL.<br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances) API to query the instance ID of NDB for MySQL.<br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances?_vtm_=a106466.b106468.0_0.0_0.0.2109_7610615829733918244&lang=en) API to query the instance ID of RDS for PostgreSQL.<br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances?lang=en) API to query the instance ID of Document Database for MongoDB. |
|InstanceType<br><br> |String |Yes |MySQL |Database types. The following database types are supported:<br><br><br>* `MySQL`: RDS for MySQL.<br><br>* `VeDBMySQL`: NDB for MySQL.<br><br>* `Postgres`: RDS for PostgreSQL.<br><br>* `Mongo`: Document Database for MongoDB. |
|RegionId |String |Yes |cn\-beijing |Region ID. |


<span id="I9qBZusf"></span>
## Response parameters


|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|DasSnapShotLists |Array of string |```JSON```<br>```[```<br>```    "Dialog"```<br>```]```<br> |Whether to enable session snapshot collection. The values are as follows:<br><br><br>* When the value is `Dialog`, it indicates that session snapshot collection is enabled for the instance.<br><br>* When the value is an empty array, it indicates that session snapshot collection is not enabled for the instance. |
|EnableBackoff<br><br> |Boolean |true |Whether to enable the backoff strategy. Valid values:<br><br><br>* `true`: indicates that the backoff strategy is enabled.<br><br>* `false`: indicates that the backoff strategy is not enabled. |


<span id="OgM1dmfE"></span>
## Request example

```JSON
POST /?Action=DescribeInstanceDasSnapShotCollectionStatus&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dbw.cn-beijing.byteplusapi.com.cn
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/dbw/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****

{
    "InstanceId": "mysql-f3b91******",
    "InstanceType": "MySQL",
    "RegionId": "cn-beijing"
}
```


<span id="f1JPeblE"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20261008142104473B3FA7AE1387227555-9df2a4",
        "Action": "DescribeInstanceDasSnapShotCollectionStatus",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "DasSnapShotLists": [
            "Dialog"
        ],
        "EnableBackoff": true
    }
}
```


<span id="DPmp4MYZ"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes?_vtm_=a106466.b106468.0_0.0_0.0.4527_7694130500017817107&lang=en).
