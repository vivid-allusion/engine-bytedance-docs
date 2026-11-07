---
title: "Copy object (cp)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Copy-object-cp"
---

You can use the `cp` command to copy objects.

<span id="48c262cf"></span>
## Precautions

Directly copying an object from a parent directory to a subdirectory or from a subdirectory to a parent directory is not supported.

<span id=".5ZG95Luk6K-t5rOV"></span>
## Command syntax


<Tabs>
<Tab zoneid="5b37NVGV" title="Linux/macOS">
<TabTitle>Linux/macOS</TabTitle>

* Copy a single object


```Bash
./tosutil cp tos://srcbucket/srckey tos://dstbucket/[dstkey] [-dryRun] [-u] [-pipe] [-pe=xxx] [-p=1] [-threshold=104857600] [-ps=auto] [-cpd=xxx] [-versionId=xxx] [-acl=xxx] [-sc=xxx] [-meta=aaa:bbb#ccc:ddd] [-sse=xxx] [-sseKeyId=xxx] [-contentType=xxx] [-contentDisposition=xxx] [-contentEncoding=xxx] [-contentLanguage=xxx] [-cacheControl=xxx] [-expires=xxx] [-fr] [-o=xxx] [-bt=xxx] [-sbt=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```



* Copy objects in batch


```Bash
./tosutil cp tos://srcbucket[/srcprefix] tos://dstbucket[/dstprefix] -r [-dryRun] [-u] [-pipe] [-pe=xxx]  [-flat] [-j=1] [-p=1] [-threshold=104857600] [-nfj=1] [-ps=auto] [-cpd=xxx] [-acl=xxx] [-sc=xxx] [-meta=aaa:bbb#ccc:ddd] [-sse=xxx] [-sseKeyId=xxx] [-contentType=xxx] [-contentDisposition=xxx] [-contentEncoding=xxx] [-contentLanguage=xxx] [-cacheControl=xxx] [-expires=xxx] [-include=*.xxx] [-exclude=*.xxx] [-timeRange=time1-time2] [-dmf] [-o=xxx] [-bt=xxx] [-sbt=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
<Tab zoneid="AiKh5o91" title="Windows">
<TabTitle>Windows</TabTitle>

* Copy a single object


```Bash
tosutil cp tos://srcbucket/srckey tos://dstbucket/[dstkey] [-dryRun] [-u] [-p=1] [-threshold=104857600] [-ps=auto] [-cpd=xxx] [-versionId=xxx] [-acl=xxx] [-meta=aaa:bbb#ccc:ddd] [-sse=xxx] [-sseKeyId=xxx] [-contentType=xxx] [-contentDisposition=xxx] [-contentEncoding=xxx] [-contentLanguage=xxx] [-cacheControl=xxx] [-expires=xxx] [-fr] [-o=xxx] [-bt=xxx] [-sbt=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```



* Copy objects in batch


