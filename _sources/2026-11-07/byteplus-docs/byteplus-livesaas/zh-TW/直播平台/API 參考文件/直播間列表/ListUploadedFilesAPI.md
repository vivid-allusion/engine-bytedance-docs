---
title: "ListUploadedFilesAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/listuploadedfilesapi-zh-TW"
---

獲取在網頁瀏覽器的直播頁面上上傳或在特定直播間互動工具選單下發送的檔案列表。如需獲取檔案的下載 URL，可使用回應中的檔案 ID 調用[GetUploadedFilesDownloadUrlAPI](https://docs.byteplus.com/docs/byteplus-livesaas/getuploadedfilesdownloadurlapi-zh-TW)。

<span id="c6877507"></span>
## 需求


* 配額：每個帳戶每分鐘 120 次查詢

* 前置條件：需具備 BytePlus 帳戶或擁有 Live control \> Edit 權限的 IAM 使用者。如需瞭解如何新增 IAM 使用者，請參見[管理使用者、組織與角色](https://docs.byteplus.com/docs/byteplus-livesaas/guan-li-shi-yong-zhe-zu-zhi-yu-jue-se-zh-TW)。


<span id="011dced4"></span>
## HTTP 請求


* URL：`https://livesaas.byteplusapi.com/?Action=ListUploadedFilesAPI&Version=2020-06-01`

* 方法：GET


<span id="aaa035dc"></span>
## 請求參數

下列表格未包含所有共用請求參數。完整列表請參見[共用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/gong-yong-can-shu-zh-TW#f1706967)。

<span id="e65365d2"></span>
### 查詢


|名稱 |資料型別 |是否必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`ListUploadedFilesAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。當前版本：`2020-06-01`。 |
|ActivityId |Long |是 |`17218312****` |直播間的活動 ID。可透過調用[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-TW)獲取 ID。 |
|FileType |Integer |否 |`0` |指定要返回的檔案類型。<br><br>預設值：`0`。<br><br>有效值：<br><br><br>* `0`：在網頁瀏覽器的直播頁面上上傳及在互動工具選單下發送的文件和圖片。<br><br>* `1`：在網頁瀏覽器的直播頁面上上傳的文件和圖片。<br><br>* `2`：在互動工具選單下發送的文件。<br><br>* `3`：在互動工具選單下發送的圖片。 |
|OrderType |Integer |否 |`0` |指定根據上傳時間或發送時間返回檔案的排序方式。<br><br>預設值：`0`。<br><br>有效值：<br><br><br>* `0`：降序排列。<br><br>* `1`：升序排列。 |
|PageNumber |Long |否 |`1` |要返回的頁碼。預設值：`1`。 |
|PageSize |Long |否 |`100` |每頁返回的結果數量。預設值：`100`。<br><br>取值範圍：[1,1000]。 |


<span id="fd359ed0"></span>
## 回應參數


|名稱 |資料型別 |範例值 |說明 |
|---|---|---|---|
|PageNumber |Long |`1` |返回的頁碼。 |
|PageSize |Long |`100` |每頁的結果數量。 |
|TotalCount |Long |`3` |檔案總數。 |
|Files |Array of[UploadedFile](https://docs.byteplus.com/docs/byteplus-livesaas/listuploadedfilesapi-zh-TW#d48e51e4) |`-` |返回的檔案列表。 |


<span id="d48e51e4"></span>
### UploadedFile


|名稱 |資料型別 |範例值 |說明 |
|---|---|---|---|
|FileId |Long |`180092831972****` |檔案 ID。 |
|FileName |String |`File_180089679222****.pdf` |檔案名稱。 |
|UploadTime |Long |`1717499084` |檔案上傳或發送時的 Unix 時間戳（秒）。 |
|FileSize |Long |`330971` |檔案大小。單位：位元組（bytes）。 |
|FileType |Integer |`0` |檔案類型。<br><br><br>* `1`：在網頁瀏覽器的直播頁面上上傳的文件和圖片。<br><br>* `2`：在互動工具選單下發送的文件。<br><br>* `3`：在互動工具選單下發送的圖片。 |


<span id="22ed0774"></span>
## 範例

<span id="8797965a"></span>
### 請求範例

```JSON
GET https://livesaas.byteplusapi.com/?Action=ListUploadedFilesAPI&Version=2020-06-01&ActivityId=17218312****&FileType=0&OrderType=0&PageNumber=1&PageSize=100
```


<span id="8ec0c8ce"></span>
### 回應範例

```JSON
{
  "ResponseMetadata": {
    "RequestId": "20180604110420010010****0022D30",
    "Action": "ListUploadedFilesAPI",
    "Version": "2020-06-01",
    "Service": "livesaas",
    "Region": "ap-singapore-1",
    "SystemTime": 1717593301
  },
    "Result": {
        "PageNumber": 1,
        "PageSize": 100,
        "TotalCount": 3,
        "Files": [
            {
                "FileId": 180092831972****,
                "FileName": "01e997353a734b5c93b153bc27c6844e~tplv-fhdptw****-image.image",
                "UploadTime": 1717499084,
                "FileSize": 1024,
                "FileType": 3
            },
            {
                "FileId": 1800928594348037,
                "FileName": "File_180089679222****.pdf",
                "UploadTime": 1717499346,
                "FileSize": 330971,
                "FileType": 2
            },
            {
                "FileId": 1800929606862854,
                "FileName": "File_180089679222****.pdf",
                "UploadTime": 1717500309,
                "FileSize": 330971,
                "FileType": 1
            }
        ]
    }
}
```


<span id="1c8671c7"></span>
## 錯誤碼

共用錯誤碼列表請參見[常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/chang-jian-cuo-wu-yu-zhuang-tai-ma-zh-TW)。
