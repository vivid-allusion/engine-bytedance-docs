---
title: "UpdateGrantsForUser - Update user privileges"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/update-grants-for-user-update-user-privileges"
---

Update the roles and privileges granted to the user.

<span id="fd83fb8e"></span>
## Request parameter

The table below lists only the specific parameters of this interface and some common parameters. For more details, refer to [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Param | | |Type |Required |Example Value |Description |
|---|---|---|---|---|---|---|
|Action | | |String |Yes |UpdateGrantsForUser |Required action, value: UpdateGrantsForUser. |
|Version | | |String |Yes |2024\-08\-31 |API version, value: 2024\-08\-31. |
|Username | | |String |Yes |user1 |Username |
|ActionType | | |String |Yes |GRANT |Permission Action, the value can be "GRANT" or "REVOKE" |
|Grants | | |Array of Object |No |[<br><br>{<br><br>"Privileges": [<br><br>{<br><br>"Name": "SELECT",<br><br>"Columns": [<br><br>"column1"<br><br>]<br><br>}<br><br>],<br><br>"Targets": [<br><br>{<br><br>"database": "db1",<br><br>"table": "tb1"<br><br>}<br><br>],<br><br>"OnCluster": "cluster1",<br><br>"ClusterID": 721,<br><br>"GrantOption": true,<br><br>"GrantTo": "user1",<br><br>"RawSql": "grant sql"<br><br>}<br><br>] |The roles granted cannot be empty or have empty assignments simultaneously |
| |Privileges | |Array of Object |Yes | |Column Permissions |
| | |Name |String |Yes |SELECT |Permission Name |
| | |Columns |Array of String |Yes |column1 |Column |
| |Targets | |Array of Object |Yes | |Authorized Tables |
| | |Database |String |Yes |db1 |Medium Library in ck |
| | |Table |String |Yes |tb1 |ck table |
| |OnCluster | |String |Yes |cluster1 |Authorized associated cluster name |
| |ClusterID | |Integer |No | |Authorized associated cluster id |
| |GrantOption | |Boolean |Yes |false |Whether permission can be granted to other users |
| |GrantTo | |String |No |user1 |The object with granted permissions |
| |RawSql | |String |No |grant sql |Authorize permissions SQL |
|Assignments | | |Array of Object |No |[<br><br>{<br><br>"RoleID": 123456,<br><br>"RoleName": "role1",<br><br>"RoleIsDefault": true,<br><br>"OnCluster": "cluster1",<br><br>"ClusterID": 12345,<br><br>"AdminOption": true,<br><br>"GrantTo": "user1",<br><br>"RawSql": "grant sql",<br><br>"Immutable": true,<br><br>"ImmutableReason": "aESvn0O8hBC"<br><br>}<br><br>] |The granted permissions cannot be empty concurrently with Grants |
| |RoleID | |Integer |Yes |123456 |Role ID |
| |RoleName | |String |No |role1 |Role name |
| |RoleIsDefault | |Boolean |No |false |Is the role a default role? |
| |OnCluster | |String |Yes |cluster1 |Cluster name associated with the role |
| |ClusterID | |Integer |No |12345 |cluster id |
| |AdminOption | |Boolean |No |false |Can authorize other users and roles |
| |GrantTo | |String |No |user1 |User or role granted roles |
| |RawSql | |String |No |grant sql |Authorize SQL |
| |Immutable | |Boolean |No |true |Can roles be removed |
| |ImmutableReason | |String |No | |Reason that cannot be removed |


<span id="ed902235"></span>
## Response parameter

The table below lists only the specific return parameters of this interface. For more information, refer to [request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Param | |Type |Example Value |Description |
|---|---|---|---|---|
|Message | |String |None |TOP gateway response information |
|Data | |Object | |Return data |
| |Message |String |successfully update grants for admin1 |Response message |


<span id="ee0e7ec5"></span>
## Parameter example

```text
POST /?Action=UpdateGrantsForUser&Version=2024-08-31 HTTP/1.1
Host: open.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20240912T043933Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240912/ap-southeast-1/bytehouse_ce/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "Username": "user1",
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
      "ClusterID": 673,
      "GrantOption": true,
      "GrantTo": "user1",
      "RawSql": "grant sql"
    }
  ],
  "Assignments": [
    {
      "RoleID": 123456,
      "RoleName": "role1",
      "RoleIsDefault": true,
      "OnCluster": "cluster1",
      "ClusterID": 12345,
      "AdminOption": true,
      "GrantTo": "user1",
      "RawSql": "grant sql",
      "Immutable": true,
      "ImmutableReason": "QWg"
    }
  ]
}
```


<span id="4400334f"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "202409121240170520760551000644EA",
    "Action": "UpdateGrantsForUser",
    "Version": "2024-08-31",
    "Service": "bytehouse_ce",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Message": "",
    "Data": {
      "Message": "successfully update grants for admin1"
    }
  }
}
```


<span id="9eada769"></span>
## Error code

The table below lists the error codes related to this interface and business logic. For common error codes, refer to [common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error code |Error information |Description |
|---|---|---|---|
|400 |Bad Request |api service received invalid request format |Parameter error |
|401 |SignatureNotMatch |The request signature provided is incorrect. | |
|500 |InternalError |The request has failed due to an unknown error. | |
|503 |ServiceUnavailable |The request has failed due to a temporary failure of the server. | |
