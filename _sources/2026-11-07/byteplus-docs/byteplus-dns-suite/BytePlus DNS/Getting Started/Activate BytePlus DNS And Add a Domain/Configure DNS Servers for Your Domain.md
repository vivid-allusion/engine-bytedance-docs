---
title: "Configure DNS Servers for Your Domain"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/docs-adding-dns-servers-to-your-domain-s-registrar"
---

If your domain is registered with a third\-party domain registrar, you need to configure DNS servers for your domain.

At the third\-party domain registrar, the DNS servers for your domain must be BytePlus DNS's DNS servers. Otherwise, BytePlus DNS cannot provide authoritative DNS service for your domain.

<span id="steps"></span>
## Steps

Follow the steps below to configure DNS servers for your domain.


1. Open the [BytePlus DNS Console](https://console.byteplus.com/TrafficRoute/dns/public-zone).

2. On the **Domain management** page, find your domain.

3. In the **Domain** column, click your domain.

4. On the **Domain management** page, click the **Instance information** tab. You will see the DNS servers under **DNS information**.

5. At your domain registrar, add all BytePlus DNS's DNS servers to the DNS server list of your domain. Ensure that this list only contains BytePlus DNS's DNS servers.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Refer to the documentation of domain registrars to learn how to use BytePlus's DNS servers (name servers) for your domain. Some of the documentation links are listed below:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><a href="https://ca.godaddy.com/help/edit-my-domain-nameservers-664">Godaddy</a>   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><a href="https://www.ionos.com/help/domains/using-your-own-name-servers/using-your-own-name-servers-for-a-domain/">IONOS</a>   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><a href="https://www.namecheap.com/support/knowledgebase/article.aspx/767/10/how-to-change-dns-for-a-domain/">Namecheap</a>   </div>
   


After you configure the DNS servers, if the **DNS status** of your domain is **Active** in the BytePlus DNS console, it indicates that BytePlus DNS is providing authoritative DNS service for your domain.
