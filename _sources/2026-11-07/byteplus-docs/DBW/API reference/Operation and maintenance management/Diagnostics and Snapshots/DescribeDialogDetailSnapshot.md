---
title: "DescribeDialogDetailSnapshot"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/DescribeDialogDetailSnapshot"
---

Call the DescribeDialogDetailSnapshot API to query the details of session information in a session snapshot.

<span id="dRdqaJbi"></span>
## Request type

Synchronous request

<span id="lOQksKhx"></span>
## Request parameters


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|InstanceId<br><br> |String<br><br> |Yes |mysql\-c\*\*\*\*\*\* |Database instance ID<br><br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances) API to query the instance ID of RDS for MySQL.<br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances) API to query the instance ID of veDB MySQL.<br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances?_vtm_=a106466.b106468.0_0.0_0.0.2109_7610615829733918244&lang=en) API to query the instance ID of RDS for PostgreSQL.<br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances?lang=en) API to query the instance ID of Document Database for MongoDB. |
|DSType |String |Yes |MySQL |Database types. The following database types are supported:<br><br><br>* `MySQL`: RDS for MySQL.<br><br>* `VeDBMySQL`: veDB for MySQL.<br><br>* `Postgres`: RDS for PostgreSQL.<br><br>* `Mongo`: Document Database for MongoDB. |
|SnapshotTime |Integer |Yes |1782349500 |Session snapshot timestamp in seconds. |
|PageNumber |Integer |Yes |1 |Page number. |
|PageSize |Integer |Yes |20 |Page size. |
|NodeId |String |No |mysql\-c\*\*\*\*\-0 |Database instance node ID. |
|QueryFilter |[QueryFilter](https://docs.byteplus.com/en/docs/DBW/data-structure?lang=en#BpRWSHHr) |No |```JSON```<br>```{```<br>```    "ShowSleepConnection":true```<br>```}```<br> |Session snapshot filter criteria. |


<span id="KcTop78u"></span>
## Response parameters


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Total |Integer |100 |Total number of session snapshots. |
|DialogDetails |Array of [DialogDetailst](https://docs.byteplus.com/en/docs/DBW/data-structure?lang=en#MJyim8S9) |```JSON```<br>```{```<br>```    "BlockingPid": "",```<br>```    "Command": "Sleep",```<br>```    "DB": "mysql",```<br>```    "Desc": "",```<br>```    "Host": "11.192.56.112:50256",```<br>```    "Info": "NULL",```<br>```    "Namespace": "",```<br>```    "NodeId": "mysql-c******-ma822-0",```<br>```    "PSM": "-",```<br>```    "PlanSummary": "",```<br>```    "ProcessID": "267808",```<br>```    "SnapshotTime": 1782791281,```<br>```    "State": "",```<br>```    "Time": "4s",```<br>```    "User": "test_user"```<br>```}```<br> |Session snapshot details.<br><br> |


<span id="YnekbAFX"></span>
## Request example

```JSON
POST /?Action=DescribeDialogDetailSnapshot&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dbw.cn-beijing.byteplusapi.com.cn
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/dbw/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****

{
    "DSType":"MySQL",
    "InstanceId":"mysql-c******",
    "SnapshotTime":1782791281,
    "PageNumber":1,
    "PageSize":20,
    "QueryFilter":{
        "ShowSleepConnection":true
    }
}
```


<span id="vPDvF1P0"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202606301149113CB9F2FE036AB424B75C-d9b210",
        "Action": "DescribeDialogDetailSnapshot",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "DialogDetails": [
            {
                "BlockingPid": "",
                "Command": "Sleep",
                "DB": "mysql",
                "Desc": "",
                "Host": "11.192.56.112:50256",
                "Info": "NULL",
                "Namespace": "",
                "NodeId": "mysql-c******-ma822-0",
                "PSM": "-",
                "PlanSummary": "",
                "ProcessID": "267808",
                "SnapshotTime": 1782791281,
                "State": "",
                "Time": "4s",
                "User": "test_user"
            }
        ],
        "Total": 1
    }
}
```


<span id="3EI6VqLH"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes).
