---
title: "Performing migration task pre-checks"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/Perform_a_migration_job_precheck"
---

Server Migration Center (SMC) provides a migration pre\-check feature. After you create a migration task, SMC checks the network conditions between the source server and the migration target to reduce migration failures due to network issues and other factors.

<span id=".5p-l55yL6aKE5qOA5oql5ZGK"></span>
## View pre\-check report

For migration tasks that have the migration pre\-check completed, you can view the corresponding results by following the guidance in this section.


1. Log in to the [Server Migration Center console](https://console.byteplus.com/ecs/source?projectName=default).

2. In the left\-side navigation pane, select "Migration Job".

3. In the top menu bar, select the project where the target migration source is located.

4. Select the "Migrate to server" tab.

5. You can view the pre\-check status of the target migration task in the "Precheck status" column. You can also hover over the pre\-check status (for example, **Passed**) of the target migration task to view a summary of check item statuses.

   Pre\-check status descriptions:

   
   |Status |Description |
   |---|---|
   |**Being prechecked** |Migration pre\-check is in progress. |
   |**Passed** |All key check items required for migration have passed the pre\-check. |
   |**Precheck failed** |There are key check items required for migration that have not passed the pre\-check. |
   

6. You can click the "Report" button in the "Precheck status" column of the target migration source to view the details of the pre\-check report.

   Check item status descriptions:

   
   |Status |Description |
   |---|---|
   |**Passed** |Pre\-check passed and no exception exists. |
   |**Warning** |Pre\-check failed. There exist exceptions that are likely to cause migration failure. |
   |**Severe** |Pre\-check failed. There exist exceptions that are highly likely to cause migration failure. |
   |**Unexecuted** |The check item does not require a pre\-check, or the prerequisite conditions for performing its pre\-check are not met. |
   

7. Based on the pre\-check result of the migration source, you can perform as follows:

   * **Passed**:

      If you check the "The migration task automatically starts once the precheck succeeds" option when creating the migration task, SMC will automatically start the migration. Otherwise, you need to [start the migration task](https://docs.byteplus.com/en/docs/smc/Managing-Migration-Jobs#i3RVYNM7) manually.

   * **Precheck failed**: You need to fix the exceptions of the key item required for migration before proceeding with the migration operations.

      1. Fix the exceptions based on the exception details. [Learn more](https://docs.byteplus.com/en/docs/smc/Precheck_item_description).

      2. After you fix the exceptions, [perform the migration pre-check](https://docs.byteplus.com/en/docs/smc/Perform_a_migration_job_precheck#.6L-b6KGM6L-B56e75Lu75Yqh6aKE5qOA) again.

      3. Proceed with the migration operations by following the guidance of the mentioned **Passed** section.


<span id=".6L-b6KGM6L-B56e75Lu75Yqh6aKE5qOA"></span>
## Perform migration task pre\-check

After fixing the exceptions detected in the source server or migration target associated with the migration task, you can perform the pre\-check again by following the guidance in this section to confirm whether the fix has succeeded.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The pre\-check operation is supported only for migration tasks in the <strong>Passed</strong> or <strong>Precheck failed</strong> status.</div>


* <div data-tips="true" data-tips-type="tip">You can select up to 20 migration tasks for pre\-check each time.</div>


1. Log in to the [Server Migration Center](https://console.byteplus.com/ecs/source?projectName=default) console.

2. In the left\-side navigation pane, select "Migration Job".

3. In the top menu bar, select the project where the target migration source is located.

4. Select the "Migrate to server" tab.

5. Click the "... \> Re\-precheck" button in the Actions column to the right of the target migration source to perform the check again.

6. After the check is complete, you can confirm whether the exceptions diagnosed in the items have been fixed by [referring to the pre-check report](https://docs.byteplus.com/en/docs/smc/Perform_a_migration_job_precheck#.5p-l55yL6aKE5qOA5oql5ZGK).
