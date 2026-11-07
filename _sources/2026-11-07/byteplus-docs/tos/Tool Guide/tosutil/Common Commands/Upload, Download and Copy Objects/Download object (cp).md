---
title: "Download object (cp)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Download-object-cp"
---

You can use the `cp` command to download objects from the bucket.

<span id=".5ZG95Luk6K-t5rOV"></span>
## Command syntax


<Tabs>
<Tab zoneid="k3wqCBBF" title="Linux/macOS">
<TabTitle>Linux/macOS</TabTitle>

* Download single object


```Bash
./tosutil cp tos://bucket/key file_url|folder_url [-dryRun] [-tempFileDir=xxx] [-u] [-vchecksum] [-p=1] [-threshold=104857600] [-ps=auto] [-cpd=xxx] [-versionId=xxx] [-fr] [-o=xxx] [-bt=xxx] [-nftr] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```



* Download multiple objects


```Bash
./tosutil cp tos://bucket[/prefix] folder_url -r [-dryRun] [-tempFileDir=xxx] [-u] [-vchecksum] [-flat] [-j=1] [-p=1] [-threshold=104857600] [-nfj=1] [-ps=auto] [-cpd=xxx] [-include=*.xxx] [-exclude=*.xxx] [-timeRange=time1-time2] [-dmf] [-o=xxx] [-bt=xxx] [-nftr] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
<Tab zoneid="P8MI2Oy0" title="Windows">
<TabTitle>Windows</TabTitle>

* Download a single object


```Bash
tosutil cp tos://bucket/key file_url|folder_url [-dryRun] [-tempFileDir=xxx] [-u] [-vchecksum] [-p=1] [-threshold=104857600] [-ps=auto] [-cpd=xxx] [-versionId=xxx] [-fr] [-o=xxx] [-bt=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```



* Batch download object


