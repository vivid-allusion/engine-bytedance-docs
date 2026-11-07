---
title: "Delete DNS Records"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/SZwt4b"
---

This document describes how to delete DNS records in BytePlus DNS.

BytePlus DNS uses record sets (RRSets) to manage one or more DNS records with the same domain, line, and type. You can set weights for multiple records in a record set to implement DNS\-based load balancing. See [RFC 7719](https://www.rfc-editor.org/rfc/rfc7719.html) for more information.

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>



* <div data-tips="true" data-tips-type="danger">Once a DNS record is deleted, it will no longer be included in the DNS responses returned to users. Moreover, you can only restore the record value by rolling back the DNS record.</div>


* <div data-tips="true" data-tips-type="danger">Once a record set is deleted, all DNS records within that record set will no longer be included in the DNS responses returned to users.</div>



<div data-tips="true" data-tips-type="danger">You can only restore DNS records and record values by rolling back the DNS records. Therefore, you need to operate with caution.</div>



* <div data-tips="true" data-tips-type="danger">If you only want to temporarily disable a record value, you can disable that record value.</div>


* <div data-tips="true" data-tips-type="danger">If you only want to temporarily disable a record set, you can disable all the record values within that record set.</div>



<span id="delete-one-or-multiple-records"></span>
## Delete one or multiple records

Follow the steps below to delete a record.


1. Open the [BytePlus DNS console](https://console.byteplus.com/dns-suite/dns/publiczone).

2. On the **Record management** tab, find the record set from which you want to delete records.

3. In the **Actions** column, click **Edit**.

4. In the **View record set** page, find the records you need to delete in the **Record value** section, and click **Delete** in the **Action** column.

5. In the prompted dialog box, click **OK** to confirm deletion. If you need to delete multiple DNS records at once, you can also select multiple DNS records and then click the **Delete** button.


<span id="delete-a-record-set"></span>
## Delete a record set

Follow the steps below to delete a record set.


1. Open the [BytePlus DNS console](https://console.byteplus.com/dns-suite/dns/publiczone).

2. On the **Record management** tab, find the record set that you want to delete.

3. In the **Actions** column, click **Delete**.

4. In the pop\-up dialog box, click **Delete**.


<span id="delete-multiple-record-sets"></span>
## Delete multiple record sets

The BytePlus DNS Console supports batch operations on record sets. You can delete multiple record sets at once. Follow the steps below to delete multiple record sets.


1. Open the [BytePlus DNS console](https://console.byteplus.com/dns-suite/dns/publiczone).

2. On the **Record management** tab, select the checkboxes in front of all the record sets that you want to delete.

3. Click the **Delete** button below the record set list.

4. In the pop\-up dialog box, click **Delete**.
