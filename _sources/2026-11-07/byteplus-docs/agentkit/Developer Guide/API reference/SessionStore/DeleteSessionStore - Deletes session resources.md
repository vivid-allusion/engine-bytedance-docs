---
title: "DeleteSessionStore - Deletes session resources"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/DeleteSessionStore_-_Deletes_session_resources"
---

You can call this operation to delete session resources.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|AM9Nat">必选</span> `Sample value: DeleteSessionStore`

The action that you want to perform. Value: DeleteSessionStore.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|yFWdIp">必选</span> `Sample value: 2025-10-30`

The API version. Value: 2025\-10\-30.



**SessionStoreId ** <span data-label="purple">string </span><span data-api-tag="require|IppmUf">必选</span> `Sample value: ss-yefjbwgpa8c1kdto****`

Session resource ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



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

* Error: An error occurred.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=DeleteSessionStore&Version=2025-10-30 HTTP/1.1
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
    "Action": "DeleteSessionStore",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
  "SessionStoreId": "ss-yefjbwgpa8c1kdto****",
  "ProviderType": "RDS_PG"
}
}

```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.SessionStoreId |The required parameter SessionStoreId is not supplied. |The parameter SessionStoreId cannot be empty. |
