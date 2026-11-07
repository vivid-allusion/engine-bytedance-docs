---
title: "Managing ModelArk Plans"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Managing_CodingPlan"
---

You can directly purchase and use ModelArk Plans (Agent Plan Team and Coding Plan Team) in ArkClaw, or you can manage Coding Plans already purchased in ModelArk and use them in ArkClaw in a centralized manner. After being managed, the Coding Plan remains under the ownership of ModelArk. ArkClaw is granted only the invocation permissions and assumes responsibility for the rotation of API Keys.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><strong>If you have enabled the "Space management type" beta feature and selected "Instance Management" as the space management type when activating the ArkClaw space, the operations described in this topic do not apply.</strong></div>


<span id="DgYucjs7"></span>
## Operation instructions


* **ModelArk Plans purchased in ArkClaw, and those brought under management in ArkClaw are not recommended for use outside ArkClaw.**  ArkClaw Enterprise periodically rotates the API keys of managed ModelArk Plans, which may affect usage in other scenarios. If a ModelArk Plan is used for both ArkClaw and other purposes, we recommend purchasing it directly from ModelArk to obtain an API key and then configuring the model via "Custom model source". For detailed instructions, see [Configuring custom model pools](https://docs.byteplus.com/en/docs/ArkClaw/Model_management?lang=en#MXrT1Usf).

* If auto\-renewal is enabled for the ArkClaw space, **ModelArk Plans purchased in ArkClaw and those managed by ArkClaw** will have auto\-renewal enabled simultaneously.

* ArkClaw seats and ModelArk Plans do not have a one\-to\-one mapping. All the ModelArk resources can be shared by any ArkClaw seat.


<span id="ADWRkeHz"></span>
## Purchase ModelArk Plans


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Resource Configuration" \> "Seats".

3. On the "Seat overview" tab, click "Purchase Ark Plan" to the right of ModelArk Plan.

4. Select the type, quantity, and duration of the ModelArk Plan you need, and check "I have read and agree to Terms of Service and Model Service Agreement".

5. Click "Confirm change" and follow the instructions to pay the relevant fees.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Unpaid orders will be automatically canceled after 30 minutes. If you initiate a new seat adjustment during this period, the existing unpaid order will also be canceled immediately.   </div>
   

   <span id="6fB80U2K"></span>
   ## Manage existing ModelArk Plans

1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Resource Configuration" \> "Seats".

3. On the "Seat overview" tab, click "Managed Seats" to the right of ModelArk Plan.

4. Select the ModelArk Plans to be managed, and click "Confirm" to complete the operation.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Only existing and unbound ModelArk Plan seats are displayed. After being managed, they can be centrally managed in the current ArkClaw space.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The managed Coding Plan remains visible in ModelArk, but its API Keys will be periodically rotated by ArkClaw.   </div>
   


<span id="AgoHFagb"></span>
## View existing ModelArk Plans

When you need to check whether the total amount of ModelArk Plans in the current workspace meets business requirements, or to investigate employee feedback of "insufficient token quotas", you can view details by performing the following steps.


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Resource Configuration" \> "Seats".

3. On the "Seat overview" tab, click "Ark Plan Details" on the right.

4. You can view the ID, seat edition, status, and expiration time of all ModelArk Plans in the current ArkClaw space.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Click "Refresh" to refresh the current ModelArk Plan data. You can use the ModelArk Plan ID to view information about a specific Plan in the ModelArk console.   </div>
   

<span id="lfxDota8"></span>
## Configure the ModelArk Plan allocation method


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Resource Configuration" \> "Seats".

3. On the "Seat overview" tab, click "Allocation Settings" on the right.

4. Set the Ark Plan allocation method and allocation priority, and then click "Confirm" to complete the operation.

   * **Manual allocation**: Disable **Auto\-Allocate Ark Plan Seats**. ModelArk Plans can be manually allocated to employees only by administrators.

   * **Automatic allocation**: Enable the "Auto\-Allocate Ark Plan Seats" option. The system will automatically allocate ModelArk Plans to employees who have not yet been allocated a ModelArk Plan seat, according to the configured allocation priority, until no allocatable quota remains.
