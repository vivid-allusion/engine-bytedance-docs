---
title: "Managing employee-level seat settings"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Managing_employee-level_seat_settings"
---

You can allocate seat quotas and ModelArk Plans (Agent Plan Team and Coding Plan Team) to specific employees and view token usage within a specified time period.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><strong>If you have enabled the "Space management type" beta feature and selected "Instance Management" as the space management type when activating the ArkClaw space, the operations described in this topic do not apply.</strong></div>


<span id="OfEYSIoB"></span>
## Prerequisites

Employee seat quotas are conditional on employee information. If no employee data is imported, the "Employee quotas" section will be empty. Resolve this issue by completing the [employee information import](https://docs.byteplus.com/en/docs/ArkClaw/Importing_user_information-) first.

<span id="afTZ9x0D"></span>
## Operation instructions


* **Seat quotas only serve as the upper limit for application eligibility. The final allocation result is subject to real\-time system inventory verification**. When inventory is insufficient, employees applying for seats will receive a prompt similar to "No seats available". Administrators can upgrade or reclaim allocated seats by referring to [Managing workspace seats](https://docs.byteplus.com/en/docs/ArkClaw/Managing_seats).

* Each employee can be allocated **one Coding Plan Team package** or **multiple Agent Plan Team packages**.

* To control overall costs, ArkClaw applies the following default token rate limits for employees:

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">This rate limiting is only the default limit on the ArkClaw side and is not related to the quota of the <strong>Agent Plan Team or Coding Plan Team</strong> you purchased. Enterprise administrators can adjust token limits for employees as needed.   </div>
   

   * If an employee is not allocated a ModelArk Plan, the Token limit is 1 million per minute and 40 million per day. If an employee is allocated a ModelArk Plan, the per\-user Token limit will be subject to the default values listed below, and the Token limit is shared across all ArkClaw instances under that employee.

      * **Agent Plan Team**: Token usage under Agent Plan is not subject to ArkClaw\-side "per\-minute/per\-day Token limit" restrictions, nor is it counted in employee rate\-limit statistics. Usage is controlled by ModelArk. For more details, see [AFP deduction rules within the package](https://docs.byteplus.com/en/docs/82379/2516283).

      * **Coding Plan Team:**  The default token rate limiting is configured in ArkClaw for employees. Enterprise administrators can adjust it as needed by referring to the **Edit employee seat quotas** section of this topic. The specific rate limiting values are subject to the actual configuration.

* Configuration priorities: When multi\-level configurations (space configuration, seat quota, and templates) coexist, refer to [Configuration priorities](https://docs.byteplus.com/en/docs/ArkClaw/Space_information#T8JVArgA) for detailed rules. The core principles are as follows:

   * Personal configuration over space\-level configuration: Customized seat quotas and token limits for an employee have higher priority than the space\-level default settings.

   * Employees with individually edited configurations: Their individually edited configurations apply and will not be affected by subsequent space\-level configuration changes.

   * Employees without individually edited configurations: They will inherit the space\-level per\-employee seat quota and the model throttling settings specified in the space\-level model configuration.

   * Space quota reduction and over\-quota management: If space quota reductions cause employee quota usage to exceed new space\-level limits, the system marks the employee as "Over\-quota". In this case, their existing seats will be retained, but they will be prohibited from applying for new seats. The administrator can directly edit the seat quota of the employees to reclaim seats, or the employees can delete excess instances. Then, the employees can continue to apply for new seats based on the new quota.


<span id="Wwp77Heu"></span>
## Editing employee seat quotas


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click "Resource Configuration" \> "Seats".

3. On the "Employee quota" tab, configure seat quotas for employees.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you manage a large number of employees or organizations, you can use the search box to quickly search for target employees or groups.   </div>
   

   
   <Tabs>
   <Tab zoneid="OlrjNThA" title="Edit seat quotas for employees individually">
   <TabTitle>Edit seat quotas for employees individually</TabTitle>
   
   1. In the employee list, find the employee and click "Edit" in the Actions column.
   
   2. In the pop\-up window, set the number of seats that can be applied for under each edition, ModelArk Plan, and token limit for the employee, then click "Confirm" to complete the edit.
   
   
   </Tab>
   <Tab zoneid="EbOZNwPv" title="Edit seat quotas for employees in batches">
   <TabTitle>Edit seat quotas for employees in batches</TabTitle>
   
   * **Method 1: Edit quotas in the employee list**
   
      1. In the employee list, select the checkboxes to the left of the target employees.
   
      2. Click "Batch edit quota" at the bottom of the list. In the pop\-up window, set the number of seats per edition that the employees can request, and click "Confirm".
   
   * **Method 2: Edit quotas in user groups**
   
      1. Click "Groups" in the upper\-right corner of the employee list to switch to the group view.
   
         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
         
   
         <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If no user group is configured, no groups will be displayed. If necessary, <a href="https://docs.byteplus.com/en/docs/ArkClaw/Manage_user_information">create a user group</a>.      </div>
         
   
      2. On the left side, select the checkbox before a user group name. The member information will be displayed on the right side.
   
         * **Change quotas for some members in a user group**
   
            1. In the right\-side group member list, select the checkboxes for the target members and click "Batch edit" at the bottom of the list.
   
            2. In the pop\-up window, set the number of seats that can be applied for under each edition, ModelArk Plan, and token limit for the employee, then click "Confirm" to complete the edit.
   
         * **Change quotas for all members in a user group**
   
            1. Select the target user group(s) on the left and click "Batch edit group quota" below the user group list.
   
            2. In the dialog box that appears, set the number of seats that the user group(s) can request per edition, and click "Confirm".
   
   
   </Tab>
   </Tabs>
   

4. After successful editing, the "Quota source" in the employee list will change to "Custom." Scroll the horizontal bar rightwards to view the employee's current ModelArk Plan edition and token limit.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can filter statistics to view token usage within a specified time period and allocate ModelArk Plans accordingly.   </div>
