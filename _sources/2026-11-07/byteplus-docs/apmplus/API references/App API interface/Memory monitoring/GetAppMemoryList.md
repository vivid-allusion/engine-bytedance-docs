---
title: "GetAppMemoryList"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAppMemoryList"
---

Get the list of memory leaks or large objects.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAppMemoryList&Version=2022\-10\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAppMemoryList |The API name. The current API name is `GetAppMemoryList`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|os |String |No |Android |The operating system.<br><br><br>* Android<br><br>* iOS |
|start_time |Integer |No |1665417600 |Start time (Unix timestamp). |
|end_time |Integer |No |1665417600 |End time (Unix timestamp). |
|type |String |No |leaked |Memory issue type.<br><br><br>* leaked: Leak<br><br>* large_object: Large object |
|filters |Object of [Condition](https://docs.byteplus.com/en/docs/299/67892#condition) |No |\- |The filter condition. You can specify multiple key‑value pairs to filter data. |
|token |String |No |ttt |Search keyword or token used to query specific information. |
|page_no |Integer |No |1 |Page number. |
|page_size |Integer |No |10 |Number of items per page. |
|order_by |String |No |count_ascend |The sorting method.<br><br><br>* count_ascend: Sort by leak count in ascending order<br><br>* count_descend: Sort by leak count in descending order<br><br>* user_ascend: Sort by affected user in ascending order<br><br>* user_descend: Sort by affected user in descending order<br><br>* avg_size_ascend: Sort by average memory size in ascending order<br><br>* avg_size_descend: Sort by average memsize in descending order<br><br>* total_ascend: Sort by total memory size in ascending order<br><br>* total_descend: Sort by total memory size in descending order |
|is_new |Integer |No |0 |Whether the issue is new.<br><br><br>* 1: Only show new issues<br><br>* 0: All issues |
|status |Array of String |No |["pending"] |Processing state.<br><br><br>* pending<br><br>* processing<br><br>* ignored<br><br>* solved<br><br>* reopen |
|managers |Array of Long |No |\- |Filter by manager. Pass a list of user IDs. |
|tags |Array of Integer |No |\- |Custom tag filtering. |


<span id="condition"></span>
### Condition


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|op |String |No |in |The operator.<br><br><br>* gt: greater than<br><br>* gte: greater than or equal to<br><br>* lt: less than<br><br>* lte: less than or equal to<br><br>* eq: equal to<br><br>* neq: not equal to<br><br>* in: contains<br><br>* not_in: does not contain<br><br>* lk: Matches data that fits a specific pattern.<br><br>* nlk: Excludes data that fits a specific pattern. |
|type |String |No |expression |The type of the filter condition.<br><br><br>* expression: The current condition is an expression.<br><br>* and: The current condition is a compound expression, and multiple sub\-conditions are in an AND logical relationship.<br><br>* or: The current condition is a compound expression, and multiple sub\-conditions are in an OR logical relationship.<br><br>* map: The current condition is of map type. |
|value |String |No |123456 |The filter value. |
|values |Array of String |No |[123456] |The filter value. Multiple filter values are supported. |
|map_key |String |No |key_1 |The key of the map type. It is required when the type is set to map. |
|dimension |String |No |aid |The name of the condition. |
|sub_conditions |Array of [Condition](https://docs.byteplus.com/en/docs/299/67892#condition) |No |\- |The sub\-condition. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAppMemoryList&Version=2022-10-12
{
    "os": "Android",
    "start_time": 1665417600,
    "end_time": 1665417600,
    "type": "leaked",
    "filters": {
        "type": "and",
        "sub_conditions": [
            {
                "dimension": "apm_version",
                "type": "expression",
                "op": "in",
                "values": [
                    "1.4.5"
                ]
            },
            {
                "dimension": "device_model",
                "type": "expression",
                "op": "in",
                "values": [
                    "MI 5X"
                ]
            }
        ]
    },
    "token": "ttt",
    "page_no": 1,
    "page_size": 10,
    "order_by": "count_ascend",
    "is_new": 0,
    "status": [
        "pending"
    ],
    "managers": [
        130
    ],
    "tags": [
        722
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [AnalysesListResponseData](https://docs.byteplus.com/en/docs/299/67892#analyseslistresponsedata) |\- |Response data. |
|error_msg |String |\- |Error message. |
|error_no |Integer |0 |Error code. |


<span id="analyseslistresponsedata"></span>
### AnalysesListResponseData


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|total |Integer |10 |Total number of items in the list. |
|result |Array of [AnalysesListItem](https://docs.byteplus.com/en/docs/299/67892#analyseslistitem) |\- |List details. |


<span id="analyseslistitem"></span>
### AnalysesListItem


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|user |Integer |75 |Affected user count. |
|count |Integer |75 |Error count. |
|issue |Object of [IssueInfo](https://docs.byteplus.com/en/docs/299/67892#issueinfo) |\- |Tag and issue status, and information about handler issue status, currently including owner and status. |
|title |String |com.example.apminsightdemo.NetworkFragment |Object and class information. It is not yet defined. |
|avg_size |Double |75KB |Average size. |
|issue_id |String |1f8f1ad29b14e18ef605e1319c8e6cfe |The unique identifier of the issue. |
|sub_title |String |thread com.apm.insight.runtime.u$c.contextClassLoader |The thread information. |
|total_size |Double |75KB |Total size. |
|max_version |String |2.0 |End version of the issue. |
|min_version |String |1.0 |Start version of the issue. |
|top_version |String |1.5 |Issue version with the greatest impact. |
|user_compare |Double |0.75 |Affected user count change rate. |
|count_compare |Double |0.75 |Error count change rate. |
|avg_size_compare |Double |0.75 |Average size change rate. |
|top_version_count |Integer |100 |Number of leaks in the version with the greatest impact. |
|total_size_compare |Double |0.75 |Total size change rate. |
|top_version_percent |Double |0.75 |Proportion of the version with the greatest impact. |
|end_update_version_code |String |1.0.5 |End app minor version |
|start_update_version_code |String |1.0.0 |Initial app minor version |


<span id="issueinfo"></span>
### IssueInfo


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |Long |1112121 |The issue ID in MySQL. It is different from issue_id. |
|tag |Array of [Tags](https://docs.byteplus.com/en/docs/299/67892#tags) |\- |Label. |
|status |String |processing |Issue status.<br><br><br>* pending<br><br>* processing<br><br>* ignored<br><br>* solved<br><br>* reopen |
|fixed_version |String |v1.1.2 |The fixed version. |


<span id="tags"></span>
### Tags


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |Long |301 |The tag ID. |
|key |String |component |The tag key. |
|values |Array of [ValueId](https://docs.byteplus.com/en/docs/299/67892#valueid) |[{"id": 202, "value": "backend"}, {"id": 203, "value": "frontend"}] |The tag value. |


<span id="valueid"></span>
### ValueId


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |Long |201 |tag valueID。 |
|value |String |production |The tag value. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "data": {
        "total": 10,
        "result": [
            {
                "user": 75,
                "count": 75,
                "issue": {
                    "id": 1112121,
                    "tag": [
                        {
                            "id": 301,
                            "key": "component",
                            "values": [
                                {
                                    "id": 201,
                                    "value": "production"
                                }
                            ]
                        }
                    ],
                    "status": "processing",
                    "fixed_version": "v1.1.2"
                },
                "title": "com.example.apminsightdemo.NetworkFragment",
                "avg_size": 75,
                "issue_id": "1f8f1ad29b14e18ef605e1319c8e6cfe",
                "sub_title": "thread com.apm.insight.runtime.u$c.contextClassLoader",
                "total_size": 75,
                "max_version": "2.0",
                "min_version": "1.0",
                "top_version": "1.5",
                "user_compare": 0.75,
                "count_compare": 0.75,
                "avg_size_compare": 0.75,
                "top_version_count": 100,
                "total_size_compare": 0.75,
                "top_version_percent": 0.75
            }
        ]
    },
    "error_msg": "",
    "error_no": 0
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
