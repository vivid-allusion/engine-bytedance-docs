---
title: "Intelligent Data Query for Lark Client"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Intelligent_Data_Query_for_Lark_Client"
---

This API is used to call the OpenAPI interface and query data using the intelligent analysis Agent on the Feishu client.

<span id="38b09ba5"></span>
# **Request note**

Request method: POST

Request URL: https://{domain}/aeolus/llm/openApi/v2/chatbi/query

<span id="32a3b5af"></span>
# **Request parameters**


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|question |string |Yes |How many articles are there on October 20? |Question |
|chatId |string |No |100000 |If it is an independent question, this parameter can be omitted. For multi\-turn conversations, the session ID must be provided. Questions with the same chatId are considered as multi\-turn conversations within the same session. |
|agentId |int |Yes |1000 |Agent ID. See the instructions below for how to obtain it. |
|imageFormat |string |Yes |lark_fragment |Specify the format type of charts in the returned query results:<br><br><br>* lark_fragment: Feishu rich text format<br><br>* image_url: Image URL address. Only supported in the North China 2 (Beijing) region of the SaaS environment.<br><br>* lark_image_key: Feishu image key<br><br>* vchart_schema: vchart chart configuration<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Since the image generation service may not be ready in some environments, to prevent errors, it is recommended to set the "imageFormat" field to the fixed value "lark_fragment".</div><br><br><br>* <div data-tips="true" data-tips-type="warning">For applicable scenarios and guidance on parsing different chart result types, see <a href="https://docs.byteplus.com/docs/dataagent/Reference_Intelligent_Analysis_Agent_OpenAPI_Chart_Consumption_Instructions">Reference: Intelligent Analysis Agent OpenAPI Chart Consumption Instructions</a>.</div><br> |
|enableAnalysis |bool |No |false |Whether to enable chart analysis. The default value is: false. When set to true, the Agent will analyze the charts of the query results synchronously during the data query process. When returning the Agent's answer, the interpretation of the chart will also be returned.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The "Basic Information" page in the DataAgent management console also has a configuration switch for "Enable chart analysis" for the agent. When calling the OpenAPI, if the parameter configuration here is inconsistent with the configuration in the console interface:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">When calling the OpenAPI, the configuration specified in the API request takes precedence over the console interface configuration. The OpenAPI response is based on the API request parameters.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">However, the OpenAPI configuration does not override the configuration in the console interface. That is, when using the agent in the interface, the result returned in the interface is based on the interface configuration.</div><br> |
|dataSetId |int |No |102\*\*362 |To specify the scope of the dataset for querying data in smart data query, you can provide the dataset ID. See [dataSetId](https://docs.byteplus.com/docs/dataagent/Reference_Methods_for_Obtaining_Resource_IDs#67395b57) for how to obtain the dataset ID. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">See the Agent web page link for how to obtain APPID and AGENT_ID:</div>


<div data-tips="true" data-tips-type="tip"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8a27bdb8fb0b4c8e925ce1b4369df86f~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<span id="06ec6bd8"></span>
# **Request example**

```JSON
{
    "question": "How many articles were there on October 20th",    // Question, required
    "chatId": "100000",    // Session ID. Questions with the same chatId are considered as multi-turn conversations. If it is an independent question, this parameter can be omitted
    "agentId": 1000,   // Agent ID
    "imageFormat": "lark_fragment"  // Provide this value
}
```


<span id="8d8af862"></span>
# **Response parameters**


|Parameter |Type |Example value |Description |
|---|---|---|---|
|charts |array |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d7dbe9c60df488ea3a1d69d79958d8d~tplv-goo7wpa0wc-image.image) </span> |Charts returned in the query results. Different types of charts are usually returned based on your query, such as line charts, bar charts, and more. Currently, up to 4 charts are returned, that is, the 4 charts most relevant to the scenario. The recommended order is from top to bottom, meaning the first chart in the returned results is the recommended chart, which is more convenient for analyzing query results.<br><br><br>* For example, in an interface\-based query, the chart results are similar to:<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e59cc89a9d46437bbf58714be33e1f74~tplv-goo7wpa0wc-image.image) </span><br><br>* Supported types include:<br><br>   * "column_parallel": Bar chart<br><br>   * "combination": Combination chart<br><br>   * "line": Line chart<br><br>   * "pie": Pie chart<br><br>   * "measure_card": Metric card<br><br>   * "table": Table<br><br>   * scatter: Scatter plot<br><br>   * map: China map<br><br>   * double_axis: dual\-axis chart<br><br>      For more information about supported chart types and usage practices, see [Best Practices: Supported Chart Types and Usage Practices](https://docs.byteplus.com/docs/dataagent/Best_Practices_Supported_Chart_Types_and_Usage_Practices).<br><br>* You set the return type of the result chart using the imageFormat parameter in the request parameters. For guidance on parsing different chart result types, see [Reference: Intelligent Analysis Agent OpenAPI Chart Consumption Instructions](https://docs.byteplus.com/docs/dataagent/Reference_Intelligent_Analysis_Agent_OpenAPI_Chart_Consumption_Instructions). |
|dataSetUrl |string |https://dataset.example.com |Link to the dataset configured for the agent |
|meta |array |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a46220dd38d749b986e11a7128e69b1c~tplv-goo7wpa0wc-image.image) </span> |Description of result fields, which can be understood as the table header. The role parameter indicates the role of the query result field, where measure represents a metric and dimension represents a category. |
|queryHistory |string |https://URL |SQL query address |
|rows |array |[ // query data results<br><br>[<br><br>369251756<br><br>]<br><br>] |Result data |
|sql |string |SELECT (count(\*)) AS article_count FROM `event_online` WHERE (`1702552137_date`) = ('2024\-10\-20') LIMIT 1000 |SQL query |
|thought_process |string |Model output information |Model thought process |


<span id="fdcf03d6"></span>
# Response example

```JSON
{
    "code": "llm/ok", // status code
    "data": {
        "charts": [ // chart type
            {
                "chartType": "measure_card",    
                "image": "",
                "imageLarkKey": null,
                "larkFragment":"{\"tag\": \"column_set\", \"flex_mode\": \"stretch\", \"background_style\": \"grey\", \"horizontal_spacing\": \"default\", \"columns\": [{\"tag\": \"column\", \"width\": \"weighted\", \"weight\": 1, \"elements\": [{\"tag\": \"markdown\", \"text_align\": \"left\", \"content\": \"article_count(\文\章\数\量):\\n**369251756**\"}]}]}"
            },
            {
                "chartType": "table",
                "image": "",
                "imageLarkKey": null,
                "larkFragment":"{\"tag\": \"table\", \"page_size\": 6, \"row_height\": \"32px\", \"custom_tag\": \"chart_type_table\", \"header_style\": {\"bold\": true, \"background_style\": \"grey\", \"text_size\": \"normal\", \"row_height\": \"middle\", \"lines\": 2}, \"columns\": [{\"name\": \"173329985\", \"display_name\": \"article_count(\文\章\数\量)\", \"data_type\": \"text\"}], \"rows\": [{\"1733765\": \"36926\"}]}"
            }
        ],
        "dataSetUrl": "https://URL",// dataset link
        "meta": [// query result field list
            {
                "dataType": "int", // field type
                "name": "article_count(article quantity)", // field name
                "role": "measure" // metric or dimension
            }
        ],
        "queryHistory": "https://data.", // SQL query address
        "rows": [ // query data results
            [
                369251756
            ]
        ],
        "sql": "  SELECT  (count(*)) AS article_count  FROM `event_online`     WHERE (`170252137_日期`) = ('2024-10-20')      LIMIT 1000   " // SQL query,
        "thought_process":"The user wants to know about the xx situation this year. According to the dataset definition, we need to filter out this year's data and display relevant indicators for xx. ...."
    },
    "msg": {} // additional information
}
```
