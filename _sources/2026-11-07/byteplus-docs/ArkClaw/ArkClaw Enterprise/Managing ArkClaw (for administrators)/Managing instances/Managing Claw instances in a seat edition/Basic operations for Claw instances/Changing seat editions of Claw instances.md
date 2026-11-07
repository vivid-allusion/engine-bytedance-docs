---
title: "Changing seat editions of Claw instances"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Changing_Claw_instance_seat_levels"
---

The administrator can change the seat edition of a Claw instance for an employee (the seat edition determines the range of models and compute specifications available to the Claw instance. For details, see [seat specifications](https://docs.byteplus.com/en/docs/ArkClaw/Billing_instructions?lang=en#Q8ldd5U3)). After the change, the instance type and available models will be updated accordingly. **This topic describes how to change the seat edition for a single Claw instance or in bulk.** 

<span id="4HOTlGQA"></span>
## Instructions


* Only Claw instances in the **Running** or **Stopped** state support changing the seat edition.

* Rules for model changes after instance scaling up or down:

   * If the original model **is still within** the available model range of the new seat, the model remains unchanged.

   * If the original model **is not within** the available model range of the new seat, it will automatically switch to the default model of the new seat.

* After the seat edition is changed, the Claw instance will restart, which is expected to take 1 minute. During this period, the Claw instance will be unavailable. Please perform this operation during idle periods.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After the seat edition is changed, Claw will automatically restart, which is expected to take about 1 minute. During this period, employees cannot use the Claw instance. Please perform this operation when employees are idle.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When you change seat editions in bulk, all selected instances will restart simultaneously. Please evaluate the impact range before proceeding. It is recommended to execute in batches or notify relevant employees in advance.   </div>
   


<span id="LdEoi3dT"></span>
## Procedure


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise)[ArkClaw Group console](https://console.byteplus.com/arkclaw/enterprise/group/).

2. In the left navigation pane, choose "Claw Management \> Claws".

3. Under the "Instances" tab, the list of currently created employee Claw/shared Claw instances is displayed,

4. In the Claw instance list, change the seat edition of the Claw instance.

   * **Single modification**

      1. Click the "More \> Seat edition change" button in the instance actions column of the target Claw instance.

      2. In the dialog box that appears, select the target seat, then click the "OK" button to complete the action.

   * **Bulk modification**

      3. Select the Claw instances whose seat editions need to be modified, and click the "<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a43ad405cbf241ce07696879335f16a7.png) </span>\> Seat edition change" button at the bottom of the page.

      4. In the dialog box that appears, select the target seat, then click the "OK" button to complete the action.

5. Return to the Claw list page and confirm that the seat edition column for the target instance has been updated to the target value, and that the instance status has been restored to Running.
