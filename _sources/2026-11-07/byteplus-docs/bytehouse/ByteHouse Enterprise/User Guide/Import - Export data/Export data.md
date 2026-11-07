---
title: "Export data"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/export-data-ce"
---

ByteHouse supports creating data export jobs to export data to BytePlus Object Storage (Torch Object Storage, TOS) either once or regularly, facilitating your data analysis.

<span id="08a1d796"></span>
# Prerequisites

Prepare the following resources before using ByteHouse data export functions:


* TOS data source: create a TOS data source in ByteHouse. For details, see [Batch import](https://docs.byteplus.com/docs/bytehouse/batch-import).

* Create the storage bucket for data export in BytePlus TOS. For operation details, see [creating a bucket](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket).


<span id="d778850d"></span>
# Create a task


1. Log in to the ByteHouse console, click **Task center** at the top, then click **Cron tasks**. On the Cron tasks page, click **Create cron task** and select **Data Export Job**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d86a77671a0c4c0a9932c2ee8a8ed363~tplv-goo7wpa0wc-image.image) </span>

2. Configure data export task details.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d0635db8948944b0a0704596aa364aa7~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameters |Configuration description |
   |---|---|
   |Cluster |Select the cluster where you want to export the data. |
   |Task name |Custom task name. The name can only include letters, numbers, characters, spaces, underscores, and hyphens. |
   |Execution type |Supports export tasks based on a repeatable task or one\-time export tasks. |
   |Description |Custom task description. |
   |Cron expression |Use a Cron expression to configure the export task's execution time. After configuration, you can view the execution time corresponding to the Cron expression in the preview area.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If system resources are insufficient during export, scheduled tasks may queue due to too many pending tasks at the specified execution time, causing delays in the actual start time of the export task.</div><br> |
   

3. Enter the query SQL to specify the data you want to export.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/27b123543b4c4d1da9e1c3173e3967f4~tplv-goo7wpa0wc-image.image) </span>

4. Configure the data export job.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9e6ac5a6cbcd4c1193af362f4f8d82c8~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Configuration description |
   |---|---|
   |Export file name |Optional. Both specifying a custom file name and not specifying a file name are supported.<br><br><br>* **Custom file name**: The system will export only one file.<br><br>* **No file name specified**: Suitable for scenarios where the exported file is large. The system splits the exported file into several small files and names each file according to the `clickhouse_outfile_n.format` format. For example,<br><br>   ```Bash```<br>```   clickhouse_outfile_1.csv、clickhouse_outfile_2.csv、clickhouse_outfile_3.csv、...、clickhouse_outfile_n.csv```<br>```   ```<br>   <br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">When customizing file names, avoid assigning the same name to different exported files. If two export tasks generate files with the same name in the same export path, the system will automatically overwrite the existing file, and the existing file data cannot be recovered.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">For periodic export tasks, because the export file name and export path are configured identically, the export file generated in the next cycle will automatically overwrite the file from the previous cycle. Please process already exported files promptly.</div><br> |
   |Source type |Select the export target data source type; currently, only S3 is supported. |
   |Data source |Select the TOS data source already added in ByteHouse to establish a connection with the export target data source.<br><br>If you have not created a data source, click the **Create** button. The system will automatically redirect to the new data source page, where you can refer to [Batch import](https://docs.byteplus.com/docs/bytehouse/batch-import) to configure data source\-related information. |
   |Bucket |Select the target bucket to export data to. |
   |Path |Select the target storage path to which data will be exported. |
   |Format |The export format supports CSV, Parquet, and JSON.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Currently, the exported Parquet files from ByteHouse do not support exporting the <code>Date</code> data type as a date type; this type automatically converts to <code>Int</code> during export. If your data table contains columns of the <code>Date</code> type, you can add <code>toString</code> to the export SQL statement for manual conversion. For example,</div><br><br><br><div data-tips="true" data-tips-type="warning">```SQL```<br>```SELECT xx, xx, toString(toDate(xx)) FROM xx```<br></div><br> |
   |Settings |It is used to define export parameters and supports both single\-line and script editing. ByteHouse has built\-in default parameters, as follows:<br><br><br>* `s3_use_virtual_hosted_style`: It is used to configure the access method for the storage bucket. The default value is `1`, which means the bucket is accessed using Virtual Hosted Style. Currently, TOS only supports Virtual Hosted Style and does not support the path style access mode. You do not need to adjust this parameter when using TOS.<br><br>* `enable_optimizer`: It specifies whether to enable the optimizer. This parameter controls file splitting. The default value is 0. You do not need to change this parameter during use.<br><br>* `max_threads`: The maximum number of threads for processing export tasks. The default value is 1, which can prevent export failures caused by insufficient performance. It is recommended to use the default values. You may also adjust them as needed.<br><br>* `max_block_size`: Parameter that controls the size of data blocks for each write or transfer operation. The default value is 1024, measured in rows. It is recommended to use the default values, and you may also adjust them as needed.<br><br>* `max_execution_time`: Timeout period for export task execution, measured in seconds. You can configure this value as needed. The default is 1800 seconds, which is equivalent to 30 minutes. It is recommended to use the default values. You may also adjust them as needed. |
   

5. After configuration, click **Save**. The system automatically creates the task and displays "**Created cron task successfully**". You can click **Task information** on the prompt page to view the task configuration.

6. After the task is executed, click **Task name** to check the task status and details.

   * If the status shows "Success," the task completed successfully. Click the link button next to the export file name to open the corresponding folder in TOS, where you can find the exported file by its name.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d0ace9cb22c143c6ad6173acc3545934~tplv-goo7wpa0wc-image.image) </span>

   * If the status shows "failure", hover over "failure" to see the cause. After identifying the cause, you can refer to [Edit task](https://docs.byteplus.com/docs/bytehouse/export-data-ce#a0924c02) to adjust the task configuration accordingly and try running the task again.


<span id="a0924c02"></span>
# Edit task

In the cron task list, click the **Edit** button in the target task's row to modify the configuration. You can refer to the parameter descriptions in [Create a task](https://docs.byteplus.com/docs/bytehouse/export-data-ce#d778850d) for guidance.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fbe08fd7be3c42509558d380b80c5ff8~tplv-goo7wpa0wc-image.image) </span>

You can also click **Task name** to enter the task details page, then click the **Edit** button to adjust the task configuration.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fd0fea33ce7840b685035b474df01b76~tplv-goo7wpa0wc-image.image) </span>

<span id="88fabf05"></span>
# Pause task

If you created a periodic task, you can pause its execution.

In the scheduled task list, click **target task name** to enter the task details page, then click **Pause**.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/def93ffedb5b4eea9ce489270fe48533~tplv-goo7wpa0wc-image.image) </span>

<span id="f0022ec7"></span>
# Delete task

In the scheduled task list, click the **Delete** button in the target task row, then click **Delete** to remove the current task.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/370a10e586e74bd29c3bce2693eb7099~tplv-goo7wpa0wc-image.image) </span>

You can also click **Task name** to enter the task details page, then click the **Delete** button to delete the current task.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9fd1b5e535e14ef0b1f611f558900f36~tplv-goo7wpa0wc-image.image) </span>