```Bash
tosutil cp tos://srcbucket[/srcprefix] tos://dstbucket[/dstprefix] -r [-dryRun] [-u] [-flat] [-j=1] [-p=1] [-threshold=104857600] [-nfj=1] [-ps=auto] [-cpd=xxx] [-acl=xxx] [-meta=aaa:bbb#ccc:ddd] [-sse=xxx] [-sseKeyId=xxx] [-contentType=xxx] [-contentDisposition=xxx] [-contentEncoding=xxx] [-contentLanguage=xxx] [-cacheControl=xxx] [-expires=xxx] [-include=*.xxx] [-exclude=*.xxx] [-timeRange=time1-time2] [-dmf] [-o=xxx] [-bt=xxx] [-sbt=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
</Tabs>


<span id="d00dbc24"></span>
## Performance optimization recommendations

tosutil supports adjusting concurrency with the `-j` and `-p` parameters. When you upload large files in batches, the actual concurrency equals `-j` multiplied by `-p`. Adjustment recommendations are as follows:


* **Insufficient resource scenarios**

   When resources such as network and memory are insufficient, avoid setting the concurrency too high to prevent performance degradation or failures caused by resource exhaustion. You can start with a lower concurrency based on actual resource conditions and gradually increase the value until you reach an optimal setting.

* **Improving overall QPS and bandwidth**

   * **Uploading, downloading, and copying small files**: Set a higher concurrency to increase QPS.

   * **Uploading, downloading, and copying large files**: Avoid excessively high concurrency to prevent bandwidth contention and performance degradation.

      You can control the concurrency of non\-shard tasks and shard tasks with the `-nfj` and `-j` parameters separately. For example, setting `-j=100, -nfj=80` means the total concurrency is 100; for non\-shard tasks (usually small files), the max concurrency is 80; for shard tasks (usually large files), the max concurrency is 20.

* **Public network scenarios**

   Due to public network instability and low client bandwidth, uploads may be slow or fail. You can adjust parameters based on the following suggestions:

   * Increase the `maxRetryCount` parameter in the config file to resolve public network instability by retrying errors continuously.

   * If the client bandwidth is limited, you need to reasonably reduce the `-j` and `-p` parameters to avoid client bandwidth overload caused by excessive concurrency, which may lead to stream interruption or failure.

   * Properly adjust the `-ps` parameter to reduce the slice size, which helps improve the success rate of uploading, downloading, or copying individual slices.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">In massive small file scenarios, if you set a high <code>-j</code> causing the TPS to exceed 1000, you need to simultaneously increase the <code>maxConnections</code> parameter. For more information, refer to <a href="https://docs.byteplus.com/docs/tos/profile-description">configuration file description</a>.</div>


<span id=".5Y-C5pWw6K-05piO"></span>
## Parameters

For a description of general optional parameters, see [General parameters](https://docs.byteplus.com/docs/tos/Command-format#.6YCa55So5Y-v6YCJ5Y-C5pWw).


|**Parameter** |**Type** |**Description** |
|---|---|---|
|srcbucket |String |Source bucket name of the copied object. |
|srckey |String |Name of the source object to copy. |
|dstbucket |String |Specify the destination bucket name for copying the object. |
|dstkey |String |Destination object name of the copied object. |
|srcprefix |String |Source object name prefix for batch copying. |
|dstprefix |String |Prefix for the target object name during batch copying. |
|\-r |Bool |Execute batch upload, download, or copy operations. |
|\-dryRun |Bool |Runs in test mode without performing actual upload, download, or copy operations. |
|\-recover |String |Task ID of the result list file for the upload, download, or copy object task to be resumed. |
|\-u |Bool |Incrementally upload, download, or copy objects. When this parameter is set, the source and target will be compared. We recommend using this parameter in the following scenarios:<br><br><br>* The target does not exist.<br><br>* The file size on the target differs from that on the source.<br><br>* Perform the corresponding operation when the last modified time on the target is earlier than the last modified time on the source. |
|\-pipe |Bool |Copy objects using the pipeline streaming mode. |
|\-pe |String |Specify the endpoint of the destination bucket when using pipeline streaming mode to copy objects. |
|\-flat |Bool |Upload, download, or copy objects without including relative parent directories. |
|\-j |Integer |The maximum concurrency for batch tasks, `-j=1` indicates the maximum concurrency is 1 for batch tasks. The default is `defaultJobs` from the configuration file, with a default value of 3. |
|\-p |Integer |The maximum concurrency per shard task, `-p=1` means the maximum concurrency of shard tasks is 1. Default is the `defaultParallels` in the configuration file. |
|\-threshold |Integer |Set the threshold for enabling multipart tasks in bytes, defaulting to `defaultBigfileThreshold` in the configuration file.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Support capacity units in configuration, for example, configuring 1 MB to represent 1,048,576 bytes.</div><br> |
|\-nfj |Integer |Maximum concurrency for processing ordinary files or objects (non\-sharded tasks) in batch jobs. After setting this parameter, the concurrency specified by the `-j` parameter splits into two parts: `nfj` for ordinary files and `j-nfj` for sharded tasks. Effective only during batch operations. |
|\-ps |Integer/String |Segment size for each sharded task, in bytes. The default is `defaultPartSize` from the configuration file.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Supports configuration with capacity units, for example, setting 1 MB equals 1,048,576 bytes.</div><br> |
|\-cpd |String |Folder for generating breakpoint record files. Defaults to `defaultCheckpointDir` in the configuration file. |
|\-versionId |String |Version ID for downloading or copying a single object. |
|\-acl |String |Specify a predefined access policy when uploading or copying objects. Supported values are as follows:<br><br><br>* `private`<br><br>* `public-read`<br><br>* `public-read-write`<br><br>* `authenticated-read`<br><br>* `bucket-owner-read`<br><br>* `bucket-owner-full-control`<br><br>* `bucket-owner-entrusted` |
|\-sc |Enum |You can specify the object storage type when copying objects. The options are as follows:<br><br><br>* `STANDARD`: Standard Storage, which is the default value.<br><br>* `IA`: Infrequent Access Storage.<br><br>* `ARCHIVE_FR`: Flashback Archive.<br><br>* `ARCHIVE`: Archive.<br><br>* `COLD_ARCHIVE`: Cold Archive.<br><br>* `DEEP_COLD_ARCHIVE`: Deep Cold Archive.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Cold Archive is currently supported only in China (Beijing), China (Shanghai), and China (Guangzhou).</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Deep Cold Archive is currently supported only in China (Beijing), China (Shanghai), and China (Guangzhou), and is in invitation testing. Contact your account manager to use this storage type.</div><br> |
|\-meta |String |Custom metadata that can be specified when uploading or copying objects. |
|\-sse |String |Server\-side encryption algorithm used for uploading or copying objects. Supported values:<br><br><br>* `aes256`<br><br>* `kms`<br><br><br>Defaults to defaultSse in the configuration file. |
|\-sseKeyId |String |When uploading or copying an object and specifying the server\-side encryption algorithm as KMS, the KMS key used defaults to the defaultSseKeyId in the configuration file. |
|\-contentType |String |Set the Content\-Type of the object when uploading or copying objects. |
|\-contentDisposition |String |Set the object's Content\-Disposition when uploading or copying objects. |
|\-contentEncoding |String |Set the object's Content\-Encoding when uploading or copying the object. |
|\-contentLanguage |String |Set the Content\-Language of the object when uploading or copying objects. |
|\-cacheControl |String |Set the object's Cache\-Control when uploading or copying objects. |
|\-expires |String |Set the object's Expires when uploading or copying, format: YYYYMMDDHHmmSS. |
|\-include |String |Use the following characters to match patterns in file names during upload, download, or copy:<br><br><br>* `?`: Matches any single character.<br><br>* `*`: Matches any sequence of characters.<br><br>* `#`: Used as a separator.<br><br><br>For example, `-include=*.png#*.txt` includes all files ending with `.png` and `.txt`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">To avoid parsing errors caused by the operating system escaping special characters, it is recommended to use quotation marks to set the name matching pattern.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The name matching pattern only applies when uploading folders or file lists.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The name matching pattern applies to the full file path (including file name and directory).</div><br> |
|\-exclude |String |Supports the following characters in name matching patterns that do not include files when uploading, downloading, or copying:<br><br><br>* `?`: Matches a single arbitrary character.<br><br>* `*`: Matches multiple arbitrary characters.<br><br>* `#`: Used as a separator.<br><br><br>For example, `-exclude=*.png#*.txt` excludes all files ending with `.png` and `.txt`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">To avoid parsing errors caused by operating system escaping special characters, using quotes to set the name matching pattern is recommended.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Name matching patterns only take effect when uploading folders or file lists.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Name matching patterns apply to the full file path (including file name and directory).</div><br> |
|\-timeRange |String |Use a time range pattern for matching the last modified time of files during upload, download, or copy, formatted as `YYYYMMDDHHmmSS-YYYYMMDDHHmmSS`. |
|\-dmf |Bool |Setting name matching modes `-include/-exclude` and time range matching mode `-timeRange` do not apply to folders. |
|\-marker |String |Specify the starting position for listing objects during batch copy. |
|\-fr |Bool |Generate a result manifest file when operating on a single object. |
|\-o |String |Folder for generated result list files, default is the `defaultOutputDir` in the configuration file. |
|\-bt |String |The type of the destination bucket when copying objects. Valid values:<br><br><br>* `fns`: FNS bucket.<br><br>* `hns`: HNS bucket.<br><br><br>If the bucket type is not specified, the bucket type is obtained from the bucket metadata by default. |
|\-sbt |String |The type of source bucket when copying objects. Valid values:<br><br><br>* `fns`: FNS bucket.<br><br>* `hns`: HNS bucket.<br><br><br>If the bucket type is not specified, the bucket type is obtained from the bucket metadata by default. |
|\-bfs |Integer |Uses the hierarchical listing method to batch copy objects and sets the concurrency level for those listings. |


