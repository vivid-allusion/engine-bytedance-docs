---
title: "Viking AI Search Billing and Pricing"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Billing_and_Pricing"
---

**Effective Date:**  May 25, 2026 

<span id="cb692428"></span>
## 1. Overview

Viking AI Search is an integrated AI service for search, recommendation, and conversational search over multimodal data (text, image, video, document). This document sets out the billing items, pricing, and settlement rules applicable to **Viking AI Search. ** For product capabilities and API references, see the [Viking AI Search documentation](https://docs.byteplus.com/en/docs/viking-aisearch/Viking_AI_Search_Product_Introduction).

<span id="aa7915eb"></span>
## 2. Definitions


|**Term** |**Definition** |
|---|---|
|Billing month |A 30\-day period beginning at the activation timestamp of the current subscription order. |
|Billing hour |A clock hour beginning on the hour (GMT+8) used as the unit of measurement for pay\-as\-you\-go settlement. |
|Viking Unit |The standard billing unit for Viking AI Search resource consumption. <br><br>There are three categories: Viking Storage Unit (VSU), Viking Processing Unit (VPU), and Viking Request Unit (VRU). |
|Multimodal Item Datasets |Datasets storing items consisting of text, image, and video fields, used for search, recommendation, and conversational search. |
|User Event Datasets |Datasets storing user behavior events used for personalization. |
|Non\-structured Datasets |Datasets storing document content (e.g., pdf, xlsx, docx) for retrieval. |
|Linked application |An application within the customer's account that consumes a dataset. <br><br>The same record processed for N linked applications is counted as N processing units. |
|Successful API request |An API request that returns an HTTP status code other than 5xx. 5xx requests are not billable. |
|Account credits |Prepaid balance held in the customer's BytePlus account, available for the settlement of pay\-as\-you\-go charges. |
|Arrears |The state in which the account's available credit is insufficient to settle the most recent hourly pay\-as\-you\-go bill. |


<span id="46ff8045"></span>
## 3. Billing items and pricing

<span id="f1a515f1"></span>
### 3.1 Billing model summary

Viking AI Search is billed on two bases:


* **Monthly subscription (prepaid):**  the customer pays a fixed monthly fee for a subscription plan and receives a fixed quota of Viking Units for use during the billing month.

* **Pay\-as\-you\-go (hourly):**  when monthly usage exceeds the included Viking Unit quota, the excess is billed hourly in USD at the unit prices set out in **Section 3.3**.


<span id="0665b542"></span>
### 3.2 Subscription plan

Viking AI Search currently offers one paid subscription plan in the Asia\-Southeast (Johor) region.


|**Plan** |**Unit** |**List price (USD)**  |**Included Viking Units** |
|---|---|---|---|
|Growth Plan |per month |110.00 |2 x VSU, 10 x VPU, 5 x VRU |


**Note:** 


* The included Viking Unit quota may be consumed flexibly in storage, processing, and request scenarios within the same billing month, in accordance with the conversion rates set out in Section 3.3.

* Quotas are measured per billing month and reset at the start of each new billing month. Unused quota is forfeited and does not roll over.


<span id="ce519cf3"></span>
### 3.3 Pay\-as\-you\-go

When monthly usage exceeds the included Viking Unit quota, the excess is billed in USD on a pay\-as\-you\-go basis at the unit prices below.

<span id="3ded2390"></span>
#### 3.3.1 Viking Unit base prices


|**Billing item** |**Unit** |**List price (USD)**  |
|---|---|---|
|Viking Storage Unit (VSU) |per unit |1.0000 |
|Viking Processing Unit (VPU) |per unit |1.0000 |
|Viking Request Unit (VRU) |per unit |1.0000 |
|Search content moderation |per 1,000 requests |0.3000 |
|Image multi\-subject recognition |per 1,000 requests |0.3000 |


<span id="3c34be7c"></span>
#### 3.3.2 Viking Storage Unit (VSU) 


|**Data type** |**Price (VSU)**  |**Unit** |**Smallest billed unit** |**Definition** |
|---|---|---|---|---|
|Text storage |0.1036<br><br> |per 1,000 records per month |per record per hour |Total number of records uploaded and stored in Multimodal Item Datasets. <br><br>**Each unique Item ID stored is counted as one record, regardless of the number of fields.** <br><br>Measured hourly at 0.000144 VSU per 1,000 records per hour. |
|Image storage |0.1607 |per 1,000 images per month |per image per hour |Total number of images uploaded and stored in Multimodal Item Datasets. <br><br>Measured hourly at 0.000223 VSU per 1,000 images per hour. |
|Video storage |0.1929 |per video\-hour per month |per video\-second per hour |Total length of video uploaded and stored in Multimodal Item Datasets. <br><br>Measured hourly at 0.000268 VSU per video\-hour per hour. |
|Document storage |0.1107 |per 1,000 pages per month |per page per hour |Total number of pages uploaded and stored in Non\-structured Datasets. <br><br>Measured hourly at 0.000154 VSU per 1,000 pages per hour.<br><br>**Definition of 1 page**<br><br><br>1. .pdf, .ppt, .pptx: 3000 tokens<br><br>2. .md, .txt, .html, .doc, .docx, .jsonl: 2000 characters<br><br>3. .csv, .xls, .xlsx: 150 cells<br><br>4. Images: 1 image |


<span id="a1a9832b"></span>
#### 3.3.3 Viking Processing Unit (VPU)


|**Data type** |**Price (VPU)**  |**Unit** |**Smallest billed unit** |**Definition** |
|---|---|---|---|---|
|Text processing and indexing |0.2286 |per 1,000 records |per record |Number of records processed and indexed in Multimodal Item Datasets linked to applications.  <br><br>**Cost of one new record = Number of linked applications. ** <br><br>No processing fee applies for record updates if the updated field is neither searchable nor used for image search. |
|Image processing and indexing |0.8327 |per 1,000 images |per image |Number of images processed and indexed in Multimodal Item Datasets linked to applications. <br><br>**Cost of one new image = Number of linked applications.** <br><br>When image URL or base64 is updated, image and text processing fee applies. |
|Video processing and indexing |3.1306 |per video\-hour |per video\-second |Number of videos processed and indexed in Multimodal Item Datasets linked to applications. <br><br>**Cost of one new video = Length of video (seconds) x number of linked applications.** <br><br>When video URL is updated, video and text processing fee applies. |
|User event data processing |0.0100 |per 1,000 records |per record |Number of user events processed in User Event Datasets linked to applications. <br><br>**Cost of one new user event record = Number of linked applications.**  |
|Document processing |8.57143 |per 1,000 pages |per page |Number of pages processed in Non\-structured Datasets linked to applications. <br><br>**Cost of one document = Number of pages x number of linked applications.** <br><br>**Definition of 1 page**<br><br><br>1. .pdf, .ppt, .pptx: 3000 tokens<br><br>2. .md, .txt, .html, .doc, .docx: 2000 characters<br><br>3. .csv, .xls, .xlsx: 150 cells<br><br>4. Images: 1 image |


<span id="9f37d7fa"></span>
#### 3.3.4 Viking Request Unit (VRU)


|**API endpoint** |**Price (VRU)**  |**Unit** |**Smallest billed unit** |**Definition** |
|---|---|---|---|---|
|Search |0.4333 |per 1,000 API requests<br><br> |per API request<br><br> |Successful API request to the `Search` or `QueryRecommendation` endpoint. |
|ChatSearch |17.8214 |per 1,000 API requests |per API request |Successful API request to the `ChatSearch` endpoint. |
|Deep Video ChatSearch |87.4214 |per 1,000 API requests |per API request |Successful API request to the `ChatSearch` endpoint that uses video understanding capabilities. |
|Recommend |0.1000 |per 1,000 API requests |per API request |Successful API request to the `Recommend` endpoint. |


<span id="6491e4d2"></span>
## 4. Billing instructions

<span id="c0f57b49"></span>
### 4.1 Prepayment and subscription activation

Viking AI Search is sold on a prepaid monthly basis. Activation of the service constitutes the customer's acknowledgment of the prices and billing rules in this document and the terms of service.


* The customer activates the service by selecting the Monthly Subscription Plan and confirming the order in the BytePlus Console.

* Subscription fees are deducted at the time of order. Service is activated immediately upon successful payment, and the billing month begins from the activation timestamp.


<span id="9631f5e5"></span>
### 4.2 Hourly pay\-as\-you\-go settlement


* Pay\-as\-you\-go charges accrue continuously and are settled hourly based on usage in the preceding billing hour.

* If the account holds sufficient credits, the charge is automatically deducted from the account balance.

* If the account does not hold sufficient credits at the time of settlement, the account enters arrears (see **Section 4.5**).


<span id="0c9ce9bc"></span>
### 4.3 Auto\-renewal


* Auto\-renewal is **enabled by default** when the customer activates a Monthly Subscription Plan. 

* The customer may disable auto\-renewal at any time in the BytePlus Console under [Billing Center → Renewal Management.](https://console.byteplus.com/finance/renew)


<span id="abf95db5"></span>
### 4.4 Service expiration and data retention


* If the subscription is not renewed by the end of the billing month and auto\-renewal is disabled, the service enters a **168\-hour (7\-day) retention period** beginning at the expiration time.

* During the retention period:

   * The platform console remains accessible.

   * All stored data, indexed data, and application configurations are retained.

   * All API requests are denied.

   * New data cannot be uploaded; existing application configurations cannot be edited; new configurations cannot be created; running tasks are stopped.

* If the subscription is renewed within the retention period, service is fully restored.

* If the subscription is not renewed within the retention period, service resources are released. Upon release:

   * All resources and configurations are deleted.

   * The platform console for this service is no longer accessible.

   * Customer data is deleted from production systems within 24 hours. Data held in routine system backups is retained and overwritten in accordance with the BytePlus standard backup\-retention schedule.


<span id="bb67f0c7"></span>
### 4.5 Arrears, suspension, and restoration


* An account is considered in arrears when account credit is insufficient to settle an hourly pay\-as\-you\-go bill at the scheduled settlement time.

* A **168\-hour (7\-day) cure period** begins at the time the account is placed in arrears. During this period:

   * The platform console remains accessible.

   * All stored data, indexed data, and application configurations are retained.

   * All API requests are denied.

   * New data cannot be uploaded; existing application configurations cannot be edited; new configurations cannot be created; running tasks are stopped.

* If the arrears are settled in full within the cure period, service is fully restored.

* If the arrears are not settled within the cure period, service resources are released on the same terms as **Section 4.4.** 


<span id="fae17e17"></span>
### 4.6 Configuration change

The customer may change the configuration of the subscribed plan in accordance with the configuration\-change rules displayed in the BytePlus Console at the time of the change. The amount payable for any configuration change is the amount displayed on the configuration\-change confirmation screen.

<span id="3c97812f"></span>
### 4.7 Unsubscribe and refunds


* The customer may unsubscribe from the Monthly Subscription Plan at any time during the billing month via the BytePlus Console under ** ** [Billing Center → Unsubscription Management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management) **. ** 

* Each account is entitled to a once\-off ** 7\-day unconditional cancellation of ** Viking AI Search Monthly Subscription Plan  (Subject to applicable mandatory law). Within the first 7 calendar days of your initial monthly subscription, you may cancel via [Billing Center] \- [Cancellation Management] \- [7\-Day Unconditional Cancellation]. **Refund is provided for unused portion of the current monthly subscription ** (Subject to applicable mandatory law). 

* Upon successful unsubscription, the service enters a **24\-hour (1\-day) retention period** beginning at the unsubscription time. During this period:

   * The platform console remains accessible.

   * All stored data, indexed data, and application configurations are retained.

   * All API requests are denied.

   * New data cannot be uploaded; existing application configurations cannot be edited; new configurations cannot be created; running tasks are stopped.

* If unsubscription is reversed within the retention period, service is fully restored.

* If unsubscription is not reversed within the retention period, service resources are released on the same terms as **Section 4.4.** 


<span id="7bf315eb"></span>
## 5. Taxes, currency, and invoicing


* All prices in this document are stated in **United States Dollars (USD)**  and are **exclusive of taxes**, including value\-added tax, goods and services tax, and any withholding or similar taxes that may apply in the customer's jurisdiction. Such taxes, if applicable, are payable by the customer in addition to the listed prices.

* Invoices are issued in USD and made available in the BytePlus Console under [Billing Center](https://console.byteplus.com/finance/overview).

* The customer is responsible for ensuring that account information used for invoicing and tax reporting is accurate and up to date.


<span id="230fd586"></span>
## 6. Service availability and exclusions

Service\-level commitments, where applicable, are governed by the separate Service Level Agreement (SLA). You can find the SLA for Viking AI Search here: [SLA for Viking AI Search](https://docs.byteplus.com/en/docs/legal/SLA_for_Viking_AI_Search)

<span id="f7ded590"></span>
## 7. Changes to this document

BytePlus may update this document from time to time. Material changes that adversely affect existing customers will be announced at least 30 days before they take effect, through the BytePlus Console, the BytePlus documentation site, or by email to the account billing contact. The version of this document in effect on the date of the customer's order shall govern that order for the duration of its billing month. Renewal orders are governed by the version in effect on the renewal date.

<span id="20b8e4f1"></span>
## 8. Billing inquiries

For questions about a specific charge, invoice, or billing event, the customer may submit a ticket through the BytePlus Console under **Support → Submit a Ticket**, selecting **Billing**  **& Payments ** as the category.
