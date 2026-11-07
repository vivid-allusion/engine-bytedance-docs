---
title: "设置 CNAME"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-set-up-cname-cn"
---

本文档介绍如何配置 CNAME 记录将您的站点连接到 BytePlus CDN。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">该文档是基于 <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-overview_1-cn">教程介绍</a> 中描述的场景。</div>


要将您的站点连接到 CDN，您需要在您的 DNS 服务商处配置一条 CNAME 记录。记录名是 `www`，记录值是 `www.example.com.bplslb.com`。不同的域名服务商的配置界面不同。下面介绍主要在 BytePlus DNS Suite 和 GoDaddy 中的配置方法。


* [BytePlus DNS Suite](https://docs.byteplus.com/en/docs/18/6915#byteplus-dns-suite)

* [GoDaddy](https://docs.byteplus.com/en/docs/18/6915#godaddy)


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">DNS 服务商的界面可能会有变化，请以实际界面为准。</div>


* <div data-tips="true" data-tips-type="tip">完成 CNAME 配置后，<a href="https://docs.byteplus.com/en/docs/18/6915#%E9%AA%8C%E8%AF%81-cname-%E8%AE%B0%E5%BD%95%E6%98%AF%E5%90%A6%E7%94%9F%E6%95%88">验证 CNAME 配置</a> 是否生效。</div>



<span id="byteplus-dns-suite"></span>
## BytePlus DNS Suite


1. 登录 [BytePlus DNS Suite 控制台](https://console.byteplus.com/dns-suite/dns/publiczone/zones)。

2. 在 **Domain management** 页面的域名列表中，找到 `example.com` 域名。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3eab5b722afa4136b5f584c3e7d40b77~tplv-goo7wpa0wc-image.image) </span>

3. 在 **Operation** 列上，点击 **Manage**。

4. 在 **Record management** 标签页，点击 **Create record set**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de120a8606d544828808daf656dd3ef2~tplv-goo7wpa0wc-image.image) </span>

5. 在 **Create record set** 页面，按照以下截图配置 CNAME 记录。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_0b74d48566aded21203c7657baec0745.png) </span>

6. 配置完成后，点击 **Submit**。


<span id="godaddy"></span>
## GoDaddy


1. 打开 [GoDaddy 站点的 My Products 页面](https://account.godaddy.com/products) 并登录。

2. 在 **Domains** 下方，找到 **example.com** 域名，然后点击 **DNS**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bfa5845daef0412e96267c778c27d023~tplv-goo7wpa0wc-image.image) </span>

3. 在 **DNS Management** 页面，点击 **Add New Record**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c5159b53e6844d1786fda6958d050c9d~tplv-goo7wpa0wc-image.image) </span>

4. 按照以下截图配置 CNAME 记录。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ebeda555ac1948d29dd0109c1a0092b1~tplv-goo7wpa0wc-image.image) </span>

5. 配置完成后，点击 **Save**。


<span id="验证-cname-记录是否生效"></span>
## 验证 CNAME 记录是否生效

在 DNS 服务商处设置 CNAME 记录后，请等待 3 分钟，然后使用以下任一方法验证您配置的 CNAME 记录是否生效。

<span id="方法一：在-cdn-控制台中查看-cname-记录的状态"></span>
### 方法一：在 CDN 控制台中查看 CNAME 记录的状态

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">如果您的 DNS 服务商支持基于运营商线路，地区等维度设置 DNS 记录，并且您配置的 CNAME 记录是基于某个维度，那么方法一可能无法使您获取 CNAME 记录的实际状态。建议您使用方法二。</div>


重新打开或者刷新 [域名接入](https://console.byteplus.com/cdn/cdn-bp/delivery-network/domain-access) 页面。如果 CNAME 前是一个橙色的感叹号，表示您配置的 CNAME 记录还未生效。请检查您在 DNS 服务商处配置的 CNAME 记录是否正确。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9e01ced5b5624dde9d9ae863a00c6b2b~tplv-goo7wpa0wc-image.image) </span>

如果 CNAME 前是一个绿色的感叹号，表示您配置的 CNAME 记录已生效。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d155484ec4c8418e8e4f721026d6dd3a~tplv-goo7wpa0wc-image.image) </span>

<span id="方法二：使用命令行工具查看-cname-记录的状态"></span>
### 方法二：使用命令行工具查看 CNAME 记录的状态

根据您使用的操作系统，参考以下步骤。

<span id="macos-和-linux"></span>
#### macOS 和 Linux


1. 在一个 Terminal 窗口中，运行命令 `dig www.example.com`。

2. 在 **ANSWER SECTION** 下方，如果出现以下信息，则表示您配置的 CNAME 已生效。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/02ff456e965346898264764b51476c48~tplv-goo7wpa0wc-image.image) </span>


<span id="windows"></span>
#### Windows


1. 在一个 **命令提示符** 窗口中，运行命令 `nslookup www.example.com`。

2. 在命令下方的信息中，如果出现以下信息，则表示您配置的 CNAME 已生效。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a5f3ec2e12c648efabe5969842cce83a~tplv-goo7wpa0wc-image.image) </span>
