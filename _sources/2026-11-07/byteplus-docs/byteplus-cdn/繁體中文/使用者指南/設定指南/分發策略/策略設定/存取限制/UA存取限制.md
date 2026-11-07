---
title: "UA存取限制"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ua-restriction_zh-tw"
---

本文件介紹如何在 BytePlus CDN 中通過 User\-Agent 請求標頭來對存取您網域名稱的請求進行限制。

<span id="什麼是-user-agent"></span>
## 什麼是 User\-Agent

User\-Agent 請求標頭包含了發起請求的用戶端的作業系統版本、CPU 類型、瀏覽器版本等資訊。網站伺服器可以針對不同的 User\-Agent 標頭的值，返回不同的頁面。

在 CDN 中，您可以通過 User\-Agent 欄位的值來允許或者阻止特定使用者存取您的網域名稱。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">您可以在搜尋引擎中搜尋 "User Agent大全" 來查找常見的 User\-Agent 值。</div>


<span id="空-user-agent"></span>
### **空 User\-Agent**

"空 User\-Agent" 的定義是 User\-Agent 標頭沒有值或者請求中不包含 User\-Agent 標頭。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>User-Agent: null</code> 不被視為是 "空 User\-Agent" 情況。</div>


<span id="操作步驟"></span>
## 操作步驟


1. 打開 **UA存取限制** 設定頁面。操作步驟參見 [網域名稱設定](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-tw)。

2. 在 **UA存取限制** 下方，設定 **狀態** 為 **開啟**。

3. 參照以下設定說明。

4. 設定完成後，點擊 **儲存**。


<span id="設定說明"></span>
### 設定說明


|**設定** |**說明** |
|---|---|
|類型 |該設定有以下選項：<br><br><br>* **允許清單**：指定設定的名單類型為允許清單。只有使用者請求的 User\-Agent 請求標頭在允許清單中，該請求才能存取您的網域名稱。<br><br>* **封鎖清單**：指定設定的名單類型為封鎖清單。如果使用者請求的 User\-Agent 請求標頭在封鎖清單中，CDN 會拒絕該請求。<br><br><br>如果一個請求的 User\-Agent 請求標頭匹配了封鎖清單或者沒有匹配允許清單，CDN 會拒絕該請求並返回 403 回應狀態碼。 |
|User\-Agent 字串 |輸入一個或者多個 User\-Agent。該設定的長度不能超過 30,000 個字元。您最多可以輸入 1,000 個 User\-Agent。您輸入的 User\-Agent 有以下要求：<br><br><br>* 您可以使用萬用字元（\*）表示任意數量的字元。但是 `*` 僅可以出現在一個 User\-Agent 的開頭和末尾。<br><br>* User\-Agent 不能包含 `**`。<br><br>* User\-Agent 只能包含可列印 ASCII 字元，除了 Delete（ASCII code 127）。<br><br>* 多個 User\-Agent 使用分隔符（\|）分隔，或者每行一個 User\-Agent。比如: `*curl*\|*Mozilla*`。<br><br>* User\-Agent 不能只包含空格。 |
|空 User\-Agent 存取 CDN 資源 |表示在 [空 User-Agent](https://docs.byteplus.com/en/docs/18/36277#%E7%A9%BA-user-agent) 情境下，CDN 處理請求的方式。<br><br><br>* 如果 **類型** 是 **封鎖清單** ，該選項是 **允許空 User\-Agent 存取 CDN 資源**。<br><br>* 如果 **類型** 是 **允許清單** ，該選項是 **不允許空 User\-Agent 存取 CDN 資源**。 |
|忽略大小寫 |表示 User\-Agent 名單在用於過濾請求時是否區分大小寫。 |


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_6268de26eae41e16af9a80c8b6313375.png) </span>
