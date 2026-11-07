---
title: "Manage data insight policies"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/Manage_data_insight_policies"
---

A data insight policy defines specific metric rules, allowing you to quickly filter data that meets those criteria in the file system. This article explains how to create data insight policies and related actions.

<span id="e05deaf7"></span>
## Create data insight policy


1. Log in to the [PFS console](https://console.byteplus.com/pfs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation panel, select **Data Insight** \> **Policy Management**.

4. On the **Policy Management**, click **Create Policy.** 

5. On the **Create Data Insight Policy** page, set the following parameters.

   * **Basic information**

      
      |**Parameter** |Required |**Note** |
      |---|---|---|
      |Policy name |Yes |Set the name for the data insights policy. Naming guidelines are as follows:<br><br><br>* Start with a letter or Chinese character.<br><br>* The permission group name can only contain Chinese characters, letters, numbers, periods (.), underscores (_), or hyphens (\-).<br><br>* The length must be between 1 and 128 characters. |
      |Description |No |Description of the policy settings; with the following constraints:<br><br><br>* Must start with a letter, Chinese character, or number.<br><br>* Only Chinese characters, letters, numbers, spaces, half\-width periods (.), full\-width periods (。), underscores (_), hyphens (\-), equal signs (=), half\-width commas (,), full\-width commas (，), or enumeration commas (、) are allowed.<br><br>* Length must be between 0 and 120 characters. |
      

   * **Policy configuration**

      
      |**Parameter** |Required |**Note** |
      |---|---|---|
      |Combination of rules |Yes |Select the logical relationship between rule groups. The system will process the filter results of each metric according to their combined relationships. The options are as follows:<br><br><br>* **Or**: Keep files that meet any rule group.<br><br>* **And**: Keep files that meet all rule groups.<br><br>* **Non**: Refers to **AND NOT**, keep files that do not meet all rule groups. |
      |Metric rules |Yes |You can set specific metric rule groups in the **Visualization** **editor** or in the **JSON** **editor** tab. For details on metric rule definitions and configuration, see [Indicator description](https://docs.byteplus.com/en/docs/pfs/Manage_data_insight_policies?lang=en#LwSpj7L6).<br><br><br>* **Visualization** **editor**/**JSON** **editor** management<br><br>   * **Bidirectional synchronization**: After configuring metric rules in the Visualization editor tab, you can switch to the JSON editor as needed. The system will generate corresponding metric rules based on syntax rules and automatically sync the selected content from the Visualization editor to the JSON editor. Conversely, metric rule content written in the JSON editor is also automatically synced to the Visualization editor.<br><br>   * **Switch criteria**:<br><br>      * When switching from the Visualization editor to the JSON editor for the first time, you must configure at least one valid metric rule.<br><br>      * The JSON editor supports pasting, format validation, and invalid parameter checks. When switching back from the JSON editor to the visual editor, ensure the JSON code is correctly formatted and all parameters are valid. If the system validation fails, you cannot switch and an error message will appear.<br><br>* **Rule group** management<br><br>   * **Add metric rule**: Click **Add row** to add multiple metric rules for this rule group. Metric rules within the same group cannot be duplicated.<br><br>   * **Add rule group**: Click **Add rule group** to add multiple rule groups. A single data insight policy can have up to 10 rule groups.<br><br>   * **Edit logic relation**: Click the logic operator (such as **And** or **Or**) in front of the metric rule to switch its logic relation for defining the combination method among metric rules within the same group.<br><br>   * **Delete rule group**: Click **Delete** in the upper right corner of the rule group to delete the group and all included metric rules.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">At least one rule group is required for each data insight policy.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Each rule group must include at least one metric rule.   </div><br>   <br><br>* **Metric rule** management<br><br>   * **Add filter condition**: Click the plus sign next to the metric rule to add a filter condition to this rule.<br><br>   * **Remove filter condition**: Click the minus sign next to the metric rule to remove this filter condition.<br><br>   * **Delete metric rule**: Click the delete icon next to the metric rule to delete this metric rule.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Each metric rule must include at least one filter condition.   </div><br>    |
      

6. Click **Confirm** to save the policy.


<span id="LwSpj7L6"></span>
### Indicator description

Data Insight policies offer the following indicators for you to select.


|**Metric content** |Description |Note |
|---|---|---|
|CreationTime |Filter files created within the specified time range, accurate to the day. |* Indicator rules description:<br><br>   * You can add up to 10 filter criteria for each indicator rule.<br><br>   * The logical relationship between conditions within the same indicator rule is **Or**.<br><br>* Optional criteria are as follows:<br><br>   * **Relative time**:<br><br>      * **More than**: Enter an integer between 1 and 365.<br><br>      * **Less than**: Enter an integer between 1 and 365.<br><br>      * **Between**: Enter two integers between 1 and 365.<br><br>   * **Absolute time**:<br><br>      * **Earlier than**: Select a date in the date picker.<br><br>      * **Later than**: Select a date in the date picker.<br><br>      * **Between**: select a date range in the date picker. |
|AccessTime |Filter files based on their last access time within the specified date range, accurate to the day. ||
|ModifyTime |Filter files whose last update time falls within a specified range, accurate to the day. ||
|ChangeTime |Filter files whose metadata was last modified within the specified time range, accurate to the day. ||
|Size |Filter files by size within a specified range. |* Metric rule description:<br><br>   * A maximum of 10 filter conditions can be added to each metric rule.<br><br>   * Within the same metric rule, conditions are logically connected using **Or**.<br><br>* Optional conditions: **Less than**, **Less than or equal to**, **Equal to**, **Greater than**, **Greater than or equal to**, **interval**<br><br>* Optional file units: **Byte**, **KiB**, **MiB**, **GiB**, **TiB**, **PiB**<br><br>* Constraint: File size cannot exceed 1 PiB |
|Type |Filter files by specific types. |* Indicator rule description:<br><br>   1. All **not equals** conditions are connected with **And**.<br><br>   2. Combine the results of the above "not equals" conditions with all **equals** conditions using **Or**.<br><br>* Optional conditions are as follows:<br><br>   * **Equal to**<br><br>   * **Not equal to**<br><br>* Optional file types: **ordinary** **file**, **Directory**, **Symbolic link**, **Character special file**, **Block special file**, **Socket**, **Pipeline** |
|Extension |Filter files by specified file extension. |* Metric rule description:<br><br>   1. All **not equal to** conditions are connected with an **And** relationship.<br><br>   2. The combined result of the above "not equal to" conditions will be evaluated with all **equal to** conditions using **Or**.<br><br>* The optional conditions are as follows:<br><br>   * **Equal to**<br><br>   * **Not equal to**<br><br>* You can select file extensions: **txt**, **jpg**, **png**.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can manually enter other extensions, such as <code>pdf</code> and <code>zip</code>.   </div><br>    |
|Name |Filter files whose names are within the specified range. |Optional conditions are as follows:<br><br><br>* **Equal to**<br><br>* **Contain**<br><br>* **Prefix equals** |
|Path |Filter files whose paths are within the specified range. |* Metric rules description:<br><br>   1. All **prefix not equal** conditions are combined with an **And** relationship.<br><br>   2. The result above does not equal the combination. Then perform an **Or** operation with all **prefix equals** conditions.<br><br>* Optional conditions are as follows:<br><br>   * **Prefix equals**<br><br>   * **Prefix is not equal to**<br><br>* File path requirements are as follows:<br><br>   * Enter the absolute path in the file system. The path must start and end with a forward slash (/).<br><br>   * Can contain letters, numbers, periods (.), underscores (_), hyphens (\-), and forward slashes (/).<br><br>   * Length of the complete path string must not exceed 1,024 characters, and each subpath segment must be limited to 255 characters or fewer. |


&nbsp;

<span id="NyDg6Vjr"></span>
## Related operations


|**Operation** |**Note** |**Steps** |
|---|---|---|
|Edit policy name |You can change the name of a created policy. Follow these naming rules:<br><br><br>* The name must start with a letter or Chinese character.<br><br>* The permission group name can only contain Chinese characters, letters, numbers, periods (.), underscores (_), or hyphens (\-).<br><br>* The length must be between 1 and 128 characters. |1. In the **Data Insight** \> **Policy Management** page list, click the Edit icon next to the target policy name.<br><br>2. Enter a new policy name in the dialog box.<br><br>3. Click **Save**. |
|View related tasks |You can view task information associated with the policy. |1. On the **Data Insight** \> **Policy Management** page, click **View Task** in the **Actions** column for the target policy.<br><br>2. Go to the **Task Management** page to view task details associated with the target policy. |
|Edit policy information |You can modify the basic information and configuration of the policy.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default" data-wrapper-indent="0">If the task associated with the target policy is <strong>In progress</strong>, you cannot modify the policy’s metric rules.</div><br> |1. On the **Data Insight** \> **policy Management** page, click **Edit** in the **Actions** column of the target policy, or click the target **policy name** to go to the **Edit Data Insight policy** page.<br><br>2. Edit the basic information and configuration of the policy. For detailed parameter descriptions, see [Create data insight policy](https://docs.byteplus.com/en/docs/pfs/Manage_data_insight_policies?lang=en#e05deaf7).<br><br>3. Click **Confirm**. |
|Delete policy |You can delete policies that are no longer used.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default" data-wrapper-indent="0">Delete the tasks associated with the policy before removing it. For specific actions, see <a href="https://docs.byteplus.com/en/docs/pfs/Manage_Data_Insight_tasks#5a259564">Related actions</a>.</div><br> |1. On the **Data Insight** \> **policy Management** page, click **Delete** in the **Actions** column of the target policy.<br><br>2. In the **Delete policy** dialog, click **Delete**. |
