---
title: "ResumeLiveStreamAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-resumelivestreamapi-zh-TW"
---

呼叫此 API 以恢復直播間中特定直播來源被禁止的串流。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">若要在恢復串流後再次禁止串流，請確保於呼叫此 API 操作後至少 30 秒再呼叫 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-forbidlivestreamapi-zh-TW">ForbidLiveStreamAPI</a>。</div>


<span id="02ad6c5d"></span>
## 需求

配額：每個帳戶每分鐘最多 120 次查詢

<span id="7ba7eaf9"></span>
## HTTP 請求


* URL：`https://livesaas.byteplusapi.com/?Action=ResumeLiveStreamAPI&Version=2020-06-01`

* 方法：POST


<span id="Request"></span>
## 請求參數

以下表格未包含所有共用請求參數。完整列表請參見 [共用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/gong-yong-can-shu-zh-TW#f1706967)。

<span id="Query string parameters"></span>
### 查詢


|名稱 |資料型別 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`ResumeLiveStreamAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。目前版本：`2020-06-01`。 |


<span id="52a59104"></span>
### Body


|名稱 |資料型別 |必填 |範例值 |說明 |
|---|---|---|---|---|
|ActivityId |Integer |是 |`17218312****` |直播間的活動 ID。可透過呼叫 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-TW) 取得此 ID。 |
|LineId |Integer 陣列 |否 |`[356218,356219]` |欲恢復串流的直播來源 ID。若未指定，則直播間所有來源的串流皆會被恢復。<br><br>一個直播間可擁有多個來源，每個來源都有自己的串流。可透過呼叫 [GetStreamsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getstreamsapi-zh-TW) 取得直播間的來源 ID。 |


<span id="96806707"></span>
## 回應參數


|名稱 |資料型別 |範例值 |說明 |
|---|---|---|---|
|Status |Boolean |`true` |表示指定的串流是否已恢復。<br><br><br>* `true`：所有指定的串流皆已恢復。<br><br>* `false`：至少有一個指定的串流未被恢復。 |


<span id="d9dbb92a"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```JSON
POST https://livesaas.byteplusapi.com/?Action=ResumeLiveStreamAPI&Version=2020-06-01
{
    "ActivityId": 17218312****,
    "LineId": [356218,356219]
}
```


<span id="Sample response"></span>
### 範例回應

```JSON
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "ResumeLiveStreamAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1662570420
    },
    "Result": {
        "Status": true
    }
}
```


<span id="e4fa63d6"></span>
## 錯誤碼

下表列出此 API 操作專屬的錯誤碼。通用錯誤碼請參見 [常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/chang-jian-cuo-wu-yu-zhuang-tai-ma-zh-TW)。


|狀態碼 |錯誤碼 |錯誤訊息 |說明 |
|---|---|---|---|
|200 |200027 |無法恢復因啟用直播串流開始時間或結束時間功能而被禁止的串流。要恢復此類串流，必須先停用這些功能。 |請在 BytePlus Live 控制台或透過呼叫 [UpdateActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitybasicconfigapi-zh-TW) 停用「直播串流開始時間」及「結束時間」功能。 |
