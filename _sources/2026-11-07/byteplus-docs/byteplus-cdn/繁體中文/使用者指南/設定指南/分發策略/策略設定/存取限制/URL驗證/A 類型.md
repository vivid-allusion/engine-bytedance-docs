---
title: "A 類型"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/Type-A_zh-tw"
---

本文件介紹 BytePlus CDN 中 URL 驗證模組中 A 類型驗證的配置。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_058974faf3d56f96437732b6b66549ad.png) </span>

<span id="控制台配置說明"></span>
## **控制台配置說明**

在 CDN 控制台中，您需要做以下配置：


|配置 |說明 |
|---|---|
|驗證規則 |表示哪些檔案的請求需要被驗證。您至少需要添加一個規則，最多可以添加 10 個。多個規則之間的關係是 **或**，表示匹配任何一個規則的請求就會被驗證。每條規則包含條件類型、匹配方式和規則內容。<br><br>&nbsp;<br><br>規則內容的長度不能超過 1,024 個字符，不能包含以下字符：<br><br><br>* 連續斜線（//）、空格、美元符號（$）、問號（?）、Delete（ASCII code 127）。<br><br><br>同時，<br><br><br>* 如果條件類型是 **檔案副檔名**，規則內容必須是一個或者多個以分號（;）分隔的檔案副檔名。檔案副檔名無需以句點（.）開頭。例如：`png;txt`。<br><br>* 如果條件類型是 **檔案目錄**，規則內容必須是一個或者多個以分號（;）分隔的目錄路徑。目錄路徑必須以斜線（/）開頭和結尾。例如：`/chs/foods/;/us/birds/`。<br><br>* 如果條件類型是 **URL 全路徑**，規則內容必須是一個或者多個以分號（;）分隔的檔案路徑。檔案路徑必須以斜線（/）開頭，可以包含星號（\*）用來表示一個或者多個字符。例如：`/chs/foods/local*sets;/us/birds/chickadee`。 |
|主金鑰 |指定一個主金鑰。金鑰由 6\-40 個字符組成，只能包含除了 Delete（ASCII code 127）的可打印 ASCII 字符。 |
|備份金鑰 |指定一個備金鑰。金鑰的輸入要求與主金鑰相同。如果驗證失敗，CDN 會使用備金鑰再計算一次簽名並嘗試與用戶端請求中的簽名比對。 |
|簽名參數 |指定請求的簽名參數名稱。參數名稱的說明如下：<br><br><br>* 不能超過 100 個字符。<br><br>* 大小寫敏感。<br><br>* 可以包含字母、數字、底線（_）、中劃線（\-）、句號（.）、逗號（,）、驚嘆號（!）。<br><br>* 至少包含一個字母或者數字。<br><br>* 不能與時間標記參數相同。<br><br>* 控制台中預設的簽名參數是 `sign`。 |
|簽名有效時間 |指定簽名的有效時間，單位是秒。該配置與用戶端請求中的 **timestamp** 參數搭配使用，用來計算簽名的過期時間。該參數的取值範圍是 0\-315,360,000。簽名的過期時間 = timestamp + 有效時間。在 CDN 收到一個請求時，如果請求中的簽名的過期時間早於當前時間，CDN 判定簽名已過期。此時，CDN 拒絕該請求並返回 403 回應狀態碼，表示驗證失敗。控制台中預設的有效時間是 `1800`。 |
|M3U8 改寫 |對於使用者請求的 .m3u8 檔案，該配置表示在發送給使用者的 .m3u8 檔案中， CDN 是否對每個分片檔案（.ts）的 URL 添加該簽名。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">當前，CDN 不支援改寫壓縮檔案。因此，在以下任意情況下，CDN 不會改寫使用者請求的 .m3u8 檔案。</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">當 CDN 收到來源伺服器返回的 .m3u8 檔案時，來源伺服器回應中包含 Content\-Encoding 標頭。該標頭表示該 .m3u8 檔案是被壓縮的。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">該 .m3u8 檔案的請求匹配 "智能壓縮" 中的配置，表示 CDN 會對該 .m3u8 檔案進行壓縮。</div><br><br><br><br>在更新分片檔案的 URL 時，CDN 可以識別以下 URL 格式：<br><br><br>* 標準 URL。例如 `https://example.com/xxx/yyy/song.ts`<br><br>* 絕對路徑。例如 `/xxx/yyy/song.ts`<br><br>* 相對路徑。例如 `yyy/song.ts`<br><br><br>對於其他 URL 格式，CDN 可能會無法識別，導致無法在 URL 中添加簽名。 |


