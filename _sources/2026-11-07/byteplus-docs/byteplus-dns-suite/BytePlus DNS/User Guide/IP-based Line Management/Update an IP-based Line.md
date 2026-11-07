---
title: "Update an IP-based Line"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/docs-updating-an-ip-based-line"
---

You can update the name, comments, or CIDR block of an IP\-based line in BytePlus DNS.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Think carefully before updating the CIDR block of an IP\-based line. If you update the CIDR block of a specific IP\-based line, all DNS records using that IP\-based line in BytePlus DNS will be affected. This operation cannot be undone.</div>


<span id="35c4bd2c"></span>
## Steps

You can follow these steps to update an IP\-based line.


1. Open the [IP-based lines](https://console.byteplus.com/dns-suite/dns/lines) page in the BytePlus DNS console.

2. Find the IP\-based line that you want to modify. Click **Edit** in the **Actions** column.

3. Update the parameters on the **Create line** page.

4. Click **OK**.

   * If there are no DNS records using the IP\-based line in BytePlus DNS, the updated IP\-based line will be displayed in the list.

   * If there are DNS records using the IP\-based line in BytePlus DNS, a confirmation window will pop up, listing all the DNS records using that IP\-based line. You need to confirm whether the updated IP\-based line will have any unexpected impact on the DNS records using it. If the impact is as expected, you can click **OK**. The updated IP\-based line will be displayed in the list.
