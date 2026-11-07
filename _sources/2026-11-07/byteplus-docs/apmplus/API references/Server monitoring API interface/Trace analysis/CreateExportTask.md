---
title: "CreateExportTask"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/CreateExportTask"
---

Creates an online Trace Span export task.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

Server\-side Monitoring has been deployed in multiple regions around the world to provide you with a more stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-server.cn\-beijing.byteplusapi.com.cn?Action=CreateExportTask&Version=2024\-07\-30


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For details, see [Common parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |CreateExportTask |The API name. The current API name is `CreateExportTask`. |
|Version |String |Yes |2024\-07\-30 |The API version. The current API version is `2024-07-30`. |
|Name |String |Yes |OnlineExportTaskA |Task name.<br><br><br>* Must start with a letter or a Chinese character, and may contain digits and underscores (_).<br><br>* Length limit: 1 to 50 characters. |
|Description |String |Yes |Online export task example |Task description. At most 200 characters. |
|TaskType |Integer |Yes |0 |Task type. Value: **0**, online task. |
|StartAt |Long |Yes |1672502400000 |Timestamp of the task start time, measured in milliseconds. |
|EndAt |Long |Yes |1675180799000 |Timestamp for the task end time, measured in milliseconds. |
|SpanFilter |Object of [SpanFilter](https://docs.byteplus.com/en/docs/299/115801#spanfilter) |Yes |{"ProjectName":"default","Conditions":[]} |Span filter criteria. |
|ExportTarget |Integer |Yes |2 |Target platform for export data. Values:<br><br><br>* **2**: AgentKit evaluation platform<br><br>* **3**: DataFinder evaluation platform |
|EvaluationConfig |Object of [EvaluationConfig](https://docs.byteplus.com/en/docs/299/115801#evaluationconfig) |Yes |{"WorkspaceId":"ws\-12345","IsNewEvaluationSet":true,"EvaluationSetName":"<br><br>EvaluationSetA","ExportType":0,"FieldSchemas":[]} |Evaluation configuration. |
|ExportSpanParam |Object of [ExportSpanParam](https://docs.byteplus.com/en/docs/299/115801#exportspanparam) |Yes |{"ExportFormat":"mapping","FieldMappings":[{"TraceFieldKey":"trace_id","TraceFieldJsonPath":"$.trace_id","FieldSchema":{"Name":"trace_id","ContentType":"Text","IsRequired":true}}]} |Export Span configuration. |
|TaskConfig |Object of [TaskConfig](https://docs.byteplus.com/en/docs/299/115801#taskconfig) |Yes |{"DataLimit":10000,"IsCycle":true,"CycleInterval":1,"CycleTimeUnit":"day","CycleDataLimit":100,"CycleStartAt":"2030\-01\-01","CycleEndAt":"2030\-01\-02"} |Task configuration information. |


<span id="spanfilter"></span>
### SpanFilter


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|ProjectName |String |No |default |The project name.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If not configured, it applies to all projects, and this field is not returned in the response.</div><br> |


<span id="evaluationconfig"></span>
### EvaluationConfig


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|ExportType |Integer |No |0 |Export method. Values:<br><br><br>* **0**: Append (default value)<br><br>* **1**: Overwrite |
|WorkspaceId |String |No |ws\-12345 |Workspace ID of evaluation platform. |
|FieldSchemas |Array of [FieldSchema](https://docs.byteplus.com/en/docs/299/115801#fieldschema) |No |[{"Name":"trace_id","Description":"Trace ID","ContentType":"Text","IsRequired":true}] |Field structure list of the evaluation set. |
|EvaluationSetId |String |No |eval\-set\-67890 |Existing evaluation set ID.<br><br><div data-tips="true" data-tips-type="default">Description</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when <code>IsNewEvaluationSet</code> is set to false.</div><br> |
|EvaluationSetName |String |No |Trace Evaluation Set |Name of the new evaluation set.<br><br><div data-tips="true" data-tips-type="default">Description</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when <code>IsNewEvaluationSet</code> is set to true.</div><br> |
|IsNewEvaluationSet |Boolean |No |true |Whether to create a new evaluation set. Values:<br><br><br>* **true**: Create<br><br>* **false**: Do not create (default value) |


<span id="fieldschema"></span>
### FieldSchema


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Name |String |No |trace_id |Field name. |
|IsRequired |Boolean |No |true |Whether the field is required. Values:<br><br><br>* **true**: Required<br><br>* **false**: Optional (default value) |
|TextSchema |String |No |{"type":"string"} |JSON Schema definition for text fields. |
|ContentType |String |No |Text |Field content type. |
|Description |String |No |Trace ID |Field description. |
|DefaultDisplayFormat |String |No |plain_text |Default display format for fields. |


<span id="exportspanparam"></span>
### ExportSpanParam


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|ExportFormat |String |Yes |mapping |Export format. Values:<br><br><br>* **mapping**: Export according to field mapping rules<br><br>* **custom_template**: Export according to custom template structure<br><br>* **span_detail**: Export according to  ** ** Span details |
|FieldMappings |Array of [FieldMappings](https://docs.byteplus.com/en/docs/299/115801#fieldmappings) |No |[{"TraceFieldKey":"trace_id","TraceFieldJsonPath":"$.trace_id","FieldSchema":{"Name":"trace_id","ContentType":"Text","IsRequired":true}}] |Field mapping.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required only when <code>ExportFormat</code> is set to mapping.</div><br> |
|CustomTemplate |String |No |{"trace_id":"{{.TraceId}}"} |Custom export template.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required only when <code>ExportFormat</code> is set to custom_template.</div><br> |


<span id="fieldmappings"></span>
### FieldMappings


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|FieldSchema |Object of [FieldSchema](https://docs.byteplus.com/en/docs/299/115801#fieldschema) |No |{"Name":"trace_id","Description":"Trace ID","ContentType":"Text","IsRequired":true} |Target evaluation set field structure. |
|TraceFieldKey |String |No |trace_id |Name of the Trace field. Sample value:<br><br><br>* **GenAIInput:**  The field containing large model input content<br><br>* **GenAIOutput:**  The field containing large model input content<br><br>* **trace_id:**  Trace identifier<br><br>* **span_id:**  Identifier for a single call unit<br><br>* **tags.type:**  Type field in Span tags |
|TraceFieldJsonPath |String |No |$.trace_id |JSON path of the trace field. |


<span id="taskconfig"></span>
### TaskConfig


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|IsCycle |Boolean |No |true |Whether the task runs in a cycle. Values:<br><br><br>* **true**: Cyclic<br><br>* **false**: Non\-cyclic (default value) |
|DataLimit |Long |No |10,000 |Upper data limit. |
|CycleEndAt |String |No |3\-14:00:00 |Cycle window end time. Example:<br><br><br>* **0\-HH:mm:ss**: Daily cycle<br><br>* **D\-HH:mm:ss**: Weekly cycle, where D represents the day of the week, ranging from 1 to 7, corresponding to Monday to Sunday.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required only when <code>IsCycle</code> is set to true.</div><br> |
|CycleStartAt |String |No |1\-14:00:00 |Cycle window start time. Example:<br><br><br>* **0\-HH:mm:ss**: Daily cycle<br><br>* **D\-HH:mm:ss**: Weekly cycle, where D represents the day of the week, ranging from 1 to 7, corresponding to Monday to Sunday.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required only when <code>IsCycle</code> is set to true.</div><br> |
|CycleInterval |Long |No |1 |Cycle interval.<br><br><br>* When `CycleTimeUnit` is set to day, it means the task runs every specified number of days.<br><br>* When `CycleTimeUnit` is set to week, it means the task runs every specified number of weeks.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required only when <code>IsCycle</code> is set to true.</div><br> |
|CycleTimeUnit |String |No |week |Cycle time unit. Values:<br><br><br>* **day**: Day<br><br>* **week**: Week<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required only when <code>IsCycle</code> is set to true.</div><br> |
|CycleDataLimit |Long |No |100 |Single\-cycle data volume. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-server.cn-beijing.byteplusapi.com.cn?Action=CreateExportTask&Version=2024-07-30
{
    "Name": "OnlineExportTaskA",
    "Description": "Online export task example",
    "TaskType": null,
    "StartAt": 1672502400000,
    "EndAt": 1675180799000,
    "SpanFilter": {
        "ProjectName": "default",
        "Conditions": []
    },
    "ExportTarget": 2,
    "EvaluationConfig": "{\"WorkspaceId\":\"ws-12345\",\"IsNewEvaluationSet\":true,\"EvaluationSetName\":\"\nEvaluationSetA\",\"ExportType\":0,\"FieldSchemas\":[]}",
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
    "TaskConfig": {
        "DataLimit": 10000,
        "IsCycle": true,
        "CycleInterval": 1,
        "CycleTimeUnit": "day",
        "CycleDataLimit": 100,
        "CycleStartAt": "2030-01-01",
        "CycleEndAt": "2030-01-02"
    }
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |1 |Task ID. |
|Name |String |OnlineExportTaskA |Task name. |
|EndAt |Long |1675180799000 |Timestamp for the task end time, measured in milliseconds. |
|Status |Integer |3 |Task status. Values:<br><br><br>* **0**: Pending<br><br>* **1**: Running<br><br>* **2**: Paused<br><br>* **3**: Completed<br><br>* **4**: Deleted<br><br>* **5**: Failed |
|StartAt |Long |1672502400000 |Timestamp of the task start time, measured in milliseconds. |
|TaskType |Integer |0 |Task type. Value: **0**, online task. |
|CreatedAt |String |2023\-01\-01T00:00:00Z |Creation time. |
|CreatedBy |String |zhangsan |Username of the task creator. |
|UpdatedAt |String |2023\-01\-01T01:00:00Z |Update time. |
|UpdatedBy |String |lisi |Username of the last operator who updated the task. |
|SpanFilter |Object of [SpanFilter](https://docs.byteplus.com/en/docs/299/115801#spanfilter) |{"ProjectName":"default","Conditions":[]} |Span filter criteria. |
|TaskConfig |Object of [TaskConfig](https://docs.byteplus.com/en/docs/299/115801#taskconfig) |{"DataLimit":10000,"IsCycle":true,"CycleInterval":1,"CycleTimeUnit":"day","CycleDataLimit":100,"CycleStartAt":"0\-00:00:00","CycleEndAt":"0\-23:59:59"} |Task configuration information. |
|TaskDetail |Object of [TaskDetail](https://docs.byteplus.com/en/docs/299/115801#taskdetail) |{"SuccessCount":950,"FailureCount":50,"TotalCount":1000} |Task execution details. |
|Description |String |Online export task example |Task description. |
|ExportTarget |Integer |2 |Target platform for export data. Values:<br><br><br>* **0**: Local file<br><br>* **1**: CozeLoop<br><br>* **2**: AgentKit evaluation platform<br><br>* **3**: DataFinder evaluation platform |
|ExportSpanParam |Object of [ExportSpanParam](https://docs.byteplus.com/en/docs/299/115801#exportspanparam) |{"ExportFormat":"mapping","FieldMappings":[{"TraceFieldKey":"trace_id","TraceFieldJsonPath":"$.trace_id","FieldSchema":{"Name":"trace_id","ContentType":"Text","IsRequired":true}}]} |Export Span configuration. |
|EvaluationConfig |Object of [EvaluationConfig](https://docs.byteplus.com/en/docs/299/115801#evaluationconfig) |{"WorkspaceId":"ws\-12345","IsNewEvaluationSet":true,"EvaluationSetName":"EvaluationSetA","ExportType":0,"FieldSchemas":[]} |Evaluation configuration. |


<span id="spanfilter"></span>
### SpanFilter


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|ProjectName |String |default |The project name.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If not configured, it applies to all projects, and this field is not returned in the response.</div><br> |


<span id="taskconfig"></span>
### TaskConfig


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|IsCycle |Boolean |true |Whether the task runs in a cycle. Values:<br><br><br>* **true**: Cyclic<br><br>* **false**: Non\-cyclic (default value) |
|DataLimit |Long |10,000 |Upper data limit. |
|CycleEndAt |String |3\-14:00:00 |Cycle window end time. Example:<br><br><br>* **0\-HH:mm:ss**: Daily cycle<br><br>* **D\-HH:mm:ss**: Weekly cycle, where D represents the day of the week, ranging from 1 to 7, corresponding to Monday to Sunday.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required only when <code>IsCycle</code> is set to true.</div><br> |
|CycleStartAt |String |1\-14:00:00 |Cycle window start time. Example:<br><br><br>* **0\-HH:mm:ss**: Daily cycle<br><br>* **D\-HH:mm:ss**: Weekly cycle, where D represents the day of the week, ranging from 1 to 7, corresponding to Monday to Sunday.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required only when <code>IsCycle</code> is set to true.</div><br> |
|CycleInterval |Long |1 |Cycle interval.<br><br><br>* When `CycleTimeUnit` is set to day, it means the task runs every specified number of days.<br><br>* When `CycleTimeUnit` is set to week, it means the task runs every specified number of weeks.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required only when <code>IsCycle</code> is set to true.</div><br> |
|CycleTimeUnit |String |week |Cycle time unit. Values:<br><br><br>* **day**: Day<br><br>* **week**: Week<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required only when <code>IsCycle</code> is set to true.</div><br> |
|CycleDataLimit |Long |100 |Single\-cycle data volume. |


<span id="taskdetail"></span>
### TaskDetail


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|TotalCount |Long |1,000 |Total export volume. |
|FailureCount |Long |50 |Failure count. |
|SuccessCount |Long |950 |Success count. |


<span id="exportspanparam"></span>
### ExportSpanParam


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|ExportFormat |String |mapping |Export format. Values:<br><br><br>* **mapping**: Export according to field mapping rules<br><br>* **custom_template**: Export according to custom template structure<br><br>* **span_detail**: Export according to  ** ** Span details |
|FieldMappings |Array of [FieldMappings](https://docs.byteplus.com/en/docs/299/115801#fieldmappings) |[{"TraceFieldKey":"trace_id","TraceFieldJsonPath":"$.trace_id","FieldSchema":{"Name":"trace_id","ContentType":"Text","IsRequired":true}}] |Field mapping.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required only when <code>ExportFormat</code> is set to mapping.</div><br> |
|CustomTemplate |String |{"trace_id":"{{.TraceId}}"} |Custom export template.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required only when <code>ExportFormat</code> is set to custom_template.</div><br> |


<span id="fieldmappings"></span>
### FieldMappings


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|FieldSchema |Object of [FieldSchema](https://docs.byteplus.com/en/docs/299/115801#fieldschema) |{"Name":"trace_id","Description":"Trace ID","ContentType":"Text","IsRequired":true} |Target evaluation set field structure. |
|TraceFieldKey |String |trace_id |Name of the Trace field. Sample value:<br><br><br>* **GenAIInput:**  The field containing large model input content<br><br>* **GenAIOutput:**  The field containing large model input content<br><br>* **trace_id:**  Trace identifier<br><br>* **span_id:**  Identifier for a single call unit<br><br>* **tags.type:**  Type field in Span tags |
|TraceFieldJsonPath |String |$.trace_id |JSON path of the trace field. |


<span id="fieldschema"></span>
### FieldSchema


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Name |String |trace_id |Field name. |
|IsRequired |Boolean |true |Whether the field is required. Values:<br><br><br>* **true**: Required<br><br>* **false**: Optional (default value) |
|TextSchema |String |{"type":"string"} |JSON Schema definition for text fields. |
|ContentType |String |Text |Field content type. |
|Description |String |Trace ID |Field description. |
|DefaultDisplayFormat |String |plain_text |Default display format for fields. |


<span id="evaluationconfig"></span>
### EvaluationConfig


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|ExportType |Integer |0 |Export method. Values:<br><br><br>* **0**: Append (default value)<br><br>* **1**: Overwrite |
|WorkspaceId |String |ws\-12345 |Workspace ID of evaluation platform. |
|FieldSchemas |Array of [FieldSchema](https://docs.byteplus.com/en/docs/299/115801#fieldschema) |[{"Name":"trace_id","Description":"Trace ID","ContentType":"Text","IsRequired":true}] |Field structure list of the evaluation set. |
|EvaluationSetId |String |eval\-set\-67890 |Existing evaluation set ID.<br><br><div data-tips="true" data-tips-type="default">Description</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when <code>IsNewEvaluationSet</code> is set to false.</div><br> |
|EvaluationSetName |String |Trace Evaluation Set |Name of the new evaluation set.<br><br><div data-tips="true" data-tips-type="default">Description</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when <code>IsNewEvaluationSet</code> is set to true.</div><br> |
|IsNewEvaluationSet |Boolean |true |Whether to create a new evaluation set. Values:<br><br><br>* **true**: Create<br><br>* **false**: Do not create (default value) |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "Result": {
        "Id": "1",
        "Name": "OnlineExportTaskA",
        "EndAt": 1675180799000,
        "Status": 0,
        "StartAt": 1672502400000,
        "TaskType": 0,
        "CreatedAt": "2023-01-01T00:00:00Z",
        "CreatedBy": "zhangsan",
        "UpdatedAt": "2023-01-01T01:00:00Z",
        "UpdatedBy": "lisi",
        "SpanFilter": {
            "ProjectName": "default"
        },
        "TaskConfig": {
            "IsCycle": true,
            "DataLimit": 10000,
            "CycleEndAt": "0-23:59:59",
            "CycleStartAt": "0-00:00:00",
            "CycleInterval": 1,
            "CycleTimeUnit": "day",
            "CycleDataLimit": 100
        },
        "TaskDetail": {
            "TotalCount": 0,
            "FailureCount": 0,
            "SuccessCount": 0
        },
        "Description": "Online export task example",
        "ExportTarget": 2,
        "ExportSpanParam": {
            "ExportFormat": "mapping",
            "FieldMappings": [
                {
                    "TraceFieldKey": "trace_id",
                    "TraceFieldJsonPath": "$.trace_id",
                    "FieldSchema": {
                        "Name": "trace_id",
                        "IsRequired": true,
                        "TextSchema": "{\"type\":\"string\"}",
                        "ContentType": "Text",
                        "Description": "Trace ID",
                        "DefaultDisplayFormat": "plain_text"
                    }
                }
            ],
            "CustomTemplate": "{\"trace_id\":\"{{.TraceId}}\"}"
        },
        "EvaluationConfig": {
            "ExportType": 0,
            "WorkspaceId": "ws-12345",
            "FieldSchemas": [
                {
                    "Name": "trace_id",
                    "IsRequired": true,
                    "TextSchema": "{\"type\":\"string\"}",
                    "ContentType": "Text",
                    "Description": "Trace ID",
                    "DefaultDisplayFormat": "plain_text"
                }
            ],
            "EvaluationSetId": "eval-set-67890",
            "EvaluationSetName": "Trace Evaluation Set",
            "IsNewEvaluationSet": true
        }
    },
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateExportTask",
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
