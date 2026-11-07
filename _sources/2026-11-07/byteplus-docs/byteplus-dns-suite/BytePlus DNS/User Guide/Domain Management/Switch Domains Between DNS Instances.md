---
title: "Switch Domains Between DNS Instances"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/Jdzr1i"
---

If a domain under your BytePlus account is enterprise edition or above, and you wish to change this domain to another domain associated with a free edition instance under your BytePlus account while retaining the current edition, you can change the domain in the BytePlus DNS console.

After the change, the new domain will inherit the edition and expiration date of the original domain. The original domain will still exist, but its edition will automatically be downgraded to free edition. Features that do not belong to the free edition will be disabled, and configurations exceeding free edition limits cannot be edited. For example, DNS backup will be disabled, and DNS records using cloud vendor lines cannot be edited.

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">If your original domain has DNSSEC enabled, you need to delete the DS record at your domain registrar before changing the domain, and then disable DNSSEC in BytePlus DNS. Otherwise, the original domain may not be resolved correctly.</div>


<span id="steps"></span>
## Steps

Follow the steps below to change the domain associated to your paid edition instance to the domain associated with the free edition instance under the same BytePlus account.


1. Open the [BytePlus DNS console](https://console.byteplus.com/dns-suite/dns).

2. On the **Domain management** page, find the domain associated with your paid edition instance. In the **Actions** column, click **Manage**.

3. Select the **Instance information** tab, and click **Switch domain** next to **Associated domain**.

4. On the **Switch domain** page, click the **Switch domain** dropdown and select the domain associated with the free edition instance that you need to change to. Click **Confirm**.
