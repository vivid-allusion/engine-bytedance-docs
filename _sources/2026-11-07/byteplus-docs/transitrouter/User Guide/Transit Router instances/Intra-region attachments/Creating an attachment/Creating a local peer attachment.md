---
title: "Creating a local peer attachment"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Creating_a_local_peer_attachment"
---

## Scenarios

Establish a connection between two Transit Router (TR) instances in the same region, enabling intercommunication between the two TR\-connected networks.

> **Tip**

> The local peer attachment feature is in the beta stage. If you need a trial, please contact your account manager.

## Prerequisites

* Ensure you have created two TR instances in the same region with separate Autonomous System Numbers (ASNs). For procedure, see [Creating a Transit Router instance](https://docs.byteplus.com/en/docs/transitrouter/TransitRouter-instances-01).

* When creating a cross\-account local peer attachment, obtain the peer TR instance ID and its account in advance.

## Instructions

* You can create up to 10 local peer attachments for a single TR instance by default.

* Local peer attachments incur attachment fees separately on both TR instances, with no traffic processing fees charged. For details, see [Billing notes](https://docs.byteplus.com/en/docs/6979/155973).

* IPv6 is enabled for local peer attachments by default and cannot be disabled. If the IPv6 feature is unavailable in the region of the local peer attachment, IPv6 is not supported by default.

* When creating a local peer attachment, TR instances on both ends must not be shared instances.

## Procedure

1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. In the section below **Basic information**, select the **Intra\-region attachment** tab.

4. Click **Create attachment**, and complete the basic configuration based on the table below.

   |Parameter |Description |Example |
   |---|---|---|
   |**Basic information** |||
   |Transit Router |Defaults to the selected TR instance, requiring no manual configuration. |tr01 |
   |Regions |Defaults to the same region as the TR instance. No manual configuration required. |China (Guangzhou) |
   |Name |The name for the network instance attachment to be created.<br><br>> **tip**<br><br><br>> After successful creation, the local peer attachment is assigned two different IDs: one for each side. You can modify the attachment name and description on TR instances separately. These modifications take effect only on the TR under my account.<br> |attach\-same region\-peer |
   |**Network Instances** |||
   |Network instance type |Select the type of network instance. This example only demonstrates configuration parameters for TR attachments. |Transit Router |
   |Account type |Select the relevant option based on the account ID of the peer TR. |Same account |
   |Peer Account ID |In cross\-account scenarios, you must provide the account ID of the peer TR. |210\*\*\*\*001 |
   |Peer TR |We recommend assigning an ASN to this TR instance different from the ASN of the local TR instance.<br><br><br>* For same\-account scenarios, select another TR instance in the same region under my account.<br><br>* For cross\-account scenarios, type the ID of a TR instance in the same region under the peer account. |tr02 |

5. Complete the route configuration and advanced options based on the table below.

   |Parameter |Description |Example |
   |---|---|---|
   |**Route configuration**<br><br>> **tip**<br><br><br>> When performing actions in the local account, Peer TR association forwarding and Peer TR route learning are disabled by default and cannot be configured. Configure association forwarding and route learning on the peer TR instance side.<br> |||
   |Local associated route table |The local TR instance forwards traffic from the local peer attachment based on its associated forwarding route table.<br><br>If disabled is selected, after creating a local peer attachment, you also need to manually configure local TR association forwarding based on [Create an association forwarding rule](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-07#.5Yib5bu65YWz6IGU6L2s5Y-R). Otherwise, the local TR instance cannot forward traffic from the peer TR instance. |Enabled, tr01\-rtb\-set |
   |Local TR route learning |The specified local TR route table automatically learns routes from the peer TR associated forwarding route table. It generates routes with the local peer attachment as the next hop in the specified TR route table.<br><br>If disable is selected, after a local peer attachment is created, see [Create a route learning rule](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-06#.5Yib5bu66Lev55Sx5a2m5Lmg) or [Create a static route](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-05#.5Yib5bu66Z2Z5oCB6Lev55Sx) to add routes pointing to the local peer attachment into the TR route table. |Enabled, tr01\-rtb\-sys |
   |**Advanced option** |||
   |Tags |A tag consists of a key\-value pair and is used for categorizing and searching resources. [Learn more](https://docs.byteplus.com/en/docs/transitrouter/Tags)<br><br>Click **Add tag**, type the tag key and tag value to add tags to the cloud resource. |* Tag key: attach\-k1<br><br>* Tag value: attach\-v1 |

6. Click **Buy now** to complete the action.

   After the creation is completed, the local peer attachment is displayed in both TR instances. You can modify its associated forwarding route table as needed.

## What to do next

* After creating a same\-account local peer attachment, configure [association forwarding](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-07) and [route learning](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-06) in the peer account.

* After creating a cross\-account local peer attachment, use the peer account to [accept the cross-account attachment](https://docs.byteplus.com/en/docs/transitrouter/Accepting_a_cross-account_peering_attachment) and then configure [association forwarding](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-07) and [route learning](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-06).

## Related documentation

[CreateTransitRouterLocalPeerAttachment](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterLocalPeerAttachment): Create a local peer attachment.
