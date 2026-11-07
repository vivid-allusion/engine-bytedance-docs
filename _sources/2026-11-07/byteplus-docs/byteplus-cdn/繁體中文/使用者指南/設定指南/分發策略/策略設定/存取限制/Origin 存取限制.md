---
title: "Origin 存取限制"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/origin-restriction_zh-tw"
---

本文件介紹如何在 BytePlus CDN 中設定 Origin 存取限制。

Origin 是一個 HTTP 請求標頭，用於指示請求的來源網域名稱。Origin 標頭包含通訊協定，網域名稱和連接埠，不包含路徑與查詢字串。連接埠號是可選的。

<span id="origin-存取限制"></span>
## Origin 存取限制

Origin 標頭的作用之一是防止盜連。您可以為您的網站設定一個 Origin 封鎖清單以拒絕來自指定網域名稱的請求。或者您可以為您的網站設定一個 Origin 允許清單只允許接受來自指定網域名稱的請求。

<span id="空-origin"></span>
### **空 Origin**

"空 Origin" 的定義是 Origin 標頭沒有值或者請求中不包含 Origin 標頭。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>Origin: null</code> 不被視為是 "空 Origin" 情況。</div>


<span id="操作步驟"></span>
## 操作步驟


1. 打開 **Origin 存取限制** 設定頁面。操作步驟參見 [網域名稱設定](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-tw)。

2. 在 **Origin 存取限制** 下方，設定 **狀態** 為 **開啟**。

3. 參照以下設定說明。

4. 設定完成後，點擊 **儲存**。



|**設定** |**說明** |
|---|---|
|類型 |該設定有以下選項：<br><br>&nbsp;<br><br>\* **允許清單**：當您只想允許來自某些網域名稱的請求時，可以設定一個允許清單。如果使用者的請求不匹配允許清單，CDN 拒絕請求並且回應 403 狀態碼<br><br>&nbsp;<br><br>\* **封鎖清單**：當您只想阻止來自某些網域名稱的請求時，可以設定一個封鎖清單。如果使用者的請求匹配了封鎖清單，CDN 拒絕請求並且回應 403 狀態碼。 |
|來源伺服器 |輸入一個或者多個 Origin 條目。名單的長度不能超過 30,000 個字元。您可以輸入一個或者多個網域名稱（支援子網域和萬用字元網域）和 IP 位址（支援 IPv4 位址、IPv6 位址、CIDR 網段）。多個條目使用分號（;）或換行符分隔。您最多可以輸入 100 個條目。需要注意的是，二級網域被認為是單個網域名稱，不是萬用字元網域。萬用字元網域不包含二級網域本身。例如：`*.test.com` 不包含二級網域 `test.com`，但是包含 `www.test.com`、`a.a.test.com` 等。<br><br>&nbsp;<br><br>子網域的級別數量沒有限制。關於 Origin 名單的匹配邏輯，參見 [Origin 匹配邏輯](https://docs.byteplus.com/en/docs/18/36279#origin-%E5%8C%B9%E9%85%8D%E9%82%8F%E8%BC%AF)。 |
|空 Origin 存取 CDN 資源 |表示在 [空 Origin](https://docs.byteplus.com/en/docs/18/36279#%E7%A9%BA-origin) 情境下，CDN 處理請求的方式。<br><br><br>* 如果 **類型** 是 **封鎖清單** ，該選項是 **允許空 Origin 存取 CDN 資源**。<br><br>* 如果 **類型** 是 **允許清單** ，該選項是 **不允許空 Origin 存取 CDN 資源**。 |
|忽略大小寫 |表示 Origin 在用於過濾請求時是否區分大小寫。 |


<span id="origin-匹配邏輯"></span>
## Origin 匹配邏輯

我們透過以下名單配置為例，闡述 Origin 標頭的匹配邏輯。如果一個請求未匹配允許清單或者匹配了封鎖清單，CDN 會拒絕請求並返回 403 回應狀態碼。


|**名單配置** |**使用者請求中 Origin 標頭** |**匹配？**  |**匹配邏輯說明** |
|---|---|---|---|
|* www.test.com<br><br>* 1.1.1.1<br><br>* 2001:0db8:3c4d:0015:0000:0000:1a2f:1a2b<br><br>* \*.test.com |http://www.test.com |是 |Origin 標頭中的網域名稱匹配名單。 |
||http://www.test.com:80 |是 ||
||www.test.com |否 |Origin 標頭不符合 HTTP 協議規範。規範要求 Origin 標頭值必須是以下格式之一：<br><br><br>* scheme://host:port<br><br>* scheme://host |
||2001:0db8:3c4d:0015:0000:0000:1a2f:1a2b |否 ||
||http://2001:0db8:3c4d:0015:0000:0000:1a2f:1a2b |否 |Origin 標頭不符合 HTTP 協議規範。規範要求當 host 是一個 IPv6 地址時，該地址必須包裹在 `[]` 中。 |
||http://[2001:0db8:3c4d:0015:0000:0000:1a2f:1a2b] |是 |Origin 標頭中的 IP 地址匹配名單。 |
||http://aaa.test.com |是 |Origin 標頭中的多級網域名稱匹配名單中的泛網域名稱條目。 |
||http://ss.aaa.test.com |是 ||
||http://test.com |否 |Origin 標頭中的二級網域名稱不匹配名單中的泛網域名稱條目。原因是泛網域名稱不包含二級網域名稱本身。 |
