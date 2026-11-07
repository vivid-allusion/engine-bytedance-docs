---
title: "Set Approval Flow"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/Set_Approval_Flow"
---

The approval flow supports three setup methods: default approval flow, custom approval flow, and inherited approval flow. This feature allows you to configure the approval flow used when others apply for resource permissions as needed.

<span id="_2-1-设置默认审批流"></span>
## Constraints

Only the authority owners of DB, table, row, and column resources can view the corresponding resources and set their approval flows.

<span id="5f4446cc"></span>
## Set Default Approval Flow

The default approval process varies by confidentiality level. The higher the confidentiality level (L4 is the highest), the stricter the approval process. The default approval flows for different confidentiality levels are as follows:


* L1: approval unrequired, application is directly approved after submission

* L2: authority owner

* L3: authority owner \> table OWNER/database administrator

* L4: authority owner \> table OWNER/database administrator


<span id="_2-2-设置自定义审批流"></span>
## Set Custom Approval Flow

If some resources are important and require approval by other individuals or roles, you can add approval nodes before or after the default node. After setting is complete, new permission applications will follow the configured approval flow and require approval at all nodes before granting permission. custom approval flow supports the following custom roles:


* role: system default roles.

   * database: database administrator

   * Table: DB admin, Database authority owner, Table Owner

   * Row/Column: DB admin, Database authority owner, Table Owner, Table authority owner

* Custom Role: roles created independently. For related instructions on creating Custom Roles, refer to [Set Automatic Approval Rules](https://docs.byteplus.com/docs/dataleap/Set_Automatic_Approval_Rules).


Custom nodes support setting trigger conditions. If trigger conditions are set, approval flows only add this node for resources meeting the conditions; if none are set, this node is added to all requests for that resource.

The process of setting approval flows for various resources is basically the same. Taking tables as an example, the steps to set the approval flow are as follows:


1. Log in to the DataLeap console.

2. Select **Overview \> Data Security \> Permission management \> Permission Settings \> Table** to enter the **Table** page.

3. Execute the following actions:

   * Set the approval flow for a single data table

      1. Click the **Set Approval Flow** button in the **Action** column of an entry to access the **Approval Flow** page for that data table.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e1687cf9878d4de5b71765b0410b0505~tplv-goo7wpa0wc-image.image) </span>

      2. You can perform the following actions. After customizing the approval flow as needed, click the **Save** button to complete the setup.

         * Click the **Add Node** icon ⊕ to the right of the default node, then select an approval role or individual in the new approval node.

         * Click the settings icon button to the right of a custom node to set trigger conditions.

            Only one trigger condition can be set for each custom node. Currently supported trigger conditions include:

            * Application type \- belongs to/does not belong to \- individual/user group; selectable from dropdown, supports multiple selection.

            * Authority owner \- belongs to/does not belong to \- related personnel; enter account keywords to search and select; supports multiple settings.

            * Table Owner \- Belongs to/Does not belong to \- Related personnel. Enter account keywords to search and select, supports multiple selections.

         * In the approval node drop\-down list, select a new role or individual to modify the approval information for that node.

         * Hover over an approval node, then click the **Delete Node** icon on the right to remove that approval node.

   * Batch set approval flow

      1. Select one or more data table options with the same classification, choose **More Batch Action** from the drop\-down list, then select **Set Approval Flow**. The **Batch Set Approval Flow** window will appear.

      2. You can add new approval nodes, modify or delete them. Click the **Confirm** button to display a dialog confirming the overwrite of the original approval flow settings. Click the **Confirm** button to complete the setup.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">In the default approval nodes, except the "Authority Owner" node which cannot be removed, other default approval nodes (such as table OWNER, DB admin) can be removed.</div>


* <div data-tips="true" data-tips-type="tip">The same approval role cannot be assigned to multiple different approval nodes.</div>


* <div data-tips="true" data-tips-type="tip">After modifying the approval flow, the changes apply immediately to new application tickets and those currently under review.</div>



<span id="_2-3-设置审批流继承"></span>
## Set Approval Flow Inheritance

If the resources you manage have lower\-level resources, you can enable the approval flow inheritance function to manage the approval flows of lower\-level resources uniformly. The database supports inheritance for tables, rows, and columns; tables support row and column inheritance; database approval flow inheritance has higher priority than table approval flow inheritance.

The process for setting approval flow inheritance on database and table resources is basically the same. Using a data table as an example, the steps for setting approval flow inheritance are as follows:


1. Log in to the DataLeap console.

2. Select **Overview \> Data Security \> Permission Management \> Permission Settings \> Table** to enter the **Table** page.

3. The following actions can be performed:

   * Set approval flow inheritance for a single table

      1. Click the **Set approval flow** button in the **Action** column of an entry to enter the **Approval flow settings** page for that table.

      2. Click the toggle button next to **On subordinate resources (including new) inherit approval flow** to display related inheritance settings.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dd89fc0199db460abf7142c3a1311148~tplv-goo7wpa0wc-image.image) </span>

      3. After setting the approval flows for subordinate data classifications, click the **Save** button, then click **Confirm** on the confirmation dialog to complete the approval flow inheritance setup.

         * When **Enable Sub\-level resource customizing approval flow** is set to **Yes**, approval flows must be configured separately for L2/L3/L4 classifications. Subordinate resources will follow the approval flow set here for the corresponding classification. Subordinates may add custom approval nodes based on the inherited flow but cannot delete inherited nodes.

         * When **Enable Sub\-level resource customizing approval flow** is set to **No**, approval flows must be configured separately for L2/L3/L4 classifications. Its subordinate resources will follow the approval flow set for the corresponding classification here and cannot be modified independently.

   * Batch set approval flow inheritance

      1. Select one or more data tables with the same classification, then choose **Set Approval Flow** from the **More Batch Action** dropdown menu to open the **Batch Set Approval Flow** window.

      2. After setting the inherited approval flow information, click the **OK** button. A dialog will appear to confirm overwriting the existing approval flow settings. Click the **OK** button to complete the setup.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">After modifying the approval flow, it only applies to newly created application work orders; work orders under review still use the original approval flow.</div>


* <div data-tips="true" data-tips-type="tip">If approval flow inheritance is disabled, subordinate resources will follow their own settings for execution. To make changes, go to the corresponding resource’s <strong>set approval flow</strong>.</div>


   * <div data-tips="true" data-tips-type="tip">When the database does not enable approval flow inheritance, its custom approval flow has no effect on the approval flows of subordinate tables, rows, or columns.</div>


   * <div data-tips="true" data-tips-type="tip">When the table does not enable approval flow inheritance, its custom approval flow does not affect the approval flows of existing row or column resources, but incremental rows and columns inherit the table’s custom approval flow.</div>


* <div data-tips="true" data-tips-type="tip">If inheritance is enabled and then disabled, subordinate approval flows will revert to their state before enabling inheritance, without resetting to empty or being overwritten.</div>


* <div data-tips="true" data-tips-type="tip">When setting resource approval flows, regardless of classification level, it is recommended to first set stricter approval flows for higher\-level resources, then set more lenient flows for subordinate resources. If needed, turn on subordinate inheritance of the higher\-level approval flow. Once enabled, subordinate approvals will be as strict as those of the higher level.</div>



<span id="d46fef03"></span>
## Operation Result

After setting the resource approval flow, when a user applies for resource permission, the approval ticket will follow the configured process. For instructions on operating approval tickets, refer to [Approve Applications](https://docs.byteplus.com/docs/dataleap/Approval_Applications).
