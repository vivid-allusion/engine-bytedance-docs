---
title: "Managing a multicast member"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Managing-multicast-members"
---

<span id="Udkr59Yx"></span>
## Add a multicast member

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can batch add up to 10 network interfaces as multicast members per request.</div>



1. Log on to the [Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target Transit Router (TR) instance to go to the details page.

3. In the area below **Basic information**, select the **Multicast domain** tab.

4. Click the name of the target multicast domain.

5. In the area below **Basic information**, select the **Multicast group** tab.

6. Click **Add multicast member** and configure the multicast member based on the table below.

   
   |Name |Description |Sample Value |
   |---|---|---|
   |**Basic information **  |||
   |Transit Router  |Defaults to the TR instance you select. No additional configuration is needed. |tr01 |
   |Multicast domain |By default, the selected multicast domain instance does not require manual configuration. |MulticastDomain\-Uf7N |
   |**Multicast group** |||
   |Multicast group |Configure the multicast group IP address.<br><br><br>* **Create a multicast group**: Enter the multicast IP address, the range is: 224.0.0.0 to 239.255.255.255.<br><br>* **Use an existing multicast group**: Select a created multicast group. |Create a multicast group |
   |**Multicast member** |||
   |Resource type |Defaults to the Virtual Private Cloud (VPC). No additional configuration is needed. |VPC |
   |Network interfaces |Select the subnet and the network interface to be used as multicast members within it.<br><br>The network interface created in the VPC do not support adding as a multicast member. |subnet01，eni01 |
   

7. Click **Add** to complete the action.


<span id="DkTP7gaz"></span>
## Delete a multicast member

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">When deleting a network interface on the VPC side, the network interface already added as a multicast member will be automatically removed from the multicast group.</div>



1. Log on to the [Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance to go to the details page.

3. In the zone below **Basic information**, select the **Multicast domain** tab.

4. Click the name of the target multicast domain.

5. In the zone below **Basic information**, select the **Multicast group** tab.

6. Click **Delete multicast member ** to the right of the target multicast group.

7. Click **Delete** to complete the action.


<span id="TFJ1Raqw"></span>
## Related documentation


* [CreateTransitRouterMulticastGroupMember](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterMulticastGroupMember): Add a multicast member

* [DeleteTransitRouterMulticastGroupMember](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterMulticastGroupMember): Delete a multicast member
