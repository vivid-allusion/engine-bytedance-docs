---
title: "TempToMediaActivityMediaAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/TempToMediaActivityMediaAPI-zh-TW"
---

將影片從暫存儲存區轉移至影片庫中的指定分類，以進行永久儲存。轉移完成後，這些影片將會從暫存儲存區中刪除。

<span id="Requirements"></span>
## 需求


* 速率限制：每個帳號每分鐘 120 次請求

* 前置條件：需擁有 BytePlus 帳號，或具備**媒體庫** \> **影片** \> **暫存儲存區** \> **編輯**權限的 IAM 使用者。如需瞭解如何新增 IAM 使用者，請參見[管理使用者、組織與角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://livesaas.byteplusapi.com/?Action=TempToMediaActivityMediaAPI&Version=2020\-06\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

下列表格未涵蓋所有通用請求參數。如需完整清單，請參見[通用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`TempToMediaActivityMediaAPI` |API 操作名稱。 |
|Version |String |是 |`2020-06-01` |本 API 操作的版本。目前版本：`2020-06-01`。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Ids |String 陣列 |是 |`["409144","409154"]` |欲轉移影片的 ID。可根據`ListActivityMediaAPI` 的回應參數 [Id](https://docs.byteplus.com/en/docs/byteplus-livesaas/listactivitymediaapi) 取得影片 ID。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">最多可設定 100 個 ID。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">以 IAM 使用者呼叫本 API 時，請確保該 IAM 使用者有權存取或編輯這些影片。如需瞭解如何設定 IAM 使用者的用戶範圍與分類範圍，請參見<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles">管理使用者、組織與角色</a>。</div><br> |
|FolderId |Long |否 |`48921` |分類 ID。影片將轉移至此 ID 所對應的分類。預設值為`0`，表示影片將轉移至預設分類。可透過呼叫[GetVideoLibraryFolderTree](https://docs.byteplus.com/en/docs/byteplus-livesaas/getvideolibraryfoldertree) 取得分類 ID。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">以 IAM 使用者呼叫本 API 且需傳遞此參數時，請確保該分類對該 IAM 使用者可見。如需瞭解如何設定 IAM 使用者的分類範圍，請參見<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles">管理使用者、組織與角色</a>。</div><br> |


<span id="Response parameters"></span>
## 回應參數


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Success |Boolean |`false` |影片是否成功轉移。有效值：<br><br><br>* `true`：成功，表示所有影片皆成功轉移。<br><br>* `false`：失敗，表示有一個或多個影片轉移失敗。 |
|FailedList |[FailedList](https://docs.byteplus.com/en/docs/11/113734#failedlist) 陣列 |`-` |轉移失敗的影片清單。僅當有一個或多個影片轉移失敗時才會返回此清單，即 `Success` 的值為 `false`。 |


<span id="failedlist"></span>
### FailedList


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Id |String |`409144` |影片的 ID。 |
|Name |String |`video1` |影片名稱。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```JSON
POST https://livesaas.byteplusapi.com/?Action=TempToMediaActivityMediaAPI&Version=2020-06-01
{
    "Ids": [
        "409144",
        "409154"
    ],
    "FolderId": 48921
}
```


<span id="Sample response"></span>
### 回應範例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "TempToMediaActivityMediaAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "Success": false,
        "FailedList": [
            {
                "Id": "409144",
                "Name": "video1"
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

如需常見錯誤碼清單，請參見[常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
