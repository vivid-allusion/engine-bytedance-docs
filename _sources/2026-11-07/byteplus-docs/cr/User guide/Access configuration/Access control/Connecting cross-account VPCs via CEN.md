---
title: "Connecting cross-account VPCs via CEN"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/Connect_VPCs_across_different_accounts"
---

Standard Edition instances support cross\-region VPC connectivity. Pulling images and Helm charts over the internal network effectively boosts push and pull speeds while eliminating public network bandwidth costs.

<span id="RNdeeEPP"></span>
## Prerequisites

This article uses internal network connectivity between account A and account B as an example to introduce the procedure.


* You have obtained the CR domain name of account A. You can obtain this information on the overview page of the CR instance.

* The VPC of account A has been connected. For details, see [Connecting to the VPC of the current account](https://docs.byteplus.com/en/docs/cr/connect-vpcs-under-the-same-account).

* On the **Access control** page, obtain the VPC **intranet resolution IP** of account A.


<span id="QQyWLERl"></span>
## Procedure

<span id="6imCPcc3"></span>
### Step 1: Connect VPCs via CEN

CEN enables CEN instance\-based connection of VPCs under account A and account B by attaching network instances from both accounts.


1. Create a CEN instance. For details, see [Creating CEN instances](https://docs.byteplus.com/en/docs/cen/CEN-instances-01).

2. Create and attach network instances for both the "**this account**" and "**cross\-account**" scenarios to add the VPC instances from both accounts to the CEN instance. For details, see [Attaching network instances](https://docs.byteplus.com/en/docs/cen/Network-instances-01).

   * This account

      
      |Parameter |Description |
      |---|---|
      |Account |Select **This account**. |
      |Region |Select the region of this account. In this example, the region of account A is selected. |
      |Instance edition |Select **VPC**. |
      |Network instance |Select the VPC instance of this account. Filtering by project is supported. In this example, the VPC of account A is selected. |
      

   * Cross account

      
      |Parameter |Description |
      |---|---|
      |Account |Select **Cross account**. |
      |Target account ID |In this example, the ID of account B is entered. |
      |Region |In this example, the region of account B is selected. |
      |Instance edition |Select **VPC**. |
      |Network instance |In this example, the VPC instance of account B is selected. |
      


<span id="lbZrryok"></span>
### Step 2: Add a resolution record in the VPC

Add a private network resolution record for connectivity with account A in the VPC of account B. This record will enable the domain names in account B to resolve to the CR in account A.


1. In Private Zone private domain management, add the domain name obtained during the **preparation steps** of account A. For details, see [Adding a domain](https://docs.byteplus.com/en/docs/byteplus-dns-suite/docs-creating-a-domain-na).

2. Add a domain name resolution record. For details, see [Create DNS Records](https://docs.byteplus.com/en/docs/byteplus-dns-suite/docs-creating-updating-or-deleting-dns-records).

   * Domain name: Enter `@`.

   * Record value: Create a new record value. Enter the VPC intranet resolution IP of account A obtained **during the preparation steps**.
