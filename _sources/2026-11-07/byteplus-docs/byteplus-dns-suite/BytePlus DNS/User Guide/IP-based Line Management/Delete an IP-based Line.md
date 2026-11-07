---
title: "Delete an IP-based Line"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/docs-deleting-an-ip-based-line"
---

If you no longer need an IP\-based line, you can delete it in BytePlus DNS.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before deleting an IP\-based line, please consider it carefully. Once you delete an IP\-based line, it cannot be recovered. This operation cannot be rolled back.</div>


<span id="2a1e0eba"></span>
## Prerequisites

There are no DNS records using the IP\-based line in BytePlus DNS.

<span id="4a6c058b"></span>
## Steps

You can follow these steps to delete an IP\-based line.


1. Open the [IP-based lines](https://console.byteplus.com/dns-suite/dns/lines) page in the BytePlus DNS console.

2. Find the IP\-based line that you want to delete. Click **Delete** in the **Operation** column.

3. A confirmation window will pop up, asking if you want to delete the IP\-based line. Click **OK**.

   * If there are no DNS records using the IP\-based line in BytePlus DNS, the IP\-based line will be deleted.

   * If there are DNS records using the IP\-based line in BytePlus DNS, a confirmation window will pop up, listing all the DNS records using that IP\-based line. You need to change the line of these DNS records before you can delete the IP\-based line.
