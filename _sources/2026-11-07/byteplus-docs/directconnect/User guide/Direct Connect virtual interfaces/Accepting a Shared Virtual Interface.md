---
title: "Accepting a Shared Virtual Interface"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Accept-shared-Direct-Connect-Virtual-Interface"
---

To use a Shared Virtual Interface, you need to accept it before using. This topic describes how to accept a Shared Virtual Interface.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Before you go


* The creator (Account A) has created a Shared Virtual Interface for the user (Account B). For procedure, see [Creating a Shared Virtual Interface](https://docs.byteplus.com/en/docs/directconnect/Create-shared-Direct-Connect-Virtual-Interface).

* The user of the Shared Virtual Interface (Account B) has created a Direct Connect (DC) Gateway instance in the same region as the Shared Virtual Interface. For procedure, see [Creating a Direct Connect Gateway](https://docs.byteplus.com/en/docs/directconnect/Creating-a-Direct-Connect-gateway-1).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The Shared Virtual Interface is currently in the beta stage. If you need a trial, please contact your account manager.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Use Account B to log in to the BytePlus [DC Virtual Interface console](https://console.byteplus.com/dc/VirtualInterface).

2. In the top menu bar, select the region where the target Virtual Interface is deployed.

3. In the virtual interface list of this region, display a Shared Virtual Interface whose status is **Pending acceptance**.

4. Click **Accept** in the Actions column of the pending Shared Virtual Interface.

5. Select the project and specific DC Gateway. This DC Gateway will be attached to the Shared Virtual Interface.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can only use DC Gateways in the same region as the Shared Virtual Interface. If no eligible DC Gateways exist, you can click <strong>Create DC Gateway</strong> to create a new DC Gateway that meets your needs.   </div>
   

6. After configuration, click **Accept**.


<span id=".5ZCO572u5pON5L2c"></span>
## What to do next

After accepting the Shared Virtual Interface, the user (Account B) also needs to configure routing parameters based on the route type of the Shared Virtual Interface:


* [Add a BGP Peer](https://docs.byteplus.com/en/docs/directconnect/Adding-a-BGP-peer): For a Shared Virtual Interface with **BGP**, add a BGP Peer on the on\-premises data center side

* [Add a static route](https://docs.byteplus.com/en/docs/directconnect/Adding-a-static-route-entry): For a Shared Virtual Interface with **Static**, add a static route on the on\-premises data center side


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

[ConfirmDirectConnectVirtualInterface](https://docs.byteplus.com/en/docs/directconnect/ConfirmDirectConnectVirtualInterface): Accept a Shared Virtual Interface.
