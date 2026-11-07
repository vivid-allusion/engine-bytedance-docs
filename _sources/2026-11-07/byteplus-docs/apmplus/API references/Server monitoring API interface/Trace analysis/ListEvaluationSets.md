---
title: "ListEvaluationSets"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/ListEvaluationSets"
---

Obtains the list of evaluation sets for the specified evaluation platform type and workspace.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

Server\-side Monitoring has been deployed in multiple regions around the world to provide you with a more stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-server.cn\-beijing.byteplusapi.com.cn?Action=ListEvaluationSets&Version=2024\-07\-30


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For details, see [Common parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListEvaluationSets |The API name. The current API name is `ListEvaluationSets`. |
|Version |String |Yes |2024\-07\-30 |The API version. The current API version is `2024-07-30`. |
|ExportTarget |Integer |Yes |2 |Export target. Values:<br><br><br>* **2**: AgentKit evaluation<br><br>* **3**: DataFinder evaluation |
|WorkspaceId |String |Yes |ws\-12345 |Workspace ID of evaluation platform. |
|Filter |Object of [ListEvaluationSetsRequestFilter](https://docs.byteplus.com/en/docs/299/115796#listevaluationsetsrequestfilter) |No |{"Name":"Trace"} |Evaluation set filter criteria. |
|CozeToken |String |No |pat_xxx |Authorization token for accessing CozeLoop.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when querying <code>CozeLoop</code>.</div><br> |


<span id="listevaluationsetsrequestfilter"></span>
### ListEvaluationSetsRequestFilter


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Name |String |No |Trace |Evaluation set name filter criteria. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-server.cn-beijing.byteplusapi.com.cn?Action=ListEvaluationSets&Version=2024-07-30
{
    "ExportTarget": 2,
    "WorkspaceId": "ws-12345",
    "Filter": {
        "Name": "Trace"
    },
    "CozeToken": "pat_xxx"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**type** |**Sample value** |**Description** |
|---|---|---|---|
|Items |Array of [EvaluationSet](https://docs.byteplus.com/en/docs/299/115796#evaluationset) |[{"ID":"eval\-set\-67890","Name":"Trace Evaluation Set","Description":"Evaluation set for Trace data","Fields":[]}] |Evaluation set list. |
|TotalCount |Long |1 |Total number of evaluation sets. |


<span id="evaluationset"></span>
### EvaluationSet


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|ID |String |eval\-set\-67890 |Evaluation set ID. |
|Name |String |Trace Evaluation Set |Evaluation set name. |
|Fields |Array of [FieldSchema](https://docs.byteplus.com/en/docs/299/115796#fieldschema) |[{"Name":"trace_id","Description":"Trace ID","ContentType":"Text","IsRequired":true}] |Field structure list of the evaluation set. |
|Description |String |Evaluation set for Trace data |Evaluation set description. |


<span id="fieldschema"></span>
### FieldSchema


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Name |String |trace_id |Field name. |
|IsRequired |Boolean |true |Whether the field is required. |
|TextSchema |String |{"type":"string"} |JSON Schema definition for text fields. |
|ContentType |String |Text |Field content type. |
|Description |String |Trace ID |Field description. |
|DefaultDisplayFormat |String |plain_text |Default display format for fields. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "Result": {
        "Items": [],
        "TotalCount": 0
    },
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListEvaluationSets",
        "Version": "2024-07-30",
        "Service": "apmplus_server",
        "Region": "cn-north-1"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

If the API call returns an exception, you can troubleshoot by referring to the API error codes and the [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) below.


|**HTTP status codes** |**Error codes** |**Error messages** |**Description** |
|---|---|---|---|
|500 |ErrInternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |
