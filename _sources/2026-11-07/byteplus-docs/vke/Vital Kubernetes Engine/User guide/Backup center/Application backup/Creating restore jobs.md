---
title: "Creating restore jobs"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Create_a_recovery_job"
---

VKE supports one\-click data restore to a specified cluster based on successful or partially failed backups. This topic describes how to create a restore job.

<span id="CreN4jog"></span>
## Background


* **Backup/Restore target clusters**: All VKE clusters, such as managed clusters and registered clusters, can be used as backup/restore target clusters.

* **Backup/Restore resource scope**: The backup center provides namespace\-level application metadata backup and restore, including Kubernetes\-native resources, CustomResourceDefinition (CRD) resources, and volume resources. The following types of data are supported for backup and restore:

   * **Application metadata**, which refers to the definition data of Kubernetes objects.

   * **Volume data**, which refers to the data in volumes mounted to pods. Volume types include PVC, local, emptyDir, and more.


The restore job states and their operation restrictions are as follows:


|**Status** |**Description** |**Notes** |<div style="text-align: center"><br><strong>Supported actions</strong></div><br> ||
|---|---|---|---|---|
||||<div style="text-align: center"><br><strong>View details</strong></div><br> |<div style="text-align: center"><br><strong>Delete</strong></div><br> |
|Starting |The restore job is initializing and the restoration has not started yet. |Intermediate status |<div style="text-align: center"><br>✔️</div><br> |<div style="text-align: center"><br>❌</div><br> |
|Restoring |The job has started execution and is restoring data. |Intermediate status |<div style="text-align: center"><br>✔️</div><br> |<div style="text-align: center"><br>❌</div><br> |
|Succeeded |All data has been restored and no errors occurred. |Stable status |<div style="text-align: center"><br>✔️</div><br> |<div style="text-align: center"><br>✔️</div><br> |
|Fail |Restore job validation failed. The restore job has not started yet. |Stable status |<div style="text-align: center"><br>✔️</div><br> |<div style="text-align: center"><br>✔️</div><br> |
||A failure occurred during the execution of the restore job, so it cannot proceed and other resources will not be restored. |Stable status |<div style="text-align: center"><br>✔️</div><br> |<div style="text-align: center"><br>✔️</div><br> |
|Partially failed |Certain resources failed to be restored. Other resources will be restored normally. |Stable status |<div style="text-align: center"><br>✔️</div><br> |<div style="text-align: center"><br>✔️</div><br> |
|Deleting |The restore job is being deleted. |Intermediate status |<div style="text-align: center"><br>❌</div><br> |<div style="text-align: center"><br>❌</div><br> |


<span id="aaCoDqrn"></span>
## Usage limits


* The recommended Kubernetes version range for backup/restore target clusters is v1.24.x to v1.32.x.

* Only successful or partially failed backup jobs can be restored.


<span id="fp3int8g"></span>
## Prerequisites


* The migrate\-plugin add\-on has been installed. For details, see [migrate-plugin](https://docs.byteplus.com/en/docs/vke/migrate-plugin).

* A backup plan has already been created, for which successful or partially failed backup jobs exist. For details, see [Creating backup plans](https://docs.byteplus.com/en/docs/vke/Create_backup_plan).


<span id="IKpowNBd"></span>
## Procedure


1. Log in to the [VKE console](https://console.byteplus.com/vke/overview).

2. In the left navigation bar, click **Backup center \> Application backup** to enter the application backup page.

3. Go to the Restore job page, configure the following settings, and click **Confirm**.

   * On the **Restore job** tab, click **Create backup job**.

   * On the **Backup job** tab, find the target backup job and click **Restore** in the right Actions column.

   * On the **Backup plan** tab, click the name of the target backup plan to go to the details page. On the backup job tab, find the target backup job and click **Restore** in the Actions column.

      
      |**Parameter** |**Description** |
      |---|---|
      |Name |Enter a custom name for the restore job. |
      |Backup job |Only successful or partially failed backup jobs support restoration.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can go to the Log of backup job tab on the backup job details page and search for <code>level=error</code> to check and confirm the scope of resources that failed to be backed up by the partially failed backup job. This helps ensure that key data is not lost when the platform restores resources.</div><br> |
      |Target cluster |Select the target cluster for restoring backup data. Make sure that the migrate\-plugin add\-on is installed in the selected cluster.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If the selected cluster does not have the required migrate\-plugin add\-on installed, click <strong>Install</strong> and wait for the add\-on to be installed successfully.</div><br> |
      |Redefine namespace |By default, the namespace for restore is the same as the source namespace. You can also redefine the restore namespace mapping. If the target namespace does not exist, it will be created in the target cluster.<br><br><br>* **Source namespace**: The namespace of the source cluster for backup.<br><br>* **Target namespace**: The namespace of the target cluster where backup data is restored. |
      |PersistentVolume |By default, this feature is disabled. To restore PV, enable PV restoration, and configure the mapping between the source storage type and the storage type in the restore target cluster. Volume restore supports StorageClass redefinition to map the StorageClass in the source backup to the StorageClass in the target cluster:<br><br><br>* **Source storage type**: The source storage type in the backup data of the source cluster. By default, all StorageClasses in the backup volumes are included.<br><br>* **Target storage type**: The target storage type after the backup data is restored to the target cluster.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The PersistentVolume restore configuration is displayed only when the source cluster backup job has enabled PV backup.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the backup job in the source cluster has PV backup enabled but the actual backup is empty, no relevant data can be obtained for the source storage type, and the selection list is empty.</div><br> |
      


<span id="q7SZ1NMH"></span>
## Subsequent operations


* After the restore job is completed, you can view the restore status using the Status field. If the status is **Partially failed**, go to the Log of restore job tab on the restore job details page and search for `level=error` to view the failed content and reason for failure. For common cases of partial failure and solutions to partially failed jobs, see [Troubleshooting partially failed jobs](https://docs.byteplus.com/en/docs/vke/Handling_partial_failure_issues).

* If you no longer need a restore job, you can delete the restore job. To do so, click **Backup center \> Application backup**, go to the **Restore job** tab, find the job in the Restore job list, and click **Delete** in the Actions column.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Deleting a restore job will also delete restoration logs and other related information. Exercise caution when you perform this operation.   </div>
