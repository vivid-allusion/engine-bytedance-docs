---
title: "Managing backup plans"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Manage_backup_plans"
---

After a backup plan has been added, you can go to the Backup plan page to perform related operations. This topic describes the scenarios, impacts, and steps for managing backup plans.

<span id="ECeiBekP"></span>
## Performing immediate backup

After a backup plan is created, scheduled backups will be performed according to the defined backup cycle. To immediately trigger a backup job, click **Backup**.


1. Log in to the [VKE console](https://console.byteplus.com/vke/overview).

2. In the left navigation bar, click **Backup center \> Application backup** to enter the application backup page.

3. On the **Backup plan** tab, find the target backup plan and click **Backup** in the Actions column to immediately trigger a backup job.


<span id="0XuH9yJb"></span>
## Editing backup plans

You can edit the content of an existing backup plan, such as the backup repository, backup cycle, validity period, resources to back up, and PV backup.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For detailed backup plan settings, see <a href="https://docs.byteplus.com/en/docs/vke/Create_backup_plan">Creating backup plans</a>.</div>



1. Log in to the [VKE console](https://console.byteplus.com/vke/overview).

2. In the left navigation bar, click **Backup center \> Application backup** to enter the application backup page.

3. On the **Backup plan** tab, find the target backup plan and click **Edit** in the Actions column to update the backup plan. After you finish, click **Confirm**.


<span id="cFM2jGMC"></span>
## Deleting backup plans

You can delete backup plans no longer needed to release resources.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Deleting a backup plan only terminates the current backup plan and does not simultaneously delete the backup jobs associated with the backup plan.</div>



1. Log in to the [VKE console](https://console.byteplus.com/vke/overview).

2. In the left navigation bar, click **Backup center \> Application backup** to enter the application backup page.

3. On the **Backup plan** tab, find the target backup plan, and in the Actions column, click `...` \> **Delete** to delete the backup plan.
