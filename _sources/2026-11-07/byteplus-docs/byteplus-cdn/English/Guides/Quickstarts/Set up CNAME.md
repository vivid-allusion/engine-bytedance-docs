---
title: "Set up CNAME"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-set-up-cname"
---

To connect your site to BytePlus CDN, you need to configure a CNAME record with your DNS provider.

This guide provides step\-by\-step instructions for popular providers like BytePlus DNS Suite and GoDaddy, and shows you how to verify that the configuration is effective.

To connect your site to the Content Distribution Network, you need to configure a CNAME record with your DNS provider. The record name is `www`, and the record value is `www.example.com.bplslb.com`. Different domain service providers have different configuration interfaces. This guide provides instructions for BytePlus DNS Suite and GoDaddy.


* [BytePlus DNS Suite](https://docs.byteplus.com/en/docs/18/6545#byteplus-dns-suite)

* [GoDaddy](https://docs.byteplus.com/en/docs/18/6545#godaddy)


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">DNS provider interfaces are subject to change. Refer to your provider's current interface if it differs from the examples in this guide.</div>


* <div data-tips="true" data-tips-type="tip">After you complete the CNAME configuration, verify that the record has taken effect. See <a href="https://docs.byteplus.com/en/docs/18/6545#verifying-the-cname-record">Verifying the CNAME record</a>.</div>



<span id="byteplus-dns-suite"></span>
## BytePlus DNS Suite


1. Log in to the [BytePlus DNS Suite Console](https://console.byteplus.com/dns-suite/dns/publiczone/zones).

2. On the **Domain management** page, find the domain `example.com` in the domain list.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3eab5b722afa4136b5f584c3e7d40b77~tplv-goo7wpa0wc-image.image) </span>

3. In the **Operation** column, click **Manage**.

4. In the **Record management** tab, click **Create record set**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de120a8606d544828808daf656dd3ef2~tplv-goo7wpa0wc-image.image) </span>

5. On the **Create record set** page, configure the CNAME record according to the screenshot below.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_9493a59303e3414db75530f40e7cf34c.png) </span>

6. After configuration, click **Submit**.


<span id="godaddy"></span>
## GoDaddy


1. Open [GoDaddy's My Products page](https://account.godaddy.com/products) and log in.

2. Under **Domains**, find the domain name **example.com** and click **DNS**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bfa5845daef0412e96267c778c27d023~tplv-goo7wpa0wc-image.image) </span>

3. On the **DNS Management** page, click **Add New Record**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c5159b53e6844d1786fda6958d050c9d~tplv-goo7wpa0wc-image.image) </span>

4. Configure the CNAME record as shown in the screenshot below.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ebeda555ac1948d29dd0109c1a0092b1~tplv-goo7wpa0wc-image.image) </span>

5. After configuration, click **Save**.


<span id="verifying-the-cname-record"></span>
## Verifying the CNAME Record

After setting up the CNAME record with your DNS provider, wait for about 3 minutes, then use one of the following methods to verify that the record has taken effect.

<span id="method-1-check-the-status-of-the-cname-record-in-the-cdn-console"></span>
### Method 1: Check the Status of the CNAME Record in the CDN Console

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If your DNS provider allows you to configure records for specific carriers or regions (dimensional routing), Method 1 might not show the correct status. In this case, use <a href="https://docs.byteplus.com/en/docs/18/6545#method-2-check-the-cname-status-using-command-line-tools">Method 2</a>.</div>


An orange exclamation mark next to the CNAME indicates that the record has not yet taken effect. If you see this, verify that your CNAME configuration with your DNS provider is correct.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5b63734388804c5799b4f05ec247411f~tplv-goo7wpa0wc-image.image) </span>

A green exclamation mark next to the CNAME indicates that the record has taken effect.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bdbf36f190c84593af7111f27fbc1cdc~tplv-goo7wpa0wc-image.image) </span>

<span id="method-2-check-the-cname-status-using-command-line-tools"></span>
### Method 2: Check the CNAME Status Using Command\-Line Tools

Depending on your operating system, follow the steps below.

<span id="macos-and-linux"></span>
#### macOS and Linux


1. In a Terminal window, run the command `dig www.example.com`.

2. In the ANSWER SECTION of the output, if you see a response similar to the following, it indicates the CNAME record has taken effect.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/02ff456e965346898264764b51476c48~tplv-goo7wpa0wc-image.image) </span>


<span id="windows"></span>
#### Windows


1. In a **Command Prompt** window, run the command `nslookup www.example.com`.

2. In the information below the command, if the following information appears, it indicates that your configured CNAME is effective.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a5f3ec2e12c648efabe5969842cce83a~tplv-goo7wpa0wc-image.image) </span>
