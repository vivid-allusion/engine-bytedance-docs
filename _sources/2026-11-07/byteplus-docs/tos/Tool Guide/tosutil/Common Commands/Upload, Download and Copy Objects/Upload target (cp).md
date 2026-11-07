---
title: "Upload target (cp)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Upload-object-cp"
---

You can upload local objects to TOS using the `cp` command.

<span id=".5ZG95Luk6K-t5rOV"></span>
## Command syntax


<Tabs>
<Tab zoneid="ra33vSb5" title="Linux/macOS">
<TabTitle>Linux/macOS</TabTitle>

* upload a single object


```Bash
./tosutil cp file_url tos://bucket[/key] [-dryRun] [-link] [-u] [-vchecksum] [-p=1] [-threshold=52428800] [-ps=auto] [-cpd=xxx] [-acl=xxx] [-sc=xxx] [-meta=aaa:bbb#ccc:ddd] [-sse=xxx] [-sseKeyId=xxx] [-contentType=xxx] [-contentDisposition=xxx] [-contentEncoding=xxx] [-contentLanguage=xxx] [-cacheControl=xxx] [-expires=xxx] [-arcDir=xxx] [-fr] [-o=xxx] [-bt=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```



* upload a folder


```Bash
./tosutil cp folder_url tos://bucket[/prefix] -r [-dryRun] [-link] [-u] [-vchecksum] [-flat] [-j=1] [-p=1] [-threshold=104857600] [-nfj=1] [-ps=auto] [-cpd=xxx] [-acl=xxx] [-sc=xxx] [-meta=aaa:bbb#ccc:ddd] [-sse=xxx] [-sseKeyId=xxx] [-contentType=xxx] [-contentDisposition=xxx] [-contentEncoding=xxx] [-contentLanguage=xxx] [-cacheControl=xxx] [-expires=xxx] [-include=*.xxx] [-exclude=*.xxx] [-timeRange=time1-time2] [-at] [-ddo] [-dmf] [-arcDir=xxx] [-o=xxx] [-bt=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```



* upload file list


```Bash
./tosutil cp file1_url,folder1_url|filelist_url tos://bucket[/prefix] -msm=1 [-r] [-dryRun] [-link] [-u] [-vchecksum] [-flat] [-j=1] [-p=1] [-threshold=104857600] [-nfj=1] [-ps=auto] [-cpd=xxx] [-acl=xxx] [-sc=xxx] [-meta=aaa:bbb#ccc:ddd] [-sse=xxx] [-sseKeyId=xxx] [-contentType=xxx] [-contentDisposition=xxx] [-contentEncoding=xxx] [-contentLanguage=xxx] [-cacheControl=xxx] [-expires=xxx] [-include=*.xxx] [-exclude=*.xxx] [-timeRange=time1-time2] [-at] [-ddo] [-dmf] [-arcDir=xxx] [-o=xxx] [-bt=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
<Tab zoneid="LnSrRnYO" title="Windows">
<TabTitle>Windows</TabTitle>

* Upload single object


```Bash
tosutil cp file_url tos://bucket[/key] [-dryRun] [-link] [-u] [-vchecksum] [-p=1] [-threshold=52428800] [-ps=auto] [-cpd=xxx] [-acl=xxx] [-meta=aaa:bbb#ccc:ddd] [-sse=xxx] [-sseKeyId=xxx] [-contentType=xxx] [-contentDisposition=xxx] [-contentEncoding=xxx] [-contentLanguage=xxx] [-cacheControl=xxx] [-expires=xxx] [-arcDir=xxx] [-fr] [-o=xxx] [-bt=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```



* Upload folder


```Bash
tosutil cp folder_url tos://bucket[/prefix] -r [-dryRun] [-link] [-u] [-vchecksum] [-flat] [-j=1] [-p=1] [-threshold=104857600] [-nfj=1] [-ps=auto] [-cpd=xxx] [-acl=xxx] [-meta=aaa:bbb#ccc:ddd] [-sse=xxx] [-sseKeyId=xxx] [-contentType=xxx] [-contentDisposition=xxx] [-contentEncoding=xxx] [-contentLanguage=xxx] [-cacheControl=xxx] [-expires=xxx] [-include=*.xxx] [-exclude=*.xxx] [-timeRange=time1-time2] [-at] [-ddo] [-dmf] [-arcDir=xxx] [-o=xxx] [-bt=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```



