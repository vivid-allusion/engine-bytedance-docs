---
title: "Custom log"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Custom_log"
---

Custom log includes custom log query and custom log decryption.

<span id="c81d81f1"></span>
## Custom log query

You can use the APIs exposed by the SDK to query custom logs, including actively reported logs, logs reported with a crash, and recovered logs.

<span id="12332b6c"></span>
### Filter dimensions

You can filter data using the following filter criteria:

Time, Operating System, Event Type, DID, and User ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Supported event types: all event types, reported upon exception or crash, log recovery, and proactive reporting.</div>


<span id="5c936228"></span>
### Custom log file list

The query list displays the list of custom log files according to the filter criteria, and supports navigation from the upper right corner to the log recovery and log query pages for further querying and locating log content.

The Actions column provides a download feature that allows log files to be downloaded to your computer.

<span id="d20f71f9"></span>
### View log file details

In the log file list, click the log file name to view the file details.


|Feature |**DescriptionS** |
|---|---|
|Filter log |Supports filtering logs by time range, content keywords, log level, and log type.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The Harmony operating system only supports the <strong>custom log</strong> type and does not support the APMPlus log.</div><br> |
|Download current results |Log information filtered by conditions. Display the contents of all columns in the details page list using the `.txt` file.<br><br><br>* The content display format is [time][process: [thread message][level][identifier][log details]].<br><br>* The level column uses the first character of each level name as its abbreviation; for example, [I] stands for INFO. |
|Download log files |View the original file without considering any filter conditions. Use the `.txt` file to display the contents of all columns in the details page list.<br><br><br>* The content display format is [time][process: [thread message][level][identifier] log details].<br><br>* The level column is indicated by its initial letter. For example, [I] stands for INFO. |


Description of file details list parameters:


|**Parameters** |**DescriptionS** |
|---|---|
|Line number |The line where the log is located. |
|time |Report time, precise to the millisecond. |
|Process: Thread information |Processes and threads. |
|level |Log level. |
|Identifier |Customize some tags. Assign different values to different scenarios. |
|Log details |Detailed log information. |


<span id="6816c454"></span>
## Custom log decryption

Custom log decryption is used to decrypt and view encrypted custom log files.

Select the operating system, then click **Upload custom log**, and you can upload the encrypted log file.


* For Android operating system: Please upload the `.vlog` file. The custom log files for Android's `.vlog` are located in the `dada/data/包名/files/volc_log/logs` directory.

* Operating system is iOS: Please upload the `.alog` file.

* The operating system is Harmony: Please upload the `.hot` file.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you need to upload multiple encrypted files, you can compress them into <code>.zip</code> format before uploading.</div>


After the encrypted log is uploaded successfully, the operating system automatically decrypts it. You can view the log file name, start and end time, and log size, and you can also download the log file in `.txt` format from the Actions column.

Click the log file name, or check multiple logs and then click **View selected log details** to view the decrypted log details.
