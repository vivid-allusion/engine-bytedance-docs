---
title: "Managing trigger logs"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-trigger-event-logs"
---

When a user performs a monitored action as defined by the dynamic control rule, SealSuite will generate a trigger log and display it through the **Trigger Logs** function. On the **Trigger Logs** page, you can view detailed information about the trigger detection, such as the trigger time, matching rule group, trigger event, the device's owner, the device, the restoration status and the remediation status, among others.

<span id="ab29c13b"></span>
# Enabling the trigger log

You can enable the trigger log function to record the trigger events that occur within one hour. When the given time period expires, the triggering log function will be automatically disabled.


1. Log in to the Admin Console.

2. In the left navigation bar, click **Dynamic Control** \> **Security Alerts** \> **Trigger Logs**.

3. At the top of the **Trigger Logs** page, click **Disabled Log Feature** icon to turn on the feature.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6e8d3f4f0cba46819f1923cadc84c37a~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To help you effectively manage generated trigger logs, the enabled trigger log function only records trigger events that occur within one hour and restores the log data for 30 days. If you need to record trigger events after the given time period expires, toggle the Trigger Log button again.   </div>
   

<span id="5cda9ad3"></span>
# Viewing trigger logs

On the **Trigger Logs** page, you can view recent trigger logs that are generated within 30 days, and filter the trigger logs by employee, device information, rule group name, status, trigger event, and time.


1. Log in to the Admin Console.

2. In the left navigation bar, click **Dynamic Control** \> **Security Alerts** \> **Trigger Logs**.

3. In the \*\*\*\* event list, you can view generated trigger logs within 30 days.

4. (Optional) At the top of the list, use the following filter criteria to locate specific trigger logs.

   
   |**Filter Criteria** |**Description** |
   |---|---|
   |Employee/Device Info |You can select **Employee** or **Device info** from the drop\-down list on the left of this option and enter an employee or device name accordingly. |
   |Rule Name |Enter an existing rule group name. You can refer to the rule group list under the **Dynamic Policies** module to obtain the corresponding rule group name. |
   |Status |Select a remediation status. Available options are listed as follows:<br><br><br>* **All**: Contains both **Miss** and **Handled** statuses\*\*.\*\*<br><br>* **Miss**: Indicates that the trigger event does not satisfy any rule group.<br><br>* **Handled**: Indicates that the trigger events that satisfy existing rule groups have been remediated. |
   |Trigger Event |Select the triggering method for a rule group. |
   |Time |Specify the trigger time by seconds. |
   

5. In the **Action** column of the **Trigger Log** page, click **Details**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e0c784cec4a744e2aa93d1a343d8775b~tplv-goo7wpa0wc-image.image) </span>

6. On the details page, you can view the following trigger details.

   * Basic information: Contains information such as the device name, the DID number of the device, the user’s name and the department of the user.

   * **General**: Contains information such as the matching rule group, triggering event and trigger time.

   * **Trigger Type**: Displays details of the triggering condition as defined by the matching rule group, including the ID number of the rule group and the trigger parameters. Displays parameters which includes Disposal time parameters, Current Parameter and Parameters in rules.

   * **Remediation**: The current remediation status. If the detected event does not satisfy any rule group, no remediation status is displayed in this option.

7. (Optional) Click to **View Device Security** or **View data sources** to view device information and data sources:

   * **View Device Security**: View the security status of the device.

   * **View data sources**: View the trigger data in JSON format.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/390498b90ab84161b73882affba26d0d~tplv-goo7wpa0wc-image.image) </span>
