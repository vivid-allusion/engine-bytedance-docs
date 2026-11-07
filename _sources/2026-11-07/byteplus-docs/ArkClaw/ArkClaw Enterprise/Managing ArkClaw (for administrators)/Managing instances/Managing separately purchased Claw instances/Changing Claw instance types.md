---
title: "Changing Claw instance types"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Changing_Claw_instance_types"
---

When existing Claw instance types no longer meet business needs due to workload changes, you can adjust **vCPU** and **memory** configurations by changing the instance type.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"> This topic applies only to specification changes (upgrade/downgrade)‌ of <strong>individually purchased instances</strong>. <strong>Your service will be ‌interrupted during specification adjustment, so perform this operation during off\-peak hours</strong>.</div>


<span id="aMvbg8u4"></span>
## Prerequisites


* The target Claw instance must be in ‌the **Running‌**  or ‌**Stopped‌**  state. You cannot change the type of instances in other states (such as **Modifying Instance Specs** or **Deleting**).

* The business impact of service interruption during the type change has been evaluated, and an appropriate maintenance window has been determined.


<span id="2NYuMauM"></span>
## Operation instructions


* You can change instance types in batches, but only for Claw instances of the same type. This means that all selected instances must **currently be of the same instance type**.

* Both upgrades and downgrades are supported. An upgrade adjusts the current Claw instance type to **a higher tier**, for example, from Starter to Standard. A downgrade adjusts the current Claw instance type to **a lower tier**, for example, from Ultimate to Standard.

* To prevent data loss after a downgrade, **the downgrade does not adjust volume specifications**. This means the price difference for the volumes is not refunded, and the refund may be USD 0.


<span id="ua8ZR5W7"></span>
## Procedure


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane​, click "Claw Management" \> "Claws".

3. Change the Claw instance type.

   * **Individually**: In the Claw list, locate the row of the target Claw instance and click "More" \> "Change instance type".

   * **In batches**: In the Claw list, select the checkboxes for multiple Claw instances, then click "..." \> "Change instance type" at the bottom of the list.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Only <strong>Claw instances of the same type</strong> can be selected. Up to <strong>10</strong> instances can be selected for a single operation.      </div>
      

4. On the "Change instance type" page, select the target instance type, select the notes and considerations checkboxes at the bottom of the page, and then click "Confirm change".

5. Follow the on\-screen instructions to confirm the order information and complete payment.

   * **Upgrade**: The payable amount is positive (for example, USD 439.82), indicating that you need to pay the price difference. Complete payment promptly. The actual amount is subject to the amount displayed on the order page.

   * **Downgrade**: The payable amount may be negative (for example, USD \-439.82), indicating a refund to your account balance. If non\-refundable items exist (for example, volume specifications unchanged), the refund may be USD 0.00. The refund is subject to the actual order.

6. After payment is complete, return to the Claw list and check whether the target instance's type has been updated.
