---
title: "URL 封禁與解封"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/url-block-zh-TW"
---

BytePlus 內容分發網路（CDN）提供 **URL 封禁與解封**功能，允許您指定並阻斷外部對加速網域下某些 URL 的存取，或對已封禁的 URL 恢復存取。該功能可幫助您快速響應安全事件，或根據業務需求靈活管理內容的存取權限。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">存取被封禁 URL 的表現</div>


> <div data-tips="true" data-tips-type="tip" data-wrapper-indent="0">如果使用者嘗試存取一個被封禁的 URL，CDN 會回應 <code>403</code> 狀態碼，且回應頭中會包含 <code>Byte-Error-Code: 007</code>。</div>



<span id="功能概述"></span>
## 功能概述

透過 BytePlus CDN 控制台的 **URL 封禁與解封** 頁面，您可以執行以下操作：


* **封禁 URL**：主動阻止外部對特定 URL 的存取。

* **解封 URL**：對已封禁的 URL 恢復正常存取。

* **查看操作記錄**：查詢歷史的封禁與解封操作狀態及執行結果。


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">泛網域限制</div>


<div data-tips="true" data-tips-type="warning">您無法直接對泛網域下的檔案和目錄執行封禁和解封操作。如需操作，請參見 <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/purge-prefetch-faq_zh-tw?lang=en#%E5%A6%82%E4%BD%95%E5%B0%8D%E8%90%AC%E7%94%A8%E5%AD%97%E5%85%83%E7%B6%B2%E5%9F%9F%E4%B8%8B%E7%9A%84%E6%AA%94%E6%A1%88%E5%92%8C%E7%9B%AE%E9%8C%84%E5%9F%B7%E8%A1%8C%E6%B8%85%E9%99%A4%E5%BF%AB%E5%8F%96%E3%80%81%E9%A0%90%E5%8F%96%E3%80%81url-%E5%B0%81%E7%A6%81%E8%88%87%E8%A7%A3%E5%B0%81%E6%93%8D%E4%BD%9C">如何對泛網域下的檔案和目錄執行相關操作</a>。</div>


<span id="封禁-url"></span>
## 封禁 URL

如果您不希望使用者存取網域下的某些特定檔案，可透過該頁面指定需要封禁的 URL。當使用者請求匹配了封禁 URL 時，CDN 將拒絕該請求。


* **操作額度**：主帳號每日最多可封禁 3,000 個 URL。

* **提交要求**：

   * 必須以 `http://` 或 `https://` 開頭。

   * 單次任務最多可包含 100 個 URL。

* **提交方式**：

   1. **手動輸入**：直接在文字方塊中每行輸入一個需要封禁的 URL。

   2. **上傳檔案**：上傳包含需封禁 URL 的 `.txt` 檔案（每行一個 URL）。


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260330142457-1672781058821.png) </span>

<span id="解封-url"></span>
## 解封 URL

用於解除之前被攔截的 URL，恢復使用者的正常存取。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">平台違規封禁的 URL 不支援自助解封</div>


<div data-tips="true" data-tips-type="warning">對於涉華業務，BytePlus CDN 會檢測您分發的內容是否符合中國大陸的相關法律法規（如《網絡安全法》、《互聯網資訊服務管理辦法》等）。對於因內容違規被 BytePlus 主動封禁的 URL，您無法透過本頁面進行自助解封，此類任務將會提示<strong>解封失敗</strong>。如需解封，請 <a href="https://console.byteplus.com/ticket/createTicketV2/">提交工單</a> 申請。</div>



* **操作額度**：主帳號每日最多可解封 3,000 個 URL。

* **提交要求**：同封禁要求，需包含 `http/https` 前綴，單次任務最多 100 個 URL。

* **提交方式**：支援**手動輸入**和**上傳檔案**。


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260330142547-1367954738950.png) </span>

<span id="查看操作記錄"></span>
## 查看操作記錄

在「URL 封禁與解封」頁面的 **操作記錄** 標籤頁，您可以追蹤各個 URL 封禁與解封任務的執行結果。

系統支援查詢過去 **92 天內** 的記錄。您可以透過以下條件進行精準過濾：


* **操作時間**：自定義過去 92 天內的時間段（預設值為「今天」）。

* **任務類型**：URL封禁 / URL解封。

* **任務狀態**：完成 / 執行中 / 執行失敗（預設包含所有狀態）。

* **封禁原因**：URL 被封禁的原因。

* **URL**：精準查詢某個具體 URL 的執行情況。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">系統僅保留 92 天內的可查詢記錄。對於 92 天前被封禁的 URL，您只能透過其返回的 <code>403</code> 狀態碼及 <code>Byte-Error-Code: 007</code> 回應頭來判斷是否處於封禁狀態。</div>


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260330142610-1162902552669.png) </span>
