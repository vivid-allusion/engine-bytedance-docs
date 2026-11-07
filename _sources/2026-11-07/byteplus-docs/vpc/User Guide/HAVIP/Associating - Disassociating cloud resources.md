---
title: "Associating/Disassociating cloud resources"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Binding-or-unbinding-cloud-resources"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Action description


* The High\-Availability Virtual IP Address (HAVIP) and its bound cloud resources must reside in the same subnet. Additionally, an HAVIP cannot be bound to both an Elastic Compute Service (ECS) instance and an elastic network interface simultaneously.

* A single HAVIP can be bound to a maximum of 10 Elastic Compute Service (ECS) instances. The ECS instances must be in the **Running** or **Stopped** state.

* A single HAVIP can be bound to a maximum of 10 network interfaces. Network interfaces must be in the **Available** or **In use** state.

* A single HAVIP can be bound to only 1 EIP. The EIP must be in the **Available** state.


<span id=".57uR5a6a5LqR6LWE5rqQ"></span>
## Associate with a cloud resource


1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **HaVip**.

3. In the top menu bar, select the project and region.

4. In the HaVip list, click the name of the target HaVip to enter the details page.

   * **Associate with an ECS**

      1. Click **Associate resource \> Instances \> Associate now**.

      2. In the **ECS** tab, select an ECS instance to associate.

      3. Click **Associate** to complete the action.

   * **Associate with a network interface**

      1. Click **Associate resource \> Instances \> Associate now**.

      2. In the **network interface** tab, select a network interface to associate.

      3. Click **Associate** to complete the action.

   * **Associate with an EIP**

      1. Click **Associate resource \> EIP \> Associate now**.

      2. Select the EIP to associate.

      3. Click **Associate** to complete the action.


<span id="04ZFfFTD"></span>
## Disassociate from a cloud resource


1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **HaVip**.

3. In the top menu bar, select the target project and region.

4. In the HaVip list, click the name of the target HaVip.

   * **Disassociate from an ECS**

      1. Click **Associate resource \> Instances \> Disassociate**.

      2. Click **Disassociate** to complete the action.

   * **Disassociate from a network interface**

      1. Click **Associate resource \> Instances \> Disassociate**.

      2. Click **Disassociate** to complete the action.

   * **Disassociate from an EIP**

      1. Click **Associate resource \> EIP \> Disassociate**.

      2. Click **Disassociate** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [AssociateHaVip](https://docs.byteplus.com/en/docs/vpc/AssociateHaVip)

* [DisassociateHaVip](https://docs.byteplus.com/en/docs/vpc/DisassociateHaVip)

* [AssociateEipAddress](https://docs.byteplus.com/en/docs/eip/AssociateEipAddress)

* [DisassociateEipAddress](https://docs.byteplus.com/en/docs/eip/DisassociateEipAddress)
