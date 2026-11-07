---
title: "Offline loading"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-batch-loading"
---

ByteHouse CDW supports offline data loading through object storage services (such as S3, BytePlus Object Storage Service TOS, Alibaba Cloud OSS). This is suitable for batch loading large volumes of data. Currently, it supports loading CSV, JSON, AVRO, and PARQUET file types.

<span id="f9571f2b"></span>
# Preparation

Starting from October 2025, configuring a virtual warehouse is required for executing data import tasks in the ByteHouse console. Before initiating the import, ensure you have the USE privilege for the virtual warehouse to be used. You can view the obtained virtual warehouse privileges by going to **Access control** \> **User** \> **User list**, clicking the **username**, and checking the \*\*Resource privileges \*\*tab on the **user details** page. If you have not been authorized yet, contact the administrator for configuration. For details, refer to [Resource privilege management](https://docs.byteplus.com/docs/bytehouse/resource-privilege-management).

<span id="bf649122"></span>
# Create a job


1. In the ByteHouse CDW console, click the **Data loading** tab, then click the **New loading job** button to enter the job creation interface.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e91e4e96e7648c5a7f3e48e6689d3fa~tplv-goo7wpa0wc-image.image) </span>

2. Fill in the general information for the data loading job. You can customize the job name and description.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/21e71d76883e466c87a2a13243d84ee3~tplv-goo7wpa0wc-image.image) </span>

