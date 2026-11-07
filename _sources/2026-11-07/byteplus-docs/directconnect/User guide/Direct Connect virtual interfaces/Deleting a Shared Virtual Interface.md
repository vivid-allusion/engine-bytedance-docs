---
title: "Deleting a Shared Virtual Interface"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Delete-shared-Direct-Connect-Virtual-Interface"
---

This topic describes how to delete a Shared Virtual Interface.

<span id=".5L2_55So5pa55Yig6Zmk5YWx5Lqr6Jma5ouf5o6l5Y-j"></span>
## Delete a Shared Virtual Interface by a user

As the user of a Shared Virtual Interface, if you no longer need to use the Shared Virtual Interface or the configuration does not meet your requirements, you can delete the Shared Virtual Interface.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Deleting a Shared Virtual Interface from the user's console does not remove the Shared Virtual Interface from the creator. That is, the creator can still view the Shared Virtual Interface in the list.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites


* The creator (Account A) has created a Shared Virtual Interface for the user (Account B). For procedure, see [Creating a Shared Virtual Interface](https://docs.byteplus.com/en/docs/directconnect/Create-shared-Direct-Connect-Virtual-Interface).

* The user of Shared Virtual Interface can only delete Shared Virtual Interfaces with the following statuses:

   * Unaccepted Shared Virtual Interfaces.

   * Accepted Shared Virtual Interfaces without configured BGP Peers or static routes.

   * If you no longer need Shared Virtual Interfaces that are accepted and configured with BGP Peers or static routes, delete all BGP Peers or static routes first and then delete the Shared Virtual Interface. For procedure, see [Delete BGP Peer](https://docs.byteplus.com/en/docs/directconnect/Managing_Direct_Connect_Gateways#.5Yig6Zmk6YWN572u) or [Delete static route](https://docs.byteplus.com/en/docs/directconnect/Managing_Direct_Connect_Gateways#.5Yig6Zmk6YWN572u).


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Use Account B to log in to the BytePlus [DC Virtual Interface console](https://console.byteplus.com/dc/VirtualInterface).

2. In the top menu bar, select the region where the target Virtual Interface is deployed.

3. In the Virtual Interface list, click **Delete** in the **Actions** column of the target Shared Virtual Interface.

4. In the pop\-up dialog box, confirm that the information is correct, and then click **Delete**.


<span id=".5Yib5bu65pa55Yig6Zmk5YWx5Lqr6Jma5ouf5o6l5Y-j"></span>
## Delete a Shared Virtual Interface by a creator

As the creator of a Shared Virtual Interface, you can delete Shared Virtual Interfaces to release network resources if your created Shared Virtual Interfaces are deleted or not accepted by users.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Once a Shared Virtual Interface is deleted from the creator's console, it is permanently deleted and unrecoverable. We recommend that you confirm with the Shared Virtual Interface user (Account B) before deleting to avoid deleting the wrong one.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites

The creator of Shared Virtual Interface can only delete Shared Virtual Interfaces with the following statuses:


* Shared Virtual Interfaces that are not accepted or already deleted by users.

* Shared Virtual Interfaces that are accepted by the user but have no configured BGP Peers or static routes.

* You cannot directly delete Shared Virtual Interfaces that are accepted and configured with BGP Peers or static routes. To delete, first contact the user to delete all BGP Peers or static routes configured for the Shared Virtual Interface.


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Use Account A to log in to the BytePlus [DC Virtual Interface console](https://console.byteplus.com/dc/VirtualInterface).

2. In the top menu bar, select the region where the target Virtual Interface is deployed.

3. In the Virtual Interface list, click **Delete** in the **Actions** column of the target Shared Virtual Interface.

4. In the pop\-up dialog box, confirm that the information is correct, and then click **Delete**.


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

[DeleteDirectConnectVirtualInterface](https://docs.byteplus.com/en/docs/directconnect/DeleteDirectConnectVirtualInterface): Delete a Virtual Interface
