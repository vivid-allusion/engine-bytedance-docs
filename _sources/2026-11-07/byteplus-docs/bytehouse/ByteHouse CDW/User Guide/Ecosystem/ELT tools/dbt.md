---
title: "dbt"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-connecting-to-bytehouse-using-dbt"
---

dbt (Data Building Tool) generates data models from business data, storing them in databases in the form of views or tables for easy data querying and analysis. The ByteHouse DBT connector (dbt\-bytehouse) achieves compatibility between DBT and ByteHouse, helping you build your own data models. This article introduces the features and usage of DBT and dbt\-bytehouse.

<span id="eee2ffc8"></span>
# Feature overview

dbt is an open\-source tool focused on data transformation (the T component of ELT), which abstracts select statements written by data analysts and engineers into data models. It describes the data's structure, relations, and transformation rules through SQL logic, and persists the data models into the database through materialization, storing them as views, tables, etc.

The current dbt\-bytehouse offers three types of materialization and also supports snapshot and seed functionalities, as described below:


|Function |Introduction |
|---|---|
|View Materialization |Logical definition, no data storage, dynamically computed on each query. Saves storage but has lower query performance, suitable for lightweight and infrequently used models. |
|Table Materialization |Data is persisted as physical tables which lead to quicker queries but occupy storage, suitable for high\-frequency queries or results needing precomputation (such as aggregate indicators). |
|Incremental materialization |Processes only new or changed data, significantly reducing computation, suitable for big data scenarios. Strategies are divided into:<br><br><br>* `append`: The incremental materialization using the `append` strategy does not create any temporary tables and directly inserts new records into existing tables.<br><br>* `insert_overwrite`: Data is overwritten by partition (e.g., by day), replacing all content in a specific partition to ensure data is up\-to\-date (suitable for time\-partitioned tables).<br><br><br>Incremental materialization currently does not support `merge` or `delete+insert` strategies. |
|Seed |Module used for loading data files such as CSV, a way to load files into the database for model building, commonly used for initializing business configurations, dimension tables, or reference data. |
|Snapshot |dbt uses mechanisms to track changes in data over time, recording the "historical versions" of data, capturing field changes in records from the source table (such as status updates, numerical changes), and retaining all historical states and their valid time ranges in the snapshot table. |


<span id="68bfa221"></span>
# Prerequisites


