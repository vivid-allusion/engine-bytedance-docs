---
title: "Quick start"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-quick-start"
---

ByteHouse is a cloud\-native data analytics warehouse that provides an integrated solution in the fields of data analysis and data warehousing, suitable for real\-time user behavior analysis, BI report creation, log data processing, and many other scenarios. It combines the key features of data warehouses, big data platforms, data development/integration/BI ecosystems, and cloud\-native services to deliver a comprehensive, high\-performance, secure, and flexible data solution. This tutorial will guide you through the activation process for ByteHouse Cloud Data Warehouse and how to quickly get started with ByteHouse, including basic data analysis procedures such as database/table creation, data loading, and SQL query operations.

<span id="88537a4b"></span>
# Step 1: Register a BytePlus main account and log in to the console

Go to the [BytePlus official website homepage](https://www.byteplus.com/en), click **Sign up** in the upper right corner, and follow the on\-screen instructions to complete account registration and billing verification for the BytePlus official website. For detailed steps, see [Sign Up and Verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

<span id="e64ee835"></span>
# Step 2: Activate ByteHouse Cloud Data Warehouse


1. Visit the [ByteHouse product homepage](https://www.byteplus.com/en/product/bytehouse) and click **Get started (CDW)** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cb98f905f1794a07bcf5ccf338b42ca2~tplv-goo7wpa0wc-image.image) </span>

2. According to the on\-screen prompts, click **Authorize now** to authorize ByteHouse Cloud Data Warehouse to access private networks, cloud monitoring, and other products across services. After authorization is complete, you can enter the ByteHouse Cloud Data Warehouse console.

3. On the ByteHouse service activation page, configure the region, computing, storage, and network resources for ByteHouse.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2d37ddfa08a140a28a0bf0579e1b364a~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameters |Description |
   |---|---|
   |**Region** ||
   |Zone |The region of the BytePlus data center. Different regions are divided according to geographic location. After an instance is created, its region cannot be changed.<br><br>To switch the region of ByteHouse, click the region name at the top of the page and select from the dropdown list.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1d9a5c61af8744d0a02871891250943f~tplv-goo7wpa0wc-image.image) </span> |
   |**Compute resources** ||
   |Payment method |ByteHouse Cloud Data Warehouse currently only supports pay\-as\-you\-go and annual and monthly subscription billing modes. For billing details, see [Settlement and renewal description](https://docs.byteplus.com/docs/bytehouse/settlement-and-renewal-description). |
   |Virtual warehouse |The virtual warehouse is ByteHouse's computing resource. You can create virtual warehouses with specific specifications as needed to provide sufficient resources for various data operations. You can set up multiple virtual warehouses. ByteHouse sets the first virtual warehouse you configure when activating the service as the global default for data writing, providing computing resources for data writing. If multiple virtual warehouses exist, you can switch between virtual warehouses in the Console after activating the service. For details, see [Set the default write virtual warehouse](https://docs.byteplus.com/docs/bytehouse/manage-virtual-warehouse-parameters#e4ec3478).<br><br>Parameter configuration for virtual warehouses is as follows:<br><br><br>* **Specification**: The specification of the virtual warehouse. Different specifications of virtual warehouses have different prices, which you can choose as needed. You can view the specifications and pricing of virtual warehouses in the interface, or refer to [Computational resources](https://docs.byteplus.com/docs/bytehouse/specifications-and-pricing#cadb49e9).<br><br>* **Name**: The name of the virtual warehouse. Custom names are supported, and the name cannot be changed after creation. The naming rules are as follows:<br><br>   * Begin with a lowercase letter.<br><br>   * Consist of lowercase letters and numbers.<br><br>   * Use a single underscore to connect names.<br><br>   * Support up to 31 characters.<br><br>* **Description**: The specific description of the virtual warehouse. You can add a custom description to the virtual warehouse to facilitate future differentiation and use. |
   |Local disk |The purpose of the local disk is to serve as a temporary storage area during data writing and a cache area during data reading.<br><br>You can enable the local disk feature as needed, with a minimum order of 100 GB. For details on the specifications and pricing of the local disk, see [Specifications and pricing](https://docs.byteplus.com/docs/bytehouse/specifications-and-pricing). |
   |Advanced features |You can enable advanced features such as full\-text search, GIS spatiotemporal analysis, and vector search.<br><br><br>* **Full Text Search**: Allows preprocessing of documents and saving indexes for fast searches in the future. For feature details, see [Full-text search ](https://docs.byteplus.com/docs/bytehouse/full_text_search).<br><br>* **GIS**: This feature provides high\-performance geographic spatial analysis (GIS) capabilities, offering geographic data analysis services for scenarios such as location insights and user segmentation. For feature details, see [GIS spatiotemporal analysis](https://docs.byteplus.com/docs/bytehouse/gis-spatiotemporal-analysis).<br><br>* **VectorSearch**: Vector search provides management and similarity queries for vector data, and supports various approximate nearest neighbor (ANN) algorithms to improve search performance and enable processing of unstructured data. For feature details, see [Enable vector search](https://docs.byteplus.com/docs/bytehouse/vector-retrieval). |
   |Auto pause/start |* **Auto start**: The system enables the auto start feature by default. Once enabled, users do not need to manually start the virtual warehouse and can send requests to the virtual warehouse to activate computing resources and perform queries. After auto start is enabled, the first query may take longer (10–30 seconds). Please configure according to business needs.<br><br>* **Auto pause**: Once enabled, if the virtual warehouse is not used within the configured interval, it will be automatically closed to reduce resource costs.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">To set a specific virtual warehouse as the private server's default write virtual warehouse, you must disable the auto start/stop setting for that virtual warehouse.</div><br> |
   |**Storage resources** ||
   |Storage space |There is no need to purchase storage resources in advance; only pay for the storage space and compressed data volume used. |
   |**Network resources** ||
   |Private Network (VPC) |Bind a private network to ByteHouse to ensure secure data transmission and enable private network connectivity with cloud resources.<br><br>To create a new private network, go to the [VPC Console](https://console.byteplus.com/vpc/region:vpc+ap-southeast-1/vpc). For instructions, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC). |
   |Subnet |Select the available subnet information under the VPC.<br><br>To create a new subnet, go to the [VPC Console](https://console.byteplus.com/vpc/region:vpc+ap-southeast-1/vpc). For instructions, see [Creating subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet). |
   |Security group |Select the security group information attached to the VPC.<br><br>To create a new security group, go to the [VPC Console](https://console.byteplus.com/vpc/region:vpc+ap-southeast-1/vpc). For instructions, see [Creating a security group](https://docs.byteplus.com/en/docs/vpc/Creating-a-security-group). |
   |**Purchase duration** (**Annual/monthly subscription mode requires configuration**) ||
   |Purchase duration |Available options: 1 month to 3 years. |
   |Auto renew |Auto renewal defaults to automatic payment by the system each month, with no manual payment required. Renewal settings can be [modified](https://console.byteplus.com/finance/renew/) at any time. |
   

4. After completing the configuration, check "I have read and agree to the [Service Specific Terms](https://docs.byteplus.com/en/docs/legal/docs-service-specific-terms?_gl=1*tchedh*_gcl_au*MTI3Mjc4MzY4NC4xNzYwNTg0OTA2LjE3OTYzMTM4OTguMTc2NTM2MzY3OS4xNzY1MzYzNzY5*_ga*Mjc0MDQwMjUwLjE3NDQzNTYyNjg.*_ga_2377LE7GQM*czE3NjUzNjMzNjUkbzQ2JGcxJHQxNzY1MzY1NDg2JGo2MCRsMCRoMA..*_ga_3H57BBC3B9*czE3NjUzNjMwNTYkbzUwJGcxJHQxNzY1MzY1NDg2JGoxNCRsMCRoMA..), [Customer Agreement](https://docs.byteplus.com/en/docs/legal/docs-customer-agreement)", click **Activate ByteHouse**, and wait about 1 minute for activation of the ByteHouse Cloud Data Warehouse service.


<span id="e98a76ad"></span>
# Step 3: Set the default virtual warehouse

Before you start using ByteHouse, you need to set a default virtual warehouse for various ByteHouse tasks (the default write virtual warehouse in Step 2 is only for data writing; the default virtual warehouse set in this step is used for query and other tasks), providing default computing resources for query processing. If no virtual warehouse is specified separately when executing subsequent tasks, the default virtual warehouse resources you have set will be used. This step is a **required operation**.

In the ByteHouse cloud data warehouse console, go to **Tenant management** \> **Parameter settings** \> **User Parameters** page, click the **Edit** button, and set the default virtual warehouse.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b5a2f44a7974e06b3d91d7539aee911~tplv-goo7wpa0wc-image.image) </span>

<span id="0946616d"></span>
# Step 4: Create data objects

This tutorial uses the creation of the database `bh_demo` and the table `employees` as examples to introduce how to create data objects in ByteHouse cloud data warehouse and import data by uploading local files.

<span id="22ea3ec0"></span>
## Create a database

You can create a database using either visual database creation or SQL statements.


* **Visual database creation**

   1. On the **Database** tab in the ByteHouse cloud data warehouse console, click the **New** button, then click **Create database**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24093fcabe904cbcbc502907b375f588~tplv-goo7wpa0wc-image.image) </span>

   2. In the popup window, fill in the database name and description. This article uses the `bh_demo` database as an example.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8441c17b845442fbeb7b05be57e626d~tplv-goo7wpa0wc-image.image) </span>

* **Create a database using SQL statements**

   Click the **SQL worksheet** tab in the ByteHouse console, enter the `CREATE DATABASE` command in the editor, and click **Run** to create the database. Example SQL statement:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6d1b3d7e7ba84407af9bfd96264d2efe~tplv-goo7wpa0wc-image.image) </span>

   ```sql
   CREATE DATABASE bh_demo;
   ```
   


<span id="ed17c8d2"></span>
## Create a table


1. Click the **Database** tab, click the `bh_demo` database in the list, then on the details page of this database, click the +**Table** button in the upper right corner, and then click **By Visualization**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b992f503e76f49f6a2ffa5fa95395c64~tplv-goo7wpa0wc-image.image) </span>

2. On the page that pops up for creating a table, configure the table information.

   1. Enter the basic information for the table, including the table name and description.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/110e57cb9bf14a78ba04c376f521ec31~tplv-goo7wpa0wc-image.image) </span>

   2. Configure columns. Enter the column names and set the column properties. For details, see the parameter description below.

      * To add multiple columns, click **Add column**.

      * To delete a column, check the box in front of the column and click **Delete**.

         Column names can be filled in according to the sample data in the prerequisites. Examples are as follows:

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/63952a8af0e641fea2fd0411923bdf7a~tplv-goo7wpa0wc-image.image) </span>

         **Parameter description**

      
      |Parameter |Configuration description |
      |---|---|
      |Column name |Set the column name.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Column names do not support slashes (/), hyphens (\-), or spaces.</div><br> |
      |Data type |Set the column's data type. For the data types currently supported by ByteHouse, see [Data type](https://docs.byteplus.com/en/docs/bytehouse/data-type). |
      |Default value |Set the column's default value. If a value for this column is not specified when inserting data, ByteHouse will automatically fill in the default value. |
      |Expression |Set whether the default value is an expression, specifying whether the column's default value is a dynamic calculation expression (rather than a fixed value). |
      |Comment |Enter a description for the column to indicate its business meaning, making future maintenance easier. |
      |Nullability |Set whether this column's value can be null.<br><br>If this option is selected, the column can store NULL values; if not selected, the column is non\-nullable and a value must be specified when inserting data. |
      

   3. Configure key settings. ByteHouse supports configuring properties for tables such as order by key, partition key, TTL (Time To Live), unique key, and more.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cbf5d33f5611451eb46f49a61c6ad9ae~tplv-goo7wpa0wc-image.image) </span>

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">After the table is successfully created, most parameter fields cannot be modified. Please understand the purpose of each key and plan accordingly before creating the table. For more details on table creation configuration, see <a href="https://docs.byteplus.com/docs/bytehouse/bytehouse-table-creation-best-practice">Best practice for creating tables in ByteHouse</a> and <a href="https://docs.byteplus.com/docs/bytehouse/bytehouse-best-practice-for-unique-key-tables">Best practice for ByteHouse Unique Key tables</a>.      </div>
      

      **Parameter description**

      
      |Parameter |Configuration details |
      |---|---|
      |Order by key |Required field. The order by key determines the physical storage order of data in the database. A table can have up to five order by keys.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">After table creation, the type of the order by key <strong>cannot</strong> be modified, and columns cannot be added or removed. To modify it, you must delete the table and re\-import the data.</div><br> |
      |Partition key |Optional field. The partition key determines the data partition to which each row in the table belongs, allowing large tables to be split into smaller parts. Partition fields cannot be nullable; up to 5 partition fields can be set.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">After table creation, the type of the partition key field <strong>cannot</strong> be modified, and columns cannot be added or removed.</div><br> |
      |TTL |Optional field. TTL (Time To Live) refers to the lifecycle of data, calculated in days, using the partition key as the basis, and can be used to automatically clean up expired data.<br><br><br>* To set this parameter through visual table creation, you must set a column of type Date or Datetime as the partition key to enable the TTL feature.<br><br>* To set other types of columns as the partition key for TTL, use SQL statements to create the table. Go to the **SQL worksheet** page to perform this operation. For table creation statements, see [CREATE statement (CREATE)](https://docs.byteplus.com/docs/bytehouse/create-statement).<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">After table creation, TTL cannot be adjusted via visual table editing, but can be adjusted using SQL statements. For operation details, see <a href="https://docs.byteplus.com/docs/bytehouse/alter-statement#ddda8af1">TTL operations (TTL)</a>.</div><br> |
      |Unique key |The unique key supports Upsert (Update and Insert) capability, ensuring data deduplication at the partition level and always returns the latest value for the corresponding unique key. Up to 10 unique keys are supported.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">After table creation, the unique key field <strong>cannot</strong> be modified in type, and columns cannot be added or removed.</div><br> |
      |Cluster key |For each table or partition, specifying a cluster key further divides it into buckets by hashing the data in the column, enabling finer granularity and improving query and sampling efficiency. Cluster keys cannot be nullable.<br><br>You can choose to set it as the default hash function.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">After table creation, the bucket key field <strong>cannot</strong> be modified in type, and columns cannot be added or removed.</div><br> |
      |Primary key |The primary key is used to organize data files and to constrain the unique identification of each record in the table. The primary key must contain unique values and cannot contain null values. Only one primary key is allowed per table.<br><br>By default, explicit specification is not required; ByteHouse will use the order by key as the primary key.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">After the table is created successfully, the primary key field <strong>does not support</strong> modifying the type, adding columns, or removing columns.</div><br> |
      |Sampling key |The sampling key is used in sampling queries. Such queries are executed only on specific portions of data (samples), and are suitable for scenarios where accuracy is sacrificed for performance, or where the result itself is an approximate value.<br><br>The sampling key must be selected from the order by key and primary key, and its data type must be UInt, including UInt8, UInt16, UInt32, and UInt64.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">After the table is created successfully, the sampling key field <strong>does not support</strong> modifying the type, adding columns, or removing columns.</div><br> |
      

      During configuration, you can click the **SQL** tab on the table creation page to view the SQL statement that ByteHouse outputs for creating the table `employees`.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ce6d1179bcb44d17a83382e3060d7ac8~tplv-goo7wpa0wc-image.image) </span>

