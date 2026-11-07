---
title: "CDN 回應標頭設定"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/response-header-setting_zh-tw"
---

本文件介紹如何在 BytePlus CDN 中配置 HTTP 回應標頭。

預設情況下，在對用戶請求的回應中，CDN 會包含來源伺服器回應中的所有標頭。您可以配置 CDN 在用戶請求的回應中所包含的標頭。

<span id="操作步驟"></span>
## 操作步驟


1. 打開 **CDN 回應標頭設定** 設定頁面。操作步驟參見 [網域名稱設定](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-tw)。

2. 在 **CDN 回應標頭設定** 下方，點擊 **新增規則**。

   您最多可以新增 50 條規則。

3. 參照以下配置說明。

4. 配置完成後，點擊 **儲存**。


<span id="配置說明"></span>
## 配置說明


|**配置** |**說明** |
|---|---|
|回應標頭操作 |表示一個操作類型。該配置有以下選項：<br><br><br>* **設定**：表示設定一個標頭。設定操作包括新增與修改。如果來源伺服器回應中已包含該標頭，該標頭的值會被覆蓋。如果來源伺服器回應中沒有包含該標頭，該標頭會被新增。<br><br>* **刪除**：表示刪除一個標頭。 |
|回應標頭名稱 |表示需要設定或者刪除的一個標頭。標頭名稱是大小寫不敏感的。您可以從下拉列表中選擇一個常用標頭，參見 [常用標頭](https://docs.byteplus.com/en/docs/18/36305#%E5%B8%B8%E7%94%A8%E6%A8%99%E9%A0%AD)。除了 [注意事項](https://docs.byteplus.com/en/docs/18/36305#%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A0%85) 中列出的那些標頭名稱之外，您可以輸入任意一個標頭名稱。標頭名稱不能超過 1,024 個字元，不能包含以下字元：<br><br><br>* 漢字、底線（_）、空格、雙引號（"）、冒號（:） |
|取值方式 |對於您在 **回應標頭名稱** 中指定標頭，該配置表示該標頭值的類型，有以下選項：<br><br><br>* **常數值**：表示該標頭值是一個字串。<br><br>* **變數**：表示該標頭值來自一個變數。<br><br>* **自訂**：表示該標頭值是變數與字串拼接後的一個字串。 |
|回應請求標頭的值 |表示您在 **回應標頭名稱** 中指定標頭的取值。<br><br><br>* 如果 **取值方式** 是 **常數值**，您需要輸入一個字串。該字串的長度不能超過 1,024 個字元，不能包含以下字元：<br><br>   * 漢字、底線（_）、空格、雙引號（"）、冒號（:）<br><br>* 如果 **取值方式** 是 **變數**，您需要從列表中選擇一個變數。參見 [變數列表](https://docs.byteplus.com/en/docs/18/36305#%E8%AE%8A%E6%95%B8%E5%88%97%E8%A1%A8)。<br><br>* 如果 **取值方式** 是 **自訂**，您需要輸入由變數和字串拼接後的一個字串。變數需要包裹在 `{}` 中，由 `$` 開頭。例如 `bind${remote_addr}to${host}done`。<br><br><br>如果 **回應標頭名稱** 是 `Access-Control-Allow-Origin`，您可以在 **回應請求標頭的值** 中輸入多個以逗號（,）分隔的來源 IP 和來源網域名稱，表示允許存取您網域名稱的來源 IP 和來源網域名稱。網域名稱可以是泛網域名稱。 |
|跨域檢驗 |此設定項決定 CDN 是否根據請求標頭中的 Origin 欄位來驗證並設定 `Access-Control-Allow-Origin` 標頭。此設定項僅在滿足以下兩個條件時才會出現：<br><br><br>* **回應標頭名稱** 為 `Access-Control-Allow-Origin`。<br><br>* **取值方式** 為 **常數值**。<br><br><br>`Access-Control-Allow-Origin` 的值支援以下格式：<br><br><br>* 任意來源 ：設定為 `*`。<br><br>* 特定來源 ：設定單個或多個 IP、網域名稱，或者 IP 與網域名稱的組合。多個來源之間用英文逗號 , 分隔。來源必須包含通訊協定 `http://` 或 `https://`，且支援攜帶連接埠。<br><br>* 萬用字元網域 ：網域名稱支援萬用字元網域格式，例如 `https://*.``example.com`。<br><br><br>啟用 **跨域檢驗** 後，CDN 的處理邏輯如下：<br><br><br>* 任意比對 ：如果標頭取值設定為 `*`，無論請求中是否攜帶 `Origin` 標頭，也不論 `Origin` 標頭的值為何，CDN 都會在回應中傳回 `Access-Control-Allow-Origin: *`。<br><br>* 精確比對 ：如果標頭取值設定了單個或多個具體的來源，CDN 會檢查請求標頭中的 `Origin` 值是否與設定的任意一個來源精確比對。<br><br>   * 如果比對成功，CDN 會在回應中傳回 `Access-Control-Allow-Origin` 標頭，該標頭的值為請求中的 `Origin` 值。<br><br>   * 如果比對失敗，CDN 不會在回應中傳回 `Access-Control-Allow-Origin` 標頭。<br><br>* 萬用字元網域比對 ：如果標頭取值設定了萬用字元網域，CDN 會檢查請求標頭中的 `Origin` 值是否比對該萬用字元網域。比對後的處理邏輯與精確比對相同。<br><br><br>如果不啟用 **跨域檢驗**，CDN 不會檢查 `Origin` 標頭，始終將您設定的 `Access-Control-Allow-Origin` 標頭新增到回應中。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">如果 <code>Access-Control-Allow-Origin</code> 的值包含多個來源，強烈建議您開啟 <strong>跨域檢驗</strong>。如果不開啟，CDN 會將所有來源作為標頭值傳回，而瀏覽器通常只允許 <code>Access-Control-Allow-Origin</code> 包含一個值，導致瀏覽器報錯。</div><br> |


<span id="變數列表"></span>
## 變數列表

CDN 提供了以下變數。


|變數名稱 |說明 |示例 |
|---|---|---|
|raw_uri |表示用戶端請求 URL 中的路徑。 |`/dir/sample.php` |
|request_uri |表示用戶端請求 URL 中的路徑和查詢字串（query string）。 |`/dir/sample.php?color=red&n=10` |
|remote_addr |表示發起本次請求的用戶端的 IP 位址。 |`10.10.10.10` |
|remote_port |表示發起本次請求的用戶端的連接埠。 |`5936` |
|host |表示用戶端請求中 host 標頭的值。<br><br>&nbsp;<br><br>需要留意的是，CDN 在處理請求時可能會修改該標頭的值。因此，不建議您使用該標頭，而是使用 `http_host`。 |`www.example.com:8080` |
|http_host |表示用戶端請求中 host 標頭的值。該標頭值不會被 CDN 修改。 | |
|args |表示用戶端請求 URL 中的查詢字串。 |`color=red&n=10` |
|msec |表示 CDN 設定回應標頭的時間，格式是 Unix 時間標記，精確到毫秒。該時間標記接近首包的回應時間。 |`1704444754.917` |
|scheme |表示用戶端使用的協定。 |`https` |
|cdn_cache_status |表示請求是否命中快取。<br><br><br>* `edge_hit`：表示請求命中了快取伺服器的快取。<br><br>* `parent_hit`：表示請求命中了區域伺服器的快取。<br><br>* `miss`：表示請求沒有命中快取 |`edge_hit` |


<span id="常用標頭"></span>
## 常用標頭

CDN 提供了以下常用的標頭。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">這些標頭是標準的 HTTP 回應標頭。如果回應標頭的值是合法的，用戶端瀏覽器會根據回應標頭做相應的操作。根據您的使用場景，您也可以設定這些常用標頭的值為任意字串。例如，您可以設定 <code>Access-Control-Allow-Origin</code> 的值為 <code>helloworld</code>。</div>



|**標頭名稱** |**說明** |**示例** |
|---|---|---|
|Access\-Control\-Allow\-Origin |指定允許存取您網站資源的來源（Origin）。<br><br><br>* 多個來源使用逗號（,）分隔。<br><br>* 您可以指定 `*`，表示任意來源。<br><br>* 來源中的 host 可以是 IP 位址，也可以是網域名稱。網域名稱可以是泛網域名稱。<br><br>* 來源可以包含連接埠。<br><br>* 如果來源不是 `*`，必須以 `http://` 或者 `https://` 開頭。 |示例一<br><br>`*`<br><br>&nbsp;<br><br>示例二<br><br>`https://www.another-site.com:448,http://10.10.10.10,https://*.example.com` |
|Access\-Control\-Allow\-Methods |指定跨域請求允許使用的 HTTP 請求方法。多個方法使用逗號（,）分隔。 |`GET` |
|Access\-Control\-Allow\-Headers |指定跨域請求允許包含的 HTTP 請求標頭。多個請求標頭使用逗號（,）分隔。 |`X-Custom-Header` |
|Access\-Control\-Expose\-Headers |指定在用戶端運行的指令碼所允許存取的回應標頭。多個回應標頭使用逗號（,）分隔。<br><br>&nbsp;<br><br>預設情況下，用戶端指令碼可以存取的回應標頭有 `Cache-Control`、`Content-Language`、`Content-Type`、`Expires`、`Last-Modified`。如果您需要用戶端指令碼存取更多的回應標頭，可以在該標頭中指定。 |`Content-Encoding` |
|Access\-Control\-Allow\-Credentials |指定跨域請求是否需要包含驗證資訊。驗證資訊包括 cookie，驗證請求標頭或用戶端 TLS 憑證。 |`true` |
|Access\-Control\-Max\-Age |指定跨域請求時，用戶端對請求內容發起的預檢請求的快取時長。單位是秒。在快取過期前，用戶端不用再次發送預檢請求。 |`3600` |
|Cache\-Control |對於 CDN 返回的內容，指定該內容在用戶端的快取方式。 |`max-age=3600` |
|Content\-Disposition |指示 CDN 返回給用戶端的內容是以下載的方式提供。並指定下載的檔案名稱。 |`attachment;filename=Demo.xlsx` |
|Content\-Language |指示 CDN 返回給用戶端的內容語言。 |`zh-CN` |
|Content\-Type |指示 CDN 返回給用戶端的內容類型。 |`text/plain` |
|Pragma |對於 HTTP/1.0，指示 CDN 回應在用戶端的快取方式。標頭值只能是 `no-cache`，指示用戶端不要快取 CDN 的回應。 |`no-cache` |


<span id="注意事項"></span>
## 注意事項

您設定的回應標頭名稱不能是以下任意標頭。


* access\-check

* server\-timing

* via

* x\-request\-ip

* x\-tt\-trace\-tag

* x\-bdcdn\-logid

* byte\-error\-code

* x\-bdcdn\-cache\-status
