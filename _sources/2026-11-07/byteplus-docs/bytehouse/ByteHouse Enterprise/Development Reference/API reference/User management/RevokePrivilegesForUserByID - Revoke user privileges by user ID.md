---
title: "RevokePrivilegesForUserByID - Revoke user privileges by user ID"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/revoke-privileges-for-user-by-id"
---

Revoke user privileges based on user ID.

<span id="e22c4cb4"></span>
## Request parameters

The table below lists only the specific request parameters for this interface and some common parameters. For more information, refer to [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Parameter | | |Type |Required |Example Value |Description |
|---|---|---|---|---|---|---|
|Action | | |String |Yes |RevokePrivilegesForUserByID |The action to be performed is: RevokePrivilegesForUserByID. |
|Version | | |String |Yes |2024\-08\-31 |The API version is: 2024\-08\-31. |
|UserID | | |String |Yes |123456 |User ID |
|Grants | | |Object |No |[<br><br>{<br><br>"Privileges": [<br><br>{<br><br>"Name": "SELECT",<br><br>"Columns": [<br><br>"column1"<br><br>]<br><br>}<br><br>],<br><br>"Targets": [<br><br>{<br><br>"Database": "db1",<br><br>"Table": "tb1"<br><br>}<br><br>],<br><br>"OnCluster": "cluster1",<br><br>"ClusterID": 137,<br><br>"GrantOption": true,<br><br>"GrantTo": "user1",<br><br>"RawSql": "grant sql"<br><br>}<br><br>] |Permission information |
| |OnCluster | |String |is |cluster1 |authorized associated cluster name |
| |GrantOption | |Boolean |is |false |whether the permission can be granted to other users |
| |GrantTo | |String |No |user1 |Object Granted Permissions |
| |RawSql | |String |No |grant sql |SQL for Granting Permissions |
| |Privileges | |Array of Object |is |[<br><br>{<br><br>"Name": "SELECT",<br><br>"Columns": [<br><br>"column1"<br><br>]<br><br>}<br><br>] |Column Permissions |
| | |Name |String |Yes |SELECT |Permission Name |
| | |Columns |Array of String |Yes |column1 |Column |
| |Targets | |Array of Object |Is |[<br><br>{<br><br>"Database": "db1",<br><br>"Table": "tb1"<br><br>}<br><br>] |Authorized library table |
| | |Database |String |Yes |db1 |The library in ck |
| | |Table |String |Yes |tb1 |CK table |
| |ClusterID | |Integer |No |123 |Cluster ID associated with authorization |


<span id="0ad16f25"></span>
## Response parameters

The table below lists only the specific response parameters for this interface. For more information, refer to [request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Parameter | |Type |Sample value |Description |
|---|---|---|---|---|
|Message | |String |None |Message returned by the top gateway |
|Data | |Object | |Return data |
| |Message |String |successfully revoke privileges from user1 |Response message |


<span id="51f1aa37"></span>
## Request example

```text
POST /?Action=RevokePrivilegesForUserByID&Version=2024-08-31 HTTP/1.1
Host: open.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20240912T092459Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240912/ap-southeast-1/bytehouse_ce/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "UserID": "123456",
  "Grants": {
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
    "ClusterID": 908,
    "GrantOption": true,
    "GrantTo": "user1",
    "RawSql": "grant sql"
  }
}
```


<span id="ded43a01"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "20240912172508081024246015C4D83D",
    "Action": "RevokePrivilegesForUserByID",
    "Version": "2024-08-31",
    "Service": "bytehouse_ce",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Message": "",
    "Data": {
      "message": "successfully revoke privileges from user1"
    }
  }
}
```


<span id="63488036"></span>
## Error code

The table below lists the error codes related to this interface and business logic. For common error codes, refer to [common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |Bad Request |api service received invalid request format |Parameter error |
|401 |SignatureNotMatch |The request signature provided is incorrect. | |
|500 |InternalError |The request has failed due to an unknown error. | |
|503 |ServiceUnavailable |The request has failed due to a temporary failure of the server. | |
