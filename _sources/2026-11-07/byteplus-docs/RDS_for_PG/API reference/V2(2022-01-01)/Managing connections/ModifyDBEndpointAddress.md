---
title: "ModifyDBEndpointAddress"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/modifydbendpointaddress"
---

Call the ModifyDBEndpointAddress API to modify the instance address.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

You cannot modify both the prefix and port of the private network connection address in one call. Only one can be modified. Request parameters DomainPrefix and Port cannot both be unset or both be set at the same time.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-21a3333b\*\*\*\* |Instance ID. |
|EndpointId |String |No |postgres\-ca7b7019\*\*\*\*\-custom\-f07b |Endpoint ID for modifying a connection endpoint address. If not set, the default endpoint is selected by default. |
|NetworkType |String |Yes |Private |Network type, currently only supports `Private`. |
|DomainPrefix |String |No |postgresc602d39c\*\*\*\* |New access address prefix. The access address prefix must meet the following rules:<br><br><br>* Consist of lowercase letters, numbers, and hyphens (\-).<br><br>* Contain at least 8 characters, with a total length (including the suffix) of no more than 63 characters.<br><br>* Start with a lowercase letter and end with a lowercase letter or number. |
|Port |String |No |5432 |Port number. Value range: 1,000\-65,534. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=ModifyDBEndpointAddress&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-ca7b7019****",
    "EndpointId": "postgres-ca7b7019****-custom-f07b",
    "NetworkType": "Private",
    "DomainPrefix": "newdomainprefix",
    "Port": "5432"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202308021628147ED0667023AE84FD018B",
        "Action": "ModifyDBEndpointAddress",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": null
}
```
