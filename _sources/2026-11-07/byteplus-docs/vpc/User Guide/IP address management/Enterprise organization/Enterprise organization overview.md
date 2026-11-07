---
title: "Enterprise organization overview"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Enterprise-organization-overview"
---

## Overview

BytePlus Enterprise Organization is tailored specifically for enterprise customers. It is an underlying service for unified management of multiple accounts, enabling you to build and maintain a hierarchical structure of all cloud accounts within the enterprise. It provides foundational support for large‑scale cloud adoption and unified, coordinated management of various business scenarios across multiple accounts.

## Role

After users Enable enterprise organization and Add member accounts, the resulting structure is shown in the figure below:

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ea28d9dc9886d61adbbf60611d837cf8.png)

For the IPAM scenario, we recommend planning the accounts within your Enterprise Organization into the following three roles:

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0fbf12cfd865d5640b9f14dcaaa58d8c.png)

|Account type |**Role** |Notes |**IPAM\-related actions** |
|---|---|---|---|
|Admin account |Enterprise organization admin account |The account used to manage the enterprise organization (e.g., adding or removing member accounts). The account should not be used to operate IPAM resources, it is advisable to create a dedicated account for managing IPAM resources. |* Enable enterprise organization<br><br>* [Enable IPAM trusted service](https://docs.byteplus.com/en/docs/vpc/Enabling-trusted-service)<br><br>* [Delegate IPAM admin](https://docs.byteplus.com/en/docs/vpc/Enabling-trusted-service)<br><br>* [Disable IPAM trusted service](https://docs.byteplus.com/en/docs/vpc/Enabling-trusted-service) |
|Member account<br><br> |IPAM delegated admin |The IPAM delegated admin account is a dedicated account for managing IPAM resources \- for example, creating IPAM address pools and sharing them with business accounts. It is not advisable to use the enterprise organization management account to directly operate IPAM resources. Instead, a separate delegated admin account should be created solely for IPAM management. |* [Create IPAM instance](https://docs.byteplus.com/en/docs/vpc/Managing-IPAM-instances)<br><br>* [Manage scope](https://docs.byteplus.com/en/docs/vpc/Managing-IPAM-scopes)<br><br>* [Manage address pool](https://docs.byteplus.com/en/docs/vpc/Managing-IPAM-pools)<br><br>* [Share address pool with business accounts](https://docs.byteplus.com/en/docs/vpc/Sharing-IPAM-Pool)<br><br>* [Manage resource discovery](https://docs.byteplus.com/en/docs/vpc/IPAM-Viewing-resource-discovery) |
||Business account |Business accounts are used to deploy business resources. They can use the address pools shared by the IPAM delegated admin to create VPCs and allocate secondary CIDR blocks. |* [Create VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC)<br><br>* [Configure custom-allocated CIDR](https://docs.byteplus.com/en/docs/vpc/Creating-Deleting-a-custom-allocated-CIDR) |

##
