---
title: "Apache Superset"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/apache-superset"
---

Apache Superset (herewith referred to as Superset) is an open\-source software application for data exploration and visualization, capable of handling petabyte\-level data. This article introduces how to connect Superset with ByteHouse for data analysis.

<span id="2388e30c"></span>
# Introduction


|**Sub\-items** |**Verified Version/Advisories** |
|---|---|
|Superset |[4.1.0](https://github.com/apache/superset/releases/tag/4.1.0) |
|Open Source ClickHouse Superset Connector |[0.8.6](https://pypi.org/project/clickhouse-connect/0.8.6/) |
|ByteHouse clickhouse\-connect support package |[0.8.6+](https://github.com/bytehouse-docs/ecosystem/tree/main/dist/clickhouse-connect) |
|Python |Python3.8 |
|Obtain ByteHouse Enterprise Account |For acquisition methods, refer to [Get cluster connection information](https://docs.byteplus.com/docs/bytehouse/get-cluster-connection-information). |


<span id="41383c69"></span>
# Install and configure Superset

<span id="a7f4559f"></span>
## Step 1 Prerequisites


1. Install Superset. For instructions, please refer to [the official Superset document](https://superset.apache.org/docs/installation/docker-compose/).

2. Install the ByteHouse clickhouse\-connect support package. The complete installation instructions can be viewed in the `official Superset document`. Below is a simple Example of installation operations.

   * Install via `pip`:

      ```Bash
      pip install https://github.com/bytehouse-docs/ecosystem/raw/main/dist/clickhouse-connect/clickhouse-connect-0.8.6+bytehouse.tar.gz
      ```
      

   * Install in `Docker`:

      ```Bash
      git clone https://github.com/apache/superset.git
      cd superset
      git checkout 4.1.0
      echo "https://github.com/bytehouse-docs/ecosystem/raw/main/dist/clickhouse-connect/clickhouse-connect-0.8.6+bytehouse.tar.gz" >> ./docker/requirements-local.txt
      docker compose -f docker-compose-image-tag.yml up
      ```
      


<span id="da68f6e3"></span>
## Step2 Create Connector


1. Log in to Superset. After installation, you can use the default created account to log in to `http://localhost:8088` in the browser to access `Superset`, the default username/password is admin/admin.

2. Create a database connector to connect to ByteHouse.

   1. Click on the **Settings** tab at the top right of the screen and select **Database Connections**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6f5b8a6e43154edca746a1be881b4823~tplv-goo7wpa0wc-image.image) </span>

   2. Click the `+DATABASE` button to create a new database connection.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/49065372804a4d9795feb8b201f00aca~tplv-goo7wpa0wc-image.image) </span>

   3. Select `ClickHouse Connect（SuperSet）` from the dropdown of available databases.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/35081812c9ac4a9c8e45d8265d9c82f8~tplv-goo7wpa0wc-image.image) </span>

   4. As shown below, fill in the connection details and click the `CONNECT` button.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d163641da86844a6ba0e3c2663bc2ced~tplv-goo7wpa0wc-image.image) </span>

      
      |**Parameters** |**Configuration Description** |
      |---|---|
      |**HOST** |Configure as ByteHouse's public Domain Name, which you can obtain in the **basic information** section of the ByteHouse console's Manage Clusters. |
      |**PORT** |Database Port number: 8123 when SSL is turned off, and 8443 when SSL is activated |
      |**DATABASE NAME** |Set as the name of the already created ByteHouse database. |
      |**USERNAME & PASSWORD** |Username and password for logging into the ByteHouse database. |
      |**DISPLAY NAME** |Customize the display name of the connector. |
      |**ADDITIONAL PARAMETERS** |Configuration is: `secure=True&compress=False`. |
      |**SSL** |Activate the SSL toggle.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">ByteHouse requires encryption authentication to protect data security, therefore, you need to activate SSL.</div><br> |
      

   5. After completing the configuration, click CONNECT to complete the connector creation.


<span id="1c6da404"></span>
## Step 3 Verify result

Below, you are provided with a set of test data to test the connection results of Superset to ByteHouse and demonstrate data analysis actions after establishing the connection.


1. Prepare example data. Run the following query in ByteHouse to prepare the example data.

   ```SQL
   CREATE DATABASE test_db on cluster <your_cluster_name>
   
   CREATE TABLE test_db.online_store_sales_local on cluster <your_cluster_name>(
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
   ENGINE = HaMergeTree()
   PARTITION BY toYYYYMM(order_date)
   ORDER BY (order_date, customer_id);
   
   CREATE TABLE test_db.online_store_sales on cluster <your_cluster_name> as test_db.online_store_sales_local
   ENGINE=Distributed(
     'bytehouse_cluster_test',
     'test_db',
     'online_store_sales_local',
     sipHash64(order_id)
   ) ;
   
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

   1. In the upper right corner of the Superset page, click the + button, and select Data\>Create dataset.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b76e10e7abd4e19b59ff1e6e9ea2836~tplv-goo7wpa0wc-image.image) </span>

   2. Select the created DATABASE, SCHEMA, and TABLE from the dropdown, and then click CREATE DATASET AND CREATE CHART to Complete the dataset creation.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bae878b3bfb141418293a8270a504ff3~tplv-goo7wpa0wc-image.image) </span>

3. Create a Superset chart.

   1. From the Charts tab, select the previously created dataset and select Line Chart as the chart type. Continue by clicking the CREATE NEW CHART button.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/97b32c77b1c24c39a1180562cb7fd42c~tplv-goo7wpa0wc-image.image) </span>

   2. Refer to the configuration chart below to obtain the ByteHouse data results graph.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5fcf0797a81c46a384256ef4a074a25c~tplv-goo7wpa0wc-image.image) </span>
