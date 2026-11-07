---
title: "Purchase a PTR record"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/purchase_a_ptr_record"
---

This document describes how to purchase a PTR record. For more information about PTR records, see [PTR Record](https://docs.byteplus.com/en/docs/byteplus-dns-suite/docs-supported-dns-record-types#ptr-record).

<span id="LsFLzEUl"></span>
## Steps

Follow these steps to purchase a PTR record.


1. Log in to the [BytePlus DNS](https://console.byteplus.com/dns-suite/dns) console.

2. In the left navigation pane, select **DNS \> PTR Record**.

3. On the **PTR record ** page, click **Purchase PTR record**.

4. On the **Purchase PTR record** page, complete the following configurations.

&nbsp;

   
   |Section |**Parameter** |**Description** |
   |---|---|---|
   |Purchase PTR records |Quantity |Enter the quantity of PTR records that you want to purchase. |
   ||Valid period |1 year<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Each PTR record is valid for one year from the time of purchase. If you do not renew a PTR record before it expires, the record becomes invalid and cannot be renewed. You must purchase a new PTR record to replace it.</div><br> |
   ||Project |Select the project group to which the resource belongs. <br><br>Upon successful purchase, the PTR record will be automatically assigned to the selected project, which facilitates subsequent permission management and resource filtering based on the project. If no selection is made, the record will default to the **default** project.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If the required project group is not found, click <strong>Create Project</strong> to create a new project group on the Project management page.</div><br> |
   ||Tag |Add one or more tags to the PTR record (in the format of key\-value pairs, such as env=prod or team=frontend). Tags allow you to categorize, retrieve, and control permissions for your resources from different dimensions, thereby increasing resource management flexibility. |
   ||Agreement |Read, check, and agree to the relevant agreements. |
   |Configure PTR records (optional) |Record configuration |In the **Configure PTR recording** section, configure the PTR record you just purchased. You can skip this step and configure the record later. For configuration details, see [Configure a PTR record](https://docs.byteplus.com/en/docs/byteplus-dns-suite/manage_ptr_records#4nwMlXTr).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If you choose to configure the PTR record during purchase and you purchase multiple records, you must configure all of them at this time.</div><br> |
   

&nbsp;

5. Click **Submit**. After confirming the order details, click **Next step**, select payment method, and then click **To pay** to complete the payment.


<span id="g8bJCc9y"></span>
## Activation timeline

After purchasing and [configuring a PTR record](https://docs.byteplus.com/en/docs/byteplus-dns-suite/manage_ptr_records#4nwMlXTr) in the console, BytePlus is required to coordinate with the upstream authority, CNNIC (China Internet Network Information Center), to complete the final configuration and delegation. This process typically takes 1 to 3 business days to take effect. During this period, the PTR record status will be displayed as **Creating**. Once the record is successfully delegated and active, the status changes to **Active**.

This process may take 1 to 3 business days to take effect. During this activation period, the PTR record status will be displayed as **Creating**. Once successfully activated, the PTR record status will change to **Active**.
