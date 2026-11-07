---
title: "GrantPrivilegesToUserByID - Grant privileges to user by user ID"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/grant-privileges-to-user-by-user-id"
---

Grant privileges to user by user ID.

<span id="40230b39"></span>
## Request parameters

The table below only lists the specific request parameters and some common parameters for this interface. For more details, refer to [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Param | | |Type |Required |Example |Description |
|---|---|---|---|---|---|---|
|Action | | |String |Yes |GrantPrivilegesToUserByID |Action to be performed, value: Grant Privileges to User by ID. |
|Version | | |String |Yes |2024\-08\-31 |API version, value: 2024\-08\-31. |
|UserID | | |Integer |Yes |123456 |User ID |
|Grants | | |Array of Object |Yes |[<br><br>{<br><br>"Privileges": [<br><br>{<br><br>"Name": "SELECT",<br><br>"Nolumns": [<br><br>"column1"<br><br>]<br><br>}<br><br>],<br><br>"Targets": [<br><br>{<br><br>"Database": "db1",<br><br>"Table": "tb1"<br><br>}<br><br>],<br><br>"OnCluster": "cluster1",<br><br>"ClusterID": 137,<br><br>"GrantOption": true,<br><br>"GrantTo": "user1",<br><br>"RawSql": "grant sql"<br><br>}<br><br>] |Permission Information |
| |OnCluster | |String |Yes |cluster1 |Associated cluster name authorized |
| |GrantOption | |Boolean |Yes |false |Can this permission be granted to other users |
| |GrantTo | |String |No |user1 |Entity Granted Permissions |
| |RawSql | |String |No |grant sql |SQL for Granting Permissions |
| |Privileges | |Array of Object |Yes |[<br><br>{<br><br>"Name": "SELECT",<br><br>"Columns": [<br><br>"column1"<br><br>]<br><br>}<br><br>] |Column Permissions |
| | |Name |String |Yes |SELECT |Permission Name |
| | |Columns |Array of String |Yes |column1 |Column |
| |Targets | |Array of Object |Yes |[<br><br>{<br><br>"Database": "db1",<br><br>"Table": "tb1"<br><br>}<br><br>] |Tables authorized for permission |
| | |Database |String |Yes |db1 |Database in ck |
| | |Table |String |Yes |tb1 |CK Column |
| |ClusterID | |Integer |No |123 |Authorized associated cluster ID |


<span id="96b58cea"></span>
## Response parameters

The table below only lists the specific response parameters for this interface. For more information, refer to [request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Param | |Type |Example Value |Description |
|---|---|---|---|---|
|Message | |String | |Top response information |
|Data | |Object | |Return data |
| |Message |String |successfully grant privileges to user1 |Response message |


<span id="8d53a6ad"></span>
## Request example

```text
POST /?Action=GrantPrivilegesToUserByID&Version=2024-08-31 HTTP/1.1
Host: open.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20240927T130640Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240927/ap-southeast-1/bytehouse_ce/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "UserID": 123456,
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
      "ClusterID": 140,
      "GrantOption": true,
      "GrantTo": "user1",
      "RawSql": "grant sql"
    }
  ]
}
```


<span id="dc7e8422"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "20240912173949051130014015BD51E7",
    "Action": "GrantPrivilegesToUserByID",
    "Version": "2024-08-31",
    "Service": "bytehouse_ce",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Message": "",
    "Data": {
      "Message": "successfully grant privileges to user1"
    }
  }
}
```


<span id="7ca9c110"></span>
## Error code

The table below lists the error codes related to the interface and business logic. For common error codes, refer to [common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error code |Error information |Description |
|---|---|---|---|
|400 |Bad Request |api service received invalid request format |Parameter error |
|401 |SignatureNotMatch |The request signature provided is incorrect. | |
|500 |InternalError |The request has failed due to an unknown error. | |
|503 |ServiceUnavailable |The request has failed due to a temporary failure of the server. | |
