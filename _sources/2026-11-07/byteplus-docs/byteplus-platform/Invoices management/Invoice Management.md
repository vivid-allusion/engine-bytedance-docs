---
title: "Invoice Management"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-invoices"
---

The Invoice page is the self\-service entry in the **BytePlus Console** for viewing billing documents. Customers can use it to confirm whether an invoice has been issued for a billing period, review issued amounts, check whether any amount has been reversed through a credit note, and download the PDF file for accounting and reconciliation.

Access path: sign in to [BytePlus Console](https://console.byteplus.com/auth/login/), click the account avatar in the upper\-right corner, open **Billing**, and then select [Invoices](http://console.byteplus.com/finance/invoice-manage) from the left\-side navigation.


1. # Invoicing profile <span id="6TdqF0va"></span>


At the top of the page, displays the current account's invoicing profile in read\-only mode, including the business legal name, contact address, email address, GST registration number, and country/region. 

<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260831132121-1280668913146.png" width="2904px" /></div>



2. # Invoice types <span id="Y1VEPt37"></span>



|**Invoice type** |**Business meaning and when it is generated** |
|---|---|
|Tax Invoice |A billing document issued by BytePlus for payment collection. It may be issued by billing period or based on a submitted request, and serves as the official document for customer payment processing and bookkeeping. |
|Credit Note |An offset document issued when an original invoice needs to be corrected or when a refund is processed. It is used to reverse part or all of the original invoice amount and is always linked to a specific invoice. |



3. # Invoice view <span id="2foHIEQ5"></span>


Default view: Each top\-level row represents one invoice. When an invoice has related credit notes, those records are grouped under the original invoice in a parent\-child structure that can be expanded or collapsed as needed.

<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260831132124-1453641667802.png" width="5114px" /></div>



1. ## Aggregation and expand rules <span id="riOqUxPd"></span>

* The list shows only invoices that have **not** been fully reversed, together with any related credit notes. Records that have already been fully reversed are available in **List view**.

* Rows with related credit notes display an expand control. Customers can expand the parent row to view child records, collapse them again when needed, or use the **Expand all** option at the bottom of the list.

* By default, related records for the most recent billing period are expanded when credit notes exist. Historical periods are collapsed by default.

* The first column is always **Billing period**, and it uses the billing period of the original invoice. A credit note may be issued in a later period than the original invoice, but when the row is collapsed, the list still shows the invoice's billing period.

2. ## Field descriptions <span id="yE0V8zCu"></span>



|**Field** |**Description** |
|---|---|
|Billing period |The billing period of the original invoice. This is the first column in the list. |
|Invoice No. |The invoice number, for example **BPSGEPS20261044472955C60001**. Credit notes show their own document number. |
|BytePlus entity |The BytePlus invoicing entity, such as Singapore, Malaysia, Hong Kong, or BytePlus Japan. The exact available values depend on the entities supported for invoicing. |
|Invoiced amount |The issued amount in the pricing currency. The page displays the amount together with the currency code, for example **1000.00 USD**. |
|Total amount |The net invoiced amount, calculated as the invoice amount plus the sum of all related credit note amounts. |
|Issue time |The document issue time, accurate to the second. |
|Status |Possible values include **Issued**, **Credit Note Processing**, and **Partially Reversed**. **Fully Reversed** records are visible only in **List view**. |
|Actions |Available actions include **Download** to get the PDF file and **View** to open the document details page. |



4. # List view <span id="suv9lrM7"></span>


**List view** complements the default Invoice view by displaying **all** invoice and credit note records for the current account in a flat transaction\-style table. It does not group child records under parent invoices, and records are sorted by **Issue time** in descending order.

This view is useful when customers need to review the full document history for a specific time range, or when they need to find historical invoices that are no longer shown in the default Invoice view because they have already been fully reversed.

The fields are the same as in the Invoice view, with two additional columns:


|**Additional field** |**Description** |
|---|---|
|Type |Identifies the record type as **invoice** or **creditNote**, so both document types can be distinguished in the same list. |
|Original invoice No. |Blank for invoice records. For credit note records, this field shows the original invoice number that the credit note offsets. |


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260831133427-655095910786.png) </span>


5. # Download and view details <span id="SpwP0UC7"></span>

* **Download directly**: click **Download** in the **Actions** column for the target record. The browser will download the PDF file directly. If the target document is a credit note, first expand the related parent invoice row and then download the child record.

* **Review details before downloading**: click **View** to open the **Invoice information** page. After checking the invoice header, tax registration details, invoice items, amount, and tax amount, click **Download pdf** in the upper\-right corner.


If the **Download** button is not available, the file is usually still being generated, for example while the status remains **Credit Note Processing**. Refresh the page after document generation is complete.


6. # Tax calculation for post\-payment orders <span id="Tzq29KIb"></span>


For post\-payment orders, BytePlus will calculate the total tax by adding up the tax for each bill generated on a daily or hourly basis. Additionally, the tax for each bill will be rounded off, which may result in a slight difference between the final total tax amount calculated by BytePlus (which is printed on the invoice) and the total tax obtained by multiplying the total bill amount with the tax rate. **This is an expected rounding outcome and does not indicate that the invoice was issued incorrectly.** 

Below is an example invoice for post\-payment orders:


|**Bill No.**  |**Amount (pre\-tax)**  |**Tax Rate** |**Tax** |
|---|---|---|---|
|1 |27.16 |8% |2.17 |
|2 |27.16 |8% |2.17 |
|3 |27.16 |8% |2.17 |
|4 |27.16 |8% |2.17 |
|5 |27.16 |8% |2.17 |
|6 |27.16 |8% |2.17 |
|Total |27.16x6 = **162.96** |*  |2.17x6 = **13.02**<br><br>***Note***: The total tax is not (162.96x8%) which is 13.04 |



7. # Tax rate reference <span id="NuTgxdFu"></span>


For more information on the tax rates BytePlus implements in each country/region, refer to [this article](https://docs.byteplus.com/en/byteplus-platform/docs/tax-rate-reference).
