---
title: "IPv6來源伺服器請求"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/origin_ip_preference_cn_tw"
---

本文件介紹 BytePlus CDN 中的 "IPv6來源伺服器請求" 功能。

<span id="概述"></span>
## 概述

IPv6 是網路層中 IP 協定的最新版本，具有比 IPv4 大得多的位址空間，以及一些其他優勢。

對於網域名稱類型的來源伺服器，當 CDN 向來源伺服器請求內容時，會首先透過 DNS 解析取得來源伺服器網域名稱的 IP 位址。 預設情況下，CDN 會嘗試取得與使用者請求相同類型的 IP 位址。也就是說：


* 假設使用者請求使用的是 IPv6 位址。在這個情況下，CDN 會嘗試取得來源伺服器網域名稱的 IPv6 位址。如果無法取得該 IP 位址，CDN 才嘗試取得來源伺服器網域名稱的 IPv4 位址。


如果您希望 CDN 在 DNS 解析時優先取得指定類型的 IP 位址，可以設定 "IPv6來源伺服器請求" 功能。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">該功能不適用於 IP 位址類型的來源伺服器。</div>


* <div data-tips="true" data-tips-type="tip">要使使用者請求存取 CDN 的 IPv6 位址，您需要先在網域名稱的設定中 <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/ipv6_zh-tw">啟用 IPv6</a>。</div>



<span id="操作步驟"></span>
## 操作步驟

要對一個網域名稱開啟該設定，您需要在一個未發布的分發策略中進行設定，然後發布該策略並將其綁定該網域名稱。如果該網域名稱已綁定了一個策略，可以透過 [策略複製](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-policy_zh-tw#%E8%A4%87%E8%A3%BD%E7%AD%96%E7%95%A5) 建立一個未發布的策略。


1. 打開 **來源伺服器設定** 標籤頁。操作步驟參見 [網域名稱設定](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-tw)。

2. 在 **來源伺服器設定** 標籤頁的 **IPv6來源伺服器請求** 下方，根據以下 **來源伺服器請求** 的設定描述，選擇一個設定選項。

   * **協定跟隨**：表示 CDN 嘗試取得與使用者請求相同類型的 IP 位址。這是預設設定。

   * **IPv6 優先**：表示 CDN 始終嘗試取得來源伺服器網域名稱的 IPv6 位址。如果無法取得該 IP 位址，CDN 才嘗試取得來源伺服器網域名稱的 IPv4 位址。

   * **IPv4 優先**：表示 CDN 始終嘗試取得來源伺服器網域名稱的 IPv4 位址。如果無法取得該 IP 位址，CDN 才嘗試取得來源伺服器網域名稱的 IPv6 位址。

3. 修改完成後，在頁面右下方，點擊 **儲存**。
