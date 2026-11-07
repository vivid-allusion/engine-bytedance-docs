---
title: "GetUploadedFilesDownloadUrlAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/getuploadedfilesdownloadurlapi-zh-TW"
---

呼叫此 API 以取得在網頁瀏覽器的直播頁面上上傳的檔案，或於特定直播間互動工具選單下發送的檔案的下載網址。

<span id="2f3ee619"></span>
## 需求


* 配額：每個帳戶每分鐘最多 120 次查詢

* 先決條件：

   * 呼叫 [ListUploadedFilesAPI](https://docs.byteplus.com/docs/byteplus-livesaas/listuploadedfilesapi-zh-TW) 以取得檔案 ID。

   * 需有 BytePlus 帳戶或具備 Live control \> Edit 權限的 IAM 使用者。如需新增 IAM 使用者的詳細資訊，請參閱 [管理使用者、組織與角色](https://docs.byteplus.com/docs/byteplus-livesaas/guan-li-shi-yong-zhe-zu-zhi-yu-jue-se-zh-TW)。


<span id="6c90ef3f"></span>
## HTTP 請求


* URL：`https://livesaas.byteplusapi.com/?Action=GetUploadedFilesDownloadUrlAPI&Version=2020-06-01`

* 方法：GET


<span id="8415fe9f"></span>
## 請求參數

下列表格未包含所有共用請求參數。完整列表請參閱 [共用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/gong-yong-can-shu-zh-TW#f1706967)。

<span id="6f2628f8"></span>
### 查詢


|名稱 |資料型別 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`GetUploadedFilesDownloadUrlAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。目前版本：`2020-06-01`。 |
|ActivityId |Long |是 |`17218312****` |直播間的活動 ID。可透過呼叫 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-TW) 取得 ID。 |
|FileIds |Long 陣列 |是 |`[1800928319729670,1800928594348037,1800929606862854]` |要取得下載網址的檔案 ID。可透過呼叫 [ListUploadedFilesAPI](https://docs.byteplus.com/docs/byteplus-livesaas/listuploadedfilesapi-zh-TW) 取得 ID。<br><br>此陣列最多可包含 100 個檔案 ID。 |
|ExpiredTime |Long |否 |`60` |下載網址的有效時間（秒）。<br><br>單位：秒。<br><br>預設值：`60`。<br><br>值範圍：[1,300] |


<span id="ca343c74"></span>
## 回應參數


|名稱 |資料型別 |範例值 |說明 |
|---|---|---|---|
|FileDownloadUrls |JSON Map |`-` |一個映射表，每個鍵為檔案 ID，對應的值為其下載網址。<br><br><br>* `"Key"`：Long。檔案 ID。<br><br>* `"Value"`：String。檔案的下載網址，包含協議標頭。 |
|FailedFileIds |Long 陣列 |`[1800928319729123,1800928319729222]` |取得網址失敗的檔案 ID。 |


<span id="fb27a92a"></span>
## 範例

<span id="898b0b43"></span>
### 請求範例

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetUploadedFilesDownloadUrlAPI&Version=2020-06-01&ActivityId=17218312****&FileIds=1800928319729670&FileIds=1800928594348037&FileIds=1800929606862854&ExpiredTime=60
```


<span id="e0f347f5"></span>
### 回應範例

```JSON
{
  "ResponseMetadata": {
    "RequestId": "201806041104200100100232280022D30",
    "Action": "GetUploadedFilesDownloadUrlAPI",
    "Version": "2020-06-01",
    "Service": "livesaas",
    "Region": "ap-singapore-1",
    "SystemTime": 1717593301
  },
    "Result": {
        "FileDownloadUrls": {
            "1800928319729670": "https://p-imagex-boei18n.byted.org/tos-boei18n-i-fhdptwgppv/01e997353a734b5c93b153bc27c6844e~tplv-****-image.image",
            "1800928594348037": "https://livesaas-medialib.tos-ap-southeast-1.bytepluses.com/1800896790231062/File_1800896790231062.pdf?X-Tos-Algorithm=TOS4-HMAC-SHA256&X-Tos-Credential=AKAPMzY3NDY5NzMyNGM2NDhkNDk2ZTQ****1NWNlZGRkOWY%2F20240604%2Ftos-ap-southeast-1%2Ftos%2Frequest&X-Tos-Date=20240604T135040Z&X-Tos-Expires=60&X-Tos-Signature=9dd51f458d2331fbd0d085f933a8e3933582e8cb5e4b8b9164b611b99****827&X-Tos-SignedHeaders=host",
            "1800929606862854": "https://livesaas-cloud-doc-sg1.tos-cn-beijing.volces.com/68a5b5e6d27740a89fe45da566a52329.pdf?X-Tos-Algorithm=TOS4-HMAC-SHA256&X-Tos-Credential=AKLTZGNlMmM1NDQwMmUxNDFkMzg5MDA3MTUwNz****IwMGY%2F20240604%2Fcn-beijing%2Ftos%2Frequest&X-Tos-Date=20240604T135040Z&X-Tos-Expires=60&X-Tos-Signature=f4525013f3436f50e784d999d3093de28c4b5fcfdd5f2f1a5ca37de****dbd7e&X-Tos-SignedHeaders=host&response-content-disposition=attachment%3Bfilename%3DFile_1800896792223766+%281%29.pdf"
        },
        "FailedFileIds": []
    }
}
  
```


<span id="747badb1"></span>
## 錯誤碼

下表列出此 API 操作專屬的錯誤碼。共用錯誤碼列表請參閱 [常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/chang-jian-cuo-wu-yu-zhuang-tai-ma-zh-TW)。


|狀態碼 |錯誤碼 |錯誤訊息 |**說明** |
|---|---|---|---|
|400 |InvalidParameter.FileIdsLengthExceed100 |FileIds 參數中的檔案 ID 數量超過 100。 |請減少 `FileIds` 參數中的檔案 ID 數量。 |
