---
title: "ShowPrivilegesForUserByName - Get privileges by user name"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/show-privileges-for-user-by-name"
---

Retrieve privileges based on user name.

<span id="673118bd"></span>
## Request parameters

The table below lists only the request parameters specific to this interface and some common parameters. For more information, refer to [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |ShowPrivilegesForUserByName |Action to be performed: ShowPrivilegesForUserByName. |
|Version |String |Yes |2024\-08\-31 |API version: 2024\-08\-31. |
|Username |String |Yes |user1 |Username |


<span id="28984c0f"></span>
## Request parameters

The table below lists only the return parameters specific to this interface. For more information, refer to [request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Parameter | | | |Type |Example Value |Description |
|---|---|---|---|---|---|---|
|Message | | | |String |None |Top Response Information |
|Data | | | |Object |{<br><br>"Grants": [<br><br>{<br><br>"ClusterID": 12345,<br><br>"ClusterName": "cluster",<br><br>"DatabaseName": "db1",<br><br>"TableName": "tb1",<br><br>"Action": "GRANT",<br><br>"Privileges": {<br><br>"Name": "SELECT",<br><br>"Columns": [<br><br>"column1"<br><br>]<br><br>}<br><br>}<br><br>]<br><br>} |Return data |
| |Grants | | |Array of Object |[<br><br>{<br><br>"Privileges": [<br><br>{<br><br>"Name": "SELECT",<br><br>"Nolumns": [<br><br>"column1"<br><br>]<br><br>}<br><br>],<br><br>"Targets": [<br><br>{<br><br>"Database": "db1",<br><br>"Table": "tb1"<br><br>}<br><br>],<br><br>"OnCluster": "cluster1",<br><br>"ClusterID": 137,<br><br>"GrantOption": true,<br><br>"GrantTo": "user1",<br><br>"RawSql": "grant sql"<br><br>}<br><br>] |Display permission interface return data |
| | |ClusterID | |Integer |12345 |Cluster ID |
| | |ClusterName | |String |cluster |Cluster Name |
| | |DatabaseName | |String |db1 |Database Name |
| | |TableName | |String |tb1 |Table Name |
| | |Privileges | |Array of Object |[<br><br>{<br><br>"Name": "SELECT",<br><br>"Columns": [<br><br>"column1"<br><br>]<br><br>}<br><br>] |Column Permissions |
| | | |Name |String |SELECT |Permission Name |
| | | |Columns |Array of String |column1 |Column |
| | |Action | |String |GRANT |Description of whether the permission is granted or cancelled |


<span id="d6382bfa"></span>
## Request example

```text
GET /?Action=ShowPrivilegesForUserByName&Version=2024-08-31&Username=user1 HTTP/1.1
Host: open.byteplusapi.com
X-Date: 20240912T131349Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240912/ap-southeast-1/bytehouse_ce/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

```


<span id="362ecb8b"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "2024111913561507623308005358FF1B",
    "Action": "ShowPrivilegesForUserByName",
    "Version": "2024-08-31",
    "Service": "bytehouse_ce",
    "Region": "ap-southeast-1"
  },
  "Result": {
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
    },
    "Message": "-"
  }
}
```


<span id="804cc6d1"></span>
## Error code

The table below lists the error codes related to this interface and business logic. For common error codes, refer to [common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status Code |Error Code |Error Information |Description |
|---|---|---|---|
|400 |Bad Request |api service received invalid request format |Parameter error |
|401 |SignatureNotMatch |The request signature provided is incorrect. | |
|500 |InternalError |The request has failed due to an unknown error. | |
|503 |ServiceUnavailable |The request has failed due to a temporary failure of the server. | |
