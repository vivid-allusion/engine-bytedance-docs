---
title: "GetFullSqlInstanceCorrespondence"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/GetFullSqlInstanceCorrespondence"
---

Call the GetFullSqlInstanceCorrespondence API to query the instance mapping relationship for FullSQL.

<span id="5KpLOCml"></span>
## Request type

Synchronous request

<span id="ffSTFdxg"></span>
## Request parameters


|**Parameter name** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|RegionId |String |Yes |cn\-beijing |Region ID. |
|InstanceID<br><br> |String |No |DBW_FullSql_ed8b2b04\-b985\-4861\-b19d\-e0d2bd\*\*\*\*\*\* |Billing instance ID. Queries the most recent mapping relationships for a billing instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is mutually exclusive with InstanceID. Choose one to pass based on your needs.</div><br> |
|FollowInstanceID |String |No |mysql\-76eda4\*\*\*\*\*\*<br><br> |Instance ID. You can query the corresponding instance ID as needed.<br><br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances?lang=en) API to query the instance ID of RDS for MySQL.<br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances?lang=en) API to query the instance ID of veDB MySQL.<br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances?lang=en) API to query the instance ID of Document Database for MongoDB.<br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances?lang=en) API to query the instance ID of RDS for PostgreSQL.<br><br>* Call the [DescribeDBInstanceSpecs](https://docs.byteplus.com/en/docs/redis/describedbinstancespecs?lang=en) API to query the instance ID for Redis.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter is mutually exclusive with FollowInstanceID. Choose one based on your actual needs.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Response parameters display mapping records in descending order of creation time.</div><br> |
|Limit |Integer |Yes |99 |Maximum number of records to return. Valid range is (0, 100). |


<span id="Qn91N6jg"></span>
## Response parameters


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|FullSqlInstanceInfo |Array of [FullSqlInstance](https://docs.byteplus.com/en/docs/DBW/data-structure?lang=en#result) |```JSON```<br>```{```<br>```    "CreateTime": "2026-06-10 10:40:19",```<br>```    "Deleted": false,```<br>```    "FollowInstanceID": "mysql-76eda4******",```<br>```    "InstanceID": "DBW_FullSql_ed8b2b04-b985-4861-b19d-e0d2bd******",```<br>```    "ModifyTime": "2026-06-10 10:40:29",```<br>```    "ProductType": "FullSqlLog",```<br>```    "Region": "cn-beijing"```<br>```}```<br><br><br> |List of instance mapping results. |


<span id="Jc0IKsYB"></span>
## Example


<Tabs>
<Tab zoneid="e62vu15DtE" title="Pass in the InstanceID parameter">
<TabTitle>Pass in the InstanceID parameter</TabTitle>

<span id="L2Jeqhoy"></span>
### Request example

```JSON
POST /?Action=GetFullSqlInstanceCorrespondence&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dbw.cn-beijing.byteplusapi.com.cn
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/dbw/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****

{
    "RegionId":"cn-beijing",
    "InstanceID":"DBW_FullSql_ed8b2b04-b985-4861-b19d-e0d2bd******",
    "Limit":99
}
```


<span id="O4lguuVa"></span>
### Response example

```SQL
{
    "ResponseMetadata": {
        "RequestId": "20260612113944939E5D56A32827426CA0-d0b463",
        "Action": "GetFullSqlInstanceCorrespondence",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstanceInfo": [
            {
                "CreateTime": "2026-06-10 10:40:19",
                "Deleted": false,
                "FollowInstanceID": "mysql-76eda4******",
                "InstanceID": "DBW_FullSql_ed8b2b04-b985-4861-b19d-e0d2bd******",
                "ModifyTime": "2026-06-10 10:40:29",
                "ProductType": "FullSqlLog",
                "Region": "cn-beijing"
            }
        ]
    }
}
```





</Tab>
<Tab zoneid="ETyOzLC5Ni" title="Pass in the FollowInstanceID parameter">
<TabTitle>Pass in the FollowInstanceID parameter</TabTitle>

<span id="LFy9fbGF"></span>
### Request example

```JSON
POST /?Action=GetFullSqlInstanceCorrespondence&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dbw.cn-beijing.byteplusapi.com.cn
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/dbw/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****

{
    "RegionId":"cn-beijing",
    "FollowInstanceID": "mysql-76eda4******",
    "Limit":99
}
```


<span id="K9aKCot8"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2026061211403906FB3A521B55BB06CFFD-707b68",
        "Action": "GetFullSqlInstanceCorrespondence",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstanceInfo": [
            {
                "CreateTime": "2026-06-10 10:40:19",
                "Deleted": false,
                "FollowInstanceID": "mysql-76eda4******",
                "InstanceID": "DBW_FullSql_ed8b2b04-b985-4861-b19d-e0d2bd******",
                "ModifyTime": "2026-06-10 10:40:29",
                "ProductType": "FullSqlLog",
                "Region": "cn-beijing"
            },
            {
                "CreateTime": "2026-03-17 17:36:18",
                "Deleted": true,
                "FollowInstanceID": "mysql-76eda4******",
                "InstanceID": "DBW_FullSql_e2f39753-a5d7-4de9-afb0-dfdeacd5ec6b",
                "ModifyTime": "2026-04-16 15:06:17",
                "ProductType": "FullSqlLog",
                "Region": "cn-beijing"
            }
        ]
    }
}
```





</Tab>
</Tabs>


<span id="Nt1Ckzhr"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes).

&nbsp;

&nbsp;
