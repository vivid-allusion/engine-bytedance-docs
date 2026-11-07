---
title: "OCI artifact repository quota"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/repository-quota"
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



* <div data-tips="true" data-tips-type="tip">Each scale\-out of the OCI artifact repository increases the quota by 1,000 units.</div>


* <div data-tips="true" data-tips-type="tip">The maximum limit for the OCI artifact repository is 10,000 units. For example, if the default OCI artifact repository quota for a Standard Edition instance is 3,000 units, you can scale it out by up to 7,000 units. The scaled\-out 7,000 OCI artifact repository units will incur charges.</div>


* <div data-tips="true" data-tips-type="tip">Longer subscription periods (e.g., annual) come with greater discounts. For specific discount ratios, please refer to the Purchase page in the console.</div>




|Billing item |Description |Billing method |Unit Price ||
|---|---|---|---|---|
||||Chinese mainland region |China (Hong Kong) and other regions |
|OCI artifact repository quota |Charged based on the number and duration of the scaled\-out OCI artifact repositories. |Pay\-as\-you\-go billing |USD 0.01971/1000 units/hour |USD 0.02571/1000 units/hour |
||Charged based on the number and monthly subscription duration of the scaled\-out OCI artifact repositories. |Subscription |USD 13.70/1000 units/month |USD 20/1000 units/month |


<span id=".5omp5a655pa55rOV"></span>
## Scaling\-out Method

On the **Quota Usage** section of the instance overview page, click **Quota Scale\-out** to log in to the quota change page and complete the quota scale\-out.
