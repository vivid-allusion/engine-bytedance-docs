---
title: "Decrypting backup files"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/decrypting_backup_files"
---

Database backup files are important files that support the data security and stability of the database. To improve the security of database backup files, RDS for MySQL supports encrypting backup files. If the encrypted backup file is downloaded to local use, the backup file needs to be decrypted. This topic introduces the operation steps for decrypting backup files.

<span id="prerequisites"></span>
## Prerequisites


* The target backup file has been downloaded to the local. For more detailed information about downloading data backup files, see [Downloading data backup files](https://docs.byteplus.com/en/docs/RDS_for_MySQL/downloading_data_backup_files); for more detailed information about downloading log backup files, see [Downloading binlog backups](https://docs.byteplus.com/en/docs/RDS_for_MySQL/downloading_binlog_backups).

* The key of the target backup file has been downloaded to the local. For more detailed information about downloading backup file keys, please see [Downloading backup file keys](https://docs.byteplus.com/en/docs/RDS_for_MySQL/downloading_backup_file_keys).


<span id="steps"></span>
## Steps


* Decrypt data backup files

   1. Store the data backup file and the key of the data backup file in the same directory.

   2. View the key in the key through the `cat` command.

   3. Create a MySQL data directory.

   4. Perform xbstream decryption.

      ```bash
      xbstream -x -v --decompress --decrypt=AES256 --encrypt-key='fa5056474928d5cfe2eeff02edcaceff' -C mysql_data < full-1713236719753042916.xbstream
      ```
      

   5. After decompression is completed, confirm that the data in the data directory has been decompressed correctly.

* Decrypt binlog backups

   1. Store the binlog backup file and the key of the binlog backup file in the same directory.

   2. View the secret key and vector saved in the key, and obtain the corresponding hexadecimal value through `xxd`.

      ```bash
      key=`echo -n b2afbc4c598bf9f613a9b07d128818e3 | xxd -p | tr -d '[:space:]'`
      
      iv=`echo -n b56727bcdf6be13e | xxd -p | tr -d '[:space:]'`
      ```
      

   3. Decrypt the file through `openssl`.

      ```bash
      openssl enc -d -aes-256-cbc -K $key -iv $iv -in binlog-1713237686709023371-binlog.000014 -out binlog.000014
      ```
      

   4. Verify the correctness of the binlog backup file.

      ```bash
      mysqlbinlog -vv binlog.000014
      ```
