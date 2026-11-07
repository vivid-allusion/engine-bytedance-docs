---
title: "ListAnswerChatAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/listanswerchatapi-zh-TW"
---

調用此 API 以獲取答案列表，並可依據按讚數或發送時間進行排序，優先返回最受歡迎或最新的回覆。

<span id="b82ccfd8"></span>
## 需求


* 配額：每個帳號每分鐘 120 次查詢

* 前置條件：

   * 調用[ListQuestionChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/listquestionchatapi-zh-TW)以獲取問題 ID。

   * 您必須擁有 BytePlus 帳號，或具備「Live control \> Edit」權限的 IAM 使用者。如需有關新增 IAM 使用者的更多資訊，請參見[管理使用者、組織與角色](https://docs.byteplus.com/docs/byteplus-livesaas/guan-li-shi-yong-zhe-zu-zhi-yu-jue-se-zh-TW)。


<span id="6825fb68"></span>
## HTTP 請求


* URL：`https://livesaas.byteplusapi.com/?Action=ListAnswerChatAPI&Version=2020-06-01`

* 方法：GET


<span id="d85f0706"></span>
## 請求參數

下列表格未包含所有通用請求參數。如需完整列表，請參見[共用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/gong-yong-can-shu-zh-TW#f1706967)。

<span id="e1a6bb09"></span>
### 查詢


|名稱 |資料型別 |是否必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`ListAnswerChatAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。當前版本：`2020-06-01`。 |
|ActivityId |Long |是 |`17218312****` |直播間的活動 ID。可通過調用[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi)獲取 ID。 |
|QuestionMsgIds |Long 陣列 |是 |`[5941305,5941306]` |欲查詢回覆的問題 ID。可通過調用[ListQuestionChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/listquestionchatapi-zh-TW)獲取 ID。<br><br>該陣列最多可包含 100 個問題 ID。 |
|PageNumber |Long |否 |`1` |要返回的頁碼。預設值：`1`。 |
|PageSize |Long |否 |`100` |每頁返回的結果數量。預設值：`100`。<br><br>取值範圍：[1,1000]。 |
|OrderType |Integer |否 |`1` |指定是否依據按讚數或建立時間排序回覆。<br><br>預設值：`0`。<br><br>有效值：<br><br><br>* `0`：依建立時間倒序排序回覆。每個問題將優先返回最新的回覆。<br><br>* `1`：依按讚數排序回覆。每個問題將優先返回最受歡迎的回覆。 |
|FilterPin |Integer |否 |`0` |指定要返回的回覆類型。<br><br>預設值：`0`。<br><br>有效值：<br><br><br>* `0`：所有回覆。<br><br>* `1`：僅返回 Q&A 選單中釘選在問題頂部的回覆。<br><br>* `2`：僅返回 Q&A 選單中未釘選在問題頂部的回覆。 |


<span id="2eac1c31"></span>
## 回應參數


|名稱 |資料型別 |範例值 |說明 |
|---|---|---|---|
|PageNumber |Long |`1` |返回的頁碼。 |
|PageSize |Long |`100` |每頁返回的結果數量。 |
|TotalCount |Long |`3` |返回回覆的總數。 |
|AnswerMsgMap |JSON Map |`-` |一個映射，每個鍵為問題 ID，對應的值為該問題的回覆列表。<br><br><br>* `"Key"`：Long。問題 ID。<br><br>* `"Value"`：[AnswerMsg](https://docs.byteplus.com/docs/byteplus-livesaas/listanswerchatapi-zh-TW#82034406)陣列。回覆列表。 |


<span id="82034406"></span>
### AnswerMsg


|名稱 |資料型別 |範例值 |說明 |
|---|---|---|---|
|AnswerMsgId |Long |`5941311` |回覆 ID。 |
|UserNickName |String |`Viewer A` |回覆該問題的用戶暱稱。 |
|UserExternalId |String |`12387404123****` |用戶在第三方平台的唯一標識符。僅當觀眾使用支援的方式登入時，才會有此 ID。您可使用此 ID 於組織內識別觀眾，以進行用戶洞察與數據分析。<br><br>該 ID 會根據觀眾登入直播間的方式而有所不同。<br><br><br>* 自定義帳戶：在自定義登入時傳入的`UserId`參數值。如需更多資訊，請參閱[自訂驗證登入](https://docs.byteplus.com/docs/byteplus-livesaas/zi-ding-yan-zheng-deng-ru-zh-TW)。<br><br>* 手機號碼：觀眾使用手機號碼註冊 BytePlus Live 時所產生的`passport_id`。<br><br>* OAuth 2.0：您自有帳戶系統中對應用戶 ID 的欄位。<br><br>* 允許名單：觀眾輸入的允許名單驗證資訊。 |
|CreateTime |Long |`1717148059` |回覆發送的時間，採用 Unix 時間戳格式（秒）。 |
|Content |String |`回覆 A` |回覆的內容。 |
|LikeCount |Long |`20` |回覆的按讚數。 |
|IsPined |Integer |`0` |表示回覆是否置頂於問答選單下的問題上方。<br><br><br>* `0`：未置頂。<br><br>* `1`：已置頂。 |


<span id="e861fb28"></span>
## 範例

<span id="8057a437"></span>
### 請求範例

```JSON
GET https://livesaas.byteplusapi.com/?Action=ListAnswerChatAPI&Version=2020-06-01&ActivityId=17218312****&QuestionMsgIds=5941305&QuestionMsgIds=5941306&PageNumber=1&PageSize=100&OrderType=1&FilterPin=0
```


<span id="3d8f9cde"></span>
### 回應範例

```JSON
{
  "ResponseMetadata": {
    "RequestId": "201806041104200100100232280022D30",
    "Action": "ListAnswerChatAPI",
    "Version": "2020-06-01",
    "Service": "livesaas",
    "Region": "ap-singapore-1",
    "SystemTime": 1717593301
  },
    "Result": {
        "PageNumber": 1,
        "PageSize": 100,
        "TotalCount": 3,
        "AnswerMsgMap": {
            "5941305": [
                {
                    "AnswerMsgId": 5941311,
                    "UserNickName": "Viewer A",
                    "UserExternalId": "",
                    "CreateTime": 1717148059,
                    "Content": "Reply A",
                    "LikeCount": 20,
                    "IsPined": 0
                },
                {
                    "AnswerMsgId": 5941309,
                    "UserNickName": "Viewer B",
                    "UserExternalId": "",
                    "CreateTime": 1717145103,
                    "Content": "Reply B",
                    "LikeCount": 10,
                    "IsPined": 1
                }
            ],
            "5941306": [
                {
                    "AnswerMsgId": 5941308,
                    "UserNickName": "Viewer C",
                    "UserExternalId": "",
                    "CreateTime": 1717145064,
                    "Content": "Reply C",
                    "LikeCount": 15,
                    "IsPined": 0
                }
            ]
        }
    }
}
```


<span id="6ccfa3f6"></span>
## 錯誤碼

如需通用錯誤碼列表，請參見[常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/chang-jian-cuo-wu-yu-zhuang-tai-ma-zh-TW)。
