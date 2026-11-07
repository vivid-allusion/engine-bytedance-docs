---
title: "How to use MySQL compression technology"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/How_to_use_MySQL_compression_technology"
---

<span id="mysql-压缩技术简介"></span>
## Introduction to MySQL compression technology

In modern database management systems, the efficiency of data storage and processing is crucial. As data volumes continue to grow, effectively compressing data to save storage space and improve query performance has become an important research topic. As a widely used open\-source database system, MySQL also continuously explores and optimizes data compression technologies to meet user demand for efficient storage and fast access.

This article introduces data compression technologies in MySQL, focusing on table compression, page compression, and their use in real\-world applications.

<span id="mysql-表压缩-table-compression"></span>
## MySQL table compression (Table Compression)

<span id="mysql-压缩表简介"></span>
### Introduction to MySQL compressed tables

Compressed tables are a special type of table in MySQL that reduce storage space by compressing the data of a specified table. Compressed tables are suitable for storing large amounts of repetitive data or for large datasets with low access frequency.

<span id="如何使用-mysql-压缩表"></span>
### How to use MySQL compressed tables


1. Create compressed tables

   1. Table compression \- When creating a table, you can use the `ROW_FORMAT=COMPRESSED` option to create a compressed table. For example:

      ```sql
      mysql> CREATE TABLE my_table (
          id INT PRIMARY KEY,
          name VARCHAR(50),
          age INT
      ) ROW_FORMAT=COMPRESSED  KEY_BLOCK_SIZE=4;
      ```
      

   2. Insert data

      Insert data into a compressed table in the same way as you would a regular table.

2. Query data

   When querying data in a compressed table, MySQL automatically decompresses the data.

3. Check space usage

   You can use the following command to obtain the space usage of a table before and after compression by viewing `TOTAL_MB`.

   ```sql
   mysql> select table_schema, table_name, table_rows,  round(data_length / 1024 / 1024)+round(index_length / 1024 / 1024)+round(data_free / 1024 / 1024) TOTAL_MB, create_options from information_schema.tables where table_name='my_table';
   +--------------+---------------+------------+----------+----------------+
   | table_schema | table_name    | table_rows | TOTAL_MB | create_options |
   +--------------+---------------+------------+----------+----------------+
   | Test         | my_table      |     100000 |       35 |                |
   +--------------+---------------+------------+----------+----------------+
   
   mysql> analyze table test_compress; -- Update table statistics
   
   mysql> select table_schema, table_name, table_rows,  round(data_length / 1024 / 1024)+round(index_length / 1024 / 1024)+round(data_free / 1024 / 1024) TOTAL_MB, create_options from information_schema.tables where table_name='my_table';
   +--------------+---------------+------------+----------+----------------+
   | table_schema | table_name    | table_rows | TOTAL_MB | create_options |
   +--------------+---------------+------------+----------+----------------+
   | Test         | my_table      |     100000 |       20 |                |
   +--------------+---------------+------------+----------+----------------+
   ```
   


<span id="mysql-压缩表特点"></span>
### MySQL compressed table features


* **Compression**:

   * **Table and index compression**: MySQL supports compressing tables and indexes to significantly reduce storage space usage. The performance improvement is more significant for tables with more reads than writes.

   * **Pros and cons**: Compression reduces disk space usage and I/O operations, but it also increases the CPU load, as data requires compression and decompression during Read/Write operations. When using compressed tables, consider increasing the `buffer_pool_size` to improve performance.

* **Best practices**:

   * **Trade\-offs and testing**: Evaluate the trade\-offs and test the use of compression and indexes based on specific application scenarios. Different application scenarios may require different optimization strategies.

      * **Monitoring and optimization**: Regularly monitor Database performance to identify bottlenecks, such as high CPU usage, and apply optimizations like expanding the Buffer pool. Ensure that using compression and indexes provides actual performance improvements.

      * **Dynamic adjustment**: Dynamically adjust compression and indexing strategies based on changing business requirements and data volume to maintain optimal performance.


<span id="如何在压缩表和非压缩表之间转换"></span>
### How to convert between compressed and uncompressed tables


1. Convert an uncompressed table to a compressed table.

   Use the `ALTER TABLE` statement to convert an uncompressed table to a compressed table. For example:

   ```sql
   ALTER TABLE my_table ROW_FORMAT=COMPRESSED;
   ```
   

2. Convert a compressed table to an uncompressed table.

   You can also use the `ALTER TABLE` statement to convert a compressed table to an uncompressed table. For example:

   ```sql
   ALTER TABLE my_table ROW_FORMAT=DYNAMIC;
   ```
   


Note the following when converting table types:


1. Converting the table type may take some time, depending on the table size and data volume.

2. Back up your data before converting the table type to prevent data loss.

3. After converting the table type, you may need to recreate indexes to ensure query performance.


<span id="注意事项"></span>
### **Precautions**


1. System tables do not support table\-level compression.

2. Table compression can be used in the `innodb_file_per_table` tablespace or the general tablespace.

3. In principle, `KEY_BLOCK_SIZE` cannot exceed `innodb_page_size` and cannot be too small. If the specified `KEY_BLOCK_SIZE` is too small, additional overhead is created to reorganize pages when data values cannot be compressed to fit multiple rows per page. Therefore, there is a strict rule: if the `KEY_BLOCK_SIZE` value is too small, the CREATE or ALTER SQL execution will fail.

