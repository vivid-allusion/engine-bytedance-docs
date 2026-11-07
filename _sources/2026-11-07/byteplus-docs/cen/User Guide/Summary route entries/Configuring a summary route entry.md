---
title: "Configuring a summary route entry"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/Summary-route-entries-01"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

When multiple Virtual Private Cloud (VPC) interconnect with an on\-premises IDC, excessive cloud routes can occupy significant routing table space on the IDC switches, leading to complex and hard\-to\-manage routing configurations in the on\-premises environment. Configuring summary route entries can significantly reduce the number of cloud routes, simplifying the routing table in the on\-premises IDC and improving manageability.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The summary route entry is currently in beta stage. If you need a trial, please contact your account manager.</div>


<span id=".5pON5L2c6K-05piO"></span>
## Action notes


* If the target CIDR block of the summary route entry is broader than that of the original cloud routes, some traffic may be discarded.

* Once successfully configured, summary route entries are published to the Direct Connect gateway routing table. You can view them by [Checking the Direct Connect gateway routes](https://docs.byteplus.com/en/docs/directconnect/Managing_Direct_Connect_Gateways).

* Summary routes do not participate in route selection. When a summary route conflicts with an instance route, the instance route takes precedence.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. Log in to the [CEN console](https://console.byteplus.com/cen/EnterpriseNetwork).

2. Click the target CEN instance name.

3. In the **Summary route** tab, click **Configure summary route** and input the Destination CIDR Block.

4. Click **Configure** to complete the action.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

For more details, see [Best practices for summary route configuration](https://docs.byteplus.com/en/docs/cen/Summary-route-entry-configuration-practice).

<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[CreateCenSummaryRouteEntry](https://docs.byteplus.com/en/docs/cen/CreateCenSummaryRouteEntry)
