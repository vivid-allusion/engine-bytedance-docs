---
title: "ListRoles - Role list"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/list-roles"
---

Retrieve role lists.

<span id="37d3c28c"></span>
## Request parameters

The table below lists only the request parameters specific to this interface and some common parameters. For more information, refer to [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListRoles |The operation to perform: ListRoles. |
|Version |String |Yes |2024\-08\-31 |The version of the API: 2024\-08\-31. |
|ClusterID |Integer |No |12345 |Cluster ID |
|Name |String |No |system_admin |Role Name |


<span id="0f575212"></span>
## Response parameters

The table below lists only the response parameters specific to this interface. For more information, refer to [request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Parameter | | |Type |Example value |Description |
|---|---|---|---|---|---|
|Message | | |String |None |Top response information |
|Data | | |Object |{<br><br>"Roles": [<br><br>{<br><br>"ID": 123456,<br><br>"Name": "system_admin",<br><br>"Description": "dAGXkve",<br><br>"IsDefault": false,<br><br>"ClusterID": 691,<br><br>"AccountID": 333,<br><br>"ClusterName": "cluster",<br><br>"GrantUsers": [<br><br>"user1"<br><br>],<br><br>"CreatedAt": 1721294525980,<br><br>"UpdatedAt": "1721294525980",<br><br>"CreatedBy": "dba",<br><br>"UpdatedBy": "x"<br><br>}<br><br>]<br><br>} |Return data |
| |Roles | |Array of Object | |Role list |
| | |ID |Integer |123456 |Role Primary Key ID |
| | |Description |String |description |Description Information |
| | |IsDefault |Boolean |false |Is Default System Role |
| | |Name |String |system_admin |Role Name |
| | |ClusterID |Integer |123456 |Cluster ID Associated with Role |
| | |AccountID |Integer |123456 |Tenant ID |
| | |ClusterName |String |cluster |Cluster Name Associated with the Role |
| | |CreatedAt |Integer |1721294525980 |Creation Time |
| | |UpdatedAt |Integer |1721294525980 |Update Time |
| | |CreatedBy |String |dba |User Creating the Role |
| | |UpdatedBy |String |dba |Update User Roles |
| | |GrantUsers |Array of String |["user1","user2"] |User granted roles (In the CreateRole interface, this field always returns an empty array) |


<span id="5b0063eb"></span>
## Request example

```text
GET /?Action=ListRoles&Version=2024-08-31&ClusterID=12345&Name=system_admin HTTP/1.1
Host: open.byteplusapi.com
X-Date: 20240929T034043Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240929/ap-southeast-1/bytehouse_ce/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

```


<span id="8dcfffce"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "202409291140510830222400585D1BFF",
    "Action": "ListRoles",
    "Version": "2024-08-31",
    "Service": "bytehouse_ce",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Message": "",
    "Data": {
      "Roles": [
        {
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
          "GrantUsers": [
            "user1","user2"
          ]
        }
      ]
    }
  }
}
```


<span id="048a815b"></span>
## Error code

The table below lists error codes related to this interface and business logic. For common error codes, refer to [common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error code |Error information |Description |
|---|---|---|---|
|400 |Bad Request |api service received invalid request format |Parameter error |
|401 |SignatureNotMatch |The request signature provided is incorrect. | |
|500 |InternalError |The request has failed due to an unknown error. | |
|503 |ServiceUnavailable |The request has failed due to a temporary failure of the server. | |
