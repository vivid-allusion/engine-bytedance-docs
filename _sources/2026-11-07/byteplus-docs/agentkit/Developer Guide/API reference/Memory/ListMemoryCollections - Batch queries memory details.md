---
title: "ListMemoryCollections - Batch queries memory details"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/ListMemoryCollections_-_Batch_queries_memory_details"
---

You can batch query memory details using custom filter conditions.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|pVJk3W">必选</span> `Sample value: ListMemoryCollections`

The action that you want to perform. Value: ListMemoryCollections.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|n59rCF">必选</span> `Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**CreateTimeAfter ** <span data-label="purple">string</span>` Optional Sample value: 2025-09-17T10:00:00+8:00`

Filter memories created after this time point. (RFC3339 format)



**CreateTimeBefore ** <span data-label="purple">string </span>`Optional Sample value: 2025-09-17T10:00:00+8:00`

Filter memories created before this time point. (RFC3339 format)



**Filters.N.Name**<span data-label="purple"> string[] </span>`Optional Sample value: name`

Field name used for exact filtering.


* Parameter \- N: Indicates the serial number of the filter condition. Value range: 1–10.

* Separate multiple field names with ampersands (&), representing an "Or" relationship.

* Value:

   * collection_id: Memory ID.

   * name: Memory name.

   * description: Memory description.

   * status: Memory status.

   * provider_type: Type of the imported knowledge base platform.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When <code>Filters.N.Name</code> and <code>Filters.N.NameContains</code> are both passed in, only <code>Filters.N.Name</code> takes effect.</div>




**Filters.N.NameContains**<span data-label="purple"> string[] </span>`Optional Sample value: name`

Field name used for fuzzy filtering.


* Parameter \- N: Indicates the serial number of the filter condition. Value range: 1–10.

* Separate multiple field names with ampersands (&), representing an "Or" relationship.

* Value:

   * collection_id: Memory ID.

   * name: Memory name.

   * description: Memory description.

   * status: Memory status.

   * provider_type: Type of the imported knowledge base platform.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When <code>Filters.N.Name</code> and <code>Filters.N.NameContains</code> are both passed in, only <code>Filters.N.Name</code> takes effect.</div>




**Filters.N.Values.N ** <span data-label="purple">string[] </span>`Optional Sample value: my_memory`

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


* VIKINGDB_MEMORY: Viking LTM.



**MaxResults ** <span data-label="purple">integer </span>`Optional Sample value: 10`

The number of entries returned on each page in a pagination query.


* Minimum value: 1.

* Maximum value: 100. 

* Default value: 10.



**NextToken ** <span data-label="purple">string </span>`Optional Sample value: unique-token`

Pagination token marking the query position. Omit this parameter for initial API requests. In the next query, set the `NextToken` parameter to the value returned by the previous API call.



**UpdateTimeAfter**<span data-label="purple"> string</span>` Optional Sample value: 2025-09-17T10:00:00+8:00`

Filter memories updated after this time point. (RFC3339 format)



**UpdateTimeBefore**<span data-label="purple"> string </span>`Optional Sample value: 2025-09-17T10:00:00+8:00`

Filter memories updated before this time point. (RFC3339 format)



**ProjectName ** <span data-label="purple">string </span>`Optional` `Sample value: default`

Name of the associated project.



**TagFilters.N.Key ** <span data-label="purple">string[] </span>`Optional` `Sample value: TagFilters.1.Key=k1`

Tag key specified when querying resources by tag. Each tag key must be unique.


* Parameter\- N: specifies the serial number of the tag key. Valid range: 1–10.

* Separate multiple tag keys with ampersands (&).



**TagFilters.N.Values.N ** <span data-label="purple">string[]</span>` Optional Sample value: TagFilters.1.Values.1=v1`

The tag value specified when resources are queried based on tags.


* The first N: the serial number of the tag key. Value range: 1–10.

* The second N: the serial number of the tag value. Value range: 1–3. You can query up to three tag values of the same tag key.

