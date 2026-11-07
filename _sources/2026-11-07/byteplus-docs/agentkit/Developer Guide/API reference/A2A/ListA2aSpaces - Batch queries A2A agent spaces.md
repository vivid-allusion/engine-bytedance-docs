---
title: "ListA2aSpaces - Batch queries A2A agent spaces"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/ListA2aSpaces_-_Batch_queries_A2A_agent_spaces"
---

Batch query A2A agent spaces.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|E59MjR">必选</span> `Sample value: ListA2aSpaces`

The operation that you want to perform. Value: ListA2aSpaces.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|RF2x5t">必选</span> `Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**PageNumber ** <span data-label="purple">integer </span>`Optional Sample value: 1`

The current page number.


* Starting value: 1.

* Default value: 1.



**PageSize**<span data-label="purple"> integer </span>`Optional Sample value: 10`

The number of entries returned on each page in a pagination query.


* Value range: 1–100.

* Default value: 10.



**ProjectName ** <span data-label="purple">string </span>`Optional` `Sample value: default`

The name of the associated project.



**TagFilters ** <span data-label="purple">object[] </span>`Optional` `Sample value: --`

The tag filters.


**Key ** <span data-label="purple">string </span><span data-api-tag="require|25gqBZ">必选</span> `Sample value: Key1`

The key of the A2A agent tag.



**Values ** <span data-label="purple">string[] </span><span data-api-tag="require|I3ibrU">必选</span> `Sample value: -`

The value of the A2A agent tag.




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**TotalCount ** <span data-label="purple">integer </span>`Sample value: 1`

The total number of A2A agent spaces that meet the conditions.



**Items ** <span data-label="purple">object[] </span>`Sample value: --`

The A2A agent spaces.


**Id ** <span data-label="purple">string </span>`Sample value: as-yeglyhjytc3srhse****`

The ID of the A2A agent space.



**Name ** <span data-label="purple">string </span>`Sample value: space`

The name of the A2A agent space.



**IntentEnabled ** <span data-label="purple">boolean </span>`Sample value: true`

Whether semantic retrieval is enabled for the A2A agent space. After this feature is enabled, the best\-matching agent in the space is returned based on the natural language of the calling intent.


* true: Enabled.

* false: Disabled.



**ProjectName ** <span data-label="purple">string </span>`Sample value: default`

The name of the project associated with the A2A agent space.



**Tags ** <span data-label="purple">object[] </span>`Sample value: --`

The tag of the A2A agent space.


**Key ** <span data-label="purple">string </span>`Sample value: Key1`

The key of the A2A agent tag.



**Value ** <span data-label="purple">string </span>`Sample value: Value1`

The value of the A2A agent tag.




**IsDefault ** <span data-label="purple">boolean </span>`Sample value: false`

Whether it is specified as the default A2A agent space. When you register an A2A agent, if no A2A agent space is specified, the agent is registered to the default A2A agent space.


* true: Specified as the default space.

* false: Not specified as the default space.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST /?Action=ListA2aSpaces&Version=2025-10-30 HTTP/1.1
Host: agentkit.ap-southeast-1.byteplusapi.com.cn
Content-Type: application/json; charset=UTF-8
X-Date: 20260309T121141Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260309/ap-southeast-1/agentkit/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "PageNumber": 1,
  "PageSize": 10,
  "ProjectName": "default",
  "TagFilters": [
    {
      "Key": "Key1",
      "Values": [
        "-"
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
    "RequestId": "2026030920115504608518910986****",
    "Action": "ListA2aSpaces",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "TotalCount": 1,
    "Items": [
      {
        "Id": "as-yeglyhjytc3srhse****",
        "Name": "space",
        "IntentEnabled": true,
        "ProjectName": "default",
        "Tags": [
          {
            "Key": "Key1",
            "Value": "Value1"
          }
        ],
        "IsDefault": true
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
|403 |AccessDenied |You are not authorized to perform this action. |You do not have permission to perform this operation. |
|500 |InternalError |The request has failed due to an unknown error. |Internal error. |
