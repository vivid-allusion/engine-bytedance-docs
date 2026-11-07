---
title: "Domain transfer-in"
product: "BytePlus Domain Names"
product_code: "domain-names"
source: "https://docs.byteplus.com/en/docs/domain-names/domain-transfer-in_en"
---

This document introduces how to transfer a domain to BytePlus Domains.

<span id="overview"></span>
## Overview

If your domain is not managed by BytePlus Domains, for example, if your domain is managed by GoDaddy, but you want BytePlus Domains to manage your domain, you can transfer the domain to BytePlus Domains.

Domains managed by BytePlus are registered with Domainipr. BytePlus has an account under Domainipr, and these domains belong to that account. If you need to transfer domains from another Domainipr account to BytePlus, please [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001150).

<span id="transfer-process"></span>
## Transfer Process


1. Submit a transfer\-out request with the original registrar to obtain the authorization code.

2. Submit a domain transfer\-in request in BytePlus Domains.

3. Wait for the transfer process to complete.


You can transfer up to 10 domains at a time.

<span id="transfer-lock"></span>
## Transfer Lock

After a domain is transferred to BytePlus, you can transfer it out from BytePlus at any time. BytePlus provides a transfer lock, which prevents the domain from being transferred out of BytePlus within 60 days after the transfer. The transfer lock can protect your domain from being accidentally or maliciously transferred out. When submitting a domain transfer\-in request, you can specify whether to enable the transfer lock for the domain.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If a domain is transferred from an account under Domainipr to BytePlus Domains, the transfer lock is enabled by default after the domain is transferred.</div>


<span id="transfer-fees"></span>
## Transfer Fees

According to domain registry regulations, domains must be renewed for 1 year during transfer and redemption (.ai domains require 2 years of renewal). Therefore,


* For .ai domains: Transfer fees include 2 years of renewal.

* For other domain suffixes: Transfer fees include 1 year of renewal.


For information about domain transfer pricing, see [Pricing](https://docs.byteplus.com/en/docs/domain-names/pricing_en).

If you plan to transfer your domain to BytePlus, but the domain has expired and was just renewed, it is recommended to wait 45 days from the renewal date before transferring the domain to BytePlus. Otherwise, after the transfer, your renewal with the former registrar will become invalid, and only the renewal during the transfer to BytePlus will take effect, resulting in the waste of one renewal fee. Please consult the former registrar regarding refund matters.

<span id="transfer-duration"></span>
## Transfer Duration

Domain transfer usually takes 5\-7 days to complete. The actual time required depends on the following factors:


* The time required by the original registrar to confirm the domain transfer\-out.

* The time required by the registry to complete the transfer review.


<span id="dns-resolution-of-the-domain"></span>
## DNS Resolution of the Domain

After a domain is transferred to BytePlus Domains, the registrant will be changed to the registrant specified in the registrant profile you selected when initiating the transfer. However, the domain's Nameservers (DNS servers) remain unchanged. Therefore, the DNS resolution administrator will not change. Once the domain transfer is complete, you can modify the domain's Nameservers as needed. Please note that before changing the Nameservers, you need to manually migrate the DNS resolution.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Before transferring your domain to BytePlus Domains, if you are using the DNS resolution service provided by the original domain registrar, please confirm with them whether the domain transfer will affect your continued use of their DNS resolution service. If there is any impact, we recommend manually migrating your domain resolution to BytePlus DNS service before you initiate the transfer.</div>


* <div data-tips="true" data-tips-type="tip">We recommend updating your Nameservers to the Nameservers of BytePlus DNS service, so you can manage your domain resolution in BytePlus DNS service. The Nameservers for DNS service are <code>ns1.byteplusdns.com</code> and <code>ns2.byteplusdns.net</code>. For information about migrating domain resolution, see <a href="https://docs.byteplus.com/en/docs/byteplus-dns-suite/docs-transferring-dns-service-to-byteplus-dns">Transfer DNS Service to BytePlus DNS</a>.</div>



<span id="prerequisites-for-transfer"></span>
## Prerequisites for Transfer


* You have created a [registrant profile](https://docs.byteplus.com/en/docs/domain-names/registrant-profile_en) in BytePlus Domains. You need to specify this registrant profile when submitting a domain transfer\-in request.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you are transferring a <strong>.hk</strong> or <strong>.com.hk</strong> domain, you must select a registrant profile that has the required identification information configured under <strong>Required information for other ccTLDs </strong>in <a href="https://docs.byteplus.com/en/docs/domain-names/registrant-profile_en#steps">Registrant profile</a>.   </div>
   

* You have obtained the authorization code from the original registrar of the domain.

* The domain has been registered for more than 60 days.

* The domain is not a [premium domain](https://docs.byteplus.com/en/docs/domain-names/introduction_en).

* In the [WHOIS lookup](https://docs.byteplus.com/en/docs/domain-names/whois_en) results, the status of the domain is not `ClientTransferProhibited`, `ServerTransferProhibited`, or `pendingTransfer`.

   * ClientTransferProhibited indicates that the domain registrar prohibits the domain from being transferred out.

   * ServerTransferProhibited indicates that the domain registry prohibits the transfer operation of the domain.

   * pendingTransfer indicates that the domain is being transferred.

* The suffix of the domain must be supported by BytePlus. You can check the list of supported suffixes on the [Domain Registration](https://console.byteplus.com/domain-service/search) page.


<span id="steps"></span>
## Steps


1. Visit [BytePlus Domains](https://console.byteplus.com/domain-service/search).

2. In the left navigation bar, click **Domain transfer\-In**.

3. On the **Domain transfer\-In** page, click **Transfer domains**.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_7f5440575690dc2bbb32c6c3d7bc31b1.png) </span>

4. On the page, enter the domains to be transferred in the following format, then click **Next**.

   * `<domain> <authorization code>`

   There is a space between `<domain>` and `<authorization code>`. If you want to transfer multiple domains, enter each domain on a new line. You can enter up to 10 domains at a time.

5. On the transfer configuration page, specify the following configurations:

   * **Registrant profile**: Select a registrant profile that contains the registrant information of the domain.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If you are transferring a <strong>.hk</strong> or <strong>.com.hk</strong> domain, you must select a registrant profile that has the required identification information configured under <strong>Required information for other ccTLDs </strong>in <a href="https://docs.byteplus.com/en/docs/domain-names/registrant-profile_en#steps">Registrant profile</a>. If the selected profile has not been configured for these specific suffixes, you will be prompted to create or update a profile before proceeding with the transfer.      </div>
      

   * **Auto\-renew**: Specify whether to enable auto\-renew for the domain. This option is unchecked by default, meaning auto\-renew is not enabled. If you check this option, BytePlus Domains will renew your domain for 1 year 15 days before the domain expires. The renewal period for domains with the .ai suffix is 2 years.

   * **Waive 60\-day transfer lock**: This option indicates whether to disable the [transfer lock](https://docs.byteplus.com/en/docs/171/36434#transfer-lock). This option is selected by default, indicating that the transfer lock is disabled.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_72e3ef49b1974711e929f8d857bbe6c1.png) </span>

6. Check the agreement, then click **Submit**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Regarding the price at the bottom left of the page, see <a href="https://docs.byteplus.com/en/docs/171/36434#transfer-fees">Transfer Fees</a>.   </div>
   

7. Complete the payment as instructed on the page.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The prices displayed on the order page in the console are pre\-tax prices. For tax rates in various countries and regions, please refer to the <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-tax-rate-reference">Tax rate reference</a>.   </div>
