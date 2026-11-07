---
title: "Others"
product: "BytePlus Domain Names"
product_code: "domain-names"
source: "https://docs.byteplus.com/en/docs/domain-names/others-faqs_en"
---

<span id="why-can-t-i-modify-the-dns-servers-of-the-domain"></span>
## Why can't I modify the DNS servers of the domain?

If the domain is being transferred or has the "Update Lock" enabled, you cannot modify the DNS servers of the domain. Please wait patiently for the domain transfer to complete, or disable the "Update Lock" before modifying the DNS servers.


* To determine if your domain is being transferred, perform a WHOIS lookup on the domain. In the lookup results, if the domain status is `pendingTransfer`, it indicates that the domain is being transferred.

* To determine if your domain has the "Update Lock" enabled, follow these steps:

   1. Visit [BytePlus Domains](https://console.byteplus.com/domain-service/search).

   2. In the left navigation bar, click **Domain list**.

   3. In the domain list, find your domain, and then click **Manage** in the **Actions** column.

   4. On the domain details page, check if the **Transfer lock** is enabled.

      <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_abd36a98caed436c02877395e38045bc.png) </span>


<span id="what-should-i-do-if-the-whois-lookup-shows-the-domain-status-as-serverhold-or-clienthold"></span>
## What should I do if the WHOIS lookup shows the domain status as serverHold or clientHold?


* `serverHold`: Indicates that domain resolution has been suspended by the registry.

* `clientHold`: Indicates that domain resolution has been suspended by the registrar.


Please [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001150) to inquire about the reason for the suspension of domain resolution.

For more information about domain statuses, see [WHOIS lookup](https://docs.byteplus.com/en/docs/domain-names/whois_en).
