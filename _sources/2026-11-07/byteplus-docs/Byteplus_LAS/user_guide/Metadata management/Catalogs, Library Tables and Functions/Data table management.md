---
title: "Data table management"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Data_table_management"
---

<span id="_1-查看数据表列表"></span>
# View data tables


1. Log in to the LAS console.

2. From the menu, select **Catalog**.

3. Click the data catalog name and then the database name in sequence to enter the **database list** page.

4. On the **database list** page, click the “Value” column in Table count to enter the **table list** page.

5. Click the name of the data table you want to view to see its basic information and data overview.


<span id="4ccceea1"></span>
# Create data tables


1. Log in to the LAS console.

2. From the menu, select **Catalog**.

3. Click the data catalog name and then the database name in sequence to enter the **database list** page.

4. On the **database list** page, click the “Value” column in Table count to enter the **table list** page.

5. On the **table list** page, click Create data table in the upper right corner, fill in information such as fields and storage location, then click **Submit** to complete the creation of the data table.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The fields selected on the current page do not support complex types. To create complex types, you need to use the Spark engine page.</div>


* <div data-tips="true" data-tips-type="tip">Currently, only the following formats (TEXTFILE, SEQUENCEFILE, ORC, PARQUET) are supported for creation on the page. To create tables with other storage formats, use the Spark page or other engine pages.</div>



<span id="827bca8f"></span>
# Edit data tables

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Users can only edit tables for which they have permission.</div>



1. Log in to the LAS console.

2. From the menu, select **Catalog**.

3. Click the data catalog name and then the database name in sequence to enter the **database list** page.

4. On the **database list** page, click the “Value” column in Table count to enter the **table list** page.

5. On the **table list** page, click **Edit** to the right of the data table name you want to edit, and modify information such as storage location.


<span id="2bf72c7c"></span>
# Delete data tables


1. Log in to the LAS console.

2. From the menu, select **Catalog**.

3. Click the data catalog name and then the database name in sequence to enter the **database list** page.

4. On the **database list** page, click the “Value” column in Table count to enter the **table list** page.

5. On the **table list** page, click **Delete** to the right of the data table name you want to delete, and confirm deletion.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Users can only delete tables for which they have permission.</div>


* <div data-tips="true" data-tips-type="tip">When deleting a table, the partitions under the table are deleted first, followed by the table itself.</div>


* <div data-tips="true" data-tips-type="tip">When deleting a table, metadata is deleted first, then the file directory corresponding to the storage location (Location) is deleted. The actions of deleting metadata and deleting files cannot guarantee transactional consistency. That is, metadata may be deleted successfully while the file directory still exists. In other words, the table may not be found, but the corresponding file directory remains.</div>


* <div data-tips="true" data-tips-type="tip">When deleting a data directory, the files will also be deleted. However, currently, file deletion does not support a recycle bin feature. Once deleted, files cannot be recovered. To recover accidentally deleted data, enable version control in TOS. For detailed instructions, please refer to: <a href="https://www.volcengine.com/docs/6349/145534">Version control</a>.</div>



<span id="a81bf5c3"></span>
# Create datasets based on Catalog data tables

Currently, you can directly create a LAS AI dataset based on an existing Catalog table. After the dataset is created, if the corresponding table is deleted in Catalog, the dataset will also be deleted synchronously.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, only dataset creation based on Lance and Iceberg tables is supported.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/631ac89ea08f427fbc42030bdedaa841~tplv-goo7wpa0wc-image.image) </span>
