---
title: "RevokePrivilegesFromUserByName - Revoke user privileges by user name"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/revoke-user-privileges-from-user-by-name"
---

Revoke user privileges based on user name.

<span id="6de052c3"></span>
## Request parameters

The table below lists only the request parameters specific to this interface and some common parameters. For more information, refer to [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Parameter | | |Type |Required |Example Value |Description |
|---|---|---|---|---|---|---|
|Action | | |String |Yes |RevokePrivilegesFromUserByName |Action to be performed: RevokePrivilegesFromUserByName. |
|Version | | |String |Yes |2024\-08\-31 |API version: 2024\-08\-31. |
|Username | | |String |Yes |user1 |Username |
|Grants | | |Array of Object |No |{<br><br>"Grants": [<br><br>{<br><br>"ClusterID": 12345,<br><br>"ClusterName": "cluster",<br><br>"DatabaseName": "db1",<br><br>"TableName": "tb1",<br><br>"Privileges": {<br><br>"Name": "SELECT",<br><br>"Columns": [<br><br>"column1"<br><br>]<br><br>}<br><br>}<br><br>]<br><br>} |Permission information |
| |OnCluster | |String |Yes |cluster1 |Cluster name associated with authorization |
| |GrantOption | |Boolean |Yes |false |Can this permission be granted to other users? |
| |GrantTo | |String |No |user1 |The object granted permission |
| |RawSql | |String |No |grant sql |SQL for authorization permissions |
| |Privileges | |Array of Object |Yes |[<br><br>{<br><br>"Name": "SELECT",<br><br>"Columns": [<br><br>"column1"<br><br>]<br><br>}<br><br>] |Column Permissions |
| | |Name |String |Yes |SELECT |Permission Name |
| | |Columns |Array of String |is |column1 |column |
| |Targets | |Array of Object |is |[<br><br>{<br><br>"Database": "db1",<br><br>"Table": "tb1"<br><br>}<br><br>] |Authorize permissions for database and tables |
| | |Database |String |Yes |db1 |Database in ck |
| | |Table |String |Yes |tb1 |ck table |
| |ClusterID | |Integer |No |123 |Authorize associated cluster ID |


<span id="785dad27"></span>
## Response parameters

The table below lists only the response parameters specific to this interface. For more information, refer to [request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Param | |Type |Sample value |Description |
|---|---|---|---|---|
|Message | |String | |Top gateway returns message |
|Data | |Object | |Return data |
| |Message |String |successfully revoke privileges from user1 |Response message |


<span id="260a803c"></span>
## Request example

```text
POST /?Action=RevokePrivilegesFromUserByName&Version=2024-08-31 HTTP/1.1
Host: open.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20240912T125444Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240912/ap-southeast-1/bytehouse_ce/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "Username": "user1",
  "Grants": [
    {
      "Privileges": [
        {
          "Name": "SELECT",
          "Columns": [
            "column1"
          ]
        }
      ],
      "Targets": [
        {
          "Database": "db1",
          "Table": "tb1"
        }
      ],
      "OnCluster": "cluster1",
      "ClusterID": 900,
      "GrantOption": true,
      "GrantTo": "user1",
      "RawSql": "grant sql"
    }
  ]
}
```


<span id="587e8530"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "202409122054500970300902085A6FF5",
    "Action": "RevokePrivilegesFromUserByName",
    "Version": "2024-08-31",
    "Service": "bytehouse_ce",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Message": "",
    "Data": {
      "Message": "successfully revoke privileges from user1"
    }
  }
}
```


<span id="c6f06332"></span>
## Error code

The table below lists the error codes related to this interface and business logic. For common error codes, refer to [common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error code |Error information |Description |
|---|---|---|---|
|400 |Bad Request |api service received invalid request format |Parameter error |
|401 |SignatureNotMatch |The request signature provided is incorrect. | |
|500 |InternalError |The request has failed due to an unknown error. | |
|503 |ServiceUnavailable |The request has failed due to a temporary failure of the server. | |
