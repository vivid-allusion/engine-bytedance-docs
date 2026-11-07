---
title: "Edit table"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/edit-table"
---

This tutorial introduces how to edit a table in ByteHouse Enterprise after creating it, using both the visual method and the SQL statement method.

<span id="2a78e085"></span>
# Feature overview

ByteHouse Enterprise supports editing tables visually and using SQL statements. The differences between the two are as follows:


* Visual editing: Currently, only modifying the table description, modifying column data types, adding columns, deleting columns, and adjusting the data life cycle are supported. If a column is set as a key or index, editing is not supported.

* SQL statement editing: The ByteHouse Enterprise Console provides ALTER statement templates. You can copy the corresponding statements to the Data Query page to edit tables. Currently, the following operations are supported: add columns, delete columns, rename columns, change column types, modify TTL, change settings, delete partitions, and unload partitions. For more SQL statements for editing actions, refer to [ALTER statement](https://docs.byteplus.com/docs/bytehouse/ce-alter-statement).


<span id="60f1a29b"></span>
# Edit tables


1. Log in to the ByteHouse Enterprise Console, click the \*\*Data object \*\*tab, select the **target cluster**, click the **target database**, and click the **target table**.

2. On the table details page, click **Edit table**, then click **Visualization edit**. The system will navigate to the update table page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ad11463149cb4fb4bb3ee2f7b6fd7bbe~tplv-goo7wpa0wc-image.image) </span>

3. Update table settings as needed. Currently ByteHouse supports changing the table description, changing column data types, adding columns, and deleting columns. You can also adjust the data lifecycle and TTL.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Before editing the table, Please fully assess the scope of the impact, fields cannot be restored after modification/deletion and historical data is not readable.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2e1bf954c40c41f6b2b52ff87b4a203a~tplv-goo7wpa0wc-image.image) </span>

4. After making the changes, click **Update**. After confirming that the change details are correct, click **Confirm**, and the changes will take effect.


<span id="8dfc4681"></span>
# Edit a table using SQL statements


1. Log in to the ByteHouse Enterprise Edition Console, click the **Data object** tab, select the **Target Cluster**, click the **Target Database**, and click the **Target Table**.

2. On the table details page, click **Edit table**, and then click **Edit by SQL**. The system navigates to the edit table page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/22912970ace141b79c4e9be91b55244a~tplv-goo7wpa0wc-image.image) </span>

3. On the **Edit table** page, check editable items, and the system will generate the corresponding SQL statements.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/73cd3327157a4baeb65f6777165fbad2~tplv-goo7wpa0wc-image.image) </span>

4. Click **Go to editor**. The system will jump to the SQL Editor page, where you can adjust parameters as needed. Then, click **Run** to execute the SQL statement.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/68576796eae648f0b59eb3f281155dd2~tplv-goo7wpa0wc-image.image) </span>
