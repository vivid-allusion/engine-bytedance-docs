---
title: "使用 HTML 轉 Markdown 優化 AI Agent 內容抓取"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/html-md-best-practice_zh-tw"
---

HTML 轉 Markdown 可將網頁的 HTML 內容轉換為 Markdown 格式。相較於原始 HTML，Markdown 結構更簡潔、以文字內容為主，通常能保留標題、段落、清單和連結等資訊，更適合 AI Agent、AI 搜尋爬蟲和大型語言模型驅動的問答系統讀取。

在 CDN 中啟用 HTML 轉 Markdown 後，轉換會在邊緣節點完成。AI 用戶端可在請求中加入 `Accept: text/markdown` 標頭來取得 Markdown；一般瀏覽器仍會收到原始 HTML。這樣既能讓 AI 用戶端以更輕量的方式取得內容，也不需要在來源站另外開發和維護轉換服務。

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260708060405-1153431407233.png) </span>

<span id="1c89793d"></span>
# 使用場景

如果您的網站有大量公開內容頁面，且來源站傳回的 HTML 已包含完整內文，建議優先試用 HTML 轉 Markdown。此功能特別適合希望讓 AI Agent、AI 搜尋爬蟲和大型語言模型驅動的問答系統更容易讀取網站內容的網站。


* 網站已有大量公開內容頁，例如說明中心、文件站、新聞文章、部落格、知識庫、商品詳情頁等。

* 希望一般瀏覽器仍收到原始 HTML，同時為 AI 用戶端提供更輕量的 Markdown 內容。

* 不希望在來源站另外開發和維護 HTML 轉 Markdown 服務。


<span id="7d9595c9"></span>
# 使用效益

對已有大量公開內容頁的網站而言，HTML 轉 Markdown 的核心價值是：在不影響一般瀏覽器存取的前提下，讓同一批內容更容易被 AI Agent 讀取和理解。實際效益取決於網頁本身的內容結構，建議透過典型頁面進行對比驗證。


|效益 |說明 |
|---|---|
|減少非內容元素的干擾 |Markdown 相較於原始 HTML 更精簡，可減少非內容元素對 AI 讀取的干擾。 |
|減少傳輸內容大小 |將 HTML 轉換為 Markdown 後，回應通常會包含較少頁面結構、樣式和指令碼資訊，因此可降低傳輸內容大小。例如，某個體積為 5 MB、包含較多導覽、樣式、指令碼等非內容元素的 HTML 頁面，轉換為 Markdown 後約為 3 MB，體積降幅超過 40%。頁面中非主要內容占比越高，轉換後的縮減效果通常越明顯。 |
|提升內容可讀性 |Markdown 保留標題、段落、清單、連結等結構，更適合 AI Agent、搜尋爬蟲和大型語言模型驅動的問答系統讀取。 |
|降低來源站改造成本 |轉換在 CDN 邊緣節點完成，來源站無需另外建置一套 HTML 轉 Markdown 服務。 |
|不影響一般瀏覽器存取 |一般瀏覽器請求未攜帶 `Accept: text/markdown` 請求標頭時，仍會傳回原始 HTML 頁面。 |


<span id="250cf4d6"></span>
# 建議使用方式

建議先選擇 3 到 5 個典型內容型頁面啟用並驗證效果，例如說明中心文章、文件頁、新聞詳情頁或商品詳情頁。使用同一 URL 進行兩次測試：一次不加入 `Accept: text/markdown` 標頭，另一次加入該標頭。比較一般瀏覽器是否仍收到原始 HTML、Markdown 是否包含預期的標題與內文，以及清單和連結是否保留。

確認效果符合預期後，再逐步擴展到同類頁面。對於需要在瀏覽器執行 JavaScript 後才顯示內文、內容結構複雜，或高度依賴互動的頁面，建議先評估轉換結果，再決定是否擴大使用範圍。

<span id="1a474c4d"></span>
# 功能運作方式