* Upload file list


```Bash
tosutil cp file1_url,folder1_url|filelist_url tos://bucket[/prefix] -msm=1 [-r] [-dryRun] [-link] [-u] [-vchecksum] [-flat] [-j=1] [-p=1] [-threshold=104857600] [-nfj=1] [-ps=auto] [-cpd=xxx] [-acl=xxx] [-meta=aaa:bbb#ccc:ddd] [-sse=xxx] [-sseKeyId=xxx] [-contentType=xxx] [-contentDisposition=xxx] [-contentEncoding=xxx] [-contentLanguage=xxx] [-cacheControl=xxx] [-expires=xxx] [-include=*.xxx] [-exclude=*.xxx] [-timeRange=time1-time2] [-at] [-ddo] [-dmf] [-arcDir=xxx] [-o=xxx] [-bt=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
</Tabs>


<span id="d00dbc24"></span>
## Performance optimization suggestions

tosutil supports adjusting concurrency using the `-j` and `-p` parameters. When uploading large files in batches, the actual concurrency equals the `-j` parameter multiplied by the `-p` parameter. Adjustment suggestions are as follows:


* **Insufficient resource scenarios**

   In cases of limited network, memory, or other resources, avoid setting concurrency too high to prevent performance degradation or failures caused by resource exhaustion. You can start with a low concurrency setting based on available resources, then gradually increase the parameters until reaching an optimal configuration.

* **Improve overall execution QPS and bandwidth**

   * **Uploading, downloading, and copying small files**: set a higher concurrency to increase QPS.

   * **Uploading, downloading, and copying large files**: avoid excessive concurrency to prevent bandwidth contention and performance decline.

      You can control the concurrency of non\-shard tasks and shard tasks separately with the `-nfj` parameter and the `-j` parameter. For example, setting `-j=100, -nfj=80` means the total concurrency is 100. When executing non\-shard tasks (usually small files), the maximum concurrency is 80; for shard tasks (usually large files), the maximum concurrency is 20.

* **Public network operation scenarios**

   Due to unstable public networks and low client bandwidth, issues like slow or failed uploads may occur. You can adjust parameters based on the following suggestions:

   * Increase the `maxRetryCount` parameter in the configuration file to resolve public network instability through continuous retries.

   * If client bandwidth is limited, reduce the `-j` and `-p` parameters reasonably to avoid bandwidth overload caused by excessive concurrency, which may lead to stream breaks and failures.

   * Adjust the `-ps` parameter appropriately; reducing shard size helps improve the success rate of uploading, downloading, or copying individual shards.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">In scenarios with massive small files, if you set a high <code>-j</code> that causes TPS to exceed 1000, you need to simultaneously increase the <code>maxConnections</code> parameter. For more information, see <a href="https://docs.byteplus.com/docs/tos/profile-description">configuration file description</a>.</div>


<span id=".5Y-C5pWw6K-05piO"></span>
## Parameters

For descriptions of general optional parameters, see [general parameters](https://docs.byteplus.com/docs/tos/Command-format#.6YCa55So5Y-v6YCJ5Y-C5pWw).


|**parameter name** |**Type** |**Description** |
|---|---|---|
|file_url |String |Local file path.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you need to upload a list of files, you can add multiple <code>file_url</code> in the command, separated by commas (,).</div><br> |
|folder_url |String |Local folder path, requires the `-r` parameter to be used together. |
|bucket |String |Bucket name. |
|key |String |Object name. |
|prefix |String |Object name prefix for batch operations. |
|\-r |Bool |Perform batch upload, download, or copy operations. |
|\-dryRun |Bool |Test mode runs without performing actual upload, download, or copy operations. |
|\-link |Bool |Upload the real path pointed to by the symbolic link file or folder. |
|\-msm |Enum |Enable multi\-file or folder upload mode with the following explanation:<br><br><br>* `-msm=1`: indicates the upload path is a list of files or folders separated by commas (,).<br><br>* `-msm=2`: indicates the upload path is a manifest file containing a list of files or folders.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If the file or folder name contains commas, do not use the <code>-msm=1</code> mode.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If the <code>-r</code> parameter is not set, folders in the list will not be uploaded.</div><br> |
|\-recover |String |Task ID for the result list file of resumable upload, download, or copy object tasks. |
|\-u |Bool |When performing incremental upload, download, or copy of objects, setting this parameter compares the source and destination. It is recommended for use in the following situations:<br><br><br>* The destination does not exist.<br><br>* The file size at the destination differs from the source.<br><br>* Execute the corresponding operation when the last modification time at the destination is earlier than the source. |
|\-vchecksum |Bool |verify data consistency using the CRC64 algorithm when uploading or downloading objects |
|\-flat |Bool |Upload, download, or copy objects without including relative parent directories. |
|\-j |Integer |The maximum concurrency for batch tasks defaults to `defaultJobs` in the configuration file, with a default value of 3. |
|\-p |Integer |The maximum concurrency for each part task defaults to `defaultParallels` in the config file, with a default value of 1. |
|\-threshold |Integer |Threshold for enabling shard tasks in bytes, defaulting to `defaultBigfileThreshold` in the configuration file.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Support capacity unit configurations, for example, configuring 1MB represents 1,048,576 bytes.</div><br> |
|\-nfj |Integer |The maximum concurrency for processing ordinary files or objects (non\-sharded tasks) in batch operations. When this parameter is set, the concurrency specified by the `-j` parameter splits into two parts: `nfj` for ordinary files and `j-nfj` for sharded tasks. Only effective during batch operations. |
|\-ps |Integer/String |The size of each part task in bytes, defaulting to `defaultPartSize` in the configuration file.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Supports configuration with size units, for example, setting 1MB represents 1,048,576 bytes.</div><br> |
|\-cpd |String |Folder for generating breakpoint record files; defaults to `defaultCheckpointDir` in the configuration file. |
|\-acl |String |The predefined access policy that can be specified when uploading or copying objects. The supported values are as follows:<br><br><br>* `private`<br><br>* `public-read`<br><br>* `public-read-write`<br><br>* `authenticated-read`<br><br>* `bucket-owner-read`<br><br>* `bucket-owner-full-control`<br><br>* `bucket-owner-entrusted` |
|\-sc |Enum |You can specify the object storage type when uploading an object. The values are explained as follows:<br><br><br>* `STANDARD`: standard storage, default value.<br><br>* `IA`: infrequent access storage.<br><br>* `ARCHIVE_FR`: archive flashback storage.<br><br>* `ARCHIVE`: archive storage.<br><br>* `COLD_ARCHIVE`: cold archive storage.<br><br>* `DEEP_COLD_ARCHIVE`: deep cold archive storage.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Currently, cold archive storage is supported only in North China 2 (Beijing), East China 2 (Shanghai), and South China 1 (Guangzhou).</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Currently, deep cold archive is supported only in North China 2 (Beijing), East China 2 (Shanghai), and South China 1 (Guangzhou), all of which are in invitation\-only testing. If you need to use this storage type, contact your account manager.</div><br> |
|\-meta |String |Custom metadata specified when uploading or copying an object. |
|\-sse |String |The server\-side encryption algorithm used when uploading or copying objects; supported values:<br><br><br>* aes256<br><br>* kms<br><br><br>Default is defaultSse in the configuration file. |
|\-sseKeyId |String |When uploading or copying an object and specifying the server\-side encryption algorithm as KMS, use the KMS key, which defaults to the defaultSseKeyId in the configuration file. |
|\-contentType |String |Set the object's Content\-Type when uploading or copying objects. |
|\-contentDisposition |String |Set the Content\-Disposition of the object when uploading or copying an object. |
|\-contentEncoding |String |Set the object's Content\-Encoding when uploading or copying objects. |
|\-contentLanguage |String |Set the object's Content\-Language when uploading or copying objects. |
|\-cacheControl |String |Set the object's Cache\-Control when uploading or copying an object. |
|\-expires |String |Set the Expires for the object when uploading or copying, in the format: YYYYMMDDHHmmSS. |
|\-include |String |Use the following characters for name matching patterns when uploading, downloading, or copying files:<br><br><br>* `?`: matches a single arbitrary character.<br><br>* `*`: matches multiple arbitrary characters.<br><br>* `#`: serves as a delimiter.<br><br><br>For example, `-include=*.png#*.txt` matches all files ending with `.png` and `.txt`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">To avoid parsing errors caused by the operating system escaping special characters, it is recommended to enclose name matching patterns in quotes.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Name matching patterns only apply when uploading folders or file lists.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Name matching patterns apply to the full file path (including filename and directory).</div><br> |
|\-exclude |String |When uploading, downloading, or copying, the name matching pattern for files not included supports the following characters:<br><br><br>* `?`: matches any single character.<br><br>* `*`: matches any multiple characters.<br><br>* `#`: used as a separator.<br><br><br>For example, `-exclude=*.png#*.txt` means matching all files ending with `.png` and `.txt`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">To avoid parsing errors caused by OS escaping special characters, it is recommended to use quotes when setting the name matching pattern.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Name matching patterns only apply when uploading folders or file lists.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Name matching patterns apply to the entire file path (including file name and directory).</div><br> |
|\-timeRange |String |Time range matching pattern for the file's last modification time during upload, download, or copy. Format: `YYYYMMDDHHmmSS-YYYYMMDDHHmmSS`. |
|\-at |Bool |A file list of files in the uploaded folder with last access time satisfying the `-timeRange` parameter. |
|\-ddo |Bool |Folders themselves are not uploaded as separate objects during upload. |
|\-dmf |Bool |Setting the name matching mode `-include/-exclude` and the time range matching mode `-timeRange` does not apply to folders. |
|\-arcDir |String |Archive folder after file upload succeeds. |
|\-fr |Bool |Generate a result manifest file when operating on a single object. |
|\-o |String |Folder for the generated result list file, defaulting to `defaultOutputDir` in the configuration file. |
|\-bt |String |Type of the bucket. Valid values:<br><br><br>* `fns`: flat bucket.<br><br>* `hns`: layered bucket<br><br><br>If the bucket type is not specified, the bucket type is obtained from the bucket metadata by default. |


