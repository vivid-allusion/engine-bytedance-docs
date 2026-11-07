---
title: "Create an Alias record pointing to a CNAME of BytePlus CDN"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/create_alias_record"
---

This document describes how to create an Alias record pointing to a CNAME of BytePlus CDN.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Alias records are currently available only through a allowlist. Please <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001151">submit a support ticket</a>.</div>


<span id="steps"></span>
## Steps

Follow these steps to learn how to create an Alias record pointing to a CNAME of BytePlus CDN.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_2bb8bff0409dcf4fa048f53ebe2627af.jpeg) </span>

<span id="step-1-get-your-domain-name-from-byteplus-cdn"></span>
### Step 1: Get your domain name from BytePlus CDN

Before creating an Alias record, you need to get your domain name from BytePlus CDN. Refer to BytePlus CDN's [Quick Start](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-overview_1) to learn how to get your domain name.

<span id="step-2-add-the-domain-from-byteplus-cdn-to-byteplus-dns"></span>
### Step 2: Add the domain from BytePlus CDN to BytePlus DNS

After getting your domain name from BytePlus CDN, you need to add it to BytePlus DNS to manage the DNS resolution of the domain. The domain can be a second\-level domain (root domain) or a delegated subdomain. Refer to [Create a domain](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-creating-a-domain-na) to learn how to add your domain in BytePlus DNS.

<span id="step-3-create-an-alias-record-for-your-domain-in-byteplus-dns"></span>
### Step 3: Create an Alias record for your domain in BytePlus DNS

Follow these steps to create an Alias record for your domain in BytePlus DNS.


1. Open the [BytePlus DNS console](https://console.byteplus.com/dns-suite/dns).

2. On the **Domain management** page, click your domain in the **Domain** column.

3. On the **Record management** tab, click **Create record set**. On the **Create record set** page, configure the settings according to the table below.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The value of the <strong>TTL</strong> parameter is fixed at <strong>10 minutes</strong> and cannot be modified.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The value of the <strong>Line</strong> parameter is fixed at <strong>Default line</strong> and cannot be modified.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The value of the <strong>Load balancing</strong> parameter is fixed at <strong>Disabled</strong> and cannot be modified.   </div>
   

   
   |Configuration |Description |
   |---|---|
   |Domain name |The domain prefix of the subdomain. For example, assuming your domain is `example.com`:<br><br><br>* If your domain from BytePlus CDN is `www.example.com`, you need to set the domain prefix to `www`.<br><br>* If your domain from BytePlus CDN is `example.com`, you need to set the domain prefix to `@`. |
   |Record type |Select a record type. You can only select **A** or **AAAA**. |
   |Alias |Whether to set the enabled record in this record set as an Alias record. Enable this parameter so that you can create an Alias record.<br><br><br>* **Enable**: Sets the enabled record in this record set as an Alias record.<br><br>* **Disable**: Does not set the enabled record in this record set as an Alias record.<br><br><br>If it is the first time you create an Alias record, you will be prompted to create and authorize the service\-linked role ServiceRoleForDNS to BytePlus DNS. This role allows BytePlus DNS to query the CNAME corresponding to the domain from BytePlus CDN. |
   |Record value |Click **Create record value**, then select a CNAME from BytePlus CDN.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">For Alias records, only one record value can be enabled in a record set.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The CNAME must match your domain from BytePlus CDN. For example, if your domain from BytePlus CDN is <code>www.example.com</code>, the CNAME is <code>www.example.com.bplslb.com</code>.</div><br> |
   |Enable |Whether to enable this record value.<br><br><br>* **Enable**: This record value is included in DNS responses.<br><br>* **Disable**: This record value will not be included in DNS responses. |
   |Remarks |Remarks for the record value. Supports UTF\-8 encoding. |
   

4. After completing the settings, click **Submit**. In the **Record management** section, you can see the Alias record you have created in the record set list.


<span id="step-4-verify-whether-the-alias-record-is-active"></span>
### Step 4: Verify whether the Alias record is active

You can use the dig or nslookup command to verify if the Alias record is active. Taking the dig command as an example, assume your domain in BytePlus CDN is `www.example.com`, you can get the IPv4 or IPv6 address of your domain by the following commands.

```Shell
# Gets the IPv4 address
dig www.example.com A

# Gets the IPv6 address
dig www.example.com AAAA
```


You can use BytePlus CDN's [IP detection tool](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-diagnostic-tools) to verify whether the IP address in the DNS response is a BytePlus CDN node IP address. If it is, it indicates that the Alias record you created is active.
