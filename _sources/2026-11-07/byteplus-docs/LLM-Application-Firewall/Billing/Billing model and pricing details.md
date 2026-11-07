---
title: "Billing model and pricing details"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/billing_model_and_pricing_details"
---

To help you select the most cost\-effective plan for your needs, this document details the billing modes for the LLM Application Firewall service. It provides a complete breakdown of the subscription and pay\-as\-you\-go options, including specific pricing for billable items like text detection, image detection, and log services. You can also find information on how to change, renew, or cancel your plan.

<span id="8bbf939d"></span>
## **Billing modes**

LLM Application Firewall offers two flexible billing modes to meet the usage needs of different users:


|Billing mode |Purchase methods |Applicable scenarios |Key advantages |
|---|---|---|---|
|Annual and monthly subscription |Purchase prepaid packages |Businesses with relatively stable usage |Predictable costs, better pricing |
|Pay\-as\-you\-go |Pay fees based on actual hourly usage |For businesses with fluctuating usage or those in an initial trial period. |pay\-as\-you\-go, no minimum spend required |


<span id="9ee9e8b7"></span>
## Subscription

The annual and monthly subscription mode offers four package options to meet the requirements of businesses of different sizes.


|Item |Basic edition |Standard edition |Advanced edition |Enterprise edition |
|---|---|---|---|---|
|Asset |10 assets |50 assets |100 assets |500 assets |
|Custom model |/\- |/\- |/\- |5 |
|Text detection |10 QPS |50 QPS |100 QPS |500 QPS |
|Image detection |/\- |/\- |/\- |5 QPS |
|Document detection |/\- |/\- |/\- |5 QPS |
|Text regeneration |/\- |/\- |/\- |5 QPS |
|Blocklist (allowlist) access control policy |100 policies |1,000 policies |1,000 policies |1,000 policies |
|Resource exhaustion mitigation policy |/\- |/\- |1,000 policies |1,000 policies |
|Prompt injection protection policy |100 policies |1,000 policies |1,000 policies |1,000 policies |
|Model abuse prevention policy |100 policies |1,000 policies |1,000 policies |1,000 policies |
|Sensitive data disclosure prevention policy |/\- |/\- |1,000 policies |1,000 policies |
|Topic control policy |/\- |/\- |100 policies |100 policies |
|Custom detection policy |1,000 policies |1,000 policies |1,000 policies |1,000 policies |
|Custom watch list policy |100 policies |100 policies |100 policies |100 policies |
|Custom watch list prompts |10,000 prompts |10,000 prompts |10,000 prompts |10,000 prompts |
|Custom response policy |/\- |/\- |/\- |100 policies |
|Log capacity |1 TB |5 TB |10 TB |50 TB |
|Costs |$320 USD/month |$2250 USD/month |$7500 USD/month |$21500 USD/month |


<span id="8e90bbb0"></span>
## Pay\-as\-you\-go

Under the pay\-as\-you\-go mode, the LLM Application Firewall provides fixed specification protection capabilities and charges based on actual hourly usage. Billing items include fees for text and image detection, text response generation, and log services.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div>



* <div data-tips="true" data-tips-type="warning">The postpaid service takes effect immediately upon successful purchase. The validity period is calculated from the date the order is successfully placed in the console, and the specific time is based on the records of the platform.</div>


* <div data-tips="true" data-tips-type="warning">Postpaid services do not support any form of refund.</div>


* <div data-tips="true" data-tips-type="warning">If your account has an overdue balance, your service will be suspended.</div>



<span id="643f4e1f"></span>
### Package specifications

LLM Application Firewall pay\-as\-you\-go edition instances currently provide the following basic capabilities:


* 100 assets

* 5 QPS for text regeneration

* 100 QPS for text detection

* 5 QPS for image detection

* 1,000 blocklist (allowlist) access control policies

* 1,000 resource exhaustion mitigation policies

* 1,000 prompt injection protection policies

* 1,000 model abuse prevention policies

* 1,000 sensitive data disclosure prevention policies

* 100 topic control policies

* 10,000 custom watch list policies


<span id="91cdabb9"></span>
### **Billing items**

Fees are charged hourly. The content detection and response generation fees are based on the number of requests, while the log service fee is based on your actual log usage.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="warning">The LLM Application Firewall bills for user prompt inputs or model response outputs for relevant assets based on the rules you configure:</div>



* <div data-tips="true" data-tips-type="warning">If you want to detect only user prompt inputs, configure the input detection classification for the corresponding policy; if you want to detect only model response outputs, configure the output detection classification for the corresponding policy.</div>


* <div data-tips="true" data-tips-type="warning">Resource exhaustion mitigation and prompt injection protection policies are billed based on input content only.</div>



