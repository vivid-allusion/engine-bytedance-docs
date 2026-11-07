---
title: "ShowRolesForUser - Retrieve the list of roles for the User"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/show-roles-for-user-retrieve-the-list-of-roles-for-the-user"
---

Retrieve the list of roles associated with a user.

<span id="f899cc25"></span>
## Request parameters

The table below only lists the specific request parameters and some common parameters for this interface. For more details, refer to [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |ShowRolesForUser |The action to be performed, value: ShowRolesForUser. |
|Version |String |Yes |2024\-08\-31 |The version of the API, value: 2024\-08\-31. |
|Username |String |Yes |user1 |User Name |


<span id="53387859"></span>
## Response parameters

The table below only lists the specific response parameters for this interface. For more information, refer to [request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Param | | |Type |Example Value |Description |
|---|---|---|---|---|---|
|Message | | |String |None |Top Response Information |
|Data | | |Object |{<br><br>"Roles": [<br><br>{<br><br>"RoleID": 123456,<br><br>"RoleName": "role1",<br><br>"RoleIsDefault": true,<br><br>"OnCluster": "cluster1",<br><br>"ClusterID": 12345,<br><br>"AdminOption": true,<br><br>"GrantTo": "user1",<br><br>"RawSql": "grant sql"<br><br>}<br><br>]<br><br>} |Return data, |
| |Roles | |Array of Object | |List of roles, |
| | |RoleID |Integer |123456 |Role ID |
| | |RoleName |String |role1 |Role Name |
| | |RoleIsDefault |Boolean |false |Is the role the default role? |
| | |OnCluster |String |cluster1 |Cluster name associated with the role |
| | |ClusterID |Integer |12345 |Cluster ID |
| | |AdminOption |Boolean |false |Whether they can authorize other users and roles |
| | |GrantTo |String |user1 |The user or role granted the role |
| | |RawSql |String |grant sql |Authorize SQL |
| | |Immutable |Boolean |true |Can the role be removed? |
| | |ImmutableReason |String | |Reason why it cannot be removed |


<span id="908e6f12"></span>
## Request example

```text
GET /?Action=ShowRolesForUser&Version=2024-08-31&Username=user1 HTTP/1.1
Host: open.byteplusapi.com
X-Date: 20240911T130959Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240911/ap-southeast-1/bytehouse_ce/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

```


<span id="add8445c"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "20240911211009146235185019CF69DE",
    "Action": "ShowRolesForUser",
    "Version": "2024-08-31",
    "Service": "bytehouse_ce",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Message": "",
    "Data": {
      "Roles": [
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
          "ImmutableReason": "X1Kqm"
        }
      ]
    }
  }
}
```


<span id="ebfefe47"></span>
## Error code

The table below lists error codes related to this interface and business logic. For common error codes, refer to [common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error code |Error information |Description |
|---|---|---|---|
|400 |Bad Request |api service received invalid request format |Parameter error |
|401 |SignatureNotMatch |The request signature provided is incorrect. | |
|500 |InternalError |The request has failed due to an unknown error. | |
|503 |ServiceUnavailable |The request has failed due to a temporary failure of the server. | |
