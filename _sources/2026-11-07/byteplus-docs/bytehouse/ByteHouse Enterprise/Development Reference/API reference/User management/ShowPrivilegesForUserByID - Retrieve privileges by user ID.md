---
title: "ShowPrivilegesForUserByID - Retrieve privileges by user ID"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/show-privileges-for-user-by-id"
---

Retrieve privileges based on user ID.

<span id="0f779622"></span>
## Request parameters

The table below lists only the request parameters specific to this interface and some general parameters. For more details, refer to [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |ShowPrivilegesForUserByID |Required action is ShowPrivilegesForUserByID. |
|Version |String |Yes |2024\-08\-31 |The version of the API is 2024\-08\-31. |
|UserID |Integer |Yes |123456 |User ID |


<span id="da7a6bc2"></span>
## Response parameters

The table below lists only the response parameters specific to this interface. For more information, refer to [request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Param | | | |Type |Example Value |Description |
|---|---|---|---|---|---|---|
|Message | | | |String |None |Top Response Information |
|Data | | | |Object |{<br><br>"Grants": [<br><br>{<br><br>"ClusterID": 12345,<br><br>"ClusterName": "cluster",<br><br>"DatabaseName": "db1",<br><br>"TableName": "tb1",<br><br>"Action": "GRANT",<br><br>"Privileges": {<br><br>"Name": "SELECT",<br><br>"Columns": [<br><br>"column1"<br><br>]<br><br>}<br><br>}<br><br>]<br><br>} |Return data |
| |Grants | | |Array of Object |[<br><br>{<br><br>"Privileges": [<br><br>{<br><br>"Name": "SELECT",<br><br>"Nolumns": [<br><br>"column1"<br><br>]<br><br>}<br><br>],<br><br>"Targets": [<br><br>{<br><br>"Database": "db1",<br><br>"Table": "tb1"<br><br>}<br><br>],<br><br>"OnCluster": "cluster1",<br><br>"ClusterID": 137,<br><br>"GrantOption": true,<br><br>"GrantTo": "user1",<br><br>"RawSql": "grant sql"<br><br>}<br><br>] |Show permission interface return data |
| | |ClusterID | |Integer |12345 |Cluster ID |
| | |ClusterName | |String |cluster |Cluster Name |
| | |DatabaseName | |String |db1 |Database Name |
| | |TableName | |String |tb1 |Table Name |
| | |Privileges | |Array of Object |[<br><br>{<br><br>"Name": "SELECT",<br><br>"Columns": [<br><br>"column1"<br><br>]<br><br>}<br><br>] |Column Permissions |
| | | |Name |String |SELECT |Permission Name |
| | | |Columns |Array of String |column1 |Column |
| | |Action | |String |GRANT |Description indicates whether the permission is granted or canceled |


<span id="00c1c3cd"></span>
## Request example

```text
GET /?Action=ShowPrivilegesForUserByID&Version=2024-08-31&UserID=123456 HTTP/1.1
Host: open.byteplusapi.com
X-Date: 20240912T124503Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240912/ap-southeast-1/bytehouse_ce/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

```


<span id="50d95659"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "2024111913543908422215701696F973",
    "Action": "ShowPrivilegesForUserByID",
    "Version": "2024-08-31",
    "Service": "bytehouse_ce",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Message": "-",
    "Data": {
      "Grants": [
        {
          "ClusterID": 12345,
          "ClusterName": "cluster",
          "DatabaseName": "db1",
          "TableName": "tb1",
          "Privileges": [
            {
              "Name": "SELECT",
              "Columns": [
                "column1"
              ]
            }
          ],
          "Action": "GRANT"
        }
      ]
    }
  }
}
```


<span id="75ff43b2"></span>
## Error code

The table below lists the error codes related to the interface and business logic. For common error codes, refer to [common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error code |Error information |Description |
|---|---|---|---|
|400 |Bad Request |api service received invalid request format |Parameter error |
|401 |SignatureNotMatch |The request signature provided is incorrect. | |
|500 |InternalError |The request has failed due to an unknown error. | |
|503 |ServiceUnavailable |The request has failed due to a temporary failure of the server. | |
