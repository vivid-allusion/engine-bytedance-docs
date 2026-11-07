---
title: "GetVideoLibraryFolderTree"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/GetVideoLibraryFolderTree-zh-TW"
---

獲取您帳戶下預設分類或特定分類及其子分類的資訊。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">以 IAM 使用者呼叫本 API 時，僅能獲取該 IAM 使用者可見的影片庫分類資訊。如需設定 IAM 使用者分類範圍的詳細資訊，請參閱<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles">使用者、組織與角色管理</a>。</div>


<span id="Requirements"></span>
## 需求


* 速率限制：每個帳戶每分鐘 120 次請求

* 前置條件：需擁有 BytePlus 帳戶，或具備**媒體庫** \> **影片** \> **影片庫** \> **編輯**或**僅檢視**權限的 IAM 使用者。如需新增 IAM 使用者的詳細資訊，請參閱[使用者、組織與角色管理](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：GET

* 端點：https://livesaas.byteplusapi.com/?Action=GetVideoLibraryFolderTree&Version=2023\-08\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

下列表格未包含所有通用請求參數。完整列表請參閱[通用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`GetVideoLibraryFolderTree` |API 操作。 |
|Version |String |是 |`2023-08-01` |本 API 操作的版本。當前版本：`2023-08-01`。 |
|FolderId |Long |否 |`0` |分類 ID。預設值為`0`，表示將返回預設分類下的所有子分類。 |


<span id="Response parameters"></span>
## 回應參數


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|FolderNode |[FolderNode](https://docs.byteplus.com/en/docs/11/113733#foldernode) 物件 |`-` |分類資訊。 |


<span id="foldernode"></span>
### FolderNode


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|FolderId |Long |`0` |分類 ID。 |
|FolderName |String |`分類 1` |分類名稱。 |
|FolderTypeForSubAccount |Integer |`-` |子分類資訊。 |
|Children |[Children](https://docs.byteplus.com/en/docs/11/113733#children) 陣列 |`0` |IAM 使用者呼叫本 API 時，對該分類擁有的操作權限。有效值：<br><br><br>* `0`：最高權限。IAM 使用者可檢視並操作該分類及其資源，例如刪除資源或編輯分類。<br><br>* `1`：IAM 使用者可檢視並操作該分類下的資源，但無法對分類本身進行操作，例如編輯分類或建立子分類。<br><br>* `2`：IAM 使用者僅可檢視分類，無法檢視或操作分類下的資源。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">以 BytePlus 帳戶呼叫本 API 時，此參數值固定為<code>0</code>。</div><br> |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetVideoLibraryFolderTree&Version=2023-08-01&FolderId=0
```


<span id="Sample response"></span>
### 回應範例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetVideoLibraryFolderTree",
        "Version": "2023-08-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "FolderNode": {
            "FolderId": 0,
            "FolderName": "All files",
            "Children": [
                {
                    "FolderId": 17959466895819,
                    "FolderName": "Subcategory 1",
                    "Children": [
                        {
                            "FolderId": 17959465298105,
                            "FolderName": "Subcategory 2",
                            "Children": []
                        }
                    ]
                }
            ],
            "FolderTypeForSubAccount": 0
        }
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

常見錯誤碼請參閱[常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
