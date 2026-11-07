---
title: "ModifyDBInstanceGlobalReadOnly"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbinstanceglobalreadonly"
---

## Request type

Synchronous request.

## Request parameters

|**Parameter** |**Type** |**Is it required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-db6d920e\*\*\*\* |Instance ID. |
|GlobalReadOnly |Boolean |Yes |false |Specifies whether to enable global read\-only for the instance. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |

## Response parameter

null

## Sample

### Sample request

```json
POST /?Action=ModifyDBInstanceGlobalReadOnly&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-db6d920e****",
    "GlobalReadOnly": false
}
```

Call the ModifyDBInstanceGlobalReadOnly API to enable or disable the global read\-only feature for an instance.

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20241029211654E46A6B19EEDC6F07C8E7-b8ab19",
        "Action": "ModifyDBInstanceGlobalReadOnly",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```

## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
