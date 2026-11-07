---
title: "Get Task Details"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Get_Task_Details"
---

<span id="8860d37a"></span>
# **Request description**

Request method: GET

Request URL: https://{domain}/dataAgent/llm/openApi/v2/deepresearch/taskDetail

<span id="cfc52c53"></span>
# **Request parameters**


|Location |Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|---|
|QueryParams |id |string |Yes |314b788f83394219afa563e47a2938a9 |The task ID. After you call the 'Execute deep research task' API, the returned result contains the task ID for the corresponding execution task. |


<span id="238df410"></span>
# Request example

```JSON
https://{domain}/dataAgent/llm/openApi/v2/deepresearch/taskDetail?id=314b788f83394219afa563e47a2938a9
```


<span id="10fe624b"></span>
# Response parameters


|Location |Parameter |Type |Example value |Description |
|---|---|---|---|---|
|ROOT |task |DeepResearchTask |See the example below |Details of the currently queried task. |


<span id="36e3c6ca"></span>
# Response example

```JSON
{
    "JSONIFY_PRETTYPRINT_REGULAR": false,
    "code": "llm/ok",
    "data": {
        "task": {
            "artifacts": [
                {
                    "artifactId": "821c905ef77c4e0ead2c22f4a20e4365",
                    "description": "Markdown Report",
                    "metadata": {
                        "type": "deep_research_markdown_report"
                    },
                    "name": "0x验证数据可视化报告",
                    "parts": [
                        {
                            "kind": "text",
                            "text": "# 0x验证数据可视化报告\n\n# 1 数据概览与图表展示\n\n基于0x验证表的数据分析，该数据集包含3个日期（2023-04-20至2023-04-22），涵盖2个项目（A和B），共计6条记录。\n\n\n\n\n| 日期         | 项目   |    数字 |      浮点 |\n|------------|------|-------|---------|\n| 2023-04-20 | B    | 49930 | 39940.4 |\n| 2023-04-20 | A    |  9980 | 19980.5 |\n| 2023-04-21 | A    |  9990 | 19990.7 |\n| 2023-04-21 | B    | 49980 | 39980.6 |\n| 2023-04-22 | A    | 10000 | 20000.9 |\n| 2023-04-22 | B    | 50000 | 40000.8 |\n\n\n\n数据可视化显示，项目B的数字总和为149,910，显著高于项目A的29,970，两者比例约为5:1。浮点数据同样呈现类似分布趋势，项目B的浮点总和约为项目A的2倍。\n\n# 参考信息\n\n本报告的数据来源与图表引用如下："
                        }
                    ]
                }
            ],
            "contextId": "fd86552d317b4733aa8e7438f81c84b5",
            "id": "314b788f83394219afa563e47a2938a9",
            "kind": "task",
            "metadata": {
                "agentId": 17368,
                "dataSetList": [
                    {
                        "appId": 1004033,
                        "id": 1836089
                    }
                ],
                "deepResearchTaskId": 181928,
                "fileList": [
                    "agent-upload-20250916121852-a79607aef5e44339ad9afa1aa41c81b5"
                ],
                "reportList": [
                    {
                        "appId": 1004033,
                        "reportId": 7112515
                    }
                ],
                "sessionId": 12013496
            },
            "status": {
                "state": "completed",
                "timestamp": "2025-09-26T14:52:00.878760"
            }
        }
    },
    "msg": {}
}
```
