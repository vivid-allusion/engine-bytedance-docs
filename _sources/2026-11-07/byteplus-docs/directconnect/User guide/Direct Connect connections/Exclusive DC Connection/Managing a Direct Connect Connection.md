---
title: "Managing a Direct Connect Connection"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Managing-Direct-Connect-connections"
---

<span id=".5p-l55yL54mp55CG5LiT57q_5L-h5oGv"></span>
## View a DC Connection


1. Log in to the[ DC Connection console](https://console.byteplus.com/dc/PhysicalConnection).

2. In the top menu bar, select the target project and region.

3. In the DC Connection list, click the name of the target DC Connection to view its details and those of its associated resources in each tab.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The MACsec and Internet Tunnel (IT) Virtual Interface features require activation before using or viewing details.   </div>
   

   * **Overview:** ​ View basic information such as name, ID, access point location, port type, port status, and bandwidth.

   * **MACsec**: View MACsec credential details.

   * **DC Virtual Interface**: View details of associated Virtual Interfaces.

   * **IT Virtual Interface**: View details of associated IT Virtual Interfaces.

   * **Data monitoring**: View[ monitoring metrics](https://console.byteplus.com/cloud_monitor/docs?namespace=VCM_DirectConnectConnection).

   * **Shared Line**: View details of created Shared Lines.


<span id=".5Yig6Zmk54mp55CG5LiT57q_"></span>
## Delete a DC Connection

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Before you begin


* The DC Connection to be deleted must be expired. Currently, you cannot delete unexpired DC Connections. To delete an unexpired DC Connection, unsubscribe the connection first. For procedure, see [Unsubscription](https://docs.byteplus.com/en/docs/6269/81013).

* The DC Connection to be deleted must not have any associated Virtual Interfaces. If have, delete those Virtual Interfaces first. For procedure, see [Deleting a Virtual Interface](https://docs.byteplus.com/en/docs/directconnect/Deleting-the-virtual-interface).

* The DC Connection to be deleted has no attached QoS policies. If any exist, detach those QoS policies first. For details, see [Disassociating a Direct Connect Connection](https://docs.byteplus.com/en/docs/directconnect/Attaching_and_detaching_DC_Connection#.UW9T562W55Wl6Kej57uR6Kej57uR54mp55CG5LiT57q_).


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After deleting a DC Connection, dependent configurations will be deleted accordingly and are unrecoverable. Proceed with caution.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to the[ DC Connection console](https://console.byteplus.com/dc/PhysicalConnection).

2. In the top menu bar, select the project and region where the target DC Connection is located.

3. In the DC Connection list, click **Delete** in the **Actions** column of the target DC Connection.

4. In the pop\-up dialog box, confirm the information is correct, and click **Delete** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation


* [DescribeDirectConnectConnectionAttributes](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectConnectionAttributes): Query the details of a specified DC Connection.

* [DescribeDirectConnectConnections](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectConnections): Query the details of DC Connections that meet the specified conditions.

* [ModifyDirectConnectConnectionAttributes](https://docs.byteplus.com/en/docs/directconnect/ModifyDirectConnectConnectionAttributes): Modify the name and description of a specified DC Connection.

* [DeleteDirectConnectConnection](https://docs.byteplus.com/en/docs/directconnect/DeleteDirectConnectConnection): Delete a specified DC Connection.
