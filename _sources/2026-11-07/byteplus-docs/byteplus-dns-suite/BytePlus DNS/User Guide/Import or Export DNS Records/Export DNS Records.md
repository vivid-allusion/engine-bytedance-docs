---
title: "Export DNS Records"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/docs-export-dns-records"
---

This document describes how to export DNS records from a specified domain to a file.

<span id="da58e755"></span>
## Steps

Complete the following steps to export DNS records.


1. Open the [BytePlus DNS console](https://console.byteplus.com/dns-suite/dns).

2. Go to the **Domain management** page. Click on your domain in the **Domain** column.

3. On the **Record management** tab, click the export button on the right side.

4. In the **Export records** dialog box, select a format. The options are:

   * **xlsx**: Export the DNS records as an `.xlsx` file. The `.xlsx` file does not include the default NS and SOA records.

   * **zone**: Export the DNS records as a `.zone` file. The `.zone` file includes the default NS and SOA records.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The <code>.zone</code> file uses the standard BIND format to describe the DNS records. You can refer to <a href="https://datatracker.ietf.org/doc/html/rfc1034">RFC 1034</a> and <a href="https://datatracker.ietf.org/doc/html/rfc1035">RFC 1035</a> for more information.      </div>
      

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d975c73c4f941538b293db112c691d9~tplv-goo7wpa0wc-image.image) </span>


After making the selection, click **Export** to export your DNS records to a file.
