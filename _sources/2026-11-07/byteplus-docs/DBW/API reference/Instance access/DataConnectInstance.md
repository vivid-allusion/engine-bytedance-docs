---
title: "DataConnectInstance"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/dataconnectinstance"
---

Call the DataConnectInstance API to connect to the instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronize request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|InstanceType |String |Yes |MySQL |Database type: The following databases are supported:<br><br><br>* `MySQL`: RDS for MySQL.<br><br>* `VeDBMySQL`: NDB for MySQL.<br><br>* `Redis`: Cache for Redis.<br><br>* `Mongo`: Document Database for MongoDB. |
|MongoNodeId |String |Yes |mongo\-shard\-aec0d9c2\*\*\*\*\-0 |Node ID of MongoDB.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The <code>MongoNodeId</code> parameter is required only when <code>InstanceType</code> is set to <code>Mongo</code>.</div><br> |
|InstanceId |String |Yes |mysql\-ba2f323b\*\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can select the following APIs to query the instance ID as needed:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances">DescribeDBInstances</a> API to query the instance ID of RDS for MySQL.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances">DescribeDBInstances</a> API to query the instance ID of NDB for MySQL.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Call the <a href="https://docs.byteplus.com/en/docs/redis/describedbinstances">DescribeDBInstance</a> API to query the instance ID of Cache for Redis.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/mongodb/describedbinstances">DescribeDBInstances</a> API to query all instance IDs of Document Database for MongoDB in the target region.</div><br> |
|Username |String |Yes |test |Database account.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When <code>Instance type</code> is set to <code>Redis</code> to connect to a Cache for Redis instance, this parameter must be set to<code> default</code>.</div><br> |
|Password |String |Yes |password123 |Database account password. |
|DatabaseName |String |No |sys |The name of the database connected to the instance. Depending on the instance type, the default connected databases are as follows:<br><br><br>* RDS for MySQL: By default, it connects to the `information_schema` database.<br><br>* NDB for MySQL: By default, it connects to the `information_schema` database.<br><br>* Cache for Redis: By default, it connects to the `DB0` database.<br><br>* Document Database for MongoDB: By default, it connects to the `admin` database. |
|KeepAliveOverTime |Integer |No |10 |Session timeout time, in second(s). Default is 1,800 seconds. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|SessionId |String |MTU4MDg1MTE1NzM5ODQ3ODg0OC8xNTgwODUxMTU3NDQ0NjIw\*\*\*\* |Session ID. |
|DatabaseName |String |information_schema |The name of the database connected to the instance. |


<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
POST /?Action=DataConnectInstance&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dbw.cn-beijing.byteplusapi.com.cn
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/dbw/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
     "InstanceType": "MySQL",
     "InstanceId": "mysql-ba2f323b*****",
     "Username": "test",
     "Password": "Password123",
     "DatabaseName": "sys",
     "KeepAliveOverTime": 10
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

The following is an example of a normal response.

```json
{
    "ResponseMetadata" : {
        "RequestId": "202210141721010102251451520552E055",
        "Action": "DataConnectInstance",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
 
    "Result": {
         "DatabaseName": "information_schema",
         "SessionId": "MTU4MDg1MTE1NzM5ODQ3ODg0OC8xNTgwODUxMTU3NDQ0NjIw****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes).
