---
title: "Creating backup plans"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Create_backup_plan"
---

The backup center supports backing up application metadata and PersistentVolume (PV) data to TOS. This topic describes how to create a backup plan.

<span id="g0LUJUJW"></span>
## Background


* **Backup/Restore target clusters**: All VKE clusters, such as managed clusters and registered clusters, can be used as backup/restore target clusters.

* **Backup/Restore resource scope**: The backup center provides namespace\-level application metadata backup and restore, including Kubernetes\-native resources, CustomResourceDefinition (CRD) resources, and volume resources. The following types of data are supported for backup and restore:

   * **Application metadata**, which refers to the definition data of Kubernetes objects.

   * **Volume data**, which refers to the data in volumes mounted to pods. Volume types include PVC, local, emptyDir, and more.


<span id="E8DuCdhj"></span>
## Usage limits


* The recommended Kubernetes version range for backup/restore target clusters is v1.24.x to v1.32.x.

* The PV backup feature supports only cluster version v1.20.x and later.


<span id="eFfKUhtD"></span>
## Prerequisites


* The migrate\-plugin add\-on has been installed. For details, see [migrate-plugin](https://docs.byteplus.com/en/docs/vke/migrate-plugin).

* A backup repository has been created and is available. For details, see [Adding repositories](https://docs.byteplus.com/en/docs/vke/Add_warehouse).


<span id="Zlnpf4Lw"></span>
## Procedure


1. Log in to the [VKE console](https://console.byteplus.com/vke/overview).

2. In the left navigation bar, click **Backup center \> Application backup** to enter the application backup page.

3. Click the **Backup plan** tab and click **Create backup plan** to specify the parameters of the backup plan.

   * **Basic** ** information**

      
      |**Parameter** |**Description** |
      |---|---|
      |Plan name |Enter a custom name for the backup plan. |
      |Backup repositories |Select a TOS warehouse that has already been added. The TOS warehouse is used as the backup warehouse. |
      |Region ID |Select a region. |
      |Source cluster |Select the source cluster containing the application data to be backed up. Make sure that the migrate\-plugin add\-on is installed in the selected cluster.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">If the selected cluster does not have the required migrate\-plugin add\-on installed, click <strong>Install</strong> and wait for the add\-on to be installed successfully.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If the selected cluster cannot access the backup warehouse, the backup warehouse cannot be used. You need to check connectivity and try again later if it is unavailable.</div><br> |
      |Source namespace |Select a namespace within the source cluster. Backup plans only at the namespace level are supported. You can select one or more namespaces in the source cluster according to your backup requirements. |
      |Backup type |Select a backup policy for the backup based on your actual requirements.<br><br><br>* **Scheduled backup**: After the backup plan is created, application data will be backed up on a schedule according to the configured backup cycle.<br><br>* **Backup now**: After the backup plan is created, a backup job will be executed immediately and only once. |
      |Backup cycle |When the backup type is scheduled backup, this setting is required. Configure the repeat cycle and trigger time of the backup job.<br><br><br>* **Time settings**: Visually configure the repetition cycle and trigger time of the backup job. The repetition cycle can be set on a monthly, weekly, or daily basis. The trigger time can be specified by time interval or fixed time.<br><br>* **Cron expression**: Set the backup cycle using a Cron expression. The China region (UTC+8) supports crontab syntax. For details, see the [official Crontab documentation](https://crontab.guru/).<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Click <strong>Trigger time preview</strong> to preview the specific trigger times of the latest four backup jobs (accurate down to seconds).</div><br> |
      |Backup validity date |The retention period for backup jobs is 30 days by default and can be configured as needed.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Backup jobs that exceed the specified duration will be deleted. Deleted resources include backup jobs, application files backed up in TOS, and all PV snapshots.</div><br> |
      |Resources for backup |By default, all resources in the selected namespaces are backed up. You can specify labels or exact resource types for data backup according to actual needs, or exclude certain resources from data backup. The resource backup conditions are combined using logical **AND**. For example:<br><br><br>* If no label, resource, or exclusion condition is configured, all resources in the selected namespaces will be backed up.<br><br>* If a label is specified, only resources that are in the selected namespaces and have the label will be backed up.<br><br>* If both labels and specific resources are configured, the **AND** logic will be applied to filter resources for data backup. |
      ||**Specify label for backup**: Filter resources within the selected namespaces by label. When multiple labels are specified, a resource is included in the backup only if all labels match. |
      ||**Specify resources for backup**: Specify resource types for data backup. Only the specified types of resources will be backed up. You can add one or more resource types, for example, Deployment and ConfigMap. |
      ||**Exclude resources for backup**: Exclude specific resources from the backup. Example resources include Pod and Secret. |
      

   * **PersistentVolume**

      
      |**Parameter** |**Description** |
      |---|---|
      |Backup PersistentVolume |The PersistentVolume backup switch is disabled by default and can be configured as needed.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This setting is supported only by cluster version v1.20.x or later.</div><br> |
      |Available method |Select the backup method for PV backup. Currently, CSI snapshots are supported. For details, see [PersistentVolume backup method](https://docs.byteplus.com/en/docs/vke/Backup_center_overview#HPyCBAHE). |
      

4. Click **Confirm**.


<span id="ePusWycQ"></span>
## Subsequent operations


* After the backup plan is created, backup jobs will be triggered according to the backup cycle. You can go to the details page to view the backup jobs for the backup plan or go to the backup job management page to view all backup jobs. For details, see [Viewing backup jobs](https://docs.byteplus.com/en/docs/vke/View_backup_job).

* You can manage an existing backup plan. For details, see [Managing backup plans](https://docs.byteplus.com/en/docs/vke/Manage_backup_plans).
