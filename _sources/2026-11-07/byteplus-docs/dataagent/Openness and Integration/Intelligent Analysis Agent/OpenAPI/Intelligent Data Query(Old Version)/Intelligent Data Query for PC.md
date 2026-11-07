---
title: "Intelligent Data Query for PC"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Intelligent_Data_Query_for_PC"
---

This API is used to call the OpenAPI interface and query data using the intelligent analysis agent on the PC.

<span id="f01844b4"></span>
# **Request information**

Request method: POST

Request URL: https://{domain}/aeolus/llm/openApi/v2/ada/query

<span id="44a6c91e"></span>
# **Request parameters**


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|question |string |Yes |How many articles are there on October 20? |Question |
|chatId |string |Can be omitted for standalone questions |100000 |Can be omitted for standalone questions; for multi\-turn conversations, the session ID must be provided. Questions with the same chatId will be treated as multi\-turn questions within the same session. |
|agentId |int |Yes |1000 |Agent ID |
|questionSource |string |Yes |openapi |Indicates the source of the question; the value is fixed as openapi |
|imageFormat |string |Yes |lark_fragment |Specifies the format type of the chart in the returned query result:<br><br><br>* feishu_fragment: Feishu format rich text<br><br>* image_url: Image URL address, supported only in the North China 2 (Beijing) region of the SaaS environment.<br><br>* feishu_image_key: Feishu image key<br><br>* vchart_schema: vchart chart configuration<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Due to possible situations where the image generation service is not ready in the environment, to prevent errors, it is recommended to set the "imageFormat" field to the fixed value "lark_fragment".</div><br><br><br>* <div data-tips="true" data-tips-type="warning">For applicable scenarios and parsing guidance for different chart result types, see <a href="https://docs.byteplus.com/docs/dataagent/Reference_Intelligent_Analysis_Agent_OpenAPI_Chart_Consumption_Instructions">Reference: Intelligent Analysis Agent OpenAPI Chart Consumption Instructions</a>.</div><br> |
|stream |bool |No |true |Whether to enable streaming output<br><br><br>* true: Indicates that streaming output is enabled. The agent will return intermediate results, and the system will output query results in real time and continuously.<br><br>* false: Indicates that streaming output is not enabled. The agent will output the final query result in batch mode. |
|enableAnalysis |bool |No |false |Whether to enable chart analysis. The default value is false. When set to true, the agent will analyze the chart of the query result synchronously during the data query process. When returning the agent's answer, the interpretation of the chart will also be returned synchronously.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The 'Basic Information' page in the DataAgent management backend also includes a configuration switch for the intelligent agent's 'Enable chart analysis' feature. When calling OpenAPI, if the parameter configuration result here is inconsistent with the configuration result in the console interface:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">When calling OpenAPI, the configuration result from OpenAPI takes precedence over the configuration result in the console interface, and the OpenAPI return result is based on the configuration result of the API request parameters.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">However, the configuration result from OpenAPI does not override the configuration result in the console interface. That is, when using the intelligent agent in the interface, the return result is based on the interface configuration.</div><br> |
|dataSetId |int |No |102\*\*362 |To specify the dataset scope for the data query, you can provide the dataset ID. For information on how to obtain the dataset ID, see [dataSetId](https://docs.byteplus.com/docs/dataagent/Reference_Methods_for_Obtaining_Resource_IDs#67395b57). |


<span id="0ee24fd2"></span>
# **Request example**

```JSON
{
    "question": "What was the original adjustment amount yesterday",
    "agentId": 1,
    "questionSource":"openapi",
    "imageFormat": "lark_fragment",  // Pass this value
    "stream": true
}
```


<span id="c8a2960e"></span>
# **Response parameters**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The following uses the parameter structure of the streaming response as an example to explain the meaning of the response parameters.</div>


* <div data-tips="true" data-tips-type="tip">The response parameters for non\-streaming responses are consistent with the parameters in the result field in the table below. Refer to the result field description for details.</div>




|Parameter |Type |Example value |Description |
|---|---|---|---|
|sub_id |int |0 |Sub\-query ID. OpenAPI does not support split queries; sub_id is always 0. |
|type |string |thought |Type of block<br><br><br>* thought: Agent thought content<br><br>* code: SQL code for the agent query<br><br>* result: Query result output by the agent |
|content |string |the question |The main content that is returned when the type field is thought/code |
|status |string |processing |When the type field is result, outputs the current status<br><br><br>* processing: In progress<br><br>* success: Indicates successful execution, but not necessarily complete<br><br>* completed: Indicates all tasks are complete and the query result is returned at once |
|result |object |0 |When the type field is result, outputs the query result. See the table below for the description of the fields in result |


The result field is described as follows:


|Parameter |Type |Example value |Description |
|---|---|---|---|
|charts |array |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9f92767fcede43198318a4e5ac292769~tplv-goo7wpa0wc-image.image) </span> |Returned query result charts. Up to four charts are returned, which are the most relevant to the scenario. The recommended order is from top to bottom, with the first chart in the result being the recommended chart, making it easier to analyze the query results.<br><br><br>* For example, in a visual query, the chart results are similar to:<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e59cc89a9d46437bbf58714be33e1f74~tplv-goo7wpa0wc-image.image) </span><br><br>* Supported types include:<br><br>   * "column_parallel": Bar chart<br><br>   * "combination": Combination chart<br><br>   * "line": Line chart<br><br>   * "pie": Pie chart<br><br>   * "measure_card": Metric card<br><br>   * "table": Table<br><br>   * scatter: Scatter plot<br><br>   * map: China map<br><br>   * double_axis: Dual\-axis chart<br><br>      For more information on supported chart types and usage practices, see [Best Practices: Supported Chart Types and Usage Practices](https://docs.byteplus.com/docs/dataagent/Best_Practices_Supported_Chart_Types_and_Usage_Practices).<br><br>* You set the return type of the result chart using the imageFormat parameter in the request parameters. For guidance on parsing different chart result types, see [Reference: Intelligent Analysis Agent OpenAPI Chart Consumption Instructions](https://docs.byteplus.com/docs/dataagent/Reference_Intelligent_Analysis_Agent_OpenAPI_Chart_Consumption_Instructions). |
|dataSetUrl |string |https://dataset URL |Dataset link |
|meta |array |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/12144566ee3147f6ba5d0fbd9bab9ee6~tplv-goo7wpa0wc-image.image) </span> |Description of the result fields, which can be understood as the table header. The role parameter indicates the role of the query result field, where measure is a metric and dimension is a dimension. |
|queryHistory |string |https:// |SQL view address |
|rows |array |[ // Query data results<br><br>[<br><br>369<br><br>]<br><br>] |Result data |
|sql |string |SELECT (count(\*)) AS article_count FROM `Perfu.aeolus_event_online` WHERE (`1700052552137_Date`) = ('2024\-10\-20') LIMIT 1000 |Query SQL |
|knowledge |string |"<br><br>Note:<br><br><br>1. Metrics are independent and cannot be summed.<br><br>   " |Knowledge information used |
|sessioinId |int |53332234 |Session ID |
|sessioinUrl |string |https://session URL link |Session URL |
|recallFieldInfo |array |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/08cf22d1a5844dff95d1a2366a6f10bd~tplv-goo7wpa0wc-image.image) </span> |List of recalled fields |


