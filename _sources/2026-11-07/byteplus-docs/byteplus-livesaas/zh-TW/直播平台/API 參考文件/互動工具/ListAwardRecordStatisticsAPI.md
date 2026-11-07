---
title: "ListAwardRecordStatisticsAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/ListAwardRecordStatisticsAPI-zh-TW"
---

呼叫 `ListAwardRecordStatisticsAPI` API，以取得直播間中特定抽獎活動的參與或中獎觀眾名單。

<span id="Requirements"></span>
## 需求


* 頻率限制：每個帳戶每秒最多 10 次請求

* 前提條件：需有 BytePlus 帳戶，或具備 **Insights** \> **僅檢視** 或 **編輯**權限的 IAM 使用者。如需新增 IAM 使用者的詳細資訊，請參閱 [管理使用者、組織與角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：GET

* 端點：https://livesaas.byteplusapi.com/?Action=ListAwardRecordStatisticsAPI&Version=2023\-08\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

下表未包含所有通用請求參數。完整列表請參閱 [通用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`ListAwardRecordStatisticsAPI` |API 操作。 |
|Version |String |是 |`2023-08-01` |此 API 操作的版本。目前版本：`2023-08-01`。 |
|ActivityId |Long |是 |1798615803\*\*\*\* |直播間活動 ID。可透過呼叫 [ListAwardConfigs](https://docs.byteplus.com/docs/byteplus-livesaas/ListAwardConfigs) 取得此 ID。 |
|SearchType |Integer |否 |1 |觀眾名單類型。支援以下值，預設值為 `0`。<br><br><br>* `0`：參與觀眾名單<br><br>* `1`：中獎觀眾名單 |
|AwardId |Long |是 |1621615169 |抽獎活動 ID。可透過呼叫 [ListAwardConfigs](https://docs.byteplus.com/en/docs/byteplus-livesaas/ListAwardConfigs) 查詢此 ID。 |
|PageNo |Integer |否 |1 |要返回的頁碼。預設值：`1`。 |
|PageItemCount |Integer |否 |10 |每頁返回的結果數量。預設值：`10`。值範圍為 [1, 500]。 |


<span id="Response parameters"></span>
## 回應參數


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|AwardRecords |Array of[AwardRecords](https://docs.byteplus.com/docs/byteplus-livesaas/ListAwardRecordStatisticsAPI-zh-TW#awardrecords) |*  |觀眾資訊列表。 |
|PageNo |Integer |1 |返回結果的頁碼。 |
|PageItemCount |Integer |10 |每頁返回的結果數量。 |
|PageTotalCount |Integer |1 |查詢結果總數。 |


<span id="awardrecords"></span>
### AwardRecords


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|ActivityId |Integer |17218346\*\*\*\* |直播間活動 ID。 |
|AwardId |Long |1621615169 |抽獎活動 ID。 |
|UserId |String |1753988749\*\*\*\* |使用者 ID。 |
|UserName |String |Audience A |使用者暱稱。 |
|LoginTel |String |158xxxx66 |觀眾登入時使用的手機號碼。 |
|AwardAddress |String |北京 |收件人地址。 |
|AwardResult |Integer |4 |觀眾抽獎結果。支援以下值：<br><br><br>* `4`：中獎<br><br>* `5`：未中獎 |
|NotifyResult |Integer |1 |表示觀眾是否已被通知抽獎結果。支援的值如下：<br><br><br>* `1`：未通知<br><br>* `2`：已通知 |
|ExternalId |String |160575648853\*\*\*\* |觀眾在第三方平台的唯一識別碼。支援模糊搜尋。<br><br>此 ID 會根據觀眾登入直播間的方式而有所不同。更多資訊請參閱 [觀眾行為數據](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-data-statistics#viewer-behavior-data)。您可使用此 ID 在組織內識別觀眾，進行用戶洞察與數據分析。 |
|AwardName |String |lucky draw event |抽獎活動名稱。 |
|ReceiverName |String |Li |收件人姓名。 |
|ReceiverTel |String |157xxxx66 |收件人手機號碼。 |
|Email |String |zhibo@xxx.com |觀眾在註冊帳戶時提供的電子郵件地址。 |
|OpenAwardTime |Integer |1673199158 |抽獎結果公布時間，採用 Unix 時間戳（秒）。 |
|Extra |String |abc |一個可與觀眾關聯的額外參數，同步至 BytePlus Live。例如，你可以將觀眾的部門從你自己的帳戶系統同步至 BytePlus Live。 |
|UserAgent |String |Intel Mac OS X 10_15_7 |觀眾裝置的 user agent 字串。 |
|Ip |String |192.0.2.1 |觀眾的 IP 位址。 |
|IsPriorityUser |Integer |1 |用戶是否具有優先獲獎資格。有效值如下：<br><br><br>* `0`: 否<br><br>* `1`: 是 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```JSON
GET https://livesaas.byteplusapi.com/?Action=ListAwardRecordStatisticsAPI&Version=2023-08-01&ActivityId=1798615803****&SearchType=1&AwardId=1621615169&PageNo=1&PageItemCount=10
```


<span id="Sample response"></span>
### 回應範例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListAwardRecordStatisticsAPI",
        "Version": "2023-08-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "PageNo": 1,
        "PageItemCount": 10,
        "PageTotalCount": 1,
        "AwardRecords": [
            {
                "ActivityId": 17218346,
                "UserName": "Audience A",
                "LoginTel": "158xxxx66",
                "AwardAddress": "Beijing",
                "AwardResult": 4,
                "NotifyResult": 1,
                "ExternalId": "160575648853****",
                "AwardName": "lucky draw event",
                "ReceiverName": "Li",
                "ReceiverTel": "157xxxx66",
                "Email": "zhibo@xxx.com",
                "OpenAwardTime": 1673199158,
                "Extra": "abc",
                "UserAgent": "Intel Mac OS X 10_15_7",
                "Ip": "192.0.2.1",
                "IsPriorityUser": 1,
                "AwardId": 1621615169,
                "UserId": "1753988749****"
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

常見錯誤碼請參閱 [常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
