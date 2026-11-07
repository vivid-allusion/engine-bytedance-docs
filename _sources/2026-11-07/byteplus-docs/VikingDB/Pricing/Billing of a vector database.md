---
title: "Billing of a vector database"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Billing_of_a_vector_database"
---

<span id="Billing of a vector database"></span>
# Vector database billing

<span id="e699c51b"></span>
# Billing overview

This topic describes the billing method, billing cycle, and billing items of a vector database.

<span id="4fe125c2"></span>
## Billing method

A vector database supports pay\-as\-you\-go, a postpaid billing method that allows you to use the product first and pay later. The fees are included in your bill. You can settle the bill after it is issued.

<span id="5615f3cc"></span>
## Billing cycle

A vector database is billed hourly for settlement based on the usage of all its billing items.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Once <strong>you create a vector database index</strong>, the system automatically reserves exclusive compute resources and starts billing in real time.</div>


<span id="6e124d51"></span>
## Billing items


|**Billing Item** |**Description** |**Measurement** |**Unit Price** |
|---|---|---|---|
|compute |Building indexes, automated optimization analysis, and computational resources required for online retrieval. |Measured in Compute Units (CU), the computing resources contained in 1 CU are 8 GB of memory and 1 CPU Core. The calculation formula is CU = MAX(CPU, MEM / 8). When the memory used is greater than 8 times the memory corresponding to 1 CPU Core, the CU usage is calculated by dividing the consumed memory amount by 8. |0.25 USD/CU/hour |
|storage |The storage resources required for vectors and the data attributes related to vectors. |Measured in gigabytes (GB) occupied. |0.002USD/GB/hour |
|Pic_embedding |Provides graphic and text vector services to help developers quickly convert graphic and text data into vector data. It can perform individual encoding on text or images, or joint encoding on text\-image pairs, and output dense vectors with 1024 dimensions. |It is measured by the input tokens. Generally, one Chinese character, one English letter, one digit or one symbol is counted as one token, and one picture is equivalent to 900 tokens. |0.00015/USD/K tokens |
|text_embedding (Multifunctional) |Provides text vector services to assist developers in quickly converting text data into vector data. It supports multiple languages and long texts, and enables the simultaneous construction and retrieval of both sparse and dense indexes. |It is measured by the input tokens. Generally, one Chinese character, one English letter, one digit or one symbol is counted as one token. |0.00015/USD/K tokens |
|text_embedding |Provides text vector services to help developers quickly convert text data into vector data. |It is measured by the input tokens. Generally, one Chinese character, one English letter, one digit or one symbol is counted as one token. |0.00015/USD/K tokens |


<span id="9ae2013d"></span>
# Arrears

If the sum of the balance and coupons in your account is less than the payable amount of your bill, your account will be considered in arrears and you will receive an SMS or email reminder. This topic introduces what happens to your resources and what actions you can take when your account is in arrears.

Please top up your account and settle the overdue bill within **24** hours of your account going into arrears, or you will no longer be able to use the vector database services.

When your account is in arrears, the service status of a vector database changes as follows:

If the arrears duration is within **24** hours, the service keeps running and is billed normally.

If the arrears duration is between **24** hours and **168** hours, the service is suspended. However, your data and resources are retained and the service is still billed.

If the arrears duration is beyond **168** hours, relevant resources and data are released and cannot be recovered.

If you settle all overdue bills within **168** hours of your account going into arrears, the service is resumed.

<span id="fc310054"></span>
# Taxes and invoices

Please note that all prices listed for products or services on BytePlus include the value\-added tax (VAT), unless otherwise stated. Any changes in the VAT rate during the provision of services or usage of products, which are subject to amendments in the national tax policies, will lead to an adjustment in the applicable VAT rate for products or services on BytePlus to comply with the new policies. However, the VAT\-exclusive prices will remain unaffected.

We offer equivalent VAT invoices based on successful subscription orders or issued bills under your BytePlus account. You can request VAT invoices from BytePlus Console \> Billing \> Invoice or through other channels updated by BytePlus. We will issue the VAT invoice in a timely manner after receiving your request. If the agreement of the service you use is inconsistent with this agreement or if the parties have made alternative arrangements, the terms and conditions specified in the service\-specific or separate agreement shall prevail. With respect to services settled periodically by usage, the company reserves the right to require credit credentials, advance payments, deposits, or any other conditions deemed necessary by the company for the purpose of activation and subscription.

We will issue VAT invoices based on the products or services you buy according to the following invoice content:


|**Product/Service** |**Service/License Duration** |**Invoice Content** |**Tax Rate** |
|---|---|---|---|
|Vector database (public cloud edition) |Subject to the actual service or license duration. |Technical service fee of *information technology service* |6% |
