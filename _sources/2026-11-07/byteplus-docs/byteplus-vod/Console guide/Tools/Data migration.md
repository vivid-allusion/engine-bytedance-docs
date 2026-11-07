---
title: "Data migration"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-data-migration"
---

BytePlus VOD provides a data migration tool for importing media assets from source URLs or TOS buckets into a VOD space. This guide describes how to prepare a migration, configure its source and destination, and check the results in the console.

<span id="migration-methods"></span>
## Migration methods


|Method |Source configuration |When to use |
|---|---|---|
|URL migration |Upload a CSV file containing the source URLs and optional media metadata. |Import files that can be retrieved through URLs, including files hosted by other cloud providers. |
|TOS bucket migration |Select the source bucket and the files to migrate. |Import all files or a filtered set of files from a TOS bucket. |


<span id="billing"></span>
## Billing

The data migration tool itself is free of charge. The source service may charge for API requests and outbound traffic. For TOS migration, transfers within the same region use the internal network, and transfers from other regions incur public network transfer charges. Check the source service's pricing before starting a task. The cost of a migration can usually be estimated with the following formula: `Migration cost = (number of source API calls × API call price) + (total data volume × outbound traffic price)`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">The rates below are illustrative only. Use the actual rates published by your source service.</div>


For example, to migrate 500 GB of data from a source provider that charges USD 0.01 per 10,000 API calls and USD 0.50 per GB of outbound traffic:

```Plain Text
API call cost     = 30,000 calls × (USD 0.01 ÷ 10,000) = USD 0.03
Outbound traffic  = 500 GB × USD 0.50/GB               = USD 250.00
Total             = USD 0.03 + USD 250.00              = USD 250.03
```


<span id="prerequisites"></span>
## Prerequisites


* Prepare a target VOD space in **Asia Pacific (Johor)** .

