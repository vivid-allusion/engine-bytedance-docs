---
title: "E 類型"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/Type-E_zh-tw"
---

本文件介紹 BytePlus CDN 中 URL 驗證模組中 E 類型驗證的配置。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_8069a5671e6db882532205c6c05c9287.png) </span>

<span id="控制台中的配置"></span>
## **控制台中的配置**

在 CDN 控制台中，您需要做以下配置：


|**配置** |**說明** |
|---|---|
|驗證規則 |表示一組規則，定義了哪些請求需要被驗證。您至少需要新增一條規則，最多可以新增 10 條。多個規則之間的關係是 **或**，表示匹配任何一個規則的請求就會被驗證。每條規則包含條件類型、匹配方式和規則內容。<br><br>&nbsp;<br><br>規則內容的長度不能超過 1,024 個字元，不能包含以下字元：<br><br><br>* 連續斜線（//）、空格、美元符號（$）、問號（?）、Delete（ASCII code 127）。<br><br><br>同時，<br><br><br>* 如果條件類型是 **檔案副檔名**，規則內容必須是一個或者多個以分號（;）分隔的檔案副檔名。檔案副檔名無需以句點（.）開頭。例如：`png;txt`。<br><br>* 如果條件類型是 **檔案目錄**，規則內容必須是一個或者多個以分號（;）分隔的目錄路徑。目錄路徑必須以斜線（/）開頭和結尾。例如：`/chs/foods/;/us/birds/`。<br><br>* 如果條件類型是 **URL 全路徑**，規則內容必須是一個或者多個以分號（;）分隔的檔案路徑。檔案路徑必須以斜線（/）開頭，可以包含星號（\*）用來表示一個或者多個字元。例如：`/chs/foods/local*sets;/us/birds/chickadee`。 |
|主金鑰 |指定一個主金鑰。金鑰由 6\-40 個字元組成，只能包含除了 Delete（ASCII code 127）的可列印 ASCII 字元。 |
|備份金鑰 |指定一個備份金鑰。金鑰的輸入要求與主金鑰相同。如果驗證失敗，CDN 會使用備份金鑰再計算一次簽章並嘗試與客戶端請求中的簽章比對。 |
|簽章參數 |指定請求的簽章參數名稱。參數名稱的說明如下：<br><br><br>* 不能超過 100 個字元。<br><br>* 大小寫敏感。<br><br>* 可以包含字母、數字、底線（_）、中線（\-）、句點（.）、逗號（,）、驚嘆號（!）。<br><br>* 至少包含一個字母或者數字。<br><br>* 不能與時間標記參數相同。<br><br>* 控制台中預設的簽章參數是 `sign`。 |
|簽章有效時間 |指定簽章的有效時間，單位是秒。該配置與 [自定義計算規則](https://docs.byteplus.com/en/docs/18/36287#%E8%87%AA%E5%AE%9A%E7%BE%A9%E8%A8%88%E7%AE%97%E8%A6%8F%E5%89%87) 中包含的 **時間標記參數** 搭配使用，用來計算簽章的過期時間。該參數的取值範圍是 0\-315,360,000。簽章的過期時間 = timestamp + 有效時間。在 CDN 收到一個請求時，如果請求中的簽章的過期時間早於當前時間，CDN 判定簽章已過期。此時，CDN 拒絕該請求並返回 403 回應狀態碼，表示驗證失敗。控制台中預設的有效時間是 `1800`。 |
|時間標記參數 |指定請求的時間標記參數的名稱。參數名稱的說明如下：<br><br><br>* 不能超過 100 個字元。<br><br>* 大小寫敏感。<br><br>* 可以包含字母、數字、底線（_）、中線（\-）、句點（.）、逗號（,）、驚嘆號（!）。<br><br>* 不能與簽章參數相同。<br><br>* 控制台中預設的簽章參數是 `t`。 |
|時間標記格式 |指定 Unix 時間標記的格式。 |
|計算規則 |指定參與簽章計算的驗證參數以及這些參數的順序。 |


<span id="新增參與簽章計算的自定義變數"></span>
### 新增參與簽章計算的自定義變數

對於 E 類型，您可以新增自定義的變數用於簽章計算。您最多可以新增 50 個變數。您可以點擊 **新增規則** 新增一個變數。規則的各配置說明如下：


|**配置** |**說明** |
|---|---|
|變數類型 |指定變數的類型。該配置有以下選項：<br><br><br>* 請求參數：表示該變數是請求 URL 中的一個查詢參數。<br><br>* 請求標頭：表示該變數是請求中的一個標頭。 |
|取值方式 |表示 CDN 如何將 **值** 與請求中的參數匹配。當前，該配置的取值必須是 **匹配**。 |
|值 |表示需要額外參與簽章計算的變數名稱。變數名稱不能超過 100 個字元。其他要求如下：<br><br><br>* 如果 **變數類型** 是 **請求參數**，變數名稱可以包含字母、數字、連字號（\-）、逗號（,）、句點（.）、驚嘆號（!）。<br><br>* 如果 **變數類型** 是 **請求標頭**，變數名稱可以包含可列印 ASCII 字元，除了以下這些字元：<br><br>   * 底線（_）、空格、雙引號（"）、冒號（:）、Delete（ASCII code 127）。 |
|操作 |表示您可以對該規則進行的操作。 |


在您新增自定義變數後，您就可以在設定 **計算規則** 時選擇該變數了。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0d9fa73bb5f6476f831777f799e66331~tplv-goo7wpa0wc-image.image) </span>

