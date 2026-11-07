---
title: "Shared Line overview"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Overview"
---

Building a Direct Connect Connection from the on\-premises data center to the BytePlus access point independently entails substantial costs and certain construction timeline. Therefore, using a DC connection of a line operator that is already connected to the BytePlus access point is a better solution. This only requires completing the last\-mile line construction between the on\-premises data center and the operator access point, significantly reducing construction time.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is currently available only for accounts with enterprise authentication completed. For procedure, see Enterprise authentication.</div>


&nbsp;

<span id=".5LuA5LmI5piv5YWx5Lqr5LiT57q_"></span>
## What is Shared Line

Shared Line refers to an access mode where tenants apply to a line operator who has connected the BytePlus access points to share the operator's DC Connection. In this mode, tenants only need to establish a network between the on\-premises data center and the operator access point. They can use the DC service via the Shared Line created by the line operator.


* When multiple tenants share the same DC Connection between **the operator access point** and the **BytePlus** ** ** **access point**, all tenants' Shared Lines share the bandwidth of the DC Connection. Therefore, Shared Line is suitable for low\-bandwidth services.

* The line operator applies to BytePlus to enable the Shared Line feature, and creates a Shared Line for tenants. The tenant accepts and uses the Shared Line.

* After completing the installation of DC Connections between **the operator access point** and the **BytePlus** ** ** **access point**, the line operator only needs to assist the tenant in completing the line installation and network connection between the tenant's data center and **the operator access point**. Compared to Dedicated Lines, Shared Lines generally have shorter construction periods and suit businesses with tighter cloud migration timelines.

* If creating a Shared Line for multiple tenants, the line operator needs to assign the VLAN ID. Tenants isolate resources based on the VLAN ID.
