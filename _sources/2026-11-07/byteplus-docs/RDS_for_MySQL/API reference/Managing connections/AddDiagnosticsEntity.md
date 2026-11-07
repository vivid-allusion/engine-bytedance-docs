---
title: "AddDiagnosticsEntity"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/adddiagnosticsentity"
---

Call the AddDiagnosticsEntity API to add diagnostic items for connection diagnostics to an instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

In a single call, you can add up to 10 diagnostic items for public network connections or 10 for private network connections. Under a single instance, you can add up to 500 diagnostic items for public network connections or private network connections.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=AddDiagnosticsEntity&serviceCode=rds_mysql&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-db6d920e\*\*\*\* |Instance ID. |
|EndpointId |String |Yes |mysql\-db6d920e\*\*\*\*\-cluster |The Endpoint ID for the connection diagnosis. |
|DiagnosticsType |String |No |PrivateLink |The type of connection to diagnose. Values:<br><br><br>* `PrivateLink`: via private network.<br><br>* `PublicLink`: via public network.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When used as a request parameter, the default value is <code>PrivateLink</code>.</div><br> |
|EcsInstanceIds |Array of String |No |["i\-yd7nac9mv44uvzod\*\*\*\*"] |Elastic Computing Services ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Required when DiagnosticsType is set to <code>PrivateLink</code> for a connection diagnosis via private network.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Add up to 50 ECS IDs can be entered. The IDs cannot be repeated.</div><br> |
|PublicIpAddresses |Array of String |No |["192. ** *.* ** .5"] |Public IP address.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is required for a connection diagnosis via public network when DiagnosticsType is set to <code>PublicLink</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Add up to 50 public network IPs can be entered. The IPs cannot be repeated.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=AddDiagnosticsEntity&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-db6d920e****",
    "EcsInstanceIds": [
        "i-yd7nac9mv44uvzod****"
    ],
    "EndpointId": "mysql-db6d920e****-cluster"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20241031104653C09CE8FBC43FB705D52A-00d4e3",
        "Action": "AddDiagnosticsEntity",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": null
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
