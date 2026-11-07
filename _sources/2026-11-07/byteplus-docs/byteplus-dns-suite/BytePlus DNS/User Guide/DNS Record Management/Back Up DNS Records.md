---
title: "Back Up DNS Records"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/docs-backing-up-dns-records"
---

This document describes how to backup and restore your DNS records based on backup records.

You can only backup and restore DNS records for your domain if the [edition](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-editions) of your domain is ultimate edition or exclusive edition.

<span id="533f2fec"></span>
## Steps

Complete the following steps to back up DNS records.


1. Open the [BytePlus DNS console](https://console.byteplus.com/dns-suite/dns).

2. Go to the **Domain management** page. Click your domain in the **Domain** column.

3. Click the **DNS backup** tab.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the edition of your domain is not ultimate edition or exclusive edition, the console will prompt you to upgrade the edition of your domain to enable this feature. Click on <strong>Upgrade now</strong> to upgrade the edition of your domain.</div>


You can perform the following operations on the **DNS backup** tab:


* Automatically backup DNS records

* Manually backup DNS records

* Rollback DNS records to a specific backup

* Download backups

* Delete backups


<span id="52bd4a73"></span>
### Automatically backup DNS records

By default, automatic backup is disabled.


1. Click **Automatic backup settings**.

2. On the **Automatic backup settings** page, set the **Interval** parameter:

   * **Hourly**: BytePlus DNS generates a backup of the domain's DNS records every hour.

   * **Daily**: BytePlus DNS generates a backup of the domain's DNS records once a day.

   * **Monthly**: BytePlus DNS generates a backup of the domain's DNS records once a month.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The DNS can store up to 10 backups for a domain. The backup with the latest creation time will replace the backup with the earliest creation time. Therefore, you can choose the appropriate backup frequency based on your needs.</div>



3. Click **OK**. The **Automatic backup settings** section will display the currently effective automatic backup mode.


<span id="2a77c98f"></span>
### Manually backup DNS records

BytePlus DNS can store up to 10 backups for a domain. If you manually backup the DNS records of a domain that already has 10 backups, the manually created backup will overwrite the backup with the earliest creation time.


1. Click **Create backup**.

2. In the **Create backup** dialog box, click **Back up**.


You can see the backups you created in the **Version list** section.

<span id="rollback-dns-records-to-a-specific-backup"></span>
### Rollback DNS records to a specific backup

If you encounter issues with the updated DNS records, you can rollback the DNS records to a previous version.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Rolling back the DNS records will affect the domain's accessibility as there may be differences between the records in the backup and the records before the rollback. This operation cannot be undone. Please proceed with caution.</div>



1. In the **Version list** section, find the backup you want to rollback to. Click **Rollback to this version** in the **Action** column.

2. Click **Rollback** in the pop\-up dialog box.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If the IP\-based line or line group used in the backup has been deleted, the rollback will fail.</div>


* <div data-tips="true" data-tips-type="tip">Suppose the edition of your domain is downgraded from exclusive edition to ultimate edition. The backup you want to rollback to was created using the exclusive edition. The DNS records in the backup use parameters that comply with the exclusive edition but exceed the ultimate edition. In this case, the rollback will succeed. However, you will not be able to edit the records that exceed the limitations again. For the limitations of different editions, see <a href="https://docs.byteplus.com/docs/byteplus-dns-suite/docs-editions">Editions</a>.</div>


* <div data-tips="true" data-tips-type="tip">If the backed\-up DNSSEC status is different from the current DNSSEC status, the current DNSSEC status will remain unchanged during rollback.</div>



If the rollback fails, the DNS will revert the rollback operation. Your domain will retain the DNS records before the rollback.

<span id="download-backups"></span>
### Download backups

The DNS can store up to 10 backups for a domain. If you need to store more backups, you can download the backups. You can use [Import DNS records](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-import-dns-records) to rollback the DNS records to the downloaded backups. When importing, you need to select **Full import**.


1. In the **Version list** section, find the backup you want to download. Click **Download** in the **Actions** column.

2. In the pop\-up dialog box, select the file format you want to download. Click **Download**.


You can download `.zone` files or `.xlsx` files. Compared to `.xlsx` files, `.zone` files do not include the following fields:


* **Line**: After importing the `.zone` file, BytePlus DNS automatically sets the **Line** of the relevant DNS records to `Default`.

* **Domain Prefix**: After importing the `.zone` file, BytePlus DNS automatically fills in the **Domain Prefix** field with the domain prefix from the FQDN.

* **Enable**: After importing the `.zone` file, BytePlus DNS automatically sets the **Enable** of the relevant DNS records to `True`.


<span id="delete-backups"></span>
### Delete backups

The DNS can store up to 10 backups for a domain. You can delete unnecessary backups.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Deleted backup versions cannot be recovered. If you want to store more backup versions, you can download the backups.</div>



1. In the **Version list** section, find the backup version you want to delete. Click **Delete** in the **Actions** column.

2. In the pop\-up dialog box, click **OK**.
