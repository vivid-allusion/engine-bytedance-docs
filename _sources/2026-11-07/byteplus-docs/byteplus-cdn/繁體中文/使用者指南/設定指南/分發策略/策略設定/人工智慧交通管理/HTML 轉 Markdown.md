---
title: "HTML 轉 Markdown"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/html-to-md_zh-tw"
---

本文介紹如何在 BytePlus CDN 中啟用 HTML 轉 Markdown 功能。啟用後，邊緣節點可將 HTML 回應內容轉換為 Markdown 格式並傳回，讓 AI Agent、爬蟲等系統更容易取得和處理內容。

<span id="3a499196"></span>
## 功能概述

HTML 轉 Markdown 是 CDN 的一項網域設定功能。啟用後，當請求存取 HTML 資源並攜帶 `Accept: text/markdown` 請求標頭時，CDN 邊緣節點會自動將來源站傳回的 HTML 內容轉換為 Markdown 格式並傳回。

轉換會在邊緣節點完成。您不需要在來源站部署轉換邏輯，即可讓 AI Agent 與爬蟲直接取得結構化的 Markdown 內容。其價值在於：


* **降低 token 使用量：**  原始 HTML 包含大量標記、指令碼、樣式等與內文無關的資訊。轉換為 Markdown 後，內容更精簡，可減少 AI 處理時不必要的 token 使用量。

* **提升內容可用性：**  結構化的 Markdown 更利於大型語言模型解析與理解，也有助於 AI 搜尋系統更有效地擷取和使用網站內容。

* **降低來源站開發成本：**  無需在來源站自行部署 HTML 轉換邏輯，在邊緣側即可完成處理。


<span id="6ccd4d4d"></span>
## 轉換說明


|項目 |說明 |
|---|---|
|**觸發方式** |CDN 會依據請求標頭判斷是否執行轉換。只有當請求標頭包含 `Accept: text/markdown` 時，CDN 才會執行轉換。 |
|**支援的來源站回應內容類型** |來源站回應的 `Content-Type` 必須為 `text/html`。 |
|**轉換結果** |Markdown 內容。 |
|**回應標頭** |轉換完成後，CDN 會在回應標頭中傳回 `content-type: text/markdown; charset=utf-8`。 |
|**轉換邏輯** |目前版本不會擷取主要內文，也不會移除非內容元素。CDN 會以來源站傳回的完整 HTML 作為輸入進行轉換；轉換結果包含哪些內容，完全取決於來源站傳回的 HTML。 |
|**快取說明** |啟用此功能後，CDN 不會快取轉換後的 Markdown 回應。 |


<span id="78e6c29e"></span>
## 使用限制

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">如果期望 Markdown 回應包含渲染後的頁面內容，不建議對用戶端渲染（CSR/SPA）頁面啟用此功能。</div>


<div data-tips="true" data-tips-type="tip">對於用戶端渲染頁面，例如以 React、Vue 等建構的單頁應用，來源站傳回的 HTML 通常只包含頁面框架，不包含主要內容；實際內容需要由瀏覽器執行 JavaScript 後，在用戶端動態產生。即使這類頁面在啟用此功能後仍會觸發轉換，也可能出現以下問題：</div>



* <div data-tips="true" data-tips-type="tip">轉換得到的 Markdown 內容可能幾乎為空，因為來源站 HTML 原本就不包含主要內容。</div>


* <div data-tips="true" data-tips-type="tip">如果瀏覽器或除錯工具送出 <code>Accept: text/markdown</code>，回應會是 Markdown 格式，瀏覽器不會將其渲染為原始 HTML 頁面。</div>



<div data-tips="true" data-tips-type="tip">因此，此功能更適合主要內容已包含在來源站 HTML 中的頁面，例如伺服器端渲染（SSR）頁面、靜態網站產生（SSG）頁面，以及透過 PHP、JSP 等伺服器端技術產生完整 HTML 的頁面。</div>


其他說明：


* 目前版本不支援自訂轉換規則，也不支援產生內容摘要。

* 請求檔案的副檔名必須為 `.html` 或 `.htm`，其他副檔名的檔案不會觸發 HTML 轉 Markdown。

* 轉換只會在請求標頭明確攜帶 `Accept: text/markdown` 時觸發。未攜帶該標頭的一般瀏覽器請求不受影響，仍會收到原始 HTML。


<span id="操作步驟"></span>
## 操作步驟


1. 開啟 **HTML 轉 Markdown** 設定頁面。操作步驟請參閱 [網域名稱設定](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-tw)。

2. 將 **狀態** 設定為「啟用」。


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260609072341-706912166292.png) </span>

<span id="效果驗證"></span>
## 效果驗證

設定生效後，可在請求中加入 `Accept: text/markdown` 標頭來存取 HTML 資源，並驗證傳回內容是否為 Markdown 格式。範例命令如下：

```Bash
curl -i -H "Accept: text/markdown" "https://<YOUR-DOMAIN>/example.html"
```


若功能已正常生效，回應標頭中的 `content-type` 會是 `text/markdown; charset=utf-8`，回應內容會是轉換後的 Markdown。作為對比，以不包含該請求標頭的請求存取同一 URL 時，應會傳回原始 HTML。
