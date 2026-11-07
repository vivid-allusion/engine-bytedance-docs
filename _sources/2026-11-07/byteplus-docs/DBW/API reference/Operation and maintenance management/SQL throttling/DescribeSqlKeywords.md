---
title: "DescribeSqlKeywords"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/DescribeSqlKeywords"
---

Call the DescribeSqlKeywords API to generate SQL throttling keywords based on the original SQL statement.

<span id="Afs3PODX"></span>
## Request type

Synchronous request

<span id="XHOgzaSR"></span>
## Request parameters


|**Name** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|InstanceId<br><br> |String |Yes |mysql\-383906\*\*\*\*\*\* |Database instance ID<br><br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances) API to query the instance ID of RDS for MySQL.<br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances) API to query the instance ID of NDB MySQL. |
|InstanceType |String |Yes |MySQL |Database types. The following database types are supported:<br><br><br>* `MySQL`: RDS for MySQL.<br><br>* `VeDBMySQL`: NDB for MySQL. |
|RegionId |String |Yes |cn\-beijing |Region ID. |
|Sql |String |Yes |select \* from test |Sample of the original SQL statement. |


<span id="tl7xU1qp"></span>
## Response parameters


|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|KeyWords |String |select~from~test |SQL keywords. |


<span id="eE3mBd9J"></span>
## Request example

```JSON
POST /?Action=DescribeSqlKeywords&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dbw.cn-beijing.byteplusapi.com.cn
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/dbw/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****

{
    "Sql": "select * from test",
    "InstanceType": "MySQL",
    "InstanceId": "mysql-383906******",
    "RegionId": "cn-beijing"
}
```


<span id="DvMZpCen"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20261008151202094E295FA0449BF29C8F-6ea562",
        "Action": "DescribeSqlKeywords",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "KeyWords": "select~from~test"
    }
}
```


<span id="tE1zBPpA"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes?_vtm_=a106466.b106468.0_0.0_0.0.4527_7694130500017817107&lang=en).