4. If `FILE_BLOCK_SIZE` is not set, the default value is `innodb_page_size`, and the `COMPRESSION` feature is not allowed.

5. Compressed tables are suitable for **storing large amounts of duplicate data** or for **large volumes of infrequently accessed data**. Compressed tables may not be suitable if the data in them is frequently updated or queried.

6. When using compressed tables, evaluate the pros and cons for your specific situation to choose the most suitable table type.

7. When converting table types, proceed with caution and back up your data to prevent data loss.


<span id="mysql-页压缩-透明压缩（page-compression）"></span>
## MySQL Page Compression/Transparent Compression (Page Compression)

<span id="mysql-页压缩简介"></span>
### Introduction to MySQL Page Compression

Unlike table compression, which compresses data at the row level, MySQL Page Compression is specifically for the InnoDB storage engine. It reduces storage space usage and I/O operations by compressing individual pages in the InnoDB buffer pool.

<span id="如何使用-mysql-页压缩"></span>
### Using MySQL Page Compression


1. To use page compression:

   1. Confirm that `innodb_file_per_table=on` is enabled (the default is ON on BytePlus).

   2. Specify the compression algorithm `COMPRESSION='zlib';`

      ```sql
      CREATE TABLE `my_table` (
          id INT PRIMARY KEY,
          name VARCHAR(50),
          age INT
      ) ENGINE=InnoDB COMPRESSION='zlib'；
      ```
      

* The table structure is changed with ALTER TABLE

   ```sql
   ALTER TABLE my_table COMPRESSION="zlib";
   OPTIMIZE TABLE my_table;
   ```
   

2. Compression algorithms: Volcengine currently supports zlib and lz4 algorithms.


<span id="mysql-页压缩特点"></span>
### MySQL page compression features

Page compression only compresses a part of the page (the page body and trailer), not the page header. Therefore, it has the following differences compared to table compression:


* The table size is larger than with table compression.

* The CPU usage for page compression is lower than that for table compression, and the compression/decompression speed is also higher.

* I/O usage is reduced compared to before compression.


<span id="注意事项"></span>
### **Precautions**


1. The operating system needs to support sparse files and hole punching (currently supported in the Volcengine environment).

2. Page compression is not supported in shared tablespaces.


<span id="关键参数"></span>
## Key parameters


|Parameter |Scope |Parameter description |
|---|---|---|
|innodb_compression_failure_threshold_pct |GLOBAL |When the ratio of Failed to total compressions reaches this Value, MySQL dynamically increases the extra available space for each page to improve the compression success rate. |
|innodb_compression_pad_pct_max |GLOBAL |The percentage of the total space reserved in each page. |
|innodb_compression_level |GLOBAL |The compression level of the zlib algorithm (0\-9, default is 6). A higher compression level results in a higher compression ratio and increased CPU consumption. |
|innodb_log_compressed_pages |GLOBAL |Determines whether to record page re\-compression information in the redolog. The default value is ON. |
|innodb_file_per_table |GLOBAL |Controls whether each InnoDB table uses a separate tablespace file. When enabled, each table has a separate `.ibd` file. This parameter is an O&M parameter for RDS for MySQL. The default value is ON and users do not need to modify it.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Setting this parameter to ON is a prerequisite for enabling page compression.</div><br> |


<span id="如何选择-mysql-压缩方式"></span>
## How to select a MySQL compression method

<span id="表压缩"></span>
### Table compression

<span id="适用情况"></span>
#### Applicable scenarios


1. **Tables that are read\-only or have more reads than writes**: Table compression is suitable for read\-only or read\-mostly tables due to the high overhead of write operations.

2. **Large tables**: Table compression is highly effective for very large tables and can significantly reduce the use of disk storage space.

3. **Backups and archives**: Suitable for backup and archive data, as this data is not frequently modified.


<span id="不适用情况"></span>
#### Inapplicable scenarios


1. **Frequent write operations**: If a table has frequent write operations, table compression can degrade performance.

2. **Applications that require fast responses**: table compression may increase response time, making it unsuitable for such applications.


<span id="页压缩"></span>
### Page compression

<span id="适用情况"></span>
#### Applicable scenarios


1. **Limited disk space**: page compression can significantly reduce disk space usage.

2. **Frequent Read/Write Actions**: page compression performs well when Read/Write Actions are frequent, as it reduces I/O operations.

3. **Sufficient CPU resources**: page compression requires more CPU resources for compression and decompression Actions.


<span id="不适用情况"></span>
#### Unsuitable scenarios


1. **Limited CPU resources**: if the server's CPU resources are limited, page compression may lead to performance degradation.

2. **High compression failure rate**: if the compression failure rate is high, you may need to adjust the `innodb_compression_failure_threshold_pct` Parameter or consider other compression methods.


<span id="总结"></span>
### Summary


* **Table compression**: use for read\-only or read\-heavy large tables and backup and archive data.

* **Page compression**: use when disk space is limited, Read/Write operations are frequent, and CPU resources are sufficient.

* **The easy choice**: if unsure, choose page compression and adjust parameters as needed.


<span id="参考资料"></span>
## References


1. https://www.percona.com/blog/mysql\-compression\-indexes\-and\-two\-smoking\-barrels/

2. https://dev.mysql.com/doc/refman/8.4/en/innodb\-compression\-usage.html