HTML 轉 Markdown 是 CDN 網域設定中的一項功能開關。啟用後，CDN 會根據請求標頭區分請求類型：AI 用戶端請求 Markdown 時傳回 Markdown；一般瀏覽器存取時仍傳回原始 HTML。

<span id="8ed52ccc"></span>
## 處理流程


1. AI Agent、AI 搜尋爬蟲等用戶端請求頁面，並在請求標頭中帶上 `Accept: text/markdown`。

2. CDN 邊緣節點接收請求，確認目標網域已啟用 HTML 轉 Markdown，並判斷請求標頭是否符合轉換條件。

3. 符合條件時，CDN 回源取得原始 HTML 頁面，並在邊緣節點將 HTML 轉換為 Markdown。

4. CDN 向用戶端傳回 Markdown 回應；一般瀏覽器請求未攜帶該請求標頭時，仍傳回原始 HTML。



|項目 |說明 |
|---|---|
|觸發方式 |僅當請求標頭攜帶 `Accept: text/markdown` 時觸發轉換。 |
|來源站回應內容類型 |來源站回應的 `Content-Type` 需為 `text/html`。 |
|轉換結果 |傳回 Markdown 內容。 |
|回應標頭 |轉換成功後，回應會包含 `content-type: text/markdown; charset=utf-8` 標頭。 |
|快取策略 |CDN 不快取轉換後的 Markdown 回應，每次請求即時轉換。 |


<span id="f3b7516c"></span>
# 使用限制

使用此功能前，請先確認以下限制。HTML 轉 Markdown 的作用是讓 AI 用戶端更方便讀取既有 HTML 內容，不會改變原始網頁內容。


* \*\*觸發條件限制：\*\*僅當請求標頭攜帶 `Accept: text/markdown` 時觸發轉換。一般瀏覽器請求不攜帶該請求標頭時，仍傳回原始 HTML。

* \*\*來源站回應內容類型限制：\*\*來源站回應的 `Content-Type` 需為 `text/html`。

* \*\*檔案副檔名限制：\*\*請求檔案的副檔名必須為 `.html` 或 `.htm`，其他副檔名的檔案不會觸發 HTML 轉 Markdown。

* \*\*適用頁面：\*\*適用於來源站 HTML 中已包含完整內文的頁面，例如說明中心、文件站、新聞文章、部落格、知識庫、商品詳情頁等內容型頁面。

* \*\*不建議使用的頁面：\*\*如果來源站 HTML 只包含頁面框架、沒有完整內文，則不建議啟用；用戶端渲染（CSR/SPA）頁面通常屬於這種情況。這類頁面通常需要在瀏覽器執行 JavaScript 後才顯示內文，因此轉換出的 Markdown 可能幾乎為空；如果瀏覽器或除錯工具送出 `Accept: text/markdown`，回應會以 Markdown 顯示，而不會渲染成原始 HTML 頁面。

* \*\*內容處理限制：\*\*目前此功能不會擷取主要內文、產生摘要，也不會移除非內容元素。CDN 會以來源站傳回的完整 HTML 作為輸入進行格式轉換。

* \*\*快取限制：\*\*CDN 不快取轉換後的 Markdown 回應，每次符合轉換條件的請求都會即時轉換。

* \*\*內容品質：\*\*此功能無法取代內容品質最佳化。標題層級、內文結構、連結文字和無關內容仍需在來源站保持清楚。


<span id="0b5b2b2d"></span>
# 查看設定方式

如需查看完整的控制台設定路徑和操作步驟，請參見 [HTML 轉 Markdown 設定文件](https://docs.byteplus.com/en/docs/byteplus-cdn/html-to-md_zh-cn)。

在 CDN 控制台進入目標網域的設定頁面，找到 HTML 轉 Markdown 設定，啟用此功能並提交設定。設定生效後，只有攜帶 `Accept: text/markdown` 請求標頭的請求會觸發轉換；未攜帶該請求標頭的一般瀏覽器請求不受影響。
