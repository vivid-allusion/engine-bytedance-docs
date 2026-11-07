---
title: "Apache Superset"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-connect-to-bytehouse-using-superset"
---

Apache Superset (hereafter referred to as Superset) is an open\-source software application for data exploration and visualization, capable of handling petabyte\-scale data. This article introduces how to connect Superset to ByteHouse for data analysis.

<span id="7744531f"></span>
# Background information


* As the `ByteHouse Superset Connector` of `bytehouse-sqlalchemy` is currently undergoing maintenance and updates, it is recommended to use the open\-source **`ClickHouse Superset Connector`** to connect to ByteHouse.

* Since ByteHouse does not natively support the open\-source **`ClickHouse Superset Connector`**, you will also need to use the **ByteHouse clickhouse\-connect support package** to modify and support the open\-source connector.


In summary. After installing Superset and connecting to ByteHouse, you will need to use both the open\-source `ClickHouse Superset Connector` and the ByteHouse clickhouse\-connect support package.

<span id="a467470d"></span>
# Cautions


|**Segments** |**Verified versions/Notes** |
|---|---|
|Superset |[4.1.0](https://github.com/apache/superset/releases/tag/4.1.0) |
|Open Source ClickHouse Superset Connector |[0.8.6](https://pypi.org/project/clickhouse-connect/0.8.6/) |
|ByteHouse ClickHouse\-connect support package |[0.8.6+](https://github.com/bytehouse-docs/ecosystem/tree/main/dist/clickhouse-connect) |
|Python |Python3.8 |
|ByteHouse account API Token obtained |For how to obtain an API Token, refer to [Retrieve API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d9bd3430). |


<span id="84a3b519"></span>
# Configure ByteHouse

<span id="a1313cbe"></span>
## Step 1: Configure public domain

After logging into the ByteHouse console, go to the **Tenant Management** section's **Basic Information** page to review the network group configuration, confirm that a VPC is bound, and a public domain name has been attached.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0d62964ae0cd4659aa4ff002f56b2af4~tplv-goo7wpa0wc-image.image) </span>


* If a VPC and public domain name have not been bound, refer to [Network settings](https://docs.byteplus.com/docs/bytehouse/network-settings) to complete the binding configuration.

* Once the binding is complete, you can copy the public domain name for use in subsequent QuickBI parameter configurations.


<span id="14683ae7"></span>
## Step 2: Obtain API key

Access the top **Tenant Management** section's **Connection Information** page, create a new API key in the API Key module, and save the API Key locally for subsequent configuration use.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9c0432f0e6dc4282b0a4927934879372~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">A sub\-account can support the creation of up to two API Keys. If you already have an API Key created previously, you can also directly use the existing one.</div>


<span id="bd208d65"></span>
## Step 3: Set default virtual warehouse

Go to **Tenant Management** \> **Parameter Settings** page. Check whether the default compute group is set, and ensure this virtual warehouse is in a running state and not stopped. After QuickBI is integrated with ByteHouse, operations such as data queries will use the default virtual warehouse configured here.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f40296c222f643cc82b2b4cfc2e7c459~tplv-goo7wpa0wc-image.image) </span>

<span id="ccbe0574"></span>
# Configure Superset

<span id="692d96f9"></span>
## Step 1: Preparation


1. Install Superset. For operating instructions, please refer to the [Superset official documentation](https://superset.apache.org/docs/installation/docker-compose/).

2. Install the ByteHouse clickhouse\-connect support package. Complete installation instructions can be found in the `Superset` official documentation; below is a simple installation procedure example.

   * Install via `pip`:

      ```Plain
      pip install https://github.com/bytehouse-docs/ecosystem/raw/main/dist/clickhouse-connect/clickhouse-connect-0.8.6+bytehouse.tar.gz
      ```
      

   * Install in `Docker`:

      ```Plain
      git clone https://github.com/apache/superset.git
      cd superset
      git checkout 4.1.0
      echo "https://github.com/bytehouse-docs/ecosystem/raw/main/dist/clickhouse-connect/clickhouse-connect-0.8.6+bytehouse.tar.gz" >> ./docker/requirements-local.txt
      docker compose -f docker-compose-image-tag.yml up
      ```
      


<span id="4921b73f"></span>
## Step 2: Create a connector


1. Log in to Superset. After installation, you can access `http://localhost:8088` in your browser to log into `Superset`, with the default username/password being admin/admin.

2. Create a database connector and connect to ByteHouse.

   1. Click the **Settings** tab at the top right of the screen and select **Database Connections**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a7f44a0e83674e2493cbd463f5fbb0f0~tplv-goo7wpa0wc-image.image) </span>

   2. Click the `+DATABASE` button to create a new database connection.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dc655b1c75b3450bab3119a026247de0~tplv-goo7wpa0wc-image.image) </span>

   3. Select `ClickHouse Connect (SuperSet)` from the dropdown menu of available databases.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/496ec0a3eae34fbeb272df5a9b5b6a6b~tplv-goo7wpa0wc-image.image) </span>

   4. As shown below, fill in the connection details and click the `CONNECT` button.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ed0348f69d0345feaf1cd5331c0beb0c~tplv-goo7wpa0wc-image.image) </span>

      
      |**Parameter** |**Configuration Description** |
      |---|---|
      |**HOST** |The configuration for ByteHouse's public domain name follows the format: `tenant-{TENANT_ID}-{REGION}-public.bytehouse.bytepluses.com`. You can obtain this information in ByteHouse's control panel under **Tenant management** \> **Basic information** \> **Network information**. |
      |**PORT** |The database port number is configured as a fixed value: 8123. |
      |**DATABASE NAME** |Configured as the database name already created by ByteHouse. |
      |**USERNAME & PASSWORD** |Username and password for logging into the ByteHouse database.<br><br><br>* Default username is `bytehouse`.<br><br>* Password is <API_Key\>, and can be obtained from the **Tenant management** \> **Connection information** section in the ByteHouse console by using the API Key. |
      |**DISPLAY NAME** |Custom connector display name. |
      |**ADDITIONAL PARAMETERS** |Configured as: `secure=True&compress=False`. |
      |**SSL** |Turn on the SSL switch.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">ByteHouse requires encrypted authentication to ensure data security, therefore, you need to enable SSL.</div><br> |
      

   5. (Optional) If you have multiple compute groups and want to use a specific compute group for subsequent Superset queries to ByteHouse, you can specify it in **ADDITIONAL PARAMETERS**.

      
      |ADDITIONAL PARAMETERS |secure=True&compress=False&**<ins>virtual_warehouse=vw\-accountId\-vwName</ins>** |
      |---|---|
      

   6. After completing the configuration, click CONNECT to finalize the connector creation.


