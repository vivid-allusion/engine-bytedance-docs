---
title: "Create a migration task - use public network"
product: "Data Migration Service"
product_code: "dms"
source: "https://docs.byteplus.com/en/docs/dms/Create-a-migration-task"
---

This article describes how to use the public network to create a migration task in the DMS console.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background Information

The DMS supports the following source cloud service providers or data source types:


* Aliyun

* Tencent Cloud

* Huawei Cloud

* Qiniu Cloud

* Kingsoft Cloud

* Google Cloud

* Other S3 protocol object storage

* Object Storage \- BytePlus


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The DMS only supports data migration between tos buckets in the same region.</div>


When migrating files, HTTP standard attributes are migrated by default, including Content\-Type, Content\-Disposition, Content\-Encoding, Content\-Language, Cache\-Control, and Expires.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite


* Before using DMS, make sure that you have signed up for BytePlus. For more information, refer to [Signing up for BytePlus accounts](https://docs.byteplus.com/byteplus-platform/docs/signing-up-your-account).

* Obtained relevant information from the data source, such as AccessKey ID and Secret AccessKey for access, Endpoint, bucket name, etc.

* Created a storage bucket in object storage. For specific steps, please refer to [Creating a Bucket](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket).


<span id="qPdq2vWs"></span>
## Notes

If the source bucket has versioning enabled, DMS only migrates the latest versions of objects to the target bucket and does not migrate previous versions.

<span id=".5Yib5bu66L-B56e75Lu75Yqh"></span>
## Create a migration task


1. Log on to the [DMS console ](https://console.byteplus.com/dms).

2. On the **Migration task list** page, click **Create migration task**.

3. On the **Select network** page, configure the following parameters.

   
   |Parameters |Description |
   |---|---|
   |Task name |Specify the name of the migration task, following the naming rules below:<br><br><br>* Between 3 and 32 characters.<br><br>* Can only contain lowercase letters, numbers, and hyphens (\-).<br><br>* The name cannot start or end with a hyphen (\-). |
   |Network type |Defaulted to **Public Network**. |
   

4. Click **Next step: Set up source and destination**, and configure the following source and destination parameters.

   * When the **Source type** is **Object Storage**, the following parameters need to be configured

      
      |Parameters ||Description |
      |---|---|---|
      |Source type ||**Source type** in this scenario is selected as **Object Storage**. |
      |Data source ||Select specific data source:<br><br><br>* **Alibaba Cloud**: Migrate data from Aliyun to Torch Object Storage.<br><br>* **Tencent Cloud**: Migrate data from Tencent Cloud to Torch Object Storage.<br><br>* **Huawei Cloud**: Migrate data from Huawei Cloud to Torch Object Storage.<br><br>* **Qiniuyun**: Migrate data from Qiniuyun to Torch Object Storage.<br><br>* **Kingsoft Cloud**: Migrate data from Kingsoft Cloud to Torch Object Storage.<br><br>* **Google Cloud**: Migrate data from Google Cloud to Torch Object Storage.<br><br>* **Other S3 protocol storage**: Any object storage compatible with the S3 protocol and supporting AWS Signature V4 authentication can be used.<br><br>* **Object Storage \- BytePlus**: Migrate data from BytePlus Torch Object Storage to BytePlus Torch Object Storage in the same region.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When the <strong>Data source</strong> is <strong>Object Storage \- BytePlus</strong>, the destination can only select a storage bucket in the same region as the source.</div><br> |
      |Access Key ID ||AccessKey ID for accessing the source end object storage. |
      |Access Key Secret ||AccessKey Secret for accessing the source end object storage. |
      |Source bucket name ||Specify the name of the source end object storage bucket to be migrated. |
      |Source Region ||Specify the region where the source end object storage is located. |
      |Endpoint ||Specify the access domain name of the source endpoint object storage, and enter http:// or https:// before the address.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Do not include the bucket name in the endpoint, otherwise it will cause the source connection to fail.</div><br> |
      |Specify migrate scope |Include<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The include and exclude functions are mutually exclusive.</div><br> |After enabling the **Specify migrate scope** feature, you can specify the scope of object migration, supporting the specification of the migration scope by specifying objects or object prefixes.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When specifying objects or object prefixes using an upload file or a download URL, the line breaks in the list file must be \n.</div><br><br><br><br>* **Prefix**<br><br>   Support the following three ways to specify the object prefix, as described below:<br><br>   * **Specify Prefix**: Enter the prefix of the target object, click **Add Field** to set multiple prefixes, and support setting up to 10 object prefixes at most. For example, if you want to migrate all objects under the user/data directory in the source bucket, you need to set the object prefix as user/data/. If you want to migrate all files with the prefix event in the source bucket, you need to set the object prefix as event.<br><br>   * **Upload file**: If you need to migrate a large number of objects, you can record the object prefixes in a file, and then upload the list file to the console. The constraints for the list file are as follows:<br><br>      * The uploaded list file must be in txt format.<br><br>      * Each line in the list file is an object prefix, please enter multiple object prefixes on separate lines.<br><br>      * The number of prefixes in the list file cannot exceed 100,000.<br><br>      * The size of the uploaded list file cannot exceed 1GB.<br><br>      * The object prefix in the list file needs to comply with the UTF\-8 encoding rules.<br><br>   * **Download address**: Record the object prefixes in a list file, then fill in the public access address of the object prefix list file with a signature that is valid. If your object prefix list file is too large to be uploaded via browser, you can save the list file to object storage and fill in the public access address of the list file in the object storage.The constraints for the list file are as follows:<br><br>      * The uploaded list file must be in txt format.<br><br>      * Each line in the list file is an object prefix, please enter multiple object prefixes on separate lines.<br><br>      * The number of prefixes in the list file cannot exceed 100,000.<br><br>      * The size of the uploaded list file cannot exceed 1GB.<br><br>      * The object prefix in the list file needs to comply with the UTF\-8 encoding rules.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When specifying object prefixes, spaces are not supported within the prefix.</div><br><br><br><br>* **Object**<br><br>   Support the following three ways to specify objects, as explained below:<br><br>   * **Manual input**: Please enter the full path of the object name, excluding the bucket name. Each line can only contain one object name. If there are multiple objects, please input them on separate lines. You can input up to 1000 objects. For example, if the object flower.png is located under bucket A in the path user/data, you should fill in user/data/flower.png.<br><br>   * **Upload file**: If you need to migrate a large number of objects, you can record the names of the objects in a file, and then upload the list file to the console. The constraints for the list file are as follows:<br><br>      * The uploaded list file must be in txt format.<br><br>      * Each line in the list file is an object name, please enter multiple objects on separate lines.<br><br>      * The uploaded list file size cannot exceed 1GB.<br><br>      * The object names in the list file need to comply with the UTF\-8 encoding rules.<br><br>   * **Download address**: Record the names of the objects in a list file, and then fill in the public access address of the object list file with a signed object list file that is valid. If your object list file is too large to be uploaded via browser, you can save the list file to object storage and fill in the public access address of the list file in the object storage. The constraints for the list file are as follows:<br><br>      * The uploaded list file must be in txt format.<br><br>      * Each line in the list file is an object name, please enter multiple objects on separate lines.<br><br>      * The uploaded list file size cannot exceed 1GB.<br><br>      * The object names in the list file need to comply with the UTF\-8 encoding rules.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">When specifying object names, spaces are not allowed within a single object name.</div><br><br><br>* <div data-tips="true" data-tips-type="default">if you wish to rename a file, you can use the format:<strong>original_object_name new_object_name</strong> (separated by a single space).For example, entering a.jpg b.jpg will rename the file a.jpg to b.jpg.</div><br> |
      ||Exclude |After enabling the **Specify migrate scope** feature,You can exclude specified objects and only migrate the remaining objects after exclusion. Currently, only exclusion of objects by object prefix is supported.Support the following three ways to specify object prefixes, as described below:<br><br><br>* **Specify Prefix**: Enter the prefix of the input object, click on **Add Field** to set multiple prefixes, supporting up to 10 object prefixes. For example, to exclude all objects under the user/data directory in the source bucket, you need to set the object prefix to user/data/, and to exclude all objects with the prefix event in the source bucket, you need to set the object prefix to event.<br><br>* **Upload file**: If you need to exclude a large number of objects, you can record the prefixes of the objects to be excluded in a file, and then upload the list file to the console. The constraints for the list file are as follows:<br><br>   * The uploaded list file must be in .txt format.<br><br>   * Each line in the file should contain one object prefix; multiple prefixes must be entered on separate lines.<br><br>   * The file size must not exceed 5 MB.<br><br>   * The number of prefixes in the file must not exceed 5,000.<br><br>   * All object prefixes in the file must comply with UTF\-8 encoding.<br><br>* **Download address**: Record the excluded object prefixes in a list file, then fill in the public access address of the object prefix list file with a signature that is valid. If your object prefix list file is too large to be uploaded via a browser, you can save the list file to object storage and fill in the public access address of the list file in the object storage.The constraints for the list file are as follows:<br><br>   * The uploaded list file must be in .txt format.<br><br>   * Each line in the file should contain one object prefix; multiple prefixes must be entered on separate lines.<br><br>   * The file size must not exceed 5 MB.<br><br>   * The number of prefixes in the file must not exceed 5,000.<br><br>   * All object prefixes in the file must comply with UTF\-8 encoding.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">When specifying object prefixes, spaces are not allowed within the prefix.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">When using an uploaded file or a download URL to specify object prefixes, line breaks in the list file must be \n .</div><br> |
      

   * When the **Source type** is **URL list**, the following parameters need to be configured:

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">The file size corresponding to each URL in the URL list file must not exceed 300 GB.      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">The length of each line (i.e., each URL) in the URL list must not exceed 65,536 characters (64 KB).      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Only URL list files encoded in UTF\-8 are supported.      </div>
      

      
      |Parameters |Description |
      |---|---|
      |Source type |**Source type** in this scenario is selected as **URL list**. |
      |Upload URL list file |Choose the upload method for the URL list file:<br><br><br>* **Manual input**: Directly enter the file URL, with the following constraints and limitations:<br><br>   * It should start with http:// or https:// and needs to include a URL.<br><br>   * Each line can only contain one URL. Please enter multiple URLs on separate lines. Up to 1000 URLs are supported.<br><br>* **Upload file**: If you have a large number of files to migrate, you can record the URLs in a file and then upload the file to the console. The file constraints are as follows:<br><br>   * The uploaded file must be in txt format.<br><br>   * Each line in the file is a URL that needs to be migrated. Please enter multiple URLs on separate lines.<br><br>   * The file size cannot exceed 1GB.<br><br>* **Download address**: If your URL list file is large and not suitable for uploading via a browser, you can save the URL list file to an object storage and then select the **Download address**. Fill in the URL access address of the list file in the object storage. There are two ways to obtain the download address:<br><br>   * **Select file list**: Set the **Source Data Authorization Pattern,**  select the **Source bucket name** and **source filename**, and DMS will read the corresponding bucket list and files.<br><br>      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div><br>      <br><br>      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Only when the source data source is an object storage bucket under the current BytePlus account, and the source bucket is located in the same region as the destination bucket, can data be migrated using the file list method.      </div><br>      <br><br>   * **Fill in the access address**: Please provide the public access address of the URL list file with a valid signature and the signature is still within the validity period.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When using an uploaded file or a download URL to specify object prefixes, line breaks in the list file must be \n.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When migrating data using <strong>Manual input</strong> or <strong>Upload file</strong>, the URL path (the part after the domain name /) is used as the name of the object by default. If you want to rename the file, you can do so by using <strong>URL</strong> + <strong>space</strong> + <strong>object file name</strong>. For example, you can rename the file <code>a.jpg</code> to <code>b.jpg</code> by using <code>http://xxx.xxx.xxx/xxx/a.jpg b.jpg</code>.</div><br> |
      

   * Setting destination parameters

      
      |Parameters |Description |
      |---|---|
      |Destination type |Destination endpoint type, currently only supports Torch Object Storage. |
      |Destination write mode |Select the target writing mode, with the following parameter descriptions:<br><br><br>* **Classic mode**: Use AccessKey ID, AccessKey Secret, and other information to migrate data.<br><br>* **Cross\-service Authorization**: You can migrate the object storage buckets under the current account using cross\-service authorization mode without filling in detailed information such as AccessKey ID and AccessKey Secret.With your authorization, the data migration service can directly read the list of storage buckets and files.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If you use a sub\-account to create a migration task and select <strong>Cross\-service Authorization</strong>, you need to grant the sub\-account permission to create IAM policies. For detailed instructions, please refer to <a href="https://docs.byteplus.com/docs/dms/Migration-issues">Migration Issues</a>.</div><br> |
      |Access Key ID |AccessKey ID used to access the destination endpoint object storage. |
      |Access Key Secret |AccessKey Secret for accessing the destination endpoint object storage. |
      |Destination bucket name |The bucket name of the destination object storage is specified.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If the <strong>Data source</strong> is <strong>Object Storage \- BytePlus</strong>, the destination bucket must be in the same region as the source bucket.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">You need to ensure that the current account has permissions for HeadBucket, HeadObject, PutObject, ListObjects, CreateMultipartUpload, AbortMultipartUpload, CompleteMultipartUpload, and UploadPart on the target bucket, otherwise it may result in migration outcomes that do not meet expectations.</div><br> |
      

5. Click **Next step: Set task parameters** and configure the following task parameters.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Click <strong>Next step: Set task parameters</strong> , the system will automatically verify the source connection information. If the information you set is incorrect, a permission pre\-check prompt dialog will pop up, indicating that the source or destination permissions are insufficient. Continuing to create the task may result in migration results that do not meet expectations.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When the <strong>Source type</strong> is <strong>URL list</strong>, only <strong>Skip archive object</strong>, <strong>Skip failed object</strong>, <strong>Range\-Get migration</strong>, <strong>Coverage policy</strong>, <strong>File storage method</strong>, <strong>Flow control</strong>, and <strong>Sampling verification</strong> parameters can be configured on the task settings page.   </div>
   

   
   |Parameters |Description |
   |---|---|
   |Migrating delta files |By default, it is turned off. After turning it on, you can customize the incremental migration parameters. The parameter explanations are as follows:<br><br><br>* incremental migration interval: After the stock migration (i.e., initial migration) is completed, how often should the incremental migration task be initiated, in hours? Only integers from 1 to 24 are supported.<br><br>* incremental migrations: After the completion of stock migration (i.e., the initial migration), the number of times for incremental migration is only supported for integers ranging from 1 to 100. |
   |Skip archive object |Enable or disable skipping archived objects. By default, it is enabled. Explanation as follows:<br><br><br>* Enable **Skip archive object**: When migrating data, files of storage types with delayed access are not migrated.<br><br>* Disable **Skip archive object**: When migrating data, migrate thawed files of the archival storage type and do not migrate unfrozen files of the archival storage type.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The latency access storage types for each data source are as follows:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Alibaba Cloud: Archive, Cold Archive</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Tencent Cloud: ARCHIVE, DEEP ARCHIVE</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Huawei Cloud: COLD, DEEP ARCHIVE</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Qiniu Cloud: Archive, Deep Archive</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Kingsoft Cloud: Archive</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Other S3 protocol object storage: GLACIER, DEEP ARCHIVE</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Object Storage \- BytePlus: ARCHIVE, COLD ARCHIVE</div><br><br><br><br><div data-tips="true" data-tips-type="tip">Google Cloud's Cloud Storage does not have a delayed access storage type. If your data source is Google Cloud, there is no need to set the skip archive object parameter.</div><br> |
   |Skip failed object |When migrating the source\-side object, if there is no permission for the source\-side object, the migration will fail.You can set whether to **Skip failed object**, which is enabled by default. The explanation is as follows:<br><br><br>* Enable **Skip failed object**: No matter how many objects fail during the migration process, the migration task will not be paused.<br><br>* Disable **Skip failed object**: If there are 20 consecutive migration failures during the migration process, the task will be paused and marked as failed. |
   |Range\-Get migration |Set whether to enable **Range\-Get migration**, which is disabled by default. After enabling **Range\-Get migration**, DMS will support the migration of files using resumable file transfer. This means that if the file transfer is interrupted due to network fluctuations or other reasons, DMS will resume the transfer from the breakpoint, avoiding the need to transfer the file from the beginning and saving costs.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">The setting of the <strong>Range\-Get migration</strong> parameters is only supported when the source type is a <strong>URL list</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Before enabling <strong>Range\-Get migration</strong>, please make sure that the source supports range\-get migration, otherwise the <strong>Range\-Get migration</strong> feature will not take effect.</div><br> |
   |File rename |By default, it is turned off. After turning it on, you can set the file renaming rules. File renaming supports regular expression replacement. You can input the regular expression rules that need to be renamed and the string that needs to be replaced. For example:<br><br><br>* Add prefix prefix\-path/: need to set the regular expression to ^, replace the text with prefix\-path/.<br><br>* Replace the prefix prefix\-old/ with prefix\-new/: Set the regular expression as ^prefix\-old/ and replace the text with prefix\-new/.<br><br>* Remove prefix prefix\-old/: You need to set the regular expression to ^prefix\-old/, and replace the text with an empty string.<br><br>* Change the file extension from .txt to .csv: You need to set the regular expression as .txt$, and replace the text with .csv.<br><br>* Change the file name from abc.jpg to aaa.jpg: You need to set the regular expression as "abc" and the replacement text as "aaa". |
   |List with delimiter |Due to the configuration of some source\-side storage buckets (such as enabling bucket acceleration), TOS can only retrieve files at the top level directory of the source\-side storage bucket. Listing with a delimiter can retrieve files under multiple levels of directories, as explained below:<br><br><br>* Enable **List with delimiter**: TOS can access files under multiple levels of directories in the source storage bucket, ensuring the integrity of files migrated to TOS.<br><br>* Disable **List with delimiter**: The migration speed of files is faster, but there may be a problem of incomplete migration to TOS when bucket acceleration is enabled in the source object storage.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If the <strong>List with delimiter</strong> feature is enabled, the migration scope is set to "Include", and the migration scope is specified via prefixes (including directly specified prefixes, uploaded files, or download URLs), then each prefix must end with a forward slash (/).</div><br><br><br>* <div data-tips="true" data-tips-type="warning">When listing objects in the source bucket, if the bucket does not return objects in lexicographical (dictionary) order, it may result in incomplete listing results or even an infinite listing loop, which can prevent the migration task from completing successfully.</div><br> |
   |Coverage policy |You can specify the overwrite policy when there are files with the same name on the source and destination sides. The policy is explained as follows:<br><br><br>* **Replace all**: For files with the same name, no judgment is made and the source side directly overwrites the destination side.<br><br>* **Uncovered**: For files with the same name, no judgment is made and they are skipped directly.<br><br>* **Overwrite according to last modified time**: When there are files with the same name on the source and target ends, the decision to overwrite is based on the `lastmodify` field (last modification time) of the files. Overwriting will only be performed if the last modification time of the source file is later than the last modification time of the target file. |
   |Ignore target back\-to\-source |When the migration task uses a **Uncovered** overwrite policy, DMS checks whether the files to be migrated already exist in the destination. If the destination bucket has HeadObject request pass\-through (origin\-fetching) enabled and the source contains the file to be migrated, DMS will incorrectly determine that the file already exists in the destination bucket and skip migrating it, resulting in fewer files being migrated than expected.<br><br>After enabling the **Ignore target back\-to\-source** option, DMS bypasses the origin\-fetching rules configured on the destination bucket and proceeds with migrating the file directly. It is recommended to enable this option when using the "Do Not Overwrite" policy and the destination bucket has origin\-fetching rules enabled. |
   |Object storage type |Set the file migration to the storage type of TOS, which supports selecting to **All using standard storage**,**Keep original storage type**, **All using Infrequent Access Storage**, **All** **useing Archive Flashback Storage**, **All using Intelligent Tiered Storage**, **All** **use Archive, All using Cold Archive**, **All** **using Deep  Cold Archive**. For detailed information about TOS storage types, please refer to [Storage Type](https://docs.byteplus.com/en/docs/tos/docs-storage-type). The parameter descriptions for Keep the original stored properties and All using intelligent tiered storage are as follows:<br><br><br>* **Keep original storage type**: When migrating to TOS, set the storage type of the files according to the corresponding relationship between S3 and TOS. For more information, please refer to [Mapping between S3 and TOS during data migration](https://docs.byteplus.com/docs/dms/Mapping-between-S3-and-TOS-during-data-migration).<br><br>* **All using Intelligent Tiered Storage**: When migrating to TOS, files will be saved to the intelligent tiering high\-frequency access layer.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Depth cold archive is currently in the invitation testing phase at TOS. If you want to set the file storage type for migration to TOS as depth cold archive, please contact your account manager to enable it.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If the migration source belongs to the delayed access storage type, please convert the status of this type to immediate access before migration, otherwise the migration source will fail.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If the availability zone attribute of the destination is different from that of the source files, the destination will be considered as the default.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the <strong>Source typ</strong>e is a <strong>URL list</strong>, The File storage method method will not support <strong>Keep the original storage type</strong>.</div><br> |
   |Migration file start time |Files are filtered for migration based on their last modification time. By default, all files are migrated. The parameter options are described below:<br><br><br>* **Migrate all**: Migrates all files in the source bucket.<br><br>* **Specify time range**: Filters files to be migrated using one of the following three modes:<br><br>   * Start Time Only: Specify only the start date, leaving the end date empty. This migrates only files whose last modification time is later than the specified start date.<br><br>   * End Time Only: Specify only the end date, leaving the start date empty. This migrates only files whose last modification time is earlier than the specified end date.<br><br>   * Time Range: Specify both start and end dates. This migrates only files whose last modification time falls within the specified time range (inclusive). |
   |Flow control |By default, it is turned off and the default speed when turned off is 1024MB/s.<br><br>Open the **Flow control**, click **Add Field**, and you can set the flow control period and maximum rate for the migration task. The rate limitation is explained as follows:<br><br><br>* The maximum speed is set to 100MB/s by default.<br><br>* The maximum speed setting range is 1MB/s to 1024MB/s. |
   |Sampling verification |Disable **Sampling verification** by default.After enabling **sampling verification**, DMS will retrieve 100 bytes of each object from the source end and 100 bytes of the corresponding object from the target end, and then perform verification to ensure the consistency of data between the source end and the target end. For detailed information about sampling verification, please refer to [Data consistency verification](https://docs.byteplus.com/docs/dms/Data-consistency-verification).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Using the sampling verification function will generate additional outbound traffic on the source end of the public network, and the corresponding fee will be charged by the source end object storage.</div><br> |
   

6. Click **Next: Confirm task information** to review the migration task parameters on this page.

7. After confirming the parameters, read and select **Storage product and service terms**, then click **Submit**.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After submission, a <strong>fee reminde</strong>r dialog box will pop up. The storage migration service itself does not incur any charges, but migrating data from the public network to BytePlus will generate public network traffic costs, which will be charged by the storage service provider of the source site.   </div>
   

8. In the **Fee reminder** dialog box, click **Known,Next step**.

9. (Optional) If you have selected **Cross\-service Authorization**, you will also need to click **OK** in the pop\-up **Cross\-service Authorization** dialog box.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the task is created, it will start automatically. You can view the creation time and status of the task in the <strong>Migration task</strong> list. In addition, you can click on the custom list field icon in the upper right corner of the <strong>Migration task</strong> list page, select <strong>Storage migration progress</strong> and <strong>Number of files migrating progress</strong>, and view the migration progress.   </div>
