---
title: "Quick start"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/ipam-Quick-start"
---

## Scenarios

Company X has two core businesses deployed on BytePlus, involving multiple VPCs. To prevent IP address conflicts, simplify maintenance, and support future expansion, all their IP addresses are centrally managed via the IPAM tool. This enables standardized management of address allocation, documentation, and reservation, reducing operational complexity across VPCs.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ed5e004cd6224f94333105420a8b8b53.png)

## Before you begin

For demonstration purposes, this topic uses the scenario shown in the diagram above. Before you begin, complete the following preparatory steps:

1. Register account X.

2. Use Account X to enable the enterprise organization and create member accounts A, B, and M. Account X serves as the management account for the enterprise organization.

## Configuration procedures

[Step 1: Enterprise organization admin configures the enterprise organization](https://docs.byteplus.com/en/docs/vpc/Step-1-configures-the-enterprise-organization)

1. [Enable trusted service](https://docs.byteplus.com/en/docs/vpc/Step-1-configures-the-enterprise-organization#iJ2lrWZf): The enterprise organization admin enables trusted services for IPAM, authorizing IPAM to retrieve resource information for accounts within the organization.

2. [Assign IPAM delegated admin](https://docs.byteplus.com/en/docs/vpc/Step-1-configures-the-enterprise-organization#r2ixHf9i): The enterprise organization admin designates a member account within the organization as the IPAM delegated admin, who is responsible for centrally managing IPAM resources.

3. [Create control policy (optional)](https://docs.byteplus.com/en/docs/vpc/Step-1-configures-the-enterprise-organization#Dl0ViUCI): The enterprise organization admin creates a control policy that enforces business accounts to create VPCs and allocate auxiliary CIDR blocks from the specified IPAM address pool.

4. [Attach control policy (optional)](https://docs.byteplus.com/en/docs/vpc/Step-1-configures-the-enterprise-organization#JaKNGNu9): The enterprise organization admin attaches the control policy to the target business accounts.

[Step 2: IPAM delegated admin plans and allocates IPAM address pools](https://docs.byteplus.com/en/docs/vpc/Step-2-plans-and-allocates-IPAM-address-pools)

1. [Create IPAM instance](https://docs.byteplus.com/en/docs/vpc/Step-2-plans-and-allocates-IPAM-address-pools#mvAomxME): The IPAM delegated admin creates an IPAM instance.

2. [Create IPAM scope](https://docs.byteplus.com/en/docs/vpc/Step-2-plans-and-allocates-IPAM-address-pools#HfqnFZl8): Within the IPAM instance, create a private network scope.

3. [Create IPAM parent pool](https://docs.byteplus.com/en/docs/vpc/Step-2-plans-and-allocates-IPAM-address-pools#DAK7v5x9): Within the private network scope, create a top\-level address pool to centrally manage and govern all private IP address ranges across the enterprise.

4. [Create IPAM sub-pool](https://docs.byteplus.com/en/docs/vpc/Step-2-plans-and-allocates-IPAM-address-pools#ROIXyo8G): Within the top\-level address pool, create multiple sub address pools based on dimensions such as business unit, region, and environment, making them available for business accounts to use.

5. [Share IPAM sub-pool](https://docs.byteplus.com/en/docs/vpc/Step-2-plans-and-allocates-IPAM-address-pools#fBZgUlVi): The IPAM delegated admin shares the IPAM sub address pools with the business accounts. Business accounts within the same enterprise organization accept these shares by default.

[Step 3: Business account creates VPC](https://docs.byteplus.com/en/docs/vpc/Step-3-Business-account-creates-VPC)

The business accounts allocate CIDR blocks from the shared IPAM address pools to create VPCs.
