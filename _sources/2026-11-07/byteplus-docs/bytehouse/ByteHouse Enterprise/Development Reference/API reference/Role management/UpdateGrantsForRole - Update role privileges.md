---
title: "UpdateGrantsForRole - Update role privileges"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/updategrantsforrole-update-role-privileges"
---

Update role privileges.

<span id="请求参数"></span>
## Request parameters

The table below lists only request parameters specific to this interface and some common parameters. For more details, refer to [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Param | | |Type |Required |Example value |Description |
|---|---|---|---|---|---|---|
|Action | | |String |Yes |UpdateGrantsForRole |The action to be performed, value: UpdateGrantsForRole. |
|Version | | |String |Yes |2024\-08\-31 |The version of the API, value: 2024\-08\-31. |
|RoleID | | |Integer |Yes |12345 |Role ID |
|ActionType | | |String |Yes |GRANT |Permission operation, the value is "Authorize" or "Revoke" |
|Grants | | |Array of Object |Yes |[<br><br>{<br><br>"Privileges": [<br><br>{<br><br>"Name": "SELECT",<br><br>"Columns": [<br><br>"column1"<br><br>]<br><br>}<br><br>],<br><br>"Targets": [<br><br>{<br><br>"database": "db1",<br><br>"table": "tb1"<br><br>}<br><br>],<br><br>"OnCluster": "cluster1",<br><br>"ClusterID": 721,<br><br>"GrantOption": true,<br><br>"GrantTo": "role1",<br><br>"RawSql": "grant sql"<br><br>}<br><br>] |Permissions granted, array length must be bigger than 0, otherwise a BadRequest error is reported |
| |OnCluster | |String |Yes |cluster1 |Authorize associated cluster Name |
| |GrantOption | |Boolean |Yes |false |Can other users be granted this permission? |
| |GrantTo | |String |No |user1 |Object granted permission |
| |RawSql | |String |No |grant sql |SQL for authorizing permissions |
| |Privileges | |Array of Object |Yes |[<br><br>{<br><br>"Name": "SELECT",<br><br>"Columns": [<br><br>"column1"<br><br>]<br><br>}<br><br>] |Column Permission |
| | |Name |String |Yes |SELECT |Permission Name |
| | |Columns |Array of String |Yes |column1 |Column |
| |Targets | |Array of Object |Yes |[<br><br>{<br><br>"Database": "db1",<br><br>"Table": "tb1"<br><br>}<br><br>] |Authorized Database and Tables |
| | |Database |String |Yes |db1 |in the Medium library |
| | |Table |String |Yes |tb1 |Medium table |
| |ClusterID | |Integer |No |123 |Authorized associated cluster ID |


<span id="返回参数"></span>
## Response parameters

The table below lists only the response parameters specific to this interface. For more details, please refer to [request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Param | |Type |Example Value |Description |
|---|---|---|---|---|
|Message | |String |None |Top response information |
|Data | |Object |{<br><br>"Message": "successfully update grants for role1"<br><br>} |Return Data |
| |Message |String |successfully update grants for admin1 |Response Message |


<span id="请求示例"></span>
## Request example

```text
POST /?Action=UpdateGrantsForRole&Version=2024-08-31 HTTP/1.1
Host: open.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20240925T125546Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240925/ap-southeast-1/bytehouse_ce/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
{
  "RoleID": 12345,
  "ActionType": "GRANT",
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
      "ClusterID": 954,
      "GrantOption": true,
      "GrantTo": "role1",
      "RawSql": "grant sql"
    }
  ]
}
```


<span id="返回示例"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "20240912215341192074065120777879",
    "Action": "UpdateGrantsForRole",
    "Version": "2024-08-31",
    "Service": "bytehouse_ce",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Message": "",
    "Data": {
      "Message": "successfully update grants for role1"
    }
  }
}
```


<span id="错误码"></span>
## Error code

The table below lists the error codes related to this interface and business logic. For common error codes, refer to the [common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status Code |Error Code |Error Information |Description |
|---|---|---|---|
|400 |Bad Request |api service received invalid request format |Parameter error |
|400 |BadRequest |api service received invalid request format |Parameter error |
|401 |SignatureNotMatch |The request signature provided is incorrect. | |
|500 |InternalError |The request has failed due to an unknown error. | |
|503 |ServiceUnavailable |The request has failed due to a temporary failure of the server. | |
