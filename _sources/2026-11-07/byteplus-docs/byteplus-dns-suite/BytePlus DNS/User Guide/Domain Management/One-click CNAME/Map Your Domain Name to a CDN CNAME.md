---
title: "Map Your Domain Name to a CDN CNAME"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/Map_Your_Domain_Name_to_a_CDN_CNAME"
---

This document describes how to use the one\-click CNAME feature to map your domain name to the CDN CNAME.

<span id="steps"></span>
## Steps

Follow these steps to learn use the one\-click CNAME feature to map your domain name to the CDN CNAME.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_d89f68180db5e40e19ecc2e4d95b3a59.png) </span>

<span id="step-1-get-your-domain-name-from-byteplus-cdn"></span>
### Step 1: Get your domain name from BytePlus CDN

Before using the one\-click CNAME feature, you need to get your domain name from BytePlus CDN. Refer to BytePlus CDN's [Quick Start](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-overview_1) to learn how to get your domain name.

<span id="step-2-manage-your-cdn-domain-name-in-byteplus-dns"></span>
### Step 2: Manage your CDN domain name in BytePlus DNS

After getting your domain name from BytePlus CDN, you need to manage the domain name in BytePlus DNS.

You can directly add your CDN domain name or add the root domain of your CDN domain name. For example:


* Suppose your CDN domain names include `a.example.com` and `b.example.com`, you can add `example.com` in BytePlus DNS.

* Suppose your CDN domain name is `example.com`, you can directly add `example.com` in BytePlus DNS.


In BytePlus, the domain you add can be a second\-level domain (root domain) or a delegated subdomain. Refer to [Create a domain](https://docs.byteplus.com/docs/bxyteplus-dns-suite/docs-creating-a-domain-na) to learn how to add your domain in BytePlus DNS.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Ensure that the status of the domain you add in BytePlus is <strong>Active</strong> before you proceed to step 3.</div>


<span id="step-3-use-one-click-cname-to-map-your-domain-to-the-cname-of-byteplus-cdn"></span>
### Step 3: Use one\-click CNAME to map your domain to the CNAME of BytePlus CDN

Follow these steps to use one\-click CNAME to map your domain to the CNAME of BytePlus CDN.


1. Open the [BytePlus DNS console](https://console.byteplus.com/dns-suite/dns).

2. On the **Domain management** page, find your domain and click **One\-click CNAME** in the **Actions** column.

3. On the **One\-click CNAME** page, configure the settings according to the table below.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If it is the first time you use the one\-click CNAME feature, you will be prompted to create and authorize the service\-linked role ServiceRoleForDNS to BytePlus DNS. This role allows BytePlus DNS to query the CNAME corresponding to the domain from BytePlus CDN.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Some of the parameters cannot be modified:   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The value of the <strong>TTL</strong> parameter can only be <strong>10 minutes</strong> and cannot be modified.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The value of the <strong>Line</strong> parameter can only be <strong>Default line</strong> and cannot be modified.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The value of the <strong>Load balancing</strong> parameter can only be <strong>Enable</strong> and cannot be modified.   </div>
   

   
   |Configuration |Description |
   |---|---|
   |Domain name |Select a CDN domain name as the domain name of your CNAME record. BytePlus DNS displays CDN domains that are either subdomains of your domain name or are the same as your domain name.<br><br>&nbsp;<br><br>For example, suppose your CDN domain names include `a.example.com` and `b.example.com` and your domain name in BytePlus DNS is `example.com`. You can select `a.example.com` or `b.example.com` from **Domain name**. |
   |CNAME |Select a CDN CNAME as the value of your CNAME record. |
   

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_2edd08259aa25c1575999a54a9633556.png) </span>

4. Click **OK**. In the **Record management** section, you can see the CNAME record you have created in the record set list.


<span id="step-4-verify-whether-the-cname-record-is-active"></span>
### Step 4: Verify whether the CNAME record is active

You can use the dig or nslookup command to verify if the CNAME record is active. Taking the dig command as an example, assume your domain in BytePlus CDN is `www.example.com`, you can get the IP address of your domain by the following commands.

```Shell
dig www.example.com
```


You can use BytePlus CDN's [IP detection tool](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-diagnostic-tools) to verify whether the IP address in the DNS response is a BytePlus CDN node IP address. If it is, it indicates that the Alias record you created is active.
