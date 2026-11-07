---
title: "Batch Create DNS Records"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/Batch_Create_DNS_Records"
---

This document describes how to create DNS records in batches in BytePlus DNS.

You can create DNS records with the same record type and record value for different root domains in one operation, or create DNS records with different record types and record values for different root domains in one operation. The domains can be root domains or delegated subdomains.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Before creating DNS records in batches, you must ensure that the current BytePlus account has DNS ownership for the domains or delegated subdomains for which you need to create DNS records. You cannot create DNS records in batches for domains or delegated subdomains for which you do not have DNS ownership.</div>


* <div data-tips="true" data-tips-type="tip">For records added through batch operations, the line will be automatically set to <strong>Default</strong>, and the TTL will be automatically set to <strong>10 minutes</strong>.</div>



<span id="create-same-dns-records-for-different-domains"></span>
## Create same DNS records for different domains

Follow these steps to create same DNS records for different root domains or delegated subdomains.


1. Open the [Batch operation](https://console.byteplus.com/dns-suite/dns/publiczone/batchOperation) page in the BytePlus DNS console.

2. On the **Batch operation** page, set **Batch operation mode** to **same DNS records**. Then configure the following parameters.

   
   |Parameter |Description |
   |---|---|
   |Domain |The root domains or delegated subdomains for which you need to create DNS records in batches. One root domain or delegated subdomain per line, for example, `example.com`. This parameter can contain up to 10,000 domains (root domains or delegated subdomains). |
   |Record type |Set the same record type for all DNS records to be added in this batch operation. |
   |Domain prefix |The domain prefix of the root domain or delegated subdomain, for example, `abc`. You can click  **+ Add** to add one or more domain prefixes.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you have added multiple domains, BytePlus DNS will combine each domain with each domain prefix to form an FQDN, and generate a DNS record based on that FQDN.</div><br><br><br><div data-tips="true" data-tips-type="tip">For example, if you added two domains <code>example.com</code> and <code>byteplus.com</code>, and added two domain prefixs <code>abc</code> and <code>123</code>, with the record type A, then BytePlus DNS will generate a DNS record for each of the following FQDNs for batch creation:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip"><code>abc.example.com.</code></div><br><br><br>* <div data-tips="true" data-tips-type="tip"><code>123.example.com.</code></div><br><br><br>* <div data-tips="true" data-tips-type="tip"><code>abc.byteplus.com.</code></div><br><br><br>* <div data-tips="true" data-tips-type="tip"><code>123.byteplus.com.</code></div><br> |
   |Record value |Set the same record value for all DNS records to be added in this batch operation. |
   |Line |The line value is fixed as **Default**. You cannot change this parameter. |
   |TTL |The TTL value is fixed at **10 minutes**. You cannot change this parameter. |
   |Record creation mode |You can set it to **Full** or **Incremental**.<br><br><br>* **Full**: After you click **Confirm**, BytePlus DNS will first delete all DNS records under the root domain or delegated subdomain, and then create the DNS records in batches.<br><br>* **Incremental**: After you click **Confirm**, BytePlus DNS will create new DNS records based on the existing DNS records. If the newly created DNS records conflict or duplicate with existing DNS records, the conflicting or duplicate DNS records will fail to be created. |
   

3. Click **Confirm**.

   * If the **Record creation mode** is **Full**, BytePlus DNS will pop up a risk warning dialog. After you click **Acknowledged** in the dialog, BytePlus DNS will start creating DNS records in batches and pop up a **Batch operation task submitted** dialog.

   * If the **Record creation mode** is **Incremental**, BytePlus DNS will start creating DNS records in batches and pop up a **Batch operation task submitted** dialog.

4. In the **Batch operation task submitted** dialog, click **View log** to jump to the **Batch operation log** page. On the **Batch operation log** page, find your batch operation based on the **Operation time**, and click **Download detailed log** in the **Actions** column to download the operation log file in .xlsx format. You can view the operation results in the operation log file. If the **Operation result** is a failure, you can check and fix the DNS record issues based on the **Operation details**. See [Troubleshooting FAQs](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-frequently-asked-questions).


<span id="create-different-dns-records-for-different-domains"></span>
## Create different DNS records for different domains

Follow these steps to create different DNS records for different domains.


1. Open the [Batch operation](https://console.byteplus.com/dns-suite/dns/publiczone/batchOperation) page in the BytePlus DNS console.

2. On the **Batch operations** page, set **Batch operation mode** to **different DNS record**. Then configure the following parameters.

   
   |Parameter |Description |
   |---|---|
   |DNS records |The DNS records you need to create in batches. One DNS record per line, in the format: `domain,record type,domain prefix,record value`, for example, `example.com,A,abc,1.1.1.1`. This parameter can contain up to 10,000 DNS records. |
   |Line |The line value is fixed as **Default**. You cannot change this parameter. |
   |TTL |The TTL value is fixed at **10 minutes**. You cannot change this parameter. |
   |Record creation mode |You can set it to **Full** or **Incremental**.<br><br><br>* **Full**: After you click **Confirm**, BytePlus DNS will first delete all DNS records under the root domain or delegated subdomain, and then create the DNS records in batches.<br><br>* **Incremental**: After you click **Confirm**, BytePlus DNS will create new DNS records based on the existing DNS records. If the newly created DNS records conflict or duplicate with existing DNS records, the conflicting or duplicate DNS records will fail to be created.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the TTL of the existing record set is not 10 minutes, after you add DNS records to the existing record set through incremental addition, the TTL of the existing record set will not change.   </div><br>    |
   

3. Click **Confirm**.

   * If the **Record creation mode** is **Full**, BytePlus DNS will pop up a risk warning dialog. After you click **Acknowledged** in the dialog, BytePlus DNS will start creating DNS records in batches and pop up a **Batch operation task submitted** dialog.

   * If the **Record creation mode** is **Incremental**, BytePlus DNS will start creating DNS records in batches and pop up a **Batch operation task submitted** dialog.

4. In the **Batch operation task submitted** dialog, click **View log** to jump to the **Batch operation log** page. On the **Batch operation log** page, find your batch operation based on the **Operation time**, and click **Download detailed log** in the **Actions** column to download the operation log file in .xlsx format. You can view the operation results in the operation log file. If the **Operation result** is a failure, you can check and fix the DNS record issues based on the **Operation details**. See [Troubleshooting FAQs](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-frequently-asked-questions).


<span id="viewing-batch-operation-logs"></span>
## Viewing batch operation logs

Follow these steps to view your batch operation logs.


1. Open the [Batch operation](https://console.byteplus.com/dns-suite/dns/publiczone/batchOperation) page in the BytePlus DNS console.

2. In the upper right corner of the **Batch operation** page, click **batch Operation Logs**.

3. On the **Batch operation logs** page, find your batch operation based on the **Operation time**, and click **Download detailed log** in the **Actions** column to download the operation log file in .xlsx format. You can view the operation results in the operation log file.


The table below shows an example of an operation log file.


|Domain Name |Record Type |Host Record |Record Value |Operation result |Operation details |Time (UTC+8) |
|---|---|---|---|---|---|---|
|china17.com |A |abc |1.1.1.1 |Failed |The record duplicates an existing record |2024\-09\-11 18:07:40 |
|example.com |A |abc |1.1.1.1 |Success | |2024\-09\-11 17:40:26 |
