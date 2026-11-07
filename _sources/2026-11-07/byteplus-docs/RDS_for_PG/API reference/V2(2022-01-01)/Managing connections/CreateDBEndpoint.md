---
title: "CreateDBEndpoint"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/createdbendpoint"
---

Call the CreateDBEndpoint API to create an endpoint for the specified instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-21a3333b\*\*\*\* |Instance ID. |
|EndpointType |String |Yes |Custom |Endpoint type, currently only supports the value `Custom`, meaning custom type. |
|ReadWriteMode |String |No |ReadOnly |Read/Write mode:<br><br><br>* `ReadWrite`: Read/write.<br><br>* `ReadOnly`: read\-only. Default value. |
|EndpointName |String |No |EndpointName |Instance endpoint name.<br><br><br>* It cannot start with a digit or hyphen (\-).<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The length must be between 1 and 64 characters.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If not provided, the endpoint will be automatically named "Customized_endpoint".</div><br> |
|Nodes |String |No |Primary,postgres\-ca7b7019\*\*\*\*\-rocbcb |Node list for endpoint configuration.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Required when <code>EndpointType</code> is <code>Custom</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">No node ID is needed for the primary node. Use the primary string.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=CreateDBEndpoint&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-ca7b7019****",
    "EndpointName": "自定义终端",
    "EndpointType": "Custom",
    "Nodes": "postgres-ca7b7019****-rocbcb",
    "ReadWriteMode": "ReadOnly"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202308021119002CCE8C74AFEBB9023B8E",
        "Action": "CreateDBEndpoint",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": null
}
```
