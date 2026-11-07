---
title: "URL 標準化"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/url-normalization_zh-tw"
---

本文件介紹了 BytePlus CDN 提供的 URL 標準化功能。此功能可降低因使用者請求 URL 不符合標準而導致請求失敗的情況。

<span id="功能概述"></span>
## 功能概述

如果使用者請求 URL 包含非標準內容，由於 CDN 在來源伺服器請求中使用相同的 URL，來源伺服器可能無法處理該來源伺服器請求。同樣地，當您在 CDN 中執行清除或預取操作時，如果您提交的 URL 包含非標準內容，清除和預取的操作結果可能不符合預期。

此功能可以對請求 URL 中出現的以下非標準內容進行標準化處理。


|**非標準內容** |**標準化方式** |**範例：不規範 URL** |**範例：標準化後的 URL** |
|---|---|---|---|
|反斜線（\） |取代為單一斜線（/） |https://www.example.com/img\test |https://www.example.com/img/test |
|連續斜線（//） |取代為單一斜線（/） |https://www.example.com//img///test |https://www.example.com/img/test |
|/./ |取代為單一斜線（/） |https://www.example.com/./img/test |https://www.example.com/img/test |
|/../ |* 如果 `/../` 前還有一個目錄，則刪除 `/../` 與該目錄。<br><br>* 如果 `/../` 前沒有目錄，則保留原 URL。 |https://www.example.com/all/img/../test |https://www.example.com/all/test |
|||https://www.example.com/../test |https://www.example.com/../test |



* URL 標準化不會將使用者請求 URL 重新導向到標準化後的 URL。因此，用戶端瀏覽器網址列中的 URL 不會改變。

* 收到使用者請求時，URL 標準化設定會優先於其他設定生效。「URL 驗證」功能是根據標準化後的 URL 進行操作。


<span id="操作步驟"></span>
## **操作步驟**


1. 開啟 **URL 標準化** 設定頁面。操作步驟請參閱 [網域名稱設定](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-tw)。

2. 將 **狀態** 設定為「啟用」。

3. 在 **設定物件** 中，勾選您需要啟用的 URL 標準化選項。

4. 設定完成後，按一下 **儲存**。


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_661fab77613b389fc41993d7e5a64526.png) </span>