<span id=".5L2_55So56S65L6L"></span>
## Examples

<span id="b4606eef"></span>
### Copy a single object

The following command copies the **object1.png** object in the **bucketname** bucket to the **tosutil** bucket, renaming the copied object to **destobject.png**.


* Command

   ```Plain
   ./tosutil cp tos://bucketname/object1.png tos://tosutil/destobject.png
   ```
   

* Output

   ```Plain
   Start at 2022-10-27 10:57:24.353686 +0000 UTC
    
    
   Parallel:      1                   Jobs:          5
   Threshold:     100.00MB            PartSize:      auto
   CheckpointDir: /.tosutil_checkpoint
    
    
   Copy successfully, 55.98KB, tos://bucketname/object1.png --> tos://tosutil/destobject.png, cost [154], status [200], request id [55fa485a6414248e635a6414-ac13a11a-1oo0Zg-CO-cb-tos-bj]
   ```
   


<span id="5f3524e0"></span>
### Batch copy objects

The following command copies objects with the prefix **object** from the **bucketname** bucket to the **tosutil** bucket, with the copied objects prefixed as **destobject** afterward.


* Command

   ```Plain
   ./tosutil cp tos://bucketname/object tos://tosutil/destobject -r
   ```
   

* Output

   ```Plain
   Start at 2022-10-27 10:57:43.32094 +0000 UTC
    
    
   Parallel:      1                   Jobs:          5
   Threshold:     100.00MB            PartSize:      auto
   CheckpointDir: /Users/.tosutil_checkpoint
   OutputDir: /Users/.tosutil_output
    
   [-------------------------------------------------] 100.00% tps:23.37 4/4 371ms
   Succeed count is:   4         Failed count is:    0
   Metrics [max cost:330 ms, min cost:92 ms, average cost:186.25 ms, average tps:10.75]
    
   Task id is: 2ee1abfa-55e6-11ed-b269-aa665a3c7f26
   ```
