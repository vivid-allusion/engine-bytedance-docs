---
title: "Manage external catalog"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/manage-external-catalog"
---

ByteHouse supports creating external catalogs, including Hive, Iceberg, Paimon, and MySQL. It supports displaying and managing external data catalogs, adding and deleting catalogs, viewing database and table information within catalogs, and configuring catalog resources and data permissions. This article introduces how to create and manage external catalogs, and to grant users relevant data and resource permissions.

<span id="c57ddcff"></span>
# Function overview

ByteHouse external catalog is used to manage the information and resources of external data sources you created. The system currently supports creating and managing four types of data sources: Hive, Iceberg, Paimon, and MySQL. This is suitable for scenarios that require unified query and management of data stored in various external data sources, such as Hive, Iceberg, Paimon, and MySQL, without the need for data migration. Description of metadata storage types supported by different data sources as follows:


|Datasource |Supported metadata storage types |
|---|---|
|Hive |Hive, BytePlus AI Data Lake Service (LAS) |
|Iceberg |Hadoop, BytePlus AI Data Lake Service (LAS) |
|Paimon |Filesystem |
|MySQL |Not applicable |


Through the external catalog, you can directly access and manage these external data sources. The specific feature details are as follows:


|Function |Introduction |
|---|---|
|Catalog management |Supports adding, deleting, and showing external catalogs, and viewing information about databases, tables, and other information within a catalog. |
|Manage Catalog data permissions |Grant users CREATE, SHOW, DROP, and other Data management permission. |
|Manage permissions for Catalog resources |Grant the user the privilege to create a new external catalog. |


After adding a new external catalog, all ByteHouse internal catalogs are migrated to the default folder.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e1e0c2ba7cbd45b7bc159e6acb782907~tplv-goo7wpa0wc-image.image) </span>

<span id="456e8832"></span>
# Prerequisites

Before using an external catalog, obtain the following information according to the metadata storage type used by your catalog. To add a MySQL catalog, only MySQL\-related information is required; there is no need to pay attention to other information in the table below.


|Prerequisites |Description |
|---|---|
|Get metadata storage service address or storage service address |To obtain the following information for Hive, Hadoop, or Filesystem metadata storage types:<br><br><br>* Metadata storage service URL/Storage service URL:<br><br>   * Hive: Hive Thrift server address.<br><br>   * Hadoop, Filesystem: Storage service address.<br><br>* Service endpoints:<br><br>   * Hive: The interface address of the S3\-compatible storage service used by Hive.<br><br>   * Hadoop, Filesystem: Access the endpoint of the object storage used by Hadoop and Filesystem.<br><br>* Access Key ID (AK)/Secret Access Key (SK): The access key for the metadata storage service or the storage service. |
|Get LAS information |If your metadata storage type is LAS, you need to obtain the following information:<br><br><br>* Service endpoint: Defines the TOS service endpoint used by LAS.<br><br>* LAS access keys: Access Key ID (AK) / Secret Access Key (SK)<br><br>* LAS Catalog name.<br><br>* LAS storage region: The region where the physical data center of the TOS storage service used by LAS is located.<br><br>* LAS metadata storage service address: The metadata storage service address of LAS. |
|Get MySQL information |To obtain the following information for a Catalog of type MySQL:<br><br><br>* IP address<br><br>* Port number<br><br>* Username and password |


<span id="e5f85708"></span>
# Limitations


* This feature is in Beta. To enable it, please submit a ticket or contact the ByteHouse team to request allowlist access.

* Iceberg, Paimon, and MySQL Catalogs require the ByteHouse engine version to be 2.3.2.0 or higher. Before use, confirm that your engine version meets this requirement. You can check your current engine version on the **Tenant management** \> **Basic information** page in the ByteHouse console. If your engine version does not meet the requirement, you can submit a ticket to contact the ByteHouse team and request an engine upgrade.


<span id="9a53257b"></span>
# Create an external catalog


1. Log in to the ByteHouse Cloud Data Warehouse Console, under the **Database** tab at the top, click  **+ New**. Then, click **Create external catalog**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1eddbae07ab14b46b8fe57b998053047~tplv-goo7wpa0wc-image.image) </span>

