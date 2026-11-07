---
title: "Data export"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-exporting-data-from-bytehouse"
---

The ByteHouse data export function efficiently and securely migrates data to object storage or your local path, meeting your needs for data backup, offline analysis, and cross\-platform sharing. This article explains how to export data through the console, CLI, and IDE tools.

<span id="decb1943"></span>
# Prerequisites

Before starting, ensure you have the following necessary permissions and information:


* Access to ByteHouse cloud data warehouse service:

   * AccountAdmin or SystemAdmin role is recommended.

   * For granting the ByteHouseFullAccess IAM policy to new users, refer to [Grant privileges](https://docs.byteplus.com/docs/bytehouse/docs-user-management#0d0076bb).

* If you want to export data to object storage, make sure you have the following permissions:

   * Obtain the Access Key ID and Secret Access Key for the object storage service. If you use BytePlus Object Storage Service (TOS), please refer to [Creating an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey) for details on how to obtain them.

   * Create a bucket in the object storage service for data export. Ensure the user you use has full read and write permissions for that bucket. If you use BytePlus TOS, see [Create a Bucket](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket) and [Grant Bucket Permissions](https://docs.byteplus.com/en/docs/tos/docs-overview_3) for operation details.


<span id="ad8a4bb3"></span>
# Cautions


* When exporting data to the object storage service, ByteHouse supports both same\-region and cross\-region export. Both methods use public network access and incur related costs. It is recommended to read the billing rules of the services you use before proceeding.

* ByteHouse supports data export through commands and IDE tools. Different methods apply to the following scenarios:

   * Export through commands: Export data to the object storage service.

   * Export using IDE tool: Export data to local.


<span id="8747dade"></span>
# Preparation

ByteHouse supports exporting data through Console, ByteHouse CLI tool, and IDE tools. Choose the export tool as needed. Before starting the export, ensure you have the required tools ready and are connected to ByteHouse.


|Tool |Installation and Connection Instructions |
|---|---|
|ByteHouse CLI |Refer to the following documents to install ByteHouse CLI and connect to ByteHouse:<br><br><br>* ByteHouse CLI [Installation](https://docs.byteplus.com/docs/bytehouse/docs-gateway-client#3bf1a375)<br><br>* [Connect to ByteHouse](https://docs.byteplus.com/docs/bytehouse/docs-gateway-client#430f8deb) |
|IDE Tools |Use IDE tools to connect to ByteHouse and export data.<br><br><br>* [DataGrip (TCP)](https://docs.byteplus.com/docs/bytehouse/docs-DataGrip)<br><br>* [DataGrip (ClickHouse)](https://docs.byteplus.com/docs/bytehouse/datagrip-clickhouse)<br><br>* [DataGrip (MySQL)](https://docs.byteplus.com/docs/bytehouse/datagrip-mysql)<br><br>* [DBeaver (ClickHouse)](https://docs.byteplus.com/docs/bytehouse/dbeaver-clickhouse)<br><br>* [DBeaver (TCP)](https://docs.byteplus.com/docs/bytehouse/docs-DBeaver)<br><br>* [DBeaver (MySQL)](https://docs.byteplus.com/docs/bytehouse/dbeaver-mysql)<br><br>* [Navicat (MySQL)](https://docs.byteplus.com/docs/bytehouse/navicat-mysql)<br><br>* [TablePlus (MySQL&ClickHouse)](https://docs.byteplus.com/docs/bytehouse/tableplus-mysql-clickhouse) |


<span id="113cf831"></span>
# Export by SQL statement

<span id="87181cee"></span>
## Syntax

The data export function is implemented with the following SQL statements, which you can use with ByteHouse Console, ByteHouse CLI, and other tools.

```sql
SELECT <expr_list> 
FROM db.table
INTO OUTFILE "destination://file_path/file_name"
[FORMAT format_name] [COMPRESSION compression_name] SETTINGS setting_name 
```


<span id="772797f5"></span>
### Parameter description


|Parameter |Required |Description |
|---|---|---|
|<expr_list\> |Yes |Specify the data to be exported. |
|db.table |Yes |Specify the database and table name of the data. |
|destination://file_path/file_name |Yes |Specify the object storage path and export file name for the exported file. Example:<br><br><br>* TOS: `'vetos://my-testing/data/data-export-test.csv'`.<br><br>* Other object storage services: `s3://bucket/test_outfile.csv`.<br><br><br>Ensure you have read and write permissions for this storage path. If exporting to TOS, verify your full read and write permissions via **TOS Console** \> **Bucket List** \> **Privilege Management** \> **Bucket Authorization Policy Management**. If permissions are missing, refer to [Authorizing IAM Users of an Account](https://docs.byteplus.com/en/docs/tos/docs-authorizing-iam-users-of-an-account) to assign TOSFullAccess permissions to the user. |
|FORMAT |No |Specify the export file format. Supports common formats including JSON, TSVWithNames, TSV, CSV, CSVWithNames, JSONEachRow, Parquet, and ORC. |
|COMPRESSION |No |Specify the compression format for the exported file. Currently supported compression types include none, gzip, deflate, br, xz, and zstd. |
|SETTINGS |Yes |Configure access information for exporting to BytePlus TOS using the settings parameter:<br><br><br>* `tos_access_key`: Access Key obtained from BytePlus Key Management. For details, refer to [Creating an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey) .<br><br>* `tos_secret_key`: Secret Access Key obtained from BytePlus Key Management. For details, refer to [Creating an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey) .<br><br>* `tos_region`: Region ID where TOS is located. For the list of available regions, see [Region and Endpoint](https://docs.byteplus.com/en/docs/tos/docs-region-and-endpoint).<br><br>* tos_endpoint: The Access domain name of TOS. The format is `http://tos-s3-{REGION}.ibytepluses.com`. For more TOS endpoints, refer to [Region and Endpoint](https://docs.byteplus.com/en/docs/tos/docs-region-and-endpoint). When you fill in the endpoint in the command, you can use the S3 endpoint in the table based on your actual TOS region.<br><br>* `tos_security_token`: Optional. STS temporary key for more secure access to TOS.<br><br><br>If you use other object storage services, configure the access information with the following settings parameters:<br><br><br>* `s3_ak_id`: Access Key ID of the object storage service. Refer to the official documentation of your object storage service to obtain the Access Key ID.<br><br>* `s3_ak_secret`: Secret Access Key of the object storage service. Refer to the official documentation of your object storage service to obtain the Secret Access Key.<br><br>* `s3_region`: Region ID of the object storage service. Refer to the official documentation of your object storage service to get the region. For example, `oss-cn-beijing`、`cn-northwest-1`.<br><br>* `s3_endpoint`: Access domain name of the object storage service. Refer to the official documentation of your object storage service to get the access domain name. For example, `http://s3.eu-west-1.amazonaws.com`、`https://oss-cn-beijing.aliyuncs.com`.<br><br>* `s3_use_virtual_hosted_style`: It sets the bucket access method. The default value is false, which means accessing the bucket using path style. |


<span id="d77ff882"></span>
## Data export examples

<span id="80f49531"></span>
### Export using ByteHouse Console

ByteHouse supports file export by configuring the object storage path and parameters, providing a more stable and persistent export solution.


1. Execute the following statement on the ByteHouse console **SQL worksheet** page to export TOS data. Refer to [Parameter description](https://docs.byteplus.com/docs/bytehouse/docs-exporting-data-from-bytehouse#772797f5) for parameter configuration.

   
   <Tabs>
   <Tab zoneid="nP2RZWafzM" title="Export to TOS">
   <TabTitle>Export to TOS</TabTitle>
   
   ```SQL
   SELECT * FROM db.table
   INTO OUTFILE 'vetos://my-testing/data/data-export-test.csv' 
   FORMAT CSV COMPRESSION 'none'
   SETTINGS 
   tos_access_key = '{YOUR_TOS_ACCESS_KEY}', 
   tos_secret_key = '{YOUR_TOS_SECRET_ACCESS_KEY}',
   tos_region = '{YOUR_REGION_ID}'
   ```
   
   
   
   </Tab>
   <Tab zoneid="V7KQDih3Vk" title="Export to AWS S3">
   <TabTitle>Export to AWS S3</TabTitle>
   
   ```SQL
   SELECT * FROM db.table
   INTO OUTFILE 's3://bucket/test_outfile.csv' 
   FORMAT CSV COMPRESSION 'none' 
   SETTINGS
   s3_ak_id = '{YOUR_S3_ACCESS_KEY_ID}',
   s3_ak_secret = '{YOUR_S3_SECRET_ACCESS_KEY}',
   s3_region = '{YOUR_REGION_ID}',
   s3_endpoint='https://s3-{YOUR_REGION_ID}.amazonaws.com',
   s3_use_virtual_hosted_style = 1;
   ```
   
   
   
   </Tab>
   <Tab zoneid="tChfL0OJD4" title="Export to Alibaba Cloud OSS">
   <TabTitle>Export to Alibaba Cloud OSS</TabTitle>
   
   ```SQL
   SELECT * FROM db.table
   INTO OUTFILE 's3://bucket/test_outfile.csv' 
   FORMAT CSV COMPRESSION 'none' 
   SETTINGS
   s3_ak_id = '{YOUR_S3_ACCESS_KEY_ID}',
   s3_ak_secret = '{YOUR_S3_SECRET_ACCESS_KEY}',
   s3_region = '{YOUR_REGION_ID}',
   s3_endpoint='https://oss-{YOUR_REGION_ID}.aliyuncs.com',
   s3_use_virtual_hosted_style = 1;
   ```
   
   
   
   </Tab>
   </Tabs>
   

2. After export completes, check the object storage bucket to verify whether the file exported successfully.


<span id="6cf1e44a"></span>
### Export using ByteHouse CLI


1. Connect to ByteHouse.

   ```Bash
   bytehouse-cli --host tenant-{TENANT_ID}-{REGION}[-{ENVIRONMENT}]-public.bytehouse.bytepluses.com --port 19000 --secure --token XXXXXXXXXXXXX
   ```
   

   
   |Parameter Items |Required |Configuration description |
   |---|---|---|
   |`--host` |is |The access address and port of the cluster. You can view the network group configuration in the ByteHouse console under **Tenant management** \> **Basic information** \> **Network information**. For details, see [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486). |
   |`--port` |is |The port of the cluster access address. The default port is 19000. For ports used by other recommended connection methods, see [Cluster connection port](https://docs.byteplus.com/docs/bytehouse/docs-supported-regions-and-providers#18dc0302). |
   |`--token` |Yes |The cluster access key, configured as API Key. You can log in to the ByteHouse Console, go to the **Tenant management** \> **Connection information** page, then click the **API Key** form's "**New**" button to create an API Key.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">API Key <strong>cannot be viewed again after creation</strong>; it is recommended to download and save the key locally.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">You can create up to two API Keys.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The key must be refreshed within 90 days to ensure security.</div><br> |
   |`--secure` |Depends on the situation |Defines whether to use a Secure TCP connection. If connecting to ByteHouse hosted by BytePlus, `--secure` is a required field. Default is true. |
   |Other |No |Refer to [Connect to ByteHouse](https://docs.byteplus.com/docs/bytehouse/docs-gateway-client#430f8deb)for more optional parameter configurations. |
   

2. Run the following command in the terminal using ByteHouse CLI to export data. Refer to [Parameter description](https://docs.byteplus.com/docs/bytehouse/docs-exporting-data-from-bytehouse#772797f5) for parameter configuration.

   
   <Tabs>
   <Tab zoneid="BGf9C2uYhp" title="Export to TOS">
   <TabTitle>Export to TOS</TabTitle>
   
   ```SQL
   SELECT * FROM db.table
   INTO OUTFILE 'vetos://my-testing/data/data-export-test.csv' 
   FORMAT CSV COMPRESSION 'none'
   SETTINGS 
   tos_access_key = '{YOUR_TOS_ACCESS_KEY}', 
   tos_secret_key = '{YOUR_TOS_SECRET_ACCESS_KEY}',
   tos_region = '{YOUR_REGION_ID}'
   ```
   
   
   
   </Tab>
   <Tab zoneid="isNLFeekVv" title="Export to AWS S3">
   <TabTitle>Export to AWS S3</TabTitle>
   
   ```SQL
   SELECT * FROM db.table
   INTO OUTFILE 's3://bucket/test_outfile.csv' 
   FORMAT CSV COMPRESSION 'none' 
   SETTINGS
   s3_ak_id = '{YOUR_S3_ACCESS_KEY_ID}',
   s3_ak_secret = '{YOUR_S3_SECRET_ACCESS_KEY}',
   s3_region = '{YOUR_REGION_ID}',
   s3_endpoint='https://s3-{YOUR_REGION_ID}.amazonaws.com',
   s3_use_virtual_hosted_style = 1;
   ```
   
   
   
   </Tab>
   <Tab zoneid="s4Bv5rraXr" title="Export to Alibaba Cloud OSS">
   <TabTitle>Export to Alibaba Cloud OSS</TabTitle>
   
   ```SQL
   SELECT * FROM db.table
   INTO OUTFILE 's3://bucket/test_outfile.csv' 
   FORMAT CSV COMPRESSION 'none' 
   SETTINGS
   s3_ak_id = '{YOUR_S3_ACCESS_KEY_ID}',
   s3_ak_secret = '{YOUR_S3_SECRET_ACCESS_KEY}',
   s3_region = '{YOUR_REGION_ID}',
   s3_endpoint='https://oss-{YOUR_REGION_ID}.aliyuncs.com',
   s3_use_virtual_hosted_style = 1;
   ```
   
   
   
   </Tab>
   </Tabs>
   

3. Access the storage path to check whether the file exported successfully. If a system error occurs, refer to [FAQ](https://docs.byteplus.com/docs/bytehouse/docs-exporting-data-from-bytehouse#72368630) for troubleshooting.


<span id="bdc5a454"></span>
### Export by IDE tools

You can use third\-party IDE tools, such as DataGrip and DBeaver, to connect to ByteHouse and export data.


1. Connect to ByteHouse using IDE tools. For activity details, see the following documentation:

   
   |Tools |Document link |
   |---|---|
   |DataGrip（TCP） |[DataGrip (TCP)](https://docs.byteplus.com/docs/bytehouse/docs-DataGrip) |
   |DataGrip（ClickHouse） |[DataGrip (ClickHouse)](https://docs.byteplus.com/docs/bytehouse/datagrip-clickhouse) |
   |DataGrip（MySQL） |[DataGrip (MySQL)](https://docs.byteplus.com/docs/bytehouse/datagrip-mysql) |
   |DBeaver（ClickHouse） |[DBeaver (ClickHouse)](https://docs.byteplus.com/docs/bytehouse/dbeaver-clickhouse) |
   |DBeaver（TCP） |[DBeaver (TCP)](https://docs.byteplus.com/docs/bytehouse/docs-DBeaver) |
   |DBeaver（MySQL） |[DBeaver (MySQL)](https://docs.byteplus.com/docs/bytehouse/dbeaver-mysql) |
   |Navicat（MySQL） |[Navicat (MySQL)](https://docs.byteplus.com/docs/bytehouse/navicat-mysql) |
   |TablePlus（MySQL&ClickHouse） |[TablePlus (MySQL&ClickHouse)](https://docs.byteplus.com/docs/bytehouse/tableplus-mysql-clickhouse) |
   

2. Execute query statements to obtain the result set to be exported.

3. Export data through the export button in the IDE tool.

   Using DBeaver as an example, after completing the query, click **Export data** in the query results view. Follow the prompts to set export destination, extraction, format, export path, and then click **Continue** to export data to the specified path.


<span id="72368630"></span>
# FAQ

<span id="54a776de"></span>
## Q1: Export to TOS error InvalidPathAccess Message: Forbidden path to access server

Specify parameter `s3_use_virtual_hosted_style = 1`. TOS only supports virtual hosted style access for buckets, so configure `s3_use_virtual_hosted_style = 1`.

<span id="c4e02f1b"></span>
## Q2: Export to TOS error Invalid tos region: xxx

The ByteHouse engine may not yet support the TOS availability zone used by SQL. You can manually specify the TOS endpoint, as shown in the example below:

```SQL
SELECT * FROM db.table
INTO OUTFILE 'vetos://my-testing/data/data-export-test.txt' 
FORMAT CSV COMPRESSION 'none'
SETTINGS 
tos_access_key = '<YOUR_TOS_ACCESS_KEY>', 
tos_secret_key = '<YOUR_TOS_SECRET_ACCESS_KEY>',
tos_region = '{REGION}'
tos_endpoint = 'http://tos-s3-{REGION}.ibytepluses.com'
```


For more available TOS endpoints, see [Region and Endpoint](https://docs.byteplus.com/en/docs/tos/docs-region-and-endpoint). When filling in the command, use the S3 Endpoint in the table.

<span id="4f8e86fc"></span>
## Q3: Export to TOS error URI is not allowed in config.xml

Starting from ByteHouse engine v2.3.1.xx (released June 2025), some regex restrictions are added to endpoints. Check whether the endpoint meets the following regex requirements:

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Endpoint requires adding the http or https protocol, formatted as http[s]://endpoint, for example <code>http://tos-s3-ap-southeast-1.bytepluses.com</code></div>


```XML
<host_regexp_1>.*[.]bytepluses[.]com</host_regexp_1>
<host_regexp_2>.*[.]ibytepluses[.]com</host_regexp_2>
<host_regexp_3>.*[.]amazonaws[.]com</host_regexp_3>
<host_regexp_4>.*[.]amazonaws[.]com[.]cn</host_regexp_4>
<host_regexp_5>.*[.]googleapis[.]com</host_regexp_5>
<host_regexp_6>.*[.]aliyuncs[.]com</host_regexp_6>
<host_regexp_7>.*[.]azure[.]com</host_regexp_7>
<host_regexp_8>.*[.]tencentcloudapi[.]com</host_regexp_8>
<host_regexp_9>.*[.]myhuaweicloud[.]com</host_regexp_9>
```


<span id="77a93537"></span>
## Q4: Export specified compression error: Syntax error: failed at position 75 ('COMPRESSION')

Follow the syntax order below:

```SQL
SELECT xxx INTO OUTFILE FORMAT xxx COMPRESSION xxx
```
