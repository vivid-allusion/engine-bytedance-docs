---
title: "AddSessionStore - Imports session resources"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/AddSessionStore_-_Imports_session_resources"
---

You can call this operation to import session resources. For operation instructions and precautions, refer to [Importing session resources](https://docs.byteplus.com/en/docs/agentkit/Importing_session_resources).

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|kBSrXc">必选</span> `Sample value: AddSessionStore`

The action that you want to perform. Value: AddSessionStore.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|OuyF4m">必选</span> `Sample value: 2025-10-30`

The API version. Value: 2025\-10\-30.



**DatabaseConfiguration.AccountName ** <span data-label="purple">string </span><span data-api-tag="require|dhtXxM">必选</span> `Sample value: user_admin`

Database account name.



**DatabaseConfiguration.Database ** <span data-label="purple">string </span><span data-api-tag="require|ppW48m">必选</span> `Sample value: mydb`

Database name.



**DatabaseConfiguration.EndpointConfiguration.EndpointId ** <span data-label="purple">string </span><span data-api-tag="require|mzBBBk">必选</span> `Sample value: ep-15d73b055d662534****`

Endpoint ID.


* RDS_MYSQL: EndpointId.

* RDS_PG: EndpointId.



**DatabaseConfiguration.InstanceId ** <span data-label="purple">string </span><span data-api-tag="require|SjwY1X">必选</span> `Sample value: cp-sound-flash-37ae****`

Database instance ID.


* RDS_MYSQL: InstanceId. For example, "mysql\-33f0bf03\*\*\*\*".

* RDS_PG: InstanceId. For example, "postgres\-8a4cf530\*\*\*\*".



**Description ** <span data-label="purple">string </span>`Optional` `Sample value: my session store`

Session resource description.


* The text length is 0\-200 Unicode characters.



**Name ** <span data-label="purple">string </span>`Optional` `Sample value: my_session_store`

Session resource name.


* Consists of letters, numbers, hyphens (\-), and underscores (_).

* The length is 2–48 characters.



**ProjectName ** <span data-label="purple">string </span>`Optional` `Sample value: default`

The name of the associated project.



**ProviderType ** <span data-label="purple">string </span>`Optional` `Sample value: RDS_PG`

Underlying storage type. Valid values:


* RDS_MYSQL: Relational MySQL, that is, RDS for MySQL.

* RDS_PG: Relational PostgreSQL, that is, RDS for PostgreSQL.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Description ** <span data-label="purple">string </span>`Sample value: sample description`

Session resource description.



**Name ** <span data-label="purple">string </span>`Sample value: my_session_store`

Session resource name.



**ProviderType ** <span data-label="purple">string </span>`Sample value: RDS_PG`

Underlying storage type.


* RDS_MYSQL: Relational MySQL, that is, RDS for MySQL.

* RDS_PG: Relational PostgreSQL, that is, RDS for PostgreSQL.



**SessionStoreId ** <span data-label="purple">string </span>`Sample value: ss-yefjbwgpa8c1kdto****`

Session resource ID.



**Status ** <span data-label="purple">string </span>`Sample value: Ready`

Session library status, including:


* Creating: Being created.

* CreateFailed: Creation failed.

* Ready: Available for use.

* Deleting: Being deleted.

* DeleteFailed: Deletion failed.

* Deleted: Resource expired.

* Error: An error occurred.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=AddSessionStore&Version=2025-10-30 HTTP/1.1
Content-Type: application/json; charset=UTF-8
{
  "Name": "my_agent_session",
  "Description": "sample description",
  "ProviderType": "RDS_PG",
  "DatabaseConfiguration": {
    "InstanceId": "pg-***",
    "EndpointConfiguration": {
      "EndpointId": "ep-***"
    },
    "Database": "mydb",
    "AccountName": "admin"
  }
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20251125162502098132110105524B2F",
    "Action": "AddSessionStore",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "SessionStoreId": "ss-123",
    "ProviderType": "RDS_PG",
    "Status": "Ready"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The format of the specified description is invalid. |
|400 |InvalidName.Malformed |The specified Name is malformed. |The specified Name is invalid. |
|400 |InvalidProjectName.Malformed |The specified ProjectName is malformed. |The specified ProjectName is invalid. |
|400 |MissingParameter.AccountName |The required parameter AccountName is not supplied. |The AccountName parameter cannot be empty. |
|400 |MissingParameter.Database |The required parameter Database is not supplied. |The Database parameter cannot be empty. |
|400 |MissingParameter.DatabaseConfiguration |The required parameter DatabaseConfiguration is not supplied. |The DatabaseConfiguration parameter cannot be empty. |
|400 |MissingParameter.EndpointId |The required parameter EndpointId is not supplied. |The EndpointId parameter cannot be empty. |
|400 |MissingParameter.InstanceId |The required parameter InstanceId is not supplied. |The instance_id cannot be empty. |
