---
title: "Exporting subscription task list"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Exporting_subscription_task_list"
---

Database Transmission Service (DTS) provides the export task list function, allowing you to filter target tasks based on business needs and export related task information (e.g., region and specification) for offline task resource management.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A data subscription task has been created. For more information, refer to [Subscription solution overview](https://docs.byteplus.com/en/docs/DTS/overview_of_subscription_solutions).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data subscription**.

4. On the **Data subscription list** page, click the download icon in the upper\-right corner.

5. In the **Export data** dialog box, select **Export range** and **Export list fields**.

   * **Export range**: Choose the export type as needed. The export type supports selecting **Export all data**, **Export selected data**, or **Export current search results**.

   * **Export list fields**: Select the list fields to export for the task as needed. Export list fields include **Task ID, Task name**, **Running status, Task type, Task specification, Source database type, Source database access method, Source region, Source database instance ID/address, Source database connection information, Target database type, Target database access method, Target database region, Target database instance ID/address, Target database connection information, Task progress, Billing method, Start time**, **End time**, **Project**, **Tag**, **Cross\-region?** , **Cross\-account?** .

6. Click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After exporting, the instance information is saved as a CSV file. You can download this file to your computer and open it with a text editor.   </div>
