---
title: "Manage Other Datasource Rule Run Results"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/Manage_Other_Datasource_Rule_Run_Results"
---

This feature manages the run results of other datasource rules. The following introduces its use.

<span id="_1-前提条件"></span>
## Prerequisites

Monitor rules have been run.

<span id="_2-操作步骤"></span>
## Operation Steps


1. Log in to the DataLeap console.

2. Choose **Overview \> Quality \> Rules \> Batch Rule \> run result** to enter the run result page.

3. Click the **Other data sources** tab to enter the other datasource run result page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f858a264348f4c1cb4003a8186838e6e~tplv-goo7wpa0wc-image.image) </span>

4. Choose the project to manage from the project dropdown list at the top right corner of the page.

5. View all rule detection records and perform the following management actions:

   * Set search criteria to find rule monitoring results that match the conditions.

   * Click the **Log** button in the **Action** column of a monitoring information entry to view the rule’s run log and analyze issues.

   * Click the  **...**   **\> Rerun** button in the **Action** column of a monitoring information entry to rerun the monitoring rule after confirmation.

   * Click the  **...**   **\> Stop** button in the **Action** column of a running rule to stop the current monitoring rule run.

   * Click the  **...**   **\> Rules details** button in the **Action** column of a rule to view the rule details and perform test runs, reruns, and other actions.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When a development task is manually debugged or scheduled to run triggering rule execution, the <strong>execution method</strong> always shows <strong>task trigger</strong>.</div>


* <div data-tips="true" data-tips-type="tip">When the engine type is <strong>non\-ByteHouse Cloud Data Warehouse Edition</strong>, the <strong>execution environment</strong> shows “<strong>\-</strong>”.</div>


* <div data-tips="true" data-tips-type="tip">When the engine type is <strong>ByteHouse Cloud Data Warehouse Edition</strong>, the rule run result display differs because this engine supports multiple environment datasource instances, such as development and production environments, as follows:</div>


   * <div data-tips="true" data-tips-type="tip">If the related task is a <strong>non\-ByteHouse Cloud Data Warehouse Edition</strong> task, the run results still show the datasource name and production environment flag configured by the rule.</div>


   * <div data-tips="true" data-tips-type="tip">If the related task is a <strong>ByteHouse Cloud Data Warehouse Edition</strong> task, the run results show the actual datasource name and environment flag of the run.</div>