2. Select the external Catalog type and the metadata storage type, and configure the external Catalog information.

   * For Hive, Iceberg, and Paimon catalog types, you can view the corresponding configuration information based on the metadata storage type.

   * MySQL Catalog does not require configuration of a metadata storage service. You can view the connection information that needs to be configured.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f08214497de841cfb8591105d9db5c94~tplv-goo7wpa0wc-image.image) </span>

      **Parameter configuration information when the metadata storage type is Hive**, **Hadoop**, **or Filesystem**:

      For catalogs whose metadata storage types are Hive, Hadoop, or Filesystem, the parameter types required for configuration are the same, but the methods for obtaining them differ. For details, see the following parameter configuration description.

   
   |Param |Hive |Hadoop |Filesystem |
   |---|---|---|---|
   |Metadata storage service address / Storage service address |The connection address of the Hive Metastore service. Hive Metastore is a service that stores Hive table metadata, such as table structure and partition information. The format for filling in and examples are as follows:<br><br><br>* Format: `thrift://hive_thrift_server_ip:port`, where `<hive_thrift_server_ip>` is the IP address of the Hive Thrift server and `<port>` is the port number. You can refer to the official documentation for your Hive service to obtain connection details.<br><br>* Example:`thrift:// 101.1 xx.xx. xxx:9 083` |Enter the connection address of the storage service used by Hadoop. You must provide the actual storage path, and you can use S3 or HDFS service addresses. Format and examples are as follows:<br><br><br>* Format:<br><br>   * S3: `s3://<bucket_name>/<path_to_metadata>`. For BytePlus TOS, use the `tos://<bucket_name>/<path_to_metadata>` format.<br><br>      * `<bucket_name>` is the name of the bucket;<br><br>      * `<path_to_metadata>` is the path of metadata in the bucket.<br><br>   * HDFS: `hdfs://<namenode_host>:<port>/<path_to_metadata>`,<br><br>      * `<namenode_host>` is the hostname or IP address of the namenode in the Hadoop cluster;<br><br>      * `<port>` is the port number.<br><br>      * `<path_to_metadata>` is the specific path in HDFS for storing metadata.<br><br>* Example:<br><br>   * `s3://bytehouse-test/iceberg`<br><br>   * `tos://test-catalog/iceberg`<br><br>   * `hdfs://haruna/home/bytehouse_test/table_store/bytehouse_test` |Enter the actual storage path as the connection address for the storage service used by the filesystem. S3 or HDFS service addresses are supported. Format and examples are as follows:<br><br><br>* Format:<br><br>   * S3: `s3://<bucket_name>/<path_to_metadata>`. If you are using BytePlus TOS, you can use the `tos://<bucket_name>/<path_to_metadata>` format.<br><br>      * `<bucket_name>` is the bucket name;<br><br>      * `<path_to_metadata>` is the path to the metadata in the bucket.<br><br>   * HDFS: `hdfs://<namenode_host>:<port>/<path_to_metadata>`,<br><br>      * `<namenode_host>` is the hostname or IP address of the Hadoop cluster's namenode.<br><br>      * `<port>` is the port number;<br><br>      * `<path_to_metadata>` is the specific path in HDFS for storing metadata.<br><br>* Example:<br><br>   * `s3://test-catalog/paimon`<br><br>   * `tos://test-catalog/paimon`<br><br>   * `hdfs://haruna/home/bytehouse_test/table_store/bytehouse_test` |
   |Service endpoint |Configure as the endpoint for the S3\-compatible storage service. If you are using BytePlus TOS, refer to the list of available service endpoints in the S3 Endpoint column in the [Region and Endpoint](https://docs.byteplus.com/en/docs/tos/docs-region-and-endpoint) table. |||
   |Access Key (AK) |The Access Key ID of the S3\-compatible storage service. For information on how to obtain it, refer to the key management documentation of the corresponding service. If you are using BytePlus TOS, refer to [Creating an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey) for instructions on how to obtain an Access Key. |||
   |Secret access key (SK) |Secret Access Key of the S3\-compatible storage service. For instructions on how to obtain it, refer to the key management documentation of the corresponding service. To obtain an Access Key when using BytePlus TOS, refer to [Creating an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey). |||
   |Catalog name |Customize the Catalog name: naming rules are as follows.<br><br><br>* A name can only contain letters, numbers, and the underscore "_".<br><br>* Length must be 1 to 64 characters. |||
   

   **Parameter configuration information when the metadata storage type is LAS**:

   
   |Param |Configuration description |
   |---|---|
   |Service endpoint |Define the TOS Service endpoint used by LAS. For a list of available service endpoints, refer to the information in the S3 Endpoint column in [Region and Endpoint](https://docs.byteplus.com/en/docs/tos/docs-region-and-endpoint). |
   |TOS access key (AK) |Configure as the access key for TOS. For information on how to obtain an AccessKey, please refer to [Creating an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey). |
   |TOS access key (SK) |Configure as the secret key for TOS. For information on how to obtain an AccessKey, see [Creating an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey). |
   |LAS access key (AK) |LAS access key. To learn how to obtain an AccessKey, see [Creating an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey). |
   |LAS secret access key (SK) |Secret key configured for LAS. For information on how to obtain an AccessKey, see [Creating an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey). |
   |LAS catalog name |Please enter here the name of the catalog that you wish to connect to, which already exists in LAS. This allows ByteHouse to locate the correct external data catalog. Log in to the LAS Console, and in the left navigation pane, click **Database** \> **Metadata Management** to view the Catalog name. |
   |LAS region |The region where the physical data center of the TOS storage service used by LAS is located. For available region names, see [Region and Endpoint](https://docs.byteplus.com/en/docs/tos/docs-region-and-endpoint). |
   |LAS metadata storage service URL |Configure the LAS metadata storage service address. You can fill in `thrift://lakeformation.las.{REGION}. ivolces.com:48869` or `thrift://lf_thrift_server_ip:port`. For information on how to obtain the address, see [Configure external tables](https://docs.byteplus.com/docs/bytehouse/best-practice-integrate-las-catalog-data#7f0a0a6d). |
   |Catalog name |Naming rules for custom catalog names:<br><br><br>* The name can only contain letters, numbers, and the underscore "_".<br><br>* The length is 1 to 64 characters. |
   

   **MySQL Catalog configuration information**:

   
   |Param |Configuration description |
   |---|---|
   |Connection address |The connection address of the MySQL service. The format is `ip:port`.<br><br><br>* `ip` is the IP address of the MySQL server, and you can refer to the official documentation for your MySQL service to obtain the IP address.<br><br>* `port` is the port number of the MySQL service. You can refer to the official documentation of the MySQL service you use to obtain the port number. |
   |Username |You can refer to the official documentation of the MySQL service you use to obtain the username. |
   |Password |You can obtain the password for your MySQL service by referring to its official documentation. |
   |Catalog name |Customize the Catalog name. The naming rules are as follows:<br><br><br>* The name can only contain letters, numbers, and the underscore "_".<br><br>* Length is 1 to 64 characters. |
   

3. Click **Create**.


<span id="19e9376d"></span>
# View external catalog

In the left navigation bar under the **Database** tab, you can view the newly created Catalog. Through the External Catalog, you can view databases, tables, DDL, data preview, and other information.


* View databases

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f4d2cd734a9f44ee844789cbc72ca109~tplv-goo7wpa0wc-image.image) </span>

* View a table

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e3012f8192bb45b5aad8780a321e0f2a~tplv-goo7wpa0wc-image.image) </span>

* View table data

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/477b99a0c24f4078a1bf0359e8455e03~tplv-goo7wpa0wc-image.image) </span>


<span id="2a25c0b4"></span>
# Delete external catalog

Click on the catalog folder to enter the external catalog detail page, click  **`...`** , click **Delete catalog**, and click **Delete** to delete the catalog.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2361d93e8cdc457bb93cccedded4fb3d~tplv-goo7wpa0wc-image.image) </span>

<span id="0a8f5a74"></span>
# Manage external catalog privileges

You can manage privileges for the external Catalog by granting roles to users or directly assigning data and resource permissions. For more details on operations, see the following documents:


* [Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management)

* [Role management](https://docs.byteplus.com/docs/bytehouse/docs-access-control-administration)

* [Data privilege management](https://docs.byteplus.com/docs/bytehouse/docs-permission)

* [Resource privilege management](https://docs.byteplus.com/docs/bytehouse/resource-privilege-management)