For detailed explanations of billing items, refer to the table below.


|Billing item |Settlement period |Unit price |Description |
|---|---|---|---|
|Text detection |Per hour |$0.38 USD per 1,000 requests |* This fee is incurred when you send text content to the LLM Application Firewall for detection.<br><br>* Billing example: For 1,800 requests detected within a single hour, the fee for text detection for that hour is: `0.38 * (1800 / 1000) = $0.684 USD`. |
|Image detection<br><br>  |Per hour |$0.75 USD per 1,000 images |* This fee is incurred when you send image content to the LLM Application Firewall for detection.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="default"></div><br><br><br><br>* Billing example: For 1,800 images detected within a single hour, the fee for detection in that hour is: `0.75 * (1800 / 1000) = $1.35 USD`. |
|Text regeneration |Per hour |$28 USD per 1,000 requests<br><br>  |* You can use the secure response generation plugin of the Large Model Application Firewall to generate safe and reliable answers and return them to the client. This process incurs response generation fees.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div><br><br><br><div data-tips="true" data-tips-type="warning">The plugin now supports online search, enabling real\-time access to the latest information and ensuring the accuracy and timeliness of the service.</div><br><br><br><br>* Billing example: With 10 response generations within a single hour, the fee for that hour is: `28 * (10 / 1000) = $0.28 USD`. |
|Log service |Per hour |$0.03 USD/TB |* The LLM Application Firewall records logs for all requests, allowing you to query and analyze them at any time. This fee is calculated based on the total volume of logs you currently store.<br><br>* Billing example: If your total log storage is 3 TB for one hour, the log storage service fee for that hour is `0.03 * 3 = $ 0.09 USD`. If the total log storage increases by 1 TB to 4 TB in the next hour, the log storage service fee for that hour is `0.03 * 4 = $ 0.12 USD`. |


<span id="74f49df5"></span>
### Billing examples

Assume you have purchased a pay\-as\-you\-go instance of the LLM Application Firewall. The usage for a particular hour is as follows:


* The number of requests for text detection is 1,218.

* Text responses were generated 28 times.

* Log usage is 2 TB.


The total cost for this hour is: 0.38 \* 1,218/1000 + 28 \* 28/1000 + 0.03 \* 2 = 0.46284 + 0.784 + 0.06 = $1.30684 USD.

<span id="71b640f9"></span>
## FAQ

<span id="e6d967c9"></span>
### How to choose a billing mode?

If your business usage is relatively stable and you want fixed and controllable costs, we recommend that you choose the annual and monthly subscription mode. If your business is in its early stages, has fluctuating usage, or you want to try the product first, we recommend that you choose the pay\-as\-you\-go mode.

<span id="ffa43e7b"></span>
### How are detection and regeneration requests calculated?

We calculate the number of detection or regeneration based on the type and quantity of the content, according to the following rules:


* **Text content**: The number of requests is calculated based on the number of tokens in the content for detection or regeneration. One request is counted for every 1,000 tokens, and content with fewer than 1,000 tokens is also counted as one request. If your content exceeds 1,000 tokens, the system splits it to calculate the number of requests. For example:

   * A submission containing 800 tokens is counted as one detection request.

   * A submission containing 1,200 tokens is counted as two detection requests.

* **Image content**: The number of requests is calculated based on the number of submitted images, and each image is counted as one request.

* **Document content**: The number of requests is calculated based on the number of submitted documents, and each document is counted as one request.


<span id="538ba543"></span>
### **What is a token for detected or regenerated content?** 

You can think of a token as the smallest unit of language that a large model processes, including Chinese characters, words, and punctuation marks. For example, a common Chinese character might be counted as 1 token, and a common phrase might also be counted as 1 token. The specific calculation method varies depending on the tokenization strategy of the large model.

<span id="baW1WqlKHv"></span>
### How to view the billing count for each detection or regeneration request?

You can go to [Log details](https://console.byteplus.com/omni-shield/llm-shield/region:llm-shield+ap-southeast-1/tls-log) to view the details of relevant log records, including the billing count, to calculate your usage costs. For an explanation of the log fields, see [Log field descriptions](https://docs.byteplus.com/docs/LLM-Application-Firewall/Log_field).

<span id="ZXUrQRZYgk"></span>
### Does it support multi\-modal hybrid detection?

LLM Application Firewall supports the hybrid detection of text, images, and documents. You can combine multi\-modal content in a single task for detection. For specific operation methods and limitations, see [Check whether input or output content is compliant](https://docs.byteplus.com/docs/LLM-Application-Firewall/Check_whether_input_or_output_content_is_compliant).