<span id="5c00df3b"></span>
# Response example

<span id="33aafa0e"></span>
## Non\-streaming response example

```JSON
{
    "JSONIFY_PRETTYPRINT_REGULAR": false,
    "code": "llm/ok",
    "data": {
        "charts":  [ //Chart type
            {
                "chartType": "measure_card",    
                "image": "",
                "imageLarkKey": null,
                "larkFragment":"{\"tag\": \"column_set\", \"flex_mode\": \"stretch\", \"background_style\": \"grey\", \"horizontal_spacing\": \"default\", \"columns\": [{\"tag\": \"column\", \"width\": \"weighted\", \"weight\": 1, \"elements\": [{\"tag\": \"markdown\", \"text_align\": \"left\", \"content\": \"article_count(\文\章\数\量):\\n**369251756**\"}]}]}",
                "vchart_schema":"{}"
            },
            {
                "chartType": "table",
                "image": "",
                "imageLarkKey": null,
                "larkFragment":"{\"tag\": \"table\", \"page_size\": 6, \"row_height\": \"32px\", \"custom_tag\": \"chart_type_table\", \"header_style\": {\"bold\": true, \"background_style\": \"grey\", \"text_size\": \"normal\", \"row_height\": \"middle\", \"lines\": 2}, \"columns\": [{\"name\": \"1733299899765\", \"display_name\": \"article_count(\文\章\数\量)\", \"data_type\": \"text\"}], \"rows\": [{\"1733299899765\": \"369251756\"}]}",
                "vchart_schema":"{}"
            }
        ],
        "dataSetId": 3231942,
        "dataSetUrl": "",
        "knowledge": "\n\n提示：\n1. 指标相互独立，不同不可相加\n",
        "meta": null,
        "originalCode": "\n# 编写SQL查询\nsql = \"\"\"\nSELECT \n    SUM(`免费量`) AS 总免费量,\n    SUM(`原始量`) AS 总原始量,\n    SUM(`付费量`) AS 总付费量\nFROM 数据集\nWHERE YEAR(`日期`) = YEAR(CURRENT_DATE);\n\"\"\"\n\n# 执行SQL查询并获取结果\ndf = execute_sql(sql, max_rows=1000)\n\n# 输出结果\nanswer(df)\n\n    ",
        
        "queryHistory": "",
        "recallFieldInfo": [
            {
                "descr": null,
                "fieldName": "`客户`",
                "id": 17000641168,
                "mapType": 0,
                "type": "string"
            }
        ],
        "rows": [[100000]],
        "sessionId": 5652519,
        "sessionUrl": "https://网址",
        "sql": "\n# 编写SQL查询\nsql = \"\"\"\nSELECT \n    SUM(`免费量`) AS 总免费量,\n    SUM(`原始量`) AS 总原始量,\n    SUM(`付费量`) AS 总调用量\nFROM 数据集\nWHERE YEAR(`日期`) = YEAR(CURRENT_DATE);\n\"\"\"\n\n# 执行SQL查询并获取结果\ndf = execute_sql(sql, max_rows=1000)\n\n# 输出结果\nanswer(df)\n\n    ",
        "sqlList": [],
        "thought": {
            "columns": [],
            "dimensions": [],
            "filters": [],
            "metrics": [],
            "redactedCode": ""
        }
    },
    "msg": {}
}
```


