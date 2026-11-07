---
title: "Limitations"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/Product-Overview-04"
---

This topic describes the default quota limits for Cloud Enterprise Network (CEN) resources under a single account and the quota items that can be adjusted for CEN.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For the adjustable quota items listed in the table below, if the default quota is insufficient, you can go to the <a href="https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=CEN">Quota Center</a> to request an increase for the corresponding quota.</div>


<span id=".6YWN6aKd6ZmQ5Yi2"></span>
## Quota limitations


|Classification |Quota parameter |Description |Maximum |Adjustable |Adjustable quota limit |
|---|---|---|---|---|---|
|&nbsp;<br><br>Create |cen |Maximum number of CEN instances that can be created under a single account |5 |&nbsp;<br><br>Yes |25 |
||cenbandwidthpackage |Maximum number of bandwidth packages that can be created under a single account |10 ||100 |
|&nbsp;<br><br>Loading |None |Maximum number of CEN instances to which a single network instance can be attached |1 |No |\-\- |
||cen/attachedinstance |Maximum number of network instances that can be attached to a single CEN instance within a single region |10 |&nbsp;<br><br>Yes |100 |
|&nbsp;<br><br>Association |None |Maximum number of bandwidth packages for a specified interconnected region that can be associated with a single CEN instance |1 |&nbsp;<br><br>No |&nbsp;<br><br>\-\- |
|||Maximum number of CEN instances that can be associated with a single bandwidth package |1 |||
|&nbsp;<br><br>&nbsp;<br><br>Routes |cen/routeentry |Maximum number of route entries supported by a single CEN instance<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This count includes the created cloud service access routes. Once the total number of routes reaches this maximum limit, any newly added route entries will be automatically discarded by the CEN instance.</div><br> |200 |Yes |1000 |
||&nbsp;<br><br>none |Maximum AS_PATH length of BGP routes that a single CEN instance can receive |200 |No |\-\- |
|||Maximum number of Summary Route Entries that can be configured for a single CEN instance<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Summary Route Entry is currently in Beta stage. If you need a trial, please contact your account manager.</div><br> |8 |No |\-\- |
|&nbsp;<br><br>Others |&nbsp;<br><br>None |Maximum bandwidth capacity for a single bandwidth package |10000Mbps |No |\-\- |
|||Maximum number of identical local\-and\-peer region pairs that can be configured within the same bandwidth package |1 |||
|||Maximum number of tags that can be added to a single CEN instance or bandwidth package |50 |||


<span id="82QNS5Bm"></span>
## Other limitations

The routing of network instances attached to the same CEN instance is subject to the following limitations:


* The subnet CIDR blocks of different VPC instances must not overlap.

* The destination CIDR blocks of the Direct Connect Gateway routes must not conflict with the subnet CIDR blocks of the VPC instances.
