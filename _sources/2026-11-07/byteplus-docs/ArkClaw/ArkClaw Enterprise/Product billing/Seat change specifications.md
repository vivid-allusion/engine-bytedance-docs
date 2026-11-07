---
title: "Seat change specifications"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Modify_seat"
---

If the current ArkClaw seat editions cannot meet your business requirements, you can modify seat settings, such as adjusting the editions and number of seats.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This topic applies to workspaces of the seat management type. Workspaces of the instance management type do not involve the concept of "seats". Related resources must be managed in the instance list. If you are using a workspace of the instance management type, please go to the instance list to view and perform the corresponding operations. For details, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Managing_separately_purchased_Claw_instances">Managing independently purchased Claw instances</a>.</div>


<span id="I03Y18sh"></span>
## Change type


* New purchase: Seat count changes from 0 to 1 (or more).

   * Upgrade: Increases the seat count or switches to a higher seat edition.

   * Downgrade: Reduces the seat count or switches to a lower seat edition.

   * Unsubscribe: Changes the seat count of the target edition to 0.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After unsubscription, the platform will provide a resource retention period of 168 hours (7 days). During the retention period, if you need to purchase the seat again, you need to resume the instance that stopped due to unsubscription to use the seat.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can resume the seat by renewing it on the <a href="https://console.byteplus.com/finance/instance-manage">Renewal center instance page</a>. You can also click "Restore original order" on the seat setting modification page to resume the seat based on the on\-screen prompts.   </div>
   


<span id="d2Jsjd2G"></span>
## Modification rules

These rules apply only to scenarios where seats are not allocated. To modify allocated seat settings, you need to [permanently delete instances](https://docs.byteplus.com/en/docs/ArkClaw/Deleting_Claw_instances) first.


|Change target |Purchase |Upgrade |Downgrade |Unsubscribe |
|---|---|---|---|---|
|ArkClaw |Supported |Supported |Supported |Supported |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="0">tip</div>


* <div data-tips="true" data-tips-type="default" data-wrapper-indent="0">After ArkClaw seats are modified, the validity period remains unchanged, and fees are calculated based on the instructions described in Instructions on changing resource billing rules. For details, see <a href="https://docs.byteplus.com/en/docs/byteplus-platform/Billing_Rules_for_Resource_Subscription_Change">Instructions on changing resource billing rules</a>.</div>


* <div data-tips="true" data-tips-type="default" data-wrapper-indent="0">CodingPlan and ArkClaw are not strongly coupled. When changing seats, you can purchase CodingPlan in combinations based on your actual needs. For more information about CodingPlan, see <a href="https://docs.byteplus.com/en/docs/ModelArk/2276791#rules">Managing Coding Plan Enterprise packages</a>.</div>


* <div data-tips="true" data-tips-type="default" data-wrapper-indent="0">The validity period of CodingPlan is the duration that you select when you modify seats (UTC+8 time). A billing cycle starts when the resources are delivered (accurate to the second) and ends at 23:59:59 on the expiration date.</div>



<span id="dliyCPBh"></span>
## Billing formula

**Total payable amount for upgrade order**

= New configuration fee \- Residual value of the original configuration

= Listed price of new configuration (hourly) \* Remaining duration (hours) \* Discount \- Listed price of original configuration (hourly) \* Remaining duration (hours) \* Discount

**Total payable amount for downgrade order**

= New configuration fee \- Refundable residual value of the original configuration

= Listed price of new configuration (hours) \* Remaining duration (hours) \* Discount \- (Actual value of order \- Actual value of order \* Used duration/Subscription duration \* Downgrade refund coefficient)

> Downgrade refund coefficient:

> * For usage duration ≤ 30 days: the refund coefficient = 1.5

> * For usage duration \> 30 days: the refund coefficient = 1.00


<span id="GexvByUC"></span>
## Procedure

If you need to change unassigned seats, refer to [Seat change](https://docs.byteplus.com/en/docs/ArkClaw/Managing_seats) for details.


&nbsp;
