---
title: "DescribeValidationTaskResult"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/describevalidationtaskresult"
---

Call the DescribeValidationTaskResult API to view the data verification result.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|TaskId |String |Yes |4aba0b3ce6a24aff82da259e27\*\*\*\*\*\* |Verification task ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/DTS/describevalidationtasks">DescribeDataValidationTasks</a> interface to query the data verification task ID.</div><br> |
|PageNumber |Integer |No |1 |Page number. The value range is 1 to 1000, with a default of 1. |
|PageSize |Integer |No |10 |Number of records per page. The value range is 1 to 1000, with a default of 10. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|ValidationResult |Object of [ValidationResult](https://docs.byteplus.com/en/docs/57/47125#validationresult) |&nbsp;<br><br>```Plain Text```<br>```{```<br>```     "FileState": "Unknown",```<br>```     "FullValidationResult": [```<br>```         {```<br>```             "DiffNum": 0,```<br>```             "EstimateNum": 100000,```<br>```             "FinishTime": 1733964705706,```<br>```             "StartTime": 1733964542000```<br>```         }```<br>```      ],```<br>```      "TaskSubType": "FullRowCompare",```<br>```      "Total": 1,```<br>```      "TotalDiffNum": 0```<br>```   }```<br>```}```<br><br><br> |Data verification result information. |


<span id="validationresult"></span>
### ValidationResult


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|FileState |String |Unknown |Whether the Diff file has been generated, and the values are as follows:<br><br><br>* `Unknown`: Indicates that no Diff data file has been generated.<br><br>* `Generating`: Indicates that the Diff file is being generated.<br><br>* `Generated`: Indicates that the Diff file has been generated and can be downloaded. |
|TaskSubType |String |FullRowCompare |Data verification task type. The values are as follows:<br><br><br>* `FullRowCompare`: Indicates full data verification.<br><br>* `FullRowCountCompare`: Indicates full row\-count verification.<br><br>* `FullPkCompare`: Indicates full primary key validation.<br><br>* `MetaCompare`: Indicates Schema Verification.<br><br>* `IncrDataValidation`: Indicates Increment validation. |
|TotalDiffNum |Long |0 |Total number of inconsistent objects. |
|FullValidationResult |Array of [FullValidationResultItem](https://docs.byteplus.com/en/docs/57/47125#fullvalidationresultitem) |```sql```<br>```[```<br>```    {```<br>```        "DiffNum": 0,```<br>```        "EstimateNum": 101439,```<br>```        "FinishTime": 1733962493369,```<br>```        "StartTime": 1733961817000,```<br>```        "Database": {```<br>```             "DestObjName": "test****",```<br>```             "ObjectType": "Database",```<br>```             "SrcObjName": "test****"```<br>```        },```<br>```        "Object": {```<br>```             "DestObjName": "test****",```<br>```             "ObjectType": "Database",```<br>```             "SrcObjName": "test****"```<br>```        }```<br>```     }```<br>```]```<br> |Full data verification results. |
|PkValidationResult |Array of [PkValidationResultItem](https://docs.byteplus.com/en/docs/57/47125#pkvalidationresultitem) |```json```<br>```[```<br>```    {```<br>```        "DiffNum": 0,```<br>```        "EstimateNum": 1,```<br>```        "FinishTime": 1733822797540,```<br>```        "StartTime": 1733822724000,```<br>```        "Database": {```<br>```             "DestObjName": "test****",```<br>```             "ObjectType": "Database",```<br>```             "SrcObjName": "test****"```<br>```        },```<br>```        "Object": {```<br>```             "DestObjName": "test****",```<br>```             "ObjectType": "Database",```<br>```             "SrcObjName": "test****"```<br>```        }```<br>```    }```<br>```]```<br> |Full primary key verification result. |
|RowCountValidationResult |Array of [RowCountValidationResultItem](https://docs.byteplus.com/en/docs/57/47125#rowcountvalidationresultitem) |```sql```<br>```[```<br>```    {```<br>```        "DestNum": 65000000,```<br>```        "DiffNum": 0,```<br>```        "FinishTime": 1733909914252,```<br>```        "SrcNum": 65000000,```<br>```        "StartTime": 1733909810000```<br>```     }```<br>```]```<br> |Full row verification result. |
|IncrValidationResult |Array of [IncrValidationResultItem](https://docs.byteplus.com/en/docs/57/47125#incrvalidationresultitem) |```json```<br>```[```<br>```    {```<br>```        "DiffNum": 0,```<br>```        "FinishTime": 1733822797540,```<br>```        "StartTime": 1733822724000,```<br>```        "Database": {```<br>```             "DestObjName": "test****",```<br>```             "ObjectType": "Database",```<br>```             "SrcObjName": "test****"```<br>```        },```<br>```        "Object": {```<br>```             "DestObjName": "test****",```<br>```             "ObjectType": "Database",```<br>```             "SrcObjName": "test****"```<br>```        }```<br>```    }```<br>```]```<br> |Increment validation result. |
|MetaValidationResult |Array of [MetaValidationResultItem](https://docs.byteplus.com/en/docs/57/47125#metavalidationresultitem) |```sql```<br>```[```<br>```    {```<br>```        "ErrorNum": 0,```<br>```        "FinishTime": 1733909874137,```<br>```        "StartTime": 1733909860000,```<br>```        "WarnNum": 0,```<br>```        "Database": {```<br>```             "DestObjName": "test****",```<br>```             "ObjectType": "Database",```<br>```             "SrcObjName": "test****"```<br>```        },```<br>```        "Object": {```<br>```             "DestObjName": "test****",```<br>```             "ObjectType": "Database",```<br>```             "SrcObjName": "test****"```<br>```        }```<br>```     }```<br>```]```<br> |Schema verification result. |
|Total |Integer |1 |The number of abnormal databases and tables in the verification task. |


<span id="fullvalidationresultitem"></span>
### FullValidationResultItem


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|DiffNum |Long |0 |Different total amount of data. |
|EstimateNum |Long |100,000 |Estimated total rows. |
|FinishTime |Long |1733962493369 |End time of full data verification, in milliseconds timestamp format. |
|StartTime |Long |1733961817000 |Start time of full data verification, in milliseconds timestamp format. |
|Database |Object of [ObjectMapping](https://docs.byteplus.com/en/docs/57/47125#objectmapping) |```json```<br>```{```<br>```     "DestObjName": "test****",```<br>```     "ObjectType": "Database",```<br>```     "SrcObjName": "test****"```<br>```}```<br> |Database information. |
|Object |Object of [ObjectMapping](https://docs.byteplus.com/en/docs/57/47125#objectmapping) |```json```<br>```{```<br>```     "DestObjName": "test****",```<br>```     "ObjectType": "Database",```<br>```     "SrcObjName": "test****"```<br>```}```<br> |Database and table mapping objects between the source and target ends. |


<span id="objectmapping"></span>
### ObjectMapping


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|ObjectType |String |Function |Object type. The values are as follows:<br><br><br>* `Database`: indicates a database.<br><br>* `Table`: indicates a table.<br><br>* `View`: indicates a view.<br><br>* `Column`: Indicates the `column`.<br><br>* `Function`: Indicates the `function`.<br><br>* `Procedure`: Indicates the `procedure`.<br><br>* `Trigger`: Indicates the `trigger`.<br><br>* `Type`: Indicates the `type`.<br><br>* `Domain`: Indicates the `domain`.<br><br>* `Sequence`: Indicates the `sequence`.<br><br>* `Rule`: Indicates the `rule`.<br><br>* `Operator`: Indicates the `operator`.<br><br>* `Aggregate`: Indicates the `aggregate`.<br><br>* `Extension`: Indicates an extension.<br><br>* `Constraint`: Indicates a constraint.<br><br>* `PostSequence`: Indicates a PostgreSQL sequence.<br><br>* `Schema`: Indicates a mode.<br><br>* `Event`: Indicates an event.<br><br>* `DomainConstraint`: Indicates a domain constraint. |
|SrcObjName |String |ceshi\*\*\*\* |Source object name. |
|DestObjName |String |test\*\*\*\* |Target object name. |
|MappingList |Array of [ObjectMapping](https://docs.byteplus.com/en/docs/57/47125#objectmapping) |&nbsp;<br><br>```JSON```<br>```[```<br>```    {```<br>```        "DestObjName": "test",```<br>```        "MappingList": [```<br>```            {```<br>```                "DestObjName": "*",```<br>```                "ObjectMappingSetting": {```<br>```                    "LastWriteWinsKey": "",```<br>```                    "ObjectTransTypes": [```<br>```                        "Meta"```<br>```                    ],```<br>```                    "PolicyForKeyConflict": "TableNone",```<br>```                    "SetObjectTransType": false```<br>```                },```<br>```                "ObjectType": "Event",```<br>```                "SrcObjName": "*"```<br>```            }```<br>```        ],```<br>```        "ObjectMappingSetting": {```<br>```            "LastWriteWinsKey": "",```<br>```            "ObjectTransTypes": [```<br>```                "Meta",```<br>```                "Full",```<br>```                "Incr"```<br>```            ],```<br>```            "PolicyForKeyConflict": "TableOverride",```<br>```            "SetObjectTransType": true```<br>```        },```<br>```        "ObjectType": "Database",```<br>```        "SrcObjName": "test"```<br>```    }```<br>```]```<br> |Transmission task object. |
|ObjectMappingSetting |Object of [ObjectMappingSetting](https://docs.byteplus.com/en/docs/57/47125#objectmappingsetting) |&nbsp;<br><br>```JSON```<br>```{```<br>```    "ESMetaMappingSetting": {```<br>```        "PidCol": [```<br>```            "id",```<br>```            "name"```<br>```        ],```<br>```        "EnableRouting": true,```<br>```        "RoutingCol": [```<br>```            "id"```<br>```        ]```<br>```    }```<br>```}```<br> |Additional parameter information that needs to be configured when synchronizing data to Elasticsearch. |


<span id="objectmappingsetting"></span>
### ObjectMappingSetting


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|ESMetaMappingSetting |Object of [ESMetaMappingSetting](https://docs.byteplus.com/en/docs/57/47125#esmetamappingsetting) |```JSON```<br>```{```<br>```    "PidCol": [```<br>```        "id",```<br>```        "name"```<br>```    ],```<br>```    "EnableRouting": true,```<br>```    "RoutingCol": [```<br>```        "id"```<br>```    ]```<br>```}```<br> |Structure mapping parameters of Elasticsearch. |


<span id="esmetamappingsetting"></span>
### ESMetaMappingSetting


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|PidCol |Array of String |["id", "name"] |Primary key (_id) value. If this parameter is not set, the default is the column of the primary key. |
|EnableRouting |Boolean |EnableRouting |Whether to enable Routing. The values are as follows:<br><br><br>* `true`: Indicates that Routing is enabled.<br><br>* `false`: Indicates that Routing is not enabled. |
|RoutingCol |Array of String |["id"] |The value of `_routing`. This parameter is required when `EnableRouting` is set to `true`. |


<span id="pkvalidationresultitem"></span>
### PkValidationResultItem


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|DiffNum |Long |0 |The total number of inconsistent full primary key validation tasks. |
|EstimateNum |Long |1 |Estimated total rows for the full primary key validation task. |
|FinishTime |Long |1733822797540 |End time of the full data verification task, using milliseconds timestamp. |
|StartTime |Long |1733822724000 |Start time of the full data verification task, using milliseconds timestamp. |
|Database |Object of [ObjectMapping](https://docs.byteplus.com/en/docs/57/47125#objectmapping) |```json```<br>```{```<br>```     "DestObjName": "test****",```<br>```     "ObjectType": "Database",```<br>```     "SrcObjName": "test****"```<br>```}```<br> |Database information. |
|Object |Object of [ObjectMapping](https://docs.byteplus.com/en/docs/57/47125#objectmapping) |```json```<br>```{```<br>```     "DestObjName": "test****",```<br>```     "ObjectType": "Database",```<br>```     "SrcObjName": "test****"```<br>```}```<br> |Database and table mapping objects between the source and target ends. |


<span id="rowcountvalidationresultitem"></span>
### RowCountValidationResultItem


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|SrcNum |Long |65000000 |Number of source rows for the full row verification task. |
|DestNum |Long |65000000 |Number of target rows of the full row verification task. |
|DiffNum |Long |0 |Number of inconsistent rows of the full row verification task. |
|FinishTime |Long |1733909914252 |End time of the full row verification task, in milliseconds timestamp format. |
|StartTime |Long |1733909810000 |Start time of the full row verification task, in milliseconds timestamp format. |
|Database |Object of [ObjectMapping](https://docs.byteplus.com/en/docs/57/47125#objectmapping) |```json```<br>```{```<br>```     "DestObjName": "test****",```<br>```     "ObjectType": "Database",```<br>```     "SrcObjName": "test****"```<br>```}```<br> |Database information. |
|Object |Object of [ObjectMapping](https://docs.byteplus.com/en/docs/57/47125#objectmapping) |```json```<br>```{```<br>```     "DestObjName": "test****",```<br>```     "ObjectType": "Database",```<br>```     "SrcObjName": "test****"```<br>```}```<br> |Database and table mapping objects between the source and target ends. |


<span id="incrvalidationresultitem"></span>
### IncrValidationResultItem


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|DiffNum |Long |0 |Number of inconsistent rows of the increment validation task. |
|StartTime |Long |1733909914252 |Start time of the incremental verification task, using the millisecond timestamp format. |
|FinishTime |Long |1733909810000 |End time of the increment validation task, in milliseconds timestamp format. |
|Database |Object of [ObjectMapping](https://docs.byteplus.com/en/docs/57/47125#objectmapping) |```json```<br>```{```<br>```     "DestObjName": "test****",```<br>```     "ObjectType": "Database",```<br>```     "SrcObjName": "test****"```<br>```}```<br> |Database information. |
|Object |Object of [ObjectMapping](https://docs.byteplus.com/en/docs/57/47125#objectmapping) |```json```<br>```{```<br>```     "DestObjName": "test****",```<br>```     "ObjectType": "Database",```<br>```     "SrcObjName": "test****"```<br>```}```<br> |Database and table mapping objects between the source and target ends. |


<span id="metavalidationresultitem"></span>
### MetaValidationResultItem


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|ErrorNum |Long |0 |Inconsistent amount of data with the error type appears in the schema verification task result. |
|FinishTime |Long |1733909874137 |Schema verification task end time, using the millisecond timestamp format. |
|StartTime |Long |1733909860000 |Schema verification task start time, using the millisecond timestamp format. |
|WarnNum |Long |0 |Inconsistent amount of data with the warning type appears in the schema verification task result. |
|Database |Object of [ObjectMapping](https://docs.byteplus.com/en/docs/57/47125#objectmapping) |```json```<br>```{```<br>```     "DestObjName": "test****",```<br>```     "ObjectType": "Database",```<br>```     "SrcObjName": "test****"```<br>```}```<br> |Database information. |
|Object |Object of [ObjectMapping](https://docs.byteplus.com/en/docs/57/47125#objectmapping) |```json```<br>```{```<br>```     "DestObjName": "test****",```<br>```     "ObjectType": "Database",```<br>```     "SrcObjName": "test****"```<br>```}```<br> |Database and table mapping objects between the source and target ends. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=DescribeValidationTaskResult&Version=2022-10-01 HTTP/1.1
Content-Type: application/json
Host: dts.cn-beijing.byteplusapi.com.cn
X-Date: 20221001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20221001/cn-beijing/dts/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "TaskId": "b75b64b9fd134026a18420f3******",
    "PageNumber": 1,
    "PageSize": 10
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20241217142238DFA631C9D4A54ACA0885-542ca0",
        "Action": "DescribeValidationTaskResult",
        "Version": "2022-10-01",
        "Service": "dts",
        "Region": "cn-beijing"
    },
    "Result": {
        "ValidationResult": {
            "FileState": "Generated",  
*               "FullValidationResult": [
                {
                    "DiffNum": 5441,
                    "EstimateNum": 199796,
                    "FinishTime": 1734387280919,
                    "StartTime": 1734387225000,
                    "Database": {
                        "DestObjName": "test****",
                        "ObjectType": "Database",
                        "SrcObjName": "test****"
                    },
                    "Object": {
                        "DestObjName": "test****",
                        "ObjectType": "Database",
                        "SrcObjName": "test****"
                    }
                }
            ],
            "TaskSubType": "FullRowCompare",
            "Total": 1,
            "TotalDiffNum": 5441
        }
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/DTS/error_codes).
