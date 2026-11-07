---
title: "Overview"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/IPAM-Overview"
---

## Introduction​

IP Address Manager (IPAM) is a management tool for the full lifecycle of IP addresses. It supports unified planning, allocation, tracking, and reclamation of addresses across multiple accounts and regions, enabling global visibility and control over address resources. It effectively addresses issues such as resource fragmentation, address conflicts, decentralized management, and low operational efficiency.

> **tip**

> IPAM is currently in beta stage. For trial requests, please contact your account manager.

## Product architecture

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_aedb3b7b081c80f9340bd08b7ca1573e.png)

|Concept |Description |
|---|---|
|IPAM instance |The IPAM instance is the core component that hosts the entire IP address management feature. |
|IPAM Scope |An IPAM scope is the top\-level container in IPAM, where each scope represents an independent IP address space. Address pools can be created under a scope. |
|IPAM Pool |An IPAM address pool is a collection of IP address blocks (CIDRs). Based on planning, it is generally divided into the following three types:<br><br><br>* **Top\-level pool**: The first\-layer address pool, containing the largest number of CIDRs.<br><br>* **Region pool**: A sub\-pool of the top\-level pool, from which CIDRs are allocated by region.<br><br>* **Business pool**: A sub\-pool of the region pool, from which CIDRs are allocated based on business requirements. |
|Resource discovery |Resource Discovery is used to automatically identify and continuously track the CIDR usage of resources such as VPCs and subnets within a region. This enables centralized resource management and provides data support for IP address planning and allocation. |
|Enterprise organization |Enterprise Organization is a multi‑account unified management service provided by BytePlus for enterprise customers. It allows you to build a hierarchical structure of all cloud accounts within the enterprise, supporting large‑scale cloud adoption and unified multi‑account management. |
|Resource Sharing |Resource sharing refers to the ability for users to share their own resources with other accounts. Accounts that receive the share can use the shared resources according to system‑preset permissions, effectively reducing operational and maintenance costs on the business side. |
|Custom\-allocated CIDR |Custom\-allocated CIDR refers to specific CIDR blocks reserved in advance for scenarios such as future business expansion or data migration. This prevents these CIDR blocks from being allocated to sub address pools or VPCs. |

## Scenarios

* **Multi\-business network management**

   When a company operates different business units, address pools can be configured to assign distinct sub\-pools to each business, enabling simplified and more intuitive IP address management.

* **Hybrid Cloud & Multi\-Cloud management**

   When network segment planning involves on\-premises IDCs or other cloud vendors, you can pre\-configure address pools and reserve specific CIDR blocks. This ensures that these reserved segments are not allocated to VPCs, preventing IP address conflicts when connectivity between on\-premises IDCs and VPCs is required.

## Billing

Currently free of charge during the invite\-only Beta testing period.
