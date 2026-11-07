---
title: "Basic Concepts"
product: "BytePlus Organization"
product_code: "organization"
source: "https://docs.byteplus.com/en/docs/organization/BasicConcepts"
---

BytePlus Organization Service is a multi\-account management solution for BytePlus users. It maintains relationships between multiple accounts and provides foundational support for enterprise cloud adoption.

The following diagram shows a simulated structure of BytePlus Organization Service, where accounts are grouped into four Organizational Units under the Root. Refer to the diagram to understand the concept of Organization.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_ef9abca10fe7dea7224439f45ae64b2a.png) </span>

<span id="organization"></span>
## **Organization**

An Organization enables hierarchical management of BytePlus accounts. You can use the BytePlus Organization Service Console to view and manage all accounts within your organization. Each account can be placed directly under the Root or moved into an Organizational Unit. An account can belong to only one node at a time. You can manage your organization structure and Member Accounts using a hierarchical tree structure.

<span id="root"></span>
## **Root**

The Root is the parent container for all Organizational Units and accounts within your Organization.

**Notes:**  Each Organization has only one Root. The Root is automatically created when the Organization is established. The Root cannot be modified or deleted.

<span id="organizational-unit"></span>
## **Organizational Unit**

An Organizational Unit is a node in the hierarchical tree structure of an Organization. The Organizational Unit is used for grouping accounts under the Root. An Organizational Unit can contain other Organizational Units. Each Organizational Unit has only one parent node. Each account belongs to only one Organizational Unit.

<span id="account"></span>
## **Account**


* **Master Account:**   By default, the account created the Organization is the Master Account. An Organization has only one Master Account. The Master Account can invite or create Member Accounts and configure their attributes.

* **Member Account:**  All other accounts within the Organization are Member Accounts. A Member Account can belong to only one Organization.


<span id="tag"></span>
## **Tag**

Tags are key\-value pairs used to manage resources within an Organization. Accounts and Organizational Units are resource entities. Each entity has a unique TRN. Tags can be assigned to accounts and Organizational Units for classification, filtering, and resource management.

<span id="invitation"></span>
## **Invitation**

You can invite external accounts to join your Organization. Only the Master Account can send invitations. Once an invited account accepts the invitation, it becomes a Member Account of the Organization.