<span id="請求-url-格式"></span>
## 請求 URL 格式

```XML
scheme://host/uri?sign=timestamp-rand-uid-<SIGNATURE>(&...)
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>timestamp</code> 的精度是秒。</div>


<span id="請求-url-示例"></span>
## 請求 URL 示例

```XML
https://www.example.com/img/image.png?sign=1644406401-2e1ca42a1bb248408fc9cf435e5af744-0-54959c1ec3448bf8e992554476248fab
```


<span id="簽名計算公式"></span>
## 簽名計算公式

簽名 的計算公式如下：

```XML
md5(uri-timestamp-rand-uid-key)
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">公式中的 <code>-</code> 是實際的字符，用來分隔驗證參數。</div>


* <div data-tips="true" data-tips-type="tip">MD5 的值是由 32 個十六進制字符組成的。</div>



簽名計算公式中各參數的說明如下：


|**參數** |**描述** |
|---|---|
|key |表示在 CDN 控制台配置的金鑰。 |
|uri |表示 [請求 URL 格式](https://docs.byteplus.com/en/docs/18/36283#%E8%AF%B7%E6%B1%82-url-%E6%A0%BC%E5%BC%8F) 中的 `uri` 參數，以斜線（/）開頭，不包含網域名稱。如果路徑包含中文字符，您需要對路徑編碼。在 [請求 URL 示例](https://docs.byteplus.com/en/docs/18/36283#%E8%AF%B7%E6%B1%82-url-%E7%A4%BA%E4%BE%8B) 中，該參數值是 `/img/image.png`。 |
|timestamp |表示 [請求 URL 格式](https://docs.byteplus.com/en/docs/18/36283#%E8%AF%B7%E6%B1%82-url-%E6%A0%BC%E5%BC%8F) 中的 `timestamp` 參數，格式是十進制的 Unix 時間標記。該參數與控制台中的 **簽名有效時間** 配置搭配使用，用來計算簽名的過期時間。在 [請求 URL 示例](https://docs.byteplus.com/en/docs/18/36283#%E8%AF%B7%E6%B1%82-url-%E7%A4%BA%E4%BE%8B) 中，該參數值是 `1644406401`。 |
|rand |表示 [請求 URL 格式](https://docs.byteplus.com/en/docs/18/36283#%E8%AF%B7%E6%B1%82-url-%E6%A0%BC%E5%BC%8F) 中的 `rand` 參數，是一個隨機字符串。長度為 1\-100 位。可以包含字母和數字。在 [請求 URL 示例](https://docs.byteplus.com/en/docs/18/36283#%E8%AF%B7%E6%B1%82-url-%E7%A4%BA%E4%BE%8B) 中，該參數值是 `2e1ca42a1bb248408fc9cf435e5af744`。 |
|uid |表示使用者 ID，暫時未使用。您需要設置該參數值為 `0` 。 |


<span id="驗證流程"></span>
## 驗證流程

在收到包含簽名的用戶端請求時，CDN 使用的驗證流程如下：


1. 基於請求中包含的驗證參數以及您在 CDN 控制台中配置的金鑰，使用 [簽名計算公式](https://docs.byteplus.com/en/docs/18/36283#%E7%AD%BE%E5%90%8D%E8%AE%A1%E7%AE%97%E5%85%AC%E5%BC%8F) 計算簽名。

2. 判斷 CDN 計算得到的簽名和用戶端請求中包含的簽名是否一致。如果不一致，CDN 判斷請求不合法，拒絕該請求。

3. 判斷請求是否過期。如果存在以下情況，CDN 判斷請求過期，拒絕該請求。

   * (用戶端請求中的 timestamp 參數) + (您在 CDN 控制台中配置的簽名過期時間) < (CDN 收到該請求的時間)
