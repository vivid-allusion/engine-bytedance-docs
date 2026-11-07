---
title: "GetStreamsAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getstreamsapi-zh-TW"
---

呼叫此 API 以取得推流至直播間所需的資訊，或將第三方平台的流拉入直播間指定直播頻道的相關資訊。

<span id="578daba1"></span>
## 需求

配額: 每個帳戶每分鐘最多 120 次查詢

<span id="364b7b23"></span>
## HTTP 請求


* URL: `https://livesaas.byteplusapi.com/?Action=GetStreamsAPI&Version=2020-06-01`

* 方法: GET


<span id="3d09167d"></span>
## 請求參數

下列表格未包含所有共用請求參數。完整列表請參見 [共用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/gong-yong-can-shu-zh-TW#f1706967)。

<span id="Request"></span>
### 查詢


|名稱 |資料型態 |必填 |範例值 |描述 |
|---|---|---|---|---|
|Action |String |是 |`GetStreamsAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。目前版本: `2020-06-01`。 |
|ActivityId |Long |是 |`17218312****` |直播間的活動 ID。可透過呼叫 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-TW) 取得此 ID。 |


<span id="b66364d9"></span>
## 回應參數


|名稱 |資料型態 |範例值 |描述 |
|---|---|---|---|
|LineDetails |Array of[LineDetails](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getstreamsapi-zh-TW#f877cb2c) |`-` |直播頻道資訊。 |


<span id="f877cb2c"></span>
### LineDetails


|名稱 |資料型態 |範例值 |描述 |
|---|---|---|---|
|LineId |Long |`3606624` |頻道 ID。 |
|LineName |String |`Default` |頻道名稱。 |
|MainPushInfo |Array of[MainPushInfo](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getstreamsapi-zh-TW#f62ab0e8) |`-` |推送主流至直播間的資訊。 |
|BackPushInfo |Array of[BackPushInfo](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getstreamsapi-zh-TW#8920920f) |`-` |用於推流至直播間的備用流資訊。 |
|Ratio |String |`1280x720` |頻道解析度。 |
|ForwardInfo |Array of[ForwardInfo](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getstreamsapi-zh-TW#e7498454) |`-` |從第三方平台拉主流至直播間的資訊。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">拉流任務自啟動後有效期為 48 小時。</div><br> |
|BackupForwardInfo |Array of[BackupForwardInfo](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getstreamsapi-zh-TW#18271609) |`-` |用於從第三方平台拉流至直播間的備用流資訊。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">拉流任務自啟動後有效期為 48 小時。</div><br> |
|ExpireTime |Long |`1697167355` |推流地址的過期時間（Unix 時間戳記格式）。單位為秒。 |


<span id="f62ab0e8"></span>
### MainPushInfo


|名稱 |資料型態 |範例值 |描述 |
|---|---|---|---|
|PushPath |String |`rtmps://push-rtmp-l1-act.****.com/live/` |伺服器 URL。 |
|PushUrl |String |`rtmps://push-rtmp-l1-act.****.com/live/stream-2421148009386476461?keeptime=00093a80&wsSecret=7c23ee8c864b672d4f****2d30c1a94b&wsTime=66695334` |推流地址。 |
|StreamingCode |String |`stream-2421148009386476461?keeptime=00093a80&wsSecret=7c23ee8c864b672d4f****2d30c1a94b&wsTime=66695334` |串流金鑰。 |


<span id="8920920f"></span>
### BackPushInfo


|名稱 |資料型態 |範例值 |描述 |
|---|---|---|---|
|PushPath |String |`rtmps://push-rtmp-f5-act.****.com/live/` |伺服器 URL。 |
|PushUrl |String |`rtmps://push-rtmp-f5-act.****.com/live/stream-2421148009386476461?keeptime=00093a80&wsSecret=7c23ee8c864b672d4f****2d30c1a94b&wsTime=66695334` |推流地址。 |
|StreamingCode |String |`stream-2421148009386476461?keeptime=00093a80&wsSecret=7c23ee8c864b672d4f****2d30c1a94b&wsTime=66695334` |串流金鑰。 |


<span id="e7498454"></span>
### ForwardInfo


|名稱 |資料型態 |範例值 |描述 |
|---|---|---|---|
|PullStreamUrl |String |`https://example/livesaas?key=example` |主串流 URL。 |
|PullStreamStatus |String |`0` |拉流任務狀態。狀態會在呼叫 [UpdatePullToPushAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updatepulltopushapi-zh-TW) 啟動或停止拉流後變更。<br><br><br>* `0`: 初始化中。<br><br>* `1`: 進行中。<br><br>* `2`: 已完成。 |
|PullStreamCheckStatus |String |`0` |拉流檢查狀態。<br><br><br>* `0`: 檢查中。<br><br>* `1`: 來源流未推送。<br><br>* `2`: 拉流成功。<br><br>* `3`: 拉流結束。<br><br>* `4`: 拉流錯誤。 |


<span id="18271609"></span>
### BackupForwardInfo


|名稱 |資料型態 |範例值 |描述 |
|---|---|---|---|
|PullStreamUrl |String |`https://example/livesaas?key=example` |備用串流 URL。 |
|PullStreamStatus |String |`0` |拉流任務狀態。狀態會在呼叫 [UpdatePullToPushAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updatepulltopushapi-zh-TW) 啟動或停止拉流後變更。<br><br><br>* `0`: 初始化中。<br><br>* `1`: 進行中。<br><br>* `2`: 已完成。 |
|PullStreamCheckStatus |String |`0` |拉流檢查狀態。<br><br><br>* `0`: 檢查中。<br><br>* `1`: 來源流未推送。<br><br>* `2`: 拉流成功。<br><br>* `3`: 拉流結束。<br><br>* `4`: 拉流錯誤。 |


<span id="2bd43b1a"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetStreamsAPI&Version=2020-06-01&ActivityId=17218312****
```


<span id="Sample response"></span>
### 範例回應

```JSON
{
    "ResponseMetadata":{
        "RequestId":"202201201826170101501312091D1C09D2",
        "Action":"GetStreamsAPI",
        "Version":"2020-06-01",
        "Service":"livesaas",
        "Region":"ap-singapore-1",
        "SystemTime":1697163541        
   },
  "Result": {
    "LineDetails": [
      {
        "LineId": 3606624,
        "ExpireTime": 1697167355,
        "MainPushInfo": {
          "PushUrl": "rtmps://push-rtmp-l1-act.****.com/live/stream-2421148009386476461?keeptime=00093a80&wsSecret=7c23ee8c864b672d4f****2d30c1a94b&wsTime=66695334",
          "PushPath": "rtmps://push-rtmp-l1-act.****.com/live/",
          "StreamingCode": "stream-2421148009386476461?keeptime=00093a80&wsSecret=7c23ee8c864b672d4f****2d30c1a94b&wsTime=66695334"
        },
        "BackPushInfo": {
          "PushPath": "rtmps://push-rtmp-f5-act.****.com/live/",
          "StreamingCode": "stream-2421148009386476461?keeptime=00093a80&wsSecret=7c23ee8c864b672d4f****2d30c1a94b&wsTime=66695334",
          "PushUrl": "rtmps://push-rtmp-f5-act.****.com/live/stream-2421148009386476461?keeptime=00093a80&wsSecret=7c23ee8c864b672d4f****2d30c1a94b&wsTime=66695334"
        },
        "ForwardInfo": {
          "PullStreamUrl": "https://example/livesaas?key=example",
          "PullStreamStatus": 0,
          "PullStreamCheckStatus": 0
        },
        "LineName": "Default",
        "BackupForwardInfo": {
          "PullStreamUrl": "https://example/livesaas?key=example",
          "PullStreamStatus": 0,
          "PullStreamCheckStatus": 0
        },
        "Ratio": "1280x720"
      }
    ]
  }
}
```
