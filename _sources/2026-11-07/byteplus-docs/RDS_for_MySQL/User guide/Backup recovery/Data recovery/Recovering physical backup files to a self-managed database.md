---
title: "Recovering physical backup files to a self-managed database"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/recovering_physical_backup_files_to_a_self-managed_database"
---

This topic describes how to recover physical backup files of RDS for MySQL to a self\-managed database. The following backup files or a combination of backup files can be used for recovery:


* A single full backup file

* A full backup file and one or more incremental backup files


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have obtained the physical backup of RDS for MySQL. For more information about obtaining backup files, refer to [Downloading backup file](https://docs.byteplus.com/en/docs/RDS_for_MySQL/downloading_data_backup_files).

   * If the backup files contain incremental backup files, ensure that you have obtained the full backup file on which the incremental backup files are based.

   * If the backup files contain multiple incremental backup files, make sure that these incremental backup files are continuous incremental backups.

* The database version of the self\-managed MySQL database must be the same as that of RDS for MySQL.

* The instance type of the self\-managed database must be a high\-availability version.

* Make sure that no other business is running on the MySQL service.

* Percona XtraBackup has been installed on the server where the self\-managed MySQL database is located.

   * You must install [Percona XtraBackup 2.4](https://docs.percona.com/percona-xtrabackup/2.4/installation.html) for MySQL 5.7 instances.

   * You must install [Percona XtraBackup 8.0 for MySQL 8.0](https://docs.percona.com/percona-xtrabackup/8.0/installation.html) instances.


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limitation

If the other business is running on your current self\-managed database, the original business becomes unavailable after the physical backup of RDS for MySQL is recovered to this database.

The recovery solution described in this document is used to recover data to a new database data directory in the self\-managed database, which does not affect the original data in the self\-managed database.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Procedure Create a data directory for each backup file on the self\-managed server. Here, `/home/mysql/data` is used as an example.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If there are multiple backup files, you must create a data directory for each backup file.   </div>
   

   ```json
   mkdir /home/mysql/data
   ```
   

2. Process the backup file.

   1. If the backup file has not been compressed or is for a MySQL 8.0 instance, use the following command to process the backup file. We use `/data/backup.xbstream` as the local path for the backup file here.

      ```json
      xbstream -x --parallel=4 -C /home/mysql/data < /data/backup.xbstream
      ```
      

   2. If the backup file is for a MySQL 5.7 instance and has been compressed, take the following steps to process the backup file. We use `/data/backup.qp.xbstream` as the local path for the backup file here.

      * Unpack the backup file.

         ```shell
         xbstream -x --parallel=4 -C /home/mysql/data < /data/backup.qp.xbstream
         ```
         

      * Unpack the backup file.

         Unpack all files with the `.qp` suffix in the target directory.

         ```shell
         xtrabackup --decompress --target-dir=/home/mysql/data
         ```
         

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Before unpacking, install the qpress command by following the steps in <a href="https://docs.percona.com/percona-xtrabackup/2.4/installation/apt_repo.html?spm=a2c4g.11186623.0.0.7e75622eWBp5N7#installing-percona-xtrabackup-via-percona-release">Percona XtraBackup \- Installing Percona XtraBackup on Debian and Ubuntu</a>.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">By default, <code>xtrabackup</code> does not delete the original <code>.qp</code> compressed files after unpacking. To delete the <code>.qp</code> compressed files after unpacking, add the <code>--remove-original</code> parameter to the command above.      </div>
      

3. Prepare backup data.

   ```json
   xtrabackup --prepare --target-dir=/home/mysql/data
   ```
   

   Prepare succeeds when the following log appears.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_76675ad5859c86934c2b12801f717d74.png) </span>

   If you have multiple incremental backup files, perform the prepare operation on each one in chronological order.

   ```json
   xtrabackup --prepare --target-dir=/home/mysql/data --incremental-dir=<增量备份解压的目录>
   ```
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If there are incremental backups, add the <code>--apply-log-only</code> parameter to the <code>--prepare</code> command for all backup files except for the last one.   </div>
   

4. Modify the data file property.

   ```json
   chown -R mysql:mysql /home/mysql/data
   ```
   

5. `json chown \-R mysql:mysql /home/mysql/data ` Start MySQL.

   ```json
   mysqld --defaults-file=/home/mysql/data/my.cnf --user=mysql --datadir=/home/mysql/data &
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">my.cnf is the profile of a self\-managed database.   </div>
   

6. Log in to the database.

   Log in with the account and password set in an instance of the source database.

   ```json
   mysql -u<源 RDS 实例账号> -p<对应密码>
   ```
   


<span id=".5bi46KeB6Zeu6aKY"></span>
## FAQ


* `json mysql \-u \-p ` FAQs How do I log in as a root user?

   You should first disable mysqld, and then add the `--skip-grant-tables` parameter to restart mysqld to skip authentication, in which mode you should modify the password of the root user. After the modification, you can restart mysqld to log in as a root user.
