---
title: "fetch()"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-fetch-cn-zh-tw"
---

傳送 HTTP 或 HTTPS 請求。請參閱 MDN 文件中的 [fetch()](https://developer.mozilla.org/docs/Web/API/WindowOrWorkerGlobalScope/fetch)。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">如果您的函數呼叫 <code>fetch()</code> 以取得 HTTP 回應並修改 HTML 主體 (例如，使用 <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/HtmlStream-zh-tw">createHtmlStream()</a> 以串流方式修改 HTML 主體)，建議您從原始 HTTP 回應中刪除 <code>Content-Length</code> 標頭。否則，可能會導致資料傳輸錯誤。這是因為 HTTP 回應可能包含 <code>Content-Length</code> 標頭。如果執行時期在函數修改 HTTP 回應的 HTML 主體時轉寄原始回應的 <code>Content-Length</code> 標頭，則承載的實際大小將與 <code>Content-Length</code> 標頭的值不同。參見 <a href="https://docs.byteplus.com/en/docs/18/45016#payload">Content\-Length 標頭如何影響承載傳輸</a> 了解更多資訊。</div>


<span id="使用限制"></span>
## 使用限制


* `fetch()` 方法會使用預設連接埠傳送請求。HTTP 請求的預設連接埠為 80，HTTPS 請求的預設連接埠為 443。

* 請求位址中不允許使用 IP 位址。

* 請求位址中不能省略協定。例如，`fetch("www.example.com")` 是不正確的。您需要將其變更為 `fetch("https://www.example.com")`。


<span id="使用方式"></span>
## 使用方式

<span id="存取-byteplus-cdn-網域"></span>
### 存取 BytePlus CDN 網域

預設情況下，`fetch()` 會透過網際網路傳送請求。如果 `fetch()` 方法存取的網域是 BytePlus CDN 網域，推薦您使用 `{proxy: "cdn"}` 參數設定 `fetch()` 方法在邊緣節點內部傳送請求。由於邊緣函數和 BytePlus CDN 共用邊緣節點，函數傳送的請求將在邊緣節點內部直接轉寄到 BytePlus CDN。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">BytePlus CDN 網域是 BytePlus CDN 為其提供內容分發服務的任何網域名稱。該網域在 BytePlus CDN 中的狀態必須為<strong>啟用</strong>。</div>


例如，您可以使用下列方法請求 BytePlus CDN 網域 `cdn.example.com` 和第三方 API 服務網域 `api.example.com`：

```js
// 請求 BytePlus CDN 網域 cdn.example.com
const responseCDN = await fetch("https://cdn.example.com", { proxy: "cdn" });

// 請求第三方 API 服務網域 api.example.com
const responseAPI = await fetch("https://api.example.com");
```


下圖顯示了傳入和不傳入 `{proxy: "cdn"}` 參數時請求路徑的差異：

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_e0b83d3c4f38d9c7c09b64a8673fea6d.png) </span>

下表比較了傳入和不傳入 `{proxy: "cdn"}` 參數的差異：


|差異項 |使用 `{proxy: "cdn"}` |不使用 `{proxy: "cdn"}` (預設) |
|---|---|---|
|**請求路徑** |函數傳送的請求會直接在邊緣節點内轉寄到 BytePlus CDN。 |函數傳送的請求會透過 DNS 解析經由網際網路路由到一個邊緣節點。此邊緣節點不一定是執行函數的邊緣節點。 |
|**費用** |BytePlus CDN 端不會產生流量費用。 |如果請求的網域是 BytePlus CDN 網域，透過網際網路的請求會在 BytePlus CDN 端產生流量費用。 |
|**適用情境** |僅適用於存取 BytePlus CDN 網域。如果請求的網域不是 BytePlus CDN 網域，請求將會失敗。函數會傳回 403 錯誤碼。 |適用於存取 BytePlus CDN 網域以外的任何可透過網際網路存取的網域。如果請求的網域是 BytePlus CDN 網域，請求可能會受到網域存取控制的限制 (例如 IP 黑白名單、地理位置限制等)。 |


<span id="遵循-3xx-重新導向"></span>
### 遵循 3xx 重新導向

您可以使用 `redirect` 參數設定 `fetch()` 方法如何處理 3xx 重新導向。