<span id="請求-url-格式"></span>
## 請求 URL 格式

```XML
scheme://host/uri?sign=\<signature\>&t=timestamp(&...)
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>timestamp</code> 的精度是秒。</div>


<span id="請求-url-示例"></span>
## 請求 URL 示例

```XML
https://www.example.com/product/cdn?sign=e954e253c33634b510443af72406600f&t=1620291453&query1=value1&query2=value2
```


<span id="簽章計算公式"></span>
## 簽章計算公式

簽章 的計算公式如下：

```XML
md5(<自定義計算規則>)
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">MD5 的值是由 32 個十六進制字元組成的。</div>


* <div data-tips="true" data-tips-type="tip"><em><自定義計算規則\></em> 表示的是參與簽章計算的驗證參數，按指定的出現順序的拼接。</div>



<span id="自定義計算規則"></span>
## 自定義計算規則

對於簽章計算，其他驗證類型只能使用預設的計算規則，但是 E 類型允許您自定義計算規則。

您可以指定計算規則包含以下參數，並且通過拖曳調整參數的在計算規則中的出現順序。


|**參數** |**是否必選** |**描述** |
|---|---|---|
|金鑰 |是 |表示在 CDN 控制台配置的金鑰。 |
|URI |是 |表示 [請求 URL 格式](https://docs.byteplus.com/en/docs/18/36287#%E8%AF%B7%E6%B1%82-url-%E6%A0%BC%E5%BC%8F) 中的 `uri` 參數，以斜線（/）開頭，不包含網域名稱。如果路徑包含中文字元，您需要對路徑編碼。在 [請求 URL 示例](https://docs.byteplus.com/en/docs/18/36287#%E8%AF%B7%E6%B1%82-url-%E7%A4%BA%E4%BE%8B) 中，該參數值是 `/product/cdn`。 |
|時間標記參數 |是 |表示 [請求 URL 格式](https://docs.byteplus.com/en/docs/18/36287#%E8%AF%B7%E6%B1%82-url-%E6%A0%BC%E5%BC%8F) 中的 `timestamp` 參數。該參數與控制台中的 **簽名有效時間** 配置搭配使用，用來計算簽名的過期時間。根據控制台中的 **時間標記格式** 配置，時間格式使用十進位或十六進位的 Unix 時間標記。在 [請求 URL 示例](https://docs.byteplus.com/en/docs/18/36287#%E8%AF%B7%E6%B1%82-url-%E7%A4%BA%E4%BE%8B) 中，該參數值是 `1620291453`，是一個十進位 Unix 時間標記。 |
|Referer |否 |表示用戶請求中 Referer 標頭的值。 |
|用戶端網域名稱 |否 |表示請求的網域名稱。 |
|Origin |否 |表示請求中 Origin 標頭的值。 |
|用戶端IP |否 |表示用戶端的 IP 位址。 |
|User\-Agent |否 |表示請求中 User\-Agent 標頭的值。 |
|<自定義變數\> |否 |表示您在自定義簽名計算變數中定義的變數名稱。您在 [添加參與簽名計算的自定義變數](https://docs.byteplus.com/en/docs/18/36287#%E6%B7%BB%E5%8A%A0%E5%8F%82%E4%B8%8E%E7%AD%BE%E5%90%8D%E8%AE%A1%E7%AE%97%E7%9A%84%E8%87%AA%E5%AE%9A%E4%B9%89%E5%8F%98%E9%87%8F) 步驟中添加的變數會出現在參數列表中。 |


<span id="驗證流程"></span>
## 驗證流程

在收到包含簽名的用戶端請求時，CDN 使用的驗證流程如下：


1. 基於請求中包含的驗證參數以及您在 CDN 控制台中配置的金鑰，使用 [簽名計算公式](https://docs.byteplus.com/en/docs/18/36287#%E7%AD%BE%E5%90%8D%E8%AE%A1%E7%AE%97%E5%85%AC%E5%BC%8F) 計算簽名。

2. 判斷 CDN 計算得到的簽名和用戶端請求中包含的簽名是否一致。如果不一致，CDN 判斷請求不合法，拒絕該請求。

3. 判斷請求是否過期。如果存在以下情況，CDN 判斷請求過期，拒絕該請求。

   * (用戶端請求中的 timestamp 參數) + (您在 CDN 控制台中配置的簽名有效時間) < (CDN 收到該請求的時間)
