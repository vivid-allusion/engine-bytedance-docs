---
title: "Viewing diagnosis results"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_diagnosis_results"
---

This topic describes the procedure to view the connection diagnostic results of an RDS for MySQL instance.

<span id="prerequisites"></span>
## Prerequisites

Diagnosis items have been added to the MySQL instance and the diagnosis has been executed. If diagnosis items have not been added or the diagnosis has not been executed yet, refer to [Adding diagnosis items](https://docs.byteplus.com/en/docs/RDS_for_MySQL/adding_diagnostic_items).

<span id="procedure"></span>
## Procedure


1. Log on to the [RDS for MySQL Console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region to which the instance belongs.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project to which the instance belongs has not been set, for this operation, you should select the project as <strong>All Resources</strong>.   </div>
   

3. Click **Instances** on the left navigation bar.

4. On the **Instances** page, click the name of the target instance to enter the **Summary** tab.

5. On the **Summary** page, click the **Connectivity** tab to enter the **Connectivity** page.

6. In the **Endpoints** area of the **Connectivity** page, click **Connection diagnosis** to enter the **Connection diagnosis** page.

7. On the **Connection diagnosis** page, after selecting the **Connection method**, click **View result** in the **Actions** column of the target diagnosis item list, and then you can view the corresponding diagnosis results in the pop\-up window.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the <strong>Result</strong> window, the diagnosis results of all diagnosis items under the corresponding connection method are displayed. For items with abnormal diagnosis results, corresponding handling suggestions can be obtained in the <strong>Suggestion</strong> column.   </div>
