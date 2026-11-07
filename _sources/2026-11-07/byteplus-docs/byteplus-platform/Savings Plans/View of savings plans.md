---
title: "View of savings plans"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/view-of-savings-plans"
---

<span id="9RN0ZQOV"></span>
# Overview

To go to the Overview tab, click [Savings plans > Overview](https://console.byteplus.com/finance/saving-plan) in the Billing Center.

On the Overview tab, you can view the overview of your instances of savings plans, such as their savings, or purchase new savings plans.

<span id="WXRsnvVm"></span>
## Parameters


* Instance ID: The instance ID of the savings plan, which is a unique identifier.

* Instance name: The instance name of the savings plan.

* Product: The name of the cloud product. For this parameter, filtering is supported.

* Configuration name: The name of the configuration. For this parameter, filtering is supported.

* Commitment: The committed spend during the term of a diminishing savings plan, or the committed spend during each period of a periodic savings plan. Whether it is used or not, the corresponding amount is charged.

* Remaining amount: The remaining amount of a diminishing savings plan during its term, or the remaining amount of a periodic savings plan during its current period.

* Cumulative savings: The total amount saved under the savings plan during its term, which is calculated against what would have been charged under pay\-as\-you\-go billing.

* Resource type: The type of the savings plan. Valid options: Diminishing or Periodic. For this parameter, filtering is supported.

* Owner: The account to which the savings plan belongs.

* Status: The status of the savings plan. Valid options: Not in effect, Effective, Used up, Expired, Refunded, Restricted or Failed to create. For this parameter, filtering is supported.

* Committed purchase duration: The committed duration of the savings plan.

* Payment option: The proportion of the savings plan cost that was paid upfront.

* Purchase time: The time when the savings plan was purchased (UTC+8). For this parameter, sorting is supported.

* Effective time: The time when the savings plan takes effect (UTC+8). For this parameter, sorting is supported.

* Expiry time: The time when the savings plan expires (UTC+8). For this parameter, sorting is supported.

* Actions: You can click Details to go to the Details tab.


<span id="9NyZBA7m"></span>
# Details

To go to the Details tab, click [Savings plans > Details](https://console.byteplus.com/finance/saving-plan?savingPlanTab=2) in the Billing Center.

On the Details tab, you can view the details of your instances of savings plans.

<span id="ZySjcoiU"></span>
## Parameters


* Owner: The account to which the savings plan belongs.

* Product: The name of the cloud product. For this parameter, filtering is supported.

* Configuration name: The name of the configuration. For this parameter, filtering is supported.

* Instance ID: The instance ID of the savings plan, which is a unique identifier.

* Instance name: The instance name of the savings plan.

* Resource type: The type of the savings plan. Valid options: Diminishing or Periodic. For this parameter, filtering is supported.

* Deduction time: The time when the savings plan was applied to offset the pay\-as\-you\-go bill.

* Deduction commitment term: The commitment term corresponding to the amount deducted by the savings plan in this transaction.

* Deduction carry\-over period: Applies only to carry\-over eligible savings plans, the carry\-over period corresponding to the amount deducted by the savings plan in this transaction.

* Amount before deduction: The remaining amount of a diminishing savings plan during its term before this deduction, or the remaining amount of a periodic savings plan during its current period before this deduction.

* Deducted amount: The amount deducted from the savings plan, which equals the gross amount multiplied by the discount percentage.

* Amount after deduction: The remaining amount of a diminishing savings plan during its term after this deduction, or the remaining amount of a periodic savings plan during its current period after this deduction.

* Gross amount of deducted portion: The gross amount of the portion of the pay\-as\-you\-go bill offset by the savings plan.

* Deduction discount: The discount used when the savings plan was applied to offset the pay\-as\-you\-go bill.

* Equivalent pay\-as\-you\-go amount: The gross amount of the portion of the bill offset by the savings plan that is to be charged if you had used the pay\-as\-you\-go discount instead of the savings plan.

* Savings: The amount saved by the savings plan, which equals the equivalent pay\-as\-you\-go amount minus the amount deducted from the savings plan.

* Gross amount of bill: The original gross amount of the pay\-as\-you\-go bill offset by the savings plan.

* Deduction rate: The percentage of the gross bill amount offset by the savings plan, which equals the gross amount of the deducted portion divided by the bill gross amount (rounded to two decimal places).

* Usage period of bill: The time when the usage in the pay\-as\-you\-go bill offset by the savings plan was consumed.

* Account of bill: The account to which the pay\-as\-you\-go bill offset by the savings plan belongs.

* Instance ID of bill: The instance ID of the pay\-as\-you\-go bill offset by the savings plan.

* Product of bill: The cloud product of the pay\-as\-you\-go bill offset by the savings plan. For this parameter, filtering is supported.

* Configuration of bill: The configuration of the pay\-as\-you\-go bill offset by the savings plan. For this parameter, filtering is supported.

* Billing unit of bill: The billing unit of the pay\-as\-you\-go bill offset by the savings plan. For this parameter, filtering is supported.

* Region of bill: The region to which the pay\-as\-you\-go bill offset by the savings plan belongs.

* Impact factor of bill: The pricing impact factor of the pay\-as\-you\-go bill offset by the savings plan.


&nbsp;

<span id="5rkYAE1h"></span>
# Commitment Term Details

You may go to [Savings plans > Overview](https://console.byteplus.com/finance/saving-plan), then click the Instance ID to access the page.

On this page, you can view the specific information for each commitment term of the Savings Plan instance.

<span id="Cbg8JksT"></span>
## Parameters


* Commitment term: The time period of each commitment cycle for the Savings Plan instance, in UTC+8 time zone.

* Configuration name: The name of the configuration.

* Commitment: The committed spend during the term of a diminishing savings plan, or the committed spend during each period of a periodic savings plan.

* Remaining amount: 

   * Parent row: Represents the total remaining amount for the current cycle of the Savings Plan.

   * Child row: Represents the remaining amount within the current cycle of the Savings Plan, broken down by different actual effective times.

* Committed purchase duration: The committed duration of the savings plan.

* Pre\-deduct Occurred：Indicates whether activation in advance has occurred in the current commitment cycle.

* Pre\-deduct activation time：The time at which activation in advance has occurred was applied in the current commitment cycle.

* Carry\-over rules: carry\-over eligible/carry\-over ineligible.

* Carry\-over ratio: Applies only to carry\-over eligible savings plans. It refers to the proportion of the commitment amount in each commitment term that may be carried over to the next commitment term.

* Actual Effective Time: It represents the valid time range during which the commitment amount of the savings plan is effective. Any unused amount after the end of the carry\-over period will expire. Time zone: UTC+8.

   * For non\-rollover quota, the actual expiration time is the end of the current cycle.

   * For rollover quota, the actual expiration time is the end of the next cycle.

* Total amount: Represents the total available amount within each actual effective term.

* Status: Status of the corresponding amount under the savings plan. Valid options: Not in effect, Effective, Expired, Used Up, Refunded, or Restricted.
