---
title: "Performing migration source pre-checks"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/Perform-a-migration-precheck"
---

Server Migration Center (SMC) provides a migration pre\-check feature. Specifically, SMC will automatically perform a pre\-check on the migration source after you import the source. This helps eliminate configurations that do not meet migration requirements and improves the migration success rate.

<span id=".5p-l55yL6aKE5qOA5oql5ZGK"></span>
## View pre\-check report

For migration sources that have the migration pre\-check completed, you can view the corresponding results by following the guidance in this section.


1. Log in [to the Server Migration Center console](https://console.byteplus.com/ecs/source?projectName=default). 

2. In the left\-side navigation pane, select "Migration Source".

3. In the top menu bar, select the project associated with the target migration source.

4. You can view the pre\-check status of the target migration source in the "Precheck status" column. You can also hover over the pre\-check status (for example, **Passed**) of the target migration task to view check item statuses.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f45a322cf98209e3cd72b3c474a03961.png) </span>

   Pre\-check status descriptions:

   
   |Status |Description |
   |---|---|
   |**Being prechecked** |Migration pre\-check is in progress. |
   |**Passed** |All key check items required for migration have passed the pre\-check. |
   |**Precheck failed** |There are key check items required for migration that have not passed the pre\-check. |
   

5. You can click the "Report" button in the "Precheck status" column of the target migration source to view the details of the pre\-check report.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_da3fb3d5345f3731dbe42c29ae1e2bb6.png) </span>

   Check item status descriptions:

   
   |Status |Description |
   |---|---|
   |**Passed** |Pre\-check passed and no exception exists. |
   |**Warning** |Pre\-check failed. There exist exceptions that are likely to cause migration failure. |
   |**Severe** |Pre\-check failed. There exist exceptions that are highly likely to cause migration failure. |
   |**Unexecuted** |The check item does not require a pre\-check, or the prerequisite conditions for performing its pre\-check are not met. |
   

6. Based on the pre\-check result of the migration source, you can perform as follows:

   * **Passed**:

      Covered scenarios include:

      * All check items have passed the pre\-check. You can continue with [migration operations](https://docs.byteplus.com/en/docs/smc/Step-2-Create-and-launch-the-migration-task).

      * There are check items that may impact migration and have not passed the precheck. You can fix related exceptions as needed and then [perform migration pre-check](https://docs.byteplus.com/en/docs/smc/Perform-a-migration-precheck#.6L-b6KGM6L-B56e75rqQ6aKE5qOA) again, or continue with the [migration operation](https://docs.byteplus.com/en/docs/smc/Step-2-Create-and-launch-the-migration-task).

   * **Precheck failed**: You need to fix the exceptions of the key item required for migration before proceeding with the migration operations.

      1. Fix the exceptions based on the exception details. [Learn more](https://docs.byteplus.com/en/docs/smc/Test-item-description).

      2. After you fix the exceptions, [perform the migration pre-check](https://docs.byteplus.com/en/docs/smc/Perform-a-migration-precheck#.6L-b6KGM6L-B56e75rqQ6aKE5qOA) again.

      3. After the source passes the pre\-check, you can continue with [migration operations](https://docs.byteplus.com/en/docs/smc/Step-2-Create-and-launch-the-migration-task).


<span id=".6L-b6KGM6L-B56e75rqQ6aKE5qOA"></span>
## Perform migration source pre\-check

After fixing the exceptions detected in pre\-check items for the source server, you can perform the pre\-check again by following the guidance in this section to confirm whether the fix has succeeded.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The pre\-check operation is supported only for migration sources in the <strong>Online</strong> status.</div>


* <div data-tips="true" data-tips-type="tip">You can select up to 20 migration sources for pre\-check each time.</div>


1. Log in to the [Server Migration Center console](https://console.byteplus.com/ecs/source?projectName=default). 

2. In the left\-side navigation pane, select "Migration Source".

3. In the top menu bar, select the project associated with the target migration source.

4. Search for the target migration source by migration source name/ID.

5. Click the "Re\-precheck" button in the Actions column to the right of the target migration source to perform migration.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_209ed4ccc6f2ef099f95c8cf1d254ac2.png) </span>

6. After the check is complete, you can confirm whether the exceptions diagnosed in the items have been fixed by [referring to the pre-check report](https://docs.byteplus.com/en/docs/smc/Perform-a-migration-precheck#.5p-l55yL6aKE5qOA5oql5ZGK).
