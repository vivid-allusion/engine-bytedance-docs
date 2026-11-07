---
title: "Recovering logical backup files to a self-managed database"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Recovering_logical_backup_files_to_a_self-managed_database"
---

This topic describes how to recover logical backup files of RDS for MySQL to a self\-managed database.

<span id="S94VNd0F"></span>
# Prerequisites


* You have obtained the logical backup of RDS for MySQL. For more information about obtaining backup files, refer to [Downloading backup file](https://docs.byteplus.com/en/docs/RDS_for_MySQL/downloading_data_backup_files).

* The major version of the self\-managed MySQL database must be the same as that of RDS for MySQL.

* Make sure that no other business is running on the MySQL service.

* Percona XtraBackup has been installed on the server where the self\-managed MySQL database is located.

   * You must install [Percona XtraBackup 2.4](https://docs.percona.com/percona-xtrabackup/2.4/installation.html) for MySQL 5.7 instances.

   * You must install [Percona XtraBackup 8.0 for MySQL 8.0](https://docs.percona.com/percona-xtrabackup/8.0/installation.html) instances.

* [Installing - MyDumper documentation](https://mydumper.github.io/mydumper/docs/html/installing.html) has been installed on the server where the self\-managed MySQL database is located.


<span id="fduryn0d"></span>
# Procedure


1. Procedure Create a data directory for each backup file on the self\-managed server. We use `/data/mydumper_backup` as an example.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If there are multiple backup files, you must create a data directory for each backup file.</div>


```Go
mkdir -p /data/mydumper_backup
```



2. Unpack the backup file.

   * Run the following command to unpack the backup file with the .tar.gz extension. Here, the local path of the backup file is `/data/export-logic.tar.gz`, and the target unpacking path is `/data/mydumper_backup`.


```Shell
tar -zxvf export-logic.tar.gz 
mv export-logic/* /data/mydumper_backup
```



   * Run the following command to unpack the backup file with the .xbstream extension. Here, the local path of the backup file is `/data/logical-mydumper.xbstream`, and the target unpacking directory is `/data/mydumper_backup`.


```Go
xbstream -x --parallel=4 -C /data/mydumper_backup < /data/logical-mydumper.xbstream
```



3. Import the logical backup to a self\-managed MySQL database.


```Go
myloader --overwrite-tables --verbose=3 --innodb-optimize-keys --host=127.0.0.1 --user=$mysql_user --port=$mysql_port --password=$mysql_password --directory=/data/mydumper_backup --threads=4
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Replace <code>$mysql_user</code> with the self\-managed MySQL database account, <code>$mysql_port</code> with its port number, and <code>$mysql_password</code> with the account password.</div>



4. After the command is completed, you can run echo $? to check the process exit code. A return value of 0 indicates that the recovering task succeeded. Any other value indicates that the recovering task failed.
