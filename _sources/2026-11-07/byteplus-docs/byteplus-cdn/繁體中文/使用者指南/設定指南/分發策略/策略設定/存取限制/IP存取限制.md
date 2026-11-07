---
title: "IP存取限制"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ip-restriction_zh-tw"
---

本文件介紹如何在 BytePlus CDN 中設定 IP 封鎖/允許清單。

您可以設定 IP 封鎖清單或者允許清單，基於用戶端 IP 對請求進行過濾。

<span id="功能優先級"></span>
## 功能優先級

CDN 提供的一系列存取控制功能有不同的優先級。在 CDN 處理使用者請求時，這些功能按優先級對請求生效。參見 [存取限制功能的優先順序](https://docs.byteplus.com/en/docs/byteplus-cdn/access-restrictions-priority_zh-tw)。

<span id="操作步驟"></span>
## 操作步驟


1. 打開 **IP存取限制** 設定頁面。操作步驟參見 [網域名稱設定](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-tw)。

2. 設定 **狀態** 為開啟。

3. 參照以下 [設定說明](https://docs.byteplus.com/en/docs/18/36276#%E8%A8%AD%E5%AE%9A%E8%AA%AA%E6%98%8E)。

4. 設定完成後，點擊 **儲存**。


<span id="設定說明"></span>
## 設定說明


|設定 |說明 |
|---|---|
|類型 |該設定的可選值如下：<br><br><br>* **允許清單**：指定來自哪些 IP 位址的請求允許存取您的網域名稱。當您只想 CDN 允許來自某些 IP 的請求時，可以設定允許清單。<br><br>* **封鎖清單**：指定來自哪些 IP 位址的請求不允許存取您的網域名稱。當您只想 CDN 阻止來自某些 IP 的請求時，可以設定封鎖清單。<br><br><br>如果一個請求的來源 IP 匹配了封鎖清單或者沒有匹配允許清單，CDN 會拒絕該請求並返回 403 回應狀態碼。 |
|設定方式 |表示名單中條目的來源。該設定有以下選項：<br><br><br>* 策略設定：表示名單中的條目是在 **規則內容** 中設定的。<br><br>* 全域設定：表示名單中的條目來自一個 [全域設定](https://docs.byteplus.com/en/docs/byteplus-cdn/universal-catalog_zh-tw)。全域設定用來定義大量條目的。一個全域設定最多可以包含 30,000 個條目。 |
|規則內容 |表示 **類型** 對應的 IP 位址條目，最多包含 1,000 個條目，總長度不超過 30,000 個字元。當 **設定方式** 是 **策略設定** 時，該設定會出現。<br><br>&nbsp;<br><br>每個條目可以是一個 IP 位址、一個 CIDR 網段或者一個 IP 位址範圍。IP 位址的格式可以是 IPv4 或者 IPv6。每個條目需要分行輸入。IPv6 位址不區分大小寫。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">如果您需要輸入的 IP 位址數量超過 1,000，參考 <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/universal-catalog_zh-tw">全域設定</a>。</div><br> |


<span id="設定示例"></span>
## 設定示例

**允許清單**

規則：

> 192.0.2.0/24

> 203.0.113.8\-203.0.113.15

> 2001:DB8::1


作用：僅允許滿足以下任一條件的 IP 位址向您的網域名稱發送請求：


* IP 位址是 2001:DB8::1

* IP 位址在 192.0.2.1\-192.0.2.254、203.0.113.8\-203.0.113.15 範圍內。


**封鎖清單**

規則

> 2001:DB8::/126

> 198.51.100.25


作用：如果 IP 位址滿足以下任一條件，則不允許來自該 IP 位址的請求。


* IP 位址是 198.51.100.25。

* IP 位址在 2001:DB8:: 與 2001:DB8::0003 範圍內。