* Separate multiple tag values with ampersands (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">To pass in this parameter, you need to pass in TagFilters.N.Key first.</div>


* <div data-tips="true" data-tips-type="tip">If you do not pass in this parameter, all tag values under the same tag key are queried.</div>


* <div data-tips="true" data-tips-type="tip">If you specify an empty string, you query tags with an empty tag value.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Memories ** <span data-label="purple">object[] </span>`Sample value: --`

Information of the memories that meet the conditions.


**AssociatedRuntimes ** <span data-label="purple">object[] </span>`Sample value: --`

List of associated runtimes.


**Id ** <span data-label="purple">string </span>`Sample value: r-ye9tu7****`

ID of the runtime.



**Name ** <span data-label="purple">string </span>`Sample value: runtime-01`

Runtime name.




**CreateTime ** <span data-label="purple">string </span>`Sample value: 2025-09-17T10:00:00+8:00`

Creation time of the memory.



**Description ** <span data-label="purple">string </span>`Sample value: memory-test`

Description of the memory.



**LastUpdateTime ** <span data-label="purple">string </span>`Sample value: 2025-09-17T10:00:00+8:00`

Memory update time.



**Managed ** <span data-label="purple">boolean </span>`Sample value: true`

Whether the memory is managed by the AgentKit platform. Value: 


* true: Indicates that the memory is created by the AgentKit platform. When the memory is deleted, the corresponding platform resources are also deleted.

* false: Indicates that the memory is imported from the provider platform. When the memory is deleted, the corresponding platform resources are retained.



**MemoryId ** <span data-label="purple">string </span>`Sample value: viking-176113869****`

Memory ID.



**Name ** <span data-label="purple">string </span>`Sample value: my_memory`

Memory name.



**NetworkConfiguration ** <span data-label="purple">object </span>`Sample value: --`

Network configuration.


**EnablePrivateNetwork ** <span data-label="purple">boolean </span>`Sample value: false`

Whether to enable private network access for the runtime. Value:


* true: Enabled.

* false: Disabled.



**EnablePublicNetwork ** <span data-label="purple">boolean </span>`Sample value: true`

Whether to enable public network access for the runtime. Value:


* true: Enabled.

* false: Disabled.



**VpcConfiguration ** <span data-label="purple">object </span>`Sample value: --`

VPC configuration.


**SecurityGroupIds ** <span data-label="purple">string[] </span>`Sample value: ["sg-w08tvkc3e****"]`

List of security group IDs.



**SubnetIds ** <span data-label="purple">string[] </span>`Sample value: ["subnet-1234567890"]`

List of subnet IDs.



**VpcId ** <span data-label="purple">string </span>`Sample value: vpc-257gqcdfvx6n****`

VPC ID.





**ProjectName ** <span data-label="purple">string </span>`Sample value: default`

Name of the associated project.



**ProviderCollectionId ** <span data-label="purple">string </span>`Sample value: mem-294775****`

ID of the imported memory.



**ProviderType ** <span data-label="purple">string </span>`Sample value: VIKINGDB_MEMORY`

Memory type. Value:


* VIKINGDB_MEMORY: Viking LTM.



**Region ** <span data-label="purple">string </span>`Sample value: ap-southeast-1`

The region.



**Status ** <span data-label="purple">string </span>`Sample value: Ready`

Memory status. Value:


* Creating: Being created.

* CreateFailed: Creation failed.

* Ready: Available for use.

* Deleting: Being deleted.

* DeleteFailed: Deletion failed.

* Deleted: Deleted.

* Error: Error.



**StrategiesCount ** <span data-label="purple">integer </span>`Sample value: 3`

Total strategy count of the memory.



**Tags ** <span data-label="purple">object[] </span>`Sample value: --`

Memory tags.


**Type ** <span data-label="purple">string </span>`Sample value: custom`

Tag type.


* system: System tag

* custom: User tag



**Key ** <span data-label="purple">string </span>`Sample value: k1`

The tag key.



**Value ** <span data-label="purple">string </span>`Sample value: v1`

The tag value.





**NextToken ** <span data-label="purple">string </span>`Sample value: bHpwdXJja2RxemU1eG5sb3NzdGcW1-RCEq******`

The query credentials value returned by this call. If null is returned, this page is the last page.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com?Action=ListMemoryCollections&Version=2025-10-30 HTTP/1.1
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
    "Action": "ListMemoryCollections",
    "Version": "2025-10-10",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "ListMemoryCollectionsResponseNextToken": {
      "Memories": [
        {
          "MemoryId": "viking-176113869****",
          "ProviderCollectionId": "viking-176113869****",
          "ProviderType": "VIKINGDB_MEMORY",
          "Description": "memory-test",
          "Status": "Ready",
          "CreateTime": "2025-09-16T10:00:00Z",
          "LastUpdateTime": "2025-09-16T10:05:00Z",
          "Name": "my_agent_memory",
          "Managed": "true",
          "StrategiesCount": "3"
        }
      ],
      "NextToken": "eyJwYWdlIjoyL****"
    }
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidProjectName.Malformed |The specified ProjectName is malformed. |The specified ProjectName is invalid. |
|400 |LimitExceeded.MaximumFilters |The number of specified Filters exceeds the maximum limit. |The specified Filters exceeds the upper limit. |
|400 |LimitExceeded.MaximumMaxResults |The number of specified MaxResults exceeds the maximum limit. |The value specified for MaxResults exceeds the upper limit. |
|400 |LimitExceeded.MaximumPageSize |The number of specified PageSize exceeds the maximum limit. |The specified PageSize exceeds the upper limit. |
