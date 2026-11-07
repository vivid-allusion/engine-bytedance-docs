---
title: "Rule Maintenance"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/Rule_Maintenance"
---

The rule maintenance function automates asset listing and marks assets as off\-shelf, significantly improving data asset maintenance efficiency.

<span id="2ea16087"></span>
## Constraints

Only business line administrators can create and edit rules; others can only view them.

<span id="5e16e151"></span>
## Prerequisites

The business line has been created.

<span id="8c598100"></span>
## Operation Steps


1. Log in to the DataLeap console.

2. Select **Overview \> Catalog \> Asset Management \> Shelf Management \> Rule Maintenance** to enter the **Rule Maintenance** page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1561ab66373b47389a5c117b32cf71f6~tplv-goo7wpa0wc-image.image) </span>

3. Select the business line to manage from the business line dropdown menu at the top right of the page.

4. You can perform the following actions:

   * Create automated rules

      Click the **New Rule** button, fill in the required information in the pop\-up side window, then click **OK** to complete creation.

      
      |Parameters |Description |
      |---|---|
      |**Basic Information** ||
      |\*Rule name |The name of the automated rule, set by the user with a maximum of 20 characters. |
      |\*Rule description |Description of the rule, limited to 100 characters. |
      |\*Rule type |The type of rule, supports **non\-listing rule** and **auto\-listing rule** options, selectable from a dropdown.<br><br><br>* Non\-listing rule: applies matching rules to off\-shelf assets to execute the off\-shelf operation.<br><br>* auto\-listing rule: for automatically listing or unmaintained classification assets (excluding off\-shelf assets), perform rule matching daily to relist assets. |
      |**Select asset range** ||
      |\*Portal Business Line |The asset's business line, auto\-filled with the selected business line and not editable. |
      |\*Asset Type |Select the asset type for the rule to apply, dropdown options available. |
      |\*Regular Form |Only supports **conditional filtering**. |
      |\*Filter |Rule filter conditions support two addition modes: **Add condition** and **Combination filter**. Added conditions default to an **or** relationship, which can be switched to **and** by clicking.<br><br><br>1. Click the corresponding button to add filter conditions.<br><br>   * Add condition: adds a row of condition configuration.<br><br>   * Combine filter conditions: adds a group of filter conditions.<br><br>2. Select the asset type property from the dropdown and set the corresponding filter information.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can only select asset type attributes after choosing <strong>asset type</strong>.</div><br> |
      |**Rule enforcement** ||
      |\*Rule priority |The priority level for rule enforcement ranges from P0 to P5 from highest to lowest, selectable from the dropdown. |
      |\*Attributed asset catalog |Asset catalogs to which the rule belongs. Select existing asset catalogs from the dropdown. Multiple selections allowed.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only when <strong>rule type</strong> is <strong>auto\-listing rule</strong>, this parameter needs to be set.</div><br> |
      |\*Release associated assets |Automatically identify downstream related data through lineage relationships.<br><br>Optionally enable this selection. Enabling supports selection of **underlying asset type**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only when <strong>rule type</strong> is <strong>auto\-listing rule</strong>, this parameter needs to be set.</div><br> |
      |\*Underlying asset type |Type of related assets. Selectable from dropdown. Multiple selections allowed.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter needs to be set when <strong>release associated assets</strong> is enabled.</div><br> |
      |\*Effective Status |Select whether to set this rule as active. |
      

   * Search rules

      Set search criteria to view the list of rules that match the conditions.

   * Edit rules

      Click the **Edit** button in the **Action** column for a specific entry to modify that rule’s information.

   * Copy rules

      Click the **Copy** button in the **Action** column for a specific entry to duplicate that rule and quickly create a new one.

   * Delete rule

      Click the **Delete** button in the **Action** column for an entry, then confirm to delete the rule.

   * Enable/disable rule

      Click the **On/off** icon button in the **Validity state** column for an entry, then confirm to enable or disable the rule.

   * Schedule execution rule

      Click the **Scheduling Configuration** button, set the scheduling time in the pop\-up window, then click the **OK** button to complete the schedule configuration. The rule will execute at this time every day.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If no scheduling configuration is set, the system defaults to executing the scheduling rule every day at 16:00.      </div>
      

   * Manual execution rule

      Click the **Manual Execution** button, choose the asset type in the pop\-up window, then click the **OK** button to immediately execute the corresponding automated maintenance rule.


<span id="88ca1bd1"></span>
## Operation Result

After rule configuration, the system executes the scheduled rules based on the schedule settings to automate asset maintenance.
