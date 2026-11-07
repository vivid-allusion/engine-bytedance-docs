---
title: "CreateDatabase"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/createdatabase"
---

CreateDatabase interface

<span id="7a198b78"></span>
## Request parameters

The following table only lists the request parameters specific to this interface and some common parameters. For more information, please refer to [Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |CreateDatabase |It refers to the operation to be executed, and the value is CreateDatabase. |
|Version |String |Yes |2025\-01\-01 |It refers to the version of the API, and the value is 2025\-01\-01. |
|Name |String |Yes |sample |Database name |
|Description |String |No |Example DB |Description |


<span id="18aae6d9"></span>
## Response parameters

The following table only lists the response parameters specific to this interface. For more information, refer to the [request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|Data |Object |{<br><br>"UUID": "f9cac8f6\-XXXX\-XXXX\-XXXX\-5066356410a2"<br><br>} |Return data. |
|UUID |String |f9cac8f6\-XXXX\-XXXX\-XXXX\-5066356410a2 |Unique key. |


<span id="30c55a5f"></span>
## Request example

```Plain
POST /?Action=CreateDatabase&Version=2025-01-01 HTTP/1.1
Host: open.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20250120T035711Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250120/ap-southeast-1/bytehouse/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "Name": "sample"
}
```


<span id="15c34044"></span>
## Response example

```JSON
{
  "ResponseMetadata": {
    "RequestId": "2025012317045724811510905458D7A5",
    "Action": "CreateDatabase",
    "Version": "2025-01-01",
    "Service": "bytehouse",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Data": {
      "UUID": "f9cac8f6-XXXX-XXXX-XXXX-5066356410a2"
    }
  }
}
```


<span id="843cd6e3"></span>
## Error codes

The following table lists the error codes related to the business logic of this interface. For common error codes, please refer to [Common Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status Code |Error Code |Message |Description |
|---|---|---|---|
|400 |errbook_Metastore_CreateDatabase_BR |Failed to create database err = database already exists |None |
|500 |500 |InternalError |The request has failed due to an unknown error |
