---
title: "Referer 防盜連結"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/referer-restrictions_zh-tw"
---

在 BytePlus CDN 中，您可以設定 "Referer 防盜連結"，阻止包含特定 Referer 的請求存取 CDN，從而防止您網站的內容被盜用連結。

如果使用者請求因為符合您的 "Referer 防盜連結" 設定而被 CDN 拒絕，CDN 會回應 403 狀態碼。

<span id="注意事項"></span>
## 注意事項

當使用者請求被 CDN 拒絕時，以下用量仍會被計算。


* CDN 對該請求的回應會計入 CDN 向使用者傳輸的資料量，雖然該資料量很小。

* 如果該請求是 HTTPS 請求，該請求會計入 HTTPS 請求數。


<span id="referer-介紹"></span>
## Referer 介紹

Referer 是 HTTP 請求中的一個標頭，用來記錄請求的來源頁面。一般而言，Referer 是一個完整 URL，包含 scheme、網域名稱、路徑和查詢字串。

當您點擊網頁 A 中的連結時，瀏覽器會向連結所指向的目標頁面發送 HTTP 請求。請求中包含 Referer 標頭，標頭值就是網頁 A 的 URL。

<span id="空-referer"></span>
### 空 Referer

空 Referer 指的是 HTTP 請求中不包含 Referer 標頭。在 "Referer 防盜連結" 中，您可以設定 CDN 如何處理不包含 Referer 標頭的使用者請求。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>Referer: null</code> 不被視為是 "空 Referer" 情況。</div>


**空 Referer 情境**

通常，空 Referer 出現在以下任一情境中：


* 您透過瀏覽器中的書籤存取目標頁面。

* 您在瀏覽器網址列中輸入 URL 存取目標頁面。

* 您在 HTTPS 頁面中點擊連結存取 HTTP 頁面。

* 您使用瀏覽器提供的隱私瀏覽模式。

* 如果您存取的頁面符合以下任一條件，您在該頁面中點擊任何連結時，HTTP 請求中不會包含 Referer 標頭。

   * 頁面的 `<meta>` 標籤中宣告了 `Referrer-Policy: no-referrer`。

   * 包含該頁面的伺服器回應中存在 `Referrer-Policy: no-referrer` 標頭。


<span id="功能優先級"></span>
## 功能優先級

