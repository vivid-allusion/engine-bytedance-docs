---
title: "GetActivityReservationAPIV2"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/GetActivityReservationAPIV2-zh-TW"
---

取得特定直播間的預約資訊。

&nbsp;

<span id="Requirements"></span>
## 需求

配額：每個帳戶每分鐘最多 120 次查詢

<span id="HTTP request"></span>
## HTTP 請求


* 方法：GET

* 端點：https://livesaas.byteplusapi.com/?Action=GetActivityReservationAPIV2&Version=2020\-06\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

下表並未包含所有通用請求參數。完整列表請參見[通用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`GetActivityReservationAPIV2` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。目前版本：`2020-06-01`。 |
|ActivityId |Long |是 |`1779187158280` |直播間的活動 ID。可透過呼叫[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi)取得 ID。 |
|Page |Integer |否 |`1` |要回傳的頁碼。預設值：`1`。 |
|PageSize |Integer |否 |`10` |每頁回傳的結果數量。預設值：`10`。數值範圍：[1,500]。 |
|Channel |String |否 |`123` |將回傳指定頻道識別碼的頻道資料。預設會回傳所有頻道的資料。你可以在[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)的直播間的**行銷工具組** \> **頻道**頁面取得頻道識別碼。 |
|TelReserve |String |否 |`182****5709` |預約直播所使用的電話號碼。 |
|NickName |String |否 |`Viewer A` |預約直播的觀眾暱稱。支援模糊搜尋。 |
|ExternalId |String |否 |`1234` |觀眾在第三方平台上的唯一識別碼。支援模糊搜尋。<br><br>ID 會根據觀眾進入直播間的方式而有所不同。更多資訊請參見[觀眾行為資料](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-data-statistics#viewer-behavior-data)。你可以使用此 ID 在你的組織內識別觀眾身分，以便進行用戶洞察與資料分析。 |


<span id="Response parameters"></span>
## 回應參數


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|ActivityId |Long |`1779187158280` |直播間的活動 ID。 |
|Total |Integer |`1` |回傳結果總數。 |
|Page |Integer |`1` |回傳頁碼。 |
|Items |[Items](https://docs.byteplus.com/en/docs/11/113517#items) 陣列 |`-` |觀眾預約資訊列表。 |


<span id="items"></span>
### 項目


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|NickName |String |`Viewer A` |觀眾暱稱。 |
|TelReserve |String |`182****5709` |預約直播所使用的電話號碼。 |
|Ip |String |`192.168.0.1` |觀眾的 IP 位址。 |
|IpAddress |String |`北京` |IP 位址所屬區域。 |
|SubmitTime |Integer |`1697080167` |觀眾預約直播的時間，Unix 時間戳格式。單位：秒。 |
|UserDevice |String |`Windows 10` |觀眾進入直播間所使用的裝置類型。 |
|ExternalId |String |`31210506554471` |觀眾在第三方平台上的唯一識別碼。你可以使用此 ID 在你的組織內識別觀眾身分，以便進行用戶洞察與資料分析。 |
|Extra |String |`abc` |額外參數。 |
|Channel |String |`123` |頻道識別碼。 |
|UserId |Long |`1744663139363934` |用戶 ID，即觀眾在 BytePlus Live 的唯一識別碼。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
GET https://livesaas.byteplusapi.com/?Action=GetActivityReservationAPIV2&Version=2020-06-01&ActivityId=1779****58280&Page=1&PageSize=10&Channel=123&TelReserve=182****5709
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetActivityReservationAPIV2",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697080180
    },
    "Result": {
        "ActivityId": 1779****58280,
        "Total": 1,
        "Page": 1,
        "Items": [
            {
                "NickName": "Viewer A",
                "UserId": 174466****363934,
                "Channel": "123",
                "Extra": "abc",
                "ExternalId": "31210****54471",
                "UserDevice": "Windows 10",
                "SubmitTime": 1697080167,
                "IpAddress": "Beijing",
                "Ip": "192.*.*.1",
                "TelReserve": "182****5709"
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

常見錯誤碼列表請參見[常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
