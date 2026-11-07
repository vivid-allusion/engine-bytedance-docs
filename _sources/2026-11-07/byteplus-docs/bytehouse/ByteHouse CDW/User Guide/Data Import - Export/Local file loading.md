---
title: "Local file loading"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-ad-hoc-file-upload"
---

The ByteHouse CDW console supports visual import of local files, helping you update and replace data. This is suitable for small batch data supplementation or function testing scenarios. Currently, ByteHouse supports importing CSV, JSON, AVRO, and PARQUET file types. This tutorial explains how to create, view, and manage local file import jobs through the console.

<span id="24f41698"></span>
# Caution

The ByteHouse CDW console supports importing local files up to 200.00 MB. For importing large amounts of data, use [Offline loading](https://docs.byteplus.com/docs/bytehouse/docs-batch-loading) or [Streaming loading](https://docs.byteplus.com/docs/bytehouse/docs-kafka-stream-data-import-practice-parsing-nested-json) methods.

<span id="49f2cedd"></span>
# Preparation

Starting from October 2025, configuring a virtual warehouse is required for executing data import tasks in the ByteHouse console. Before initiating the import, ensure you have the USE privilege for the virtual warehouse to be used. You can view the obtained virtual warehouse privileges by going to **Access control** \> **User** \> **User list**, clicking the **username**, and checking the \*\*Resource privileges \*\*tab on the **user details** page. If you have not been authorized yet, contact the administrator for configuration. For details, refer to [Resource privilege management](https://docs.byteplus.com/docs/bytehouse/resource-privilege-management).

<span id="0bbdbb48"></span>
# Create a job


1. Log in to the ByteHouse CDW console, click **Data loading** at the top, then click **New loading job** to enter the new data loading job page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/87e3b8f4e91f4c07b3adca520022de2d~tplv-goo7wpa0wc-image.image) </span>

2. Fill in the general information of the data loading job. You can customize the job name and description.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42343729b78f45df98e2d1d487dfe970~tplv-goo7wpa0wc-image.image) </span>

3. Select the data source type as **File** and upload a sample file to define the job and parse the schema.

   Click **Click Here** or drag files to the upload area to upload files. After uploading, the system will automatically detect the format. You can confirm whether the format is correct.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/85be72cc5b4a44cdb0427293f4fe9239~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">ByteHouse currently supports uploading files of CSV, JSON, AVRO, and PARQUET types only, with a maximum file size of 200.00 MB.   </div>
   

4. (Optional) If you upload CSV or JSON files, you can configure the corresponding format parameters.

   
   |Format |Configuration Item |Configuration Description |Interface Illustration |
   |---|---|---|---|
   |CSV |Header |ByteHouse supports setting to no header or with header.<br><br><br>* No header: ByteHouse uses "_c0, _c1" as source column names to map the schema to the target table.<br><br>* With header: ByteHouse separates the header to map the schema to the target table. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a3be0b09d84a429697c839904ee4ac5d~tplv-goo7wpa0wc-image.image) </span> |
   ||CSV format |ByteHouse supports setting field separator, encoding method, quote character, escape character, skipping lines, multi\-line support, null value, and triming whitespace. ||
   |JSON |Multi\-line support |Set whether to enable multi\-line support. Enabling multi\-line support means each JSON object in the file (representing one line) is formatted as a separate line. This differs from ['JSON Lines'](https://jsonlines.org/), where JSON objects are flattened into one line per object. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fc37ca4c0d35497ca68a355a6f554650~tplv-goo7wpa0wc-image.image) </span> |
   ||Allow comments |Set whether to allow comments in the file. ||
   

5. Select the target database and table for import.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3ae25eed79a44311b8e605f5c97be901~tplv-goo7wpa0wc-image.image) </span>

