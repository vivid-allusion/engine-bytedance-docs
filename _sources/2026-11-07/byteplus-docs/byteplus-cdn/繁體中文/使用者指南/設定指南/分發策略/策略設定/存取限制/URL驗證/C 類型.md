---
title: "C 類型"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/Type-C_zh-tw"
---

本文件介紹 BytePlus CDN 中 URL 驗證模組中 C 類型的配置。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_987f835192a52d2587c82ef99c4c658a.png) </span>

<span id="控制台中的配置"></span>
## **控制台中的配置**

在 CDN 控制台中，您需要做以下配置：


|**配置** |**說明** |
|---|---|
|驗證規則 |表示一條規則，定義了哪些請求需要被驗證。規則包含條件類型、匹配方式和規則內容。當 CDN 收到一個使用者請求時，會將該規則與請求相匹配。如果規則與請求匹配，則 CDN 對該請求進行驗證。<br><br>&nbsp;<br><br>規則內容的長度不能超過 1,024 個字元，不能包含以下任意字元：<br><br><br>* 連續斜線（//）、空格、美元符號（$）、問號（?）、Delete（ASCII code 127）。<br><br><br>同時，<br><br><br>* 如果條件類型是 **檔案副檔名**，規則內容必須是一個或者多個以分號（;）分隔的檔案副檔名。檔案副檔名無需以句點（.）開頭。例如：`png;txt`。<br><br>* 如果條件類型是 **檔案目錄**，規則內容與匹配類型只能使用系統預設值。預設值表示所有檔案的請求都需要被驗證。 |
|主金鑰 |指定一個主金鑰。金鑰由 6\-40 個字元組成，只能包含除了 Delete（ASCII code 127）的可列印 ASCII 字元。 |
|備份金鑰 |指定一個備份金鑰。金鑰的輸入要求與主金鑰相同。如果驗證失敗，CDN 會使用備份金鑰再計算一次簽章並嘗試與用戶端請求中的簽章比對。 |
|簽章有效時間 |指定簽章的有效時間，單位是秒。該配置與用戶端請求中的 **timestamp** 參數搭配使用，用來計算簽章的過期時間。該參數的取值範圍是 0\-315,360,000。簽章的過期時間 = timestamp + 有效時間。在 CDN 收到一個請求時，如果請求中的簽章的過期時間早於目前時間，CDN 判定簽章已過期。此時，CDN 拒絕該請求並返回 403 回應狀態碼，表示驗證失敗。控制台中預設的有效時間是 `1800`。 |


<span id="請求-url-格式"></span>
## 請求 URL 格式

```XML
scheme://host/<signature>/timestamp/uri(?query_params)
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>timestamp</code> 的精度是秒。</div>


<span id="請求-url-示例"></span>
## 請求 URL 示例

```XML
https://www.example.com/b1725c0a6120092863001cd8004c4adb/6093AF7D/product/cdn?query1=value1&query2=value2
```


<span id="簽章計算公式"></span>
## 簽章計算公式

簽章 的計算公式如下：

```XML
md5(key + uri + timestamp)
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">公式中的 <code>+</code> 表示參數值的拼接，並不是實際的字符。</div>


* <div data-tips="true" data-tips-type="tip">MD5 的值是由 32 個十六進制字符組成的。</div>



簽章計算公式中各參數的說明如下：


|**參數** |**描述** |
|---|---|
|key |表示在 CDN 控制台配置的密鑰。 |
|uri |表示 [請求 URL 格式](https://docs.byteplus.com/en/docs/18/36285#%E8%AF%B7%E6%B1%82-url-%E6%A0%BC%E5%BC%8F) 中的 `uri` 參數，以斜線（/）開頭，不包含網域名稱。如果路徑包含中文字元，您需要對路徑編碼。在 [請求 URL 示例](https://docs.byteplus.com/en/docs/18/36285#%E8%AF%B7%E6%B1%82-url-%E7%A4%BA%E4%BE%8B) 中，該參數值是 `/product/cdn`。 |
|timestamp |表示 [請求 URL 格式](https://docs.byteplus.com/en/docs/18/36285#%E8%AF%B7%E6%B1%82-url-%E6%A0%BC%E5%BC%8F) 中的 `timestamp` 參數，格式是十六進位的 Unix 時間標記。該參數與控制台中的 **簽名有效時間** 配置搭配使用，用來計算簽名的過期時間。在 [請求 URL 示例](https://docs.byteplus.com/en/docs/18/36285#%E8%AF%B7%E6%B1%82-url-%E7%A4%BA%E4%BE%8B) 中，該參數值是 `6093AF7D`。 |


<span id="驗證流程"></span>
## 驗證流程

在收到包含簽名的用戶端請求時，CDN 使用的驗證流程如下：


1. 基於請求中包含的驗證參數以及您在 CDN 控制台中配置的密鑰，使用 [簽名計算公式](https://docs.byteplus.com/en/docs/18/36285#%E7%AD%BE%E5%90%8D%E8%AE%A1%E7%AE%97%E5%85%AC%E5%BC%8F) 計算簽名。

2. 判斷 CDN 計算得到的簽名和用戶端請求中包含的簽名是否一致。如果不一致，CDN 判斷請求不合法，拒絕該請求。

3. 判斷請求是否過期。如果存在以下情況，CDN 判斷請求過期，拒絕該請求。

   * (用戶端請求中的 timestamp 參數) + (您在 CDN 控制台中配置的簽名有效時間) < (CDN 收到該請求的時間)
