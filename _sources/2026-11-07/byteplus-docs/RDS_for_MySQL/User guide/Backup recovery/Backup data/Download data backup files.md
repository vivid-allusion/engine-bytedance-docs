---
title: "Download data backup files"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/downloading_data_backup_files"
---

This topic describes the steps for downloading data backup files within the same region.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The instance has been created and is in the **Running** or **Stopped** status. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* You have a data backup file in the same region.

* RDS for MySQL allows you to configure whether to generate public network download addresses for backups. If you need to obtain a public network download address for a backup, ensure that this setting is enabled. For more details, refer to [Modifying backup policy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_data_backup_policies).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Billing

Currently, downloading data backup files over the public network is free of charge. The specific billing start time and prices are subject to official announcements. For more information, refer to [Billing items and prices](https://docs.byteplus.com/en/docs/RDS_for_MySQL/charge_items_and_price?lang=en#.6K6h6LS56aG5).

<span id="ZZpaN3E4"></span>
## Precautions


* Downloading backup files for Volume instances is not supported.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.</div>



3. Click on **Instances** in the left navigation bar.

4. On the **Instances** page, click on the target instance name to enter the instance details page.

5. At the top of the page, click the **Backups** tab.

6. On the **Data backup** tab, click **Data backup** under the **Basic backup list** subtab to go to the data backup list and locate the target backup. Complete the following steps to download the backup file based on the type of the target backup file.



<Tabs>
<Tab zoneid="XZM1huo3lm" title="Physical backup">
<TabTitle>Physical backup</TabTitle>

7. Click the **Download backup file** button in the **Actions** column of the target physical backup file.

8. In the popped\-up **Download backup file** window, the download links for the backup file on the private network and the public network are provided, as well as the expiration time of the download links.

   * Click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a25e5d02ca2929978790bdd0cfaadfb5.png)<sub> </sub></span>icon to the right of the download link to copy the download link.

   * Click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d75c7a6c69094276df0c4cdab768450d.png)<sub> </sub></span>icon to the right of the download link to download the backup file.


</Tab>
<Tab zoneid="E2gXM2vfUW" title="Logical backup">
<TabTitle>Logical backup</TabTitle>

7. In the **Actions** column of the target logical backup file, click **Obtain backup**.

8. In the popped\-up **Download backup file** window, click **Obtain**. The backend then automatically completes the preliminary tasks to obtain the backup file and displays the progress in the window. After the preliminary tasks are completed, the window provides the download links for the backup file on the private and public networks, along with their expiration time.

   * Click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a25e5d02ca2929978790bdd0cfaadfb5.png)<sub> </sub></span>icon to the right of the download link to copy the download link.

   * Click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d75c7a6c69094276df0c4cdab768450d.png)<sub> </sub></span>icon to the right of the download link to download the backup file.


</Tab>
</Tabs>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The download link for the backup file is valid for 7 days. Backup files can be downloaded from this link at any time within the valid period. If the download link expires, you can get a new one by clicking the <strong>Download backup file</strong> button, but the download address will be different each time.</div>


* <div data-tips="true" data-tips-type="tip">The same set of full and incremental backups has the same name prefix. It is recommended to download the same set of full and incremental backups to obtain the full backup data.</div>


* <div data-tips="true" data-tips-type="tip">Please copy the download link and download it in a private network environment (such as on an ECS in the same VPC). <code>test.xbstream</code> in the command is the name defined for the backup file. You can replace it as needed.</div>


   <div data-tips="true" data-tips-type="tip">   ```bash
   curl -o test.xbstream "https://rds-mysql-inner-fake.tos-s3-cn-beijing.ivolces.com/rds/mysql-7347b308****/mysql-7347b308****-m4ab1-0/data/full/full-1748255100060065177.xbstream?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKLTMzI4MTNiZmQ5MzZiNDM1NmEzYmEyM2FmOTY4ODk****%2F20250529%2Fcn-beijing%2Fs3%2Faws4_request&X-Amz-Date=20250529T111545Z&X-Amz-Expires=604800&X-Amz-SignedHeaders=host&X-Amz-Signature=c19b893b41d53a7ec51a8d2a2d6d5447ed169ba10067624c655a54dda863****"
   ```
      </div>
   


<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Description |
|---|---|
|[DownloadBackup](https://docs.byteplus.com/en/docs/RDS_for_MySQL/downloadbackup) |Call the DownloadBackup API to download a backup. |
|[GetBackupDownloadLink](https://docs.byteplus.com/en/docs/RDS_for_MySQL/getbackupdownloadlink) |Call the GetBackupDownloadLink API to obtain the backup download link. |
