---
title: "Asset Circling"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/Asset_Circling"
---

The asset circling feature allows you to create asset circling strategies for the current business line as needed. The system automatically assigns assets that meet the circling conditions to the current business line.

<span id="b16444ff"></span>
## Constraints

Only business line administrators can perform asset circling.

<span id="f87ba347"></span>
## Prerequisites

A business line has been created.

<span id="5e2b44d3"></span>
## Operation Steps


1. Log in to the DataLeap Console.

2. Select **Overview \> Catalog \> Asset Management \> Shelf Management \> Asset Circling** to enter the **Asset Circling** page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/37c65c540a744df09a7d732b3f1450f9~tplv-goo7wpa0wc-image.image) </span>

3. Select the business line to manage from the business line dropdown in the upper right corner of the page.

4. You can perform the following actions:

   * Create a new circle selection

      Click the **New circle selection** button to go to the new circle selection page. After setting the relevant information, click the **OK** button to complete the creation.

      
      |Parameters |Description |
      |---|---|
      |**Basic Information** ||
      |\*Circle name |Name of the asset circle, set by the user.<br><br>The circle name cannot be duplicated within the same business line. |
      |\*Execution type |The execution type of the circle supports two options: **Timing** and **Manual**, selectable from the dropdown.<br><br><br>* Manual: The user manually clicks to execute.<br><br>* Timing: The system schedules execution at 0 o'clock every day. |
      |Creator |The creator of the circle, defaulting to the current user and cannot be changed. |
      |Description |Circled description information. |
      |**Circle selection condition** ||
      |\*Data type |Circled data type, supported options include ByteHouse CDW table, ByteHouse CE table, LAS Catalog table, LAS Schema DB, etc.; selectable from the dropdown. |
      |Whether to enable database & table circling |Choose whether to enable database & table circling.<br><br>When enabled, circling uses database and table names plus the filter conditions added below.<br><br><br>* DB Name: The database corresponding to the data type, selectable from created databases in the dropdown.<br><br>* Table Name: Data tables under the selected database, selectable from created tables in the dropdown. |
      |Filter |The filter criteria for asset circling support multiple directions such as owner, status, and core or not, varying by data type.<br><br>You can set multiple filter criteria using the **Add condition** button; the relationship between each condition is **and**. |
      

   * Edit circle selection

      Click the **Edit** button in the **Action** column of an entry to modify its configuration information.

   * Turn circle selection off/on

      Click the **Close/Enable** button in the **Action** column of an entry with on/off status to turn the circle selection off or on.

   * Run circle selection

      Click the  **...**   **\> Run** button \*\*\*\* in the **Action** column of an enabled entry to execute the selection once. After running, the system assigns matching assets to the current business line based on the configured conditions in the selection.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">This operation is supported only for asset circling with <strong>execution type</strong> set to <strong>manual</strong>.      </div>
      

   * Delete selection

      Click the  **...**   **\> Delete** button in the **Action** column of a closed status entry to remove the selection after secondary confirmation.


<span id="85a01d28"></span>
## Subsequent Operations

After selecting assets, perform [Asset Maintenance](https://docs.byteplus.com/docs/dataleap/Asset_Maintenance) as needed.
