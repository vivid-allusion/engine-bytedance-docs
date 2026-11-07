---
title: "Offline Downgrade Management"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/offline_downgrade_management"
---

To cope with sudden spikes in traffic (e.g., during major holidays like the Spring Festival) or unexpected computational resource anomalies, businesses may adopt tiered operational strategies based on task importance. This ensures that core tasks are prioritized, and non\-core tasks are downgraded, thereby freeing up computational resources. The offline downgrade management feature can downgrade lower\-priority tasks through scheduling limits and also supports setting ACK in batches for related alarms. This article will introduce how to configure offline downgrade management rules.

<span id="e7c688be"></span>
## Glossary


* Scheduling Limit: During a specified period, restrict the scheduling submission of specified tasks.

* Alarm Shielding: For tasks that are prohibited from being scheduled in certain periods, if there are related alarms set up, to avoid ineffective alarms during these periods, they can be mass\-shielded through alarm shielding.


<span id="_1-约束限制"></span>
## Constraints

Only project administrators can configure offline downgrade rules.

<span id="_2-前提条件"></span>
## P**rerequisite**

A project has been created.

<span id="_3-操作步骤"></span>
## Manage Scheduling Limit Rules


1. Log in to the DataLeap Console.

2. Click on **Projects** on the left navigation bar to enter the **Project Management** page.

3. Check the **My managed projects** option to display the list of projects you manage.

4. Click any **Action** button in the column of the project list to enter the **Project Console**.

5. Click on **Offline Downgrade** in the left navigation bar to directly enter the **Scheduling Limit** page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5e2da55e8ad545cbb6bbad824bbaa34d~tplv-goo7wpa0wc-image.image) </span>

6. The following operations can be performed:

   * Create New Rule

      Click the **New Rule** button. In the pop\-up **New Rule** window, set the scheduling limit after which click the **OK** button to complete creation.

      The parameters related to setting scheduling limits are shown in the table below. Parameters indicated with \* are required, while others without \* are optional.

      
      |Parameters |Description |
      |---|---|
      |\*Rule name |Name of the scheduling limit rule, set by yourself. |
      |\*Description |Description of the rule for subsequent management. |
      |Apply Task |Tasks with scheduling limits can be configured in the following ways:<br><br><br>* Priority: The priority of the task ranges from high to low, D1 to D5, selectable from a dropdown.<br><br>* Task type: The type of task, supporting options like Batch Integration, EMR Doris, and more, selectable from a dropdown, with multiple settings available.<br><br>* Owner: The owner of the task, select by entering account keywords from a dropdown, with multiple settings available.<br><br>* Exclusion settings: Tasks that match the exclusion rules. After searching by task name keyword or ID, choose from a dropdown.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">At least one of the priority, task type, or owner must be set.</div><br> |
      |\*Prohibited Scheduling Period |Times when scheduling is prohibited for the application task. |
      

   * Edit Rules

      Click the **Edit** button in the **Action** column of an item in the list. In the pop\-up window, you can modify the rule information.

   * On/Off Rules

      Click the **On/Off** toggle button in the **Action** column of an item in the list. After confirmation, you can enable or disable the rule. Once disabled, the rule will no longer be effective.

   * Delete rule

      Click the **Delete** button in the **Action** column of an item in the list, and after confirming twice, delete the rule.


<span id="a41f231e"></span>
## Manage Alarm Shielding Rules


1. Log in to the DataLeap console.

2. Click **Projects** in the left sidebar to enter the **Project Management** page.

3. Select the **My managed projects** option to display the list of projects you manage.

4. Click any one button in the **Action** column of the project list you want to manage to enter the **Project Console**.

5. Select **Offline Downgrade \> Alarm Shielding** to enter the **Alarm Shielding** page.

6. Perform the following operations:

   * Create New Rule

      Click the **New Rule** button, and in the pop\-up **New Rule** window, set the scheduling limit rule. Then, click the **OK** button to complete the creation.

      The parameters related to the creation of the alarm shielding rule are described in the table below.

      
      |Parameters |Description |
      |---|---|
      |\*Rule name |Name of the scheduling restriction rule, customizable. |
      |\*Description |Description of the rule for subsequent management. |
      |\*Apply Task |Tasks adopting the scheduling restriction rules can select settings from the following aspects:<br><br><br>* Priority: Task priority ranges from high to low as D1~D5, dropdown to choose.<br><br>* Task type: Task type, supports various options such as Batch Integration, EMR Doris, etc., which can be selected from a dropdown and multiple can be set.<br><br>* Owner: Task owner, input account keywords can be selected from a dropdown, and multiple can be set.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">At least one of the priority, task type, or owner must be set.</div><br> |
      |\*Shielded alarm type |Shielded Application Task alarm types, supported options include Execution Failed, Not executed successfully, Data output monitoring, etc., selectable from a dropdown, and multiple selections are allowed. |
      |\*Alarm shielding period |Time period for shielding Application Task alarms.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Since task execution takes time, the <strong>alarm shielding period</strong> is generally longer than the <strong>prohibited scheduling period</strong>.</div><br> |
      |ACK operation notification |Alarm shielding confirmation notification, provides options **Send to alarm recipient** and **Do not send**, default is Do not send. |
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If no tasks are filtered out based on the current filtering conditions, an attempt to create a project alarm shielding rule will indicate a failure.      </div>
      

   * Edit Rules

      Click the **Edit** button in the **Action** column for a piece of information in the list. In the pop\-up window, you can modify the rule information.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Once alarm shielding rules are set, they remain effective during the shielding period. To end the shielding earlier, modify the shielding period.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you need to shield baseline\-related alarms, go to <a href="https://docs.byteplus.com/docs/undefined/689b106ca5abd9051f272182">Baseline management</a> and close the baseline where the assurance task is located.   </div>
