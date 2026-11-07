---
title: "ModifyDBInstanceSSL"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/ModifyDBInstanceSSL"
---

Call the ModifyDBInstanceSSL interface to modify the SSL configuration of the specified instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-f006d308\*\*\*\* |Instance ID. |
|SSLEnable |Boolean |No |false |Enable SSL encryption or not, with values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|ReloadSSLCertificate |Boolean |No |true |Update the SSL certificate validity period. When set to `true`, updates the SSL certificate validity period.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter takes effect only when SSL encryption is enabled for the instance.</div><br><br><br>* <div data-tips="true" data-tips-type="default">ReloadSSLCertificate and SSLEnable cannot be passed in simultaneously.</div><br> |
|ForceEncryption |Boolean |No |true |Enable SSL force encryption or not, with values:<br><br><br>* `true`: yes.<br><br>* `false`: no.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter takes effect only when SSL encryption is enabled for the instance.</div><br><br><br>* <div data-tips="true" data-tips-type="default">ReloadSSLCertificate and SSLEnable cannot be passed in simultaneously.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=ModifyDBInstanceSSL&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-f006d308****",
    "SSLEnable": false,
    "ReloadSSLCertificate": true,
    "ForceEncryption": true
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20240423194017B2017EFDCA4047D90871-5308fb",
        "Action": "ModifyDBInstanceSSL",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-guangzhou"
    },
    "Result": null
}
```