```Bash
tosutil cp tos://bucket[/prefix] folder_url -r [-dryRun] [-tempFileDir=xxx] [-u] [-vchecksum] [-flat] [-j=1] [-p=1] [-threshold=104857600] [-nfj=1] [-ps=auto] [-cpd=xxx] [-include=*.xxx] [-exclude=*.xxx] [-timeRange=time1-time2] [-dmf] [-o=xxx] [-bt=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
</Tabs>


<span id="d00dbc24"></span>
## Performance optimization recommendations

tosutil supports adjusting concurrency through the `-j` and `-p` parameters. When you batch upload large files, the actual concurrency equals the `-j` parameter multiplied by the `-p` parameter. Adjustment recommendations are as follows:


* **Insufficient resource scenarios**

   In cases where network, memory, or other resources are insufficient, avoid setting concurrency too high to prevent performance degradation or failures caused by resource exhaustion. You can start with a lower concurrency based on your actual resources, then gradually increase parameters until reaching an optimal setting.

* **Improve overall execution QPS and bandwidth**

   * **Uploading, downloading, and copying small files**: require setting a higher concurrency to increase QPS.

   * **Uploading, downloading, and copying large files**: avoid overly high concurrency that causes bandwidth contention and performance degradation.

      You can control the concurrency of non\-shard tasks and shard tasks separately using the `-nfj` parameter and the `-j` parameter. For example, setting `-j=100, -nfj=80` means the total concurrency is 100; when running non\-shard tasks (usually small files), the max concurrency is 80; when running shard tasks (usually large files), the max concurrency is 20.

* **Public network operating scenarios**

   Due to unstable public network conditions and low client bandwidth, upload slowdowns and failures may occur. You can adjust parameters based on the following recommendations:

   * Increase the `maxRetryCount` parameter in the configuration file to resolve unstable public network issues through repeated retries.

   * If the client bandwidth is limited, reduce the `-j` and `-p` parameters appropriately to prevent excessive concurrency causing client bandwidth overload, resulting in stream interruptions or failures.

   * Adjust the `-ps` parameter sensibly to reduce the shard size, which helps improve the success rate of uploading/downloading/copying individual shards.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">In scenarios with massive small files, if you set a high <code>-j</code> causing TPS to exceed 1000, you need to increase the <code>maxConnections</code> parameter accordingly. For more information, see <a href="https://docs.byteplus.com/docs/tos/profile-description">Configuration File Description</a>.</div>


<span id=".5Y-C5pWw6K-05piO"></span>
## Parameters

For the description of general optional parameters, see [general parameters](https://docs.byteplus.com/docs/tos/Command-format#.6YCa55So5Y-v6YCJ5Y-C5pWw).


|**Parameter name** |**Type** |**description** |
|---|---|---|
|file_url |String |Path of the object to download. |
|folder_url |String |Local folder path for downloads. |
|bucket |String |Bucket name. |
|key |String |The object name. |
|prefix |String |Object name prefix for batch operations. |
|\-r |Bool |Execute batch upload, download, or copy operations. |
|\-dryRun |Bool |Run in test mode without performing actual upload, download, or copy operations. |
|\-tempFileDir |String |The folder to save temporary files during segmented downloads; defaults to `defaultTempFileDir` in the configuration file.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If the <code>-tempFileDir</code> parameter is empty, temporary files generated during segmented downloads are stored by default in the same path as the downloaded file, with filenames ending in <code>.tos.temp</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Since temporary files generated during downloads are saved in this directory, ensure the user running tosutil has write permission for this path. The available space on this path must be greater than the size of the object to be downloaded.</div><br> |
|\-recover |String |list file task ID for pending upload, download, or copy object task recovery. |
|\-u |Bool |Incremental upload, download, or copy objects. After setting this parameter, the data between the source and target will be compared. It is recommended to use this parameter in the following scenarios:<br><br><br>* The target does not exist.<br><br>* The file size at the target differs from that at the source.<br><br>* Execute the corresponding operation when the target's last modified time is earlier than the source's last modified time. |
|\-vchecksum |Bool |verify data consistency using CRC64 algorithm when uploading or downloading objects. |
|\-flat |Bool |Do not include relative parent directories when uploading, downloading, or copying objects. |
|\-j |Integer |maximum concurrency of batch tasks, `-j=1` means the maximum concurrency of batch tasks is 1. defaults to `defaultJobs` in the configuration file, with a default value of 3. |
|\-p |Integer |The maximum concurrency for each shard task. `-p=1` means the maximum concurrency is 1. Defaults to `defaultParallels` in the configuration file, with a default value of 1. |
|\-threshold |Integer |Enable the threshold for multipart tasks. Unit: bytes. The default is the `defaultBigfileThreshold` in the configuration file.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Support configuration with capacity units. For example, setting 1MB represents 1,048,576 bytes.</div><br> |
|\-nfj |Integer |The maximum concurrency for processing ordinary files or objects (non\-sharded tasks) in batch operations. After setting this parameter, the concurrency set by the `-j` option splits into two parts: `nfj` for ordinary files and `j-nfj` for sharded tasks. Effective only during batch operations. |
|\-ps |Integer/String |The segment size of each shard task in bytes, defaulting to `defaultPartSize` in the configuration file.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Support capacity unit configuration, for example, configuring 1MB represents 1,048,576 bytes.</div><br> |
|\-cpd |String |folder for generating breakpoint record files, default is `defaultCheckpointDir` in the configuration file. |
|\-versionId |String |Version number for downloading or copying a single object. |
|\-include |String |Match patterns for file names during upload, download, or copy support the following characters:<br><br><br>* `?`: Matches a single arbitrary character.<br><br>* `*`: Matches multiple arbitrary characters.<br><br>* `#`: Serves as a separator.<br><br><br>For example, `-include=*.png#*.txt` matches all files ending with `.png` and `.txt`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">To avoid parsing failures caused by operating system escaping special characters, it is recommended to enclose the name matching pattern in quotes.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The name matching pattern only applies when uploading folders or file lists.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The name matching pattern applies to the full file path (including file name and directory).</div><br> |
|\-exclude |String |When uploading, downloading, or copying, the name matching pattern for names without files supports the following characters:<br><br><br>* `?`: matches any single character.<br><br>* `*`: matches multiple characters.<br><br>* `#`: used as a separator.<br><br><br>For example, `-exclude=*.png#*.txt` matches all files ending with `.png` and `.txt`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">To avoid parsing errors caused by operating systems escaping special characters, it is recommended to use quotation marks when setting name matching patterns.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Name matching mode only applies when uploading folders or file lists.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Name matching mode applies to the full file path (including file name and directory).</div><br> |
|\-timeRange |String |Time period matching pattern for the file's last modification time during upload, download, or copy, formatted as: `YYYYMMDDHHmmSS-YYYYMMDDHHmmSS`. |
|\-dmf |Bool |Set the name matching mode `-include/-exclude` and time range matching mode `-timeRange` to be ineffective for folders. |
|\-marker |String |Specify the start position of the object when downloading in batch. |
|\-fr |Bool |Generate a result list file when operating on a single object. |
|\-o |String |Folder for generated result list files, defaulting to `defaultOutputDir` in the configuration file. |
|\-bt |String |Type of the bucket. Valid values:<br><br><br>* `fns`: flat bucket.<br><br>* `hns`: hierarchical bucket.<br><br><br>If the bucket type is not specified, the type will be obtained from the bucket metadata by default. |
|\-bfs |Integer |Uses the hierarchical listing method to batch download objects and sets the concurrency level for those listings. |
|\-nftr |Bool |When creating a new file, do not use the `Truncate` parameter to specify the file size. |


