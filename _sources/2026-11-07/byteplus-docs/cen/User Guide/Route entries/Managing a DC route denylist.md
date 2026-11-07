---
title: "Managing a DC route denylist"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/Managing-Direct-Connect-route-denylist"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

You can configure a Direct Connect Route Denylist to prevent routes within the Cloud Enterprise Network (CEN) from being advertised to the loaded Direct Connect Gateway(s).

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits

By default, a single CEN instance can have a maximum of 100 Direct Connect Route Denylist entries. If the default quota does not meet your needs, please contact your account manager.

<span id=".6YWN572u5LiT57q_6Lev55Sx6buR5ZCN5Y2V"></span>
## Configure Direct Connect route denylist

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Once configured, if a route's CIDR block in the CEN exactly matches a CIDR block in the denylist, that route will be blocked from being published to the Direct Connect Gateway. Any route already published will be automatically withdrawn.</div>



1. Log in to the [CEN console](https://console.byteplus.com/cen/EnterpriseNetwork).

2. In the top navigation bar, select the target project.

3. Click the target CEN instance name.

4. On the **Direct Connect route denylist** tab, click **Configure Direct Connect route denylist** and input the Destination CIDR Block of the routes to be blocklisted from being advertised to the Direct Connect Gateway.

5. Click **Configure** to complete the action.


<span id=".5Yig6Zmk5LiT57q_6Lev55Sx6buR5ZCN5Y2V"></span>
## Delete Direct Connect route denylist

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Routes previously blocked due to an exact match with a denylist entry will be re\-advertised to the Direct Connect Gateway after the corresponding denylist entry is deleted.</div>



1. Log in to the [CEN console](https://console.byteplus.com/cen/EnterpriseNetwork).

2. In the top navigation bar, select the target project.

3. Click the target CEN instance name.

4. In the **Direct Connect route denylist** tab, click **Delete** on the right side of the target route denylist.

5. Click **Delete** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [CreateCenRouteBlockRule](https://docs.byteplus.com/en/docs/cen/CreateCenRouteBlockRule)

* [DescribeCenRouteBlockRules](https://docs.byteplus.com/en/docs/cen/DescribeCenRouteBlockRules)

* [ModifyCenRouteBlockRuleAttributes](https://docs.byteplus.com/en/docs/cen/ModifyCenRouteBlockRuleAttributes)

* [DeleteCenRouteBlockRule](https://docs.byteplus.com/en/docs/cen/DeleteCenRouteBlockRule)
