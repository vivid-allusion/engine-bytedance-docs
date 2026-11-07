---
title: "Associating or disassociating subnet for a multicast domain"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Attaching-or-detaching-subnet-for-multicast-domain"
---

<span id="2oJYt9dZ"></span>
## Associate a subnet with a multicast domain

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Before associating a subnet, ensure that the Virtual Private Cloud (VPC) to which the subnet belongs has established an Network Instance Attachment with the Transit Router (TR) instance.</div>


* <div data-tips="true" data-tips-type="default">A single multicast domain supports associating a maximum of 10 subnets by default. If the default quota is insufficient, see <a href="https://console.byteplus.com/quota/productList">create a quota application</a> to submit a quota increase request.</div>


1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. In the zone below **Basic information**, select the **Multicast domain** tab.

4. Click the name of the target multicast domain.

5. Click **Associate subnet**, and sequentially select the VPC and subnet.

6. Click **Associate** to complete the action.


<span id="vmkDoyWR"></span>
## Disassociate a subnet from a multicast domain

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Before disassociating a subnet, ensure that no multicast sources or multicast members belong to the subnet. If any, delete the multicast sources and multicast members first. For procedure, see <a href="https://docs.byteplus.com/en/docs/transitrouter/Managing-the-multicast-source#ojkEI891">Delete a multicast source</a> and <a href="https://docs.byteplus.com/en/docs/transitrouter/Managing-multicast-members#DkTP7gaz">Delete a multicast member</a>.</div>


* <div data-tips="true" data-tips-type="default">When deleting a subnet in the VPC console, subnets already associated with a multicast domain are automatically disassociated.</div>


1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. In the zone below **Basic information**, select the **Multicast domain** tab.

4. Click the name of the target multicast domain.

5. Click **Disassociate** to the right of the target subnet.

6. Click **Disassociate** to complete the action.


<span id="mwYDYxIZ"></span>
## Related documentation


* [AssociateTransitRouterMulticastDomain](https://docs.byteplus.com/en/docs/transitrouter/AssociateTransitRouterMulticastDomain): Associate a multicast domain with a specified subnet.

* [DissociateTransitRouterMulticastDomain](https://docs.byteplus.com/en/docs/transitrouter/DissociateTransitRouterMulticastDomain): Disassociate a specified subnet from a multicast domain.
