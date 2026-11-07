---
title: "ETL introduction"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/brief_introduction_to_etl"
---

Streaming data ETL (Extract Transform Load) is a data processing tool provided by Database Transmission Service (DTS). It uses SQL statements written in a script language configured with Domain Specific Language (DSL) syntax and combines DTS's efficient streaming data replication capability to extract, transform, process, and load streaming data. This topic introduces the background and application scenarios of ETL.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

DSL is a script language designed by DTS based on the LISP\-1 standard for data processing needs in data synchronization scenarios. DTS uses the DSL script language to extract, transform, process, and load strings, dates, and numerical values in data, typically for data filtering scenarios. For details on DSL syntax, refer to [DSL syntax](https://docs.byteplus.com/en/docs/DTS/dsl_syntax).

<span id=".5bqU55So5Zy65pmv"></span>
## Application scenarios

DTS, combined with ETL tools, is used for typical scenarios such as data filtering, data desensitization, data modification time recording, and data change auditing. The specific examples are as follows:

<span id=".5pWw5o2u6L-H5ruk"></span>
### Data filtering


* Row filtering

   In some e\-commerce scenarios, when synchronizing paid order rows, you can configure ETL filtering function for the DTS task, using DSL syntax to insert additional transformation logic to delete unpaid orders. This example configures the ETL filtering function to filter unpaid order rows based on the following SQL statements:

   ```sql
       CREATE TABLE orders (id bigint(20) primary key,state tinyint);
       INSERT INTO orders VALUES (1,0); -- 0 unpaid orders
       INSERT INTO orders VALUES (2,1); -- 1 paid orders
   ```
   

   The ETL filtering function is as follows:

   ```lisp
       (defn filter-payed-orders []
         (dts/match-table "orders"
           (if (= 0 (dts/column 'state))
              (dts/drop))))
   ```
   

* Field filtering

   In some special scenarios, when filtering certain fields is required, you can configure ETL filtering function for the DTS task, using DSL syntax to insert additional transformation logic to filter out sensitive fields. This example configures the ETL function to filter sensitive fields based on the following SQL statements:

   ```sql
       CREATE TABLE staff (id bigint(20) primary key, name varchar(30), marriage varchar(20));
       INSERT INTO staff VALUES (1,"Tom","已婚");
   ```
   

   The ETL filtering function is as follows:

   ```lisp
           (defn    drop-marriage-field    []
                   (dts/match-table    "staff"    
                                   (dts/drop-column    'marriage)))
   ```
   


<span id=".5pWw5o2u6ISx5pWP"></span>
### Data desensitization

In scenarios such as data backup and data integration that require statistical analysis, to ensure the security of user privacy data, you need to configure ETL filtering function for the DTS task, using DSL syntax to insert additional transformation logic to desensitize sensitive data. This example uses the following SQL statements to configure the ETL function to convert identity information into MD5 values to filter sensitive data:

```sql
    CREATE TABLE user(id int NOT NULL PRIMARY KEY, id_card varchar(100) NOT NULL, name varchar(100) NOT NULL);
    INSERT INTO user VALUES(1, '123456789', '张三');
    INSERT INTO user VALUES(2, '987654321', '李四');
```


The ETL filtering function is as follows:

```lisp
    (defn    desensitization    []
            (dts/match-table    "user"    (dts/map-column    'id_card    str/md5)))
```


<span id=".5a2X5q615Y-Y5o2i"></span>
### Field transformation


* Convert JSON string to JSON struct

   Since DTS supports synchronization between heterogeneous data types, for example, synchronizing the education field as a JSON string in the MySQL employee table to Elasticsearch and presenting it as a JSON struct. This example uses the following SQL statements to configure the ETL function to convert JSON strings to JSON structs:

   ```sql
   CREATE TABLE `employee` (
     `id` bigint NOT NULL,
     `name` varchar(32) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
     `education` json DEFAULT NULL,
     PRIMARY KEY (`id`)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci
   -- write data
   insert into employee values(1,"Jack",
   '[{"name":"dts university","duration":{"from":"2000-01-01","to":"2004-01-01"}}]');
   ```
   

   The ETL filtering function is as follows:

   ```lisp
   (defn    transform-education    []
           (dts/match-table    "employee"
                       (dts/map-column    'education    json/parse)))
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The <code>education</code> field, after ETL transformation, will be written into the target ES database as a JSON array.   </div>
   

   * Convert SET to a string

   ```sql
   create table mytab (color set('red','blue','green','black'));
   ```
   

   The ETL filtering function is as follows:

   ```lisp
   (defn dts/transform []
       (dts/match-table "mytab"
                  (dts/set-column (case (dts/column "color") 
                                  0b1 "red"
                                      0b10 "blue"
                                      0b100 "green"
                                      0b1000 "black"))))
   ```
   

   * Convert ENUM to a string

   ```sql
       create table mytab (color enum('red','blue','green','black'));
       
   ```
   

   The ETL filtering function is as follows:

   ```lisp
       (defn dts/transform []
           (dts/match-table "mytab"
                   (dts/set-column (case (dts/column "color") 
                                 1 "red"
                                     2 "blue"
                                     3 "green"
                                     4 "black"))))    
   ```
   


<span id=".5ri45oiP5ZCI5pyN"></span>
### Game server merge

Each regional server in a certain game application contains User data, using UUID as the unique business identifier to ensure global uniqueness and prevent data overlap across regions. After the server merge, discard the auto\-increment primary key and use `user_id` as the unique identifier:

```sql
    -- source table structure
    CREATE TABLE `user` (
        `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
        `user_id` varchar(64) NOT NULL,
        `name` varchar(64) DEFAULT NULL,
      PRIMARY KEY (`id`),
      UNIQUE KEY `userid_idx` (`user_id`) USING BTREE
    ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
    -- target table structure (consistent with source end)
    CREATE TABLE `user` (
        `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
        `user_id` varchar(64) NOT NULL,
        `name` varchar(64) DEFAULT NULL,
      PRIMARY KEY (`id`),
      UNIQUE KEY `userid_idx` (`user_id`) USING BTREE
    ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```


Configure the ETL merge function as follows:

```lisp
    (defn main []
       (dts/match-table "user"
           ;; discard auto-increment column
           (dts/drop-column "id")
           ;; specify user_id as primary key
           (dts/use-index "user_id")))
```


Example: Information from two different source ends is as follows.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b2db42ec6152724b4f429fb889af13e2.png) </span>

Create two DTS tasks to fetch data from two source ends and merge into one target table (assuming the target auto\-increment ID starts from 1):

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b710cf55bbf8ba5ec85630791ced1371.png) </span>

<span id=".5Yy65Z-f5Lia5Yqh5ZCI5bqT"></span>
### Regional business database merge

This scenario is similar to the game server merge, but with slight differences. For example, a social application platform needs to add a Region column to the like actions counted domestically and overseas and merge into a global summary table, using `region+user_id` as the unique identifier:

Partitioned table CN/US:

```sql
    CREATE TABLE `user_stats` (
        `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
        `user_id` varchar(64) DEFAULT NULL,
        `star` bigint,
      PRIMARY KEY (`id`),
      UNIQUE KEY `userid_idx` (`user_id`) USING BTREE
    ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```


Summary table:

```sql
    CREATE TABLE `user_stats` (
        `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
        `region` varchar(32),
        `user_id` varchar(64) DEFAULT NULL,
        `star` bigint,
      PRIMARY KEY (`id`),
      UNIQUE KEY `region_userid_idx` (`region`,`user_id`) USING BTREE
    ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```


Configure the ETL merge function:

```lisp
    // 例如这是 CN 区 DTS 任务的 ETL 函数
    (defn main []
       (dts/match-table "user_wallets"
           ;; discard auto-increment column
           (dts/drop-column "id")
           ;; set new column region value to CN
           (dts/set-column "region" "CN")
           ;; specify primary key region+user_id
           (dts/use-index "region" "user_id")))
    
    // 比如，这是 US 区 DTS 任务的 ETL 函数
    (defn main []
       (dts/match-table "user_wallets"
           ;; discard auto-increment column
           (dts/drop-column "id")
           ;; set new column region value to US
           (dts/set-column "region" "US")
           ;; specify primary key region+user_id
           (dts/use-index "region" "user_id")))
```


Example: Wallet information of domestic and overseas users is as follows.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_988476fc4aa4e11ddcf0622c10f21a5e.png) </span>

Create two DTS tasks to fetch data from two source ends and merge into one target table (assuming the target auto\-increment ID starts from 1):

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_39c5192e81f139967eab333d155d2e63.png) </span>

<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [Creating and starting a data synchronization task](https://docs.byteplus.com/en/docs/DTS/creating_and_initiating_a_synchronization_task)

* [How to configure ETL in a DTS synchronization task](https://docs.byteplus.com/en/docs/DTS/configuring_etl_in_dts_synchronization_task)

* [DSL syntax](https://docs.byteplus.com/en/docs/DTS/dsl_syntax)

* [Verifying ETL rules using the ETL Playground tool](https://docs.byteplus.com/en/docs/DTS/debugging-ETL-rules-with-ETL-Playground-tool)
