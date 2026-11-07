---
title: "GetVoteListAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/GetVoteListAPI-zh-TW"
---

調用`GetVoteListAPI`以獲取指定直播間的投票配置信息。

<span id="Requirements"></span>
## 需求


* 配額：每個帳號每分鐘 120 次查詢。

* 前提條件：需擁有 BytePlus 帳號，或具備**Insights** \> **View only** 或 **Edit** 權限的 IAM 使用者。如需瞭解如何新增 IAM 使用者，請參見[管理使用者、組織與角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：GET

* 端點：https://livesaas.byteplusapi.com/?Action=GetVoteListAPI&Version=2020\-06\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

下列表格未包含所有通用請求參數。完整列表請參見[通用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`GetVoteListAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |本 API 操作的版本。當前版本：`2020-06-01`。 |
|ActivityId |Long |是 |17218346\*\*\*\* |直播間的活動 ID。可通過調用[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi)獲取 ID。 |
|PageNo |Integer |否 |`1` |要返回的頁碼。預設值：`1`。 |
|PageCount |Integer |否 |`10` |每頁返回的結果數量。預設值：`10`。 |


<span id="Response parameters"></span>
## 回應參數


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|PageNo |Integer |`1` |要返回的頁碼。 |
|PageCount |Integer |`10` |每頁返回的結果數量。 |
|VoteList |Array of[VoteList](https://docs.byteplus.com/docs/byteplus-livesaas/GetVoteListAPI-zh-TW#votelist) |`-` |直播間的投票配置列表。 |


<span id="votelist"></span>
### VoteList


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|VoteId |String |`vote1779514244272189` |投票 ID。 |
|Title |String |Vote |投票標題。 |
|TotalCount |Integer |`1` |參與人數。 |
|ChoiceType |String |`Single` |投票類型。取值如下：<br><br><br>* `Single`：單選<br><br>* `Multiple`：多選 |
|Deadline |Integer |`1697166317` |投票截止時間。Unix 時間戳，單位為秒。 |
|Status |String |`Export` |投票狀態。取值如下：<br><br><br>* `Init`：已建立<br><br>* `Export`：已發送<br><br>* `Deadline`：已結束<br><br>* `Delete`：已刪除 |
|ActivityId |Long |17218346\*\*\*\* |直播間的活動 ID。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetVoteListAPI&Version=2020-06-01&ActivityId=17218346****&PageNo=1&PageCount=10
```


<span id="Sample response"></span>
### 回應範例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetVoteListAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "PageNo": 1,
        "PageCount": 10,
        "VoteList": [
            {
                "VoteId": "vote1779514244272189",
                "Title": "Vote",
                "TotalCount": 1,
                "ChoiceType": "Single",
                "Deadline": 1697166317,
                "Status": "Export",
                "ActivityId": 17218346****
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

常見錯誤碼請參見[常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