<span id=".5L2_55So56S65L6L"></span>
## Examples

<span id="16a25b47"></span>
### Download a single object

The following command downloads the **object1.png** object from the **bucketname** bucket to the  **/Users/Downloads/TOS/tosutil** folder.


* Command

   ```Plain
   ./tosutil cp tos://bucketname/object1.png /Users/Downloads/TOS/tosutil
   ```
   

* Back

   ```Plain
   Start at 2022-10-27 10:56:20.611282 +0000 UTC
    
    
   Parallel:      1                   Jobs:          5
   Threshold:     100.00MB            PartSize:      auto
   VerifyChecksum: false
   CheckpointDir: /.tosutil_checkpoint
   TempFileDir:
    
   [-------------------------------------------] 100.00% ?/s 55.98KB/55.98KB 106ms
    
   Download successfully, 55.98KB, n/a, tos://bucketname/object1.png --> /Downloads/TOS/tosutil/object1.png, cost [106], status [200], request id [5c81485a63d4b1d7635a63d4-ac17b21f-1oo0Ye-GO-cb-tos-bj]
   ```
   


<span id="94db6545"></span>
### Batch download objects

The following command downloads objects with the prefix **object** from the **bucketname** bucket to the  **/Users/Downloads/TOS/tosutil** folder.


* command

   ```Plain
   ./tosutil cp tos://bucketname/object /Users/Downloads/TOS/tosutil -r
   ```
   

* return

   ```Plain
   Start at 2022-10-27 10:56:35.434563 +0000 UTC
    
    
   Parallel:      1                   Jobs:          5
   Threshold:     100.00MB            PartSize:      auto
   VerifyChecksum: false
   CheckpointDir: /Users/.tosutil_checkpoint
   OutputDir: /Users/.tosutil_output
   TempFileDir:
    
   [----------------------] 100.00% tps:51.09 3.02MB/s 4/4 238.21KB/238.21KB 278ms
   Succeed count is:   4         Failed count is:    0
   Succeed bytes is:   238.21KB
   Metrics [max cost:216 ms, min cost:163 ms, average cost:191.50 ms, average tps:14.23]
    
   Task id is: 0653482e-55e6-11ed-afb8-aa665a3c7f26
   ```
   


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more example commands in download scenarios, see <a href="https://docs.byteplus.com/docs/tos/Download-object-example">download examples</a>.</div>
