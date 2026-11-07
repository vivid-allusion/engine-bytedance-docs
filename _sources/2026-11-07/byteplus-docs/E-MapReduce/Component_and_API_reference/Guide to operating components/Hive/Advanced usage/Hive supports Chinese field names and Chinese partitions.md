---
title: "Hive supports Chinese field names and Chinese partitions"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Hive_supports_Chinese_field_names_and_Chinese_partitions"
---

Open\-source Hive does not support Chinese field names and Chinese partitions. To use Chinese field names, modify the metadata database. The following statements are used to modify the metadata database:

```SQL
-- Modify metadata
/usr/lib/emr/current/dbservice/bin/mysql -h {IP Adress} -u admin -p
-- Add Chinese partition
ALTER TABLE `PARTITIONS` CHANGE `PART_NAME` `PART_NAME` varchar(767)  CHARACTER SET utf8 COLLATE utf8_bin DEFAULT NULL;
ALTER TABLE `SDS` CHANGE `LOCATION` `LOCATION` varchar(4000) CHARACTER SET utf8 COLLATE utf8_bin DEFAULT NULL;
-- Add Chinese partition, with the partition field as a Chinese field
ALTER TABLE `PARTITION_KEYS` CHANGE `PKEY_NAME` `PKEY_NAME` varchar(128)  CHARACTER SET utf8 COLLATE utf8_bin NOT NULL;
ALTER TABLE `PARTITION_KEY_VALS` CHANGE `PART_KEY_VAL` `PART_KEY_VAL` varchar(256) CHARACTER SET utf8 COLLATE utf8_bin DEFAULT NULL;

-- Only add Chinese fields
ALTER TABLE `COLUMNS_V2` CHANGE `COMMENT` `COMMENT` varchar(256) CHARACTER SET utf8 COLLATE utf8_bin DEFAULT NULL;
ALTER TABLE `COLUMNS_V2` CHANGE `COLUMN_NAME` `COLUMN_NAME` varchar(767) CHARACTER SET utf8 COLLATE utf8_bin NOT NULL;
ALTER TABLE `COLUMNS_V2` CHANGE `TYPE_NAME` `TYPE_NAME` mediumtext  CHARACTER SET utf8 COLLATE utf8_bin DEFAULT NULL;
-- Support Chinese in views
ALTER TABLE TBLS CHANGE VIEW_ORIGINAL_TEXT VIEW_ORIGINAL_TEXT MEDIUMTEXT CHARACTER SET utf8 COLLATE utf8_bin ;
ALTER TABLE TBLS CHANGE VIEW_EXPANDED_TEXT VIEW_EXPANDED_TEXT MEDIUMTEXT CHARACTER SET utf8 COLLATE utf8_bin ;
```
