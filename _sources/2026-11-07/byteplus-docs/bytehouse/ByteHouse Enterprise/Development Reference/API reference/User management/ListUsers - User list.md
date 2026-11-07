---
title: "ListUsers - User list"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/list-users"
---

Retrieve the list of users under the tenant.

<span id="01516b70"></span>
## Request parameters

The table below lists only the request parameters specific to this interface and some common parameters. For more information, refer to [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListUsers |The action to be performed, value: ListUsers. |
|Version |String |Yes |2024\-08\-31 |The version of the API, value: 2024\-08\-31. |
|Offset |Integer |No |0 |Pagination query start position |
|Limit |Integer |No |10 |Page Size |


<span id="0ef0efd4"></span>
## Response parameters

The table below lists only the response parameters specific to this interface. For more information, refer to [request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Parameter | | |Type |Example value |Description |
|---|---|---|---|---|---|
|Message | | |String | |Top response information |
|Data | | |Object |{<br><br>"Users": [<br><br>{<br><br>"ID": 123,<br><br>"UserID": 12345678,<br><br>"AccountID": 12345678,<br><br>"Username": "user1",<br><br>"CloudName": "cloudname",<br><br>"UserType": "MAIN",<br><br>"Status": "ACTIVE",<br><br>"Emaill": "xxx@xxx.com",<br><br>"Description": "description",<br><br>"Readonly": true,<br><br>"IsSystemAdmin": true,<br><br>"LastLoginAt": 0,<br><br>"CreatedAt": 1716264720906,<br><br>"UpdatedAt": 1716264720906,<br><br>"Clusters": [<br><br>"UGyGxMqpT"<br><br>]<br><br>}<br><br>],<br><br>"Message": ""<br><br>} |Return data |
| |Users | |Array of Object | |User list |
| | |ID |Integer |123 |User primary ID |
| | |UserID |Integer |12345678 |BytePlus user id |
| | |AccountID |Integer |12345678 |BytePlus tenant id |
| | |Username |String |user1 |Username |
| | |CloudName |String |cloudname |BytePlus Username |
| | |UserType |String |MAIN |User types include "SYSTEM", "MAIN", "NORMAL", "ASSUMED_ROLE" |
| | |Status |String |ACTIVE |User status contains four states "Active_Removed", "Inactive_Removed", "Inactive", "Active" |
| | |Emaill |String |xxx@xxx.com |User E\-mail |
| | |Description |String |description |description information |
| | |Readonly |Boolean |false |Is it read\-only for the user? |
| | |IsSystemAdmin |Boolean |false |Is it a system administrator? |
| | |LastLoginAt |Long |0 |Last login time |
| | |CreatedAt |Long |1716264720906 |Created at |
| | |UpdatedAt |Long |1716264720906 |Last updated |
| | |Immutable |Boolean | |Abandoned Field |
| | |Clusters |Array of String | |User Bound Cluster |
|Meta | | |Object |{<br><br>"Offset": 0,<br><br>"Total": 184<br><br>} |Pagination related data |
| |Offset | |Integer |0 |Start position of data |
| |Total | |String |100 |Total number of data entries |


<span id="014d8080"></span>
## Request example

```text
GET /?Action=ListUsers&Version=2024-08-31&Offset=0&Limit=10 HTTP/1.1
Host: open.byteplusapi.com
X-Date: 20240912T132732Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240912/ap-southeast-1/bytehouse_ce/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

```


<span id="acd1d1ce"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "20240925120141117050224247117731",
    "Action": "ListUsers",
    "Version": "2024-08-31",
    "Service": "bytehouse_ce",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Message": "",
    "Data": {
      "Users": [
        {
          "ID": 123,
          "UserID": 12345678,
          "AccountID": 12345678,
          "Username": "user1",
          "CloudName": "cloudname",
          "UserType": "MAIN",
          "Status": "ACTIVE",
          "Emaill": "xxx@xxx.com",
          "Description": "description",
          "Readonly": true,
          "IsSystemAdmin": true,
          "LastLoginAt": 0,
          "CreatedAt": 1716264720906,
          "UpdatedAt": 1716264720906,
          "Immutable": true,
          "Clusters": [
            "98Al3s"
          ]
        }
      ]
    },
    "Meta": {
      "Offset": 0,
      "Total": "1"
    }
  }
}
```


<span id="fa210bb8"></span>
## Error code

The table below lists the error codes related to this interface and business logic. For common error codes, refer to [common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status Code |Error Code |Error Information |Description |
|---|---|---|---|
|400 |Bad Request |api service received invalid request format |Parameter Error |
|401 |SignatureNotMatch |The request signature provided is incorrect. | |
|500 |InternalError |The request has failed due to an unknown error. | |
|503 |ServiceUnavailable |The request has failed due to a temporary failure of the server. | |
