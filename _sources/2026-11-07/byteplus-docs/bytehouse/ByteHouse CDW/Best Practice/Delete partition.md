---
title: "Delete partition"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-delete-partition"
---

ByteHouse Cloud Data Warehouse (CDW) supports both unique table and normal table. Unique table supports deleting a single data record through delete flag, while normal table does not, and can only delete data under a partition. To delete a single data record from a normal table, delete the partition where the data is located and then re\-import the data.

Here, we use cell_tower data as an example to introduce two ways of deleting partitions. For the creation of cell_tower table and data import, refer to [Sample query](https://docs.byteplus.com/docs/bytehouse/docs-sample-query).

<span id="deleting-partitions-using-the-console"></span>
## Deleting partitions using the console

After importing the cell_tower data, you can view the corresponding database table (the metadata may have a refreshing delay of 5 minutes), and see partition statistics information. This data table uses monthly partitioning based on the first day of each month. You can use filters to search for partition keys with finer granularity .

Select the specific partition key, delete the data in the upper right corner, and choose confirm to delete the corresponding partition.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/eaf8a0d-Screenshot_2023-03-20_at_5.53.33_PM.png) </span>

<span id="deleting-partitions-using-sql"></span>
## Deleting partitions using SQL

You can execute the following SQL to drop partitions based on the structure of the table and the status of partitions.


* Unique table

   
   |Delete Partition Command |Function Description |
   |---|---|
   |alter drop partition statement (recommended) |Delete Partition, supports all tables, directly deletes directories at the underlying level, offers good performance, and is highly recommended for use.<br><br><br>* General Example<br><br>   ```SQL```<br>```   ALTER TABLE $database_name.$table_name DROP PARTITION '2024-10-09'，DROP PARTITION '2024-10-08';```<br>```   ```<br>   <br><br>* Delete partition according to conditions<br><br>   ```SQL```<br>```   ALTER TABLE $database_name.$table_name DROP PARTITION where `toDate(toStartOfDay(date1))` >'2024-10-06';```<br>```   ```<br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">DROP PARTITION where the Expression must contain a complete PARTITION BY expression, and if it's a complex expression, use backticks (``) to enforce separation. <code>toDate(toStartOfDay(date1))</code> is used after PARTITION BY and can refer to the create table statement.   </div><br>    |
   |Delete statement (Not recommended) |Deleting data is a synchronous operation; the underlying method first searches then deletes, using an append\-file method for deletion, which consumes performance, and only supports unique tables.<br><br>Examples are as follows.<br><br>```SQL```<br>```DELETE FROM $database_name.$table_name WHERE date1 = '2024-10-10';```<br> |
   

* Non\-unique table

   
   |Delete Partition command |Function Description |
   |---|---|
   |alter drop partition statement (Recommended) |Delete Partition supports all tables. It directly deletes directories at the underlying level, providing excellent performance. It is recommended as the preferable method.<br><br><br>* General Example<br><br>   ```SQL```<br>```   ALTER TABLE $database_name.$table_name DROP PARTITION '2024-10-09'，DROP PARTITION '2024-10-08';```<br>```   ```<br>   <br><br>* Delete partition based on conditions<br><br>   ```SQL```<br>```   ALTER TABLE $database_name.$table_name DROP PARTITION where `toDate(toStartOfDay(date1))` >'2024-10-06';```<br>```   ```<br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">toDate(toStartOfDay(date1)) is used after PARTITION BY and can refer to the create table statement.   </div><br>    |
   |alter delete (Not recommended) |Deleting data is an asynchronous operation and does not support unique tables.<br><br>Examples are as follows.<br><br>```SQL```<br>```ALTER TABLE $database_name.$table_name DELETE WHERE k1 = 'a';```<br> |
   


&nbsp;