<span id="5fc2de82"></span>
## Streaming response example

```JSON
data: {"sub_id": 0, "type": "thought", "content": ""}
data: {"sub_id": 0, "type": "thought", "content": "用户"}
data: {"sub_id": 0, "type": "thought", "content": "的问题"}
data: {"sub_id": 0, "type": "thought", "content": "是"}
data: {"sub_id": 0, "type": "thought", "content": "询"}
data: {"sub_id": 0, "type": "thought", "content": "问"}

......

data: {"sub_id": 0, "type": "code", "content": ");"}
data: {"sub_id": 0, "type": "code", "content": "\n"}
data: {"sub_id": 0, "type": "code", "content": ""}
data: {"sub_id": 0, "type": "result", "status": "processing", "msg": "processing", "result": {}}
data: {"sub_id": 0, "type": "result", "status": "success", "msg": "success", "result": {"historyId": 1446196}}
data: {"sub_id": 0, "type": "result", "status": "completed", "result": {"data_set_id": null, "sql": "\n# \u7f16\u5199SQL\u67e5\u8be2\nsql = \"\"\"\nSELECT \n    SUM(`\u539f\u59cb\u8c03\u7528\u91cf`) AS `\u6628\u65e5\u539f\u59cb\u8c03\u7528\u91cf`\nFROM \n    \u6570\u636e\u96c6\nWHERE \n    `\u8c03\u7528\u65e5\u671f` = DATE_SUB(CURRENT_DATE, INTERVAL 1 DAY);\n\"\"\"\n\n# \u6267\u884cSQL\u67e5\u8be2\u5e76\u83b7\u53d6\u7ed3\u679c\ndf = execute_sql(sql, max_rows=1000)\n\n# \u8f93\u51fa\u7ed3\u679c\nanswer(df)\n\n    ", "thought": {"columns": ["\u6628\u65e5\u539f\u59cb\u8c03\u7528\u91cf"], "dimensions": [], "metrics": ["\u6628\u65e5\u539f\u59cb\u8c03\u7528\u91cf"], "filters": ["\u8c03\u7528\u65e5\u671f(\u7b49\u4e8e\u6628\u65e5)", "p_date(\u7b49\u4e8e2025-05-07)", "\u4e3b\u5ba2\u6237\u7b49\u7ea7(\u4e0d\u7b49\u4e8e'\u5185\u90e8\u5ba2\u6237'\u6216\u4e3a\u7a7a)", "\u8c03\u7528\u65e5\u671f(\u5927\u4e8e\u7b49\u4e8e2024-03-01)", "\u9650\u52361000\u6761"], "redacted_code": ""}, "thought_process": "\u7528\u6237\u7684\u95ee\u9898\u662f\u8be2\u95ee\u6628\u5929\u7684\u539f\u59cb\u8c03\u7528\u91cf\u3002\u6211\u4eec\u9700\u8981\u4ece\u6570\u636e\u96c6\u4e2d\u7b5b\u9009\u51fa\u8c03\u7528\u65e5\u671f\u4e3a\u6628\u5929\u7684\u6570\u636e\uff0c\u5e76\u5bf9\u5b57\u6bb5 `\u539f\u59cb\u8c03\u7528\u91cf` \u8fdb\u884c\u6c47\u603b\uff08SUM\uff09\u3002\u6628\u5929\u7684\u65e5\u671f\u53ef\u4ee5\u901a\u8fc7\u5f53\u524d\u65e5\u671f\u51cf\u53bb\u4e00\u5929\u6765\u8ba1\u7b97\u3002\n", "rows": [[1231866173336]], "meta": [{"name": "\u6628\u65e5\u539f\u59cb\u8c03\u7528\u91cf", "dataType": "float", "role": "measure"}], "charts": [{"chartType": "measure_card", "image": "https://tosv.byted.org/obj/davinci-render-output/da911f72-cad0-436d-afcb-dee07cf74e68"}, {"chartType": "table", "image": "https://tosv.byted.org/obj/davinci-render-output/82e1a6b1-1f06-4adb-bef4-a3e640c25333"}], "data_set_url": "", "query_history": "", "chart_html": "\n        <html>\n            <head>\n                <meta http-equiv=\"content-type\" content=\"text/html; charset=utf-8\" />\n            </head>\n        <body>\n            <div style='overflow:auto'>\n            \n                <div style='float:left;width:400px;padding:20'>\n                    <p style='text-align:center'>\n                    measure_card (\u9ed8\u8ba4)\n                    </p>\n                    <img src='https://tosv.byted.org/obj/davinci-render-output/da911f72-cad0-436d-afcb-dee07cf74e68' width='400px' />\n                </div>\n                \n\n                <div style='float:left;width:400px;padding:20'>\n                    <p style='text-align:center'>\n                    table\n                    </p>\n                    <img src='https://tosv.byted.org/obj/davinci-render-output/82e1a6b1-1f06-4adb-bef4-a3e640c25333' width='400px' />\n                </div>\n                \n            </div>\n        </body>\n        ", "prompts": [], "sql_list": [{"origin_sql": "\nSELECT \n    SUM(`\u539f\u59cb\u8c03\u7528\u91cf`) AS `\u6628\u65e5\u539f\u59cb\u8c03\u7528\u91cf`\nFROM \n    \u6570\u636e\u96c6\nWHERE \n    `\u8c03\u7528\u65e5\u671f` = DATE_SUB(CURRENT_DATE, INTERVAL 1 DAY);\n", "rewrite_sql": "  SELECT  (`1700060687188_\u539f\u59cb\u8c03\u7528\u91cf`) AS `\u6628\u65e5\u539f\u59cb\u8c03\u7528\u91cf`  FROM `\u706b\u5c71\u5f15\u64ce\u7ecf\u8425\u7ba1\u7406.\u884c\u4e1a\u8c46\u5305\u5927\u6a21\u578b\u8c03\u7528\u805a\u5408 for \u667a\u80fd\u4f53`     WHERE ( (`1700060687218_\u8c03\u7528\u65e5\u671f`) = ((date_sub(to_date(today()), INTERVAL 1 DAY))) ) AND (to_date(`1700060687175_p_date`) = '2025-05-07') AND (((`1700060687225_\u4e3b\u5ba2\u6237\u7b49\u7ea7`) != ('\u5185\u90e8\u5ba2\u6237')) or ((`1700060687225_\u4e3b\u5ba2\u6237\u7b49\u7ea7`) IS NULL)) AND ((`1700060687218_\u8c03\u7528\u65e5\u671f`) >= ('2024-03-01'))      LIMIT 1000   "}], "recall_field_info": {}, "original_code": "\n# \u7f16\u5199SQL\u67e5\u8be2\nsql = \"\"\"\nSELECT \n    SUM(`\u539f\u59cb\u8c03\u7528\u91cf`) AS `\u6628\u65e5\u539f\u59cb\u8c03\u7528\u91cf`\nFROM \n    \u6570\u636e\u96c6\nWHERE \n    `\u8c03\u7528\u65e5\u671f` = DATE_SUB(CURRENT_DATE, INTERVAL 1 DAY);\n\"\"\"\n\n# \u6267\u884cSQL\u67e5\u8be2\u5e76\u83b7\u53d6\u7ed3\u679c\ndf = execute_sql(sql, max_rows=1000)\n\n# \u8f93\u51fa\u7ed3\u679c\nanswer(df)\n\n    ", "knowledge": null}}
```
