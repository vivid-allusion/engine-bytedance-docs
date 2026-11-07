---
title: "ListCozeloopEvaluationSets"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/ListCozeloopEvaluationSets"
---

Obtains a paginated list of evaluation sets under the specified CozeLoop workspace.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

Server\-side Monitoring has been deployed in multiple regions around the world to provide you with a more stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-server.cn\-beijing.byteplusapi.com.cn?Action=ListCozeloopEvaluationSets&Version=2024\-07\-30


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For details, see [Common parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListCozeloopEvaluationSets |The API name. The current API name is `ListCozeloopEvaluationSets`. |
|Version |String |Yes |2024\-07\-30 |The API version. The current API version is `2024-07-30`. |
|WorkspaceId |String |Yes |ws\-12345 |CozeLoop workspace ID. |
|Filter |Object of [ListCozeloopEvaluationSetsRequestFilter](https://docs.byteplus.com/en/docs/299/115795#listcozeloopevaluationsetsrequestfilter) |No |{"Name":"Trace"} |Evaluation set filter criteria. |
|PageToken |String |No |next\-page\-token |Pagination cursor, not required for the first request. |
|PageSize |Integer |No |20 |Number of items per page, ranging from 1 to 200. |
|Order |String |No |Desc |Sorting order. Values:<br><br><br>* **ASC**: Ascending order<br><br>* **DESC**: Descending order (default value) |
|OrderBy |String |No |CreatedAt |A field for sorting. Values:<br><br><br>* **CreatedAt**: Creation time<br><br>* **UpdatedAt**: Update time (default value) |
|CozeToken |String |Yes |pat_xxx |Authorization token for accessing CozeLoop. |


<span id="listcozeloopevaluationsetsrequestfilter"></span>
### ListCozeloopEvaluationSetsRequestFilter


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Name |String |No |Trace |Evaluation set name filter criteria. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-server.cn-beijing.byteplusapi.com.cn?Action=ListCozeloopEvaluationSets&Version=2024-07-30
{
    "WorkspaceId": "ws-12345",
    "Filter": {
        "Name": "Trace"
    },
    "PageToken": "next-page-token",
    "PageSize": 20,
    "Order": "Desc",
    "OrderBy": "CreatedAt",
    "CozeToken": "pat_xxx"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Items |Array of [EvaluationSet](https://docs.byteplus.com/en/docs/299/115795#evaluationset) |[{"Id":"eval\-set\-67890","Name":"Trace Evaluation Set","Status":"active"}] |Evaluation set list. |
|HasMore |Boolean |false |Whether there is a next page. |
|TotalCount |Long |1 |Total number of evaluation sets. |
|NextPageToken |String |next\-page\-token |Next page pagination cursor. |


<span id="evaluationset"></span>
### EvaluationSet


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |eval\-set\-67890 |Evaluation set ID. |
|Name |String |Trace Evaluation Set |Evaluation set name. |
|Status |String |active |Evaluation set status. |
|BaseInfo |Object of [BaseInfo](https://docs.byteplus.com/en/docs/299/115795#baseinfo) |{"CreatedBy":{"UserId":"10000001"},"UpdatedBy":{"UserId":"10000002"}} |Evaluation set creation and update information. |
|ItemCount |Long |100 |Number of data items in the evaluation set. |
|Description |String |Evaluation set for Trace data |Evaluation set description. |
|LatestVersion |String |v1 |Latest version number. |
|CurrentVersion |Object of [EvaluationSetVersion](https://docs.byteplus.com/en/docs/299/115795#evaluationsetversion) |{"VersionId":"version\-1","Version":"v1","Description":"Initial version","ItemCount":100} |Current evaluation set version. |
|ChangeUncommitted |Boolean |false |Whether there are unsubmitted changes. |


<span id="baseinfo"></span>
### BaseInfo


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|CreatedBy |Object of [UserInfo](https://docs.byteplus.com/en/docs/299/115795#userinfo) |{"UserId":"10000001"} |Task creator information. |
|UpdatedBy |Object of [UserInfo](https://docs.byteplus.com/en/docs/299/115795#userinfo) |{"UserId":"10000002"} |Username of the last operator who updated the task. |


<span id="userinfo"></span>
### UserInfo


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|UserId |String |10000001 |The user ID. |


<span id="evaluationsetversion"></span>
### EvaluationSetVersion


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Version |String |v1 |Evaluation set version number. |
|BaseInfo |Object of [BaseInfo](https://docs.byteplus.com/en/docs/299/115795#baseinfo) |{"CreatedBy":{"UserId":"10000001"},"UpdatedBy":{"UserId":"10000002"}} |Version creation and update information. |
|ItemCount |Long |100 |Number of data items in the current version. |
|VersionId |String |version\-1 |Evaluation set version ID. |
|Description |String |Initial version |Evaluation set version description. |
|EvaluationSetSchema |Object of [EvaluationSetSchema](https://docs.byteplus.com/en/docs/299/115795#evaluationsetschema) |{"FieldSchemas":[{"Name":"trace_id","Description":"Trace ID","ContentType":"Text","IsRequired":true}]} |Field structure of the evaluation set. |


<span id="evaluationsetschema"></span>
### EvaluationSetSchema


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|FieldSchemas |Array of [FieldSchema](https://docs.byteplus.com/en/docs/299/115795#fieldschema) |[{"Name":"trace_id","Description":"Trace ID","ContentType":"Text","IsRequired":true}] |Field structure list of the evaluation set. |


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
        "Items": [
            {
                "Id": "eval-set-67890",
                "Name": "Trace Evaluation Set",
                "Status": "active",
                "BaseInfo": {
                    "CreatedBy": {
                        "UserId": "10000001"
                    },
                    "UpdatedBy": {
                        "UserId": "10000002"
                    }
                },
                "ItemCount": 100,
                "Description": "Evaluation set for Trace data",
                "LatestVersion": "v1",
                "CurrentVersion": {
                    "VersionId": "version-1",
                    "Version": "v1",
                    "Description": "Initial version",
                    "BaseInfo": {
                        "CreatedBy": {
                            "UserId": "10000001"
                        },
                        "UpdatedBy": {
                            "UserId": "10000002"
                        }
                    },
                    "ItemCount": 100,
                    "EvaluationSetSchema": {
                        "FieldSchemas": [
                            {
                                "Name": "trace_id",
                                "Description": "Trace ID",
                                "ContentType": "Text",
                                "IsRequired": true,
                                "TextSchema": "{\"type\":\"string\"}",
                                "DefaultDisplayFormat": "plain_text"
                            }
                        ]
                    }
                },
                "ChangeUncommitted": false
            }
        ],
        "HasMore": false,
        "TotalCount": 1,
        "NextPageToken": "next-page-token"
    },
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListCozeloopEvaluationSets",
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
