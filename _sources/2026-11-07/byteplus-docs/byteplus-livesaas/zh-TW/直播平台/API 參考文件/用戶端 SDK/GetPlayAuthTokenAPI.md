---
title: "GetPlayAuthTokenAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getplayauthtokenapi-zh-TW"
---

調用此 API 以獲取初始化 Web Player SDK 所需的播放權杖。

<span id="Request"></span>
## 請求

<span id="Details"></span>
### 詳細資訊


* API 操作：`GetPlayAuthTokenAPI`

* 請求方法：POST

* 請求 URI：`https://livesaas.byteplusapi.com/?Action=GetPlayAuthTokenAPI&Version=2020-06-01`

* 配額：每個帳號每分鐘 120 次查詢


<span id="Query string parameters"></span>
### 查詢字串參數

下表未包含所有共用請求參數。如需完整列表，請參見[共用請求參數](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**參數名稱** |**是否必填** |**資料型別** |**說明** |
|---|---|---|---|
|Action |是 |String |API 操作名稱。 |
|Version |是 |String |此 API 操作的版本。目前版本：2020\-06\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數名稱** |**是否必填** |**資料型別** |**說明** |
|---|---|---|---|
|Vid |是 |String |要播放的影片 ID。 |
|FormatType |是 |String |要播放的影片格式。<br><br><br>* 若需在 iOS 上播放影片，請將`FormatType`設為`hls`。<br><br>* 否則，請將`FormatType`設為`mp4`。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">建議不要在 Android 裝置上播放 HLS 影片。</div><br> |
|ActivityId |是 |Integer |直播活動 ID。 |


<span id="Sample request"></span>
### 請求範例

```JSON
POST https://livesaas.byteplusapi.com/?Action=GetPlayAuthTokenAPI&Version=2020-06-01
{
    "Vid": "v10a05g50000ccojp2bc77ua104s****", 
    "ActivityId": 170453116614****,
    "FormatType": "mp4"
}
```


<span id="Response"></span>
## 回應

<span id="Response schema"></span>
### 回應結構


|**參數名稱** |**資料型別** |**說明** |
|---|---|---|
|PlayAuthToken |String |播放權杖。 |
|ActivityId |Integer |直播活動 ID。 |


<span id="Sample response"></span>
### 回應範例

以下範例顯示成功的回應：

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202209271353310102511970410027****",
        "Action": "GetPlayAuthTokenAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1664286811
    },
    "Result": {
        "PlayAuthToken": "xxxxxx",
        "ActivityId": 170453116614****
    }
}
```
