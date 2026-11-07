---
title: "Application of savings plans"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/application-of-savings-plans"
---

<span id="Njfn3Qrc"></span>
# Application rules


* The Savings Plan supports offsetting billing items corresponding to pay\-as\-you\-go bills. Deduction is applicable when, at the end of the consumption period of a pay\-as\-you\-go bill, the Savings Plan quota period is either in  **"Active"**  status, or in  **"Pending"**  status that supports pre\-deduction.

   * For example, you purchased a 3‑month commitment Savings Plan on September 5th, expiring on December 5th. The three corresponding commitment terms are: September 5th – October 5th, October 6th – November 5th, November 6th – December 5th.

   * For the second commitment term, the validity period of the carry\-over ineligible portion is October 6th – November 5th, and the validity period of the carry\-over eligible portion is October 6th – December 5th. For the third commitment term (the final term of the order), the validity period of all amount is November 6th – December 5th.

   * Bills with usage period end times between November 6th and December 5th may be deducted using the carry\-over eligible portion from the second commitment term and all amount from the third commitment term. Examples include hourly bills from 14:00–15:00 on November 8th, and monthly bills for November 1st – 30th.

   * Monthly bills for consumption during December 1st – 31st are not eligible for deduction, as no valid Savings Plan applies.

   * If early deduction is supported, bills with a consumption end time falling between October 6 and November 5 — for example, an hourly bill for 14:00–15:00 on October 8 — can be offset using the full quota of the 2nd commitment period as well as the full quota of the 3rd commitment period.

* Savings plans do not apply to spot Instances or elastic scheduled instances.

* Savings plans deduction discount: Take the lower of the contract price discount and the default deduction discount of the savings plan; special event discounts are not eligible for the savings plan deduction.

* Financial hosting:

   * The charges of pay\-as\-you\-go instances under a Sub\-Account can be offset by the savings plans of the Sub\-Account or the Master Account. However, the savings plans of the Sub\-Account are preferred.

   * The charges of pay\-as\-you\-go instances under a Master Account can only be offset by the savings plans of the Master Account.

* Resell:

   * End users from a reseller cannot purchase savings plans.

   * Resellers can purchase savings plans to offset the charges of their own pay\-as\-you\-go instances, but not those of their end users.


<span id="4IHiVYdD"></span>
# Deduction order


* If savings plans, resource packages, reserved instance vouchers, reserved capacity plans, and coupons exist at the same time, they are deducted in the following order: reserved instances or reserved storage capacities \> resource packages \> savings plans \> coupons.

* If multiple savings plans are eligible to offset bills, for multiple billing items of the same product, the system determines their priorities as follows:

   1. In the financial hosting scenario, the sub\-account’s bills are first deducted with the sub\-account’s own savings plans; any excess amount can then be further deducted with the master account’s savings plans.

   1. Savings plans that expire sooner are preferentially applied. The expiration time of a periodic savings plan refers to the end of its current carry\-over period.

   1. Combinations of savings plans and pay\-as\-you\-go bills that yield higher savings rates are preferentially applied.

   1. For combinations that yield the same savings rate, savings plans with higher discount percentages are preferentially applied.

* A savings plan is applied in the preceding order until all pay\-as\-you\-go charges are covered or the committed spend of the savings plan is used up. Pay\-as\-you\-go charges not covered by savings plans are billed and settled in standard pay\-as\-you\-go mode.
