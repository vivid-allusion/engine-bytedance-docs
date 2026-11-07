---
title: "Download objects using authorization code (share-cp)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Download-object-with-authorization-code-share-cp"
---

You can use the `share-cp` command to download objects or multiple objects by object name prefix to your local device via an authorization code.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Considerations

Before using this command to download objects or multiple objects, ensure that the source objects in the bucket have not changed. Otherwise, it may cause data inconsistencies or download failures.

<span id=".5ZG95Luk5qC85byP"></span>
## Command format


<Tabs>
<Tab zoneid="vebQEr4z" title="Linux/macOS">
<TabTitle>Linux/macOS</TabTitle>

* Download a single object using an authorization code


```Bash
./tosutil share-cp authorization_code|authorization_code_file_url file_url|folder_url [-key=xxx] [-dryRun] [-tempFileDir=xxx] [-u] [-vchecksum] [-p=1] [-threshold=104857600] [-ps=auto] [-cpd=xxx] [-versionId=xxx] [-fr] [-o=xxx] [-bt=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```



* Download multiple objects using an authorization code


```Bash
./tosutil share-cp authorization_code|authorization_code_file_url folder_url -r [-key=xxx] [-dryRun] [-tempFileDir=xxx] [-u] [-vchecksum] [-flat] [-j=1] [-p=1] [-threshold=104857600] [-ps=auto] [-cpd=xxx] [-include=*.xxx] [-exclude=*.xxx] [-timeRange=time1-time2] [-dmf] [-o=xxx] [-bt=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
<Tab zoneid="dffybjXh" title="Windows">
<TabTitle>Windows</TabTitle>

* Download a single object using the authorization code


```Bash
tosutil share-cp authorization_code|authorization_code_file_url file_url|folder_url [-key=xxx] [-dryRun] [-tempFileDir=xxx] [-u] [-vchecksum] [-p=1] [-threshold=104857600] [-ps=auto] [-cpd=xxx] [-versionId=xxx] [-fr] [-o=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```



* Batch download objects using the authorization code


&nbsp;




</Tab>
</Tabs>


<span id=".5Y-C5pWw6K-05piO"></span>
## Parameters

For a description of common optional parameters, see [General parameters](https://docs.byteplus.com/docs/tos/Command-format#.6YCa55So5Y-v6YCJ5Y-C5pWw).


|**Parameter** |**Type** |**Description** |
|---|---|---|
|authorization_code |String |Authorization code used. |
|file://authorization_code_file_url |String |Path to the authorization code file used. |
|file_url |String |Local file path when downloading. |
|folder_url |String |Local folder path for downloading objects. |
|\-key |String |Object name when downloading a single object. |
|\-dryRun |Bool |Run in test mode without executing the actual download. |
|\-tempFileDir |String |Folder for saving temporary files during shard downloads, defaulting to `defaultTempFileDir` in the configuration file.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If this value is empty and <code>defaultTempFileDir</code> in the configuration file is also empty, temporary files generated during shard downloads will be saved in the same directory as the file to be downloaded, ending with <code>.tos.temp</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Because temporary files generated during downloads are saved in this directory, ensure the user running tosutil has write permissions for this path. The available space on this path must be larger than the size of the object to be downloaded.</div><br> |
|\-u |Bool |When incrementally downloading an object, setting this parameter compares data consistency between source and target. Use this parameter in the following scenarios:<br><br><br>* The target does not exist.<br><br>* The file size on the target differs from that on the source.<br><br>* Perform the corresponding operation if the target's last modification time is earlier than the source's. |
|\-vchecksum |Bool |Verify data consistency when downloading objects using the CRC64 algorithm. |
|\-flat |Bool |Downloaded objects do not include relative parent directories. |
|\-j |Integer |Maximum concurrency for batch tasks. `-j=3` means the maximum concurrency is 3. Defaults to `defaultJobs` in the configuration file, with a default value of 3. |
|\-p |Integer |The maximum concurrency for each shard task. `-p=1` means the maximum concurrency for shard tasks is 1. Defaults to `defaultParallels` in the config file, with a default value of 1. |
|\-threshold |Integer |Threshold for enabling shard tasks, unit: bytes, defaulting to `defaultBigfileThreshold` in the configuration file.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Supports configuring with capacity units, for example, 1MB equals 1,048,576 bytes.</div><br> |
|\-ps |Integer/String |Segment size for each shard task, in bytes. Defaults to `defaultPartSize` in the configuration file.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Supports capacity units configuration. For example, setting 1MB equals 1,048,576 bytes.</div><br> |
|\-cpd |String |Folder for generating breakpoint record files, defaulting to `defaultCheckpointDir` in the configuration file. |
|\-versionId |String |Download the version number of a single object. |
|\-include |String |The object matching pattern used to include objects for downloads. You can use the wildcards `?` and `*` and the delimiter "#" in the match expression. |
|\-exclude |String |The object matching pattern used to exclude objects for downloads. You can use the wildcards `?` and `*` and the delimiter "#" in the match expression. |
|\-timeRange |String |Time range matching pattern for the last modification time of the file when downloading an object, format: `YYYYMMDDHHmmSS-YYYYMMDDHHmmSS`. |
|\-dmf |Bool |Setting name matching mode `-include/-exclude` and time range matching mode `-timeRange` does not apply to folders. |
|\-fr |Bool |Generate a result manifest file when operating on a single object. |
|\-o |String |The folder for generating the result list file, defaulting to `defaultOutputDir` in the configuration file. |
|\-bt |String |Type of bucket. Valid values:<br><br><br>* `fns`: FNS bucket.<br><br>* `hns`: HNS bucket.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the bucket type is not specified, the bucket type will be fetched from the bucket metadata when listing files; when listing directories, the bucket type cannot be identified, which may cause request errors.</div><br> |


<span id=".5L2_55So56S65L6L"></span>
## Usage example

<span id="e4447b93"></span>
### Download a single object

The following command downloads the **object1.png** object from the **bucketname** bucket to the  **/Users/Downloads/TOS/tosutil** folder using an authorization code. The authorization code path used is  **/tmp/tosutil/authorization_code**.


* Command

   ```bash
   ./tosutil share-cp file:///tmp/tosutil/authorization_code /Users/Downloads/TOS/tosutil -key=object1.png
   ```
   

* Return

   ```plain
   Start at 2022-10-27 10:56:20.611282 +0000 UTC
    
    
   Parallel:      1                   Jobs:          5
   Threshold:     100.00MB            PartSize:      auto
   VerifyChecksum: false
   CheckpointDir: /Users/.tosutil_checkpoint
   TempFileDir: /Users/
   
   Waiting to prepare the temp file [93456].
   
   [-----------------------------------------------------------------------------] 100.00% 201.47KB/s 55.98KB/55.98KB 306ms
   Waiting to rename temporary file...
   
    
   Download successfully, 55.98KB, n/a, tos://bucketname/object1.png --> /Downloads/TOS/tosutil/object1.png, cost [106], status [200], request id [5c81485a63d4b1d7635a63d4-ac17b21f-1oo0Ye-GO-cb-tos-bj]
   The authorized prefix is empty, all the content of bucket can be accessed
   ```
   


<span id="4ef82287"></span>
### Batch download objects

The following command downloads objects with the prefix **object** from the **bucketname** bucket to the  **/Users/Downloads/TOS/tosutil** folder based on the authorization code. The authorization code path used is  **/tmp/tosutil/authorization_code**.


* Command

   ```bash
   ./tosutil share-cp file:///tmp/tosutil/authorization_code /Users/Downloads/TOS/tosutil -key=object -r
   ```
   

* Return

   ```plain
   Start at 2022-10-27 10:56:35.434563 +0000 UTC
    
    
   Parallel:      1                   Jobs:          5
   Threshold:     100.00MB            PartSize:      auto
   VerifyChecksum: false
   CheckpointDir: /Users/.tosutil_checkpoint
   OutputDir: /Users/.tosutil_output
   TempFileDir: /Users/
    
   [----------------------] 100.00% tps:51.09 3.02MB/s 4/4 238.21KB/238.21KB 278ms
   Succeed count is:   4         Failed count is:    0
   Succeed bytes is:   238.21KB
   Metrics [max cost:216 ms, min cost:163 ms, average cost:191.50 ms, average tps:14.23]
    
   Task id is: 0653482e-55e6-11ed-afb8-aa665a3c7f26
   The authorized prefix is empty, all the content of bucket can be accessed
   ```
