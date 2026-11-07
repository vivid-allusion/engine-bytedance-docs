---
title: "GetCheckInRecordStatisticsAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/GetCheckInRecordStatisticsAPI-zh-TW"
---

呼叫 `GetCheckInRecordStatisticsAPI` 以取得特定直播間的簽到記錄。

<span id="Requirements"></span>
## 需求


* 配額：每個帳戶每分鐘最多 120 次查詢。

* 前提條件：需有 BytePlus 帳戶，或具備 **Insights** \> **View only** 或 **Edit** 權限的 IAM 使用者。如需新增 IAM 使用者的詳細資訊，請參閱 [管理使用者、組織與角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：GET

* 端點：https://livesaas.byteplusapi.com/?Action=GetCheckInRecordStatisticsAPI&Version=2020\-06\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

下表並未包含所有通用請求參數。完整列表請參閱 [通用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`GetCheckInRecordStatisticsAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |本 API 操作的版本。目前版本：`2020-06-01`。 |
|ActivityId |Long |是 |17218346\*\*\*\* |直播間的活動 ID。可透過呼叫 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) 取得此 ID。 |
|PageNo |Integer |否 |1 |要返回的頁碼。預設值：`1`。 |
|PageItemCount |Integer |否 |`10` |每頁返回的結果數量。預設值：`10`。 |
|CheckInId |String |是 |`checkIn1754478641140752` |直播間的簽到 ID。可透過呼叫 GetCheckInListAPI 取得此 ID。 |


<span id="Response parameters"></span>
## 回應參數


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|CheckInStatisticsList |Array of[CheckInStatisticsList](https://docs.byteplus.com/docs/byteplus-livesaas/GetCheckInRecordStatisticsAPI-zh-TW#checkinstatisticslist) |`-` |已簽到觀眾的資訊列表。 |
|PageNo |Integer |1 |要返回的頁碼。 |
|PageItemCount |Integer |10 |每頁返回的結果數量。 |
|PageTotalCount |Integer |1 |查詢結果總數。 |


<span id="checkinstatisticslist"></span>
### CheckInStatisticsList


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|ActivityId |Long |17218346\*\*\*\* |直播間的活動 ID。 |
|CheckInID |String |`checkIn1754478641140752` |簽到 ID。 |
|UserID |Long |173868673758\*\*\*\* |觀眾 ID。 |
|UserName |String |`aa` |觀眾暱稱。 |
|LoginTel |String |`158xxxx66` |觀眾登入所用的手機號碼。 |
|Email |String |zhibo@xxx.com |觀眾的電子郵件。 |
|CheckInTime |Integer |`1673202796` |觀眾簽到時間，Unix 時間戳（秒）。 |
|PersonInfo |String |`aa` |觀眾簽到資訊。 |
|Extra |String |abc |同步至 BytePlus Live 的額外參數，可與觀眾建立關聯。例如，您可以將觀眾的部門從自有帳戶系統同步至 BytePlus Live。 |
|UserAgent |String |Intel Mac OS X 10_15_7 |觀眾裝置的 user agent 字串。 |
|Ip |String |192.0.2.1 |簽到直播間觀眾的 IP 位址。 |
|ExternalId |String |160575648853\*\*\*\* |觀眾在第三方平台上的唯一識別碼。支援模糊搜尋。<br><br>此 ID 會依觀眾登入直播間的方式而有所不同。更多資訊請參閱 [觀眾行為數據](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-data-statistics#viewer-behavior-data)。您可以使用此 ID 在組織內識別觀眾，進行用戶洞察與數據分析。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetCheckInRecordStatisticsAPI&Version=2020-06-01&ActivityId=17218346****&PageNo=1&PageItemCount=10&CheckInId=checkIn1754478641140752
```


<span id="Sample response"></span>
### 回應範例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetCheckInRecordStatisticsAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "CheckInStatisticsList": [
            {
                "ActivityId": 17218346****,
                "CheckInID": "checkIn1754478641140752",
                "UserID": 173868673758****,
                "UserName": "aa",
                "LoginTel": "158xxxx66",
                "Email": "zhibo@xxx.com",
                "CheckInTime": 1673202796,
                "PersonInfo": "aa",
                "Extra": "abc",
                "UserAgent": "Intel Mac OS X 10_15_7",
                "Ip": "192.0.2.1",
                "ExternalId": "160575648853****"
            }
        ],
        "PageNo": 1,
        "PageItemCount": 10,
        "PageTotalCount": 1
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

下表列出本 API 操作專屬的錯誤碼。通用錯誤碼請參閱 [通用錯誤與狀態碼](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|400 |InvalidParameter.ActivityIDInvalid |指定的參數 ActivityID 無效。 |無效的直播間 ID。請輸入有效的 ID 並重新嘗試。可透過呼叫 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) 取得此 ID。 |
|500 |InternalError |請求因未知錯誤而失敗。 |處理請求時發生未知錯誤。請聯絡技術支援以取得協助。 |
