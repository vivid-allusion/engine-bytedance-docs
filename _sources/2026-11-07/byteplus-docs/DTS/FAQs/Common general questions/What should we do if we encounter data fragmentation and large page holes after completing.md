---
title: "What should we do if we encounter data fragmentation and large page holes after completing data synchronization through DTS?"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/What_should_we_do_if_we_encounter_data_fragmentation"
---

After completing MySQL data synchronization via the Database Transmission Service (DTS), data fragmentation may occur along with relatively large page holes. You can resolve this issue by performing the following operations to reduce fragmentation in database tables, reclaim disk space, and improve query performance.


1. Execute the following command to log in to the MySQL instance:

   ```sql
   mysql -u username -p
   ```
   

2. Execute the following command to select database:

   ```sql
   USE your_database_name;
   ```
   

3. Execute the following command to reclaim space, consolidate fragments, and optimize the table:

   ```sql
   OPTIMIZE TABLE your_table_name;
   ```
