---
title: "Managing space-level seat settings"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Managing_seats"
---

Administrators can view and manage Claw seats and ModelArk Plans (Agent Plan Team and Coding Plan Team) in real time based on actual business conditions, and purchase and allocate them appropriately to reduce costs.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><strong>If you have enabled the "Space management type" beta feature and selected "Instance Management" as the space management type when activating the ArkClaw space, the operations described in this topic do not apply.</strong></div>


<span id="bFA7u5YW"></span>
## View space\-level seat information


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Resource Configuration" \> "Seats".

3. On the "Seat overview" tab, view Claw seats and ModelArk Plans.

   
   |Module |Description |Screenshot |
   |---|---|---|
   |Overview |Displays the total number of purchased Claw seats and the number of available seats in the current space, as well as the total number and the remaining available number of ModelArk Plans. |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_76c7b4ceb0931f5200db3fd6a4e9c7eb.png) </span><br><br> |
   |Claw seats |Displays information about Claw seats of different editions in the current space.<br><br><br>* **Purchased seat information**: The total number of seats of all editions currently purchased, and the total number of remaining allocable seats. If the seat purchase limit has been reached and can no longer meet business needs, you can [increase the space seat quota limit](https://docs.byteplus.com/en/docs/ArkClaw/Managing_seats?TagIDs=&lang=en#vcdZU86f).<br><br>* **Seat information of editions**: The allocation status of seats under each purchased edition. Administrators can change seat configurations at any time based on business requirements. For detailed instructions, see [Changing seat editions for spaces](https://docs.byteplus.com/en/docs/ArkClaw/Managing_seats?TagIDs=2,522,512,502&lang=en#VXiPTnK5). ||
   |Ark Plan |Displays the number of available Agent Plan Team and Coding Plan Team resources in the current ArkClaw space, including ModelArk Plans purchased and managed within the ArkClaw space. Administrators can view ModelArk Plan details in the current space, configure ModelArk Plan allocation schemes, and manage plans purchased in ModelArk. For detailed instructions, see [Managing ModelArk Plans](https://docs.byteplus.com/en/docs/ArkClaw/Managing_CodingPlan). ||
   


<span id="PgemHtiH"></span>
## Check the space renewal status.


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Resource Configuration" \> "Seats".

3. Click "Order management" in the upper\-right corner.

4. Check whether auto\-renewal is enabled for the current space.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you select the "Auto\-renewal on expiration" option during space activation, automatic renewal will be enabled for the space.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If automatic renewal is enabled, all changed and managed orders will be automatically renewed before expiration. To disable this option separately:   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For <strong>ArkClaw seats</strong>, do so in the <a href="https://console.byteplus.com/finance/renew">order center</a>.   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For <strong>Coding Plan Team</strong> and <strong>Agent Plan Team</strong>, do so in <a href="https://console.byteplus.com/ark/region:ark+cn-beijing/overview?briefPage=0&briefType=introduce&type=new">BytePlus ModelArk</a>.   </div>
   


<span id="VXiPTnK5"></span>
## Change the seat edition for the space.

If the purchased seats are insufficient, or if you need to change seat editions after purchasing seats, you can change the seats at any time. For details on the rules and fees related to changing seat settings, see [Notes on seat changes](https://docs.byteplus.com/en/docs/ArkClaw/Modify_seat). You can also change the allocated seat editions. For details, see [Changing Claw instance seat levels](https://docs.byteplus.com/en/docs/ArkClaw/Managing_instances).


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Resource Configuration" \> "Seats".

3. Click "Change seats" in the upper\-right corner of the page.

4. In the pop\-up window, select the number of seats for the target edition.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Expiration time alignment rule</strong>: Modifying the seat quantity does not affect the expiration time of the original order. All seats in the same edition always share the same expiration time. If the original seat quantity for an edition (that is, the first purchase of this edition) is 0, the seat expiration time will be automatically aligned with the order with the shortest validity period among all your already purchased seats.   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Example: Suppose that you already have 10 Standard seats (expiring on December 31, 2026) and 10 Premium seats (expiring on October 31, 2026), and purchase 5 additional Standard seats and 5 Ultimate seats (which were previously zero). The 15 Standard seats will automatically adopt the expiration date of December 31, 2026, while the 5 Ultimate seats will inherit the shortest existing term, expiring on October 31, 2026 (matching the Premium seats). Fees are charged based on the actual number of days used.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Bundled purchase of Agent Plan Team</strong>: If you need to purchase Agent Plan Team together with seats of a specific edition, select an Agent Plan Team package as needed from the "Recommended to pair with Agent Plan Team" card below. <strong>Agent Plan Team purchases are ‌non\-refundable‌ once completed</strong>.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Purchase quantity limit</strong>: The total cumulative number of Agent Plan Team seats in ArkClaw (including those purchased and managed ModelArk Agent Plan Team within ArkClaw) must be at least 5, and the maximum quantity per order is 1,000.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Other limits</strong>:   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">ArkClaw seats and Agent Plan Team packages do not have a one\-to\-one mapping. All Claw instances under an employee's account share the allocated Agent Plan Team packages.   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">All Claw instances with access to the seat edition of Coding Plan Team packages share all Coding Plan Team resources for that seat edition.   </div>
   

5. On the right side of the dialog box, inspect the change details and the price difference. If nothing is wrong, select the "I have read and agree to the Terms of Service and Model Service Agreement" checkbox.

6. Click "Confirm" and follow the on\-screen instructions to cover the price difference or receive your refund.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Seat changes take effect immediately upon completion. For detailed billing rules, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Modify_seat?lang=zh#dliyCPBh">Notes on seat changes</a>.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you purchase Claw seats and the Agent Plan Team at the same time, you need to pay for the orders separately. You can view details of unpaid orders on the "Order management" page.   </div>
   

   <span id="BoYDpX91"></span>
   ## Manage space order information.

   Manage seats and ModelArk Plan orders. On the "Order management" page, you can view unpaid ArkClaw seat orders and ModelArk Plan orders, as well as paid ArkClaw seat orders. To view paid ModelArk Plan orders, go to the ModelArk console. For more information, see [Managing orders](https://docs.byteplus.com/en/docs/ArkClaw/Managing_orders).

   1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Resource Configuration" \> "Seats".

3. Click "Order management" in the upper\-right corner of the page.

4. Manage orders.

   * **Unpaid orders**: In the list, click "Pay" or "Cancel order" next to the unpaid order to make payment or cancel the order.

   * **Paid ArkClaw orders**: View information on currently paid ArkClaw orders. Click the "Renew" button on a target order to renew the ArkClaw seat edition. Click "View ModelArk Plan orders" to go to the ModelArk platform to view ModelArk Plan orders.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>ArkClaw seat expiration</strong>: After expiration, all Claw instances associated with the expired seat edition will be frozen. Employees cannot start new sessions, but existing sessions and bound resources remain read\-only during the 7‑day retention period. After the retention period expires, data will be permanently deleted and cannot be recovered. To renew seats during the 7\-day retention period, pay for the full seat quantity in the original order.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>ModelArk Plan seat expiration</strong>: After expiration, the related plans cannot be used normally, and <strong>renewal is supported only within the 12\-hour window after that. After the 12\-hour window, renewal is unavailable</strong>. To continue using the service, repurchase ModelArk Plan seats. We recommend enabling automatic renewal or setting a reminder 3 days before expiration to prevent business disruptions.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Invalidation of unpaid orders</strong>: Unpaid orders will be automatically canceled after 30 minutes. If you initiate a new seat adjustment during this period, the existing unpaid order will also be canceled immediately.   </div>
   

   <span id="vcdZU86f"></span>
   ## Increase the space seat quota limit

   The total quota displayed under each seat edition is the platform's default minimum quota that each workspace can apply for that seat edition. If this quota cannot meet business needs, administrators can apply to increase the seat quota on their own.

   1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Resource Configuration" \> "Seats".

3. Click "Quota center" in the upper\-right corner of the page.

4. In the BytePlus quota center, select "arkclaw" from the product drop\-down list. In the Quota parameter field, enter the keyword "claw_seat_" and select the seat quota to be increased. Then, select the target region.

5. Click "Apply" in the Actions column for the target seat quota. Set the target quota and provide the application reason.

6. Click "Submit". When your application is approved, the seat quota is increased.
