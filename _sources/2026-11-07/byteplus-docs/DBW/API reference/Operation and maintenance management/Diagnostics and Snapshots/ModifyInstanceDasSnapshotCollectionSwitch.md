---
title: "ModifyInstanceDasSnapshotCollectionSwitch"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/ModifyInstanceDasSnapshotCollectionSwitch"
---

Call the ModifyInstanceDasSnapshotCollectionSwitch operation to modify the session snapshot collection feature.

<span id="vuq5Ht1F"></span>
## Request type

Synchronous request

<span id="uJb3jsrm"></span>
## Request parameters


|**Name** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-f3b91\*\*\*\*\*\*\*\*\*<br><br> |Database instance ID<br><br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances) API to query the instance ID of RDS for MySQL.<br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances) API to query the instance ID of NDB MySQL.<br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances?_vtm_=a106466.b106468.0_0.0_0.0.2109_7610615829733918244&lang=en) API to query the instance ID of RDS for PostgreSQL.<br><br>* Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances?lang=en) API to query the instance ID of Document Database for MongoDB. |
|InstanceType<br><br> |String |Yes |MySQL |Database types. The following database types are supported:<br><br><br>* `MySQL`: RDS for MySQL.<br><br>* `VeDBMySQL`: NDB for MySQL.<br><br>* `Postgres`: RDS for PostgreSQL.<br><br>* `Mongo`: Document Database for MongoDB. |
|DasSnapShotLists |Array of string |Yes |```JSON```<br>```[```<br>```    "Dialog"```<br>```]```<br> |Whether to enable session snapshot collection. The values are as follows:<br><br><br>* When the value is set to `Dialog`, it indicates that session snapshot collection is enabled for the instance.<br><br>* When the value is set to an empty array, it indicates that session snapshot collection is not enabled for the instance. |
|Switch |Boolean |Yes |true |Whether to enable session snapshot collection. Valid values:<br><br><br>* `true`: Indicates that session snapshot collection is enabled.<br><br>* `false`: Indicates that session snapshot collection is disabled.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The API takes effect only when <code>DasSnapShotLists</code> is configured as <code>["Dialog"]</code> and <code>Switch</code> is configured as <code>true</code>.</div><br> |
|RegionId |String |Yes |cn\-beijing |Region ID. |
|EnableBackoff |Boolean |No |true |Specifies whether to enable the backoff strategy. Valid values:<br><br><br>* `true`: (Default) Enables the backoff strategy. After the backoff strategy is enabled, if collection fails due to an instance anomaly, the collection automatically applies the backoff strategy and gradually reduces the collection frequency until it returns to normal.<br><br>* `false`: Disables the backoff strategy.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter takes effect only when the <code>Switch</code> parameter is set to <code>true</code>.</div><br> |


<span id="I4N9ZIDb"></span>
## Response parameters


|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Success |Boolean |true |Modify session snapshot collection. Valid values:<br><br><br>* `true`: Indicates that the session snapshot collection feature is successfully modified.<br><br>* `false`: indicates that modifying the session snapshot collection feature failed. |


<span id="JYzMElTV"></span>
## Request example

```JSON
POST /?Action=ModifyInstanceDasSnapshotCollectionSwitch&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dbw.cn-beijing.byteplusapi.com.cn
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/dbw/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****

{
    "InstanceId": "mysql-f3b916bef3c8",
    "InstanceType": "MySQL",
    "RegionId": "cn-beijing",
    "DasSnapShotLists": [
        "Dialog"
    ],
    "Switch": true,
    "EnableBackoff": true
}
```


<span id="Sb2kUHNf"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20261008142104473B3FA7AE1387227552-201086",
        "Action": "ModifyInstanceDasSnapshotCollectionSwitch",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "Success": true
    }
}
```


<span id="y24FLc0R"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes?_vtm_=a106466.b106468.0_0.0_0.0.4527_7694130500017817107&lang=en).
