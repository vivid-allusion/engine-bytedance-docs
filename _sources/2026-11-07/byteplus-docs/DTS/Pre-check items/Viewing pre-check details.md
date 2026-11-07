---
title: "Viewing pre-check details"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/viewing_consumption_checkpoint_details"
---

This topic explains how to view detailed pre\-check items for transmission tasks and data verification tasks in the Database Transmission Service (DTS) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Tasks to be started have been created or saved. For more information, refer to [Creating a migration task](https://docs.byteplus.com/en/docs/DTS/overview_of_migration_solutions), [Creating a subscription task](https://docs.byteplus.com/en/docs/DTS/overview_of_subscription_solutions), [Creating a synchronization task](https://docs.byteplus.com/en/docs/DTS/overview_of_synchronization_solutions), or [Creating a data verification task](https://docs.byteplus.com/en/docs/DTS/configuring_data_validation).

<span id=".5p-l55yL5Lyg6L6T5Lu75Yqh6aKE5qOA5p-l6K-m5oOF"></span>
## View transmission task pre\-check details


1. Log on to the [DTS console](https://console.byteplus.com/dts).

2. On the top menu bar, select the project and region.

3. In the left navigation bar, select the target task type, including **Data migration**, **Data subscription, Data synchronization, or Data verification**.

4. On the **Migration task list**, **Subscription task list, Synchronization task list**, or **Verification task list** page, click the target task name.

5. On the Task details page, click the **Health status** tab.

6. In the **Diagnostic report** pane, click the earliest diagnostic report by time to view the pre\-check details. The details are as follows.

   * Basic information of the pre\-check: In the **Basic information** pane, view the pre\-check state, progress, creation time, and update time.

   * AI analysis: When the health level is not **Healthy**, click **AI analysis**, then click **OK** in the pop\-up confirmation window. DTS will analyze the current diagnosis results. Later, you can view the AI analysis results and optimization suggestions in the AI analysis results column of the check result list.

   * Pre\-check results: In the **Health check results** pane, view the total number of completed check items during task creation, including prompt items, failed items, and pass items. At the same time, you can also view specific check items, check item descriptions, check results, and results details.

   * Export pre\-check report: In the top\-right corner of the **Basic information** area, click **Export report** to save the diagnostic report locally.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">When a pre\-check item’s check result is <strong>Failed</strong> or <strong>Prompt</strong>, you can view detailed information in the <strong>Results details</strong> column and make corresponding adjustments.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">All historical diagnostic records are saved in the diagnostic report pane. The earliest diagnostic report record is the pre\-check report record created during the task creation.      </div>
      


<span id=".5p-l55yL5qCh6aqM5Lu75Yqh6aKE5qOA5p-l6K-m5oOF"></span>
##