CDN 提供的一系列存取限制功能有不同的優先級。在 CDN 處理使用者請求時，這些功能按優先級對請求生效。參見 [存取限制功能的優先順序](https://docs.byteplus.com/en/docs/byteplus-cdn/access-restrictions-priority_zh-tw)。

<span id="操作步驟"></span>
## 操作步驟


1. 打開 **Referer存取限制** 設定頁面。操作步驟參見 [網域名稱設定](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-tw)。

2. 在 **Referer存取限制** 下方，設定 **狀態** 為開啟。

3. 參照以下 [設定說明](https://docs.byteplus.com/en/docs/18/36278#%E8%A8%AD%E5%AE%9A%E8%AA%AA%E6%98%8E)。

4. 設定完成後，點擊 **儲存**。


<span id="設定說明"></span>
## 設定說明


|設定 |說明 |
|---|---|
|類型 |表示清單的類型。該設定有以下選項：<br><br><br>* **白名單**：指定一個白名單。如果使用者請求中的 Referer 不符合該清單，CDN 會拒絕請求。<br><br>* **黑名單**：指定一個黑名單。如果使用者請求中的 Referer 符合該清單，CDN 會拒絕請求。 |
|設定方式 |表示清單中項目的來源。該設定有以下選項：<br><br><br>* 策略設定：表示清單中的項目在 **一般清單** 和 **正規表示式清單** 中設定。<br><br>* 全域設定：表示清單中的項目來自一個 [全域設定](https://docs.byteplus.com/en/docs/byteplus-cdn/universal-catalog_zh-tw)。全域設定用來定義大量項目。一個全域設定最多可以包含 4,000 個項目。 |
|規則內容 |表示清單的設定選項，包含：<br><br><br>* 一般清單：清單中的每個項目是一個 IP 位址或者網域名稱，用來對 Referer 中的 hostname 進行符合驗證。<br><br>* 正規表示式清單：清單中的每個項目是一個正規表示式，用來對 Referer 中的完整 URL 進行符合驗證。<br><br>* 空 Referer：表示當使用者請求不包含 Referer 標頭時，CDN 處理請求的方式。該設定有以下選項：<br><br>   * 勾選：表示如果請求不包含 Referer 標頭，則該請求被視為**符合**您設定的清單。<br><br>   * 不勾選：表示如果請求不包含 Referer 標頭，則該請求被視為**不符合**您設定的清單。 |
|一般清單（輸入框） |表示一個一般清單。如果您在 **規則內容** 下勾選了 **一般清單**，該輸入框會出現。<br><br>&nbsp;<br><br>**輸入要求**<br><br>清單最多可以包含 1,000 個項目，總長度不能超過 30,000 個字元。您可以輸入一個或多個網域名稱和 IP 位址。網域名稱可以是萬用字元網域名稱。IP 位址只能是 IPv4 位址或者 IPv4 CIDR 位址。多個項目之間使用分號（;）分隔或者每個項目一行。<br><br>&nbsp;<br><br>如果您需要輸入的項目數量超過 1,000，參考 [全域設定](https://docs.byteplus.com/en/docs/byteplus-cdn/universal-catalog_zh-tw)。<br><br>&nbsp;<br><br>**關於萬用字元網域名稱和子網域名稱**<br><br><br>* 萬用字元網域名稱不符合網域名稱本身。例如：`*.example.com` 不符合 `example.com`，但是符合 `www.example.com`、`a.a.example.com` 等。<br><br>* 子網域名稱的層級數量沒有限制。例如，您可以在清單中指定 `aaa.bbb.ccc.ddd.eee.fff.ggg.eee.example.com`。 |
|忽略大小寫 |表示一般清單中的項目是否區分大小寫。 |
|忽略 Scheme 驗證 |表示 CDN 是否對 Referer 中的 scheme 進行驗證，也就是驗證 Referer 是否包含 `http://` 或者 `https://`。該設定有以下選項：<br><br><br>* 勾選：表示 CDN 不驗證 Referer 是否包含 scheme。在這個情況下，無論 Referer 是否包含 scheme，CDN 都會將 Referer 與您設定的清單進行符合驗證。<br><br>* 不勾選：表示 CDN 會先驗證 Referer 是否包含 scheme。只有 Referer 包含 scheme，CDN 才會將 Referer 與您設定的清單進行符合驗證。否則，CDN 判定請求與您設定的清單不符合。<br><br><br>該設定對**正規表示式清單**不生效，因為 CDN 依賴正規表示式來判斷 Referer 是否符合正規表示式清單。 |
|正規表示式清單（輸入框） |表示一個正規表示式清單，用於對 Referer 中的完整 URL 進行符合驗證。您最多可以指定 100 個正規表示式，每個正規表示式一行。如果您在 **規則內容** 下勾選了 **正規表示式清單**，該輸入框會出現。 正規表示式清單中的項目不區分大小寫。 |


<span id="設定範例"></span>
## 設定範例

假設您設定的清單中包含以下項目：


* www.example.com

* \*.example.com


相關設定及符合結果如下表所示：


|**清單類型** |**使用者請求中的 Referer** |**忽略大小寫** |**忽略 Scheme 驗證** |**空 Referer** |**符合結果** |
|---|---|---|---|---|---|
|黑名單 |https://www.eXampLe.com/file?p=v |勾選 |N/A ||拒絕請求 |
|||不勾選 |||接受請求 |
||www.example.com/file?p=v |N/A |勾選 |N/A |拒絕請求 |
||||不勾選 ||接受請求 |
||不包含 Referer 標頭 |N/A ||勾選 |拒絕請求 |
|||||不勾選 |接受請求 |
||https://www.example.com |N/A |||拒絕請求 |
||https://docs.www.example.com ||||拒絕請求 |
||https://example.com ||||接受請求 |
|白名單 |https://www.eXampLe.com/file?p=v |勾選 |N/A ||接受請求 |
|||不勾選 |||拒絕請求 |
||www.example.com/file?p=v |N/A |勾選 |N/A |接受請求 |
||||不勾選 ||拒絕請求 |
||不包含 Referer 標頭 |N/A ||勾選 |接受請求 |
|||||不勾選 |拒絕請求 |
||https://www.example.com |N/A |||接受請求 |
||https://docs.www.example.com ||||接受請求 |
||https://example.com ||||拒絕請求 |
