---
title: "GetSessionStore - Queries session resource details"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/GetSessionStore_-_Queries_session_resource_details"
---

You can call this operation to query details of a session resource.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|c8Te5P">必选</span> `Sample value: GetSessionStore`

The action that you want to perform. Value: GetSessionStore.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|Z5TDGa">必选</span> `Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**SessionStoreId ** <span data-label="purple">string </span><span data-api-tag="require|GhzIgN">必选</span> `Sample value: ss-yefjbwgpa8c1kdto****`

Session resource ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**AssociatedAgents ** <span data-label="purple">object[] </span>`Sample value: --`

Information about the associated agent.


**Id ** <span data-label="purple">string </span>`Sample value: r-yefiu7g5q8c1kdto****`

ID of the runtime.



**Name ** <span data-label="purple">string </span>`Sample value: my_agent`

Runtime name.



**UpdateTime ** <span data-label="purple">string </span>`Sample value: 2025-09-17T10:00:00+8:00`

Association time. （RFC3339）




**CreateTime ** <span data-label="purple">string </span>`Sample value: 2026-02-11T10:00:00+8:00`

Creation time of the session resource. (RFC3339)



**DatabaseConfiguration ** <span data-label="purple">object </span>`Sample value: --`

Database configuration information.


**AccountName ** <span data-label="purple">string </span>`Sample value: user_admin`

Database account name.



**Database ** <span data-label="purple">string </span>`Sample value: mydb`

Database name.



**EndpointConfiguration ** <span data-label="purple">object </span>`Sample value: --`

Configuration information about the database attachment point.


**EndpointId ** <span data-label="purple">string </span>`Sample value: mysql-6284d149****-cluster`

Attachment point ID.


* RDS_MYSQL: EndpointId.

* RDS_PG: EndpointId.



**PrivateEndpoint ** <span data-label="purple">string </span>`Sample value: mysql33f0bf03*****.rds.ivolces.com:3306`

Private network connection address.



**PublicEndpoint ** <span data-label="purple">string </span>`Sample value: mysql-33f0bf03****-public.rds.volces.com:3306`

Public network connection address.




**InstanceId ** <span data-label="purple">string </span>`Sample value: mysql-33f0bf03****`

Database instance ID.


* RDS_MYSQL: InstanceId. For example, "mysql\-33f0bf03\*\*\*\*".

* RDS_PG: InstanceId. For example, "postgres\-8a4cf530\*\*\*\*".




**Description ** <span data-label="purple">string </span>`Sample value: sample description`

Session resource description.



**Managed ** <span data-label="purple">boolean </span>`Sample value: true`

Whether it is managed by the platform.



**Name ** <span data-label="purple">string </span>`Sample value: my_session_store`

Session resource name.



**ProjectName ** <span data-label="purple">string </span>`Sample value: default`

Name of the associated project.



**ProviderType ** <span data-label="purple">string </span>`Sample value: RDS_PG`

Underlying storage type.


* RDS_MYSQL: Relational MySQL, that is, RDS for MySQL.

* RDS_PG: Relational PostgreSQL, that is, RDS for PostgreSQL.



**SessionStoreId ** <span data-label="purple">string </span>`Sample value: ss-yefjbwgpa8c1kdto****`

Session resource ID.



**Status ** <span data-label="purple">string </span>`Sample value: Ready`

Session library status. Values:


* Creating: Being created.

* CreateFailed: Creation failed.

* Ready: Available for use.

* Deleting: Being deleted.

* DeleteFailed: Deletion failed.

* Deleted: Resource expired.

* Error: Error.



**Trn ** <span data-label="purple">string </span>`Sample value: trn:appo:SessionStore:cn-beijing:123456:sessionstore/ss-yefjbwgpa8c1kdto****`

Resource TRN.



**UpdateTime ** <span data-label="purple">string </span>`Sample value: 2026-02-11T18:00:00+8:00`

Update time of the session resource. (RFC3339)



**VpcId ** <span data-label="purple">string </span>`Sample value: vpc-257gqcdfvx6n****`

VPC ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=GetSessionStore&Version=2025-10-30 HTTP/1.1
Content-Type: application/json; charset=UTF-8
{
  "SessionStoreId": "ss-yefjbwgpa8c1kdto****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20251125162502098132110105524B2F",
    "Action": "GetSessionStore",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
  "SessionStoreId": "ss-yefjbwgpa8c1kdto****",
  "Name": "my_session_store",
  "Description": "sample description",
  "Trn": "trn:appo:SessionStore:cn-beijing:123456:sessionstore/ss-yefjbwgpa8c1kdto****",
  "DatabaseConfiguration": {
    "InstanceId": "mysql-33f0bf03****",
    "EndpointConfiguration": {
      "EndpointId": "mysql-6284d149****-cluster",
      "PublicEndpoint": "mysql-33f0bf03****-public.rds.volces.com:3306",
      "PrivateEndpoint": "mysql33f0bf03*****.rds.ivolces.com:3306"
    },
    "Database": "mydb",
    "AccountName": "user_admin"
  },
  "ProviderType": "RDS_MYSQL",
  "Status": "Ready",
  "CreateTime": "2026-02-11T10:00:00+8:00"
}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.SessionStoreId |The required parameter SessionStoreId is not supplied. |The parameter SessionStoreId cannot be empty. |
