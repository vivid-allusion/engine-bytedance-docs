---
title: "ExportTraceSpan"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/ExportTraceSpan"
---

Exports Trace Span data by specified query criteria and then writes to an evaluation platform or returns local exported data.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

Server\-side Monitoring has been deployed in multiple regions around the world to provide you with a more stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-server.cn\-beijing.byteplusapi.com.cn?Action=ExportTraceSpan&Version=2024\-07\-30


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For details, see [Common parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ExportTraceSpan |The API name. The current API name is `ExportTraceSpan`. |
|Version |String |Yes |2024\-07\-30 |The API version. The current API version is `2024-07-30`. |
|SpanListParam |Object of [SpanListParam](https://docs.byteplus.com/en/docs/299/115794#spanlistparam) |Yes |{"StartTime":1672502400,"EndTime":1672506000,"SpanIds":["0af7651916cd43dd8448eb211c80319c"]} |Span query criteria to be exported. |
|ExportSpanParam |Object of [ExportSpanParam](https://docs.byteplus.com/en/docs/299/115794#exportspanparam) |Yes |{"ExportFormat":"mapping","FieldMappings":[{"TraceFieldKey":"trace_id","TraceFieldJsonPath":"$.trace_id","FieldSchema":{"Name":"trace_id","ContentType":"Text","IsRequired":true}}]} |Span export format and field mapping configuration. |
|ExportTarget |Integer |Yes |2 |Export target. Values:<br><br><br>* **2**: AgentKit evaluation<br><br>* **3**: DataFinder evaluation |
|EvaluationConfig |Object of [EvaluationConfig](https://docs.byteplus.com/en/docs/299/115794#evaluationconfig) |Yes |{"WorkspaceId":"ws\-12345","IsNewEvaluationSet":true,"EvaluationSetName":"<br><br>EvaluationSetA","ExportType":0,"FieldSchemas":[]} |Unified evaluation platform configuration. |
|ProjectName |String |Yes |default |The project name. |
|CozeToken |String |Yes |pat_xxx |Authorization token for accessing CozeLoop.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when querying <code>CozeLoop</code>.</div><br> |


<span id="spanlistparam"></span>
### SpanListParam


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Limit |Integer |No |100 |Maximum number of items to export. |
|Order |String |No |DESC |Sorting order. Values:<br><br><br>* **ASC**: Ascending order<br><br>* **DESC**: Descending order |
|Offset |Integer |No |0 |Export data offset. |
|EndTime |Long |No |1672506000 |Query end timestamp in seconds. |
|Filters |Array of [FilterConditionV2](https://docs.byteplus.com/en/docs/299/115794#filterconditionv2) |No |[{"Key":"service_name","Op":"in","Values":["checkout\-service"]}] |Span filter criteria. |
|OrderBy |String |No |start_time_millisecond |A field for sorting. Example:<br><br><br>* **start_time_millisecond:**  Start time of the Span<br><br>* **duration_microseconds:**  Duration of the Span |
|SpanIds |Array of String |No |["0af7651916cd43dd8448eb211c80319c"] |Specify the list of Span IDs to export. |
|StartTime |Long |No |1672502400 |Timestamp of Query start time, measured in seconds. |
|MaxCallCostMillisecond |Long |No |1,000 |Upper limit of call duration in milliseconds.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">A value of 0 means no limit is applied to this parameter.</div><br> |
|MinCallCostMillisecond |Long |No |0 |Lower limit of call duration. Unit: milliseconds.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">A value of 0 means no limit is applied to this parameter.</div><br> |


<span id="filterconditionv2"></span>
### FilterConditionV2


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Op |String |No |in |Operator in filter criteria. Values:<br><br><br>* **gt**: greater than<br><br>* **gte**: greater than or equal to<br><br>* **lt**: less than<br><br>* **lte**: less than or equal to<br><br>* **eq**: equal to<br><br>* **neq**: not equal to<br><br>* **in**: contains<br><br>* **not_in**: does not contain<br><br>* **lk**: Matches data that fits a specific pattern.<br><br>* **nlk**: Excludes data that fits a specific pattern. |
|Key |String |No |session_id |Filter criteria key. |
|Values |Array of String |No |["sess_001"] |Filter criteria value. |


<span id="exportspanparam"></span>
### ExportSpanParam


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|ExportFormat |String |No |mapping |Export format. Values:<br><br><br>* **mapping:**  Field mapping<br><br>* **custom_template:**  Custom template<br><br>* **span_detail:**  Span details |
|FieldMappings |Array of [FieldMappings](https://docs.byteplus.com/en/docs/299/115794#fieldmappings) |No |[{"TraceFieldKey":"trace_id","TraceFieldJsonPath":"$.trace_id","FieldSchema":{"Name":"trace_id","ContentType":"Text","IsRequired":true}}] |Field mapping.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required only when <code>ExportFormat</code> is set to mapping.</div><br> |
|CustomTemplate |String |No |{"trace_id":"{{.TraceId}}"} |Custom export template.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required only when <code>ExportFormat</code> is set to custom_template.</div><br> |


<span id="fieldmappings"></span>
### FieldMappings


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|FieldSchema |Object of [FieldSchema](https://docs.byteplus.com/en/docs/299/115794#fieldschema) |No |{"Name":"trace_id","Description":"Trace ID","ContentType":"Text","IsRequired":true} |Target evaluation set field structure. |
|TraceFieldKey |String |No |trace_id |Name of the Trace field. Sample value:<br><br><br>* **GenAIInput:**  The field containing large model input content<br><br>* **GenAIOutput:**  The field containing large model input content<br><br>* **trace_id:**  Trace identifier<br><br>* **span_id:**  Identifier for a single call unit<br><br>* **tags.type:**  Type field in Span tag |
|TraceFieldJsonPath |String |No |$.trace_id |JSON path of the trace field. |


<span id="fieldschema"></span>
### FieldSchema


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Name |String |No |trace_id |Field name. |
|IsRequired |Boolean |No |true |Whether the field is required. |
|TextSchema |String |No |{"type":"string"} |JSON Schema definition for text fields. |
|ContentType |String |No |Text |Field content type. |
|Description |String |No |Trace ID |Field description. |
|DefaultDisplayFormat |String |No |plain_text |Default display format for fields. |


<span id="evaluationconfig"></span>
### EvaluationConfig


|**Parameters** |**type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|ExportType |Integer |No |0 |Export method. Values:<br><br><br>* **0**: Append<br><br>* **1**: Overwrite |
|WorkspaceId |String |No |ws\-12345 |Workspace ID of evaluation platform. |
|FieldSchemas |Array of [FieldSchema](https://docs.byteplus.com/en/docs/299/115794#fieldschema) |No |[{"Name":"trace_id","Description":"Trace ID","ContentType":"Text","IsRequired":true}] |Field structure list of the evaluation set. |
|EvaluationSetId |String |No |eval\-set\-67890 |Existing evaluation set ID.<br><br><div data-tips="true" data-tips-type="default">Description</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when <code>IsNewEvaluationSet</code> is set to false.</div><br> |
|EvaluationSetName |String |No |Trace Evaluation Set |Name of the new evaluation set.<br><br><div data-tips="true" data-tips-type="default">Description</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when <code>IsNewEvaluationSet</code> is set to true.</div><br> |
|IsNewEvaluationSet |Boolean |No |true |Whether to create a new evaluation set. Values:<br><br><br>* **true**: Create<br><br>* **false**: Do not create |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-server.cn-beijing.byteplusapi.com.cn?Action=ExportTraceSpan&Version=2024-07-30
{
    "SpanListParam": {
        "StartTime": 1672502400,
        "EndTime": 1672506000,
        "SpanIds": [
            "0af7651916cd43dd8448eb211c80319c"
        ]
    },
    "ExportSpanParam": {
        "ExportFormat": "mapping",
        "FieldMappings": [
            {
                "TraceFieldKey": "trace_id",
                "TraceFieldJsonPath": "$.trace_id",
                "FieldSchema": {
                    "Name": "trace_id",
                    "ContentType": "Text",
                    "IsRequired": true
                }
            }
        ]
    },
    "ExportTarget": 2,
    "EvaluationConfig": "{\"WorkspaceId\":\"ws-12345\",\"IsNewEvaluationSet\":true,\"EvaluationSetName\":\"\nEvaluationSetA\",\"ExportType\":0,\"FieldSchemas\":[]}",
    "ProjectName": "default",
    "CozeToken": "pat_xxx"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Items |Array of [ExportTraceSpanItem](https://docs.byteplus.com/en/docs/299/115794#exporttracespanitem) |[{"FieldList":[],"status":"success"}] |List of exported data items. |
|ItemCount |Integer |100 |Number of export data items successfully generated. |
|EvaluationSetId |String |eval\-set\-67890 |ID of the evaluation set to write to. |
|EvaluationSetName |String |Trace Evaluation Set |Name of the evaluation set to write to. |


<span id="exporttracespanitem"></span>
### ExportTraceSpanItem


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|status |String |success |Data export status. |
|FieldList |Array of [FieldData](https://docs.byteplus.com/en/docs/299/115794#fielddata) |[{"Key":"trace_id","Name":"trace_id","Content":{"ContentType":"Text","Text":"0af7651916cd43dd8448eb211c80319c"}}] |Data item field list. |


<span id="fielddata"></span>
### FieldData


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Key |String |trace_id |Unique identifier for the field. |
|Name |String |trace_id |Field name. |
|Content |Object of [FieldContent](https://docs.byteplus.com/en/docs/299/115794#fieldcontent) |{"ContentType":"Text","Text":"0af7651916cd43dd8448eb211c80319c"} |Field content. |


<span id="fieldcontent"></span>
### FieldContent


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Text |String |0af7651916cd43dd8448eb211c80319c |Text content. |
|ContentType |String |Text |Field content type. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "Result": {
        "EvaluationSetId": "eval-set-67890",
        "EvaluationSetName": "Trace Evaluation Set",
        "ItemCount": 100,
        "Items": []
    },
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ExportTraceSpan",
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
