---
title: "Data backup"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/data-backup"
---

ByteHouse provides a data backup function, which can solve the problem of data recovery after accidental deletion or modification, as well as the function of disaster recovery in extreme cases. ByteHouse supports both full and incremental backups. You can configure backup policies as needed to ensure data security, enhancing data recovery efficiency.

<span id="b11edf4f"></span>
# Usage restrictions


* Version requirements:

   * Before using complete and incremental backups, please ensure that your ByteHouse engine version is v2.7.1.61 or above.

   * You can view the current cluster’s version via the **ByteHouse Console** \> **Manage clusters** \> **Cluster** **list** \> **Cluster details** \> **Basic information** \> **Version** path.

* This feature is in Beta. To use it, submit a support ticket or contact the ByteHouse team to obtain whitelist access.


<span id="02bd01eb"></span>
# Precautions


|Segmentation |Precautions |
|---|---|
|Supported Tables |* Currently, only the backup of tables is supported. Backup for views, materialized views, Kafka tables, and other data objects is not supported.<br><br>* Currently, only backups within the same region are supported. Cross\-region backups are not supported. |
|Costs |* Computing Costs: During the execution of data backup and restoration, computing group resources are used, resulting in computation costs.<br><br>* Storage Costs: Data backup will occupy storage resources, incurring storage costs, which start being billed upon the activation of the backup strategy. |


<span id="e14cbe9d"></span>
# Data backup

<span id="5cba2d21"></span>
## Enable backup

Log in to the ByteHouse Enterprise console, go to the cluster details page via the path **Cluster management** \> **Cluster list** \> **Cluster name**, and click the **Data Backup** tab. A welcome prompt will appear on your first visit; click the **Enable Now** button on the prompt page to enable the data backup function. The welcome prompt for the first visit is shown in the figure below.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5d3197cb63fb41e588d144d3b845ad90~tplv-goo7wpa0wc-image.image) </span>

<span id="eb323284"></span>
## Create backup strategy


1. After logging in to the ByteHouse Enterprise control console, enter **Manage clusters** \> **Cluster list** \> **Cluster name** to enter the cluster details page. Click the "**Data Backup**" page at the top and then click the "**Create backup policy**" button under the "**Backup policy**" tab.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/08b51cd4fe2a46a6a1d85a63f7f092a8~tplv-goo7wpa0wc-image.image) </span>

2. On the pop\-up page, fill in the information to create a backup strategy.

   1. Fill in the basic information and you can customize the backup strategy name.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6689d4404d99436997bacf3fc3a57bc7~tplv-goo7wpa0wc-image.image) </span>

      The strategy name must meet the following conditions: supports numbers, letters, and underscores, but cannot start with a number, a maximum of 64 characters, and must not duplicate existing task names.

   2. Select the backup object, supporting backup on the levels of the entire cluster, entire database, or specific tables. You can choose according to your actual backup needs.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f66d3ef021f441be8e77e2278e9160be~tplv-goo7wpa0wc-image.image) </span>

   3. Confirm the backup schedule. Choose either full backup or full + incremental backup.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c12ec002d65a4125ab51784b6c00928d~tplv-goo7wpa0wc-image.image) </span>

   * Full backup: Complete data backup for the cluster.

   * Full + incremental backup: For the initial backup of the cluster, a full backup is used, followed by subsequent incremental backups. Incremental backups are based on a previous full backup or the last incremental backup under the same strategy.

3. Click "**Create**."

4. Tasks saved successfully will appear in the "**Backup policy**" list.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/45bff4326aa5443594b892f36e7ba52f~tplv-goo7wpa0wc-image.image) </span>

5. Click on the "**Backups**" tab. When the scheduled time arrives, the backup mission will automatically execute.


<span id="c3db9c09"></span>
## View the status of the backups

After the automatic completion of the backup mission, you can check the status of the backups in the backup set. If the backup is unsuccessful, you can click on the corresponding backup set mission to view the task details, and see the data scope and reasons for failure.

<span id="1787bfa5"></span>
## View backups storage usage

After the backup task starts, you can view the storage space occupied by all backup sets at **Data Backup** \> **Backups** and estimate the storage costs of all backup sets.

<span id="a68775e2"></span>
# Restore data

After running the backup task, we can restore the data in the backup set.


1. Access the "**Data Backup** \> **Backups**" page, and click the "**Restore**" button on the right of the data to be restored.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/16bcb7b5424443939863ed14647cb84c~tplv-goo7wpa0wc-image.image) </span>

2. Select the database and table information that needs to be restored.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/efef1c45b7404c32a03ada57f3181e11~tplv-goo7wpa0wc-image.image) </span>

3. Click "**OK**", and the data restoration will start.

4. After successful restoration, you can view the history of the restored data on the "**Restoration records**" tab.


<span id="cba4b555"></span>
# Delete backups

You can view all executed backup sets in the backup set tab, and for redundant backup sets that are no longer useful, you can click the delete button next to the corresponding backup set to delete and save on storage costs.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The operation to delete datasets is irreversible. Please proceed with caution.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/226195e7c7b44697b33fbb40a38a187c~tplv-goo7wpa0wc-image.image) </span>