3. After table configuration is complete, click **Create table**. ByteHouse will automatically create the table and indicate whether creation was successful. When the interface indicates that creation is successful, follow the guidance on the database details page and click **Start Loading Data**. ByteHouse will automatically navigate to the **Create data loading job** page, where you can continue with the instructions in Step 5 below to start importing data.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/13e1f9530db0430cb02f7fcef16488fd~tplv-goo7wpa0wc-image.image) </span>


<span id="5dcd4239"></span>
# Step 5: Import data

Currently, ByteHouse Cloud Data Warehouse supports local small file import, offline import, streaming import and S3/TOS external table import. This article uses uploading a CSV file as an example. For more import methods and operational guidance, see [Overview](https://docs.byteplus.com/docs/bytehouse/docs-data-loading-feature-overview).

<span id="bc794f84"></span>
## Prerequisites


* Download the sample data to be imported.

   <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/74848b71865447b1bd4e47e3340bfe9c~tplv-goo7wpa0wc-image.image" name="employees.csv">employees.csv</Attachment>
   

* Click to open the [virtual warehouse](https://console.byteplus.com/bytehouse/region:bytehouse+ap-southeast-1/virtual-warehouse) page, and view and record the name of the running virtual warehouse. In the import task, you need to specify a virtual warehouse. Before specifying the virtual warehouse, ensure that the virtual warehouse you want to use is running.


<span id="f6a2d627"></span>
## Steps


1. Configure the data loading task.

   1. Fill in the basic information for the import task, and customize the task name and task description.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b03fd33890a41bfb97448ed1316bcd5~tplv-goo7wpa0wc-image.image) </span>

   2. Select the data source type as **File**, and upload a sample file to define the task and parse the schema.

      Click **Click here** or drag the file to the upload area to upload the file. After uploading, the system will automatically read the format. You can verify whether the format is correct.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9a2978ce14a5435786ee72debc65d64d~tplv-goo7wpa0wc-image.image) </span>

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">This tutorial uses CSV file import as an example; ByteHouse also supports JSON, AVRO, and PARQUET file types. For import operations of other file formats, see <a href="https://docs.byteplus.com/docs/bytehouse/docs-ad-hoc-file-upload">Local file loading</a>.      </div>
      

   3. (Optional) For files in CSV format, you can configure format parameters as needed.

      
      |Format |Configuration items |Description |Interface diagram |
      |---|---|---|---|
      |CSV |Header |Supports setting either no header or a header.<br><br><br>* No header: ByteHouse will use "_c0, _c1" as the source column names to map the schema to the target table.<br><br>* With header: ByteHouse will separate the header to map the schema to the target table. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6d655da222bd4e50b0adeb87f234a861~tplv-goo7wpa0wc-image.image) </span> |
      ||CSV format |Supports setting delimiter, quote character, number of filed separator, encoding, quote character, escape character, skip lines, multi\-line support, null value, and trim whitespace. ||
      

   4. Select the target database and table for data loading. Since you navigated to the data import page from the creation page link, ByteHouse will automatically fill in the target database and table. You can confirm that the options here are set to target database `bh_demo` and table `employees`.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fa1ec20ff6b842fd851a28f4112e0abc~tplv-goo7wpa0wc-image.image) </span>

   5. Define schema mapping. After setting the data source and target table, the system will automatically fill in the schema mapping table and generate the mapping relationship between the data source and the target table. ByteHouse currently supports the following schema mapping configuration operations. You can adjust the generated schema mapping as needed.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ab466bff29dc44d081c8ebe7c92ae47a~tplv-goo7wpa0wc-image.image) </span>

      * **Adjust schema mapping logic**

         If the generated schema does not meet expectations or you need to adjust the mapping relationship between source columns and target columns, you can click **Re\-parser** and the system will re\-parse.

      * **Adjust the target table**

         You can open a new browser tab, go to the [Database page](https://console.byteplus.com/bytehouse/region:bytehouse+ap-southeast-1/n/default/database), and adjust the target table. After making adjustments, in the Data loading page, click **Refresh target table** in the **Define Schema mapping** module. The system will automatically read the changes to the target table and update the Schema mapping table.

      * **Date parsing format configuration**

         ByteHouse data import supports automatic parsing of the following date format by default: `yyyy-MM-dd'T'HH:mm:ss` (Java default time format). Caution: Use the constant T to separate the year\-month\-day and hour\-minute\-second sections. If your data uses another format, manual configuration is required. For configuration steps, see [How to configure date parsing format?](https://docs.byteplus.com/docs/bytehouse/faq#ae91a828)

   6. Configure the loading type and virtual warehouse for the task. You can select incremental write or full coverage write as needed.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/da75bbb713c54a8b81e2a737d046f261~tplv-goo7wpa0wc-image.image) </span>

      * **Append data**: With each job execution, data will be incrementally written to the target table, and existing data will not be overwritten.

      * **Overwrite**: Replace the entire target table with the latest data. You can choose partition\-level overwrite or full data replacement. Before selecting partition\-level overwrite, ensure that the target table has a partition key defined.

      * **Virtual warehouse**: Select the virtual warehouse to be used for the task from the dropdown list. Please ensure you have permission to use the selected virtual warehouse and that it is in **running** status; otherwise, the import task may fail to execute.

2. Click **Create** to create the data loading task.

3. After the import task is created, the system will jump to the task details page. At this point, the task will be in a paused state, and you can click **Start** to start the task.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8c64fe96e6a64dbb8c42b91613847ac2~tplv-goo7wpa0wc-image.image) </span>