* Please ensure Python 3.10 is installed; see the installation guide at [Python 3.10.0](https://www.python.org/downloads/release/python-3100/).

* Please make sure `pip` is installed. For installation instructions, see [pip install](https://pip.pypa.io/en/stable/cli/pip_install/).


<span id="d4b70326"></span>
# Install dbt and ByteHouse dbt adapter


1. Install dbt.

   ```Bash
   pip install dbt-core==1.8.9
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">It is recommended to install dbt Core v1.8.x. For detailed installation instructions, refer to <a href="https://docs.getdbt.com/docs/core/installation-overview">dbt Core Introduction and Installation Documentation</a>.   </div>
   

2. Install the ByteHouse dbt adapter dbt\-bytehouse.

   ```Bash
   pip install dbt-bytehouse==1.8.9
   ```
   

3. Check if the installation was successful.

   ```Bash
   dbt --version
   ```
   

   The output result of a successful installation is as follows:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a115a713f614bc3977b4035130677d1~tplv-goo7wpa0wc-image.image) </span>


<span id="2e042fcc"></span>
# Project initialization

This section explains how to create a new dbt project, setup a virtual environment, initialize the dbt project, and connect dbt with ByteHouse.


1. Create a new dbt project named `bytehouse_demo_project` and open the project.

   ```Bash
   mkdir bytehouse_demo_project
   cd bytehouse_demo_project
   ```
   

2. Create a virtual environment using Python 3.10.

   ```Bash
   python3.10 -m venv venv
   source venv/bin/activate
   ```
   

3. Initialize the dbt project.

   `dbt init` command initializes the created dbt project, creating a new folder containing the project name, sample files in models/example, and the configuration file dbt_project.yml.

   During initialization, the `dbt init` command prompts you to enter project name and database, at which point you should select `clickhouse`.

   ```Bash
   dbt init bytehouse_demo_project
   ```
   

4. Switch to the directory where the project is located.

   ```Bash
   cd bytehouse_demo_project
   ```
   

5. Remove the sample files created by dbt.

   ```Bash
   rm -rf models/example
   ```
   

6. Create a profiles.yml file in the `dbt` directory to configure details for dbt's connection to ByteHouse.

   ```YAML
   dbt_bytehouse_profile:
     target: <target-name>
     outputs:
       <target-name>:
         type: clickhouse
         schema: <database-name>
   
         driver: http
         host: <bytehouse-host>
         port: 8123
         user: bytehouse
         password: <bytehouse-api-key>
         secure: True
         verify: False
         
         custom_settings:
             <setting-key>: <settings-value>
   ```
   

   The explanation of parameters in the sample file is as follows. For more parameter information, please see the [dbt official documentation](https://pypi.org/project/dbt-bytehouse/1.8.9/#description).

   
   |Parameter |Configuration |
   |---|---|
   |dbt_bytehouse_profile |The configuration file name used in a dbt project configuration. You can customize this name as needed. |
   |`target` |Defines the target environment for the dbt project output. |
   |`outputs` |Define the output information for the dbt project, allowing for multiple output environments to be configured in the same profiles.yml file by setting information under `outputs`. The following example showcases defining output information for dev and prod, with the target environment specified through `target` as prod:<br><br>```YAML```<br>```dbt_bytehouse_profile:```<br>```  target: <prod>```<br>```  outputs:```<br>```    <dev>:```<br>```      ...```<br>```      host: <host-for-dev>```<br>```      ...```<br>```    <prod>:```<br>```      ...```<br>```      host: <host-for-prod>```<br>```      ...```<br> |
   |`type` |The dbt adapter type to use should be set to the fixed value: `clickhouse`. |
   |`schema` |The default schema used for creating objects should be configured to the database name already created by ByteHouse. |
   |`driver` |Communication protocol, which should be set to the fixed value: `http`. |
   |`host` |Configure as the public domain name of the ByteHouse server, in the format: `tenant-{TENANT_ID}-{REGION}-public.bytehouse.bytepluses.com`. You can obtain this from the Tenant Management \> Basic Information \> Network Information section in the ByteHouse console. |
   |`port` |The port number to be connected on the ByteHouse server, the HTTP protocol must be set to a fixed value: 8123. |
   |`user` |The username for logging into the ByteHouse database should be set to a fixed value `bytehouse`. |
   |`password` |The password for logging into the ByteHouse database is `<API_Key>`, which can be obtained from **ByteHouse Console**\>**Tenant Management**\>**Connection Information**. For detailed acquisition methods, please refer to [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311). |
   |`secure` |Boolean flag (true/false), indicating whether to use a secure connection (HTTPS). Must be set to `True`. |
   |`verify` |It needs to be set to `false`. |
   |`custom_settings` |Additional ByteHouse connection settings need to be passed to the connector. You can set parameters such as compute group and maximum execution time. Here's an example:<br><br>```YAML```<br>```custom_settings:```<br>```    virtual_warehouse: {VIRTUAL_WAREHOUSE_ID}```<br>```    max_execution_time: 3600```<br><br><br>The compute group ID can be obtained through the **ByteHouse Console** \> **Tenant Management** \> **Parameter Settings** \> **Default Compute Group**. |
   

7. Using a text editor, open the `bytehouse_demo_project` project directory and update the dbt_project.yml file within that project, ensuring that the `profile` parameter value matches the name you configured in the dbt/profiles.yaml in step 6.

   For example, if the dbt/profiles.yaml file in the system is configured with the name `dbt_bytehouse_profile`, then the dbt_project.yaml file in the project should maintain the `profile` value consistently.

   The configuration of the dbt/profiles.yaml file in the system is shown below, with the name highlighted in a box:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/835ad86d32ce4a988979925fec2e1eef~tplv-goo7wpa0wc-image.image) </span>

   The configuration example of the `dbt_projet.yaml` file in the project is as follows, the framed part is the `profile` parameter value that needs to be updated

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d874b9a6b67d436ab51ecfa7dfedf326~tplv-goo7wpa0wc-image.image) </span>

8. Test if dbt successfully connects to ByteHouse. If the connection is successful, the output result will display "All checks passed!"

   ```Bash
   dbt debug
   ```
   

   The output result example of a successful connection is as follows:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bae66a64b9ec459d82199758c366f251~tplv-goo7wpa0wc-image.image) </span>


<span id="d75f5ba0"></span>
# Usage example

<span id="1f939708"></span>
## Prepare the ByteHouse Dataset

Prepare tables and data examples in ByteHouse for testing the dbt project. You can execute the following SQL command in the [ByteHouse console](https://console.byteplus.com/bytehouse/region:bytehouse+ap-southeast-1/query):

```SQL
DROP DATABASE IF EXISTS bytehouse_demo;
CREATE DATABASE bytehouse_demo;

CREATE TABLE bytehouse_demo.customers (
    id UInt64,
    name String,
    email String,
    updated_at DateTime
) 
ENGINE = CnchMergeTree
PRIMARY KEY id
ORDER BY (id, updated_at)
PARTITION BY updated_at;

INSERT INTO bytehouse_demo.customers (id, name, email, updated_at) VALUES
    (1, 'John Smith', 'john.smith@example.com', '2023-01-15 08:30:00'),
    (2, 'Jane Doe', 'jane.doe@example.com', '2023-01-16 10:45:00'),
    (3, 'Robert Johnson', 'robert.j@example.com', '2023-01-16 14:20:00'),
    (4, 'Sarah Williams', 'sarah.w@example.com', '2023-01-17 09:15:00'),
    (5, 'Michael Brown', 'michael.b@example.com', '2023-01-18 11:30:00');
```


<span id="31c5d95c"></span>
## Create dbt source

Create a schema.yml file in the dbt project models folder, define the `customers` table as a dbt source:

```YAML
version: 2

sources:
  - name: customers_source
    schema: bytehouse_demo
    tables:
      - name: customers
```


<span id="64af00c8"></span>
## Create materialized view

<span id="e65f17fd"></span>
### Usage example

Create a customers_summary_view.sql file in the dbt project models folder to materialize the view:

```SQL
{{
  config(
    materialized = 'view'
  )
}}

SELECT
  id,
  name,
  email,
  updated_at
FROM {{ source('customers_source', 'customers') }}
```


The parameter description is as follows:


|Parameter |Configuration description |
|---|---|
|`materialized` |The materialized form of the table. |


<span id="e79c83b2"></span>
### How it works

dbt\-bytehouse internally executes the following SQL command to create the view.

```SQL
CREATE OR REPLACE VIEW `ecosystem`.`customers_summary_view` AS (
  SELECT
    id,
    name,
    email,
    updated_at
  FROM `bytehouse_demo`.`customers`
);
```


<span id="dd82d3ca"></span>
## Create materialized table

<span id="e018442d"></span>
### Usage example

Create a customers_summary_table.sql file in the dbt project models folder to materialize the table:

```SQL
{{
  config(
    materialized = 'table'
  )
}}

SELECT
  id,
  name,
  email,
  updated_at
FROM {{ source('customers_source', 'customers') }}
```


The parameter description is as follows:


|Parameters |Configuration instructions |
|---|---|
|`materialized` |The materialized form of the table. |


<span id="1003db4d"></span>
### How it works


1. dbt\-bytehouse will execute the following SQL commands to create a table.

   ```SQL
   CREATE TABLE `bytehouse_demo`.`customers_summary_table`
   ENGINE = CnchMergeTree()
   ORDER BY (tuple())
   AS (
    SELECT
      id,
      name,
      email,
      updated_at
    FROM `bytehouse_demo`.`customers`
   );
   ```
   

2. If the table already exists, dbt\-bytehouse will perform subsequent operations and execute a complete set of SQL queries.

   ```SQL
   -- 1. Create a temporary table using a model declaration, which will be used to replace the existing table
   CREATE TABLE `bytehouse_demo`.`customers_summary_table__dbt_tmp`
   ENGINE = CnchMergeTree()
   ORDER BY (tuple())
   AS (
    SELECT
      id,
      name,
      email,
      updated_at
    FROM `bytehouse_demo`.`customers`
   );
   
   -- 2. If the backup table exists, delete the backup table
   DROP TABLE IF EXISTS `bytehouse_demo`.`customers_summary_table__dbt_backup`;
   
   -- 3. Rename the existing table to backup table
   RENAME TABLE `bytehouse_demo`.`customers_summary_table` TO `bytehouse_demo`.`customers_summary_table__dbt_backup`;
   
   -- 4. Delete the existing table
   DROP TABLE IF EXISTS `bytehouse_demo`.`customers_summary_table`;
   
   -- 5. Rename the temporary table to the required table name
   RENAME TABLE `bytehouse_demo`.`customers_summary_table__dbt_tmp` TO `bytehouse_demo`.`customers_summary_table`;
   
   -- 6. Delete the backup table
   DROP TABLE IF EXISTS `bytehouse_demo`.`customers_summary_table__dbt_backup`;
   ```
   


<span id="b73c3547"></span>
## Create incremental materialization

<span id="06534ecc"></span>
### Usage example

Create a file named customers_summary_incremental.sql in the models folder of the dbt project to create incremental materialization. Here, you need to provide the dbt `unique_key` and `is_incremental` clauses.

```SQL
{{
  config(
    materialized='incremental',
    unique_key='id'
  )
}}

SELECT
  id,
  name,
  email,
  updated_at
FROM {{ source('customers_source', 'customers') }}
{% if is_incremental() %}
  WHERE updated_at > (SELECT max(updated_at) FROM {{ this }})
{% endif %}
```


Parameter description is as follows:


|Parameter |Configuration Instructions |
|---|---|
|`materialized` |The materialized form of the table. |
|`unique_key` |The unique_key value of the unique key table. |


<span id="da2034de"></span>
### How it works


1. dbt\-bytehouse will execute the following SQL commands to create an incremental table:

   ```SQL
   CREATE TABLE `bytehouse_demo`.`customers_summary_incremental` 
   ENGINE = CnchMergeTree() 
   ORDER BY (tuple()) 
   AS (
     SELECT 
       id, 
       name, 
       email, 
       updated_at 
     FROM `bytehouse_demo`.`customers`
   );
   ```
   

2. Assuming the table already exists, dbt\-bytehouse will continue to execute the following queries:

   ```SQL
   -- 1. Create the intermediate table __dbt_new_data containing updated/new data
   DROP TABLE IF EXISTS `bytehouse_demo`.`customers_summary_incremental__dbt_new_data`;
   
   CREATE TABLE `bytehouse_demo`.`customers_summary_incremental__dbt_new_data`
   ENGINE = CnchMergeTree()
   ORDER BY (tuple())
   AS (
     SELECT
       id,
       name,
       email,
       updated_at
     FROM `bytehouse_demo`.`customers`
     WHERE updated_at > (
       SELECT max(updated_at) 
       FROM `bytehouse_demo`.`customers_summary_incremental`
     )
   );
   
   -- 2. Create the temporary table __dbt_tmp containing data yet to be updated/new
   CREATE TABLE `bytehouse_demo`.`customers_summary_incremental__dbt_tmp`
   AS `bytehouse_demo`.`customers_summary_incremental__dbt_new_data`;
   
   INSERT INTO `bytehouse_demo`.`customers_summary_incremental__dbt_tmp` 
     ("id", "name", "email", "updated_at")
   SELECT 
     "id", 
     "name", 
     "email", 
     "updated_at"
   FROM `bytehouse_demo`.`customers_summary_incremental`
   WHERE (id) NOT IN (
     SELECT id
     FROM `bytehouse_demo`.`customers_summary_incremental__dbt_new_data`
   );
   
   -- 3. Insert new/updated records from the __dbt_new_data table into the temporary table, at which point, the temporary table __dbt_tmp contains all records
   INSERT INTO `bytehouse_demo`.`customers_summary_incremental__dbt_tmp` 
     ("id", "name", "email", "updated_at")
   SELECT 
     "id", 
     "name", 
     "email", 
     "updated_at"
   FROM `bytehouse_demo`.`customers_summary_incremental__dbt_new_data`;
   
   -- 4. Delete the intermediate table __dbt_new_data
   DROP TABLE IF EXISTS `bytehouse_demo`.`customers_summary_incremental__dbt_new_data`;
   
   -- 5. If the backup table already exists, delete it. The backup table is used to store the data of existing tables.
   DROP TABLE IF EXISTS `bytehouse_demo`.`customers_summary_incremental__dbt_backup`;
   
   -- 6. Create a backup table using the data of the existing tables.
   RENAME TABLE `bytehouse_demo`.`customers_summary_incremental` 
   TO `bytehouse_demo`.`customers_summary_incremental__dbt_backup`;
   
   -- 7. Delete the existing table.
   DROP TABLE IF EXISTS `bytehouse_demo`.`customers_summary_incremental`;
   
   -- 8. Rename the temporary table to the final table name.
   RENAME TABLE `bytehouse_demo`.`customers_summary_incremental__dbt_tmp` 
   TO `bytehouse_demo`.`customers_summary_incremental`;
   
   -- 9. Finally, delete the backup table, which will no longer be used thereafter. The backup table is only used for fault recovery and atomicity purposes.
   DROP TABLE IF EXISTS `bytehouse_demo`.`customers_summary_incremental__dbt_backup`;
   ```
   


<span id="e1468d31"></span>
## Create incremental materialization using the append strategy

<span id="6a1ed4f0"></span>
### Using example

Create customers_summary_incremental_append in the models folder of the dbt project. SQL file, create incremental materialization using the `append` strategy:

```SQL
{{
  config(
    materialized='incremental',
    unique_key='id',
    incremental_strategy='append'
  )
}}

SELECT
  id,
  name,
  email,
  updated_at
FROM {{ source('customers_source', 'customers') }}
{% if is_incremental() %}
  WHERE updated_at > (SELECT max(updated_at) FROM {{ this }})
{% endif %}
```


The parameters are described as follows:


|Parameters |Configuration Description |
|---|---|
|`materialized` |The materialized form of the table. |
|`unique_key` |Unique key value of the unique key table. |
|`incremental_strategy` |Incremental strategy. |


<span id="8b22db41"></span>
### How it works


1. Inside dbt\-bytehouse, the following SQL command will be executed to create an incremental table:

   ```SQL
   CREATE TABLE `bytehouse_demo`.`customers_summary_incremental_append` 
   ENGINE = CnchMergeTree() 
   ORDER BY (tuple()) 
   AS (
     SELECT 
       id, 
       name, 
       email, 
       updated_at 
     FROM `bytehouse_demo`.`customers`
   );
   ```
   

2. If the table already exists, dbt\-bytehouse will continue to execute the following INSERT query:

   ```SQL
   INSERT INTO `bytehouse_demo`.`customers_summary_incremental_append` 
     ("id", "name", "email", "updated_at") 
   SELECT 
     id, 
     name, 
     email, 
     updated_at 
   FROM `bytehouse_demo`.`customers` 
   WHERE updated_at > (
     SELECT max(updated_at) 
     FROM `bytehouse_demo`.`customers_summary_incremental_append`
   );
   ```
   


<span id="d3f65d9d"></span>
## Create incremental materialization using the insert_overwrite strategy

<span id="f3937985"></span>
### Usage example

Create the file customers_summary_incremental_override.sql in the models folder of the dbt project, and use the `insert_overwrite` strategy to create an incremental materialization:

```SQL
{{
  config(
    materialized='incremental',
    partition_by='updated_at',
    incremental_strategy='insert_overwrite'
  )
}}

SELECT
  id,
  name,
  email,
  updated_at
FROM {{ source('customers_source', 'customers') }}
{% if is_incremental() %}
  WHERE updated_at > (SELECT max(updated_at) FROM {{ this }})
{% endif %}
```


Parameter description is as follows:


|Parameter |Configuration description |
|---|---|
|`materialized` |The materialized form of the table. |
|`partition_by` |The partition column of the table. |
|`incremental_strategy` |Incremental Strategy. |


<span id="1e853a5e"></span>
### How it works


1. Inside dbt\-bytehouse, the following SQL will be executed to create the incremental table:

   ```SQL
   CREATE TABLE `bytehouse_demo`.`customers_summary_incremental_override` 
   ENGINE = CnchMergeTree() 
   ORDER BY (tuple()) 
   PARTITION BY (updated_at)
   AS (
       SELECT 
           id, 
           name, 
           email, 
           updated_at 
       FROM `bytehouse_demo`.`customers`
   )
   ```
   

2. If the table already exists, dbt\-bytehouse will continue to execute the following INSERT query:

   ```SQL
   DROP TABLE IF EXISTS `bytehouse_demo`.`customers_summary_incremental_override__dbt_new_data_4992e4f4_05fc_42d1_b98f_860e4006d3cc`;
   
   CREATE TABLE `bytehouse_demo`.`customers_summary_incremental_override__dbt_new_data_4992e4f4_05fc_42d1_b98f_860e4006d3cc`
   ENGINE = CnchMergeTree()
   ORDER BY (tuple())
   PARTITION BY (updated_at)
   AS (
       SELECT
           id,
           name,
           email,
           updated_at
       FROM `bytehouse_demo`.`customers`
       WHERE updated_at > (SELECT max(updated_at) FROM `bytehouse_demo`.`customers_summary_incremental_override`)
   );
   
   SELECT DISTINCT partition_id
   FROM system.cnch_parts
   WHERE part_type <= 2
   AND database = 'bytehouse_demo'
   AND table = 'customers_summary_incremental_override__dbt_new_data_4992e4f4_05fc_42d1_b98f_860e4006d3cc';
   
   ALTER TABLE `bytehouse_demo`.`customers_summary_incremental_override`
   REPLACE PARTITION ID '1705276800'
   FROM `bytehouse_demo`.`customers_summary_incremental_override__dbt_new_data_4992e4f4_05fc_42d1_b98f_860e4006d3cc`;
   
   DROP TABLE IF EXISTS `bytehouse_demo`.`customers_summary_incremental_override__dbt_distributed_new_data`;
   
   DROP TABLE IF EXISTS `bytehouse_demo`.`customers_summary_incremental_override__dbt_new_data_4992e4f4_05fc_42d1_b98f_860e4006d3cc`;
   ```
   


<span id="35731dbf"></span>
## Using seeds


1. Using the following content, create the country_codes.csv file in the seeds folder of the dbt project:

   ```Plain
   country_code,country_name
   US,United States
   CA,Canada
   GB,United Kingdom
   ```
   

2. Execute the `dbt seed` command:

   ```Bash
   dbt seed
   ```
   

   This command generates the following ByteHouse query:

   ```SQL
   INSERT INTO `bytehouse_demo`.`country_codes` ("country_code", "country_name")
   FORMAT CSV
   US,United States
   CA,Canada
   GB,United Kingdom
   ```
   


<span id="b242786d"></span>
## (Optional) Use ByteHouse Unique Key

ByteHouse Unique Key table refers to a CnchMergeTree table that specifies a Unique Key. For more details, see [Unique Key table](https://docs.byteplus.com/docs/bytehouse/unique-key-table).

dbt\-bytehouse supports using ByteHouse Unique Key tables when creating materialized views. If needed, you can add `cnch_unique_key` in the model configuration file models/xxx.sql.

```SQL
{{ config(order_by='(id)', cnch_unique_key='(id)', materialized='table') }}
```


Parameter description:


|Parameter |Configuration |
|---|---|
|`order_by` |The sorting form of this table. |
|`cnch_unique_key` |ByteHouse Unique Table’s Key Column. |
|`materialized` |The materialized form of this table. |