* `{redirect: "manual"}` (預設)：不會自動遵循 3xx 重新導向。您可以手動處理重新導向。

* `{redirect: "follow"}`：自動遵循 3xx 重新導向。對於同一個請求，`fetch()` 方法預設會遵循最多 4 次重新導向，並允許跨網域和跨協定重新導向。

* `{redirect: "error"}`：遇到 3xx 重新導向時擲回錯誤。


下列範例說明如何自動遵循 3xx 重新導向：

```js
const response = await fetch("https://www.example.com", {redirect: "follow"});
```


`fetch()` 對於不同狀態碼的重新導向行為如下：


|**狀態碼** |**重新導向行為** |
|---|---|
|301, 302, 303, 308 |重新導向請求的請求方法會變更為 GET。請求主體會被忽略。 |
|307 |僅遵循 GET 方法。對於使用其他 HTTP 方法發起的請求，此方法不會自動遵循重新導向，並會擲回錯誤。 |


重新導向位址是從 `Location` 回應標頭取得。`Location` 回應標頭目前接受以逗號分隔的清單，但只會遵循第一個 URL，其他 URL 將會被忽略。

<span id="解壓縮回應資料"></span>
### 解壓縮回應資料

`fetch()` 方法目前僅支援解壓縮 **gzip** 格式的回應資料。您可以使用 `decompression` 參數設定 `fetch()` 方法是否解壓縮回應資料：

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>fetch()</code> 方法透過回應中的 <code>Content-Encoding</code> 標頭來識別壓縮格式。例如：</div>



* <div data-tips="true" data-tips-type="tip">如果 <code>Content-Encoding</code> 為 <code>gzip</code> 或 <code>gzip, identity</code>，回應將被識別為 gzip 壓縮。</div>


* <div data-tips="true" data-tips-type="tip">如果 <code>Content-Encoding</code> 為 <code>brotli, gzip</code>，<code>fetch()</code> 方法只會解壓縮最外層的 gzip 壓縮。</div>


* `manual`：**不解壓縮**。直接傳回原始的回應資料。

* `fallbackIdentity`：（預設）**自動解壓縮**。對於不支援的壓縮格式將傳回原始資料。

* `decompress`：**自動解壓縮**。對於不支援的壓縮格式將拋出錯誤。


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">解壓縮後，<code>Content-Length</code> 回應標頭將不再準確反映資料大小。為了防止資料傳輸錯誤，執行時期會刪除此回應標頭，並新增 <code>X-Content-Length-Before-Decompression</code> 回應標頭來記錄原始資料大小。</div>


以下範例示範了如何設定 `fetch()` 方法自動解壓縮回應資料，並對於不支援的壓縮格式傳回原始資料。

```js
const response = await fetch("https://www.example.com", {decompression: "fallbackIdentity"});
```


<span id="解壓縮後對-content-encoding-標頭的處理"></span>
#### 解壓縮後對 `Content-Encoding` 標頭的處理

解壓縮後，`fetch()` 方法會相應地修改 `Content-Encoding` 回應標頭：


* `Content-Encoding: identity, gzip` 將被修改為 `Content-Encoding: identity`。

* `Content-Encoding: gzip` 將被刪除。

* `Content-Encoding: gzip, identity` 將被刪除。

* `Content-Encoding: brotli, gzip` 將被修改為 `Content-Encoding:brotli`。


<span id="更多資訊"></span>
## 更多資訊

&nbsp;

<span id="content-length-標頭如何影響承載傳輸"></span>
### Content\-Length 標頭如何影響承載傳輸

`Request` 對象和 `Response` 對象中的 `Content-Length` 標頭會影響承載的傳輸方式：


* 如果`Request` 對象或`Response` 對象包含 `Content-Length` 標頭：

   * 如果 `Content-Length` 標頭的值是等於或大於 0 的數字：執行時期將遵循 `Content-Length` 標頭，並且只傳輸 `Content-Length` 標頭指定的承載位元組數。承載的其餘部分將被捨棄。

   * 如果 `Content-Length` 標頭的值無效：執行時期將忽略 `Content-Length` 標頭，並使用分塊傳輸編碼來傳輸承載。

* 如果`Request` 對象或`Response` 對象不包含 `Content-Length` 標頭，執行時期將使用分塊傳輸編碼來傳輸承載。
