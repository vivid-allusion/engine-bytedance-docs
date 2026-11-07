---
title: "RestartDBInstance"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/restartdbinstance"
---

Call the RestartDBInstance API to restart an instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-21a3333b\*\*\*\* |Instance ID. |
|ApplyScope |String |No |AllNode |Restart scenario. The value can be:<br><br><br>* `AllNode`: all nodes. Default value.<br><br>* `CustomNode`: custom read\-only nodes. |
|CustomNodeIds |Array of String |No |["postgres\-6a85fdfd\*\*\*\*\-ro30f7","postgres\-6a85fdfd\*\*\*\*\-rod958"] |ID of the read\-only node to restart.<br><br><br>* When `ApplyScope` is set to `All nodes`, the entire instance restarts, and the CustomNodeIds parameter cannot be set.<br><br>* When `ApplyScope` is set to `CustomNode`, this parameter requires the IDs of the read\-only nodes to restart. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=RestartDBInstance&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-21a3333b****",
    "ApplyScope": "CustomNode",
    "CustomNodeIds": [
        "postgres-857a4a97****-rod301"
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202306192236493E0DA6BBDC4CB9AB1711",
        "Action": "RestartDBInstance",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": null
}
```
