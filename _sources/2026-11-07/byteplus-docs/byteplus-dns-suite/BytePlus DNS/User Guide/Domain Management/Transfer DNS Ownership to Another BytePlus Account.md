---
title: "Transfer DNS Ownership to Another BytePlus Account"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/M12cH9"
---

This document describes how to transfer DNS ownership and all DNS records of a domain from one BytePlus primary account to another without interrupting DNS resolution.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You can only transfer the DNS ownership of the root domain, not the subdomains hosted in BytePlus DNS.</div>


* <div data-tips="true" data-tips-type="tip">If both the root domain and its subdomains exist under one BytePlus primary account, the resolution of the subdomains will not be affected after the root domain is transferred.</div>



<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After the DNS ownership transfer is completed, the DNS records of the domain in the original BytePlus primary account will be cleared, and the domain status will change to <strong>DNS is managed by another account</strong>.</div>



* <div data-tips="true" data-tips-type="warning">If the domain's edition is free, the DNS ownership and DNS records will be transferred to another BytePlus primary account without changing the edition.</div>


* <div data-tips="true" data-tips-type="warning">If the domain's edition is paid, it will automatically downgrade to the free edition in the new BytePlus primary account after the transfer. This will result in:</div>


   * <div data-tips="true" data-tips-type="warning">The original paid edition's DNS record configurations (such as IP\-based lines) becoming unchangeable.</div>


   * <div data-tips="true" data-tips-type="warning">Features supported only by the paid edition (such as data backup) becoming unavailable.</div>



<div data-tips="true" data-tips-type="warning">Refer to <a href="https://docs.byteplus.com/docs/byteplus-dns-suite/docs-editions">Editions</a> for detailed information on feature changes after downgrading. If you want to continue using the features supported by the paid edition, you can upgrade the domain's edition in the current BytePlus primary account. Refer to <a href="https://docs.byteplus.com/docs/byteplus-dns-suite/docs-editions">Editions</a>.</div>


<span id="steps"></span>
## Steps

Follow the steps below to transfer the DNS ownership and all DNS records of a domain from the current BytePlus primary account to another BytePlus primary account.

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">If your domain has DNSSEC enabled, you need to delete the DS record at the original domain registrar and then disable DNSSEC in BytePlus DNS before transferring the domain resolution. Otherwise, the domain may not be resolved correctly after the transfer.</div>



1. Open the [BytePlus DNS console](https://console.byteplus.com/dns-suite/dns).

2. Find the domain you need to transfer and click **Manage** in the **Actions** column.

3. Select the **Instance information** tab. Click **Transfer to another account**.

4. On the **Transfer to another account** page, review the prompts and edition change information in the **Domain information** section. After confirming, set the following parameters in the **Transfer to another account** section:



|Parameter |Description |
|---|---|
|Account ID |The account ID of the other BytePlus primary account. |
|Account name |The account name of the other BytePlus primary account. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can find the account ID and account name on the <a href="https://console.byteplus.com/user/basics/">Basic information</a> page of the BytePlus console.</div>


<div data-tips="true" data-tips-type="tip"><img src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_c7b042f15d086ea154315796c781049d.jpeg" width="300px" /></div>


After setting, check **Confirm** and click **Submit**. If the transfer is successful, the DNS records of the domain in the current BytePlus primary account will be cleared, and the status will change to **DNS is managed by another account**.

<span id="verify-whether-the-dns-ownership-transfer-is-successful"></span>
## Verify whether the DNS ownership transfer is successful

Log in to the [BytePlus DNS console](https://console.byteplus.com/dns-suite/dns) using the other BytePlus primary account. If the transferred domain appears in the domain list and its status is **normal**, the DNS ownership has been successfully transferred to the new BytePlus primary account.
