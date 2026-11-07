---
title: "Deleting a Virtual Interface"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Deleting-the-virtual-interface"
---

You can promptly delete unused Virtual Interfaces to release network resources. When a Virtual Interface is deleted, its dependent configurations will be deleted accordingly, and its associated DC Connections and DC Gateways will be detached.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Deletion is irreversible. Deleted data and deleted Virtual Interfaces cannot be restored.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* If a Virtual Interface to be deleted is the only interface of a Direct Connect (DC) Gateway, confirm that the DC Gateway is unloaded from the Cloud Enterprise Network (CEN), and then delete the Virtual Interface. For procedure, see [Cancel cross-account authorization](https://docs.byteplus.com/en/docs/directconnect/Cross-account-authorization#.6Kej6Zmk6Leo6LSm5Y-35o6I5p2D).

* Confirm that the Direct Connect Gateway to be deleted has no static route entries or BGP Peers. If present, first [delete the static route entries](https://docs.byteplus.com/en/docs/directconnect/Managing_Direct_Connect_Gateways#.5Yig6Zmk6YWN572u) and [delete the BGP Peers](https://docs.byteplus.com/en/docs/directconnect/Managing_Direct_Connect_Gateways#.5Yig6Zmk6YWN572u).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [DC Virtual Interface console](https://console.byteplus.com/dc/VirtualInterface).

2. In the top menu bar, select the region where the target Virtual Interface is deployed.

3. In the Virtual Interface list, click **Delete** in the **Actions** column of the target Virtual Interface.

4. In the pop\-up dialog box, confirm the information is correct, and click **Delete** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

[DeleteDirectConnectVirtualInterface](https://docs.byteplus.com/en/docs/directconnect/DeleteDirectConnectVirtualInterface): Delete the specified Virtual Interface instance.
