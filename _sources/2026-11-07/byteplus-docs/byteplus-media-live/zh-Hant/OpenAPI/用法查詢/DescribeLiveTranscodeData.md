---
title: "DescribeLiveTranscodeData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivetranscodedata-zh-TW"
---

調用 `DescribeLiveTranscodeData` API，以查詢指定直播域名在特定時間範圍內的轉碼時長用量。

<span id="Requirements"></span>
## 需求


* 計費：有關轉碼價格，請參閱 [Transcoding](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-transcoding)。

* 限制：支持查詢指定域名（包含已刪除域名）產生的轉碼總時長。

* 頻率限制：每個帳戶每秒最多查詢 30 次

* 數據延遲：20 分鐘


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeLiveTranscodeData&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 在調用時，除需傳入 API 專屬參數外，還需包含 [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**數據類型** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveTranscodeData` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。當前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**數據類型** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|DomainList |Array of String |否 |`["push.example.com","push2.example.com"]` |域名列表。預設為空，表示將查詢你 BytePlus MediaLive 下所有域名的轉碼用量數據。你可調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail) API，或前往 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面獲取需查詢的域名。 |
|App |String |否 |`live` |直播流 URL 中的 AppName 欄位。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及點（.），長度為 1 至 30 字元。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">查詢流粒度數據時，需同時傳入 <code>App</code> 和 <code>Stream</code> 參數。</div><br> |
|Stream |String |否 |`example_stream` |直播流 URL 中的 StreamName 欄位。可包含大寫及小寫字母（A\-Z, a\-z）、數字（0\-9）、底線（_）、連字號（\-）及點（.），長度為 1 至 100 字元。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">查詢流粒度數據時，必須同時提供 <code>App</code> 和 <code>Stream</code> 參數。</div><br> |
|TranscodeType |Array of String |否 |`["Normal_H264","ByteHD_H265"]` |視頻編碼格式：若留空，則不指定特定編碼格式。支持的值如下：<br><br><br>* `Normal_H264`：H.264。<br><br>* `Normal_H265`：H.265。<br><br>* `Normal_H266`：H.266。<br><br>* `ByteHD_H264`：低碼率高清模式下的 H.264。<br><br>* `ByteHD_H265`：低碼率高清模式下的 H.265。<br><br>* `ByteHD_H266`：低碼率高清模式下的 H.266。<br><br>* `Audio`：純音頻流。 |
|Resolution |Array of String |否 |`["720P","1080P"]` |轉碼解析度層級為選填，預設不指定解析度。例如，選擇 `720P` 表示轉碼配置將針對面積（以長邊乘短邊計算）大於 `480P` 解析度（640x480），且不超過 `720P` 解析度（1280x720）的視頻。支持的值及其含義如下：<br><br><br>* `480P`：640 × 480；<br><br>* `720P`：1280 × 720；<br><br>* `1080P`：1920 × 1080；<br><br>* `2K`：2560 × 1440；<br><br>* `4K`：4096 × 2160；<br><br>* `8K`：大於 4096 x 2160；<br><br>* `0P`：純音頻轉碼，表示無視頻內容。 |
|StartTime |String |是 |`2021-04-13T00:00:00Z` |查詢範圍的開始時間，需以 RFC 3339 格式（精確到秒）填寫。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">單次查詢的最大時間跨度為93天，歷史查詢的最大時間範圍為366天。</div><br> |
|EndTime |String |是 |`2021-04-14T00:00:00Z` |查詢範圍的結束時間，採用RFC 3339格式，精確到秒。 |
|Aggregation |Integer |否 |`86400` |資料聚合時間粒度：資料聚合的單位，目前介面預設且僅支援以86400秒（1天）為間隔進行資料聚合。 |


<span id="Response parameters"></span>
## 回應參數

有關 API 專屬回應參數，請參見下表。更多詳情請參閱 [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|DomainList |Array of String |`["push.example.com","push2.example.com"]` |域名列表。 |
|App |String |`live` |查詢串流粒度資料時的AppName欄位。 |
|Stream |String |`example_stream` |查詢串流粒度資料時的StreamName欄位。 |
|TranscodeType |Array of String |`["Normal_H264","ByteHD_H265"]` |查詢的視頻編碼格式，支援以下值：<br><br><br>* `Normal_H264`：H.264。<br><br>* `Normal_H265`：H.265。<br><br>* `Normal_H266`：H.266。<br><br>* `ByteHD_H264`：低碼率高清模式下的H.264。<br><br>* `ByteHD_H265`：低碼率高清模式下的H.265。<br><br>* `ByteHD_H266`：低碼率高清模式下的H.266。<br><br>* `Audio`：純音訊流。 |
|Resolution |Array of String |`["720P","1080P"]` |查詢的轉碼解析度層級，支援以下值及對應像素尺寸：<br><br><br>* `480P`：640 × 480；<br><br>* `720P`：1280 × 720；<br><br>* `1080P`：1920 × 1088；<br><br>* `2K`：2560 × 1440；<br><br>* `4K`：4096 × 2160；<br><br>* `8K`：大於4096 × 2160；<br><br>* `0P`：純音訊轉碼，表示無視頻內容。 |
|StartTime |String |`2021-04-13T00:00:00Z` |查詢範圍的開始時間，採用RFC 3339格式，精確到秒。 |
|EndTime |String |`2021-04-14T00:00:00Z` |查詢範圍的結束時間，採用RFC 3339格式，精確到秒。 |
|Aggregation |Integer |`300` |資料粒度，以秒為單位。 |
|Duration |Float |`12.860403541550001` |指定時間範圍內的轉碼總時長，以分鐘為單位。 |
|TranscodeDataList |Array of [TranscodeDataList](https://docs.byteplus.com/en/docs/24/107392#transcodedatalist) |`-` |各粒度層級的全部資料：所有可用時間粒度層級的資料。 |


<span id="transcodedatalist"></span>
### TranscodeDataList


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|TranscodeType |String |`Normal_H264` |查詢的視頻編碼格式，支援以下值：<br><br><br>* `Normal_H264`：H.264。<br><br>* `Normal_H265`：H.265。<br><br>* `Normal_H266`：H.266。<br><br>* `ByteHD_H264`：低碼率高清模式下的H.264。<br><br>* `ByteHD_H265`：低碼率高清模式下的H.265。<br><br>* `ByteHD_H266`：低碼率高清模式下的H.266。<br><br>* `Audio`：純音訊流。 |
|Resolution |String |`720P` |查詢的轉碼解析度層級，支援以下值：<br><br><br>* `480P`：640 × 480；<br><br>* `720P`：1280 × 720；<br><br>* `1080P`：1920 × 1088；<br><br>* `2K`：2560 × 1440；<br><br>* `4K`：4096 × 2160；<br><br>* `8K`：大於4096 × 2160；<br><br>* `0P`：純音訊轉碼，表示無視頻內容。 |
|TimeStamp |String |`2022-04-13T00:00:00Z` |以時間粒度聚合資料時，每個時間粒度的開始時間，採用RFC3339 UTC時間格式，精確到秒。 |
|Duration |Float |`1.4475713543666666` |當前資料聚合時間粒度內的轉碼總時長，以分鐘為單位。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveTranscodeData&Version=2023-01-01
{
    "DomainList": [
        "push.example.com",
        "push2.example.com"
    ],
    "StartTime": "2021-04-13T00:00:00Z",
    "EndTime": "2021-04-14T00:00:00Z",
    "Aggregation": 86400
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "DescribeLiveTranscodeData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DomainList": [
            "push.example.com"
        ],
        "StartTime": "2021-04-13T00:00:00Z",
        "EndTime": "2021-04-14T00:00:00Z",
        "Aggregation": 86400,
        "Duration": 12.860403541550001,
        "TranscodeDataList": [
            {
                "Duration": 1.4475713543666666,
                "Resolution": "720P",
                "TimeStamp": "2022-03-07T00:00:00Z",
                "TranscodeType": "Normal_H264"
            },
            {
                "Duration": 11.412832187183334,
                "Resolution": "720P",
                "TimeStamp": "2022-03-08T00:00:00Z",
                "TranscodeType": "Normal_H264"
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為本操作相關的錯誤碼。其他錯誤碼請參見 [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**Status Code** |**Error Code** |**Error Message** |**Description** |
|---|---|---|---|
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考[Request Parameters](https://docs.byteplus.com/en/docs/24/107392#request-parameters)說明進行檢查。 |
|403 |RequestForbidden |*  |因當前帳戶下無請求資源（資源包括域名空間、域名、App名稱、配置及憑證），請求被拒絕。 |
|500 |InternalError |發生內部錯誤，請聯繫管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
