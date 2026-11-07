---
title: "Data verification billing method"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Data_verification_billing_method"
---

This topic describes the billing method and standards for the data verification task of Database Transmission Service (DTS).

<span id=".6K6h6LS55pa55byP"></span>
## Billing method

Among the data verification methods supported, only the following two are currently charged:


* Content validation for full validation: Full data verification currently only supports the pay\-as\-you\-go (post\-payment) billing method.

* Increment validation: The increment validation task currently only supports the pay\-as\-you\-go (post\-payment) billing method.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Other verification methods are currently in the promotion period and are not charged. After the promotion period, billing will be based on actual usage.</div>


<span id=".6K6h6LS55qCH5YeG"></span>
## Billing standards

Data verification supports the following verification methods:


* Full validation: Full validation supports the following verification methods.

   * Content validation: Full data verification is charged based on the amount of source data. The amount of source data is the amount of data obtained by compressing the source instance data using Hash. Paused and failed verification tasks are still billable.

   * Row verification: Not charged for now.

   * Primary key validation: Not charged for now.

* Schema verification: No fee is charged temporarily.

* Increment validation: Increment validation is charged based on the verification duration. Paused and failed verification tasks are still billable.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The actual cost is subject to the purchase page and the bill.</div>
