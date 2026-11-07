---
title: "Namespace Quota"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/namespace-quota"
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



* <div data-tips="true" data-tips-type="tip">Each scale\-out of the namespace increases the quota by 10 units.</div>


* <div data-tips="true" data-tips-type="tip">The maximum number of namespaces is 300. For example, if the default namespace quota for a Standard Edition instance is 50, you can scale it out by up to 250 namespaces. The scaled\-out 250 namespace will incur charges.</div>


* <div data-tips="true" data-tips-type="tip">Longer subscription periods (e.g., annual) come with greater discounts. For specific discount ratios, please refer to the Purchase page in the console.</div>




|Billing item |Description |Billing method |Unit Price ||
|---|---|---|---|---|
||||Chinese mainland |China (Hong Kong) and other regions |
|Namespace Quota |Charged based on the number and duration of the scaled\-out namespaces. |Pay\-as\-you\-go billing |USD 0.01/10 units/hour |USD 0.01286/10 units/hour |
||Charged based on the number and monthly subscription duration of the scaled\-out namespaces. |Subscription |USD 6.85/10 units/month |USD 10/10 units/month |


<span id="0fvYFQsO"></span>
## Scaling\-out Method

On the **Quota Usage** section of the instance overview page, click **Quota Scale\-out** to log in to the quota change page and complete the quota scale\-out.
