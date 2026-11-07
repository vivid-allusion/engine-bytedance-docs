---
title: "ModifyDBEndpointProxyConfig"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/ModifyDBEndpointProxyConfig"
---

Call the ModifyDBEndpointProxyConfig API to modify the number of read/write separation proxy connections for the connection endpoint.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Ensure the connection endpoint’s read/write separation function is enabled before calling this API to modify the number of proxy connections.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-0af11cd4\*\*\*\* |Instance ID. |
|EndpointId |String |Yes |postgres\-0af11cd4\*\*\*\*\-cluster |ID of the connection endpoint with the instance enabled for read/write separation.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Currently, only the default endpoint supports read/write separation.</div><br> |
|ReadWriteProxyConnection |Integer |Yes |200 |After enabling read/write separation on a connection endpoint, the number of proxy connections set for the endpoint.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The minimum value for the number of proxy connections is 20.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The maximum number of proxy connections depends on the specification of the instance primary node. Different specifications support different maximum numbers of proxy connections. For details, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/product_specifications">Product specification</a>.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=ModifyDBEndpointProxyConfig&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-f511b775****",
    "EndpointId": "postgres-f511b775****-cluster",
    "ReadWriteProxyConnection": 100
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyDBEndpointProxyConfig",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": null
}
```
