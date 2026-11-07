---
title: "DescribeCdnConfig"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnConfig_zh-tw"
---

獲取 BytePlus CDN 中一個網域名稱的設定。

<span id="使用限制"></span>
## 使用限制

請求頻率限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=DescribeCdnConfig&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `DescribeCdnConfig`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|Domain |String |是 |表示一個網域名稱，獲取該網域名稱的設定。 |`www.example.com` |


<span id="回應"></span>
## 回應


|參數 |類型 |說明 |範例 |
|---|---|---|---|
|DomainConfig |Object |表示 `Domain` 的設定。 | |
|Domain |String |表示請求參數中的 `Domain`。 |`www.example.com` |
|Origin |Object[] |表示來源伺服器設定。 | |
|OriginAction |Object |表示來源伺服器設定,，套用於所有使用者請求。 | |
|OriginLines |Object[] |表示一個來源伺服器列表。 | |
|Address |String |表示列表中一個來源伺服器的地址。 |`www.example.com` |
|InstanceType |String |表示來源伺服器的類型。該參數有以下取值：<br><br><br>* `ip`：表示 IP 位址。<br><br>* `domain`：表示網域名稱。<br><br>* `tos`：表示物件儲存桶。 |`ip` |
|OriginType |String |表示該來源伺服器的類別。該參數有以下取值：<br><br><br>* `primary`：表示主來源伺服器。<br><br>* `backup`：表示備用來源伺服器。 |`primary` |
|HttpPort |String |表示 CDN 使用 HTTP 協定存取該來源伺服器時所存取的連接埠。 |`80` |
|HttpsPort |String |表示 CDN 使用 HTTPS 協定存取該來源伺ا服器時所存取的連接埠。 |`443` |
|OriginHost |String |表示來源伺服器請求存取的站點網域名稱，優先順序高於全域 `OriginHost` 參數。 |`img.example.com` |
|PrivateBucketAccess |Boolean |表示儲存桶是否為私有桶。該參數僅當 `InstanceType` 為 `tos` 時有效。該參數有以下取值：<br><br><br>* `true`：表示該儲存桶是私有桶。<br><br>* `false`：表示該儲存桶不是私有桶。 |`false` |
|PrivateBucketAuth |Object |表示存取儲存桶的憑證。存取同一 BytePlus 帳戶下的儲存桶無需憑證。 | |
|Switch |Boolean |表示存取儲存桶是否需要憑證。該參數有以下取值：<br><br><br>* `true`：表示需要憑證。<br><br>* `false`：表示無需憑證。 |`false` |
|AuthType |String |表示儲存桶使用的是哪個物件儲存服務所提供的驗證方式。該參數有以下取值：<br><br><br>* `tos`：表示 BytePlus TOS。<br><br>* `cos`：表示騰訊雲 COS。<br><br>* `oss`：表示阿里雲 OSS。<br><br>* `azure`：表示 Microsoft Azure。<br><br>* `aws_common`：表示 AWS S3 或其他使用與 S3 相容的驗證方式的第三方物件儲存服務。 |`cos` |
|TosAuthInformation |Object |表示儲存桶的存取憑證。 | |
|AccessKeyId |String |表示存取憑證中的 Access Key ID，在騰訊雲稱為 SecretId。<br><br>说明<br><br>如果 `AuthType` 是 `azure`，則憑證在 `AccountKey` 中，該參數值為空（""）。 |`xxxxxxxx` |
|AccessKeySecret |String |表示存取憑證中的 Access Key Secret，在騰訊雲稱為 SecretKey。<br><br>说明<br><br>如果 `AuthType` 是 `azure`，則憑證在 `AccountKey` 中，該參數值為空（""）。 |`xxxxxx` |
|AccountKey |String |表示您 Azure 儲存帳戶的共用金鑰（Key）。該參數僅當 `AuthType` 為 `azure` 時有效。 |`xxxxxx` |
|Region |String |表示儲存桶所在地域的資訊，也就是儲存桶的 region code。Region code 參與簽名的計算。 |`us-east-1` |
|Weight |String |表示該來源伺服器的權重，權重越大，該來源伺服器在 CDN 傳送來源伺服器請求時被選擇到的機率也越大。<br><br>該參數僅當 `InstanceType` 為 `ip` 或 `domain` 時才有效。 |`100` |
|BucketName |String |表示您 Azure 儲存帳戶的名稱。該參數僅當 `AuthType` 為 `azure` 時有效。 |`mystorageaccount` |
|OriginProtocol |String |表示來源伺服器請求使用的協定。該參數有以下取值：<br><br><br>* `http`：表示來源伺服器請求使用 HTTP 協定。<br><br>* `https`：表示來源伺服器請求使用 HTTPS 協定。<br><br>* `followclient`：表示來源伺服器協定與使用者請求使用的協定相同。 |`http` |
|AreaAccessRule |Object |表示 "地域存取控制" 特性的設定。 | |
|Area |String[] |表示一個國家和地區的列表，對該列表套用地域存取限制。國家和地區的名稱使用簡寫來表示。您可以呼叫 [DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeCdnRegionAndIsp_zh-tw) 並指定 `Area` 為 `Global` 以取得國家和地區的簡寫。 |`["CHE","AZE"]` |
|RuleType |String |表示 `Area` 的類型。該參數有以下取值：<br><br><br>* `deny`: 表示 `Area` 是一個黑名單。CDN 將封鎖來自這些國家和地區的請求。<br><br>* `allow`: 表示 `Area` 是一個白名單。CDN 僅允許來自這些國家和地區的請求。 |`allow` |
|Switch |Boolean |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示停用該特性。 |`true` |
|BrowserCache |Object[] |表示 "瀏覽器快取" 特性的設定，包含一個規則列表，說明如下：<br><br><br>* 每條規則包含比對條件設定和操作設定。<br><br>* 規則在列表中出現的順序表示規則的優先順序。列表中第一條規則的優先順序最高。<br><br>* 當收到一個使用者請求時，CDN 按規則的優先順序，從高到低將規則與請求比對。如果一條規則比對了請求，CDN 就停止處理其餘規則。 | |
|CacheAction |Object |當一個請求滿足 `Condition` 中的比對條件時，CDN 會對請求檔案執行指定的操作。該參數定義了該操作相關的設定。 | |
|Action |String |表示瀏覽器需要執行的操作。目前該參數值只能是 `cache`，表示快取請求的檔案。`DefaultPolicy` 中指定了如何快取請求的檔案。 |`cache` |
|IgnoreCase |Boolean |表示 `Value` 是否是區分大小寫。<br><br><br>* `true`：表示不區分大小寫。<br><br>* `false`：表示區分大小寫。 |`true` |
|Ttl |Long |表示瀏覽器需要快取請求檔案的時長，單位是秒。CDN 會在回應標頭中包含 `Cache-Control: max-age` 標頭，標頭值就是該參數值。 |`100` |
|DefaultPolicy |String |表示瀏覽器該如何快取請求的檔案。該參數有以下取值：<br><br><br>* `cache`：表示需要快取請求的檔案。<br><br>* `origin_first`：表示遵循來自來源伺服器的快取策略。該策略會包含在 CDN 的回應中。<br><br>* `no_cache`：表示不需要快取請求的檔案。<br><br><br>關於瀏覽器快取策略的詳細資訊，參見 [瀏覽器快取策略](https://docs.byteplus.com/en/docs/byteplus-cdn/browser-cache_zh-tw)。 |`cache` |
|SetCookieNoCache |Boolean |是否设置cookie不缓存，仅支持节点缓存规则 | |
|Condition |Object |表示比對條件的設定。如果請求比對了某個條件，CDN 對該請求執行 `CacheAction` 中指定的操作。 | |
|ConditionRule |Object[] |表示比對條件列表。目前，列表中只能包含一個比對條件。 | |
|Object |String |表示比對物件。該參數有以下取值：<br><br><br>* `filetype`：表示請求 URL 中的副檔名。<br><br>* `directory`：表示請求 URL 中的某個目錄。<br><br>* `path`：表示請求 URL 中的完整路徑。 |`directory` |
|Operator |String |表示比對類型。該參數的值只能是 `match`，表示如果 `Value` 比對了請求中的 `Object`，該請求就滿足這個比對條件。 |`match` |
|Type |String |該參數值只能是 `url`，表示 "請求 URL"。 |`url` |
|Value |String |表示一個或者多個比對值。多個比對值之間使用分號（;）分隔。 |`png` |
|Cache |Object[] |表示 "快取規則" 特性的設定，包含一個規則列表，說明如下：<br><br><br>* 列表中規則的順序定義了規則的優先順序。列表中第一條規則的優先順序最高。<br><br>* 當收到一個使用者請求時，CDN 按規則的優先順序，從高到低將規則與請求比對。如果一條規則比對了請求，CDN 就停止處理其餘規則。 | |
|CacheAction |Object |當一個請求滿足 `Condition` 中的比對條件時，CDN 會對請求檔案執行指定的操作。該參數定義了該操作相關的設定。 | |
|Action |String |表示 CDN 執行的操作。目前該參數值只能是 `cache`，表示快取請求的檔案。`DefaultPolicy` 中指定了如何快取請求的檔案。 |`cache` |
|IgnoreCase |Boolean |表示 `Value` 是否是區分大小寫。該參數有以下取值：<br><br><br>* `true`：表示不區分大小寫。<br><br>* `false`：表示區分大小寫。 |`true` |
|Ttl |Long |表示請求檔案的快取時長，單位為`秒`。<br><br>如果該參數值為 `0`，CDN 在收到符合規則的請求時，會按以下方式處理：<br><br><br>* 如果檔案尚未被快取，CDN 不會快取該檔案。<br><br>* 如果檔案已被快取，該檔案會立即過期，後續對該檔案的請求將觸發 [回源校驗](https://docs.byteplus.com/en/docs/byteplus-cdn/cdn-cache-rules_zh-tw#%E4%BE%86%E6%BA%90%E4%BC%BA%E6%9C%8D%E5%99%A8%E6%A0%A1%E9%A9%97)。這種情況通常發生在您修改快取規則，將已快取檔案的快取時間從非零值改為 `0` 時。 |`100` |
|DefaultPolicy |String |表示 CDN 對請求檔案的快取行為。該參數有以下取值：<br><br><br>* `force_cache`：對應 CDN 控制台中的 **CDN快取** + **強制快取（開）**  的設定組合。<br><br>* `default`：對應 CDN 控制台中的 **CDN快取** + **強制快取（關）**  的設定組合。<br><br>* `origin_first`：對應 CDN 控制台中的 **遵循來源伺服器** + **補充快取（開）**  的設定組合。<br><br>* `origin_first_Replenish`：對應 CDN 控制台中的 **遵循來源伺服器** + **補充快取（關）**  的設定組合。<br><br><br>關於這些快取策略的描述，參見 [快取規則](https://docs.byteplus.com/en/docs/byteplus-cdn/cdn-cache-rules_zh-tw)。 |`force_cache` |
|SetCookieNoCache |Boolean |是否设置cookie不缓存，仅支持节点缓存规则 | |
|Condition |Object |表示比對條件的設定。如果請求比對了某個條件，CDN 對該請求執行 `CacheAction` 中指定的操作。 | |
|ConditionRule |Object[] |表示比對條件列表。 | |
|Object |String |表示比對物件。該參數有以下取值：<br><br><br>* `filetype`：表示請求 URL 中的副檔名。<br><br>* `directory`：表示請求 URL 中的某個目錄。<br><br>* `path`：表示請求 URL 中的完整路徑。 |`directory` |
|Operator |String |表示比對類型。該參數的值只能是 `match`，表示如果 `Value` 比對了請求中的 `Object`，該請求就滿足這個比對條件。 |`match` |
|Type |String |該參數值只能是 `url`，表示 "請求 URL"。 |`url` |
|Value |String |表示一個或者多個比對值。多個比對值之間使用分號（;）分隔。 |`png` |
|CacheHost |Object |表示 "共享快取" 特性的設定。 | |
|CacheHostRule |Object[] |表示一組共享快取的設定。 | |
|CacheHostAction |Object |表示某個設定的詳情。 | |
|CacheHost |String |表示目標網域名稱。 該目標網域名稱必須是您帳戶下的一個另一個網域名稱。該參數指示 `Domain` 共享 `CacheHost` 的 CDN 快取。 |`www.test.com` |
|Switch |Boolean |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示禁用該特性。 |`true` |
|CacheKey |Object[] |表示 "快取索引鍵規則" 特性的設定，包含一個規則列表，說明如下：<br><br><br>* 每條規則包含比對條件設定和操作設定。<br><br>* 規則在列表中出現的順序表示規則的優先順序。列表中第一條規則的優先順序最高。<br><br>* 當收到一個使用者請求時，CDN 按規則的優先順序，從高到低將規則與請求比對。如果一條規則比對了請求，CDN 就停止處理其餘規則。 | |
|CacheKeyAction |Object |當一個請求滿足 `Condition` 中的比對條件時，CDN 會為請求檔案設定快取索引鍵。該參數表示快取索引鍵的設定。 | |
|CacheKeyComponents |Object[] |快取索引鍵是由請求中的 host、路徑和查詢字串等部分組成。該參數表示其中各組成部分的設定。 | |
|Action |String |表示 CDN 如何在請求檔案的快取索引鍵中設定查詢字串。該參數有以下取值：<br><br><br>* `exclude`：表示快取索引鍵不包含請求中的任何查詢參數。<br><br>* `include`：表示快取索引鍵包含請求中所有的查詢參數。<br><br>* `includePart`：表示快取索引鍵僅包含 `Subobject` 中指定的查詢參數。<br><br>* `excludePart`：表示快取索引鍵包含請求中除了 `Subobject` 中指定的查詢參數之外的所有查詢參數。 |`excludePart` |
|IgnoreCase |Boolean |表示 `Subobject` 是否是區分大小寫。該參數有以下取值：<br><br><br>* `true`：表示不區分大小寫。<br><br>* `false`：表示區分大小寫。 |`true` |
|Object |String |表示快取索引鍵中的一個組成部分。當前該參數值只能是 `querystring`，表示查詢字串。 |`queryString` |
|Subobject |String |該參數對應於 `Action`，表示 CDN 在快取索引鍵中包含的具體查詢參數。該參數的說明如下：<br><br><br>* 如果 `Action` 是 `include` 或者 `exclude`，`Subobject` 是 `*`，表示請求中的全部查詢參數。<br><br>* 如果 `Action` 是 `includePart` 或者 `excludePart`，表示需要保留或者不保留的查詢參數。多個查詢參數之間使用分號（;）分隔。 |`sign;testParams` |
|Condition |Object |表示比對條件的設定。如果請求比對了某個條件，CDN 對該請求執行 `CacheKeyAction` 中指定的操作。 | |
|ConditionRule |Object[] |表示比對條件列表。列表中只能包含一個比對條件。 | |
|Object |String |表示比對物件。該參數有以下取值：<br><br><br>* `filetype`：表示請求 URL 中的副檔名。<br><br>* `directory`：表示請求 URL 中的某個目錄。<br><br>* `path`：表示請求 URL 中的完整路徑。 |`directory` |
|Operator |String |表示比對類型。該參數的值只能是 `match`，表示如果 `Value` 比對了請求中的 `Object`，該請求就滿足這個比對條件。 |`match` |
|Type |String |該參數值只能是 `url`，表示 "請求 URL"。 |`url` |
|Value |String |表示一個或者多個比對值。多個比對值之間使用分號（;）分隔。 |`png` |
|IgnoreCase |Boolean |表示 `Value` 是否是區分大小寫。該參數有以下取值：<br><br><br>* `true`：表示不區分大小寫。<br><br>* `false`：表示區分大小寫。 |`true` |
|Compression |Object |表示 "智慧壓縮" 特性的設定。 | |
|Switch |Boolean |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示禁用該特性。 |`true` |
|CompressionRules |Object[] |表示一組規則。每條規則包含比對條件設定以及操作設定。 | |
|CompressionAction |Object |表示當使用者請求滿足 `Condition` 時，CDN 對請求檔案執行的壓縮操作的設定。 | |
|CompressionType |String[] |表示 CDN 使用的一個或者多個壓縮演算法。該參數有以下取值：<br><br><br>* `br`：表示 Brotli 壓縮演算法。<br><br>* `gzip`：表示 Gzip 壓縮演算法。<br><br><br>需要留意的是，CDN 基於使用者請求中 `Accept-Encoding` 標頭來決定是否對請求檔案進行壓縮以及使用的壓縮演算法。 |`["gzip","br"]` |
|CompressionFormat |String |表示 CDN 基於請求中的 `Content-Type` 標頭對請求進行比對。該參數有以下取值：<br><br><br>* `default`：表示如果 `Content-Type` 標頭值在下方的預設清單中，CDN 對請求檔案執行 `CompressionAction` 中設定的操作。<br><br>* `customize`：表示如果 `Content-Type` 標頭值在 `CompressionFormat` 指定的標頭值中，CDN 對請求檔案執行 `CompressionAction` 中設定的操作。<br><br><br>**預設清單**<br><br>text/html、text/xml、text/plain、text/css、application/javascript、application/x\-javascript、application/rss+xml、text/javascript、image/tiff、image/svg+xml、application/json、application/xml、text/plain; charset=utf\-8 |`customize` |
|CompressionTarget |String |表示 `Content-Type` 的過濾值。<br><br><br>* 如果 `CompressionFormat` 為 `default` 或者 `all`，該參數為 `*`。<br><br>* 如果 `CompressionFormat` 為 `customize`，該參數包含一個或者多個檔案類型。多個檔案類型之間以逗號（,）分隔。 |`application/xml,hello/world` |
|MinFileSizeKB |Long |表示檔案大小的最小值，CDN 僅對大小在 `MinFileSizeKB` 和 `MaxFileSizeKB` 所表示的範圍內的檔案進行壓縮。該參數的單位是 KB，使用的進位是 1,024。 |`10` |
|MaxFileSizeKB |Long |表示檔案大小的最大值，單位是 KB，使用的進位是 1,024。如果不指定該參數，表示不限制檔案大小的上限。 |`1000` |
|Condition |Object |表示比對條件的設定。如果請求比對了某個條件，CDN 對該請求執行 `CompressionAction` 中指定的操作。 | |
|ConditionRule |Object[] |表示比對條件列表。 | |
|Object |String |表示比對物件。該參數有以下取值：<br><br><br>* `filetype`：表示請求 URL 中的副檔名。<br><br>* `directory`：表示請求 URL 中的某個目錄。<br><br>* `path`：表示請求 URL 中的完整路徑。 |`directory` |
|Operator |String |表示比對類型。該參數的值只能是 `match`，表示如果 `Value` 比對了請求中的 `Object`，該請求就滿足這個比對條件。 |`match` |
|Type |String |該參數值只能是 `url`，表示 "請求 URL"。 |`url` |
|Value |String |表示一個或者多個比對值。多個比對值之間使用分號（;）分隔。 |`/img/` |
|CustomErrorPage |Object |表示 "自訂錯誤頁面" 特性的設定。 | |
|Switch |Boolean |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示禁用該特性。 |`true` |
|ErrorPageRule |Object[] |表示一個設定規則列表。 | |
|ErrorPageAction |Object |表示規則的相關設定。 | |
|Action |String |表示操作的設定。當前該參數值只能為 `redirect`。表示對用戶端請求進行重新導向。 |`redirect` |
|RedirectCode |String |表示重新導向的回應狀態碼。該參數的取值有 `301`、`302`、`303`、`307`、`308`。<br><br>需要留意的是：<br><br><br>* 對於 301 和 302，如果原請求使用的方法不是 GET，那麼用戶端向新的URL傳送請求時，新請求使用的方法可能變成 GET。<br><br>* 對於 303，新請求使用的方法是 GET。<br><br>* 對於 307 和 308，新請求使用的方法與原請求相同，不會被改變。 |`302` |
|RedirectUrl |String |表示跳轉的目標地址。 |`http://www.test.com/friendlyurl.html` |
|StatusCode |String |表示一個狀態碼，可以是 4xx 或者 5xx。4xx 表示 400\-499 之間的所有狀態碼。5xx 表示 500\-599 之間的所有狀態碼。 |`4xx` |
|DownloadSpeedLimit |Object |表示 "下載限速" 特性的設定。 | |
|Switch |Boolean |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示禁用該特性。 |`true` |
|DownloadSpeedLimitRules |Object[] |表示一個限速規則的列表。該參數的其他說明如下：<br><br><br>* 每條規則包含比對條件設定和限速設定。<br><br>* 列表中規則的出現順序表示規則的優先順序排序。列表中第一條規則的優先順序最高。<br><br>* 當收到一個使用者請求時，CDN 按規則的優先順序，從高到低將規則與請求比對。如果一條規則比對了請求，CDN 就停止處理其餘規則。 | |
|DownloadSpeedLimitAction |Object |表示限速設定。 | |
|SpeedLimitRate |Long |表示 CDN 在回應單個請求時的最大資料傳輸速度，單位是 `B/S`，使用的進位是 `1,024`。 |`500000` |
|SpeedLimitRateAfter |Long |表示一個初始資料量，單位是 `bytes`，使用的進位是 `1,024`。<br><br>當 CDN 對一個請求開始傳輸資料時，在傳輸的資料量達到該初始資料量前，該限速規則不會啟用。<br><br>如果該參數值是 `0`，表示在 CDN 對一個請求開始傳輸第一個位元組時，該限速規則就啟用了。 |`1000` |
|SpeedLimitTime |Object |表示限速規則啟用的日期和時間段。 | |
|DayWeek |String |表示該限速規則啟用的日期，有以下取值：`monday`，`tuesday`，`wednesday`，`thursday`，`friday`，`saturday`，`sunday`，`unlimited`。<br><br>`unlimited` 表示每天。多個日期之間使用分號（;）分隔。 |`monday;friday` |
|BeginTime |String |表示該限速規則啟用的開始時間，格式是 `mm:ss`。 |`05:08` |
|EndTime |String |表示該限速規則啟用的結束時間，格式是 `mm:ss`。 |`16:48` |
|DynamicLimitUnit |String |动态限速类型时必填，表示动态限速单位，可选B/S、KB/S、MB/S | |
|LimitQueryName |String |动态限速类型时必填，表示限速参数名称 | |
|LimitType |String |限速类型。非必填，不传为 normal ，表示固定限速值，dynamic_limit:表示动态限速 | |
|Condition |Object |表示比對條件的設定。如果請求比對了某個條件，CDN 對該請求執行 `DownloadSpeedLimitAction` 中指定的操作。<br><br>如果該參數未出現或者為 `null`，CDN 對所有請求執行 `DownloadSpeedLimitAction` 中指定的操作。 | |
|ConditionRule |Object[] |表示比對條件列表。 | |
|Object |String |表示比對物件。該參數有以下取值：<br><br><br>* `filetype`：表示請求 URL 中的副檔名。<br><br>* `directory`：表示請求 URL 中的某個目錄。<br><br>* `path`：表示完整的請求路徑。<br><br>* `unlimited`：表示網域名稱下的所有檔案。<br><br>* `regex`：表示完整的請求路徑，透過正規表示式比對。 |`filetype` |
|Operator |String |表示比對類型。該參數的值只能是 `match`，表示如果 `Value` 比對了請求中的 `Object`，該請求就滿足這個比對條件。 |`match` |
|Type |String |該參數值只能是 `url`，表示 "請求 URL"。 |`url` |
|Value |String |表示一個或者多個比對值。多個比對值之間使用分號（;）分隔。 |`/www/img/f1/;/www/doc/` |
|FollowRedirect |Boolean |表示 "來源伺服器重新導向跟隨" 特性的設定。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示禁用該特性。 |`true` |
|HTTPS |Object |表示 HTTPS 加密服務的設定。 | |
|Switch |Boolean |表示是否啟用 HTTPS 加密服務。該參數有以下取值：<br><br><br>* `true`：表示啟用 HTTPS 加密服務。<br><br>* `false`：表示禁用 HTTPS 加密服務。 |`true` |
|CertInfo |Object |表示要與網域名稱關聯的憑證。 | |
|CertId |String |表示要關聯的憑證 ID。 |`cert-eb5d99026753499a8a34d2a4f0a08d92` |
|DisableHttp |Boolean |表示是否允許請求 URL 中 Scheme 是 `HTTP` 的請求。該參數有以下取值：<br><br><br>* `true`：表示允許 Scheme 是 `HTTP` 的請求。<br><br>* `false`：表示不允許 Scheme 是 `HTTP` 的請求。 |`false` |
|ForcedRedirect |Object |表示 "HTTP 強制重新導向到 HTTPS" 特性的設定。<br><br>说明<br><br>CDN 提供了兩種協定重新導向的特性。<br><br><br>* HTTP 重新導向到 HTTPS，也就是 `ForcedRedirect` 特性。<br><br>* HTTPS 重新導向到 HTTP，也就是 `HttpForcedRedirect` 特性。<br><br><br>這兩個協定重新導向特性是互斥的。也就是說，其中一個特性啟用了，另一個就不能啟用。 | |
|EnableForcedRedirect |Boolean |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。啟用後，CDN 會將收到的 HTTP 請求重新導向到 HTTPS 請求。<br><br>* `false`：表示禁用該特性。禁用後，CDN 不會將 HTTP 請求重新導向到 HTTPS 請求。 |`true` |
|StatusCode |String |表示當收到 HTTPS 請求時 CDN 的重新導向回應狀態碼。該參數有以下取值：<br><br><br>* `301`：表示返回的狀態碼是 301。<br><br>* `302`：表示返回的狀態碼是 302。 |`301` |
|HTTP2 |Boolean |表示是否為使用者請求啟用 HTTP/2 支援。該參數有以下取值：<br><br><br>* `true`：表示啟用 HTTP/2。<br><br>* `false`：表示禁用 HTTP/2。 |`true` |
|Hsts |Object |表示 HSTS 特性的設定。 | |
|Subdomain |String |表示 HSTS 設定是否也應用於網域名稱的子網域名稱。該參數有以下取值：<br><br><br>* `include`：表示 HSTS 設定應用於子網域名稱網站。<br><br>* `exclude`：表示 HSTS 設定不應用於子網域名稱網站。 |`include` |
|Switch |Boolean |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示禁用該特性。 |`true` |
|Ttl |Long |表示 `Strict-Transport-Security` 回應標頭在瀏覽器中的快取過期時間，單位是秒。<br><br>如果該參數值為 `0`，其效果等同於禁用 HSTS 設定。 |`300` |
|OCSP |Boolean |表示是否啟用 "OCSP 裝訂" 特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示禁用該特性。 |`true` |
|TlsVersion |String[] |表示 "TLS 版本" 特性的設定。該參數指定使用者請求可以使用的 TLS 版本，有以下取值：<br><br><br>* `tlsv1.0`：表示 TLS 1.0。<br><br>* `tlsv1.1`：表示 TLS 1.1。<br><br>* `tlsv1.2`：表示 TLS 1.2。<br><br>* `tlsv1.3`：表示 TLS 1.3。 |`["tlsv1.1","tlsv1.2"]` |
|Keyless |Object |KeylessServer | |
|CertInfoList |Object[] |Keyless服务器证书校验\-CA证书 | |
|CertId |String |证书ID | |
|CertName |String |证书名 | |
|Certificate |Object |证书信息 | |
|Certificate |String |证书内容 | |
|EncryptionCert |String |加密公私钥 | |
|EncryptionKey |String |无 | |
|PrivateKey |String |密钥 | |
|Desc |String |证书描述信息 | |
|EffectiveTime |Long |证书生效起始时间 | |
|EncryType |String |证书类型 国际/国密 | |
|ExpireTime |Long |证书过期时间 | |
|Source |String |证书来源 | |
|CheckType |String |Keyless服务器证书校验 | |
|ClientCertInfoList |Object[] |Keyless服务器证书校验\-客户端证书 | |
|CertId |String |证书ID | |
|CertName |String |证书名 | |
|Certificate |Object |证书信息 | |
|Certificate |String |证书内容 | |
|EncryptionCert |String |加密公私钥 | |
|EncryptionKey |String |无 | |
|PrivateKey |String |密钥 | |
|Desc |String |证书描述信息 | |
|EffectiveTime |Long |证书生效起始时间 | |
|EncryType |String |证书类型 国际/国密 | |
|ExpireTime |Long |证书过期时间 | |
|Source |String |证书来源 | |
|KeylessServer |String |Keyless服务器地址 | |
|Switch |Boolean |Keyless开关 | |
|HttpForcedRedirect |Object |表示 "HTTPS 強制重新導向到 HTTP" 特性的設定。 | |
|EnableForcedRedirect |Boolean |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。啟用後，CDN 會將收到的 HTTPS 請求重新導向到 HTTP 請求。<br><br>* `false`：表示禁用該特性。CDN 不會將 HTTPS 請求重新導向到 HTTP 請求。 |`true` |
|StatusCode |String |表示當收到 HTTPS 請求時，CDN 返回的重新導向狀態碼。該參數有以下取值：**301**、**302**、**303**、**307**、**308**。<br><br>需要留意的是：<br><br><br>* 對於 301 和 302，如果原請求使用的方法不是GET，那麼用戶端向新的URL傳送請求時，新請求使用的方法可能變成 GET。<br><br>* 對於 303，新請求使用的方法是 GET。<br><br>* 對於 307 和 308，新請求使用的方法與原請求相同，不會被改變。 |`302` |
|IPv6 |Object |表示 IPv6 設定。 | |
|Switch |Boolean |表示是否為使用者請求啟用 IPv6 支援。該參數有以下取值：<br><br><br>* `true`：表示啟用 IPv6。<br><br>* `false`：表示禁用 IPv6。 |`true` |
|IpAccessRule |Object |表示 "IP 黑白名單" 特性的設定。<br><br>該特性提供了兩種設定方式：<br><br><br>* 常規設定：指定 `RuleType` 和 `Ip` 對目前網域名稱進行設定。<br><br>* 全域設定：指定 `SharedConfig` 使用一個全域設定。 | |
|Ip |String[] |表示黑名單或白名單中的 IP 位址。 |`["xx.xxx.xx.xx","x.x.x.x"]` |
|RuleType |String |表示 IP 名單的類型。該參數有以下取值：<br><br><br>* `allow`：表示白名單。<br><br>* `deny`：表示黑名單。 |`deny` |
|Switch |Boolean |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示禁用該特性。 |`true` |
|SharedConfig |Object |表示一個全域設定。 | |
|ConfigName |String |表示一個全域設定的名稱。該全域設定的 `ConfigType` 必須是 `deny_ip_access_rule` 或者 `allow_ip_access_rule`。<br><br><br>* `deny_ip_access_rule`：表示 IP 黑名單。<br><br>* `allow_ip_access_rule`：表示 IP 白名單。<br><br><br>您可以呼叫 [ListSharedConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-ListSharedConfig_zh-tw) 獲取全域設定的列表。 |`my_whitelist` |
|DenyStatusCode |Long |拦截状态码 | |
|IpSource |Object |IP判断来源 | |
|SourceList |String[] |无 | |
|Type |String |无 | |
|MethodDeniedRule |Object |表示 "禁用 HTTP Method" 特性的設定。 | |
|Switch |Boolean |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示禁用該特性。 |`true` |
|Methods |String |表示被禁用的一個或多個 HTTP 請求方法。多個方法使用逗號（,）分隔。該參數有以下取值：<br><br><br>* `get`：表示禁用 GET 請求方法。<br><br>* `post`：表示禁用 POST 請求方法。<br><br>* `delete`：表示禁用 DELETE 請求方法。<br><br>* `put`：表示禁用 PUT 請求方法。<br><br>* `head`：表示禁用 HEAD 請求方法。<br><br>* `patch`：表示 PATCH 請求方法。<br><br>* `connect`：表示 CONNECT 請求方法。<br><br>* `options`：表示 OPTIONS 請求方法。 |`delete,put` |
|NegativeCache |Object[] |表示 "狀態碼快取" 特性的設定，包含一個規則列表，說明如下：<br><br><br>* 每條規則包含過比對條件設定和操作設定。<br><br>* 規則在列表中出現的順序表示規則的優先順序。列表中第一條規則的優先順序最高。<br><br>* 當收到一個使用者請求時，CDN 按規則的優先順序，從高到低將規則與請求比對。如果一條規則比對了請求，CDN 就停止處理其餘規則。 | |
|NegativeCacheRule |Object |當一個請求滿足 `Condition` 中的比對條件時，CDN 會對請求檔案執行指定的操作。該參數定義了該操作相關的設定。 | |
|Action |String |表示 CDN 執行的操作。目前該參數值只能是 `cache`，表示快取來源伺服器的回應狀態碼。 |`cache` |
|StatusCode |String |表示一個需要快取的狀態碼，範圍是 `400-599`，可以是 `4xx` 或者 `5xx`。`4xx` 表示 400 到 499 之間的所有狀態碼。`5xx` 表示 500 到 599 之間的所有狀態碼。 |`404` |
|Ttl |Long |表示狀態碼的快取時間。單位是`秒`。 |`100` |
|IgnoreCase |Boolean |表示 `Value` 是否是大小寫敏感的。<br><br><br>* `true`：表示大小寫不敏感。<br><br>* `false`：表示大小寫敏感。 |`true` |
|Condition |Object |表示比對條件的設定。如果請求比對了某个條件，CDN 對該請求執行 `NegativeCacheRule` 中指定的操作。 | |
|ConditionRule |Object[] |表示比對條件列表。 | |
|Object |String |表示比對物件。該參數有以下取值：<br><br><br>* `filetype`：表示請求 URL 中的副檔名。<br><br>* `directory`：表示請求 URL 中的某個目錄。<br><br>* `path`：表示請求 URL 中的完整路徑。 |`directory` |
|Operator |String |表示比對類型。該參數的值只能是 `match`，表示如果 `Value` 比對了請求中的 `Object`，該請求就滿足這個比對條件。 |`match` |
|Type |String |該參數值只能是 `url`，表示 "請求 URL"。 |`url` |
|Value |String |表示一個或者多個比對值。多個比對值之間使用分號（;）分隔。 |`png` |
|OriginAccessRule |Object |表示 "來源伺服器黑白名單" 特性的設定。 | |
|AllowEmpty |Boolean |表示當使用者請求不包含 Origin 標頭時，CDN 處理請求的方式。該參數有以下取值：<br><br><br>* `true`：表示如果請求不包含 Origin 標頭，則該請求被認為比對設定的 Origin 列表。<br><br>* `false`：表示如果請求不包含 Origin 標頭，則該請求被認為不比對設定的 Origin 列表。 |`true` |
|IgnoreCase |Boolean |表示 Origin 列表是否是大小寫敏感的。該參數有以下取值：<br><br><br>* `true`: 表示 Origin 列表是大小寫不敏感的。<br><br>* `false`: 表示 Origin 列表是大小寫敏感的。 |`true` |
|Origins |String[] |表示一個 Origin 列表。 |`["www.test.com"]` |
|RuleType |String |表示 Origin 列表的類型。該參數有以下取值：<br><br><br>* `allow`：表示白名單。<br><br>* `deny`：表示黑名單。 |`deny` |
|Switch |Boolean |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示禁用該特性。 |`true` |
|OriginArg |Object[] |表示 "來源伺服器參數" 設定的規則列表。<br><br><br>* 每條規則包含一個比對條件（`Condition`）和 CDN 執行操作（`OriginArgAction`）。<br><br>* 列表中規則的順序定義了規則的優先順序。列表中第一條規則的優先順序最高。<br><br>* 當收到一個使用者請求時，CDN 按規則的優先順序，從高到低將規則與請求比對。如果一條規則比對了請求，CDN 就停止處理其餘規則。 | |
|Condition |Object |表示比對條件的設定。如果請求滿足該比對條件，CDN 執行 `OriginArgAction` 中指定的操作。 | |
|ConditionRule |Object[] |表示一個比對條件的列表。 | |
|Object |String |表示比對類型。該參數有以下取值：<br><br><br>* `filetype`：表示請求 URL 中的副檔名。<br><br>* `directory`：表示請求 URL 中的某個目錄。<br><br>* `path`：表示請求 URL 中的完整路徑。<br><br>* `regex`：表示請求 URL 中的完整路徑，透過正規表示式比對。 |`directory` |
|Operator |String |表示比對類型。目前，該參數值只能是 `match`，表示只有比對成功才算是滿足了比對條件。 |`match` |
|Type |String |該參數值只能是 `url`，表示 "請求 URL"。 |`url` |
|Value |String |表示一個或多個比對值。多個比對值之間使用分號（;）分隔。 |`/` |
|OriginArgAction |Object |表示在請求滿足 `Condition` 時 CDN 執行的操作。 | |
|OriginArgComponents |Object[] |表示一個操作列表。這些操作定義了 CDN 如何處理來源伺服器請求中的查詢參數。 | |
|Action |String |表示 CDN 執行的操作。該參數有以下取值：<br><br><br>* `include`: 表示來源伺服器請求 URL 中包含使用者請求 URL 中的全部查詢參數。<br><br>* `exclude`：表示來源伺服器請求 URL 中不包含使用者請求 URL 中的任何查詢參數。<br><br>* `addPart`：表示來源伺服器請求 URL 中包含使用者請求 URL 中的全部查詢參數，並額外包含 `Subobject` 中指定的查詢參數。<br><br>* `includePart`：表示如果使用者請求 URL 中包含 `Subobject` 中指定的查詢參數，那麼來源伺服器請求 URL 中包含這些指定的查詢參數。<br><br>* `excludePart`：表示來源伺服器請求 URL 中包含使用者請求 URL 中的全部查詢參數，除了`Subobject` 中指定的查詢參數。<br><br>* `set`：表示來源伺服器請求 URL 中包含使用者請求 URL 中的全部查詢參數。同時，對於 `Subobject` 中指定的查詢參數和參數值，CDN 會執行以下操作:<br><br>   * 如果這些查詢參數在使用者請求 URL 中，CDN 會在來源伺服器請求 URL 中將這些參數的值設定為指定的值。<br><br>   * 如果使用者請求 URL 中不包含這些查詢參數，CDN 會在來源伺服器請求 URL 中新增這些查詢參數。 |`exclude` |
|Object |String |表示 CDN 對哪個物件執行 `Action`。目前，該參數值只能是 `queryString`，表示請求 URL 中的查詢字串。 |`queryString` |
|Subobject |String |表示一個或多個查詢參數。多個查詢參數之間使用分號（;）分隔。<br><br>在比對請求 URL 中的查詢參數時，`Subobject` 中的參數是大小寫敏感的。<br><br>如果 `Subobject` 是 `*`，則表示請求 URL 中的所有查詢參數。 |`*` |
|OriginHost |String |如果來源伺服器上有有多個站點，該參數表示來源伺服器請求存取的站點網域名稱。該參數對所有來源伺服器設定生效，但優先順序低於來源伺服器設定中 `OriginHost` 參數。 |`img.example.com` |
|OriginRange |Boolean |表示 "來源伺服器請求 Range" 特性的設定。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示停用該特性。 |`true` |
|OriginRewrite |Object |表示 "來源伺服器請求 URL 改寫" 特性的設定。 | |
|OriginRewriteRule |Object[] |表示一個規則列表。當 `Switch` 是 `true` 時，該參數為必填。<br><br><br>* 列表中規則的順序定義了規則的優先順序。列表中第一條規則的優先順序最高。<br><br>* 當收到一個使用者請求時，CDN 按規則的優先順序，從高到低嘗試將請求與規則比對。如果請求比對了一條規則，CDN 就停止處理其餘規則。 | |
|OriginRewriteAction |Object |表示 CDN 執行的動作。 | |
|SourcePath |String |表示一個正規表示式，用於比對使用者請求 URL 中的路徑。參見 [設定範例](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-origin-path-rewrite_1-cn-tw#%E8%B7%AF%E5%BE%91%E6%94%B9%E5%AF%AB%E8%A8%AD%E5%AE%9A%E7%AF%84%E4%BE%8B)。 |`^/img/food.png$` |
|TargetPath |String |表示改寫後的路徑。參見 [設定範例](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-origin-path-rewrite_1-cn-tw#%E8%B7%AF%E5%BE%91%E6%94%B9%E5%AF%AB%E8%A8%AD%E5%AE%9A%E7%AF%84%E4%BE%8B)。 |`/png/food.webp` |
|Switch |Boolean |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示停用該特性。 |`true` |
|OriginSni |Object |表示 "來源伺服器請求 SNI" 特性的設定。 | |
|SniDomain |String |指定來源伺服器請求 SNI 的網域名稱。 |`img.example.com` |
|Switch |Boolean |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示停用該特性。 |`true` |
|PageOptimization |Object |表示 "頁面最佳化" 特性的設定。 | |
|OptimizationType |String[] |表示最佳化的物件。該參數有以下取值：<br><br><br>* `html`: 表示 HTML 頁面。<br><br>* `js`: 表示 Javascript 程式碼。<br><br>* `css`: 表示 CSS 程式碼。 |`["html","js"]` |
|Switch |Boolean |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示停用該特性。 |`true` |
|Quic |Object |表示 QUIC 設定。 | |
|Switch |Boolean |表示是否為使用者請求啟用 QUIC。該參數有以下取值：<br><br><br>* `true`：表示啟用 QUIC。<br><br>* `false`：表示停用 QUIC。 |`true` |
|RedirectionRewrite |Object |表示 "URL 重新導向改寫" 特性的設定。 | |
|Switch |Boolean |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示停用該特性。 |`true` |
|RedirectionRule |Object[] |表示一個 URL 重新導向改寫的規則的列表。列表中第一條規則的優先順序最高。<br><br>當收到一個使用者請求時，CDN 按規則的優先順序，從高到低將規則與請求比對。如果一條規則比對了請求，CDN 就停止處理其餘規則。 | |
|RedirectionAction |Object |表示一個 URL 重新導向改寫的規則。 | |
|RedirectCode |String |表示 URL 重新導向的回應狀態碼。該參數的取值有 `301`、`302`、`303`、`307`、`308`。<br><br>需要留意的是：<br><br><br>* 對於 301 和 302，如果原請求使用的方法不是 GET，那麼用戶端向新的URL傳送請求時，新請求使用的方法可能變成 GET。<br><br>* 對於 303，新請求使用的方法是 GET。<br><br>* 對於 307 和 308，新請求使用的方法與原請求相同，不會被改變。 |`301` |
|SourcePath |String |表示檔案的原路徑。也就是請求中包含的路徑。 |`/img/image.png` |
|TargetHost |String |表示目標路徑所屬的網域名稱或 IP 位址。 |`www.test.com` |
|TargetPath |String |表示跳轉後的目標路徑。 |`/png/image.png` |
|TargetProtocol |String |表示 URL重新導向後的新請求所使用的協定。該參數有以下取值：<br><br><br>* `followclient`：表示使用原請求的協定。<br><br>* `http`：表示新請求強制使用 HTTP 協定。<br><br>* `https`：表示新請求強制使用 HTTPS 協定。 |`followclient` |
|TargetQueryComponents |Object |表示原請求 URL 中的查詢參數的處理方式。 | |
|Action |String |表示原請求 URL 中的查詢參數的處理方式。該參數有以下取值：<br><br><br>* `include`：表示在跳轉後的 URL 中包含原請求 URL 中的所有查詢參數。<br><br>* `exclude`：表示在跳轉後的 URL 中不包含原請求 URL 中的任何查詢參數。<br><br>* `includePart`：表示在跳轉後的 URL 中包含原請求 URL 中特定的查詢參數。<br><br>* `excludePart`：表示在跳轉後的 URL 中不包含原請求 URL 中特定的查詢參數。 |`include` |
|Value |String |表示要保留或刪除的查詢參數。多個查詢參數間使用英文分號（;）分隔。如果 `Value` 是 `*`，表示所有的查詢參數。 |`seq` |
|RefererAccessRule |Object |表示 "Referer 黑白名單" 特性的設定。關於不同設定對請求比對結果的影響，參見 [Referer 防盜連結](https://docs.byteplus.com/en/docs/byteplus-cdn/referer-restrictions_zh-tw#%E8%A8%AD%E5%AE%9A%E7%AF%84%E4%BE%8Bw)。 | |
|AllowEmpty |Boolean |表示當使用者請求不包含 Referer 標頭時，CDN 處理請求的方式。該參數有以下取值：<br><br><br>* `true`：表示如果請求不包含 Referer 標頭，則該請求被認為比對設定的 Referer 列表。<br><br>* `false`：表示如果請求不包含 Referer 標頭，則該請求被認為不比對設定的 Referer 列表。 |`true` |
|Referers |String[] |表示一個 Referer 列表。Referers 也可以在 `ReferersType` 中指定。 |`["www.test.com","xxx.xx.x.x","xx.xx.xx.x/24"]` |
|ReferersType |Object |表示一個 `ReferersType` 物件。其包含一個 `CommonType` 物件和一個 `RegularType` 物件，分別表示一個常規 Referer 列表和一個用於比對 Referer 的正規表示式列表。`CommonType` 和 `RegularType` 可以同時存在。 | |
|CommonType |Object |表示一個 `CommonType` 物件，其包含一個常規 Referer 列表。 | |
|IgnoreCase |Boolean |表示 `CommonType` 下的 `Referers` 列表是否是大小寫敏感的。該參數有以下取值：<br><br><br>* `true`: 表示大小寫不敏感。<br><br>* `false`: 表示大小寫敏感。 |`true` |
|Referers |String[] |表示一個常規 Referer 列表。 |`["www.test.com","xxx.xxx.xx.xxx","1xx.xx.xx.x/24"]` |
|IgnoreScheme |Boolean |表示 CDN 是否對 Referer 中的 scheme 進行校驗，也就是校驗 Referer 是否包含 `http://` 或 `https://`。該參數有以下取值：<br><br><br>* `true`: 表示 CDN 不校驗 Referer 是否包含 scheme。在這種情況下，無論 Referer 是否包含 scheme，CDN 都會將 Referer 與設定的名單進行比對校驗。<br><br>* `false`: 表示 CDN 會先校驗 Referer 是否包含 scheme。只有 Referer 包含 scheme，CDN 才會將 Referer 與設定的名單進行比對校驗。否則，CDN 判定請求與設定的名單不比對。<br><br><br>該設定對 `RegularType` 下的正規表示式列表不生效，因為 CDN 依賴正規表示式來判斷 Referer 是否比對正規名單。 |`false` |
|ContMainDomain |Boolean |泛域名匹配包含主域名 | |
|RegularType |Object |表示一個 `RegularType` 物件，其包含一個正規表示式列表用來比對請求中的 Referer 標頭。 | |
|Referers |String[] |表示一個用於比對 Referer 的正規表示式列表。 |`^http://a.com` |
|RuleType |String |表示 Referer 名單的類型。該參數有以下取值：<br><br><br>* `allow`：表示白名單。<br><br>* `deny`：表示黑名單。 |`deny` |
|Switch |Boolean |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示停用該特性。 |`true` |
|SharedConfig |Object |表示一個全域性設定。 | |
|ConfigName |String |表示一個全域性設定的名稱。該全域性設定的 `ConfigType` 必須是 `deny_referer_access_rule` 或 `allow_referer_access_rule`。<br><br><br>* `deny_referer_access_rule`：表示 Referer 黑名單。<br><br>* `allow_referer_access_rule`：表示 Referer 白名單。<br><br><br>您可以呼叫 [ListSharedConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-ListSharedConfig_zh-tw) 獲取全域性設定的列表。 |`my_allowlist` |
|RemoteAuth |Object |表示 "遠程驗證" 特性的設定。 | |
|Switch |Boolean |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示停用該特性。 |`true` |
|RemoteAuthRules |Object[] |表示一個驗證規則的列表。每條規則包含比對條件設定和驗證設定。 | |
|Condition |Object |表示比對條件的設定。如果一個請求滿足比對條件，CDN 對該請求執行 `RemoteAuthRuleAction` 中指定的操作。 | |
|ConditionRule |Object[] |表示比對條件列表。<br><br>這些比對條件之間的關係是 "或"，表示如果一個請求滿足任意比對條件，CDN 就對該請求執行 `RemoteAuthRuleAction` 中指定的操作。 | |
|Object |String |表示比對物件。該參數有以下取值：<br><br><br>* `filetype`：表示請求 URL 中的副檔名。<br><br>* `directory`：表示請求 URL 中的某個目錄。<br><br>* `path`：表示請求 URL 中的完整路徑。 |`filetype` |
|Operator |String |表示比對類型。該參數有以下取值：<br><br><br>* `match`：表示如果 `Value` 比對了請求中的 `Object`，該請求就滿足這個比對條件。<br><br>* `not_match`：表示如果 `Value` 不比對請求中的 `Object`，該請求就滿足這個比對條件。 |`match` |
|Type |String |該參數值只能是 `url`，表示 "請求 URL"。 |`url` |
|Value |String |表示一個或多個比對值，多個比對值之間使用分號（;）分隔。 |`png;jpg` |
|RemoteAuthRuleAction |Object |表示驗證相關的設定。<br><br>當一個請求滿足 `Condition` 中的比對條件時，CDN 會將其傳送到驗證伺服器進行驗證，並基於驗證的結果接受或拒絕該請求。 | |
|AuthModeConfig |Object |表示驗證伺服器的設定。 | |
|MasterRemoteAddr |String |表示驗證伺服器的主位址。 |`https://primary.example.com` |
|PathType |String |表示驗證請求的路徑。驗證位址和請求路徑組成了完整的驗證 URL。CDN 會把使用者的請求轉發到該驗證 URL。該參數有以下取值：<br><br><br>* `constant`：表示驗證請求中的路徑與使用者請求中的路徑相同。<br><br>* `variable`：表示 `pathValue` 中指定的路徑。 |`constant` |
|RequestMethod |String |表示在傳送驗證請求時，CDN 所使用的請求方法。該參數有以下取值：<br><br><br>* `default`：表示驗證請求所使用的方法與使用者的請求相同。<br><br>* `get`：表示驗證請求使用 GET 方法。<br><br>* `post`：表示驗證請求使用 POST方法。<br><br>* `head`：表示驗證請求使用 HEAD 方法。 |`get` |
|BackupRemoteAddr |String |表示驗證伺服器的備用位址。 |`https://secondary.example.com` |
|PathValue |String |表示一個驗證請求的路徑。 |`/auth` |
|AuthResponseConfig |Object |CDN 需要對驗證伺服器返回的驗證狀態碼進行處理。該參數表示相關的設定。 | |
|CacheAction |Object |CDN 可以快取驗證狀態碼。該參數表示相關的設定。 | |
|Action |String |表示 CDN 是否快取驗證狀態碼。該參數有以下取值：<br><br><br>* `nocache`：表示 CDN 不快取驗證狀態碼。<br><br>* `cache`：CDN 快取驗證狀態碼。 |`nocache` |
|Ttl |Long |表示驗證狀態碼的快取時間，單位是秒。 |`5` |
|CacheKey |String[] |快取 key 指定了用於區分不同請求 URI 的查詢參數。每個參數都必須以 `$` 開頭。參見 [遠端驗證](https://docs.byteplus.com/en/docs/byteplus-cdn/remote-authentication_zh-tw#%E9%A9%97%E8%AD%89%E8%AB%8B%E6%B1%82%E5%8F%83%E6%95%B8)中的參數。 |`[$URI,$host]` |
|ResponseAction |Object |表示驗證失敗時，CDN 如何回應使用者。 | |
|StatusCode |String |表示驗證失敗時，CDN 回應使用者的狀態碼。 |`403` |
|StatusCodeAction |Object |表示 CDN 對驗證狀態碼的處理方式。 | |
|DefaultAction |String |表示如果驗證狀態碼既不是 `FailCode`，又不是 `SuccessCode` 時，CDN 處理驗證請求的方式。該參數有以下取值：<br><br><br>* `reject`：表示 CDN 認為驗證失敗。<br><br>* `pass`：表示 CDN 認為驗證成功。 |`pass` |
|FailCode |String |表示驗證失敗時的驗證狀態碼。多個狀態碼使用英文分號（;）分隔。 |`403` |
|SuccessCode |String |表示驗證成功時的驗證狀態碼。多個狀態碼使用英文分號（;）分隔。 |`200` |
|TimeOutAction |Object |表示驗證超時後，CDN 如何處理驗證請求。 | |
|Action |String |表示驗證超時後，CDN 處理驗證請求的策略。該參數有以下取值：<br><br><br>* `reject`：表示 CDN 認為驗證失敗。<br><br>* `pass`：表示 CDN 認為驗證成功。 |`reject` |
|Time |Long |表示驗證超時的時間，單位是毫秒。 |`200` |
|QueryStringRules |Object |表示驗證請求的參數設定。 | |
|QueryStringComponents |Object |表示驗證請求參數的設定策略。 | |
|Action |String |表示驗證請求是否包含使用者請求 URL 中的查詢參數。該參數有以下取值：<br><br><br>* `exclude`：表示驗證請求不包含任何查詢參數。<br><br>* `include`：表示驗證請求包含所有查詢參數。<br><br>* `includePart`：表示驗證請求包含指定的查詢參數。 |`exclude` |
|Value |String |表示 `Action` 參數所對應的參數值。`*` 表示所有查詢參數。 |`*` |
|QueryStringInstances |Object[] |表示驗證請求中額外的參數設定。 | |
|Action |String |表示如何設定驗證請求參數。目前參數值只能是 `set`。`set` 表示設定參數。`Key` 指定了需要設定的驗證請求參數。<br><br><br>* 如果指定的驗證請求參數不存在，CDN 會在驗證請求中新增該參數。<br><br>* 如果指定的驗證請求參數已存在，CDN 會使用 `Value` 的值作為該驗證請求參數的值。 |`set` |
|Key |String |表示需要設定的驗證請求參數。 |`sign` |
|Value |String |表示驗證請求參數的值，區分大小寫。 |`1235565` |
|ValueType |String |表示 `Key` 指定的驗證請求參數的類型。`ValueType` 有以下取值：<br><br><br>* `constant`：表示驗證請求參數是一個常數。<br><br>* `variable`：表示驗證請求參數的值來自一個變數。參見 `Value` 的說明。<br><br>* `customize`：表示驗證請求參數的值是一個變數與固定字串拼接後的字串。 |`variable` |
|RequestHeaderRules |Object |表示驗證請求標頭的設定。 | |
|RequestHeaderComponents |Object |表示驗證請求標頭的設定策略。 | |
|Action |String |表示驗證請求標頭是否包含使用者請求標頭。該參數有以下取值：<br><br><br>* `exclude`：表示驗證請求標頭中不包含任何使用者請求標頭。<br><br>* `include`：表示驗證請求標頭中包含所有使用者請求標頭。<br><br>* `includePart`：表示驗證請求標頭包含指定的使用者請求標頭。 |`exclude` |
|Value |String |表示 `Action` 參數所對應的參數值。如果參數值是 `*`，表示所有請求標頭。 |`*` |
|RequestHeaderInstances |Object[] |表示一組驗證請求標頭的設定。<br><br>需要留意的是，在 CDN 發起驗證請求時，請求中可能已經包含了以下標頭：<br><br><br>* `X-Forwarded-Protocol`，`X-Forwarded-Proto`，`X-Client-Scheme`：這三個標頭都表示使用者請求所使用協議，沒有區別。<br><br>* `X-Real-IP`：表示使用者真實的 IP 位址。該標頭的值不會受代理伺服器的影響。<br><br>* `X-Forwarded-For`：表示使用者的 IP 位址。如果使用者的請求經過了代理伺服器，該標頭的值會變成代理伺服器的 IP 位址。 | |
|Action |String |表示如何設定驗證請求標頭。當前該參數值只能為 `set`，表示設定請求標頭。`Key` 指定了需要設定的請求標頭。<br><br><br>* 如果設定的請求標頭不存在，CDN 會在驗證請求中新增該請求標頭。<br><br>* 如果設定的請求標頭已存在，CDN 會使用 `Value` 的值作為該請求標頭的值。 |`set` |
|Key |String |表示需要設定的請求標頭。 |`x-test-header` |
|ValueType |String |表示請求標頭的類型。該參數有以下取值：<br><br><br>* `constant`：表示請求標頭的值是一個常數。<br><br>* `variable`：表示請求標頭的值來自一個變數。<br><br>* `customize`：表示請求標頭的值是一個變數與固定字串拼接後的字串。 |`variable` |
|Value |String |表示請求標頭的值。 |`1234fdf` |
|RequestHost |String |表示驗證請求中 HOST 標頭的值。該參數的預設值是 `default`，表示 HOST 標頭的值與網域名稱相同。 |`www.example.com` |
|RequestHeader |Object[] |表示 "來源伺服器請求 HTTP 請求標頭" 特性的設定。 | |
|RequestHeaderAction |Object |表示一個請求標頭的設定規則列表。每個規則都包含一個標頭的相關操作設定。 | |
|RequestHeaderInstances |Object[] |表示一個請求標頭的設定規則列表。每個規則都包含一個標頭的相關操作設定。 | |
|Action |String |表示對請求標頭的操作。該參數有以下取值：<br><br><br>* `set`：表示設定一個標頭。設定操作包括新增與修改。如果請求中已包含該標頭，該標頭的值會被覆寫。如果請求中沒有包含該標頭，該標頭會被新增。<br><br>* `delete`，表示刪除一個標頭。 |`set` |
|Key |String |表示一個標頭的名稱，不區分大小寫。 |`Cdn-provider` |
|ValueType |String |表示 `Key` 的取值類型。該參數僅當 `Action` 是 `set` 的時候才有效。該參數有以下取值：<br><br><br>* `constant`：表示 `Key` 的值是一個固定字串。<br><br>* `variable`：表示 `Key` 的值來自一個變數。<br><br>* `customize`：表示 `Key` 的值是變數與固定字串拼接後的一個字串。 |`constant` |
|Value |String |表示 `Key` 的值。 |`bp-cdn` |
|ResponseHeader |Object[] |表示 "HTTP 回應標頭" 特性的設定。 | |
|ResponseHeaderAction |Object |表示 CDN 在回應使用者請求的時候，對回應標頭的操作。 | |
|ResponseHeaderInstances |Object[] |表示一個回應標頭的設定規則列表。每個規則都包含一個標頭的相關操作設定。 | |
|Action |String |表示對回應標頭的操作。該參數有以下取值：<br><br><br>* `set`：表示設定一個標頭。設定操作包括新增與修改。如果來源伺服器回應中已包含該標頭，該標頭的值會被覆寫。如果來源伺服器回應中沒有包含該標頭，該標頭會被新增。<br><br>* `delete`，表示刪除一個標頭。 |`set` |
|Key |String |表示一個標頭的名稱。 |`Content-Disposition` |
|ValueType |String |表示 `Key` 的取值類型。該參數僅當 `Action` 是 `set` 的時候才有效。該參數有以下取值：<br><br><br>* `constant`：表示 `Key` 的值是一個字串。<br><br>* `variable`：表示 `Key` 的值來自一個變數。<br><br>* `customize`：表示 `Key` 的值是一個變數與字串拼接後的字串。 |`constant` |
|AccessOriginControl |Boolean |表示在 CDN 回應使用者請求時，是否校驗請求中的 Origin 標頭。<br><br>該參數有以下取值：<br><br><br>* `true`：表示 CDN 會校驗 Origin 標頭。如果校驗成功，CDN 會在回應中包含 Access\-Control\-Allow\-Origin 標頭。標頭值與 Origin 標頭值相同。如果校驗失敗，回應中不會包含 Access\-Control\-Allow\-Origin 標頭。<br><br>* `false`：表示 CDN 不會校驗 Origin 標頭。在回應中，CDN 會包含 Access\-Control\-Allow\-Origin 標頭。標頭值是設定的 Access\-Control\-Allow\-Origin 的內容。<br><br><br>該參數僅在以下條件都滿足的情況下有效：<br><br><br>* `Action` 是 `set`。<br><br>* `Key` 是 `Access-Control-Allow-Origin`。<br><br>* `ValueType` 是 `constant`。 | |
|Value |String |表示 `Key` 的值。 |`attachment;filename=FileName.xls` |
|ServiceRegion |String |表示網域名稱的服務區域。該參數有以下取值：<br><br><br>* `chinese_mainland`：表示中國大陸。<br><br>* `global`：表示全球。<br><br>* `outside_chinese_mainland`：表示全球（不含中國大陸）。 |`outside_chinese_mainland` |
|SignedUrlAuth |Object |表示 "URL 驗證" 特性的設定。 | |
|Switch |Boolean |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示停用該特性。 |`true` |
|SignedUrlAuthRules |Object[] |表示一個規則列表。每條規則包含比對條件設定和驗證設定。 | |
|Condition |Object |表示比對條件的設定。CDN 對符合條件的使用者請求進行驗證。 | |
|ConditionRule |Object[] |表示一個比對條件列表。 | |
|Object |String |表示比對條件中的比對類型。該參數有以下取值：<br><br><br>* `filetype`：表示 URL 路徑末尾的副檔名。<br><br>* `directory`：表示 URL 路徑中的一個目錄。<br><br>* `path`：表示完整的 URL 路徑。<br><br>* `regex`: 表示完整的 URL 路徑，透過正規表示式比對。 |`directory` |
|Operator |String |表示比對條件中的比對方式。該參數有以下取值：<br><br><br>* `match`：表示如果 `object` 比對 `Value`，該請求就滿足了這個比對條件。<br><br>* `not_match`：表示如果 `object` 不比對 `Value`，該請求就滿足了這個比對條件。 |`match` |
|Type |String |表示比對物件。當前該參數值必須是 `url`，表示 URL 請求連結。 |`url` |
|Value |String |表示比對條件中的比對值。 |`png;jpg` |
|Connective |String |表示多個 `ConditionRule` 之間的邏輯關係。該參數有以下取值：<br><br><br>* `AND`: 表示邏輯關係是 "AND"。<br><br>* `OR`：表示邏輯關係是 "OR"。 |`OR` |
|SignedUrlAuthAction |Object |表示簽章計算的設定。 | |
|Duration |Long |表示簽章的有效時間，單位是秒。該參數與請求中包含時間標記搭配使用，用來計算簽章的過期時間。簽章的過期時間 = 時間標記 + `Duration`。在 CDN 收到某個請求時，如果簽章的過期時間小於當前時間，CDN 判定簽章已過期。 |`1000` |
|MasterSecretKey |String |表示主金鑰。 |`abcdefg` |
|URLAuthType |String |簽章類型。該參數有以下取值：`typea`、`typeb`、`typec`、`typed`、`typee`，每種類型得驗證說明見 [URL 驗證概覽](https://docs.byteplus.com/en/docs/byteplus-cdn/signed-url-authentication-overview_zh-tw) 。 |`typea` |
|BackupSecretKey |String |表示備用金鑰。 |`abcdefg` |
|CustomVariableRules |Object |表示自訂簽算變數。 | |
|CustomVariableInstances |Object[] |表示一個變數列表。 | |
|Operator |String |表示變數的比對方式。該參數的取值只能是 `match`。 |`match` |
|Type |String |表示變數的類型。該參數有以下取值：<br><br><br>* `queryString`：表示該變數是請求中的一個查詢參數。<br><br>* `requestHeader`：表示該變數是請求中的一個標頭欄位。 |`queryString` |
|Value |String |表示變數的名稱。 |`myparam1` |
|RewriteM3u8 |Boolean |對於 HLS Manifest (.m3u8) 的請求，該參數表示 CDN 是否要修改 Manifest，從而為每個影片分片產生簽章並將簽章新增到 URI 中。<br><br>該參數有以下取值：<br><br><br>* `true`：表示需要修改 Manifest。<br><br>* `false`：表示不需要修改 Manifest。<br><br><br>说明<br><br>當前，CDN 不會修改壓縮檔案。因此，在以下任何情況下，CDN 都不會修改 Manifest。<br><br><br>* 來源伺服器回應中包含 `Content-Encoding` 標頭。該標頭表明該 Manifest 已被壓縮。<br><br>* 使用者請求比對 "智慧壓縮" 特性中的規則。 |`true` |
|SignName |String |表示簽章參數的名稱。 |`sign` |
|SignatureRule |String[] |當 `URLAuthType` 為 `typee` 時，該參數有效，表示需要納入簽章計算的欄位。必須納入簽章計算的欄位如下：<br><br><br>* `key`：表示`MasterSecretKey`或 `BackupSecretKey` 指定的金鑰。<br><br>* `uri`：表示使用者請求的 URI，僅包含字路徑和查詢參數。<br><br>* `TimeName`：表示 `TimeFormat` 指定的時間標記。<br><br><br>可選擇納入簽章計算的欄位如下：<br><br><br>* `domain`：表示網域名稱。<br><br>* `referer`：表示使用者請求攜帶的 referer 值。<br><br>* `ua`：表示使用者請求攜帶的 User\-Agent 值。<br><br>* `ip`：表示使用者請求的用戶端 IP。<br><br>* `origin`：表示使用者請求攜帶的 Origin 值。<br><br>* 自訂變數：表示您在 `CustomVariableInstances` 中定義的變數的值。<br><br><br>CDN 按列表中欄位的順序將這些欄位拼接成一個字串，然後計算該字串的 MD5 值。該 MD5 值就是簽章。 |`["domain","ip","key","TimeName","uri"]` |
|TimeFormat |String |表示 `TimeName` 使用的進位。該參數有以下取值：<br><br><br>* `decimal`：表示十進位。<br><br>* `heximal`：表示十六進位。 |`heximal` |
|TimeName |String |表示時間標記參數的名稱。 |`TimeParam` |
|DeleteAuthCacheAndOrigin |Boolean |去除鉴权参数缓存和回源，仅类型e | |
|AuthRulesF |Object[] |表示 Type\-F 設定，包含一個規則列表。列表中第一條規則的優先順序最高。<br><br>當收到一個使用者請求時，CDN 按規則的優先順序，從高到低將規則與請求比對。如果一條規則比對了請求，CDN 就停止處理其餘規則。 | |
|RuleName |String |表示規則列表中一條規則的名稱。 |`Authentication rule A` |
|Condition |Object |表示比對條件的設定。如果一個請求符合比對條件，CDN 對該請求進行 URL 驗證。 | |
|ConditionRule |Object[] |表示一個比對條件列表。 | |
|Object |String |表示比對物件。該參數有以下取值：<br><br><br>* `filetype`：表示請求檔案的副檔名。<br><br>* `directory`：表示請求路徑中的某个目錄。<br><br>* `path`：表示請求的完整路徑，不包含查詢字串。<br><br>* `regex`：表示用於比對完整路徑的正規表示式。 |`directory` |
|Operator |String |表示比對運算子。該參數有以下取值：<br><br><br>* `match`：表示如果 `Value` 比對了請求中的 `Object`，則該請求符合這個比對條件。<br><br>* `not_match`：表示如果 `Value` 不比對請求中的 `Object`，該請求就符合這個比對條件。 |`match` |
|Type |String |表示比對物件的來源。當前，該參數值只能是 `url`，表示請求 URL。 |`url` |
|Value |String |表示一個或者多個比對值。多個比對值之間使用分號（;）分隔。 |`/chs/foods/;/us/birds/` |
|Connective |String |表示比對條件之間的關係。該參數有以下取值：<br><br><br>* `OR`：表示關係是 "或"。<br><br>* `AND`：表示關係是 "和"。 |`OR` |
|SecretKey |Object |表示用於計算權杖的金鑰。包含一個主金鑰和一個備用金鑰。 | |
|MasterSecretKey |String |表示主金鑰。 |`primary-key-123` |
|BackupSecretKey |String |表示備用金鑰。 |`secondary-key-456` |
|SignCapRule |Object |表示從使用者請求中獲取權杖的方式。 | |
|ArgSegment |Object |表示基於 `ParamName` 或 `UriLevel` 獲取的內容是否需要被拆分，以提取某個層級的片段。該層級的片段才是需要獲取的權杖。 | |
|Switch |Boolean |表示獲取到的內容是否需要被拆分。該參數有以下取值：<br><br><br>* `true`：表示內容需要被拆分。<br><br>* `false`：表示內容無需被拆分。 |`true` |
|Level |Long |表示將內容拆分為多個層級的片段後，權杖所在的層級。<br><br>如果層級是負整數，表示從最右邊的片段開始向左計數。 |`2` |
|SplitSymbol |String |表示用於拆分內容的分隔符。 |`//` |
|CapMode |String |表示權杖的來源。該參數有以下取值：<br><br><br>* `name`：表示查詢參數。相關設定在 `ParamName` 中指定。<br><br>* `uri`：表示請求路徑中的一個目錄。相關設定在 `UriLevel` 中指定。<br><br>* `header`：表示請求中的一個標頭。相關設定在 `CustomValue` 中指定。<br><br>* `cookie`：表示請求中的一個 cookie。相關設定在 `CustomValue` 中指定。 |`name` |
|CustomValue |String |該參數的含義如下：<br><br><br>* 當 `CapMode` 是 `header` 時，該參數表示指定的請求標頭。<br><br>* 當 `CapMode` 是 `cookie` 時，該參數表示指定的 cookie 的 key，CDN 會獲取該 cookie 的 value。 |`myheader` |
|ParamName |String |當 `CapMode` 是 `name` 時，該參數表示要指定的查詢參數。 |`myparam` |
|UriLevel |Long |當 `CapMode` 是 `uri` 時，該參數表示指定的目錄層級。<br><br>如果層級是負整數，表示從路徑最右邊的目錄開始向左計數。 |`3` |
|ExpireTimeRule |Object |表示權杖過期時間的相關設定。 | |
|Duration |Long |表示權杖的有效時長（TTL），單位是秒。<br><br><br>* 權杖過期時間 = 基於 `ExpTimeCapRule` 獲取的權杖時間標記 + `Duration` |`20` |
|ExpTimeCapRule |Object |表示權杖時間標記的獲取方式。權杖時間標記是一個 Unix 時間標記。 | |
|CapMode |String |表示權杖時間標記的來源。該參數有以下取值：<br><br><br>* `name`：表示查詢參數。相關設定在 `ParamName` 和 `ArgSegment` 中指定。<br><br>* `uri`：表示請求路徑中的一個目錄。相關設定在 `UriLevel` 和 `ArgSegment` 中指定。<br><br>* `header`：表示請求中的一個標頭。相關設定在 `CustomValue` 中指定。<br><br>* `cookie`：表示請求中的一個 cookie。相關設定在 `CustomValue` 中指定。 |`header` |
|ParamName |String |當 `ParamType` 是 `ReqHeader` 時，該參數表示指定的查詢參數。 |`myparm1` |
|UriLevel |Long |當 `ParamType` 是 `uri` 時，該參數表示指定的目錄層級。<br><br>如果層級是負整數，表示從路徑最右邊的目錄開始向左計數。 |`2` |
|ArgSegment |Object |表示基於 `ParamName` 或 `UriLevel` 獲取的內容是否需要被拆分，以提取某個層級的片段。該層級的片段才是需要獲取的權杖時間標記。 | |
|Switch |Boolean |表示獲取到的內容是否需要被拆分。該參數有以下取值：<br><br><br>* `true`：表示內容需要被拆分。<br><br>* `false`：表示內容無需被拆分。 |`true` |
|Level |Long |表示將內容拆分為多個層級的片段後，權杖時間標記所在的層級。<br><br>如果層級是負整數，表示從最右邊的片段開始向左計數。 |`2` |
|SplitSymbol |String |表示用於拆分內容的分隔符。 |`-` |
|CustomValue |String |該參數的含義如下：<br><br><br>* 當 `CapMode` 是 `header` 時，該參數表示指定的請求標頭。<br><br>* 當 `CapMode` 是 `cookie` 時，該參數表示指定的 cookie 的 key，CDN 會獲取該 cookie 的 value。 |`myheader1` |
|TimeFormat |String |表示權杖時間標記的格式。<br><br><br>* `octal`：表示八進位。例如 `14751410031`。<br><br>* `decimal`：表示十進位。例如 `1738936345`。<br><br>* `heximal`：表示十六進位。例如 `67a61019`。 |`heximal` |
|AuthTokenCalRule |Object |表示權杖計算的設定。<br><br>CDN 使用 `SignJoinSymbol` 將 `SignParam` 中的各物件進行拼接，然後對拼接後的物件應用 `ParamCalRules` 中指定的演算法計算權杖，用於與使用者請求中包含的權杖進行比較。 | |
|ParamCalRules |String[] |表示計算權杖所使用的演算法列表。CDN 按列表中演算法的出現順序產生權杖的計算公式。<br><br>該參數有以下取值：`md5_bin`、`base64url`、`sha256`、`md5`、`base64_encode`、`sha1`、`sha224`、`sha384`、`sha512`、`sha3_224`、`sha3_256`、`sha3_384`、`sha3_512`、`upper_case`、`lower_case`。 |`["sha1"、"md5_bin"、"base64url"]` |
|SignJoinSymbol |String |表示拼接 `SignParam` 中各物件而使用的拼接符。 |`00` |
|SignParam |Object[] |表示 CDN 在計算權杖時使用的物件列表。每個物件由 `ParamType` 和相關設定組成。例如，以下範例表示物件是一個字串，字串的值是 `str-for-token-calc`。<br><br>```json```<br>```{```<br>```    "ParamType": "SupString",```<br>```    "SupContent": "str-for-token-calc"```<br>```}```<br> | |
|ParamType |String |表示物件的類型。該參數有以下取值：<br><br><br>* `SecretKey`：表示 `SecretKey` 結構體中的 `MasterSecretKey` 或 `BackupSecretKey`。當驗證失敗時，CDN 會使用 `BackupSecretKey` 計算權杖，重新對使用者請求進行驗證。<br><br>* `SupString`：表示一個字串。相關設定在 `SupContent` 中指定。<br><br>* `URI`：表示請求路徑中的連續片段。路徑不包含查詢字串。相關設定在 `UriParamSup` 與 `ParamSource` 中指定。<br><br>* `URLParam`：表示請求 URL 中的某類物件。物件可以是一個查詢參數或某個目錄。相關設定在 `UriParam` 與 `ParamSource` 中指定。<br><br>* `ClientDomain`：表示請求網域名稱。<br><br>* `Referer`：表示使用者請求中 Referer 標頭的值。<br><br>* `Origin`：表示使用者請求中 Origin 標頭的值。<br><br>* `ClientIP`：表示傳送使用者請求的用戶端 IP 位址。<br><br>* `UA`：表示使用者請求中 Use\-Agent 標頭的值。<br><br>* `ReqHeader`：表示使用者請求中某個標頭的值。相關設定在 `RequestHeader` 中指定。<br><br>* `Cookie`：表示請求中的一個 cookie。相關設定在 `CookieToken` 中指定。<br><br>* `FullURI`：表示請求的完整路徑，不包含查詢字串。相關設定在 `ParamSource` 中指定。 |`URI` |
|CookieToken |String |當 `ParamType` 是 `Cookie` 時，該參數表示指定的 cookie 的 key。CDN 會獲取該 cookie 的 value。 |`mycookiekey` |
|RequestHeader |String |當 `ParamType` 是 `ReqHeader` 時，該參數表示指定的請求標頭。 |`myheader2` |
|SupContent |String |當 `ParamType` 是 `SupString` 時，該參數表示指定的字串。 |`123abc` |
|UriParamSup |Object |表示從請求路徑中獲取連續片段的方式。<br><br>該參數是一個結構體，包含以下設定：<br><br><br>* 拆分請求路徑所使用的分隔符。<br><br>* 所需連續路徑片段的開始層級和結束層級。<br><br>* 拼接這些路徑片段所使用的拼接符。拼接後的路徑片段用於計算權杖。 | |
|SplitSymbol |String |表示拆分請求路徑所使用的分隔符。 |`-` |
|StartLevel |Long |表示起始片段所在的層級。 |`2` |
|TermLevel |Long |表示結束片段所在的層級。<br><br>如果 `TermLevel` 是負整數，表示從最右邊的片段開始向左計數。 |`3` |
|JoinSymbol |String |表示拼接這些路徑片段所使用的拼接符。 |`00` |
|UrlParam |Object |表示從 URL 中獲取所需物件的方式。<br><br>該參數是一個結構體，包含物件的來源以及相關設定。 | |
|CapMode |String |表示物件的來源。該參數有以下取值：<br><br><br>* `name`：表示查詢參數。相關設定在 `ParamName` 和 `ArgSegment` 中指定。<br><br>* `uri`：表示請求路徑中指定的目錄。相關設定在 `UriLevel` 和 `ArgSegment` 中指定。 |`uri` |
|ParamName |String |當 `ParamType` 是 `name` 時，該參數表示指定的查詢參數。 |`myparam3` |
|UriLevel |Long |當 `ParamType` 是 `uri` 時，該參數表示指定的目錄層級。<br><br>如果層級是負整數，表示從最右邊的目錄開始向左計數。 |`2` |
|ArgSegment |Object |表示基於 `ParamName` 或 `UriLevel` 獲取的內容是否需要被拆分，以提取某個層級的片段。該片段才是需要獲取的物件。 | |
|Switch |Boolean |表示獲取到的內容是否需要被拆分。該參數有以下取值：<br><br><br>* `true`：表示內容需要被拆分。<br><br>* `false`：表示內容無需被拆分。 |`true` |
|Level |Long |表示將獲取到的內容拆分為多個層級的片段後，所需物件所在的層級。<br><br>如果層級是負整數，表示從最右邊層級的片段開始向左計數。 |`2` |
|SplitSymbol |String |表示用於拆分內容而使用的分隔符。 |`-` |
|ParamSource |String |對於新增到 Manifest 中的權杖，該參數表示 CDN 在使用該物件計算權杖時，該物件的來源。<br><br>該參數有以下取值：<br><br><br>* `ParentLink`：表示該物件來自使用者請求中的 URL。<br><br>* `ChildLink`：表示該物件來自 Manifest 中影片分片的 URI。 |`ParentLink` |
|RewriteM3U8 |Object |表示 HLS Manifest 改寫的設定，也就是設定如何在 Manifest 中的影片分片 URI 中新增權杖。 | |
|Switch |Boolean |表示是否需要改寫 HLS Manifest。該參數有以下取值：<br><br><br>* `true`：表示需要改寫 Manifest。<br><br>* `false`：表示無需改寫 Manifest。<br><br><br>預設情況下，CDN 僅對 Manifest 中 `EXTINF` 標籤下的影片分片 URI 新增權杖。 |`true` |
|RewriteM3U8Tag |Object |表示額外的標籤。對於 `Tags` 中包含的標籤，CDN 會將權杖新增到這些標籤下的 URL 中。參見 [F 類型](https://docs.byteplus.com/en/docs/byteplus-cdn/typef_zh-tw#m3u8-%E9%A1%8D%E5%A4%96%E6%A8%99%E7%B1%A4%E7%9A%84%E6%94%B9%E5%AF%AB%E7%AF%84%E4%BE%8B)。 | |
|Switch |Boolean |表示是否需要設定额外的標籤。該參數有以下取值：<br><br><br>* `true`：表示需要設定额外的標籤。<br><br>* `false`：表示無需設定额外的標籤。 |`true` |
|Tags |String[] |表示額外標籤的列表。 |`["tag1","tag2","tag3"]` |
|RewriteMPD |Object |表示 DASH Manifest 改寫的設定，也就是設定如何在 Manifest 中的影片分片 URI 中新增權杖。 | |
|Switch |Boolean |表示是否需要改寫 DASH Manifest。該參數有以下取值：<br><br><br>* `true`：表示需要改寫 Manifest。<br><br>* `false`：表示無需改寫 Manifest。 |`true` |
|MpdVarExpand |Boolean |表示是否要將 `SegmentTemplate` 下 URI 中的變數替換為實際值。該參數有以下取值：<br><br><br>* `true`：表示啟用該設定。該設定啟用後，CDN 會先將影片分片 URI 中的變數替換為實際值，然後基於包含實際值的 URI 產生權杖，最後將權杖新增到 URI 中。<br><br>* `false`：表示不啟用該設定。變數名本身會作為固定字串用於產生權杖。<br><br><br>該設定啟用後，目前只有滿足以下所有條件的變數才會被替換為實際值：<br><br><br>* 變數為 `$RepresentationID$`。<br><br>* `SegmentTemplate` 下存在至少一個 URI 符合以下條件：<br><br>   * 在該 URI 中，至少有一個 `$RepresentationID$` 出現的位置不是 URI 路徑中的最後一段。<br><br>* `<SegmentTemplate ... />` 和 `<Representation .../>` 之間不能出現其他內容。<br><br><br>另外，在改寫後的 DASH Manifest 中，原始的 `SegmentTemplate` 會被保留。<br><br>參見 [F 類型](https://docs.byteplus.com/en/docs/byteplus-cdn/typef_zh-tw#dash-mpd-%E8%AE%8A%E6%95%B8%E6%93%B4%E5%B1%95-%E9%85%8D%E7%BD%AE%E7%9A%84%E9%A1%8D%E5%A4%96%E8%AA%AA%E6%98%8E%E5%92%8C%E7%AF%84%E4%BE%8B)。 |`true` |
|CustomRewrite |Object |表示影片 Manifest 的擴充改寫設定。該設定啟用後，CDN 使用 [特殊重寫邏輯](https://docs.byteplus.com/en/docs/byteplus-cdn/typef_zh-tw#%E5%BD%B1%E7%89%87-manifest-%E7%9A%84%E7%89%B9%E6%AE%8A%E9%87%8D%E5%AF%AB%E9%82%8F%E8%BC%AF) 覆蓋 [預設改寫邏輯](https://docs.byteplus.com/en/docs/byteplus-cdn/typef_zh-tw#%E5%BD%B1%E7%89%87-manifest-%E6%AA%94%E6%A1%88%E7%9A%84%E9%A0%90%E8%A8%AD%E6%94%B9%E5%AF%AB%E9%82%8F%E8%BC%AF)。 | |
|Switch |Boolean |表示是否啟用擴充改寫設定。該參數有以下取值：<br><br><br>* `true`：表示啟用擴充改寫設定。<br><br>* `false`：表示不啟用擴充改寫設定。 |`true` |
|RewriteParam |Object[] |表示一個物件列表。CDN 將這些物件拼接而產生權杖，新增到影片分片的 URL 中。 | |
|ParamType |String |表示物件的類型。該參數有以下取值：<br><br><br>* `ParentLinkUrlParam`：表示使用者請求 URL 中的某類物件。物件可以是一個查詢參數或某個層級的路徑目錄。相關設定在 `ParentLinkUrlParam` 結構體中指定。<br><br>* `SupString`：表示一個字串。相關設定在 `SupContent` 中指定。<br><br>* `ParentLinkURI`：表示使用者請求路徑中的連續片段。路徑不包含查詢字串。相關設定在 `ParentLinkUriParamSup` 中指定。<br><br>* `ParentLinkExpire`：表示使用者請求中權杖的時間標記。參見 `ExpireTimeRule` 下 `Duration` 參數的說明。<br><br>* `AuthToken`：表示基於 `AuthTokenCalRule` 計算的權杖。<br><br>* `ParentFullURI`：表示使用者請求的完整路徑，不包含查詢字串。 |`ParentLinkURI` |
|SupContent |String |當 `ParamType` 是 `SupString` 時，該參數表示指定的字串。 |`abc-13343` |
|ParentLinkUriParamSup |Object |表示從使用者請求路徑中獲取物件的方式。<br><br>該參數是一個結構體，包含以下設定：<br><br><br>* 拆分請求路徑所使用的分隔符。<br><br>* 連續路徑片段的開始層級和結束層級。<br><br>* 拼接這些路徑片段所使用的拼接符。拼接後的路徑片段用於產生權杖。 | |
|SplitSymbol |String |表示拆分請求路徑所使用的分隔符，要求與 `JoinSymbol` 相同。 |`-` |
|StartLevel |Long |表示起始片段所在的層級。 |`1` |
|TermLevel |Long |表示結束片段所在的層級，要求如下：<br><br><br>* 只能是非 0 的整數。<br><br>* 絕對值不能大於層級總數。<br><br><br>如果 `TermLevel` 是負整數，表示從最右邊的片段開始向左計數。 |`3` |
|JoinSymbol |String |表示拼接這些路徑片段所使用的拼接符。 |`00` |
|ParentLinkUrlParam |Object |表示從 URL 中獲取物件的方式。<br><br>該參數是一個結構體，包含物件的來源以及相關設定。 | |
|CapMode |String |表示物件的來源。該參數有以下取值：<br><br><br>* `name`：表示查詢參數。相關設定在 `ParamName` 和 `ArgSegment` 中指定。<br><br>* `uri`：表示請求路徑中指定的目錄。相關設定在 `UriLevel` 和 `ArgSegment` 中指定。 |`name` |
|ParamName |String |當 `CapMode` 是 `name` 時，該參數表示指定的查詢參數。 |`myparam5` |
|UriLevel |Long |當 `CapMode` 是 `uri` 時，該參數表示指定的目錄層級。<br><br>如果層級是負整數，表示從最右邊的目錄開始向左計數。 |`4` |
|ArgSegment |Object |表示基於 `ParamName` 或 `UriLevel` 獲取的內容是否需要被拆分，以提取某個層級的片段。該片段才是需要獲取的物件。 | |
|Switch |Boolean |表示獲取的內容是否需要被拆分。該參數有以下取值：<br><br><br>* `true`：表示內容需要被拆分。<br><br>* `false`：表示內容無需被拆分。 |`true` |
|Level |Long |表示將獲取的內容拆分為多個層級的片段後，需要的片段所在的層級。<br><br>如果層級是負整數，表示從最右邊的片段開始向左計數。 |`2` |
|SplitSymbol |String |表示用於拆分內容的分隔符。 |`-` |
|RewriteRule |Object |表示 CDN 在影片分片 URI 中新增權杖的方式。 | |
|CapMode |String |表示 CDN 如何在影片分片 URI 中新增產生的權杖。該參數有以下取值：<br><br><br>* `name`：表示將 URI 中指定的查詢參數設定為權杖。相關設定在 `ParamName` 中指定。<br><br>* `uri`：表示在 URI 中指定的目錄層級插入一個目錄，並將該目錄設定為權杖。相關設定在 `UriLevel` 中指定。 |`name` |
|ParamName |String |當 `CapMode` 是 `name` 時，表示指定的查詢參數。 |`myparam4` |
|UriLevel |Long |當 `CapMode` 是 `uri` 時，表示指定的目錄層級。<br><br>如果層級是負整數，表示從最右邊層級的目錄開始向左計數。 |`2` |
|SignJoinSymbol |String |表示拼接 `RewriteParam` 中各物件而使用的拼接符。 |`00` |
|ArgumentRule |Object |表示來源伺服器請求參數相關的設定。 | |
|KeepOriginArg |Boolean |表示是否在來源伺服器請求中包含基於 `AuthTokenCalRule` 計算的權杖。該參數有以下取值：<br><br><br>* `true`：表示在來源伺服器請求中包含權杖。來源伺服器請求中權杖出現的位置與 `SignCapRule` 中的設定相同。<br><br>* `false`：表示不在來源伺服器請求中包含權杖。 |`true` |
|GeneralParamRule |Object |表示 CDN 設定影片分片 URI 中查詢參數的方式。 | |
|ParentLinkParamInherit |String |表示改寫後的影片分片 URI 是否包含使用者請求 URL 中除表示權杖和權杖時間標記的參數之外的所有查詢參數。該參數有以下取值：<br><br><br>* `not_inherit`：表示改寫後的分片 URI 不會包含這些查詢參數。<br><br>* `inherit`：表示改寫後的分片 URI 會包含這些查詢參數。 |`not_inherit` |
|SubLinkParamRule |Object |該結構體包含額外的查詢參數設定。該結構體包含額外的查詢參數設定。 | |
|InheritMode |String |表示當影片分片 URI 和使用者請求 URL 中存在相同的查詢參數時，CDN 如何設定影片分片 URI 中該參數的值。<br><br>該參數有以下取值：<br><br><br>* `sub_link_first`：表示使用影片分片 URI 中該參數的值。<br><br>* `inherit_first`：表示使用使用者請求 URL 中該參數的值。 |`inherit_first` |
|KeepSubLinkArg |String |表示改寫後的影片分片 URI 是否保留 URI 中原有的查詢參數。該參數有以下取值：<br><br><br>* `delete`：表示改寫後的分片 URI 不會保留這些查詢參數。<br><br>* `keep`：表示改寫後的分片 URI 會保留這些查詢參數。 |`delete` |
|RewriteFormat |String |表示改寫後的影片分片 URI 格式。該參數有以下取值：<br><br><br>* `default`：該參數值的含義與 `absolute` 相同。<br><br>* `relative`：保持 URI 的目前格式。<br><br>* `absolute`：如果 URI 的格式是相對路徑，CDN 將格式轉換成絕對路徑。如果 URI 是絕對路徑或完整 URL，則保持目前格式。<br><br>* `full`：如果 URI 的格式是絕對路徑或相對路徑，CDN 將格式轉換成完整 URL。 |`default` |
|Timeout |Object |表示 "來源伺服器請求逾時" 特性的設定。 | |
|Switch |Boolean |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示停用該特性。此時，TCP 請求和 HTTP 請求的逾時時間使用預設值，分別是 2 秒和 60 秒。 |`true` |
|TimeoutRules |Object[] |表示一組逾時時間的設定。 | |
|TimeoutAction |Object |表示超时时间的配置。 | |
|HttpTimeout |Long |表示 HTTP 请求的超时时间。 |`60` |
|TcpTimeout |Long |表示 TCP 请求的超时时间。 |`2` |
|UaAccessRule |Object |表示 "UA 黑白名单" 特性的配置。 | |
|AllowEmpty |Boolean |表示當使用者請求不包含 User\-Agent 標頭時，CDN 處理請求的方式。該參數有以下取值：<br><br><br>* `true`：表示如果請求不包含 User\-Agent 標頭，則該請求被認為比對設定的 User\-Agent 列表。<br><br>* `false`：表示如果請求不包含 User\-Agent 標頭，則該請求被認為不比對設定的 User\-Agent 列表。 |`true` |
|IgnoreCase |Boolean |表示 UA 字符串是否是大小写敏感的。该参数有以下取值：<br><br><br>* `true`: 表示 UA 字符串是大小写不敏感的。<br><br>* `false`: 表示 UA 字符串是大小写敏感的。 |`true` |
|RuleType |String |表示 UA 名单的类型。当 `Switch` 是 `true` 时，该参数为必填。该参数有以下取值：<br><br><br>* `allow`：表示白名单。<br><br>* `deny`：表示黑名单。 |`deny` |
|Switch |Boolean |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|UserAgent |String[] |表示一个 UA 的列表。该参数的说明如下：<br><br><br>* 如果 `RuleType` 是 `allow`，表示仅允许包含列表中的 UA 的请求访问域名。<br><br>* 如果 `RuleType` 是 `deny`，表示如果访问请求包含列表中的 UA，则不允许访问域名。<br><br><br>UA 中的 `*` 表示一个或者多个字符。 |`["*curl*","*Mozilla*"]` |
|VideoDrag |Object |表示 "视频拖拽" 特性的配置。 | |
|Switch |Boolean |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|OriginIPv6 |String |表示 "IPv6 回源" 的配置。该参数有以下取值：<br><br><br>* `ipv6_first`：表示 CDN 始终尝试获取源站域名的 IPv6 地址。如果无法获取该 IP 地址，CDN 才尝试获取源站域名的 IPv4 地址。<br><br>* `ipv4_first`：表示 CDN 始终尝试获取源站域名的 IPv4 地址。如果无法获取该 IP 地址，CDN 才尝试获取源站域名的 IPv6 地址。<br><br>* `followclient`：表示 CDN 尝试获取与用户请求相同类型的 IP 地址。<br><br><br>由于海外部分 CDN 回源节点不支持向 IPv6 地址发送回源请求，该功能仅适用于位于中国内地的回源节点。 |`followclient` |
|UrlNormalize |Object |表示 "URL 标准化" 特性的配置。 | |
|NormalizeObject |String[] |表示一个 URL 标准化选项列表。当 `Switch` 为 `true` 时，该参数为必填。列表中可以包含以下选项：<br><br><br>* `dot_segments`：表示将请求 URL 中的以下内容进行替换：<br><br>   * `/./`：替换为单个斜杠（/）。<br><br>   * `/../`：如果 `/../` 前还有一个级别的目录，则删除 `/../` 与该目录。如果 `/../` 前没有目录，则保留原 URL。<br><br>* `back_slashes`：表示将请求 URL 中的反斜杠（\）替换为单个斜杠（/）。<br><br>* `successive_slashes`：表示将请求 URL 中连续斜杠（//）替换为单个斜杠（/）。 |`["dot_segments","back_slashes","successive_slashes"]` |
|Switch |Boolean |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|RequestBlockRule |Object |表示 "自定义拦截" 特性的配置。 | |
|BlockRule |Object[] |表示一个规则列表。列表中第一条规则的优先级最高。<br><br>当收到一个用户请求时，CDN 按规则的优先级，从高到低将规则与请求匹配。如果一条规则匹配了请求，CDN 就停止处理其余规则。 | |
|BlockAction |Object |表示一条规则中 CDN 行为的配置。 | |
|Action |String |表示 CDN 如何处理匹配 `Condition` 的请求。该参数有以下取值：<br><br><br>* `refuse`：表示 CDN 拒绝请求并响应一个 4xx 的错误码。错误码在 `StatusCode` 中指定。<br><br>* `redirect`：表示 CDN 将请求重定向到 `RedirectUrl` 中指定的 URL。 |`refuse` |
|StatusCode |String |表示对于匹配 `Condition` 的用户请求，CDN 的响应状态码。<br><br><br>* 当 `Action` 是 `refuse` 时，该参数表示一个 400\-499 范围内的错误码。<br><br>* 当 `Action` 是 `redirect` 时，该参数有以下取值：<br><br>   * `301`：表示响应状态码是 301。<br><br>   * `302`：表示响应状态码是 302。 |`403` |
|ErrorPage |String |* 当 `Action` 是 `refuse` 时，该参数是可选的，说明如下：<br><br>   * 如果指定该参数，该参数表示 "全局配置" 特性中的一个自定义响应页面的名称。也就是说，当 CDN 拒绝请求时，返回该自定义页面。<br><br>   * 如果不指定该参数，表示 CDN 使用 `StatusCode` 中指定错误码的标准响应正文。 |`GlobalConfigName` |
|RedirectUrl |String |* 当 `Action` 是 `redirect` 时，表示重定向 URL。<br><br>* 当 `Action` 是 `refuse` 时，该参数无效。 |`http://www.example.com` |
|Condition |Object |表示该规则中匹配条件的定义。 | |
|ConditionRule |Object[] |表示一个匹配条件列表，用于匹配请求 URL 中的路径和查询参数、以及请求来自的客户端 IP 地址。每个匹配条件包含匹配类型、对比类型和匹配值。 | |
|Object |String |表示一个匹配类型。<br><br><br>* 当 `Type` 是 `url` 时，该参数有以下取值：<br><br>   * `path`：表示表示请求 URL 中的路径。<br><br>   * `directory`：表示路径中的一个目录。<br><br>   * `filetype`：表示路径末尾的扩展名。<br><br>   * `regex`：表示请求 URL 中的路径，通过正则表达式匹配。<br><br>* 当 `Type` 是 `querystring` 时，该参数有以下取值：<br><br>   * `query_name`：表示请求 URL 中的一个查询参数。<br><br>   * `full_querystring`：表示请求 URL 中的查询字符串。<br><br>* 当 `Type` 是 `client_ip` 时，该参数有以下取值：<br><br>   * `client_ip`：表示客户端的 IP 地址。<br><br>* 当 `Type` 是 `request_header` 时，该参数有以下取值：<br><br>   * `ua`：表示请求中 User\-Agent 头部。<br><br>   * `customize`：表示请求中的自定义头部。 |`filetype` |
|Operator |String |表示一个对比类型。<br><br><br>* 当 `Object` 是 `path`、`directory`、`filetype` 时，该参数有以下取值：<br><br>   * `equal`：表示如果匹配 `Value` 中的任何值，该请求就满足这个匹配条件。<br><br>   * `not_equal`：表示如果不匹配 `Value` 中的所有值，该请求才满足这个匹配条件。<br><br>* 当 `Object` 是 `query_name` 时，该参数有以下取值：<br><br>   * `exist`：表示存在。匹配逻辑与 `equal` 相同。<br><br>   * `not_exist`：表示不存在。匹配逻辑与 `not_equal` 相同。<br><br>   * `belong_shared_config`：表示如果匹配 `Value` 表示的全局配置中所包含的任何值，该请求就满足这个匹配条件。<br><br>   * `not_belong_shared_config`：表示如果不匹配 `Value` 表示的全局配置中的所有值，该请求才满足这个匹配条件。<br><br>   * `empty`：表示值为空。<br><br>   * `not_empty`：表示值不为空。<br><br>   * `equal`：参见以上描述。<br><br>   * `not_equal`：参见以上描述。<br><br>* 当 `Object` 是 `regex`、`full_querystring`、`client_ip` 或 `ua` 时，该参数有以下取值：<br><br>   * `match`：描述与 `equal` 相同。<br><br>   * `not_match`：描述与 `not_equal` 相同。<br><br>* 当 `Object` 是 `ua` 或 `customize` 时，该参数还有以下**额外**取值：<br><br>   * `empty`：参见以上描述。<br><br>   * `not_empty`：参见以上描述。 |`not_equal` |
|Type |String |表示一个匹配对象的类型。该参数有以下取值：<br><br><br>* `url`：表示请求 URL。<br><br>* `querystring`：表示请求 URL 中的查询字符串。<br><br>* `request_header`：表示请求中的头部。 |`url` |
|Value |String |表示一个或者多个匹配值。<br><br><br>* 如果 `Type` 是 `request_header`，多个匹配值之间使用竖线（\|）分隔。<br><br>* 如果 `Type` 不是 `request_header`，多个匹配值之间使用分号（;）分隔。 |`png;txt` |
|Name |String |当 `Object` 是 `query_name` 或者 `customize` 时，该参数有效。<br><br><br>* 如果 `Object` 是 `query_name`，该参数表示一个查询参数的名称。<br><br>* 如果 `Object` 是 `customize`，该参数表示一个自定义请求头的名称。 |`color` |
|Connective |String |表示多条 `ConditionRule` 之间的关系。该参数有以下取值：<br><br><br>* `AND`：表示 "和"。<br><br>* `OR`：表示 "或"。 |`AND` |
|RuleName |String |表示规则的名称。 |`MyRule` |
|Switch |Boolean |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|OriginCertCheck |Object |表示 "源站证书校验" 特性的配置。<br><br>该特性启用后，CDN 会校验源站证书的合法性，包括证书是否已被吊销、证书是否由可信 CA 签发、证书与源站域名是否匹配等。CDN 内置了常见可信 CA 的根证书。如果源站证书未通过校验，CDN 进行 [來源伺服器請求重試](https://docs.byteplus.com/en/docs/byteplus-cdn/origin-fetch-retry_zh-tw)。如果回源重试时源站证书依然未通过校验，CDN 判定无法从该源站获取文件，并对用户请求响应 504 状态码。 | |
|Switch |Boolean |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|CertInfoList |Object[] |表示一个 CA 证书列表，列表中的 CA 证书托管在 CDN。CDN 使用该列表中的 CA 证书对来自源站的服务器证书进行校验。 | |
|CertId |String |表示列表中一本 CA 证书的 ID，以 `cert_hosting` 开头。 |`cert_hosting-104663` |
|ConditionalOrigin |Object |表示 "條件源站" 特性的設定。 | |
|OriginRules |Object[] |表示一個規則清單。清單中的每條規則中定義了一組符合條件以及 CDN 對滿足符合條件的請求所執行的操作。<br><br>當收到一個使用者請求時，CDN 按規則的優先順序，從高到低將規則與請求比對。如果一條規則符合了請求，CDN 就停止處理其餘規則。 | |
|Actions |Object |表示一條規則中定義的操作設定。 | |
|OriginLines |Object[] |表示一個源站清單。 | |
|Address |String |表示一個源站的位址。<br><br><br>* 當 `InstanceType` 是 `ip` 時，`Address` 表示一個 IPv4 或者 IPv6 位址。<br><br>* 當 `InstanceType` 是 `domain` 時，`Address` 表示一個網域名稱。<br><br>* 當 `InstanceType` 是 `storage` 時，`Address` 表示儲存桶網域名稱，可以是雲端廠商分配的桶網域名稱，也可以是您在雲端廠商處為儲存桶設定的自訂網域名稱。 |`203.0.113.8` |
|HttpPort |String |表示 CDN 使用 HTTP 協定存取該源站時所使用的連接埠。 |`80` |
|HttpsPort |String |表示 CDN 使用 HTTPS 協定存取该源站时所使用的端口。 |`443` |
|InstanceType |String |表示源站的類型。該參數有以下取值：<br><br><br>* `ip`：表示 IP 位址。<br><br>* `domain`：表示網域名稱。<br><br>* `storage`：表示物件儲存桶。 |`ip` |
|OriginHost |String |表示回源請求存取的站點網域名稱，適用於源站伺服器上有多個站點的情況。<br><br>該參數的優先順序高於全域 `OriginHost` 參數。 |`img.example.com` |
|BucketSource |String |表示儲存桶使用的是哪個物件儲存服務所提供的鑑權方式。該參數有以下取值：<br><br><br>* `tos`：表示 BytePlus TOS。<br><br>* `cos`：表示騰訊雲 COS。<br><br>* `oss`：表示阿里雲 OSS。<br><br>* `aws_common`：表示 AWS S3 或者其他使用相容 S3 鑑權方式的第三方物件儲存服務。 |`aws_common` |
|PrivateBucketAccess |Boolean |表示儲存桶是否是私有桶。該參數僅當 `InstanceType` 為 `storage` 時有效。該參數有以下取值：<br><br><br>* `true`：表示該儲存桶是私有桶。<br><br>* `false`：表示該儲存桶不是私有桶。 |`true` |
|TosAuthInformation |Object |表示儲存桶的存取憑證。當以下任意條件滿足时，该参数有效。<br><br><br>* `InstanceType` 不是 `storage`。<br><br>* 儲存桶屬於另一個主帳號下的 TOS 服務。 | |
|AccessKeyId |String |表示存取憑證中的 AccessKey ID，在騰訊雲稱為 SecretId。 |`xxxxxxxxxxxxxxx` |
|AccessKeySecret |String |表示存取憑證中的 AccessKey Secret，在騰訊雲稱為 SecretKey。 |`xxxxxx` |
|Region |String |表示儲存桶所在地域的資訊，也就是儲存桶的 region code。Region code 參與簽名的計算。 |`us-east-1` |
|AccountName |String |账户名，azure专用 | |
|OriginType |String |源站类型，主源还是备源 | |
|Weight |String |权重，【1\-100校验】 | |
|Condition |Object |表示該規則中符合條件的設定。 | |
|ConditionGroups |Object[] |表示一個符合條件清單。 | |
|Condition |Object |表示一個符合条件的設定。 | |
|Object |String |表示一个匹配对象。该参数有以下取值：<br><br><br>* `path`：表示请求 URL 中的完整路径。<br><br>* `directory`：表示请求 URL 中的某个目录。<br><br>* `filetype`：表示请求 URL 中的扩展名。<br><br>* `full_querystring`：表示请求 URL 中的所有查询参数。<br><br>* `client_ip`：表示客户端的 IP 地址。<br><br>* `query_name`：表示请求 URL 中的而某个查询参数。<br><br>* `customize`：表示用户请求中的某个头部。 |`path` |
|Operator |String |表示符合類型。 |`equal` |
|Value |String[] |表示一個或者多個符合值。 |`/www/img/my*image.png;/doc` |
|Name |String |* 当 `Object` 为 `query_name` 时，该参数表示指定的查询参数的名称。<br><br>* 当 `Object` 为 `customize` 时，该参数表示指定的请求头的名称。<br><br>* 当 `Object` 为其他值时，该参数无效。 |`param` |
|Type |String |* 当 `Object` 为 `query_name` 时，该参数值必须是 `querystring`。<br><br>* 当 `Object` 为 `customize` 时，该参数值必须是 `request_header`。<br><br>* 当 `Object` 为其他值时，该参数无效。 |`querystring` |
|Connective |String |表示这些匹配条件之间的关系。该参数有以下取值：<br><br><br>* `or`：表示关系是 "或"。<br><br>* `and`：表示关系是 "与"。 |`and` |
|IsGroup |Boolean |该参数值是 `true`。 |`true` |
|Switch |Boolean |表示该特性是否已启用。该参数有以下取值：<br><br><br>* `true`：表示该特性已启用。<br><br>* `false`：表示该特性未启用。 |`true` |
|Websocket |Object |表示 Websocket 設定。 | |
|Switch |Boolean |表示是否為使用者請求啟用 WebSocket 支援。該參數有以下取值：<br><br><br>* `true`：表示啟用 WebSocket。該設定啟用後，CDN 可以回應來自用戶端的 Websocket 請求。<br><br>* `false`：表示停用 WebSocket。 |`true` |
|Timeout |Long |表示 Websocket 連線的逾時時間，單位是秒。 |`60` |
|MultiRange |Object |表示 "多重範圍（Multi\-range)" 特性的設定。 | |
|Switch |Boolean |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。該特性啟用後，CDN 允許指定了多重範圍的 Range 請求。<br><br>* `false`：表示不啟用該特性。如果收到一個指定了多重範圍的 Range 請求，CDN 會拒絕該請求並傳回 416 回應狀態碼。 |`true` |
|OfflineCache |Object |表示 "離線快取" 特性的設定。 | |
|Object |String |表示該特性的觸發條件，該參數有以下取值：<br><br><br>* `request_error`：表示來源伺服器請求異常。當來源伺服器請求出現異常時，CDN 沒有獲得來源伺服器的回應。<br><br>* `error_code`：表示來源伺服器回應狀態碼是 5xx。<br><br>* `request_error,error_code`：表示以上兩個條件都包含。 |`request_error,error_code` |
|StatusCode |String |表示一個或多個回應狀態碼，範圍是 500\-599。多個狀態碼之間使用分號（;）分隔。`5xx` 表示任意以數字 5 開頭的狀態碼。<br><br>當 `Object` 是 `error_code` 或 `request_error,error_code` 時，該參數才有效。 |`504;505` |
|Switch |Boolean |表示是否啟用該特性。該參數有以下取值：<br><br><br>* `true`：表示啟用該特性。<br><br>* `false`：表示停用該特性。 |`true` |
|Cname |String |表示 CDN 為該網域名稱分配的 CNAME。 |`www.example.com.volcgslb.com` |
|CreateTime |Long |表示該網域名稱的建立時間，格式是 Unix 時間標記。 |`1636612244` |
|Project |String |表示該網域名稱歸屬的專案。 |`default` |
|Status |String |表示該網域名稱的狀態。該參數有以下取值：<br><br><br>* `online`：表示狀態是 正常執行。<br><br>* `configuring`：表示狀態是 設定中。<br><br>* `offline`：表示狀態是 已下線。 |`offline` |
|UpdateTime |Long |表示該網域名稱設定的最近更新時間，格式是 Unix 時間標記。如果該網域名稱設定在建立後未被更新，該參數值與 `CreateTime` 的值相同。 |`1639621409` |
|ResourceTags |Object[] |表示該網域名稱的標籤。 | |
|Key |String |表示一個標籤的 Key。 |`Key1` |
|Value |String |表示該標籤的 Value。 |`Value1` |
|ProxyProtocol |Object |透传ProxyProtocol | |
|Switch |Boolean |无 | |
|Range |Object |表示 Range GET 請求中分片大小的設定。 | |
|RangeSize |Long |表示分段的大小。 |`512` |
|Switch |Boolean |表示該設定是否已啟用。該參數有以下取值：<br><br><br>* `true` ：表示該設定已啟用。<br><br>* `false` ：表示該設定已禁用。 |`true` |
|Unit |String |表示 `RangeSize` 的單位。該參數有以下取值：<br><br><br>* `KB`<br><br>* `MB` |`KB` |
|ServerSentEvent |Object |表示 SSE 的设置。 | |
|Switch |Boolean |表示是否启用了该设置。该参数有以下取值：<br><br><br>* `true`：表示该设置已启用。<br><br>* `false`：表示该设置已禁用。 |`true` |
|CustomLogField |Object |客户自定义日志94字段 | |
|CustomLogFieldRule |Object[] |CustomLogFieldRule 表示自定义94日志字段配置规则，最多支持50条。 | |
|LogFieldKey |String |LogFieldKey 表示日志字段名称。 \- 支持字母、数字、下划线、连字符、点号 \- 长度不超过32个字符 | |
|LogFieldSource |String |LogFieldSource 表示日志字段值采集来源。有如下取值： \- request_header：请求头部 \- response_header：响应头部 \- customize：自定义输入 | |
|LogFieldValue |String |LogFieldValue 表示日志字段值采集。 如果LogFieldSource = request_header、response_header，Value表示从哪个头部取值，输入限制如下： \- 支持字母、数字、下划线、连字符、点号 \- 长度不超过64个字符 如果LogFieldSource = customize，Value表示自定义输入内容，输入限制如下： \- 长度不超过256个字符 | |
|Switch |Boolean |Switch 表示是否启用该特性。该参数有以下取值： \- true：表示启用该特性，需要指定CustomLogFieldRule \- false：表示禁用该特性，不需要指定CustomLogFieldRule，若指定则报错。 该参数的默认值是false。 | |


<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=DescribeCdnConfig&Version=2021-03-01
{
    "Domain": "test111.example.com"
}
```


<span id="範例回應"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "202508160551554488555F346DC5A960D4",
        "Action": "DescribeCdnConfig",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DomainConfig": {
            "AreaAccessRule": {
                "Area": [
                    "CHN",
                    "HKG",
                    "MAC",
                    "TWN",
                    "CHE"
                ],
                "RuleType": "allow",
                "Switch": true
            },
            "ProxyProtocol": {
                "Switch": true
            },
            "BrowserCache": [
                {
                    "CacheAction": {
                        "Action": "cache",
                        "DefaultPolicy": "cache",
                        "IgnoreCase": true,
                        "Ttl": 216000
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "filetype",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "jpg;png"
                            }
                        ],
                        "Connective": "OR"
                    }
                },
                {
                    "CacheAction": {
                        "Action": "cache",
                        "DefaultPolicy": "origin_first",
                        "IgnoreCase": false,
                        "Ttl": 0
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "directory",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/foods/;/dogs/ragdolls/"
                            }
                        ],
                        "Connective": "OR"
                    }
                },
                {
                    "CacheAction": {
                        "Action": "cache",
                        "DefaultPolicy": "no_cache",
                        "IgnoreCase": false,
                        "Ttl": 0
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "path",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/file1;/docs/file2"
                            }
                        ],
                        "Connective": "OR"
                    }
                },
                {
                    "CacheAction": {
                        "Action": "cache",
                        "DefaultPolicy": "cache",
                        "IgnoreCase": false,
                        "Ttl": 3000
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "regex",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "^/a{1,2}(.*)g$"
                            }
                        ],
                        "Connective": "OR"
                    }
                }
            ],
            "Cache": [
                {
                    "CacheAction": {
                        "Action": "cache",
                        "DefaultPolicy": "default",
                        "IgnoreCase": true,
                        "Ttl": 50
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "filetype",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "jpg;png"
                            }
                        ],
                        "Connective": "OR"
                    }
                },
                {
                    "CacheAction": {
                        "Action": "cache",
                        "DefaultPolicy": "force_cache",
                        "IgnoreCase": false,
                        "Ttl": 80
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "directory",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/foods/;/dogs/ragdolls/"
                            }
                        ],
                        "Connective": "OR"
                    }
                },
                {
                    "CacheAction": {
                        "Action": "cache",
                        "DefaultPolicy": "origin_first",
                        "IgnoreCase": false,
                        "Ttl": 40
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "path",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/file1;/docs/file2"
                            }
                        ],
                        "Connective": "OR"
                    }
                },
                {
                    "CacheAction": {
                        "Action": "cache",
                        "DefaultPolicy": "origin_first_Replenish",
                        "IgnoreCase": false,
                        "Ttl": 0
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "regex",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "^/a{1,2}(.*)g$"
                            }
                        ],
                        "Connective": "OR"
                    }
                }
            ],
            "CacheKey": [
                {
                    "CacheKeyAction": {
                        "CacheKeyComponents": [
                            {
                                "Action": "include",
                                "IgnoreCase": false,
                                "Object": "queryString",
                                "Subobject": "*"
                            }
                        ]
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "filetype",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "jpg;png",
                                "IgnoreCase": true
                            }
                        ],
                        "Connective": "OR"
                    }
                },
                {
                    "CacheKeyAction": {
                        "CacheKeyComponents": [
                            {
                                "Action": "exclude",
                                "IgnoreCase": false,
                                "Object": "queryString",
                                "Subobject": "*"
                            }
                        ]
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "directory",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/foods/;/dogs/ragdolls/"
                            }
                        ],
                        "Connective": "OR"
                    }
                },
                {
                    "CacheKeyAction": {
                        "CacheKeyComponents": [
                            {
                                "Action": "includePart",
                                "IgnoreCase": true,
                                "Object": "queryString",
                                "Subobject": "param1;param2"
                            }
                        ]
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "path",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/file1;/docs/file2"
                            }
                        ],
                        "Connective": "OR"
                    }
                },
                {
                    "CacheKeyAction": {
                        "CacheKeyComponents": [
                            {
                                "Action": "excludePart",
                                "IgnoreCase": false,
                                "Object": "queryString",
                                "Subobject": "param3;param4"
                            }
                        ]
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "regex",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "^/a{1,2}(.*)g$"
                            }
                        ],
                        "Connective": "OR"
                    }
                },
                {
                    "CacheKeyAction": {
                        "CacheKeyComponents": [
                            {
                                "Action": "include",
                                "IgnoreCase": true,
                                "Object": "queryString",
                                "Subobject": "*"
                            }
                        ]
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "directory",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/"
                            }
                        ],
                        "Connective": "OR"
                    }
                }
            ],
            "Cname": "test111.example.com.bplslb.com",
            "Compression": {
                "CompressionRules": [
                    {
                        "CompressionAction": {
                            "CompressionFormat": "all",
                            "CompressionTarget": "*",
                            "CompressionType": [
                                "gzip",
                                "br"
                            ],
                            "MinFileSizeKB": 10240
                        },
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "filetype",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "jpg;png"
                                }
                            ],
                            "Connective": "OR"
                        }
                    },
                    {
                        "CompressionAction": {
                            "CompressionFormat": "all",
                            "CompressionTarget": "*",
                            "CompressionType": [
                                "gzip"
                            ],
                            "MinFileSizeKB": 10000
                        },
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "directory",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "/docs/foods/;/dogs/ragdolls/"
                                }
                            ],
                            "Connective": "OR"
                        }
                    },
                    {
                        "CompressionAction": {
                            "CompressionFormat": "all",
                            "CompressionTarget": "*",
                            "CompressionType": [
                                "br"
                            ],
                            "MinFileSizeKB": 12345
                        },
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "path",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "/docs/file1;/docs/file2"
                                }
                            ],
                            "Connective": "OR"
                        }
                    }
                ],
                "Switch": true
            },
            "ConditionalOrigin": {
                "OriginRules": [
                    {
                        "Actions": {
                            "OriginLines": [
                                {
                                    "Address": "203.0.113.6",
                                    "HttpPort": "80",
                                    "HttpsPort": "443",
                                    "InstanceType": "ip",
                                    "OriginHost": ""
                                }
                            ]
                        },
                        "Condition": {
                            "ConditionGroups": [
                                {
                                    "Condition": {
                                        "Name": "myparam",
                                        "Object": "query_name",
                                        "Operator": "equal",
                                        "Type": "querystring",
                                        "Value": [
                                            "myvalue"
                                        ]
                                    },
                                    "IsGroup": false
                                }
                            ],
                            "Connective": "and",
                            "IsGroup": true
                        }
                    },
                    {
                        "Actions": {
                            "OriginLines": [
                                {
                                    "Address": "mybucket.s3-ap-southeast-1.amazonaws.com",
                                    "BucketSource": "aws_common",
                                    "HttpPort": "",
                                    "HttpsPort": "",
                                    "InstanceType": "storage",
                                    "OriginHost": "",
                                    "PrivateBucketAccess": true,
                                    "TosAuthInformation": {
                                        "AccessKeyId": "xxxxxxxxxxxxx",
                                        "AccessKeySecret": "xxxxx",
                                        "Region": "ap-southeast-1"
                                    }
                                }
                            ]
                        },
                        "Condition": {
                            "ConditionGroups": [
                                {
                                    "Condition": {
                                        "Name": "myheader",
                                        "Object": "customize",
                                        "Operator": "match",
                                        "Type": "request_header",
                                        "Value": [
                                            "myvalue"
                                        ]
                                    },
                                    "IsGroup": false
                                }
                            ],
                            "Connective": "and",
                            "IsGroup": true
                        }
                    },
                    {
                        "Actions": {
                            "OriginLines": [
                                {
                                    "Address": "mybucket.cos.ap-singapore.myqcloud.com",
                                    "BucketSource": "cos",
                                    "HttpPort": "",
                                    "HttpsPort": "",
                                    "InstanceType": "storage",
                                    "OriginHost": "",
                                    "PrivateBucketAccess": true,
                                    "TosAuthInformation": {
                                        "AccessKeyId": "xxxxxxxxxxxxx",
                                        "AccessKeySecret": "xxxxx"
                                    }
                                }
                            ]
                        },
                        "Condition": {
                            "ConditionGroups": [
                                {
                                    "Condition": {
                                        "Object": "client_ip",
                                        "Operator": "belong",
                                        "Value": [
                                            "HKG",
                                            "CHE"
                                        ]
                                    },
                                    "IsGroup": false
                                }
                            ],
                            "Connective": "and",
                            "IsGroup": true
                        }
                    },
                    {
                        "Actions": {
                            "OriginLines": [
                                {
                                    "Address": "banana-health.tos-ap-southeast-1.bytepluses.com",
                                    "BucketSource": "tos",
                                    "HttpPort": "",
                                    "HttpsPort": "",
                                    "InstanceType": "storage",
                                    "OriginHost": "banana-health.tos-ap-southeast-1.bytepluses.com",
                                    "PrivateBucketAccess": true
                                }
                            ]
                        },
                        "Condition": {
                            "ConditionGroups": [
                                {
                                    "Condition": {
                                        "Object": "filetype",
                                        "Operator": "equal",
                                        "Value": [
                                            "png"
                                        ]
                                    },
                                    "IsGroup": false
                                }
                            ],
                            "Connective": "and",
                            "IsGroup": true
                        }
                    },
                    {
                        "Actions": {
                            "OriginLines": [
                                {
                                    "Address": "www.example.com",
                                    "HttpPort": "80",
                                    "HttpsPort": "443",
                                    "InstanceType": "domain",
                                    "OriginHost": "non-img.example.com"
                                }
                            ]
                        },
                        "Condition": {
                            "ConditionGroups": [
                                {
                                    "Condition": {
                                        "Object": "directory",
                                        "Operator": "not_equal",
                                        "Value": [
                                            "/img/"
                                        ]
                                    },
                                    "IsGroup": false
                                }
                            ],
                            "Connective": "and",
                            "IsGroup": true
                        }
                    },
                    {
                        "Actions": {
                            "OriginLines": [
                                {
                                    "Address": "198.51.100.5",
                                    "HttpPort": "80",
                                    "HttpsPort": "443",
                                    "InstanceType": "ip",
                                    "OriginHost": "img.example.com"
                                }
                            ]
                        },
                        "Condition": {
                            "ConditionGroups": [
                                {
                                    "Condition": {
                                        "Object": "full_querystring",
                                        "Operator": "regex_match",
                                        "Value": [
                                            "^/a{1,2}.*g$"
                                        ]
                                    },
                                    "IsGroup": false
                                }
                            ],
                            "Connective": "and",
                            "IsGroup": true
                        }
                    },
                    {
                        "Actions": {
                            "OriginLines": [
                                {
                                    "Address": "mybucket.oss-ap-southeast-1.aliyuncs.com",
                                    "BucketSource": "oss",
                                    "HttpPort": "",
                                    "HttpsPort": "",
                                    "InstanceType": "storage",
                                    "OriginHost": "",
                                    "PrivateBucketAccess": true,
                                    "TosAuthInformation": {
                                        "AccessKeyId": "xxxxxxxxxxxxx",
                                        "AccessKeySecret": "xxxxx"
                                    }
                                }
                            ]
                        },
                        "Condition": {
                            "ConditionGroups": [
                                {
                                    "Condition": {
                                        "Object": "path",
                                        "Operator": "equal",
                                        "Value": [
                                            "/docs/file1",
                                            "/docs/file2/"
                                        ]
                                    },
                                    "IsGroup": false
                                },
                                {
                                    "Condition": {
                                        "Object": "path",
                                        "Operator": "equal",
                                        "Value": [
                                            "/docs/file3",
                                            "/docs/file4/"
                                        ]
                                    },
                                    "IsGroup": false
                                }
                            ],
                            "Connective": "or",
                            "IsGroup": true
                        }
                    }
                ],
                "Switch": true
            },
            "CreateTime": 1755314680,
            "CustomErrorPage": {
                "ErrorPageRule": [
                    {
                        "ErrorPageAction": {
                            "Action": "redirect",
                            "RedirectCode": "301",
                            "RedirectUrl": "http://www.example.com/newpage1",
                            "StatusCode": "405"
                        }
                    },
                    {
                        "ErrorPageAction": {
                            "Action": "redirect",
                            "RedirectCode": "307",
                            "RedirectUrl": "http://www.example.com/newpage2",
                            "StatusCode": "504"
                        }
                    }
                ],
                "Switch": true
            },
            "Domain": "test111.example.com",
            "DownloadSpeedLimit": {
                "DownloadSpeedLimitRules": [
                    {
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "unlimited",
                                    "Operator": "match",
                                    "Type": "url"
                                }
                            ],
                            "Connective": "OR"
                        },
                        "DownloadSpeedLimitAction": {
                            "SpeedLimitRate": 100,
                            "SpeedLimitRateAfter": 50,
                            "SpeedLimitTime": {
                                "BeginTime": "01:00",
                                "DayWeek": "unlimited",
                                "EndTime": "02:00"
                            }
                        }
                    },
                    {
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "filetype",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "jpg;png"
                                }
                            ],
                            "Connective": "OR"
                        },
                        "DownloadSpeedLimitAction": {
                            "SpeedLimitRate": 200,
                            "SpeedLimitRateAfter": 90,
                            "SpeedLimitTime": {
                                "BeginTime": "04:00",
                                "DayWeek": "monday",
                                "EndTime": "06:00"
                            }
                        }
                    },
                    {
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "directory",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "/docs/foods/;/dogs/ragdolls/"
                                }
                            ],
                            "Connective": "OR"
                        },
                        "DownloadSpeedLimitAction": {
                            "SpeedLimitRate": 300,
                            "SpeedLimitRateAfter": 90,
                            "SpeedLimitTime": {
                                "BeginTime": "04:00",
                                "DayWeek": "tuesday",
                                "EndTime": "06:00"
                            }
                        }
                    },
                    {
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "path",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "/docs/file1;/docs/file2"
                                }
                            ],
                            "Connective": "OR"
                        },
                        "DownloadSpeedLimitAction": {
                            "SpeedLimitRate": 400,
                            "SpeedLimitRateAfter": 90,
                            "SpeedLimitTime": {
                                "BeginTime": "04:00",
                                "DayWeek": "wednesday",
                                "EndTime": "13:59"
                            }
                        }
                    },
                    {
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "regex",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "^/a{1,2}(.*)g$"
                                }
                            ],
                            "Connective": "OR"
                        },
                        "DownloadSpeedLimitAction": {
                            "SpeedLimitRate": 500,
                            "SpeedLimitRateAfter": 90,
                            "SpeedLimitTime": {
                                "BeginTime": "04:00",
                                "DayWeek": "thursday",
                                "EndTime": "05:59"
                            }
                        }
                    }
                ],
                "Switch": true
            },
            "FollowRedirect": true,
            "HTTPS": {
                "CertInfo": {
                    "CertId": "cert-7fade0eb4f8d4aadbde5dd25f2ffdf35",
                    "CertName": "1000011991",
                    "EncryType": "inter_cert",
                    "ExpireTime": 1763086346,
                    "Source": "cert_center"
                },
                "DisableHttp": false,
                "ForcedRedirect": {
                    "EnableForcedRedirect": true,
                    "StatusCode": "303"
                },
                "HTTP2": true,
                "Hsts": {
                    "Subdomain": "include",
                    "Switch": true,
                    "Ttl": 50
                },
                "OCSP": true,
                "Switch": true,
                "TlsVersion": [
                    "tlsv1.1",
                    "tlsv1.2"
                ]
            },
            "HttpForcedRedirect": {
                "EnableForcedRedirect": false,
                "StatusCode": "301"
            },
            "IPv6": {
                "Switch": true
            },
            "IpAccessRule": {
                "Ip": [
                    "203.0.113.0/24",
                    "198.51.100.4"
                ],
                "RuleType": "allow",
                "Switch": true
            },
            "MethodDeniedRule": {
                "Methods": "POST,DELETE,CONNECT,OPTIONS",
                "Switch": true
            },
            "MultiRange": {
                "Switch": false
            },
            "NegativeCache": [
                {
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "filetype",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "jpg;png"
                            }
                        ],
                        "Connective": "OR"
                    },
                    "NegativeCacheRule": {
                        "Action": "cache",
                        "IgnoreCase": false,
                        "StatusCode": "400",
                        "Ttl": 60
                    }
                },
                {
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "directory",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/foods/;/dogs/ragdolls/"
                            }
                        ],
                        "Connective": "OR"
                    },
                    "NegativeCacheRule": {
                        "Action": "cache",
                        "IgnoreCase": true,
                        "StatusCode": "401",
                        "Ttl": 59
                    }
                },
                {
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "path",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/file1;/docs/file2"
                            }
                        ],
                        "Connective": "OR"
                    },
                    "NegativeCacheRule": {
                        "Action": "cache",
                        "IgnoreCase": false,
                        "StatusCode": "402",
                        "Ttl": 70
                    }
                },
                {
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "regex",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "^/a{1,2}(.*)g$"
                            }
                        ],
                        "Connective": "OR"
                    },
                    "NegativeCacheRule": {
                        "Action": "cache",
                        "IgnoreCase": false,
                        "StatusCode": "404",
                        "Ttl": 60
                    }
                }
            ],
            "OfflineCache": {
                "Object": "request_error,error_code",
                "StatusCode": "504;505",
                "Switch": true
            },
            "Origin": [
                {
                    "OriginAction": {
                        "OriginLines": [
                            {
                                "Address": "203.0.113.8",
                                "HttpPort": "80",
                                "HttpsPort": "443",
                                "InstanceType": "ip",
                                "OriginHost": "myorigin.example.com",
                                "OriginType": "primary",
                                "PrivateBucketAccess": false,
                                "Weight": "1"
                            },
                            {
                                "Address": "img.example.com",
                                "HttpPort": "80",
                                "HttpsPort": "443",
                                "InstanceType": "domain",
                                "OriginHost": "myorigin2.example.com",
                                "OriginType": "primary",
                                "PrivateBucketAccess": false,
                                "Weight": "1"
                            },
                            {
                                "Address": "bpcntest.tos-ap-southeast-3.bytepluses.com",
                                "InstanceType": "tos",
                                "OriginHost": "bpcntest.tos-ap-southeast-3.bytepluses.com",
                                "OriginType": "primary",
                                "PrivateBucketAccess": true,
                                "PrivateBucketAuth": {
                                    "AuthType": "tos",
                                    "Switch": true
                                },
                                "Region": "ap-southeast-3",
                                "Weight": "1"
                            },
                            {
                                "Address": "mybucket.oss-ap-southeast-1.aliyuncs.com",
                                "InstanceType": "tos",
                                "OriginHost": "mybucket.oss-ap-southeast-1.aliyuncs.com",
                                "OriginType": "primary",
                                "PrivateBucketAccess": true,
                                "PrivateBucketAuth": {
                                    "AuthType": "oss",
                                    "Switch": true,
                                    "TosAuthInformation": {
                                        "AccessKeyId": "xxxxxxxxxx",
                                        "AccessKeySecret": "xxxxxx"
                                    }
                                },
                                "Region": "oss-ap-southeast-1",
                                "Weight": "2"
                            },
                            {
                                "Address": "mybucket.cos.ap-singapore.myqcloud.com",
                                "InstanceType": "tos",
                                "OriginHost": "mybucket.cos.ap-singapore.myqcloud.com",
                                "OriginType": "primary",
                                "PrivateBucketAccess": true,
                                "PrivateBucketAuth": {
                                    "AuthType": "cos",
                                    "Switch": true,
                                    "TosAuthInformation": {
                                        "AccessKeyId": "xxxxxxxxxxxxxxxxxxx",
                                        "AccessKeySecret": "xxxxxxxxxxxx"
                                    }
                                },
                                "Region": "ap-singapore",
                                "Weight": "3"
                            },
                            {
                                "Address": "my-bucket.s3.ap-southeast-1.amazonaws.com",
                                "InstanceType": "tos",
                                "OriginHost": "my-bucket.s3.ap-southeast-1.amazonaws.com",
                                "OriginType": "primary",
                                "PrivateBucketAccess": true,
                                "PrivateBucketAuth": {
                                    "AuthType": "aws_common",
                                    "Switch": true,
                                    "TosAuthInformation": {
                                        "AccessKeyId": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
                                        "AccessKeySecret": "xxxxxxxxxx"
                                    }
                                },
                                "Region": "ap-southeast-1",
                                "Weight": "5"
                            },
                            {
                                "Address": "myazstorage.blob.core.windows.net",
                                "BucketName": "myazstorage",
                                "InstanceType": "tos",
                                "OriginHost": "myazstorage.blob.core.windows.net",
                                "OriginType": "primary",
                                "PrivateBucketAccess": true,
                                "PrivateBucketAuth": {
                                    "AuthType": "azure",
                                    "Switch": true,
                                    "TosAuthInformation": {
                                        "AccountKey": "xxxxxxxxxxxxxxxx"
                                    }
                                },
                                "Weight": "1"
                            },
                            {
                                "Address": "203.0.113.9",
                                "HttpPort": "80",
                                "HttpsPort": "443",
                                "InstanceType": "ip",
                                "OriginType": "backup",
                                "PrivateBucketAccess": false,
                                "Weight": "1"
                            },
                            {
                                "Address": "img2.example.com",
                                "HttpPort": "80",
                                "HttpsPort": "443",
                                "InstanceType": "domain",
                                "OriginType": "backup",
                                "PrivateBucketAccess": false,
                                "Weight": "1"
                            }
                        ]
                    }
                }
            ],
            "OriginAccessRule": {
                "AllowEmpty": true,
                "IgnoreCase": true,
                "Origins": [
                    "test.example.net",
                    "my.example.net"
                ],
                "RuleType": "deny",
                "Switch": true
            },
            "OriginArg": [
                {
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "regex",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "^/a{1,2}(.*)g$"
                            }
                        ],
                        "Connective": "OR"
                    },
                    "OriginArgAction": {
                        "OriginArgComponents": [
                            {
                                "Action": "set",
                                "Object": "queryString",
                                "Subobject": "key3=val3;key4=val4"
                            }
                        ]
                    }
                },
                {
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "filetype",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "png;jpg"
                            }
                        ],
                        "Connective": "OR"
                    },
                    "OriginArgAction": {
                        "OriginArgComponents": [
                            {
                                "Action": "excludePart",
                                "Object": "queryString",
                                "Subobject": "param1;param2"
                            }
                        ]
                    }
                },
                {
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "directory",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/foods/;/dogs/ragdolls/"
                            }
                        ],
                        "Connective": "OR"
                    },
                    "OriginArgAction": {
                        "OriginArgComponents": [
                            {
                                "Action": "includePart",
                                "Object": "queryString",
                                "Subobject": "param1;param2"
                            }
                        ]
                    }
                },
                {
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "path",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/file3;/docs/file4"
                            }
                        ],
                        "Connective": "OR"
                    },
                    "OriginArgAction": {
                        "OriginArgComponents": [
                            {
                                "Action": "addPart",
                                "Object": "queryString",
                                "Subobject": "key1=val1;key2=val2"
                            }
                        ]
                    }
                },
                {
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "path",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/file1;/docs/file2"
                            }
                        ],
                        "Connective": "OR"
                    },
                    "OriginArgAction": {
                        "OriginArgComponents": [
                            {
                                "Action": "exclude",
                                "Object": "queryString",
                                "Subobject": "*"
                            }
                        ]
                    }
                },
                {
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "directory",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/"
                            }
                        ],
                        "Connective": "OR"
                    },
                    "OriginArgAction": {
                        "OriginArgComponents": [
                            {
                                "Action": "include",
                                "Object": "queryString",
                                "Subobject": "*"
                            }
                        ]
                    }
                }
            ],
            "OriginCertCheck": {
                "Switch": true
            },
            "OriginHost": "superhost.example.com",
            "OriginIPv6": "ipv6_first",
            "OriginProtocol": "https",
            "OriginRange": true,
            "Range": {
                "Switch": true,
                "RangeSize": "2",
                "Unit": "MB"
            },
            "OriginRewrite": {
                "Switch": false
            },
            "OriginSni": {
                "SniDomain": "superhost.example.com",
                "Switch": true
            },
            "PageOptimization": {
                "OptimizationType": [
                    "html",
                    "js",
                    "css"
                ],
                "Switch": true
            },
            "Project": "default",
            "Quic": {
                "Switch": true
            },
            "RedirectionRewrite": {
                "RedirectionRule": [
                    {
                        "RedirectionAction": {
                            "RedirectCode": "302",
                            "SourcePath": "^/a{1,2}(.*)g$",
                            "TargetHost": "www.example.com",
                            "TargetPath": "/food$1g",
                            "TargetProtocol": "https",
                            "TargetQueryComponents": {
                                "Action": "includePart",
                                "Value": "param1"
                            }
                        }
                    },
                    {
                        "RedirectionAction": {
                            "RedirectCode": "307",
                            "SourcePath": "aaa(.*)",
                            "TargetHost": "www.example.com",
                            "TargetPath": "/food/$1g",
                            "TargetProtocol": "followclient",
                            "TargetQueryComponents": {
                                "Action": "include",
                                "Value": "*"
                            }
                        }
                    }
                ],
                "Switch": true
            },
            "RefererAccessRule": {
                "AllowEmpty": true,
                "Referers": [
                    "www.example.org",
                    "docs.example.com",
                    "^https://test.example.com/a{1,2}bc/.*\\.jpg$"
                ],
                "ReferersType": {
                    "CommonType": {
                        "IgnoreCase": true,
                        "IgnoreScheme": true,
                        "Referers": [
                            "www.example.org",
                            "docs.example.com"
                        ]
                    },
                    "RegularType": {
                        "Referers": [
                            "^https://test.example.com/a{1,2}bc/.*\\.jpg$"
                        ]
                    }
                },
                "RuleType": "allow",
                "Switch": true
            },
            "RemoteAuth": {
                "RemoteAuthRules": [
                    {
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "filetype",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "bmp;pdf"
                                },
                                {
                                    "Object": "directory",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "/docs/foods/;/dogs/ragdolls/"
                                },
                                {
                                    "Object": "path",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "/docs/file1;/docs/file2"
                                }
                            ],
                            "Connective": "OR"
                        },
                        "RemoteAuthRuleAction": {
                            "AuthModeConfig": {
                                "BackupRemoteAddr": "https://myendpoint2.com",
                                "MasterRemoteAddr": "https://myendpoint1.com",
                                "PathType": "variable",
                                "PathValue": "/sign",
                                "RequestMethod": "post"
                            },
                            "AuthResponseConfig": {
                                "CacheAction": {
                                    "Action": "cache",
                                    "CacheKey": [
                                        "URI",
                                        "content_type"
                                    ],
                                    "IgnoreCase": false,
                                    "Ttl": 40
                                },
                                "ResponseAction": {
                                    "StatusCode": "403"
                                },
                                "StatusCodeAction": {
                                    "DefaultAction": "pass",
                                    "FailCode": "401",
                                    "SuccessCode": "200"
                                },
                                "TimeOutAction": {
                                    "Action": "pass",
                                    "Time": 200
                                }
                            },
                            "QueryStringRules": {
                                "QueryStringComponents": {
                                    "Action": "includePart",
                                    "Value": "size;color"
                                },
                                "QueryStringInstances": [
                                    {
                                        "Action": "set",
                                        "Key": "param1",
                                        "Value": "val1",
                                        "ValueType": "constant"
                                    },
                                    {
                                        "Action": "set",
                                        "Key": "param2",
                                        "Value": "content_type",
                                        "ValueType": "variable"
                                    }
                                ]
                            },
                            "RequestBodyRules": "default",
                            "RequestHeaderRules": {
                                "RequestHeaderComponents": {
                                    "Action": "includePart",
                                    "Value": "header1;header2"
                                },
                                "RequestHeaderInstances": [
                                    {
                                        "Action": "set",
                                        "Key": "hd1",
                                        "Value": "val1",
                                        "ValueType": "constant"
                                    },
                                    {
                                        "Action": "set",
                                        "Key": "hd2",
                                        "Value": "client_ip",
                                        "ValueType": "variable"
                                    }
                                ],
                                "RequestHost": "test.example.com"
                            }
                        }
                    }
                ],
                "Switch": true
            },
            "RequestBlockRule": {
                "BlockRule": [
                    {
                        "BlockAction": {
                            "Action": "refuse",
                            "StatusCode": "404"
                        },
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "path",
                                    "Operator": "equal",
                                    "Type": "url",
                                    "Value": "/docs/file1;/docs/file2"
                                },
                                {
                                    "Object": "directory",
                                    "Operator": "equal",
                                    "Type": "url",
                                    "Value": "/docs/foods/;/dogs/ragdolls/"
                                },
                                {
                                    "Object": "filetype",
                                    "Operator": "equal",
                                    "Type": "url",
                                    "Value": "jpg;png"
                                },
                                {
                                    "Name": "param1",
                                    "Object": "query_name",
                                    "Operator": "equal",
                                    "Type": "querystring",
                                    "Value": "val1"
                                },
                                {
                                    "Object": "regex",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "/a{1,2}(.*)g$"
                                }
                            ],
                            "Connective": "OR"
                        },
                        "RuleName": "myrule1"
                    },
                    {
                        "BlockAction": {
                            "Action": "redirect",
                            "RedirectUrl": "https://www.example.com/helloworld",
                            "StatusCode": "301"
                        },
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "full_querystring",
                                    "Operator": "not_match",
                                    "Type": "querystring",
                                    "Value": ".*size=.*\\&.*"
                                },
                                {
                                    "Object": "client_ip",
                                    "Operator": "match",
                                    "Type": "client_ip",
                                    "Value": "203.0.113.2;203.0.113.5"
                                },
                                {
                                    "Object": "ua",
                                    "Operator": "not_empty",
                                    "Type": "request_header"
                                },
                                {
                                    "Name": "myheader",
                                    "Object": "customize",
                                    "Operator": "match",
                                    "Type": "request_header",
                                    "Value": "value1"
                                }
                            ],
                            "Connective": "AND"
                        },
                        "RuleName": "myrule2"
                    }
                ],
                "Switch": true
            },
            "RequestHeader": [
                {
                    "RequestHeaderAction": {
                        "RequestHeaderInstances": [
                            {
                                "Action": "set",
                                "Key": "header1",
                                "Value": "val1",
                                "ValueType": "constant"
                            },
                            {
                                "Action": "set",
                                "Key": "header2",
                                "Value": "uri",
                                "ValueType": "variable"
                            },
                            {
                                "Action": "set",
                                "Key": "header3",
                                "Value": "myval${http_host}is${query_string}",
                                "ValueType": "customize"
                            },
                            {
                                "Action": "delete",
                                "Key": "header4"
                            }
                        ]
                    }
                }
            ],
            "ResourceTags": [
                {
                    "Key": "key1",
                    "Value": "value1"
                },
                {
                    "Key": "key2",
                    "Value": "value2"
                }
            ],
            "ResponseHeader": [
                {
                    "ResponseHeaderAction": {
                        "ResponseHeaderInstances": [
                            {
                                "AccessOriginControl": true,
                                "Action": "set",
                                "Key": "Access-Control-Allow-Origin",
                                "Value": "myval",
                                "ValueType": "constant"
                            },
                            {
                                "AccessOriginControl": false,
                                "Action": "set",
                                "Key": "Access-Control-Allow-Headers",
                                "Value": "raw_uri",
                                "ValueType": "variable"
                            },
                            {
                                "AccessOriginControl": false,
                                "Action": "set",
                                "Key": "Access-Control-Expose-Headers",
                                "Value": "my${host}data${query_string}",
                                "ValueType": "customize"
                            },
                            {
                                "AccessOriginControl": false,
                                "Action": "delete",
                                "Key": "Access-Control-Max-Age"
                            }
                        ]
                    }
                }
            ],
            "RuleEngine": {
                "Rules": [],
                "Switch": false
            },
            "ServiceRegion": "outside_chinese_mainland",
            "ServiceType": "web",
            "SignedUrlAuth": {
                "AuthRulesF": [
                    {
                        "ArgumentRule": {
                            "GeneralParamRule": {
                                "ParentLinkParamInherit": "inherit",
                                "SubLinkParamRule": {
                                    "InheritMode": "inherit_first",
                                    "KeepSubLinkArg": "keep"
                                }
                            },
                            "KeepOriginArg": true
                        },
                        "AuthTokenCalRule": {
                            "ParamCalRules": [
                                "md5_bin",
                                "base64url",
                                "sha256",
                                "md5",
                                "base64_encode"
                            ],
                            "SignJoinSymbol": "abc",
                            "SignParam": [
                                {
                                    "ParamType": "SecretKey"
                                },
                                {
                                    "ParamType": "SupString",
                                    "SupContent": "fixstring"
                                },
                                {
                                    "ParamSource": "ChildLink",
                                    "ParamType": "URI",
                                    "UriParamSup": {
                                        "JoinSymbol": "/",
                                        "SplitSymbol": "-",
                                        "StartLevel": 3,
                                        "TermLevel": 5
                                    }
                                },
                                {
                                    "ParamSource": "ParentLink",
                                    "ParamType": "URLParam",
                                    "UrlParam": {
                                        "ArgSegment": {
                                            "Level": 0,
                                            "Switch": false
                                        },
                                        "CapMode": "uri",
                                        "UriLevel": 3
                                    }
                                },
                                {
                                    "ParamType": "ClientDomain"
                                },
                                {
                                    "ParamType": "Referer"
                                },
                                {
                                    "ParamType": "Origin"
                                },
                                {
                                    "ParamType": "ClientIP"
                                },
                                {
                                    "ParamType": "UA"
                                },
                                {
                                    "ParamType": "ReqHeader",
                                    "RequestHeader": "myheader1"
                                },
                                {
                                    "CookieToken": "mycookie1",
                                    "ParamType": "Cookie"
                                },
                                {
                                    "ParamSource": "ChildLink",
                                    "ParamType": "FullURI"
                                }
                            ]
                        },
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "filetype",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "jpg;png"
                                },
                                {
                                    "Object": "directory",
                                    "Operator": "not_match",
                                    "Type": "url",
                                    "Value": "/docs/foods/;/dogs/ragdolls/"
                                },
                                {
                                    "Object": "path",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "/docs/file1;/docs/file2"
                                },
                                {
                                    "Object": "regex",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "^/a{1,2}(.*)g$"
                                }
                            ],
                            "Connective": "OR"
                        },
                        "CustomRewrite": {
                            "RewriteParam": [
                                {
                                    "ParamType": "ParentLinkUrlParam",
                                    "ParentLinkUrlParam": {
                                        "ArgSegment": {
                                            "Level": 0,
                                            "Switch": false
                                        },
                                        "CapMode": "name",
                                        "ParamName": "param23"
                                    }
                                },
                                {
                                    "ParamType": "SupString",
                                    "SupContent": "string2"
                                },
                                {
                                    "ParamType": "ParentLinkURI",
                                    "ParentLinkUriParamSup": {
                                        "JoinSymbol": "/",
                                        "SplitSymbol": "-",
                                        "StartLevel": 4,
                                        "TermLevel": 6
                                    }
                                },
                                {
                                    "ParamType": "ParentLinkExpire"
                                },
                                {
                                    "ParamType": "AuthToken"
                                },
                                {
                                    "ParamType": "ParentFullURI"
                                }
                            ],
                            "RewriteRule": {
                                "CapMode": "name",
                                "ParamName": "myparam1"
                            },
                            "SignJoinSymbol": "/",
                            "Switch": true
                        },
                        "ExpireTimeRule": {
                            "Duration": 30,
                            "ExpTimeCapRule": {
                                "ArgSegment": {
                                    "Level": 0,
                                    "Switch": false
                                },
                                "CapMode": "name",
                                "ParamName": "param1"
                            },
                            "TimeFormat": "heximal"
                        },
                        "RewriteFormat": "default",
                        "RewriteM3U8": {
                            "RewriteM3U8Tag": {
                                "Switch": true,
                                "Tags": [
                                    "tag1",
                                    "tag2"
                                ]
                            },
                            "Switch": true
                        },
                        "RewriteMPD": {
                            "MpdVarExpand": true,
                            "Switch": true
                        },
                        "RuleName": "Authentication rule A",
                        "SecretKey": {
                            "BackupSecretKey": "secondarykey",
                            "MasterSecretKey": "primarykey"
                        },
                        "SignCapRule": {
                            "ArgSegment": {
                                "Level": 2,
                                "SplitSymbol": "-",
                                "Switch": true
                            },
                            "CapMode": "uri",
                            "UriLevel": 2
                        }
                    },
                    {
                        "ArgumentRule": {
                            "GeneralParamRule": {
                                "ParentLinkParamInherit": "not_inherit",
                                "SubLinkParamRule": {
                                    "InheritMode": "sub_link_first",
                                    "KeepSubLinkArg": "keep"
                                }
                            },
                            "KeepOriginArg": false
                        },
                        "AuthTokenCalRule": {
                            "ParamCalRules": [
                                "base64url"
                            ],
                            "SignJoinSymbol": "45yu",
                            "SignParam": [
                                {
                                    "ParamType": "SecretKey"
                                }
                            ]
                        },
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "directory",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "/"
                                }
                            ],
                            "Connective": "OR"
                        },
                        "ExpireTimeRule": {
                            "Duration": 67,
                            "ExpTimeCapRule": {
                                "CapMode": "cookie",
                                "CustomValue": "mycookie56"
                            },
                            "TimeFormat": "octal"
                        },
                        "RewriteFormat": "default",
                        "RuleName": "Authentication rule B",
                        "SecretKey": {
                            "BackupSecretKey": "sk",
                            "MasterSecretKey": "pk"
                        },
                        "SignCapRule": {
                            "CapMode": "header",
                            "CustomValue": "myheader56"
                        }
                    }
                ],
                "Switch": true
            },
            "Status": "online",
            "Timeout": {
                "Switch": true,
                "TimeoutRules": [
                    {
                        "TimeoutAction": {
                            "HttpTimeout": 10,
                            "TcpTimeout": 5
                        }
                    }
                ]
            },
            "UaAccessRule": {
                "AllowEmpty": true,
                "IgnoreCase": true,
                "RuleType": "deny",
                "Switch": true,
                "UserAgent": [
                    "*curl*",
                    "*firefox*"
                ]
            },
            "UpdateTime": 1755323476,
            "UrlNormalize": {
                "NormalizeObject": [
                    "back_slashes",
                    "successive_slashes",
                    "dot_segments"
                ],
                "Switch": true
            },
            "VideoDrag": {
                "Switch": true
            },
            "Websocket": {
                "Switch": true,
                "Timeout": 60
            }
        }
    }
}
```


&nbsp;