4. In the popup window for launching the file upload job, select the file upload path and click **OK**. The system will execute the data loading task.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eaad03a83dc8448fbb37ad7351bb0b3d~tplv-goo7wpa0wc-image.image) </span>

   * **Sample path**: Import data using the file uploaded when creating the import task. Select this option to directly use the employees.csv file you uploaded in Step 5.1 for task definition to import data.

   * **Upload A New File**: If you have new data to upload, you can choose to upload a new file. Ensure that the file type and table schema are consistent with the original task configuration.

5. When the import task status displays "**Success**", it indicates that the data import was successful. You can use ByteHouse to manage the imported data.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fac6ccfe22ad40f7b9348824f8ffd292~tplv-goo7wpa0wc-image.image) </span>


<span id="dc864207"></span>
# Step 6: Data query


1. Click the \*\*SQL worksheet \*\*tab. By default, ByteHouse automatically creates a new worksheet and sets the query database to `bh_demo`.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c7f98892d4bf4e2694ce19564b27dc0a~tplv-goo7wpa0wc-image.image) </span>

2. Execute the following SQL statements in the SQL editor area to experience ByteHouse's data query and data writing features.

   * **Query the number of data records**

      ```sql
      SELECT COUNT(*) 
      FROM employees;
      ```
      

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/649a1e4e7822420b8a190d9b95b13a6d~tplv-goo7wpa0wc-image.image) </span>

   * Insert more test data

      ```sql
      INSERT INTO employees
      VALUES
          ('Clementine', 'Adamou', 'cadamou@bytedance.com', '10510 Sachs Road', 'Klenak', '2017-9-22'),
          ('Marlowe', 'De Anesy', 'madamouc@bytedance.co.uk', '36768 Northfield Plaza', 'Fangshan', '2017-1-26');
      ```
      

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7cafd9a5061440239bb9473ebdb3d72c~tplv-goo7wpa0wc-image.image) </span>

   * Query records by email address

      ```SQL
      SELECT email
      FROM employees
      WHERE email LIKE '%.uk';
      ```
      

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6f76f187fda94513b665efacbe002e3b~tplv-goo7wpa0wc-image.image) </span>

