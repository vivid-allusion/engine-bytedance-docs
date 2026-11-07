---
title: "Specification changes"
product: "IPv6 Gateway"
product_code: "IPv6"
source: "https://docs.byteplus.com/en/docs/IPv6/Bandwidth_modifications"
---

You can adjust the maximum IPv6 Internet bandwidth at any time to meet diverse business scenarios.

<span id=".6KeE5qC85Y-Y5pu06K-05piO"></span>
## Specification changes


|Item |Pay\-by\-bandwidth\-cap |Pay\-by\-data\-transfer |
|---|---|---|
|Specification limits |Supports both increasing and decreasing the maximum bandwidth ||
|Bandwidth cap |1\-1000 Mbps |1\-200 Mbps |
|Formula |Cycle change fee = Fees in original billing cycle + Fees in changed billing cycle<br><br><br>* Fees in original billing cycle = Bandwidth unit price (USD/hour per Mbps) × Original usage duration (hours) × Original maximum bandwidth (Mbps)<br><br>* Fees in changed billing cycle = Bandwidth unit price (USD/hour per Mbps) × Changed usage duration (hours) × Changed maximum bandwidth (Mbps)<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Usage duration is accurate to seconds.</div><br> |See [Pay-by-data-transfer](https://docs.byteplus.com/en/docs/IPv6/Pay-as-you-go#.5oyJ5a6e6ZmF5rWB6YeP6K6h6LS5) |
|Effective time |Instant effect ||
|Related documentation |[Modifying IPv6 Internet bandwidth](https://docs.byteplus.com/en/docs/IPv6/Modify_the_IPv6_internet_bandwidth) ||


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Decreasing bandwidth cap may affect business traffic and lead to packet loss. Evaluate the possible impacts of the action on your business and proceed with caution.</div>
