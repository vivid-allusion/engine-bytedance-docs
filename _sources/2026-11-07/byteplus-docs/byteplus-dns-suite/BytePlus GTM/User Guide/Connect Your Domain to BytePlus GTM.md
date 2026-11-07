---
title: "Connect Your Domain to BytePlus GTM"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/pHJ6zL"
---

This document introduces how to create a CNAME record to map your domain to the routing domain of your GTM instance.

If you select **CNAME** as the **Connection method** when creating your BytePlus GTM instance, you also need to create a CNAME record at your DNS service provider to map your domain to the CNAME of the GTM instance. Only in this way can BytePlus GTM route user requests visiting your domain.

Assume your domain is `www.example.com` and your GTM instance's CNAME is `www.example.com.byteplus.com`.

<span id="steps"></span>
## Steps

Refer to the steps below to create a CNAME record in BytePlus DNS to point your domain to the CNAME name of the GTM instance. This document takes Alibaba Cloud and Tencent DNSPod as an example.


<Tabs>
<Tab zoneid="UxUNciqpkO" title="Alibaba Cloud DNS">
<TabTitle>Alibaba Cloud DNS</TabTitle>

Follow these steps to create a CNAME record in Alibaba Cloud DNS, pointing your domain name to the routing domain of the GTM instance in this CNAME record.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the actual console UI interface changes, please refer to the updated interface.</div>



1. Log in to the [Alibaba Cloud DNS console](https://dns.console.aliyun.com/).

2. On the **Authoritative Domain Names** page, find your domain name **example.com**, and click **DNS Settings** in the **Actions** column.

3. Click **Add DNS Record**. On the **Add DNS Record** page, set **Record Type** to **CNAME**, set **Hostname** to `www`, and set **Record Value** to the routing domain `www.example.com.byteplus.com`. Click **OK**.


At this point, your domain name has been mapped to the routing domain of the GTM instance.


</Tab>
<Tab zoneid="ck7lnglBYW" title="Tencent Cloud DNSPod">
<TabTitle>Tencent Cloud DNSPod</TabTitle>

Follow these steps to create a CNAME record in Tencent Cloud DNSPod, pointing your domain name to the routing domain of the GTM instance in this CNAME record.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the actual console UI interface changes, please refer to the updated interface.</div>



1. Log in to the [Tencent Cloud DNSPod console](https://console.dnspod.cn/dns/list).

2. On the **My Domains** page, find your domain name **example.com**, then click on the domain to enter the **Record Management** page.

3. Click **Add Records**. Set **Type** to **CNAME**, set **Host** to `www`, and set **Value** to the routing domain `www.example.com.byteplus.com`. Click **OK**.


At this point, your domain name has been mapped to the routing domain of the GTM instance.


</Tab>
</Tabs>


<span id="verify-that-the-cname-record-is-active"></span>
## Verify that the CNAME record is active

Using the `nslookup` command as an example, open the command line window and run the following command:

```shell
nslookup www.example.com
```
