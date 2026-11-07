---
title: "ListQuestionnaireDataAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-listquestionnairedataapi-zh-TW"
---

呼叫此 API 以取得與特定直播活動相關的問卷統計資料分頁清單。這包括問卷 ID、標題、發布時間，以及提交者數量等詳細資訊。

<span id="64b48720"></span>
## 請求

<span id="4ea84dd3"></span>
### 詳細資訊


* API 操作：`ListQuestionnaireDataAPI`

* 請求方法：GET

* 請求 URI：`http://livesaas.byteplusapi.com/?Action=ListQuestionnaireDataAPI&Version=2020-06-01`

* 配額：每個帳戶每分鐘最多 120 次查詢


<span id="8f085832"></span>
### 查詢字串參數

下表未包含所有共用請求參數。完整清單請參見[共用請求參數](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**參數名稱** |**資料型別** |**必填** |**說明** |
|---|---|---|---|
|Action |String |是 |API 操作。 |
|Version |String |是 |此 API 操作的版本。目前版本：`2020-06-01`。 |
|ActivityId |Integer |是 |直播活動的 ID。可透過呼叫[ListActivityAPI](https://docs.byteplus.com/en/byteplus-livesaas/docs/listactivityapi)取得 ID。 |
|PageNo |Integer |否 |要返回的頁碼。預設值：`1`。 |
|PageItemCount |Integer |否 |每頁返回的結果數量。預設值：`10`。數值範圍：[1,50] |
|Source |Integer |否 |指定要返回資料的來源。預設值：`0`。<br><br>有效值：<br><br><br>* `-1`：返回所有地址的資料。<br><br>* `0`：僅返回預設地址的資料。<br><br>* `1`：僅返回地址 A 的資料。<br><br>* `2`：僅返回地址 B 的資料。<br><br>* `3`：僅返回地址 C 的資料。<br><br>* `4`：僅返回地址 D 的資料。 |


<span id="afcd3304"></span>
### 請求範例

```JSON
Get http://livesaas.byteplusapi.com/?Action=ListQuestionnaireDataAPI&Version=2020-06-01&ActivityId=1231231231&Source=0
```


<span id="ec2412a8"></span>
## 回應

<span id="c87420d8"></span>
### 回應結構


|**參數名稱** |**資料型別** |**說明** |
|---|---|---|
|PageItemCount |Integer |每頁返回的結果數量。 |
|PageNo |Integer |返回結果的頁碼。 |
|TotalItemCount |Integer |返回的結果總數。 |
|StatisticsQuestionnaires |[StatisticsQuestionnaires](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listquestionnairedataapi#StatisticsQuestionnaires) 陣列 |問卷資料。 |


**StatisticsQuestionnaires**


|**參數名稱** |**資料型別** |**說明** |
|---|---|---|
|QuestionnaireId |Integer |問卷的 ID。 |
|Title |String |問卷的標題。 |
|PublishTime |Integer |問卷的發布時間，Unix 時間戳格式。單位：秒。 |
|UserCount |Integer |答題者數量。 |


<span id="ef841ad3"></span>
### 回應範例

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
## 錯誤碼

常見錯誤碼清單請參見[共用錯誤與狀態碼](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes)。
