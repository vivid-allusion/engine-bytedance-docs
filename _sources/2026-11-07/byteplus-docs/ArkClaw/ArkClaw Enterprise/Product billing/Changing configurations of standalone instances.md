---
title: "Changing configurations of standalone instances"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Changing_configurations_of_standalone_instances"
---

ArkClaw standalone instances have exclusive computing resources (vCPU, memory, and cloud disks) and do not share resources with other instances. When the current instance type cannot handle the business load, or when business volume decreases and costs need to be reduced, you can change the instance type online by changing its configurations (upgrading or downgrading the instance) without the need to recreate an instance.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This topic applies to operations on <strong>standalone instances</strong> in workspaces of the <strong>instance management</strong> type. To change the specifications of <strong>seats</strong> in workspaces of the <strong>seat management</strong> type, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Modify_seat">Changing seat specifications</a>.</div>


<span id="UWQXr98z"></span>
## Billing formula

**Standalone instances** support real\-time configuration upgrades or downgrades. After configurations are changed, the new configurations remain effective until the next configuration change or instance release.


* **Total payable amount for an upgrade order**

      * = New configuration fee \- Residual value of the original configuration

      * = Listed price of new configuration (hourly) \* Remaining duration (hours) \* Discount \- Listed price of original configuration (hourly) \* Remaining duration (hours) \* Discount

   * **Total payable amount for downgrade order**

      * = New configuration fee \- Refundable residual value of the original configuration

      * = Listed price of new configuration (hours) \* Remaining duration (hours) \* Discount \- (Actual value of order \- Actual value of order \* Used duration/Subscription duration \* Downgrade refund coefficient)

   > Downgrade refund coefficient:1.5   
   

   <span id="ndX3eUds"></span>
   ## Notes for modifying instance specifications


|Module |Description |
|---|---|
|**Billing rules** |The configuration change is billed immediately at the hourly list price of the new instance type. Prices are rounded to four decimal places, and the final amount displayed in the console prevails.<br><br>The configuration change is a paid operation. **For upgrades, you pay the price difference** (calculated based on the remaining billing cycle and the price difference). **For downgrades, a refund is issued based on the rules**. The refund amount is the lesser of the actual paid amount of the original order and the price difference between the new and old configurations. If the original order enjoyed a high discount, the refund may be **0**.<br><br>Vouchers can be used to offset the configuration change order amount. Refunds are returned to your account balance via the original payment method. |
|**Change scope** |The configuration change only involves **vCPU** and **memory**. It does not involve **cloud disks** or the **instance expiration time**. |
|**Operation path** |For detailed steps, see [Changing instance types](https://docs.byteplus.com/en/docs/ArkClaw/Changing_Claw_instance_types). |
|**Effective method** |After the configuration change order is placed, the instance **automatically restarts and is unavailable for about 5 minutes,**  and the new configuration takes effect immediately after the instance restarts. |
|**Failed rollback** |If configurations fail to be changed, the system will automatically roll back the instance to the original type and original status. |