6. Define the schema mapping. After setting the data source and target table, the system automatically populates the schema mapping table to generate the mapping between the data source and target table. ByteHouse currently supports the following schema mapping configuration operations. You can adjust the generated schema mapping as needed.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/449645a1f2fa4aa1bd921ecdd45d8e86~tplv-goo7wpa0wc-image.image) </span>

   * **Adjust the schema mapping logic**

      If the generated schema does not meet expectations or you need to adjust the mapping between source and target columns, you can click **Re\-parser** to re\-parse the system.

   * **Adjust the target table**

      You can open a new browser tab, go to the [Database page](https://console.byteplus.com/bytehouse/region:bytehouse+ap-southeast-1/n/default/database) to adjust the target table. After adjusting, click **Refresh target table** in the **Define Schema Mapping** module on the data loading page. The system will automatically read the target table adjustments and update the Schema mapping table.

   * **Configure date parsing format**

      `yyyy-MM-dd'T'HH:mm:ss` (the default time format in Java). Note that the date (year\-month\-day) and time (hours\-minutes\-seconds) are separated by the constant `T`. If your data uses other formats, manual configuration is required. For configuration steps, please see [How to configure date parsing format?](https://docs.byteplus.com/docs/bytehouse/faq#ae91a828).

   * **Configure timezone**

      If the data you need to import contains fields with dates that include time zone information, refer to [How to configure timezone?](https://docs.byteplus.com/docs/bytehouse/faq#b08d5e59) to adjust the data format and avoid time zone import exceptions.

7. Configure the load type and virtual warehouse for the loading job. You can select either incremental write or full overwrite as needed.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ae27d7b4499d4a56bab2de7d9a5c24dc~tplv-goo7wpa0wc-image.image) </span>

   * **Append data**: Each job execution adds data incrementally to the target table without overwriting existing data.

   * **Overwrite**: Replace the entire target table with the latest data. You can choose either partition\-level overwrite or full data replacement. Before choosing partition overwrite, confirm that the target table has a partition key defined.

   * **Virtual warehouse**: Select a virtual warehouse from the dropdown list. Before use, make sure you have the USE privilege of this virtual warehouse.

8. Click **Create** to create the loading job. After creation, follow the instructions in [Start a job](https://docs.byteplus.com/docs/bytehouse/docs-ad-hoc-file-upload#5fc60a17) to import the data into ByteHouse’s target table.


<span id="5fc60a17"></span>
# Start a job


1. After creating the data loading job, the system will redirect to the job details page. The job will be paused at this point. You can click **Start** to start the job.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bad1a32108d940ad9f37a74d0ac9e2e6~tplv-goo7wpa0wc-image.image) </span>

2. In the **Start File Job** popup window, select the file upload path and click **OK**. The system will execute the data loading job.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8cf9cbb6cc84448b9a023ec09351143e~tplv-goo7wpa0wc-image.image) </span>

   * **Sample Path**: Use the file uploaded when creating the import job to import data.

   * **Upload A New File**: If you have new data to upload, you can choose to upload a new file. Ensure the file type and table schema match the original job configuration.


<span id="f48fa1b8"></span>
# View jobs

On the data loading page, you can view all created jobs through the job view.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b918afba971f4b949c522de5f771770d~tplv-goo7wpa0wc-image.image) </span>

You can also check the execution status, execution logs, and configurations in the execution view. You can query data once the job type shows a success state.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b3942247cc74d9296141543e1a3c301~tplv-goo7wpa0wc-image.image) </span>


* **View job execution logs**

   Click the **Log** button on the target job row to view the current job’s execution log. You can click to copy or download the log.

* **View configuration**

   Click the **Config** button in the target job row to view the current execution configuration of the job. You can click to copy or download the configuration JSON file for reference when importing data via OpenAPI.

* **Troubleshoot import job**

   To troubleshoot an imported job, click the **job name**, then click the **execution ID** under **Execution history** to check the loading status, error details, logs, and other information to help assess and optimize the import.


<span id="71bed580"></span>
# Start/Stop a job


1. In the job list, click the source type dropdown and select **File** to filter data loading jobs.

2. Click the **Start** button in the target job row to launch the current data loading job.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c4c79a666c884a709d89585553eef857~tplv-goo7wpa0wc-image.image) </span>

3. Click the **job name**, enter the job details page, where you can view job sync history, current Schema mapping, logs, and configuration.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e265df8c7fbe4642894538ce3d2f74e6~tplv-goo7wpa0wc-image.image) </span>

4. If you need to stop the data loading job, click **Stop**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aa64328cf8f74f26a0edb0e3cd3a5056~tplv-goo7wpa0wc-image.image) </span>


<span id="0d5b8794"></span>
# Edit a job


1. In the job list, click the source type dropdown and select **File** to filter data loading jobs.

2. Click the **Edit** button on the target job row to enter the file upload job configuration page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/da1d07f3f902401895e66391e3f35c64~tplv-goo7wpa0wc-image.image) </span>

3. Adjust the job configuration as needed, then click **Update** after editing.


<span id="a772f45a"></span>
# Copy job configuration

If you need to import data via OpenAPI, you can copy the job configuration as a reference.

**Steps**:


1. In the job list, click the source type dropdown and select **File** to filter import jobs.

2. Click the  **...**  button on the target job row and click **Copy Config**. The system will copy the current import job configuration.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c6890ff1b5bd476abf26ca319a15fb90~tplv-goo7wpa0wc-image.image) </span>


<span id="1a0b816e"></span>
# Delete a job

In the job list, click the  **...**  of the target job row button, click **Delete job**, and confirm to delete the current job.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8ca5729ca9ed403ab0fedb547308524e~tplv-goo7wpa0wc-image.image) </span>
