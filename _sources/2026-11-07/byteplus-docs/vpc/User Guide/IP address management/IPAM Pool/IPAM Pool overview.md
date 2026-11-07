---
title: "IPAM Pool overview"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/IPAM-Pool-overview"
---

## Overview

An IPAM address pool is a collection of IP address blocks (CIDRs).

## Classification

Based on planning, it is generally divided into the following three types:

* **Top\-level pool:**  The first\-layer address pool, containing the largest number of CIDRs.

* **Region pool**: A sub\-pool of the top\-level pool, from which CIDRs are allocated by region.

* **Business pool**: A sub\-pool of the region pool, from which CIDRs are allocated based on business requirements.

## Terms

|Term |Description |
|---|---|
|Pre\-populated CIDR |Pre\-populated CIDRs are allocatable address segments added to the address pool by the address pool owner. |
|Allocate CIDR |Allocating a CIDR means the address pool user allocates a segment from the pre\-populated CIDRs for use by VPC resources. |
|Allocation rules |Allocation Rules refer to the rules for sub\-address pools and VPCs to allocate CIDRs from an address pool. Consists of three parameters: Minimum netmask length, default netmask length, and maximum netmask length. |
|Custom\-allocated CIDR |Custom\-allocated CIDR refers to a CIDR block that users can manually reserve within an IPAM address pool to pre‑allocate addresses in advance for scenarios such as hybrid cloud, multi‑cloud, and data migration. |

## Limits

After an IPAM address pool is shared with a business account, to ensure IP traceability, IPAM must first have the capability to monitor the IP usage of the business account. Only then can the business account allocate CIDR blocks from the shared pool to create VPCs. If the business account's VPC resources cannot be automatically discovered by IPAM, the business account must share its own Resource Discovery with the IPAM owner. For more details, see [Managing a resource discovery](https://docs.byteplus.com/en/docs/vpc/IPAM-Viewing-resource-discovery) and [Sharing a resource discovery](https://docs.byteplus.com/en/docs/vpc/Sharing-Resource-Discovery).

## Configuration procedures

> **tip**

> For cross\-enterprise organizations, complete Resource Discovery sharing before sharing the address pool.

1. [Create Address Pool](https://docs.byteplus.com/en/docs/vpc/Managing-IPAM-pools): Create an address pool to be shared.

2. [Share Address Pool](https://docs.byteplus.com/en/docs/vpc/Managing-IPAM-pools): Share the address pool with a business account.

3. [Accept Shared Address Pool](https://docs.byteplus.com/en/docs/vpc/Managing-IPAM-pools): For the same enterprise organization, the shared address pool is accepted by default; for different enterprise organizations, you must manually accept the sharing.

4. [Create VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC): The shared party creates a VPC through this address pool.
