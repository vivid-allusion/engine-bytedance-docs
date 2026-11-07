---
title: "Enable or Disable DNS Records"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/Enable_or_Disable_DNS_Records"
---

This document describes how to enable or disable DNS records in BytePlus DNS.

BytePlus DNS uses record sets (RRSets) to manage one or more DNS records with the same domain, line, and type. You can set weights for multiple records in a record set to implement DNS\-based load balancing. See [RFC 7719](https://www.rfc-editor.org/rfc/rfc7719.html) for more information.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Once a DNS record is disabled, it will no longer be included in the DNS responses returned to users. Moreover, you can only restore the record value by rolling back the DNS record.</div>


* <div data-tips="true" data-tips-type="tip">Once a record set is disabled, all DNS records within that record set will no longer be included in the DNS responses returned to users.</div>



<span id="enable-or-disable-one-or-multiple-records"></span>
## Enable or disable one or multiple records

Follow the steps below to enable or disable a record.


1. Open the [BytePlus DNS console](https://console.byteplus.com/dns-suite/dns/publiczone).

2. On the **Record management** tab, find the record set from which you want to enable or disable records.

3. In the **Actions** column, click **Edit**.

4. In the **View record set** page, find the records you need to enable or disable in the **Record value** section, and click **Enable**. If you need to enable or disable multiple DNS records at once, you can also select multiple DNS records and then click the **Enable** button or the **Disable** button.


<span id="enable-or-disable-one-or-multiple-record-sets"></span>
## Enable or disable one or multiple record sets

The BytePlus DNS Console supports batch operations on record sets. You can enable or disable multiple record sets at once. Follow the steps below to enable or disable multiple record sets.


1. Open the [BytePlus DNS console](https://console.byteplus.com/dns-suite/dns/publiczone).

2. On the **Record management** tab, select the checkboxes in front of all the record sets that you want to enable or disable.

3. Click the **Enable** button or the **Disable** button below the record set list.

4. In the pop\-up dialog box, click **Enable** or **Disable**.