3. Select the data source type as object storage, choose the vendor, and select an existing data source from the dropdown list.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d00c6d46f7254cb6a85df63412fea154~tplv-goo7wpa0wc-image.image) </span>

   If you have not created a data source, click **Connect a new datasource** to create and configure a data source, then click **Connect**. Different vendors require different configuration details for the data source connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d0c800a30f4f4eb3a8f0d0ee416361f4~tplv-goo7wpa0wc-image.image) </span>

   
   |Configuration Item |TOS |S3 |Alibaba OSS |
   |---|---|---|---|
   |Source Name |Customize your data source name. |||
   |Enable path access mode |None |After enabling, access the specified bucket using path\-style access mode. If not enabled, virtual hosted style will be used. ||
   |Access Key |Configure the Access Key for BytePlus TOS service. For details, see [Creating an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey). |Configure the Access Key for S3 service. You can log in to the S3 service console or contact the administrator to obtain it. |Configure the AccessKey ID for Alibaba OSS service. For details, see [Create AccessKey](https://www.alibabacloud.com/help/en/ram/user-guide/create-an-accesskey-pair). |
   |Secret Key |Configure the Secret Key for BytePlus TOS service. For details, see [Creating an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey). |Configure the Secret Key for S3 service. You can log in to the S3 service console or contact the administrator to obtain it. |Configure the AccessKey Secret for Alibaba OSS service. For details, see [Create AccessKey](https://www.alibabacloud.com/help/en/ram/user-guide/create-an-accesskey-pair). |
   |default region |Set to the region of the TOS service. For details, see [Region and Endpoint](https://docs.byteplus.com/en/docs/tos/docs-region-and-endpoint). |none |Set to the region of the Alibaba OSS service. For details, see [OSS regions and endpoints](https://www.alibabacloud.com/help/en/oss/user-guide/regions-and-endpoints?spm=a2c63.p38356.help-menu-31815.d_4_0_0.611d7cccdnTaTX&scm=20140722.H_31837._.OR_help-T_intl~en-V_1). |
   

4. After selecting the data source, configure its details, including the region, bucket, schema sample file path, path prefix, and format. Different data source types require different detailed data source configurations. Please refer to the actual interface. The following are the full parameter configuration instructions:

   
   |Parameter |Configuration Description |
   |---|---|
   |Region |Set to the region where the object storage data source is located. |
   |Bucket |Select the storage bucket where the data source is located. |
   |Path to schema sample file |Set the schema sample file for subsequent schema parsing and loading configuration generation. |
   |Path prefix |Set the file path prefix for the loading job; this job can load any file under this prefix that matches the sample file schema. |
   |Format |ByteHouse supports CSV, JSON, AVRO, and Parquet file formats. The system will automatically match the format based on the schema sample file you select.<br><br>For CSV and JSON files, you can configure the corresponding format parameters. See the table below for details. |
   

   If you upload a CSV or JSON file, you need to configure the corresponding format parameters.

   
   |Format |Parameter |Configuration Description |
   |---|---|---|
   |CSV |Header |ByteHouse supports setting with or without header.<br><br><br>* No header: ByteHouse uses "_c0, _c1" as source column names to map the schema to the target table.<br><br>* With header: ByteHouse separates the header to map the schema to the target table. |
   ||CSV format |ByteHouse supports setting field separator, encoding method, quote character, escape character, skipping lines, multi\-line support, null value, and triming whitespace. |
   |JSON |Multi\-line support |Set whether to enable multi\-line support. Enable multi\-line support means each JSON object in the file (representing one line) is formatted separately. This differs from ['JSON Lines'](https://jsonlines.org/), where JSON objects are flattened into one line per object. |
   ||Allow comments |Set whether comments are allowed in the file. |
   

5. Select the target database and table for loading.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aea4839a501e4e5082fa0a577d910f9d~tplv-goo7wpa0wc-image.image) </span>

6. Define schema mapping. After setting the data source and target table, the system automatically populates the schema mapping table to create a mapping between the data source and the target table. ByteHouse currently supports the following schema mapping configuration operations, which you can adjust as needed.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1de0a4235f86443a8a1135cdfcf2e300~tplv-goo7wpa0wc-image.image) </span>

   * **Adjust schema mapping logic**

      If the generated schema does not meet expectations or you need to adjust the mapping between source and target columns, click **Parse** to reparse the data.

   * **Adjust target table**

      You can open a new browser tab, go to the [Database page](https://console.byteplus.com/bytehouse/region:bytehouse+ap-southeast-1/n/default/database) , and adjust the target table. After adjustment, click **Refresh target table** in the **Define Schema Mapping** module on the data loading page. The system will automatically read the adjustments to the target table and update the schema mapping table.

   * **Configure date parsing format**

      `yyyy-MM-dd'T'HH:mm:ss` (the default time format in Java). Note that the date (year\-month\-day) and time (hours\-minutes\-seconds) are separated by the constant `T`. If your data uses other formats, manual configuration is required. For configuration steps, please see [How to configure date parsing format?](https://docs.byteplus.com/docs/bytehouse/faq#ae91a828).

   * **Configure timezone**

      If the data you need to import contains fields with dates that include time zone information, refer to [How to configure timezone?](https://docs.byteplus.com/docs/bytehouse/faq#b08d5e59) to adjust the data format and avoid time zone import exceptions.

7. Configure the loading job's loading type; you can choose incremental write or full overwrite based on your needs.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2f73a40bb92d45cc90f623e90018fe4f~tplv-goo7wpa0wc-image.image) </span>

   * **Append data**: Each job execution adds data incrementally to the target table without overwriting existing data.

   * **Overwrite**: Replace the entire target table with the latest data. You can choose either partition\-level overwrite or full data replacement. Before choosing partition overwrite, confirm that the target table has a partition key defined.

   * **Virtual warehouse**: Select a virtual warehouse from the dropdown list. Before use, make sure you have the USE privilege of this virtual warehouse.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you choose to create a new sync table, the table and loading job will be created sequentially. This may result in the loading job failing to create while the table is created successfully. If you encounter this, return to step 6 and select loading to an existing table for the loading.   </div>
   

8. Click **Create** to generate the loading job. After creating the data loading job, the system will redirect to the job details page. The job will be paused at this point. You can click **Start** to start the job.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/04f802221ce14daea638f3ff1c85d58e~tplv-goo7wpa0wc-image.image) </span>

9. In the **Start TOS Job** popup, confirm the file name to upload and click **OK**. The system will execute the data loading job.

   If you have a new file to upload, you can select and replace it from the dropdown list. The following is an interface example when TOS is used as the loading data source:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bddc242fd21145018494a64883e1f185~tplv-goo7wpa0wc-image.image) </span>

   Object Storage jobs support wildcard search. Once enabled, you can perform fuzzy searches to load multiple files. Supported cases are as follows:

   * Asterisk (\*) matches zero or more arbitrary characters.

   * Question mark (?) matches up to the number of arbitrary characters equal to the number of question marks.

   * Square brackets ([ ]) match any character within the specified range.


<span id="86e39cba"></span>
# View jobs

On the data loading page, you can view all created jobs through the job view.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/80ae6d8c670546c283cf218efbe917bc~tplv-goo7wpa0wc-image.image) </span>

You can also check job execution status, execution logs, and configurations via the execution view. Data queries are enabled only when the job type is in a successful state.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9cc191dcf6b44a75b5c7f78ec61bf392~tplv-goo7wpa0wc-image.image) </span>


* **View job execution logs**

   Click the **Log** button on the target job row to view the current job’s execution log. You can click to copy or download the log.

* **View configuration**

   Click the **Config** button in the target job row to view the current execution configuration of the job. You can click to copy or download the configuration JSON file for reference when importing data via OpenAPI.

* **Troubleshoot import job**

   To troubleshoot an imported job, click the **job name**, then click the **execution ID** under **Execution history** to check the loading status, error details, logs, and other information to help assess and optimize the import.


<span id="0eeb65f0"></span>
# Start/stop a job


1. In the job list, click the source type dropdown and select your storage service vendor to filter loading jobs.

2. Click the **Start** button in the target job row to launch the current loading job.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ef5aa67c279a4b4eb355cd1a6df3a1c3~tplv-goo7wpa0wc-image.image) </span>

3. Click **job name**, go to the job details page, where you can view the job’s synchronization history, current configured schema mappings, logs, and configuration.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/47d3327fc4f4455dac597403d7a47f90~tplv-goo7wpa0wc-image.image) </span>

4. If you need to stop the data loading job, click **Stop**.


<span id="044801d0"></span>
# Edit a job


1. In the job list, click the source type dropdown, select your storage service vendor, and filter loading jobs.

2. Click the **Edit** button in the target job row to enter the loading job configuration page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/474ff67645e64ef4be4e482c861b3c3e~tplv-goo7wpa0wc-image.image) </span>

3. Adjust the job configuration as needed, then click **Update** after editing.


<span id="85e0dfba"></span>
# Copy job configuration

If you need to load data via OpenAPI, you can copy the job configuration for reference.

**Steps**:


1. In the job list, click the source type dropdown, select your storage service vendor, and filter loading jobs.

2. Click the  **...**  button, then click **Copy Config**. The system will copy the current loading job configuration.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/454e5ff8c85444df864fccc0f162638f~tplv-goo7wpa0wc-image.image) </span>


<span id="34957d20"></span>
# Delete a job

In the job list, click the  **...**  button on the target job row Click **Delete job**, then confirm to delete the current job.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3c3d7833ceb2477c8fbf363ab23958bd~tplv-goo7wpa0wc-image.image) </span>
