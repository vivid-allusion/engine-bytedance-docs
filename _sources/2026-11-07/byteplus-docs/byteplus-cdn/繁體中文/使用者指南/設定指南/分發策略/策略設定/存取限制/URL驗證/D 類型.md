---
title: "D 類型"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/Type-D_zh-tw"
---

本文件介紹 BytePlus CDN 中 URL 驗證模組中 D 類型的配置。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/71f50329184542e99abdd617c43fe11a~tplv-goo7wpa0wc-image.image) </span>

<span id="控制台中的配置"></span>
## **控制台中的配置**

在 CDN 控制台中，您需要做以下配置：


|**配置** |**說明** |
|---|---|
|驗證規則 |表示一組規則，定義了哪些請求需要被驗證。您至少需要添加一條規則，最多可以添加 10 條。多個規則之間的關係是 **或**，表示匹配任何一個規則的請求就會被驗證。每條規則包含條件類型、匹配方式和規則內容。<br><br>&nbsp;<br><br>規則內容的長度不能超過 1,024 個字符，不能包含以下字符：<br><br><br>* 連續斜杠（//）、空格、美元符號（$）、問號（?）、Delete（ASCII code 127）。<br><br><br>同時，<br><br><br>* 如果條件類型是 **檔案後綴**，規則內容必須是一個或者多個以分號（;）分隔的檔案後綴。檔案後綴無需以句點（.）開頭。例如：`png;txt`。<br><br>* 如果條件類型是 **檔案目錄**，規則內容必須是一個或者多個以分號（;）分隔的目錄路徑。目錄路徑必須以斜杠（/）開頭和結尾。例如：`/chs/foods/;/us/birds/`。<br><br>* 如果條件類型是 **URL 全路徑**，規則內容必須是一個或者多個以分號（;）分隔的檔案路徑。檔案路徑必須以斜杠（/）開頭，可以包含星號（\*）用來表示一個或者多個字符。例如：`/chs/foods/local*sets;/us/birds/chickadee`。 |
|主密鑰 |指定一個主密鑰。密鑰由 6\-40 個字符組成，只能包含除了 Delete（ASCII code 127）的可打印 ASCII 字符。 |
|備份密鑰 |指定一個備密鑰。密鑰的輸入要求與主密鑰相同。如果驗證失敗，CDN 會使用備密鑰再計算一次簽名並嘗試與請求中的簽名比對。 |
|簽名參數 |指定請求的簽名參數名稱。參數名稱的說明如下：<br><br><br>* 不能超過 100 個字符。<br><br>* 大小寫敏感。<br><br>* 可以包含字母、數字、底線（_）、中劃線（\-）、句號（.）、逗號（,）、驚嘆號（!）。<br><br>* 至少包含一個字母或者數字。<br><br>* 不能與時間標記參數相同。<br><br>* 控制台中預設的簽名參數是 `sign`。 |
|簽名有效時間 |指定簽名的有效時間，單位是秒。該配置與用戶端請求中的 **timestamp** 參數搭配使用，用來計算簽名的過期時間。該參數的取值範圍是 0\-315,360,000。簽名的過期時間 = timestamp + 有效時間。在 CDN 收到一個請求時，如果請求中的簽名的過期時間早於當前時間，CDN 判定簽名已過期。此時，CDN 拒絕該請求並返回 403 回應狀態碼，表示驗證失敗。控制台中預設的有效時間是 `1800`。 |
|時間標記參數 |指定請求的時間標記參數的名稱。參數名稱的說明如下：<br><br><br>* 不能超過 100 個字符。<br><br>* 大小寫敏感。<br><br>* 可以包含字母、數字、底線（_）、中劃線（\-）、句號（.）、逗號（,）、驚嘆號（!）。<br><br>* 不能與簽名參數相同。<br><br>* 控制台中預設的簽名參數是 `t`。 |
|時間標記格式 |指定 Unix 時間標記的格式。 |


<span id="請求-url-格式"></span>
## 請求 URL 格式

```XML
scheme://host/uri?sign=<signature>&t=timestamp(&...)
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>timestamp</code> 的精度是秒。</div>


<span id="請求-url-示例"></span>
## 請求 URL 示例

```XML
https://www.example.com/product/cdn?sign=e954e253c33634b510443af72406600f&t=1620291453&query1=value1&query2=value2
```


<span id="簽名計算公式"></span>
## 簽名計算公式

簽名 的計算公式如下：

```XML
md5(key + uri + timestamp)
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">公式中的 <code>+</code> 表示參數值的拼接，並不是實際的字元。</div>


* <div data-tips="true" data-tips-type="tip">MD5 的值是由 32 個十六進位字元組成的。</div>



簽名計算公式中各參數的說明如下：


|**參數** |**描述** |
|---|---|
|金鑰 |表示在 CDN 控制台配置的金鑰。 |
|uri |表示 [請求 URL 格式](https://docs.byteplus.com/en/docs/18/36286#%E8%AF%B7%E6%B1%82-url-%E6%A0%BC%E5%BC%8F) 中的 `uri` 參數，以斜杠（/）開頭，不包含網域名稱。如果路徑包含中文字符，您需要對路徑編碼。在 [請求 URL 示例](https://docs.byteplus.com/en/docs/18/36286#%E8%AF%B7%E6%B1%82-url-%E7%A4%BA%E4%BE%8B) 中，該參數值是 `/product/cdn`。 |
|時間標記 |表示 [請求 URL 格式](https://docs.byteplus.com/en/docs/18/36286#%E8%AF%B7%E6%B1%82-url-%E6%A0%BC%E5%BC%8F) 中的 `timestamp` 參數。該參數與控制台中的 **簽名有效時間** 配置搭配使用，用來計算簽名的過期時間。根據控制台中的 **時間標記格式** 配置，時間格式使用十進制或十六進制的 Unix 時間標記。在 [請求 URL 示例](https://docs.byteplus.com/en/docs/18/36286#%E8%AF%B7%E6%B1%82-url-%E7%A4%BA%E4%BE%8B) 中，該參數值是 `1620291453`，是一個十進制 Unix 時間標記。 |


<span id="驗證流程"></span>
## 驗證流程

在收到包含簽名的用戶端請求時，CDN 使用的驗證流程如下：


1. 基於請求中包含的驗證參數以及您在 CDN 控制台中配置的金鑰，使用 [簽名計算公式](https://docs.byteplus.com/en/docs/18/36286#%E7%AD%BE%E5%90%8D%E8%AE%A1%E7%AE%97%E5%85%AC%E5%BC%8F) 計算簽名。

2. 判斷 CDN 計算得到的簽名和用戶端請求中包含的簽名是否一致。如果不一致，CDN 判斷請求不合法，拒絕該請求。

3. 判斷請求是否過期。如果存在以下情況，CDN 判斷請求過期，拒絕該請求。

   * (用戶端請求中的 timestamp 參數) + (您在 CDN 控制台中配置的簽名有效時間) < (CDN 收到該請求的時間)
