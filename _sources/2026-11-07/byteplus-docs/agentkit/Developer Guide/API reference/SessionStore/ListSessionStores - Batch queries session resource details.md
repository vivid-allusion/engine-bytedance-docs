---
title: "ListSessionStores - Batch queries session resource details"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/ListSessionStores_-_Batch_queries_session_resource_details"
---

You can batch query session resource details using custom filter conditions.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|aJ8NKZ">必选</span> `Sample value: ListSessionStores`

The action that you want to perform. Value: ListSessionStores.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|1NyedF">必选</span> `Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**CreateTimeAfter ** <span data-label="purple">string </span>`Optional` `Sample value: 2026-02-11T20:00:47+8:00`

Filter session resources created after this time point. (RFC3339 format)



**CreateTimeBefore ** <span data-label="purple">string </span>`Optional` `Sample value: 2026-02-11T10:05:37+8:00`

Filter session resources created before this time point. (RFC3339 format)



**Filters.N.Name ** <span data-label="purple">string[] </span>`Optional` `Sample value: status`

Field name used for exact filtering.


* Parameter \- N: Indicates the serial number of the filter condition. Value range: 1–10.

* Separate multiple field names with ampersands (&), representing an "Or" relationship.

* Value:

   * session_store_id: Session resource ID.

   * name: Session resource name.

   * status: Session resource status.

   * provider_type: Platform type of the imported session resource.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When <code>Filters.N.Name</code> and <code>Filters.N.NameContains</code> are both passed in, only <code>Filters.N.Name</code> takes effect.</div>




**Filters.N.NameContains ** <span data-label="purple">string[] </span>`Optional` `Sample value: sample description`

Field name used for fuzzy filtering.


* Parameter \- N: Indicates the serial number of the filter condition. Value range: 1–10.

* Separate multiple field names with ampersands (&), representing an "Or" relationship.

* Value:

   * name: Session resource name.

   * description: Session resource description.

   * provider_type: Platform type of the imported session resource.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When <code>Filters.N.Name</code> and <code>Filters.N.NameContains</code> are both passed in, only <code>Filters.N.Name</code> takes effect.</div>




**Filters.N.Values.N ** <span data-label="purple">string[]</span>` Optional Sample value: Ready`

Value of the filter field.


* Parameter \- N: Indicates the serial number of the filter condition. Value range: 1–10.

* Separate multiple field names with ampersands (&).


When the filter condition is status, the values are:


* Creating: Being created.

* CreateFailed: Creation failed.

* Ready: Available for use.

* Deleting: Being deleted.

* DeleteFailed: Deletion failed.

* Deleted: Resource expired.

* Error: Error.


When the filter condition is provider_type, the values are:


* RDS_MYSQL: Cloud database MySQL.

* RDS_PG: Cloud database PostgreSQL.



**MaxResults ** <span data-label="purple">integer </span>`Optional Sample value: 10`

The number of entries returned on each page in a pagination query.


* Minimum value: 1.

* Maximum value: 100. 

* Default value: 10.



**NextToken ** <span data-label="purple">string </span>`Optional Sample value: bS15ZTcwMjZiaWY0cTdvaTVjc3****==`

Pagination token marking the query position. Omit this parameter for initial API requests. In the next query, set the `NextToken` parameter to the value returned by the previous API call.



**PageNumber ** <span data-label="purple">integer </span>`Optional Sample value: 1`

The current page number.


* Starting value: 1.

* Default value: 1



**PageSize**<span data-label="purple"> integer </span>`Optional Sample value: 10`

The number of entries returned on each page in a pagination query.


* Value range: 1–100.

* Default value: 10.



**ProjectName ** <span data-label="purple">string </span>`Optional` `Sample value: default`

Name of the associated project.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageNumber ** <span data-label="purple">integer </span>`Sample value: 1`

The current page number.


* Starting value: 1.

* Default value: 1



**PageSize ** <span data-label="purple">integer </span>`Sample value: 10`

The number of entries returned on each page in a pagination query.


* Value range: 1–100.

* Default value: 10.



**SessionStores ** <span data-label="purple">object[] </span>`Sample value: --`

Session resource information.


**AssociatedAgentsCount ** <span data-label="purple">integer </span>`Sample value: 1`

Number of associated agents.



**CreateTime ** <span data-label="purple">string </span>`Sample value: 2026-02-10T10:00:00+8:00`

Creation time of the session resource. （RFC3339）



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




**Description ** <span data-label="purple">string </span>`Sample value: my session store`

Session resource description.



**Managed ** <span data-label="purple">boolean </span>`Sample value: true`

Whether it is managed by the platform.



**Name ** <span data-label="purple">string </span>`Sample value: my_session_store`

Session resource name.



**ProjectName ** <span data-label="purple">string </span>`Sample value: default`

Name of the associated project.



**ProviderType ** <span data-label="purple">string </span>`Sample value: RDS_MYSQL`

Underlying storage type. Including:


* RDS_MYSQL: Cloud database MySQL.

* RDS_PG: Cloud database PostgreSQL.



**SessionStoreId ** <span data-label="purple">string </span>`Sample value: ss-****`

Session resource ID.



**Status ** <span data-label="purple">string </span>`Sample value: Ready`

Session library status, including:


* Creating: Being created.

* CreateFailed: Creation failed.

* Ready: Available for use.

* Deleting: Being deleted.

* DeleteFailed: Deletion failed.

* Deleted: Resource expired.

* Error: Error.



**UpdateTime ** <span data-label="purple">string </span>`Sample value: 2026-02-11T18:00:00+8:00`

Update time of the session resource. （RFC3339）



**VpcId ** <span data-label="purple">string </span>`Sample value: vpc-****`

VPC ID.




**TotalCount ** <span data-label="purple">integer </span>`Sample value: 1`

Total number of session resources that meet the conditions.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=ListSessionStores&Version=2025-10-30 HTTP/1.1
Content-Type: application/json; charset=UTF-8
{
  "PageSize": 10,
  "PageNumber": 1,
  "CreateTimeAfter": "2025-09-01T00:00:00Z",
  "Filters": [
    {
      "Name": "name",
      "NameContains": "agent"
    },
    {
      "Name": "status",
      "Values": [
        "Ready"
      ]
    },
    {
      "Name": "provider_type",
      "Values": [
        "SERVERLESS_PG"
      ]
    }
  ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20251125162502098132110105524B2F",
    "Action": "ListSessionStores",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
  "MaxResults": 20,
  "NextToken": "eyJwYWdlIjoyLCJzaXplIjoxMH0",
  "Filters": [
    {
      "Name": "status",
      "Values": [
        "Ready",
        "Deleted"
      ]
    }
  ]
}
}

```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidProjectName.Malformed |The specified ProjectName is malformed. |The specified ProjectName is invalid. |