<span id="0e3acfe8"></span>
## Step 3: Verify results

Below is a sample dataset for you to test the Superset connection to ByteHouse, along with examples of data analytics operations using Superset after the connection.


1. Prepare the sample data. Execute the following query in ByteHouse to prepare the sample data.

   ```SQL
   CREATE DATABASE test_db;
   
   CREATE TABLE test_db.online_store_sales (
       order_id String,
       order_date DateTime,
       customer_id String,
       product_id String,
       category String,
       sub_category String,
       region String,
       sales_amount Float64,
       quantity UInt32
   ) 
   ENGINE = CnchMergeTree()
   PARTITION BY toYYYYMM(order_date)
   ORDER BY (order_date, customer_id);
   
   INSERT INTO test_db.online_store_sales VALUES
   ('OID001', '2024-11-01 10:00:00', 'CID001', 'PID001', 'Electronics', 'Smartphones', 'North America', 899.99, 2),
   ('OID004', '2024-11-02 09:20:00', 'CID004', 'PID004', 'Furniture', 'Desks', 'North America', 1599.99, 5),
   ('OID005', '2024-11-02 14:10:00', 'CID005', 'PID005', 'Home Decor', 'Lamps', 'South America', 49.99, 100),
   ('OID006', '2024-11-02 17:50:00', 'CID006', 'PID006', 'Electronics', 'Tablets', 'Europe', 799.99, 7),
   ('OID007', '2024-11-03 11:00:00', 'CID007', 'PID007', 'Clothing', 'Jackets', 'Asia', 149.99, 25),
   ('OID008', '2024-11-03 13:40:00', 'CID008', 'PID008', 'Clothing', 'Shoes', 'Africa', 89.99, 50),
   ('OID010', '2024-11-04 19:30:00', 'CID010', 'PID010', 'Electronics', 'Cameras', 'North America', 399.99, 3),
   ('OID013', '2024-11-05 08:50:00', 'CID013', 'PID013', 'Electronics', 'Headphones', 'North America', 99.99, 100),
   ('OID014', '2024-11-05 11:30:00', 'CID014', 'PID014', 'Furniture', 'Coffee Tables', 'Asia', 499.99, 50),
   ('OID015', '2024-11-05 14:00:00', 'CID015', 'PID015', 'Clothing', 'T-Shirts', 'Europe', 19.99, 300),
   ('OID016', '2024-11-06 09:40:00', 'CID016', 'PID016', 'Furniture', 'Bookshelves', 'North America', 999.99, 10),
   ('OID017', '2024-11-06 13:25:00', 'CID017', 'PID017', 'Electronics', 'Laptops', 'Europe', 2299.99, 4),
   ('OID020', '2024-11-07 14:00:00', 'CID020', 'PID020', 'Home Decor', 'Rugs', 'Africa', 199.99, 20);
   ```
   

2. Create a dataset in Superset.

   1. Click the + button at the top right corner of the Superset page, and select Data \> Create dataset.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1c94b7f270634e9e93d9be5669abe05c~tplv-goo7wpa0wc-image.image) </span>

   2. Select the created DATABASE, SCHEMA, and TABLE from the dropdown menu, then click the CREATE DATASET AND CREATE CHART button to complete the dataset creation.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a1a88d8b89844b64b8da37c81f9a3df8~tplv-goo7wpa0wc-image.image) </span>

3. Create a Superset chart.

   1. From the Charts tab, select the previously created dataset and choose Line Chart as the chart type. Continue by clicking the CREATE NEW CHART button.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5d303a1c604243228d1df4ac41c465e6~tplv-goo7wpa0wc-image.image) </span>

   2. Refer to the diagram below to configure the chart parameters to obtain the queried ByteHouse data result graph.

      
      |Chart Parameters |Configuration Result Illustrations |
      |---|---|
      |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f00bdcfd167a474d9b3edf59c704d279~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06bebdeea4ee4c859211fdb8bc72ef87~tplv-goo7wpa0wc-image.image) </span> |
