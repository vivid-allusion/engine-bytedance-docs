---
title: "GrantPrivilegesToUserByName - Grant privileges to user by user name"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/grant-privileges-to-user-by-name"
---

Authorize privileges to users by user name.

<span id="36330705"></span>
## Request parameters

The table below only lists the specific Request Parameters and some common parameters for this interface. For more details, refer to [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Param | | |Type |Required |Example value |description |
|---|---|---|---|---|---|---|
|Action | | |String |Yes |GrantPrivilegesToUserByName |Action to be performed: GrantPrivilegesToUserByName. |
|Version | | |String |Yes |2024\-08\-31 |API version, value: 2024\-08\-31. |
|Username | | |String |Yes |user1 |User Name |
|Grants | | |Array of Object |No |[<br><br>{<br><br>"ClusterID": 12345,<br><br>"ClusterName": "cluster",<br><br>"DatabaseName": "db1",<br><br>"TableName": "tb1",<br><br>"Privileges": {<br><br>"Name": "SELECT",<br><br>"Columns": [<br><br>"column1"<br><br>]<br><br>}<br><br>}<br><br>] |Permission Information |
| |OnCluster | |String |Yes |cluster1 |Authorized Cluster Name |
| |GrantOption | |Boolean |Yes |false |Can permissions be granted to other users? |
| |GrantTo | |String |No |user1 |Subject to be granted permission |
| |RawSql | |String |No |grant sql |SQL permission authorization |
| |Privileges | |Array of Object |Yes |[<br><br>{<br><br>"Name": "SELECT",<br><br>"Columns": [<br><br>"column1"<br><br>]<br><br>}<br><br>] |Column Permissions |
| | |Name |String |Yes |SELECT |Permission Name |
| | |Columns |Array of String |Yes |column1 |Column |
| |Targets | |Array of Object |Yes |[<br><br>{<br><br>"Database": "db1",<br><br>"Table": "tb1"<br><br>}<br><br>] |Authorized library tables |
| | |Database |String |Yes |db1 |Library in ck |
| | |Table |String |Yes |tb1 |ck table |
| |ClusterID | |Integer |No |123 |Authorize associated cluster id |


<span id="ce937d12"></span>
## Return parameters

The table below only lists the specific Return Parameters for this interface. For more details, refer to [request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Parameter | |Type |Sample Value |Description |
|---|---|---|---|---|
|Message | |String |None |Top response information |
|Data | |Object | |Return Data |
| |Message |String |successfully revoke privileges from user1 |Response Message |


<span id="bf5a05cd"></span>
## Request example

```text
POST /?Action=GrantPrivilegesToUserByName&Version=2024-08-31 HTTP/1.1
Host: open.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20240912T125849Z
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
      "ClusterID": 400,
      "GrantOption": true,
      "GrantTo": "user1",
      "RawSql": "grant sql"
    }
  ]
}
```


<span id="b0f8ae7d"></span>
## Return example

```json
{
  "ResponseMetadata": {
    "RequestId": "20240912205854194014179032533E5C",
    "Action": "GrantPrivilegesToUserByName",
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


<span id="0b64de69"></span>
## Error code

The table below lists the error codes related to the interface and business logic. For common error codes, refer to [common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status Code |Error Code |Error Information |Description |
|---|---|---|---|
|400 |Bad Request |api service received invalid request format |Parameter Error |
|401 |SignatureNotMatch |The request signature provided is incorrect. | |
|500 |InternalError |The request has failed due to an unknown error. | |
|503 |ServiceUnavailable |The request has failed due to a temporary failure of the server. | |
