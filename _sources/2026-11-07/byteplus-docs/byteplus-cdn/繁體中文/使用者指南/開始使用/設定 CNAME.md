---
title: "設定 CNAME"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-set-up-cname_zh-tw"
---

本文檔介紹如何配置 CNAME 記錄將您的網站連接到 BytePlus CDN。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">該文件是基於 <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/docs-overview_zh-tw">教學簡介</a> 中描述的場景。</div>


要將您的網站連接到 CDN，您需要在您的 DNS 服務商處配置一條 CNAME 記錄。記錄名是 `www`，記錄值是 `www.example.com.bplslb.com`。不同的網域名稱服務商的配置介面不同。下面介紹主要在 BytePlus DNS Suite 和 GoDady 中的配置方法。


* [BytePlus DNS Suite](https://docs.byteplus.com/en/docs/18/36119#byteplus-dns-suite)

* [GoDaddy](https://docs.byteplus.com/en/docs/18/36119#godaddy)


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">DNS 服務商的介面可能會有變化，請以實際介面為準。</div>


* <div data-tips="true" data-tips-type="tip">完成 CNAME 配置後，<a href="https://docs.byteplus.com/en/docs/18/36119#%E9%A9%97%E8%AD%89-cname-%E8%A8%98%E9%8C%84%E6%98%AF%E5%90%A6%E7%94%9F%E6%95%88">驗證 CNAME 配置</a> 是否生效。</div>



<span id="byteplus-dns-suite"></span>
## BytePlus DNS Suite


1. 登入 [BytePlus DNS Suite 控制台](https://console.byteplus.com/dns-suite/dns/publiczone/zones)。

2. 在 **Domain management** 頁面的網域名稱列表中，找到 `example.com` 網域名稱。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3eab5b722afa4136b5f584c3e7d40b77~tplv-goo7wpa0wc-image.image) </span>

3. 在 **Operation** 列上，點擊 **Manage**。

4. 在 **Record management** 標籤頁，點擊 **Create record set**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de120a8606d544828808daf656dd3ef2~tplv-goo7wpa0wc-image.image) </span>

5. 在 **Create record set** 頁面，按照以下截圖配置 CNAME 記錄。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_9493a59303e3414db75530f40e7cf34c.png) </span>

6. 配置完成後，點擊 **Submit**。


<span id="godaddy"></span>
## GoDaddy


1. 開啟 [GoDaddy 站點的 My Products 頁面](https://account.godaddy.com/products) 並登入。

2. 在 **Domains** 下方，找到 **example.com** 網域名稱，然後點擊 **DNS**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bfa5845daef0412e96267c778c27d023~tplv-goo7wpa0wc-image.image) </span>

3. 在 **DNS Management** 頁面，點擊 **Add New Record**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c5159b53e6844d1786fda6958d050c9d~tplv-goo7wpa0wc-image.image) </span>

4. 按照以下截圖配置 CNAME 記錄。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ebeda555ac1948d29dd0109c1a0092b1~tplv-goo7wpa0wc-image.image) </span>

5. 配置完成後，點擊 **Save**。


<span id="驗證-cname-記錄是否生效"></span>
## 驗證 CNAME 記錄是否生效

在 DNS 服務商處設置 CNAME 記錄後，請等待 3 分鐘，然後使用以下任一方法驗證您配置的 CNAME 記錄是否生效。

<span id="方法一：在-cdn-控制台中查看-cname-記錄的狀態"></span>
### 方法一：在 CDN 控制台中查看 CNAME 記錄的狀態

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">如果您的 DNS 服務商支援基於營運商線路，地區等維度設置 DNS 記錄，並且您配置的 CNAME 記錄是基於某個維度，那麼方法一可能無法使您獲取 CNAME 記錄的實際狀態。建議您使用方法二。</div>


重新開啟或者重新整理 [網域名稱](https://console.byteplus.com/cdn/cdn-bp/delivery-network/domain-access) 頁面。如果 CNAME 前是一個橙色的感嘆號，表示您配置的 CNAME 記錄還未生效。請檢查您在 DNS 服務商處配置的 CNAME 記錄是否正確。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_7ea8ebe97d9ae5820dda5bdf6cd59854.png) </span>

如果 CNAME 前是一個綠色的感嘆號，表示您配置的 CNAME 記錄已生效。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_0488b1cdbfc8224265d2d14a109d5137.png) </span>

<span id="方法二：使用命令列工具查看-cname-記錄的狀態"></span>
### 方法二：使用命令列工具查看 CNAME 記錄的狀態

根據您使用的作業系統，參考以下步驟。

<span id="macos-和-linux"></span>
#### macOS 和 Linux


1. 在一個 Terminal 視窗中，執行命令 `dig www.example.com`。

2. 在 **ANSWER SECTION** 下方，如果出現以下資訊，則表示您配置的 CNAME 已生效。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/02ff456e965346898264764b51476c48~tplv-goo7wpa0wc-image.image) </span>


<span id="windows"></span>
#### Windows


1. 在一個 **命令提示字元** 視窗中，執行命令 `nslookup www.example.com`。

2. 在命令下方的資訊中，如果出現以下資訊，則表示您配置的 CNAME 已生效。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a5f3ec2e12c648efabe5969842cce83a~tplv-goo7wpa0wc-image.image) </span>
