---
title: "StarRocks access TOS"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/StarRocks_access_TOS"
---

StarRocks supports accessing table data stored on Volcano Engine TOS.

<span id="_1-使用前提"></span>
## Prerequisites

You must first create a Volcano Engine E\-MapReduce (EMR) StarRocks cluster version 3.6.0 or later.

<span id="_2-示例一：创建-catalog"></span>
## Example 1: Create a catalog

Specify the storage address of TOS by creating a catalog.


* The example is as follows:

   ```sql
   -- Create Hive catalog
   CREATE EXTERNAL CATALOG hive
   PROPERTIES
   (
       "type" = "hive",
       "hive.metastore.uris" = ${HiveMetaStore的地址},
       "aws.s3.access_key" = ${access_key},
       "aws.s3.secret_key" = ${secret_key},
       "aws.s3.endpoint" = ${endpoint},
       "aws.s3.enable_ssl" = "false"
   );
   ```
   

* Note:

   
   |Parameter |Note |
   |---|---|
   |HiveMetaStore |The address of Hive MetaStore in the cluster. Example: thrift://192.168.10.64:9083 |
   |access_key/secret_key |The Access Key ID and Secret Access Key of the Volcano Engine account.<br><br>You can obtain the Access Key ID and Secret Access Key from the [IAM Access Control > Key Management](https://console.volcengine.com/iam/keymanage) interface. For details, see: [Access keys](https://www.volcengine.com/docs/6291/65568). |
   |endpoint |The Endpoint address in the Volcano Engine TOS service. For details, see: [Regions and access domain names (Endpoint)](https://www.volcengine.com/docs/6349/107356). |
