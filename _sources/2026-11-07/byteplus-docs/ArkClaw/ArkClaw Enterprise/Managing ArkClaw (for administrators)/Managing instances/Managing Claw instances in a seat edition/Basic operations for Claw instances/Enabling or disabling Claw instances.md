---
title: "Enabling or disabling Claw instances"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Managing_instances"
---

To temporarily reclaim an employee's Claw instance usage permissions, release a seat quota, or handle cases where an employee leaves or has their account disabled, the administrator can disable the employee's Claw instance in the console. The instance can be enabled again after the employee resumes usage or the seat quota meets the required condition. **This article describes how to disable a running Claw instance or re\-enable a stopped instance.** 

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Enabling a Claw instance occupies a seat quota again. After a Claw instance is disabled, it may fail to be enabled again for the following reasons:</div>



* <div data-tips="true" data-tips-type="warning">The number of seats used in the current space has reached the seat quota. It is recommended to confirm <a href="https://docs.byteplus.com/en/docs/ArkClaw/Managing_seats?lang=en#bFA7u5YW">seat quota and current usage</a>. To re\-enable the instance, modify the seat quota or delete other instances that occupy seats, and then retry.</div>


* <div data-tips="true" data-tips-type="warning">The number of seats used by the current employee has reached the upper limit of the seat quota assigned to them. You can <a href="https://docs.byteplus.com/en/docs/ArkClaw/Managing_employee-level_seat_settings">increase the seat quota</a> for the employee.</div>



<span id="oWWU977A"></span>
## Scenarios

When an employee is temporarily away, needs to freeze an instance for security reasons, or needs to free up seat quota, their Claw instance can be disabled. Disabling is a **reversible** action; instance configuration and data are retained, and the instance can be re\-enabled at any time. To completely release resources, [delete Claw instances](https://docs.byteplus.com/en/docs/ArkClaw/Deleting_Claw_instances?lang=en) (irreversible).

<span id="ll2LNNMU"></span>
## Procedure


1. Log in to [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise)[ArkClaw Group console](https://console.byteplus.com/arkclaw/enterprise/group/).

2. In the left\-side navigation pane, choose "Claw management \> Claw list".

3. The "Instances" tab displays the list of currently created employee Claw and shared Claw instances. Enable or disable Claw instances as needed.

   * **Disable a Claw instance**

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">After disabling, the corresponding Claw instance becomes unavailable immediately. Any task or session in progress is interrupted. It is recommended to confirm with the relevant employee before disabling to avoid affecting ongoing work.      </div>
      

      1. In the Claw list, click "Disable" in the "Actions" column for the target Claw.

      2. In the dialog box that appears, click the "Disable" button to complete the operation. After it is disabled, the Claw instance status changes to "Stopped". On the enterprise employee side, this Claw instance becomes unavailable, and the status of the corresponding instance on the employee side is updated synchronously.

   * **Enable a Claw instance**

      1. In the Claw list, click the "Enable" button in the "actions" column for the target Claw.

      2. In the pop\-up dialog box, click the "Enable" button to complete the operation. After enabling, the Claw instance status changes to "Running". On the enterprise employee side, this Claw becomes usable again, and the status of the corresponding instance on the employee side is updated synchronously.
