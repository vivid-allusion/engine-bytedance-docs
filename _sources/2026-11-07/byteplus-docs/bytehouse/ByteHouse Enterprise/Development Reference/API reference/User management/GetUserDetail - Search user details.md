---
title: "GetUserDetail - Search user details"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/get-user-detail-search-user-details"
---

Query user details.

<span id="3b791826"></span>
## Request parameters

The table below lists only the specific request parameters and some common parameters for this interface. For more information, refer to [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |GetUserDetail |The operation to be performed is: GetUserDetail. |
|Version |String |Yes |2024\-08\-31 |The version of the API is: 2024\-08\-31. |
|Username |String |Yes |user1 |Username |


<span id="6b5b40c3"></span>
## Response parameters

The table below lists only the specific response parameters for this interface. For more information, refer to [request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Parameter | | |Type |Example Value |Description |
|---|---|---|---|---|---|
|Message | | |String |None |Top gateway response information |
|Data | | |Object |{<br><br>"User": {<br><br>"ID": 123,<br><br>"UserID": 12345678,<br><br>"AccountID": 12345678,<br><br>"Username": "user1",<br><br>"CloudName": "cloudname",<br><br>"UserType": "MAIN",<br><br>"Status": "ACTIVE",<br><br>"Emaill": "xxx@xxx.com",<br><br>"Description": "description",<br><br>"Readonly": true,<br><br>"IsSystemAdmin": true,<br><br>"LastLoginAt": 0,<br><br>"CreatedAt": 1716264720906,<br><br>"UpdatedAt": 1716264720906,<br><br>"Clusters": [<br><br>"MZ"<br><br>]<br><br>}<br><br>} |Return data |
| |User | |Object | |User details |
| | |ID |Integer |123 |User primary key ID |
| | |UserID |Integer |12345678 |BytePlus user ID |
| | |AccountID |Integer |12345678 |BytePlus tenant ID |
| | |Username |String |user1 |Username |
| | |CloudName |String |cloudname |BytePlus Username |
| | |UserType |String |MAIN |User Types, includes "SYSTEM", "MAIN", "NORMAL", "ASSUMED_ROLE" |
| | |Status |String |ACTIVE |User Status, includes four states "ACTIVE_REMOVED", "INACTIVE_REMOVED", "INACTIVE", "ACTIVE" |
| | |Emaill |String |xxx@xxx.com |User Email |
| | |Description |String |description |Description Information |
| | |Readonly |Boolean |false |Read\-only User? |
| | |IsSystemAdmin |Boolean |false |System Administrator? |
| | |LastLoginAt |Long |0 |Last log in time |
| | |CreatedAt |Long |1716264720906 |Created at |
| | |UpdatedAt |Long |1716264720906 |Last updated |
| | |Immutable |Boolean | |Abandoned Field |
| | |Clusters |Array of String | |User binds Cluster |


<span id="bebcd943"></span>
## Request example

```text
GET /?Action=GetUserDetail&Version=2024-08-31&Username=user1 HTTP/1.1
Host: open.byteplusapi.com
X-Date: 20240912T090304Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240912/ap-southeast-1/bytehouse_ce/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

```


<span id="fc4925bd"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "202409121703080060030331274C8626",
    "Action": "GetUserDetail",
    "Version": "2024-08-31",
    "Service": "bytehouse_ce",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Message": "",
    "Data": {
      "User": {
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
        "Immutable": false,
        "Clusters": [
          "rsVYp46yV"
        ]
      }
    }
  }
}
```


<span id="8ece9df9"></span>
## Error code

The table below lists the error codes related to this interface and business logic. For common error codes, refer to [common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Error code |Error code |Error information |Description |
|---|---|---|---|
|400 |Bad Request |api service received invalid request format |Parameter error |
|400 |InvalidUsername |invalid username |Invalid Username |
|401 |SignatureNotMatch |The request signature provided is incorrect. | |
|500 |InternalError |The request has failed due to an unknown error. | |
|503 |ServiceUnavailable |The request has failed due to a temporary failure of the server. | |
