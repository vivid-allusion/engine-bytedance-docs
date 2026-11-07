---
title: "ListKnowledgeBases - Batch queries knowledge base details"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/ListKnowledgeBases_-_Batch_queries_knowledge_base_details"
---

You can batch query knowledge base details using custom filter conditions.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string   </span>`Sample value: ListKnowledgeBases`

The action that you want to perform. Value: ListKnowledgeBases.



**Version ** <span data-label="purple">string   </span>`Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**CreateTimeAfter ** <span data-label="purple">string </span>`Optional Sample value: 2025-09-17T10:00:00+8:00`

Filter knowledge bases created after this time point. (RFC3339 format)



**CreateTimeBefore ** <span data-label="purple">string </span>`Optional Sample value: 2025-09-17T10:00:00+8:00`

Filter knowledge bases created before this time point. (RFC3339 format)



**Filters.N.Name ** <span data-label="purple">string[] </span>`Optional Sample value: name`

Field name used for exact filtering.


* Parameter \- N: Indicates the serial number of the filter condition. Value range: 1–10.

* Separate multiple field names with ampersands (&), representing an "Or" relationship.

* Value:

   * knowledge_id: Knowledge base ID.

   * name: Knowledge base name.

   * status: Knowledge base status.

   * provider_type: Type of the imported knowledge base platform.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When <code>Filters.N.Name</code> and <code>Filters.N.NameContains</code> are both passed in, only <code>Filters.N.Name</code> takes effect.</div>




**Filters.N.NameContains ** <span data-label="purple">string[] </span>`Optional Sample value: name`

Field name used for fuzzy filtering.


* Parameter \- N: Indicates the serial number of the filter condition. Value range: 1–10.

* Separate multiple field names with ampersands (&), representing an "Or" relationship.

* Value:

   * knowledge_id: Knowledge base ID.

   * name: Knowledge base name.

   * status: Knowledge base status.

   * provider_type: Type of the imported knowledge base platform.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When <code>Filters.N.Name</code> and <code>Filters.N.NameContains</code> are both passed in, only <code>Filters.N.Name</code> takes effect.</div>




**Filters.N.Values.N ** <span data-label="purple">string[] </span>`Optional Sample value: my_collection`

Value of the filter field.


* Parameter \- N: Indicates the serial number of the filter condition. Value range: 1–10.

* Separate multiple field names with ampersands (&).


When the filter field is provider_type, the value is:


* VIKINGDB_KNOWLEDGE: Viking knowledge base.



**MaxResults ** <span data-label="purple">integer </span>`Optional Sample value: 10`

The number of entries returned on each page in a pagination query.


* Minimum value: 1.

* Maximum value: 100.

* Default value: 10.



**NextToken ** <span data-label="purple">string </span>`Optional Sample value: unique-token`

Pagination token marking the query position. Omit this parameter for initial API requests. In the next query, set the `NextToken` parameter to the value returned by the previous API call.



**UpdateTimeAfter ** <span data-label="purple">string </span>`Optional Sample value: 2025-09-17T10:00:00+8:00`

Filter knowledge bases updated after this time point. (RFC3339 format)



**UpdateTimeBefore ** <span data-label="purple">string </span>`Optional Sample value: 2025-09-17T10:00:00+8:00`

Filter knowledge bases updated before this time point. (RFC3339 format)



**ProjectName ** <span data-label="purple">string </span>`Optional Sample value: default`

Project name.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**KnowledgeBases ** <span data-label="purple">object[] </span>`Sample value: --`

Information of knowledge bases that meet the requirements.


**AssociatedRuntimes ** <span data-label="purple">object[] </span>`Sample value: --`

Associated runtime information.


**Id ** <span data-label="purple">string </span>`Sample value: r-ye9tu7****`

ID of the runtime.



**Name ** <span data-label="purple">string </span>`Sample value: runtime-01`

Runtime name.




**NetworkConfiguration ** <span data-label="purple">object </span>`Sample value: --`

Access information for the runtime, including public network.


**EnablePublicNetwork ** <span data-label="purple">boolean </span>`Sample value: true`

Whether to enable public network access for the runtime. Value:


* true: Enable.

* false: Do not enable.




**ProjectName ** <span data-label="purple">string </span>`Sample value: default`

Name of the project associated with the runtime.



**Region ** <span data-label="purple">string </span>`Sample value: ap-southeast-1`

Region of the knowledge base.



**CreateTime ** <span data-label="purple">string </span>`Sample value: 2025-09-17T10:00:00+8:00`

Creation time of the knowledge base.



**Description ** <span data-label="purple">string </span>`Sample value: knowledge-test`

Description of the knowledge base.



**KnowledgeId ** <span data-label="purple">string </span>`Sample value: kb-4yds45****`

Knowledge base ID.



**LastUpdateTime ** <span data-label="purple">string </span>`Sample value: 2025-09-17T10:00:00+8:00`

Update time of the knowledge base.



**Name ** <span data-label="purple">string </span>`Sample value: my_collection`

Knowledge base name.



**ProviderKnowledgeId ** <span data-label="purple">string </span>`Sample value: kb-ye7s2g****`

ID of the imported knowledge base.



**ProviderType ** <span data-label="purple">string </span>`Sample value: VIKINGDB_KNOWLEDGE`

Type of the knowledge base platform. Value:


* VIKINGDB_KNOWLEDGE: Viking knowledge base.



**Status ** <span data-label="purple">string </span>`Sample value: Ready`

Knowledge base status. Value:


* Importing: Importing.

* ImportFailed: Importing failed.

* Ready: Succeeded.

* Deleting: It is being deleted.

* DeleteFailed: Deletion failed.

* Deleted: It is deleted.

* Error: Exception occurs.




**NextToken ** <span data-label="purple">string </span>`Sample value: bHpwdXJja2RxemU1eG5sb3NzdGcW1-RCEq******`

The query credentials value returned by this call. If null is returned, this page is the last page.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com?Action=ListKnowledgeBases&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
  "PageNumber": 1
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202106111445100102252431000052****",
        "Action": "ListKnowledgeBases",
        "Version": "2025-10-10",
        "Service": "agentkit",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "ListKnowledgeBasesResponseNextToken":{
        "KnowledgeBases": [
            {
                "KnowledgeId":"kb-1761138694808283000-1" ,
                "Name":"my_travel_knowledge" ,
                "ProviderKnowledgeId":"kb-travel-001" ,
                "ProviderType":"VIKINGDB_KNOWLEDGE" ,
                "Description":"knowledge-test" ,
                "Status":"Ready" ,
                "CreateTime":"2025-09-16T10:00:00Z" ,
                "LastUpdateTime":"2025-09-16T10:05:00Z"
            }
        ],
        "NextToken":"next-token"
        }
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |LimitExceeded.MaximumMaxResults |The number of specified MaxResults exceeds the maximum limit. |The value specified for MaxResults exceeds the upper limit. |
|400 |LimitExceeded.MaximumPageSize |The number of specified PageSize exceeds the maximum limit. |The specified PageSize exceeds the upper limit. |
