---
title: "Managing a multicast source"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Managing-the-multicast-source"
---

<span id="yWkTcEed"></span>
## Add a multicast source

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">A maximum of 10 network interfaces can be added in batch as multicast sources per request.</div>



1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target Transit Router (TR) instance.

3. In the zone below **Basic information**, select the **Multicast domain** tab.

4. Click the name of the target multicast domain.

5. In the zone below **Basic information**, select the **Multicast group** tab.

6. Click **Add multicast source** and configure the multicast source based on the table below

   
   |Parameter |Description |Example |
   |---|---|---|
   |**Basic information** |||
   |Transit Router |Defaults to the selected TR instance, requiring no manual configuration. |tr01 |
   |Multicast domain |Defaults to the selected multicast domain instance. No manual configuration required. |MulticastDomain\-Uf7N |
   |**Multicast group** |||
   |Multicast group |Configure the multicast group IP address.<br><br><br>* **Create multicast group**: Enter the multicast IP address. Values: 224.0.0.0 to 239.255.255.255.<br><br>* **Use existing group**: Select a created multicast group. |Create multicast group |
   |**Multicast source** |||
   |Resource type |Defaults to VPC. No additional configuration is needed.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">In this Virtual Private Cloud (VPC), multicast traffic fails for Elastic Compute Service (ECS) instances with Elastic IP Addresses (EIPs). Contact your account manager to enable the User CIDR Block feature for the VPC and add the multicast group IP as a User CIDR block to ensure normal multicast traffic forwarding.</div><br> |VPC |
   |Network interface |Select a subnet and the network interface to be used as the multicast source.<br><br>The network interface created in the VPC by the TR does not support being added as a multicast source. |subnet01, eni01 |
   

7. Click **Add** to complete the action.


<span id="ojkEI891"></span>
## Delete multicast source

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">When deleting a network interface on the VPC side, the network interface added as a multicast source will be automatically removed from the multicast group.</div>



1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. In the zone below **Basic information**, select the **Multicast domain** tab.

4. Click the name of the target multicast domain.

5. In the zone below **Basic information**, select the **Multicast group** tab.

6. Click **Delete multicast source** to the right side of the target multicast group.

7. Click **Delete** to complete the action.


<span id="fp5cxGMi"></span>
## Related documents


* [CreateTransitRouterMulticastGroupSource](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterMulticastGroupSource): Add a multicast source.

* [DeleteTransitRouterMulticastGroupSource](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterMulticastGroupSource): Delete a multicast source.