<span id=".5L2_55So56S65L6L"></span>
## Usage example

<span id="c1c7b4a3"></span>
### Upload a single file

The following command uploads the **object** file in the  **/Users/Downloads/TOS/tosutil** folder to the **bucketname** bucket. The file will be named **object** after upload.


* Command

   ```Plain
   ./tosutil cp /Users/Downloads/TOS/tosutil/object  tos://bucketname/object
   ```
   

* Return

   ```Plain
   Start at 2022-10-27 10:49:12.407874 +0000 UTC
    
    
   Parallel:      1                   Jobs:          5
   Threshold:     100.00MB            PartSize:      auto
   VerifyChecksum: false
   CheckpointDir: /.tosutil_checkpoint
    
   [-------------------------------------------] 100.00% ?/s 50.50KB/50.50KB 162ms
    
   Upload successfully, 50.50KB, n/a, /Users/Downloads/TOS/tosutil/object --> tos://bucketname/object, cost [164], status [200], request id [2643485a6228acbb635a6228-ac1173a1-1oo0Rk-PuO-cb-tos-bj-3]
   ```
   


<span id="936d0ecc"></span>
### Upload folder

The following command uploads all files in the  **/Users/Downloads/TOS/tosutil** folder to the **bucketname** bucket. The folder will be named **cpfile** after upload.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This command uploads the folder itself; after uploading, all files remain in the <strong>cpfile</strong> folder.</div>



* Command

   ```Plain
   ./tosutil cp /Users/Downloads/TOS/tosutil  tos://bucketname/cpfile -r
   ```
   

* Return

   ```Plain
   Start at 2022-10-27 10:50:43.872787 +0000 UTC
    
    
   Parallel:      1                   Jobs:          5
   Threshold:     100.00MB            PartSize:      auto
   VerifyChecksum: false
   CheckpointDir: /Users/.tosutil_checkpoint
   OutputDir: /Users/.tosutil_output
    
   [----------------------------] 100.00% tps:0.00 ?/s 4/4 181.45KB/181.45KB 183ms
   Succeed count is:   4         Failed count is:    0
   Succeed bytes is:   181.45KB
   Metrics [max cost:178 ms, min cost:103 ms, average cost:143.75 ms, average tps:21.62]
    
   Task id is: 34c8480e-55e5-11ed-806b-aa665a3c7f26
   ```
   


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more example commands for different upload scenarios, see <a href="https://docs.byteplus.com/docs/tos/Upload-object-example">upload examples</a>.</div>
