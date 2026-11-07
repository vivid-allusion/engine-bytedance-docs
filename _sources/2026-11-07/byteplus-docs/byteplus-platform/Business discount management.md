---
title: "Business discount management"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
section: "Document"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/business-discount-management"
---

On the "[Business Discount](https://console.byteplus.com/finance/contract-discount)" page, you can centrally view all your signed contract price information. There is no need to download and verify each contract PDF individually, facilitating internal reconciliation and cross\-platform service comparison.

Common usage scenarios:


* **Financial reconciliation**: When finance staff need to verify whether the actual spending of a certain service is consistent with the contract price, they can quickly query and export detailed pricing information here.

* **Procurement decision‑making**: When business owners plan new services, they can view existing contract discounts here to support procurement decisions.

* **Multi‑cloud price comparison**: When you need to compare service prices of different cloud providers, you can clearly see the exclusive contract prices that BytePlus offers you here.


Note: Contract price, also called business discount, refers to the exclusive price or discount agreed in the contract between you and BytePlus.


1. ## Operation process <span id="v0XnrS9S"></span>


<span id="sUnfkpOs"></span>
### 1.1 View contract prices

<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260515091023-1217598285550.png" width="1699px" /></div>


Pre‑operation notes:


* If you are an IAM user, the admin account must grant you the “Contract Price Query” permission in advance.

   * Only when the following permissions are configured can the IAM user, view contract prices. For detailed steps, see the documentation at “[Editing a user](https://docs.byteplus.com/en/docs/byteplus-platform/docs-editing-a-user)”.

      * QueryContractDiscount is set to allow.

      * QueryDiscountPrice is not set to deny (remove the deny setting).

* If you are a Finance Cloud – Finance Management sub‑account, the admin account must grant you the “Contract Price Sharing” permission in advance.

* If you are a Finance Cloud – Finance Custody sub‑account, you share the primary account’s contract prices by default.



&nbsp;

1. Log in to the Cost Center, and in the left navigation bar find and click **Business Discount Management**.

2. After entering the page, you can see the contract price information related to your account. Depending on your account type, different tabs will be displayed on the page:

   * **Current account business discounts**: Shows contract prices directly associated with your currently logged‑in account. Applicable to all direct customers, reseller accounts, and end customer accounts that have their own contract prices.

   * **IAM admin account business discounts**: If you are an authorized IAM user, this tab shows the contract price information of your admin account.

   * **Finance Cloud primary account business discounts**: If you are an authorized Finance Cloud sub‑account, this tab shows the contract price information of your primary account.


> Note: If you have not been granted the corresponding authorization, you will not see the corresponding tab or its content.



3. You can use the filters at the top of the page (such as related contract, applicable product, payment method, etc.) to quickly locate the contract price you want to find.

4. By default, the list displays contract price data in the “By all records” view, including both active and expired records. You can click the **By priority** button to switch the view.


<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260515091023-282930503814.png" width="1468px" /></div>



   * **By all records**: Displays all signed contract prices, including expired ones.

   * **By priority**: Based on internal price matching logic, the system shows you the highest‑priority valid contract price for each product. In this view, the first column of the list displays the “Priority” index.


&nbsp;

<span id="uJ2u6WOB"></span>
### 1.2 Export contract prices


1. As needed, set the appropriate filter conditions, or directly click the **Export** button under a specific tab.


<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260515091022-351315290648.png" width="1458px" /></div>



2. The system supports exporting in **Excel** format.

3. The exported file will contain all contract price details under the current filter conditions. If no filter is set, all data under the current tab will be exported.


Operation result: You will get an Excel file named “【Current tab name】+ Business Discount List + 【Export date】”, which contains detailed contract price field information.

<span id="sRnFQGto"></span>
### 1.3 Use the "Discount Priority Query" tool

If you want to know which contract price a specific resource (instance) will actually match, you can use this tool.

<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260515091022-301605695619.png" width="1456px" /></div>



1. On the “Business Discount” page, click the **Discount Priority Query** button.


<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260515091022-164691863942.png" width="1437px" /></div>



2. In the pop‑up window, enter the **Instance ID** you want to query.

3. Click **Query**.


Operation result: The system will list all contract price rules that the instance can match in order of priority, and the first one is the contract price that actually takes effect.


2. ## Reference information for contract prices <span id="6gH7sHr8"></span>


<span id="nl3qNcBI"></span>
### 2.1 Field descriptions

The meanings of some important fields on the “Business Discount” page and in the exported file are as follows:


* **Effective target**: Indicates which entity the contract price applies to. It is generally divided into two types: account type (indicating that the price is only effective for a specific account ID) and entity type (indicating that the price is effective for all accounts under your company’s verified legal entity).

* **Pricing method / discount type**: The specific calculation method of the contract price. Common types include: single discount (multiplying a fixed discount on the list price, such as “50% off”), fixed unit price (regardless of usage, it is calculated at a fixed price, such as “0.5 USD/GiB”), and tiered pricing (such as time‑based discounts or progressive discounts beyond a threshold, where the price changes according to usage duration or usage tiers).

* **Status**: The current business status of the contract price, divided into “Active” (currently usable) and “Expired” (past the validity period or unavailable).

* **Configuration rule related fields** (such as configuration category, billing method, region, etc.): These fields together define the specific scope where the contract price applies.


<span id="0Ah9xNjU"></span>
### 2.2 Complex logic explanations

<span id="pXjTsAJC"></span>
#### 2.2.1 "All options" and "Specific options"

<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260515091023-1589016514351.png" width="1446px" /></div>



* **Specific options**: The filter results include contract price information for both all options and specific options, because for specific options, in actual price inquiries it may match not only the contract prices corresponding to the specific options but also those corresponding to all options.

* **All options**: The filter results include only contract price information corresponding to all options.


<span id="MVsZijzO"></span>
#### 2.2.2 "By all records" and "By priority"

To make it easier for you to view contract prices from different dimensions, we provide two list views: “By all records” and “By priority”.


* **By all records (default view)** : Used for comprehensive audit and historical tracing. It displays all contract price information you have signed, including historical records that have already “expired”.

* **By priority**: Helps you quickly determine, for a specific product, which contract price will take effect first. The system filters out “expired” records and, based on internal price matching rules, sorts multiple valid contract prices under the same product.

3. ## FAQ <span id="LC94CQFe"></span>


<span id="KP290Iuh"></span>
### 3.1 Q: Why can’t I see the "Business Discount" menu, or why is the "IAM/Finance Cloud primary account business discount" tab missing?

A: This is usually caused by insufficient permissions or a mismatched account type. Please check according to your situation:


* **You are an IAM sub‑account**: You need to contact the primary account and have it grant you discount‑viewing permissions in the IAM permission policy. After authorization, you will be able to see the “IAM primary account business discounts” tab.

* **You are a Finance Cloud – Finance Management sub‑account**: You need to contact the primary account to enable “Contract Price Sharing” for you. After authorization, you will be able to see the “Finance Cloud primary account business discounts” tab.

* **You are another type of account**: The first phase of this feature only supports direct‑sales customers and their associated IAM and Finance Cloud customers. If you are an agent, reseller, or other customer type, you currently cannot use this feature.


<span id="TOZrmfEd"></span>
### 3.2 Q: Why can’t I find any contract price after entering an instance ID in the "Discount Priority Query" tool?

A: Possible reasons include the following:


* **Instance ownership mismatch**: The instance ID does not belong to the account you are currently logged in with, nor to a primary account you are authorized to view.

* **No applicable price**: The instance truly has no valid contract price that can be matched.

* **Input error**: Please check whether the instance ID you entered is correct.


<span id="zdJTgI7A"></span>
### 3.3 Q: I want to export a very large volume of contract price data, and the export fails or times out. What should I do?

A: If you have a very large number of contract price records, exporting all data at once may cause performance issues. It is recommended that you use the filters at the top of the page (such as related contract, applicable product, etc.) to narrow the data range and export in batches.
