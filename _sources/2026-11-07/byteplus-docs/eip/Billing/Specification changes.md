---
title: "Specification changes"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/Bandwidth-modifications"
---

After the creation of an Elastic IP Address (EIP) instance, you can modify the EIP bandwidth cap anytime according to your actual business needs.

**Upgrade**: Increase the bandwidth cap.

**Downgrade**: Decreases the bandwidth cap.

**Billing cycle**: the billing period for executing the modification.

<span id=".5bi46KeE5Y-Y6YWN"></span>
## Normal modification

Regular Modify Spec refers to regularly modifying the maximum bandwidth of an EIP. The new bandwidth remains until the next modification or resource release.


|Item |Subscription |Pay\-by\-bandwidth |Pay\-by\-data\-transfer |
|---|---|---|---|
|Fee description |The fees displayed in the console shall prevail. |Change cycle fee equals the sum of the pre\-change and post\-change usage fees. |The fees displayed in the console shall prevail. |
|Billing formula |Refer to [Resource Subscription Change](https://docs.byteplus.com/en/docs/byteplus-platform/Billing_Rules_for_Resource_Subscription_Change#.5LiA44CB5Y-Y5pu05YyF5bm05YyF5pyI6LWE5rqQ6KeE5qC8). |Change cycle fee = Original bandwidth unit price (USD/hour) × Original usage duration (hours) + Changed bandwidth unit price (USD/hour) × Changed usage duration (hours).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Usage duration accurate to seconds.</div><br> |Refer to [Pay-by-data-transfer](https://docs.byteplus.com/en/docs/eip/Pay-as-you-go#.5oyJ5a6e6ZmF5rWB6YeP6K6h6LS5). |
|Effective period |Effective immediately. |Effective immediately. |Effective immediately. |
|Related documents |Refer to [Modify the maximum bandwidth > Normal modification](https://docs.byteplus.com/en/docs/eip/Modifying-the-maximum-bandwidth#.5bi46KeE5Y-Y6YWN). |||


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Decreasing maximum bandwidth may affect business traffic and lead to packet loss. Evaluate the possible impacts on your business and proceed with caution.</div>
