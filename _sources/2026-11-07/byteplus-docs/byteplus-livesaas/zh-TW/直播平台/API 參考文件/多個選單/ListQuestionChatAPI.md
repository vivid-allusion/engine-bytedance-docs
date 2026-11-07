---
title: "ListQuestionChatAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/listquestionchatapi-zh-TW"
---

呼叫此 API 以取得直播間問答選單中的問題。結果可依按讚數或發送時間排序，讓您能優先取得最熱門或最新的問題。若要取得特定問題的回覆，您可以使用回應中的問題 ID 呼叫 [ListAnswerChatAPI](https://docs.byteplus.com/ihay5kb0/7mknjxub)

<span id="fdea8512"></span>
## 必要條件


* 配額：每個帳戶每分鐘最多 120 次查詢

* 前提條件：需有 BytePlus 帳戶或具備 Live 控制 \> 編輯權限的 IAM 使用者。如需新增 IAM 使用者的詳細資訊，請參閱 [管理使用者、組織與角色](https://docs.byteplus.com/docs/byteplus-livesaas/guan-li-shi-yong-zhe-zu-zhi-yu-jue-se-zh-TW)。


<span id="79719cd3"></span>
## HTTP 請求


* URL：`https://livesaas.byteplusapi.com/?Action=ListQuestionChatAPI&Version=2020-06-01`

* 方法：GET


<span id="c0f49424"></span>
## 請求參數

以下表格未包含所有共用請求參數。完整列表請參閱 [共用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/gong-yong-can-shu-zh-TW#f1706967)。

<span id="32f3e185"></span>
### 查詢


|名稱 |資料型態 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`ListQuestionChatAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。目前版本：`2020-06-01`。 |
|ActivityId |Long |是 |`17218312****` |直播間的活動 ID。您可以透過呼叫 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) 取得此 ID。 |
|PageNumber |Long |否 |`1` |要回傳的頁碼。預設值：`1`。 |
|PageSize |Long |否 |`100` |每頁要回傳的結果數量。預設值：`100`。<br><br>數值範圍：[1,1000]。 |
|OrderType |Integer |否 |`0` |指定回傳的問題是否依按讚數或提交時間排序。<br><br>預設值：`0`。<br><br>有效值：<br><br><br>* `0`：問題依發送時間倒序排列。最先回傳最新的問題。<br><br>* `1`：問題依按讚數排序。最先回傳最熱門的問題。 |
|FilterPin |Integer |否 |`0` |指定要回傳哪些問題。<br><br>預設值：`0`。<br><br>有效值：<br><br><br>* `0`：所有問題。<br><br>* `1`：置頂於問答選單的問題。<br><br>* `2`：未置頂於問答選單的問題。 |


<span id="78eacc9f"></span>
## 回應參數


|名稱 |資料型態 |範例值 |說明 |
|---|---|---|---|
|PageNumber |Long |`1` |回傳頁面的頁碼。 |
|PageSize |Long |`100` |每頁回傳的結果數量。 |
|TotalCount |Long |`1` |回傳問題的總數。 |
|QuestionMsgs |Array of[QuestionMsg](https://docs.byteplus.com/docs/byteplus-livesaas/listquestionchatapi-zh-TW#e2930158) |`-` |回傳問題的列表。 |


<span id="e2930158"></span>
### QuestionMsg


|名稱 |資料型態 |範例值 |說明 |
|---|---|---|---|
|QuestionMsgId |Long |`5941305` |問題 ID。 |
|UserNickName |String |`Viewer A` |發送問題的使用者暱稱。 |
|UserExternalId |String |`12387404123****` |發送問題的使用者在第三方平台上的唯一識別碼。僅以以下方式登入直播間的觀眾才會有此 ID。您可以利用此 ID 在組織內識別觀眾，以進行用戶洞察與數據分析。<br><br>此 ID 會根據觀眾登入直播間的方式而有所不同。<br><br><br>* 自訂帳號：自訂登入時透過 `UserId` 參數傳遞的值。如需詳細資訊，請參閱 [自訂驗證登入](https://docs.byteplus.com/docs/byteplus-livesaas/zi-ding-yan-zheng-deng-ru-zh-TW)。<br><br>* 手機號碼：觀眾以手機號碼註冊 BytePlus Live 時所產生的 `passport_id`。<br><br>* OAuth 2.0：對應於您自有帳戶系統中用戶 ID 的欄位。<br><br>* Allowlist：觀眾輸入的 allowlist 驗證資訊。 |
|CreateTime |Long |`1717145029` |問題發送時的時間，採用 Unix 時間戳格式。單位：秒。 |
|Content |String |`Question A` |問題的內容。 |
|LikeCount |Long |`20` |問題的按讚數。 |
|IsPined |Integer |`0` |表示該問題是否置頂於問答選單。<br><br><br>* `0`：未置頂。<br><br>* `1`：已置頂。 |


<span id="8c70f7da"></span>
## 範例

<span id="bf1a2f5e"></span>
### 範例請求

```JSON
GET https://livesaas.byteplusapi.com/?Action=ListQuestionChatAPI&Version=2020-06-01&ActivityId=17218312****&PageNumber=1&PageSize=100&OrderType=0&FilterPin=0
```


<span id="34c8cb31"></span>
### 範例回應

```JSON
{
  "ResponseMetadata": {
    "RequestId": "201806041104200100100232280022D30",
    "Action": "ListQuestionChatAPI",
    "Version": "2020-06-01",
    "Service": "livesaas",
    "Region": "ap-singapore-1",
    "SystemTime": 1717593301
  },
    "Result": {
        "PageNumber": 1,
        "PageSize": 100,
        "TotalCount": 1,
        "QuestionMsgs": [
            {
                "QuestionMsgId": 5941305,
                "UserNickName": "Viewer A",
                "UserExternalId": "",
                "CreateTime": 1717145029,
                "Content": "Question A",
                "LikeCount": 20,
                "IsPined": 0
            }
        ]
    }
}
```


<span id="2b1e6a6a"></span>
## 錯誤碼

共用錯誤碼列表請參閱 [常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/chang-jian-cuo-wu-yu-zhuang-tai-ma-zh-TW)。
