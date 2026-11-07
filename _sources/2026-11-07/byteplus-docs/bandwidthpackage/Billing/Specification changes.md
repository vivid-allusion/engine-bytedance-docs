---
title: "Specification changes"
product: "Bandwidth Package"
product_code: "bandwidthpackage"
source: "https://docs.byteplus.com/en/docs/bandwidthpackage/Bandwidth-modifications"
---

You can adjust the maximum bandwidth of Bandwidth Package instance at any time to meet diverse business scenarios.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Decreasing bandwidth cap may affect business traffic and lead to packet loss. Evaluate the possible impacts of the action on your business and proceed with caution.</div>


<span id=".6KeE5qC85Y-Y5pu06K-05piO"></span>
## Specification changes


|Item |Pay\-by\-bandwidth |Subscription |Pay\-by\-main\-traffic |Pay\-by\-95th\-peak |
|---|---|---|---|---|
|Specification limits |Supports both increasing and decreasing the maximum Internet bandwidth |Support increasing the maximum bandwidth only |Supports both increasing and decreasing the maximum Internet bandwidth |Supports both increasing and decreasing the maximum bandwidth |
|Bandwidth cap |2\-5000 Mbps |5\-5000 Mbps |2\-2000 Mbps |2\-5000 Mbps |
|Formula |Cycle change fee = Fees in original billing cycle + Fees in changed billing cycle<br><br><br>* Fees in original billing cycle = Bandwidth unit price (USD/hour per Mbps) × Original usage duration (hours) × Original maximum bandwidth (Mbps)<br><br>* Fees in changed billing cycle = Bandwidth unit price (USD/hour per Mbps) × Changed usage duration (hours) × Changed maximum bandwidth (Mbps) |See [Specification change for Subscription resources](https://docs.byteplus.com/en/docs/byteplus-platform/Billing_Rules_for_Resource_Subscription_Change#.5LiA44CB5Y-Y5pu05YyF5bm05YyF5pyI6LWE5rqQ6KeE5qC8) |See [Pay-by-main-traffic](https://docs.byteplus.com/en/docs/bandwidthpackage/Pay-by-domain-traffic#.6K6h6LS55YWs5byP) |See [Pay-by-95th-peak](https://docs.byteplus.com/en/docs/bandwidthpackage/Pay-by-traditional-95th-percentile#.6K6h6LS55YWs5byP) |
|Effective time |Instant effect ||||
|Related documents |[Modifying the maximum bandwidth](https://docs.byteplus.com/en/docs/bandwidthpackage/Modifying-the-maximum-bandwidth) ||| |
