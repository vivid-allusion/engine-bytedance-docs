---
title: "ListQuestionnaireDataAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-listquestionnairedataapi-zh-CN"
---

调用此 API 以获取与指定直播活动关联的问卷统计数据的分页列表。包括问卷 ID、标题、发布时间以及提交人数等详细信息。

<span id="64b48720"></span>
## 请求

<span id="4ea84dd3"></span>
### 详情


* API 接口行为：`ListQuestionnaireDataAPI`

* 请求方式：GET

* 请求 URI：`http://livesaas.byteplusapi.com/?Action=ListQuestionnaireDataAPI&Version=2020-06-01`

* 配额：每个账号每分钟最多可查询 120 次


<span id="8f085832"></span>
### 查询字符串参数

下表未包含所有共享请求参数。完整列表请参见[共享请求参数](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**参数名称** |**数据类型** |**是否必填** |**接口行为** |
|---|---|---|---|
|Action |String |是 |API 接口行为。 |
|Version |String |是 |此 API 接口行为的版本。当前版本：`2020-06-01`。 |
|ActivityId |Integer |是 |直播活动的 ID。可通过调用[ListActivityAPI](https://docs.byteplus.com/en/byteplus-livesaas/docs/listactivityapi)获取该 ID。 |
|PageNo |Integer |否 |返回的页码。默认值：`1`。 |
|PageItemCount |Integer |否 |每页返回的结果数量。默认值：`10`。取值范围：[1,50] |
|Source |Integer |否 |指定返回数据的来源。默认值：`0`。<br><br>有效值：<br><br><br>* `-1`：返回所有地址的数据。<br><br>* `0`：仅返回默认地址的数据。<br><br>* `1`：仅返回地址 A 的数据。<br><br>* `2`：仅返回地址 B 的数据。<br><br>* `3`：仅返回地址 C 的数据。<br><br>* `4`：仅返回地址 D 的数据。 |


<span id="afcd3304"></span>
### 请求示例

```JSON
Get http://livesaas.byteplusapi.com/?Action=ListQuestionnaireDataAPI&Version=2020-06-01&ActivityId=1231231231&Source=0
```


<span id="ec2412a8"></span>
## 返回调用结果

<span id="c87420d8"></span>
### 返回结构


|**参数名称** |**数据类型** |**接口行为** |
|---|---|---|
|PageItemCount |Integer |每页返回的结果数量。 |
|PageNo |Integer |返回结果的页码。 |
|TotalItemCount |Integer |返回结果的总数。 |
|StatisticsQuestionnaires |[StatisticsQuestionnaires](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listquestionnairedataapi#StatisticsQuestionnaires)数组 |问卷数据。 |


**StatisticsQuestionnaires**


|**参数名称** |**数据类型** |**接口行为** |
|---|---|---|
|QuestionnaireId |Integer |问卷的 ID。 |
|Title |String |问卷的标题。 |
|PublishTime |Integer |问卷的发布时间，Unix 时间戳格式。单位：秒。 |
|UserCount |Integer |答题人数。 |


<span id="ef841ad3"></span>
### 返回示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "ListQuestionnaireDataAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1681983419
    },
    "Result": {
        "TotalItemCount": 1,
        "PageNo": 0,
        "PageItemCount": 0,
        "StatisticsQuestionnaires": [
            {
                "QuestionnaireId": 31402,
                "Title": "Title",
                "PublishTime": 1681982646,
                "UserCount": 2
            }
        ]
    }
}
```


<span id="d9fa6e91"></span>
## 错误码

常见错误码列表请参见[共享错误及状态码](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes)。
