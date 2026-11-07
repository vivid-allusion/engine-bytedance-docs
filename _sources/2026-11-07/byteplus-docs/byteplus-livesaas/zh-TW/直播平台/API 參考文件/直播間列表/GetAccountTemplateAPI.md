---
title: "GetAccountTemplateAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getaccounttemplateapi-zh-TW"
---

調用此 API 以獲取您 BytePlus 帳戶下的直播間範本列表。然後，您可以找到已發佈範本的 ID，並使用該範本的配置來建立直播間。

<span id="2ca56b67"></span>
## 需求

配額：每個帳戶每分鐘 120 次查詢

<span id="974fd95c"></span>
## HTTP 請求


* URL：`https://livesaas.byteplusapi.com/?Action=GetAccountTemplateAPI&Version=2020-06-01`

* 方法：GET


<span id="ee806223"></span>
## 請求參數

下表未包含所有通用請求參數。完整列表請參見[共用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/gong-yong-can-shu-zh-TW#f1706967)。

<span id="34ed5072"></span>
### 查詢


|名稱 |資料型別 |是否必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`GetAccountTemplateAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。當前版本：`2020-06-01`。 |
|PageNo |Integer |否 |`1` |要返回的頁碼。<br><br>預設值：`1`。 |
|PageItemCount |Integer |否 |`10` |每頁返回的結果數量。<br><br>取值範圍：[1,500]。<br><br>預設值：`10`。 |
|Status |Integer |否 |`0` |範本狀態。<br><br>預設值：`0`。<br><br>有效值：<br><br><br>* `0`：返回已建立、未發佈和已發佈的範本。<br><br>* `1`：返回已建立和未發佈的範本。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">「已建立」的範本尚未發佈，而「未發佈」的範本則是曾經發佈過的範本。</div><br> |
|Keyword |String |否 |`Template A` |用於依名稱篩選範本的關鍵字。API 僅返回名稱包含此關鍵字的範本。<br><br>取值範圍：[1,64] |


<span id="06ba436b"></span>
## 回應參數


|名稱 |資料型別 |範例值 |說明 |
|---|---|---|---|
|TemplateList |Array of[TemplateList](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getaccounttemplateapi-zh-TW#07e0ad3c) |`-` |範本列表。 |
|PageNo |Integer |`1` |返回的頁碼。 |
|PageItemCount |Integer |`10` |每頁返回的結果數量。 |
|TotalItemCount |Integer |`1` |返回的範本總數。 |
|EnabledTemplateCount |Integer |`0` |已發佈範本的總數。 |


<span id="07e0ad3c"></span>
### TemplateList


|名稱 |資料型別 |範例值 |說明 |
|---|---|---|---|
|TemplateId |Long |`172436707693****` |範本 ID。 |
|TemplateName |String |`Template A` |範本名稱。 |
|Status |Integer |`1` |範本狀態。<br><br><br>* `1`：已建立。<br><br>* `2`：未發佈。<br><br>* `3`：已發佈。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">已建立的範本尚未發佈，而未發佈的範本曾經發佈過。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">僅已發佈的範本可用於建立直播間。</div><br> |
|CoverImage |String |`//p1-live.byteimg.com/tos-cn-i-gjr78lqtd0/29133e74110444****42013881a6be4b~tplv-gjr78lqtd0-image.image` |返回範本封面圖片的 URL，不含協議頭。 |
|說明 |String |`用於遊戲直播的範本。` |範本描述。 |
|ModifyTime |Long |`1706166059` |範本最後更新的時間，Unix 時間戳格式（秒）。 |
|IsSystemTemplate |Integer |`2` |表示該範本是系統範本還是自定義範本。您無法修改系統範本。<br><br><br>* `1`：系統範本。<br><br>* `2`：自定義範本。 |
|IsDefaultTemplate |Integer |`0` |表示該範本是否為預設範本。<br><br><br>* `0`：非預設範本。<br><br>* `1`：預設範本。 |


<span id="1fa1ba96"></span>
## 範例

<span id="79106916"></span>
### 範例請求

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetAccountTemplateAPI&Version=2020-06-01&PageNo=1&PageItemCount=10&Status=0&Keyword=Template A
```


<span id="749ee2c4"></span>
### 範例回應

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "GetAccountTemplateAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1706166145
    },
    "Result": {
        "PageNo": 1,
        "PageItemCount": 10,
        "TotalItemCount": 1,
        "TemplateList": [
            {
                "TemplateId": 172436707693****,
                "TemplateName": "Template A",
                "Status": 1,
                "CoverImage": "//p1-live.byteimg.com/tos-cn-i-gjr78lqtd0/29133e74110444****42013881a6be4b~tplv-gjr78lqtd0-image.image",
                "Description": "A template for game streaming.",
                "ModifyTime": 1706166059,
                "IsSystemTemplate": 2,
                "IsDefaultTemplate": 0
            }
        ],
        "EnabledTemplateCount": 0
    }
}
```


<span id="49fb22b1"></span>
## 錯誤碼

下表列出此 API 操作專用的錯誤碼。有關通用錯誤碼的列表，請參見[常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/chang-jian-cuo-wu-yu-zhuang-tai-ma-zh-TW)。


|名稱 |訊息 |解決方案 |
|---|---|---|
|100000 |內部錯誤。 |請聯繫技術支援。 |
|200001 |PageItemCount 必須小於或等於 500。 |請更改`PageItemCount`值。 |
|200001 |指定的參數 Status 無效。 |請更改`Status`值。 |
