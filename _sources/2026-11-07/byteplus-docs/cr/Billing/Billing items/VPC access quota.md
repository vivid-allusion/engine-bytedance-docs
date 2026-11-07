---
title: "VPC access quota"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/vpc-quota"
---

If the standard quota in your current instance does not meet your business requirements, you may apply for quota scale\-out. The scaled\-out portion will incur corresponding charges.

<span id=".6K6h6LS56KeE5YiZ"></span>
## Billing Rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Only <strong>Standard Edition instances</strong> support quota scale\-out.</div>


* <div data-tips="true" data-tips-type="warning">Once the quota scale\-out is completed, <strong>scale\-in is not supported</strong>.</div>


* <div data-tips="true" data-tips-type="warning">Only the scaled\-out quota is charged; the standard quota is free of charge. For standard quota details, see <a href="https://docs.byteplus.com/en/docs/cr/limits">Limits</a>.</div>



The specific charging rules are as follows:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The increment for each VPC access quota scale\-out is 1.</div>


* <div data-tips="true" data-tips-type="tip">The maximum VPC access quota is 20. For example, the default VPC access quota for a Standard Edition instance is 5, so you can expand up to 15 additional VPC access quotas. The cost is charged for the 15 expanded VPC access quotas.</div>


* <div data-tips="true" data-tips-type="tip">Longer subscription periods (e.g., annual) come with greater discounts. For specific discount ratios, please refer to the Purchase page in the console.</div>




|Billing item |Description |Billing method |Unit Price ||
|---|---|---|---|---|
||||Chinese mainland |China (Hong Kong) and other regions |
|VPC access quota |Billing is based on the number and duration of the scaled\-out VPC access quotas. |Pay\-as\-you\-go billing |USD 0.01286/unit/hour |USD 0.01714/unit/hour |
||Billing is based on the number and monthly subscription duration of the scaled\-out VPC access quotas. |Subscription |USD 8.85/unit/month |USD 12.5/unit/month |


<span id="EmpfjWwb"></span>
## Scaling\-out Method

On the **Quota Usage** section of the instance overview page, click **Quota Scale\-out** to log in to the quota change page and complete the quota scale\-out.
