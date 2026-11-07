---
title: "Database"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Database_faq"
---

<span id=".dmVkYi1teXNxbC3lrp7kvovmlK_mjIHkv67mlLnmlbDmja7lupPlkI3np7DlkJfvvJ8="></span>
### Can you rename databases in NDB for MySQL instance?

No, because database renaming is not a native MySQL feature.

If you must rename a database, you can migrate databases and tables using the following methods.


* Method 1: Export with mysqldump, then recreate and import into a new database. While this method is relatively reliable, it may require significant time for large\-scale data migrations.

* Method 2: Rename tables within the database. For SQL procedures, refer to [MySQL documentation](https://dev.mysql.com/doc/refman/8.0/en/rename-table.html). While faster than mysqldump, this method carries higher risks. For example, views may become invalid because although the view names are updated, their definition statements still reference the original table names.

   ```sql
   -- Create a new database
   CREATE DATABASE new_db_name; 
   -- Rename all tables
   RENAME TABLE db_name.table1 TO new_db_name.table1; 
   -- Delete the original database
   DROP DATABASE db_name;
   ```
   

   For larger number of tables, use the following script to perform batch renaming.

   ```sql
   mysql -uroot -p -e "select concat('rename table db.',table_name,' to new_db.',table_name,';') from information_schema.TABLES where TABLE_SCHEMA='db';" > rename_mysql_name.sql
   
   -- Batch modification
   mysql -uroot -p < rename_mysql_name.sql
   ```
   


<span id=".5omL5bel5omn6KGM55qELWRkbC3mnKrnlJ_mlYjvvJ8="></span>
### Is your manually executed DDL not taking effect?

Check for any active Online DDL tickets when executing DDL manually, as they may override manual DDL changes. For more details about ticket operations, refer to [Ticket management](https://docs.byteplus.com/en/docs/DBW/Managing_data_change_tickets).

<span id="W4DZtJHR"></span>
### What encryption algorithm is used for storing passwords in NDB for MySQL databases?

NDB for MySQL uses the same encryption algorithm as native MySQL. You can execute the following SQL to view the user's password security plugin.

```SQL
select Host,User,plugin,authentication_string from mysql.user; 
```


For a detailed description of the `mysql_native_password` and `caching_sha2_password` plugins, refer to the [MySQL official documentation](https://dev.mysql.com/doc/refman/8.0/en/native-pluggable-authentication.html).

<span id="P3eTu32o"></span>
###
