---
title: "Whitelist management"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/whitelist-management"
---

ByteHouse Enterprise Edition supports setting up a whitelist for clusters to manage cluster access permissions. This article will introduce how to view, edit, and delete a whitelist.

<span id="1eb24580"></span>
# Prerequisites

Only users with the SystemAdmin or ClusterAdmin role can use this feature.

<span id="0a1dd3cc"></span>
# View whitelist

Log in to the ByteHouse Console, click **Access control** at the top, click **White List** tab to enter the whitelist list page. You can hover your mouse over the number in the whitelist IP address column to view the configured whitelist addresses.

The cluster is defaulted to "0.0.0.0" IP address, which means all addresses are allowed to access by default.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ed858eacfbfe4c2ba8229f224cd9bf35~tplv-goo7wpa0wc-image.image) </span>

<span id="7460d09e"></span>
# Edit whitelist


1. Click the cluster search box, input the required cluster name in the cluster search box and select the cluster, then click the edit button in the Actions column.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f813cfc730874413bfc8196753ee54bb~tplv-goo7wpa0wc-image.image) </span>

2. In the text box on the whitelist configuration page, input the IP address or address range, fill in a custom description as needed, and click **Save**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/358804a540be4fe6b2436a6a89e3143d~tplv-goo7wpa0wc-image.image) </span>

   The IP address settings are as follows:

   * Support inputting or pasting IP addresses/subnets; separate multiple addresses or subnets with a newline character.

   * Setting "0.0.0.0/0" allows access from all addresses, while "127.0.0.1" blocks access from all addresses.

   * If both "0.0.0.0/0" and "127.0.0.1" are set, all addresses will be allowed access.

   * Once an IP is removed from the whitelist, any established connections with that IP will be immediately disconnected.

   * Up to 300 IP subnets can be set.

      If the IP address you input does not meet the requirements, the system will display that an illegal IP address or CIDR segment, please check before submitting.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42ca15fa873c4e6a96ab7914521806fb~tplv-goo7wpa0wc-image.image) </span>


<span id="dfde3de6"></span>
# Delete whitelist

Click the **edit** button next to the cluster name, then delete the IP address in the text box on the whitelist configuration page, and click **save**.
