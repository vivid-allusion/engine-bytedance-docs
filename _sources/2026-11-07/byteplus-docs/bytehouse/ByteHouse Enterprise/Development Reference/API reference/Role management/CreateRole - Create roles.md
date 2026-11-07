---
title: "CreateRole - Create roles"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/create-roles"
---

Create a role

<span id="0ea4ff2d"></span>
## Request parameters

This table only lists the request parameters specific to this interface, along with some common parameters. For more information, refer to [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Parameter | |Type |Required |Example Value |Description |
|---|---|---|---|---|---|
|Action | |String |Yes |CreateRole |The action to be performed: CreateRole. |
|Version | |String |Yes |2024\-08\-31 |The version of the API: 2024\-08\-31. |
|Name | |String |Yes |role1 |Role name |
|Description | |String |No |description |Description information |
|ClusterID | |Integer |Yes |123456 |Cluster ID |
|Users | |Array of Object |No |[<br><br>{<br><br>"Username": "user1",<br><br>"AdminOption": true<br><br>}<br><br>] |Grant User Information |
| |Username |String |No |user1 |Username |
| |AdminOption |Boolean |No |false |Grantable to other users |


<span id="c3a4a3fc"></span>
## Response parameters

This table only lists the response parameters specific to this interface. For more information, refer to [request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Parameter | | |Type |Sample value |Description |
|---|---|---|---|---|---|
|Message | | |String |None |Top response information |
|Data | | |Object |{<br><br>"Message": "create role successfully",<br><br>"Role": {<br><br>"ID": 123456,<br><br>"Name": "system_admin",<br><br>"Description": "MwrIZqDiy",<br><br>"IsDefault": false,<br><br>"ClusterID": 306,<br><br>"AccountID": 898,<br><br>"ClusterName": "cluster",<br><br>"GrantUsers": [],<br><br>"CreatedAt": 1721294525980,<br><br>"UpdatedAt": "1721294525980",<br><br>"CreatedBy": "dba",<br><br>"UpdatedBy": "dTa"<br><br>}<br><br>} |Return data |
| |Message | |String |create role successfully |Response message |
| |Role | |Object | |Role information |
| | |ID |Integer |123456 |Role primary key id |
| | |Description |String |description |Description information |
| | |IsDefault |Boolean |false |Is it a default system role? |
| | |Name |String |system_admin |Role name |
| | |ClusterID |Integer |123456 |Cluster ID associated with the role |
| | |AccountID |Integer |123456 |Tenant ID |
| | |ClusterName |String |cluster |Name of cluster associated with the role |
| | |CreatedAt |Integer |1721294525980 |Created at |
| | |UpdatedAt |Integer |1721294525980 |Last updated |
| | |CreatedBy |String |dba |Create Gamerole User |
| | |UpdatedBy |String |dba |Update the roles of users |
| | |GrantUsers |Array of String |["user1","user2"] |The user assigned roles (always returns an empty array in the CreateRole field) |


<span id="ea0a1723"></span>
## Request example

```text
POST /?Action=CreateRole&Version=2024-08-31 HTTP/1.1
Host: open.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20240912T142615Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240912/ap-southeast-1/bytehouse_ce/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "Name": "role1",
  "Description": "description",
  "ClusterID": 123456,
  "Users": [
    {
      "Username": "user1",
      "AdminOption": true
    }
  ]
}
```


<span id="f10e3e94"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "20240929142824215140052248F4D25D",
    "Action": "CreateRole",
    "Version": "2024-08-31",
    "Service": "bytehouse_ce",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Message": "",
    "Data": {
      "Message": "create role successfully",
      "Role": {
        "ID": 123456,
        "Description": "description",
        "IsDefault": true,
        "Name": "system_admin",
        "ClusterID": 123456,
        "AccountID": 123456,
        "ClusterName": "cluster",
        "CreatedAt": 1721294525980,
        "UpdatedAt": 1721294525980,
        "CreatedBy": "dba",
        "UpdatedBy": "dba",
        "GrantUsers": []
      }
    }
  }
}
```


<span id="0a052dba"></span>
## Error code

The table below lists the error codes related to this interface and business logic. For common error codes, refer to [common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Error Code |Error code |Error information |Description |
|---|---|---|---|
|400 |Bad Request |api service received invalid request format |Parameter error |
|400 |BadRequest |api service received invalid request format |Parameter error |
|401 |SignatureNotMatch |The request signature provided is incorrect. | |
|500 |InternalError |The request has failed due to an unknown error. | |
|503 |ServiceUnavailable |The request has failed due to a temporary failure of the server. | |
