---
title: "Direct Connect access process"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Direct-Connect-access-procedure"
---

BytePlus Direct Connect Connection supports two access modes: independently applying Dedicated Lines and sharing partners' Shared Lines. This topic describes the processes for the two access modes. You can choose the most suitable one based on your actual needs.

<span id=".54us5Lqr5LiT57q_5o6l5YWl5rWB56iL"></span>
## Dedicated Line access process

In the Dedicated Line mode, you apply for a dedicated DC Connection independently to achieve cloud access. Each stage in this process requires a lead time. Fully assess the duration needed for each stage according to your business situation, and reserve adequate time accordingly.

<span id=".55Sz6K-35rWB56iL"></span>
### Application process

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Letter of Authorization (LOA) is a letter authorizing access. The LOA for Direct Connect authorizes third\-party line operators to enter the BytePlus data center for construction and DC Connection installation.</div>



1. Before creating a DC Connection in the console, complete the preparations first. For details, see [Preparations before access](https://docs.byteplus.com/en/docs/directconnect/Preparation-for-access).

2. After completing all preparations, you need to log in to the BytePlus Direct Connect console to complete the creation of the DC Connection. For procedure, see [Creating a Direct Connect Connection](https://docs.byteplus.com/en/docs/directconnect/Accessing-a-Direct-Connect-connection-1).

3. After creating a DC Connection, you need to create a DC Gateway and a Virtual Interface to enable cloud access. For procedure, see [Creating a Direct Connect Gateway](https://docs.byteplus.com/en/docs/directconnect/Creating-a-Direct-Connect-gateway-1), [Creating a Virtual Interface](https://docs.byteplus.com/en/docs/directconnect/Creating-a-virtual-interface-1), and [Connecting an on-premises data center to a VPC via a single Direct Connect with static routing](https://docs.byteplus.com/en/docs/directconnect/Best-Practices-4).


<span id=".5a6h5om55rWB56iL"></span>
### Approval process


1. After completing all preparations, you need to go to the BytePlus DC Connection console to apply for a DC Connection port.

2. After receiving the approval notification via internal message and SMS from BytePlus, apply for a LOA via the BytePlus DC Connection console. The LOA authorizes entry into the BytePlus access point data center for line construction.

3. After receiving the LOA approval notification via internal message and SMS from BytePlus, contact your line operator to enter the BytePlus data center based on the construction schedule on the LOA.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Complete line construction and pay the port occupancy fee within 45 days after LOA approval. Otherwise, the allocated port will be released.   </div>
   

<span id=".5YWx5Lqr5LiT57q_5o6l5YWl5rWB56iL"></span>
## Shared Line access process

In the Shared Line mode, tenants do not need to install their own links to the BytePlus Direct Connect. Instead, they can apply to a line operator (also referred as BytePlus partner) who has connected the BytePlus access points to share the operator's DC Connection. In this mode, tenants only need to establish a network between the on\-premises data center and the operator access point. They can use the DC service via the Shared Line created by the line operator.


* When multiple tenants share the same DC Connection between "the operator access point" and the "BytePlus access point", all tenants' Shared Lines share the bandwidth of the DC Connection. Therefore, Shared Line is suitable for low\-bandwidth services.

   The line operator applies to BytePlus to enable the Shared Line feature, and creates a Shared Line for tenants. The tenant accepts and uses the Shared Line.

* After completing the installation of DC Connections between "the operator access point" and "the BytePlus access point", the line operator only needs to assist the tenant in completing the line installation and network connection between the tenant's data center and "the operator access point". Compared to Dedicated Lines, Shared Lines generally have shorter construction periods and suit businesses with tighter cloud migration timelines.

* If creating a Shared Line for multi\-tenants, the line operator needs to assign the VLAN ID. Tenants isolate resources based on the VLAN ID.
