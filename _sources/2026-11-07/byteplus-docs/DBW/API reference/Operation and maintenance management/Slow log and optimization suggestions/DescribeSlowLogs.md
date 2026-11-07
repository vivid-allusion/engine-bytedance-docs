---
title: "DescribeSlowLogs"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/describeslowlogs"
---

Call the DescribeSlowLogs API to query slow log information.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|RegionId |String |Yes |cn\-beijing |Region ID. |
|InstanceId |String |Yes |mysql\-71dffd\*\*\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Call the <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances">DescribeDBInstances</a> API to query the instance ID of RDS for MySQL.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances">DescribeDBInstances</a> API to query the instance ID of NDB for MySQL.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Call the <a href="https://docs.byteplus.com/en/docs/mongodb/describedbinstances?lang=en">DescribeDBInstances</a> API to query the instance ID of Document Database for MongoDB.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Call the <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances?lang=en">DescribeDBInstances</a> API to query the instance ID of RDS for PostgreSQL.</div><br> |
|InstanceType |String |Yes |MySQL |Database type. Valid values are as follows:<br><br><br>* `MySQL`: instance for RDS for MySQL.<br><br>* `VeDBMySQL`: Instance for NDB MySQL.<br><br>* `Document Database for MongoDB`: Document Database for MongoDB.<br><br>* `Postgres`: represents an RDS for PostgreSQL instance. |
|StartTime |Integer |Yes |1681092900 |The start time to query slow logs, which is in the format of a timestamp in seconds. |
|EndTime |Integer |Yes |1681144800 |End time for querying slow logs, using the second timestamp format.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The end time must be later than the start time.</div><br> |
|NodeId |String |No |mysql\-71dffd\*\*\*\-rb45f |Node ID |
|SearchParam |SearchParamObject |No |[SlowLogSearchParam](https://docs.byteplus.com/en/docs/DBW/data-structure#slowlogsearchparam) |Slow log execution search information. |
|PageNumber |Integer |No |1 |Page number. The value range is 1 to 1,000, with a default of 1. |
|PageSize |Integer |No |10 |Number of records per page. The value range is 1 to 1,000, with a default of 10. |
|SortBy |String |No |ASC |Sort slow logs in descending or ascending order. The values are as follows:<br><br><br>* `ASC`: ascending order. Default value.<br><br>* `DESC`: descending order. |
|OrderBy |String |No |Timestamp |Sort method of the returned results. The values are as follows:<br><br><br>* `Timestamp`: Sorts by query start time. Default value.<br><br>* `QueryTime`: Sorts by query time.<br><br>* `LockTime`: Sorts by lock wait time.<br><br>* `RowsExamined`: Sorts by rows scanned.<br><br>* `RowsSent`: Sorts by the rows returned.<br><br>* `RowsAffected`: Sorts by the rows affected. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">A maximum of 5,000 slow logs is supported.</div>



|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|SlowLogs |Array of SlowLog |\- |Slow log list information. For more information, refer to [SlowLog](https://docs.byteplus.com/en/docs/DBW/data-structure#slowlog). |
|Total |Integer |2 |Number of slow logs. |


<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
POST https://dbw.cn-beijing.byteplusapi.com.cn/?Action=DescribeSlowLogs&Version=2018-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: dbw.cn-beijing.byteplusapi.com.cn
X-Date: 20210328T100802Z
Authorization: HMAC-SHA256 Credential=AKLTYmYwNjAzYjFmMjRkNDQwZWI4MzI1MzhjZGY******/20210328/cn-beijing/dbw/request, SignedHeaders=x-date, Signature=e1d274292f8b36eb096e1d2fec02822bd2e5cb3435699938adb7341*******

{
    "PageNumber":1,
    "PageSize":10,
    "RegionId":"cn-beijing",
    "InstanceId":"mysql-71dffd******",
    "NodeId": "mysql-71dffd***-rb45f",
    "InstanceType":"MySQL",
    "StartTime":1681092900,
    "EndTime":1681144800,
    "SearchParam":{
        "DBs":[
            "information_schema"
        ],
        "SourceIPs":[
            "192.168.0.33"
        ],
        "Users":[
            "rootgg"
        ]
    }
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
    "ResponseMetadata":{
        "RequestId":"2023041019454862DC40A243FF051E4892",
        "Action":"DescribeSlowLogs",
        "Version":"2018-01-01",
        "Service":"dbw",
        "Region":"cn-beijing"
    },
    "Result":{
        "SlowLogs":[
            {
                "ConnectionId":2145056,
                "DB":"information_schema",
                "LockTime":0,
                "QueryTime":3.000151,
                "RowsExamined":1,
                "RowsSent":1,
                "SQLTemplate":"select sleep(3);\n/usr/sbin/mysqld, Version: 8.0.26 (MySQL Community Server (GPL)). started with:\nTcp port: 3306  Unix socket: /var/run/mysqld/mysqld.sock\nTime                 Id Command    Argument",
                "SQLText":"select sleep(3);\n/usr/sbin/mysqld, Version: 8.0.26 (MySQL Community Server (GPL)). started with:\nTcp port: 3306  Unix socket: /var/run/mysqld/mysqld.sock\nTime                 Id Command    Argument",
                "SourceIP":"192.168.0.33",
                "Timestamp":1681097392,
                "User":"rootgg"
            }
        ],
        "Total":1
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes).
