---
title: "Viewing backup jobs"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/View_backup_job"
---

A backup plan supports immediate backup or scheduled backup. Backup data is used for restoring jobs. This topic describes backup job management and related information.

<span id="nCmvXhNt"></span>
## Background

<span id="mRSVquXz"></span>
### Naming rules for backup jobs

Backup jobs are sorted by creation time, and their names are related to the backup plan. The detailed naming rules for backup jobs are as follows:


* If a backup plan uses **scheduled backup**, its job names follow the `<Backup plan name>-<timestamp>` format, for example, `plan1-1720515600`.

* If a backup plan uses **immediate backup**, its job name is the same as the backup plan name.


<span id="bzgFfzjE"></span>
### Backup job status

The status of backup jobs and their action restrictions are as follows:


|**Backup status** |**Description** |**Notes** |<div style="text-align: center"><br><strong>Supported actions</strong></div><br> |||
|---|---|---|---|---|---|
||||<div style="text-align: center"><br><strong>View details</strong></div><br> |<div style="text-align: center"><br><strong>Restore</strong></div><br> |<div style="text-align: center"><br><strong>Delete</strong></div><br> |
|Starting |The backup job is initializing and has not started backing up data yet. |Intermediate status |<div style="text-align: center"><br>✔️</div><br> |<div style="text-align: center"><br>❌</div><br> |<div style="text-align: center"><br>❌</div><br> |
|Backing up |The job has started execution and is backing up data. |Intermediate status |<div style="text-align: center"><br>✔️</div><br> |<div style="text-align: center"><br>❌</div><br> |<div style="text-align: center"><br>❌</div><br> |
|Success |All data has been backed up and no errors have occurred. |Stable status |<div style="text-align: center"><br>✔️</div><br> |<div style="text-align: center"><br>✔️</div><br> |<div style="text-align: center"><br>✔️</div><br> |
|Fail |Backup job validation failed. The job has not started execution yet. |Stable status |<div style="text-align: center"><br>✔️</div><br> |<div style="text-align: center"><br>❌</div><br> |<div style="text-align: center"><br>✔️</div><br> |
||A failure occurred during backup job execution. The backup job cannot proceed, and other resources will not be backed up. |Stable status |<div style="text-align: center"><br>✔️</div><br> |<div style="text-align: center"><br>❌</div><br> |<div style="text-align: center"><br>✔️</div><br> |
|Partially failed |Certain resources failed to be backed up. Other resources will be backed up normally. |Stable status |<div style="text-align: center"><br>✔️</div><br> |<div style="text-align: center"><br>✔️</div><br> |<div style="text-align: center"><br>✔️</div><br> |
|Deleting |The backup job is being deleted. |Intermediate status |<div style="text-align: center"><br>❌</div><br> |<div style="text-align: center"><br>❌</div><br> |<div style="text-align: center"><br>❌</div><br> |


<span id="hhTkcyn3"></span>
## Procedure

VKE provides a dedicated page for backup job management and also supports viewing backup jobs for a specified backup plan.

<span id="WxCecgdA"></span>
### Method 1: View all backup jobs

All backup jobs triggered by all backup plans are displayed in order of creation time on the backup job page.


1. Log in to the [VKE console](https://console.byteplus.com/vke/overview).

2. In the left navigation bar, click **Backup center \> Application backup** to enter the application backup page.

3. On the **Backup job** tab, view all backup jobs triggered by all backup plans and their job details, such as backup status, source cluster, number of resources, creation time, and backup validity date.

4. Click the name of the target backup job to view its details and those of the resources it backs up.


<span id="RDlWcDmm"></span>
### Method 2: View backup jobs from the backup plan page

You can go to the backup plan details page to view the backup jobs associated with the specified backup plan.


1. Log in to the [VKE console](https://console.byteplus.com/vke/overview).

2. In the left navigation bar, click **Backup center \> Application backup** to enter the application backup page.

3. On the **Backup plan** tab, click the name of the target backup plan to go to the backup plan details page. On the **Backup plan** page, you can view the backup jobs associated with the current backup plan and their details, such as backup status, source cluster, number of resources, creation time, and backup validity date.

4. Click the name of the target backup job to view its details and those of the resources it backs up.


<span id="kGrQK41h"></span>
## Subsequent operations


* If the status of a backup job is **Partially failed**, you can go to the Log of backup job tab on the details page and search for `level=error` to view the failed content and reason for failure. For common cases of partial failure and solutions to partially failed jobs, see [Troubleshooting partially failed jobs](https://docs.byteplus.com/en/docs/vke/Handling_partial_failure_issues).

* If you no longer need a backup job and its backup data, you can delete the backup job. To do so, click **Backup center \> Application backup**, go to the **Backup job** tab, find the job in the backup job list, and click **Delete** in the Actions column.

   <div data-tips="true" data-tips-type="danger" data-tips-is-title="true" data-wrapper-indent="1">danger   </div>
   

   <div data-tips="true" data-tips-type="danger" data-wrapper-indent="1">Deleting a backup job will permanently delete the backup data in the TOS warehouse. Exercise caution when you perform this operation.   </div>