* For URL migration, prepare a CSV file as described in [Prepare a CSV file](https://docs.byteplus.com/en/docs/25/114204#prepare-a-csv-file).

* For TOS migration, ensure that you have access to the source bucket.

* If you want to transcode the imported media automatically, prepare a [workflow](https://docs.byteplus.com/docs/byteplus-vod/docs-workflow) in the target space.


<span id="create-a-migration-task"></span>
## Create a migration task


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and choose **Tools** \> **Data migration**.

2. Click **Create a new migration task**.

3. Enter a unique **Migration task name**, up to 64 characters.

4. Configure the [migrate source](https://docs.byteplus.com/en/docs/25/114204#configure-the-migrate-source).

5. Configure the [migration target](https://docs.byteplus.com/en/docs/25/114204#configure-the-migration-target).

6. Click **Save** and review any confirmation shown by the console. The task appears in the list and runs asynchronously.


<span id="configure-the-migrate-source"></span>
### Configure the migrate source

<span id="configure-a-url-source"></span>
#### Configure a URL source

Select the URL option under **Service provider**, then configure the following fields:


|Console field |Configuration |
|---|---|
|**Service provider** |Select **URL**. |
|**Upload space** |Select the space in which to store the CSV file. This is the storage location for the CSV, not the destination for the imported media. |
|**URL upload** |Click **Select CSV file** and upload the prepared CSV file. To change the upload space after uploading a CSV, remove the uploaded CSV from the form first. |
|**Skip HLS integrity check** |When off (the default), the migration verifies that each TS segment referenced by an M3U8 file exists and is not empty; if the check fails, the M3U8 file fails to migrate. When on, the migration skips this check and imports the M3U8 file without validating its TS segments. |
|**Transfer concurrency limit** |Optionally limit the number of files being migrated at the same time. This setting controls concurrency, not requests per second. It is off by default. |


<span id="configure-a-tos-source"></span>
#### Configure a TOS source

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">Migrating from a TOS bucket into a VOD space that has an <a href="https://docs.byteplus.com/docs/byteplus-vod/process-media-files-stored-in-tos-buckets">associated TOS bucket</a> is not supported.</div>


Select the TOS option under **Service provider**, then configure the following fields:


|Console field |Configuration |
|---|---|
|**Bucket location** |Select the source bucket's region. Available options include Beijing, Guangzhou, Shanghai, Hong Kong, Johor, and Jakarta. |
|**Select bucket** |Select the source bucket. |
|**File migration method** |Choose **Full migration**, **Migrate only matching files**, or **Only migrate files that match regular expressions**. For matching files, enter the source path prefixes, one per line, without the bucket name. For regular expressions, enter one expression per line; a file is selected if it matches any expression. |
|**Skip HLS integrity check** |When off (the default), the migration verifies that each TS segment referenced by an M3U8 file exists and is not empty; if the check fails, the M3U8 file fails to migrate. When on, the migration skips this check and imports the M3U8 file without validating its TS segments. |
|**Time frame** |Leave off to include existing files without a specified time window. Turn on to migrate files added or changed within the selected start and end dates. |
|**Transfer concurrency limit** |Optionally limit the number of files migrated simultaneously. |


<span id="configure-the-migration-target"></span>
### Configure the migration target


|Console field |Configuration |
|---|---|
|**On\-demand region** |The destination region is the current VOD region, **Asia Pacific (Johor)** . |
|**Target space** |Select the VOD space to receive the imported media. |
|**In\-bucket path settings** |**Use the path in the URL in the bucket** retains the source path. **Ignore the path in the URL** removes the directory prefix and keeps only the filename. For URL migration, a CSV `FileName`, when supplied, is used as the base path. |
|**Save path** |Choose **Save to root directory** or **Save to the specified directory**. A specified directory must not contain whitespace, `%`, `+`, `?`, `,`, `&`, `，`, or `#`. |
|**File with the same name** |**Cover** replaces a file at the same destination path. **Skip** preserves the existing file and skips the incoming file. |
|**Automatic transcoding** |Choose **Direct upload without transcoding** or **Upload and automatically transcode**. For automatic transcoding, select a workflow in the target space. |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>



* <div data-tips="true" data-tips-type="warning"><strong>Overwriting files</strong>: The <strong>Cover</strong> option requires the target space to allow overwrite uploads. If overwrite uploads are disabled, an incoming file with an existing destination path can fail. Check the target space configuration before migrating files with duplicate paths.</div>


* <div data-tips="true" data-tips-type="warning"><strong>Default workflow</strong>: If the target space has a <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-workflow#a4c2517e">default workflow</a>, it still runs when you select <strong>Direct upload without transcoding</strong>. Check the space's default workflow before starting the migration.</div>



<span id="manage-migration-tasks"></span>
## Manage migration tasks

The task list shows the migration task name, status, file source, start time, and available actions.


|Action |Description |
|---|---|
|View details |Click **Details** to inspect progress, successful, failed, and skipped file counts, migrated data size, source settings, and destination settings. |
|Pause or resume |Pause an active task and resume it using the action shown in the task list. Completed tasks cannot be paused. |
|Export results |Open **More** and select **Export migration Success list**, **Export migration Fail list**, or **Export migration Skip list**. Use the failed\-file list to investigate migration failures. |
|Delete a task |Choose **More** \> **Delete**. Deleting a completed task removes its task records without deleting the media already migrated. |


Check the failed and skipped counts as well as the overall task status. If files fail, review source accessibility, destination path conflicts, overwrite permissions, and HLS integrity as applicable. Verify the imported media in the target space.

<span id="reference-information"></span>
## Reference information

<span id="prepare-a-csv-file"></span>
### Prepare a CSV file


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and choose **Tools** \> **Data migration**.

2. Click **Create a new migration task** and select **URL** as the service provider.

3. Click **Download template file** and fill in the CSV file. Keep the column names unchanged.

   
   |Column |Required |Description |
   |---|---|---|
   |`SourceUrl` |Yes |URL of the source media file. |
   |`Title` |No |Media title. |
   |`ClassificationId` |No |Category ID for the media. Use a category in the target space. For information about creating categories, see [CreateVideoClassification](https://docs.byteplus.com/docs/byteplus-vod/reference-createvideoclassification). |
   |`FileName` |No |Custom destination file path. If omitted, the source URL path is used. The task's path settings also affect the final path. See [Destination file paths](https://docs.byteplus.com/en/docs/25/114204#destination-file-paths). |
   |Additional columns, such as `Tags` |No |Use the corresponding parameter names from [UploadMediaByUrl](https://docs.byteplus.com/docs/byteplus-vod/reference-uploadmediabyurl), with one parameter per column. |
   


Only CSV files encoded in UTF\-8, GBK, or GB2312 are supported. Upload one CSV file per migration task.

<span id="estimate-migration-time"></span>
### Estimate migration time

Migration time depends on the number and size of files, source read speed, network conditions, destination write speed, and transfer concurrency. Regular\-expression filtering scans the source bucket and can take longer when the bucket contains many files.

The overall speed is limited by the slowest stage in the migration path. Assuming the source service is stable and network conditions are good, the following speeds can help you estimate migration time:


|Stage |Speed |
|---|---|
|Source read speed |Varies by source provider. The transfer speed is typically 1–10 Gbps, and read concurrency is 50–500. Migrating a large number of small files is limited by concurrency. |
|Migration transfer speed |The data migration task provides up to 10 Gbps of migration bandwidth. |
|Destination write speed |VOD storage supports a write speed of up to 10 Gbps and up to 500 concurrent writes. |


<span id="destination-file-paths"></span>
### Destination file paths

The base path depends on the migration method:


* **URL migration**: The CSV `FileName`, if supplied; otherwise, the path extracted from `SourceUrl`.

* **TOS migration**: The source object's key, excluding the bucket name.


The **In\-bucket path settings** option determines whether to retain that path or keep only its final filename. The **save path** option determines the destination directory.

The following examples use **Save to root directory**:


|Source |CSV `FileName` |Path setting |Destination path |
|---|---|---|---|
|URL: `https://example.com/a/b/video.mp4` |Empty |Retain path |`/a/b/video.mp4` |
|URL: `https://example.com/a/b/video.mp4` |Empty |Ignore path |`/video.mp4` |
|URL: `https://example.com/a/b/video.mp4` |`custom/demo.mp4` |Retain path |`/custom/demo.mp4` |
|URL: `https://example.com/a/b/video.mp4` |`custom/demo.mp4` |Ignore path |`/demo.mp4` |
|TOS object key: `a/b/video.mp4` |Not applicable |Retain path |`/a/b/video.mp4` |
|TOS object key: `a/b/video.mp4` |Not applicable |Ignore path |`/video.mp4` |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Avoid duplicate destination paths</div>


<div data-tips="true" data-tips-type="tip">Ignoring source directories can cause files from different directories to have the same destination filename. Review the <strong>File with the same name</strong> setting before starting the task.</div>
