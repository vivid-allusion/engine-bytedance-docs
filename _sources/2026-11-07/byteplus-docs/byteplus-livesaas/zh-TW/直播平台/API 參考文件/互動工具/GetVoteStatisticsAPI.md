---
title: "GetVoteStatisticsAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/GetVoteStatisticsAPI-zh-TW"
---

呼叫 `GetVoteStatisticsAPI` 以獲取直播間的投票數據。

<span id="Requirements"></span>
## 需求


* 配額：每個帳戶每分鐘最多 120 次查詢。

* 前提條件：需有 BytePlus 帳戶，或具備 **Insights** \> **僅查看** 或 **編輯** 權限的 IAM 使用者。如需瞭解如何新增 IAM 使用者，請參閱 [管理使用者、組織和角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：GET

* 端點：https://livesaas.byteplusapi.com/?Action=GetVoteStatisticsAPI&Version=2020\-06\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

以下表格未包含所有通用請求參數。完整列表請參閱 [通用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`GetVoteStatisticsAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。目前版本：`2020-06-01`。 |
|ActivityId |Long |是 |17218346\*\*\*\* |直播間的活動 ID。可透過呼叫 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) 獲取該 ID。 |
|PageNo |Integer |否 |1 |要返回的頁碼。預設值：`1`。 |
|PageCount |Integer |否 |10 |每頁返回的結果數量。預設值：`10`。 |
|VoteId |String |是 |vote1754472505032763 |投票 ID。可透過呼叫 [GetVoteListAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/GetVoteListAPI) 獲取投票 ID。 |


<span id="Response parameters"></span>
## 回應參數


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|PageNo |Integer |1 |要返回的頁碼。 |
|PageCount |Integer |10 |每頁返回的結果數量。 |
|TotalCount |Integer |1 |總條目數。 |
|VoteStatisticsList |Array of[VoteStatisticsList](https://docs.byteplus.com/docs/byteplus-livesaas/GetVoteStatisticsAPI-zh-TW#votestatisticslist) |*  |投票者資訊列表。 |


<span id="votestatisticslist"></span>
### VoteStatisticsList


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|UserChose |Array of[UserChose](https://docs.byteplus.com/docs/byteplus-livesaas/GetVoteStatisticsAPI-zh-TW#userchose) |*  |使用者所選的選項。 |
|UserName |String |Audience A |觀眾暱稱。 |
|IP |String |10.5.xx.xx |觀眾的 IP 位址。 |
|VoteTime |Integer |1673169500 |投票時間，Unix 時間戳。 |
|Extra |String |abc |同步至 BytePlus Live 的額外參數，可用於與觀眾關聯。例如，可將觀眾的部門從自有帳戶系統同步至 BytePlus Live。 |
|UserID |Long |1738686737584142 |觀眾在 BytePlus Live 的唯一識別碼。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若觀眾未以暱稱或其他方式登入直播間，其用戶 ID 為 0。</div><br> |
|UserTel |String |137xxxxx88 |觀眾的電話號碼。 |
|Email |String |zhibo@xxx.com |觀眾的電子郵件。 |
|UserAgent |String |Intel Mac OS X 10_15_7 |觀眾裝置的 user agent 字串。 |
|ExternalId |String |1605756488530014 |觀眾在第三方平台的唯一識別碼。支援模糊搜尋。<br><br>該 ID 會根據觀眾登入直播間的方式而有所不同。如需更多資訊，請參閱 [觀眾行為數據](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-data-statistics#viewer-behavior-data)。可使用此 ID 在組織內識別觀眾，並根據需求進行用戶洞察與數據分析。 |


<span id="userchose"></span>
### UserChose


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|OptionSite |String |D |所選選項的識別碼。 |
|OptionName |String |選項內容 |所選選項的文字內容。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetVoteStatisticsAPI&Version=2020-06-01&ActivityId=17218346****&PageNo=1&PageCount=10&VoteId=vote1754472505032763
```


<span id="Sample response"></span>
### 範例回應

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetVoteStatisticsAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "PageNo": 1,
        "PageCount": 10,
        "TotalCount": 1,
        "VoteStatisticsList": [
            {
                "UserChose": [
                    {
                        "OptionSite": "D",
                        "OptionName": "Option content"
                    }
                ],
                "UserName": "Audience A",
                "IP": "10.5.xx.xx",
                "VoteTime": 1673169500,
                "Extra": "abc",
                "UserID": 1738686737584142,
                "UserTel": "137xxxxx88",
                "Email": "zhibo@xxx.com",
                "UserAgent": "Intel Mac OS X 10_15_7",
                "ExternalId": "1605756488530014"
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

常見錯誤碼列表請參閱 [常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