3. If query execution fails, you can use the **Audit Log** feature to analyze the reason for the query failure.

   1. Click the query ID in the **SQL worksheet**'s **query results**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c53b0308eea744009e26fc9642aef5bb~tplv-goo7wpa0wc-image.image) </span>

   2. ByteHouse will automatically jump to **Audit logs**. You can click **query ID** to view execution details, or click the **Details** button after a failure to view detailed error information and analyze and optimize the query. Examples are as follows:

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/31a71cecd2b445c1b025bf38a1fb101b~tplv-goo7wpa0wc-image.image) </span>


<span id="ff0a15e9"></span>
# Further use

This concludes the ByteHouse Cloud Data Warehouse Quick Start Guide. More operation instructions and best practices are as follows:


* In addition to uploading local files via , ByteHouse also supports importing data from various data sources. For details, see [Overview](https://docs.byteplus.com/docs/bytehouse/docs-data-loading-feature-overview).

* ByteHouse also provides multiple connection methods, such as ByteHouse CLI, drivers, and ecosystem tools (ELT tools, BI tools, IDE tools). For details, see:

   * [ByteHouse CLI](https://docs.byteplus.com/docs/bytehouse/docs-gateway-client)

   * [Connect to ByteHouse using drivers](https://docs.byteplus.com/en/docs/bytehouse/connection-drivers-overview)

   * [Connect to ByteHouse using ecosystem tools](https://docs.byteplus.com/en/docs/bytehouse/docs-elt-and-orchestration)

* ByteHouse also supports creating tables via SQL statements and provides best practices for configuring tables to help you quickly create high\-performance tables. For details, see:

   * [CREATE statement (CREATE)](https://docs.byteplus.com/docs/bytehouse/create-statement)

   * [Best practice for creating tables in ByteHouse](https://docs.byteplus.com/docs/bytehouse/bytehouse-table-creation-best-practice)

   * [Best practice for ByteHouse Unique Key tables](https://docs.byteplus.com/docs/bytehouse/bytehouse-best-practice-for-unique-key-tables)
