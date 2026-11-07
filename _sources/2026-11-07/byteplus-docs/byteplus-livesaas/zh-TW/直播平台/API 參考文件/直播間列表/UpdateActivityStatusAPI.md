---
title: "UpdateActivityStatusAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-updateactivitystatusapi-zh-TW"
---

更新直播間的狀態。您可以將直播間恢復至**預覽**狀態、鎖定預覽，以及解除預覽鎖定。

<span id="bdc66057"></span>
## 限制

配額：每個帳戶每分鐘最多 120 次查詢

<span id="8ca2b6a5"></span>
## HTTP 請求


* URL：`https://livesaas.byteplusapi.com/?Action=UpdateActivityStatusAPI&Version=2020-06-01`

* 方法：POST


<span id="13052e60"></span>
## 請求參數

以下表格未包含所有共用請求參數。完整列表請參見[共用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/gong-yong-can-shu-zh-TW#f1706967)。

<span id="62c1343f"></span>
### 查詢


|名稱 |資料型別 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`UpdateActivityStatusAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。值為`2020-06-01`。 |


<span id="Body parameters"></span>
### Body


|名稱 |資料型別 |必填 |範例值 |說明 |
|---|---|---|---|---|
|ActivityId |Long |是 |`17218346****` |直播間的活動 ID。您可以透過呼叫[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-TW)取得 ID。 |
|IsStreamViewEnable |Integer |是 |`4` |指定您要執行的操作。<br><br>有效值：<br><br><br>* `3`：將直播間恢復至**預覽**狀態。<br><br>* `4`：鎖定預覽。觀看頁面將被鎖定於**預覽**狀態，且不會播放直播影片或回放。<br><br>* `5`：解除預覽鎖定。觀看頁面即可播放直播影片及回放。 |


<span id="c12dbcce"></span>
## 回應參數


|名稱 |資料型別 |範例值 |說明 |
|---|---|---|---|
|ActivityId |Long |`-` |已棄用。 |
|ActivityIdStr |String |`-` |已棄用。 |
|Status |Integer |`-` |已棄用。 |


<span id="69439ad1"></span>
## 範例

<span id="6663a6da"></span>
### 範例請求

```JSON
POST https://livesaas.byteplusapi.com/?Action=UpdateActivityStatusAPI&Version=2020-06-01
{    
    "ActivityId": 17218346****,
    "IsStreamViewEnable": 4
}
```


<span id="Response"></span>
### 範例回應

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "UpdateActivityStatusAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1696235450
    },
    "Result": {
        "ActivityId": 0,
        "ActivityIdStr": "",
        "Status": 0
    }
}
```


<span id="977bc201"></span>
## 錯誤碼

共用錯誤碼列表請參見[常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/chang-jian-cuo-wu-yu-zhuang-tai-ma-zh-TW)。
