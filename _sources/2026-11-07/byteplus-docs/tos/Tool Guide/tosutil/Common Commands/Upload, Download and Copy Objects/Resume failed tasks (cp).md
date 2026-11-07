---
title: "Resume failed tasks (cp)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Resume-failed-tasks--cp"
---

You can use the `cp` command to resume previously failed tasks.

<span id=".5ZG95Luk6K-t5rOV"></span>
## Command syntax


<Tabs>
<Tab zoneid="oOiGpYaG" title="Linux/macOS">
<TabTitle>Linux/macOS</TabTitle>

&nbsp;

```Bash
./tosutil cp -recover=xxx [-dryRun] [-tempFileDir=xxx] [-u] [-vchecksum] [-j=1] [-p=1] [-threshold=52428800] [-nfj=1] [-ps=auto] [-cpd=xxx] [-acl=xxx] [-meta=aaa:bbb#ccc:ddd] [-sse=xxx] [-sseKeyId=xxx] [-contentType=xxx] [-contentDisposition=xxx] [-contentEncoding=xxx] [-contentLanguage=xxx] [-cacheControl=xxx] [-expires=xxx] [-include=*.xxx] [-exclude=*.xxx] [-timeRange=time1-time2] [-at] [-ddo] [-dmf] [-o=xxx] [-bt=xxx] [-sbt=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
<Tab zoneid="IpFZssmT" title="Windows">
<TabTitle>Windows</TabTitle>

&nbsp;

```Bash
tosutil cp -recover=xxx [-dryRun] [-tempFileDir=xxx] [-u] [-vchecksum] [-j=1] [-p=1] [-threshold=52428800] [-nfj=1] [-ps=auto] [-cpd=xxx] [-acl=xxx] [-meta=aaa:bbb#ccc:ddd] [-sse=xxx] [-sseKeyId=xxx] [-contentType=xxx] [-contentDisposition=xxx] [-contentEncoding=xxx] [-contentLanguage=xxx] [-cacheControl=xxx] [-expires=xxx] [-include=*.xxx] [-exclude=*.xxx] [-timeRange=time1-time2] [-at] [-ddo] [-dmf] [-o=xxx] [-bt=xxx] [-sbt=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
</Tabs>


&nbsp;

<span id=".5Y-C5pWw6K-05piO"></span>
## Parameters

For descriptions of common optional parameters, see [general parameters](https://docs.byteplus.com/docs/tos/Command-format#.6YCa55So5Y-v6YCJ5Y-C5pWw).


|**Parameter Name** |**Type** |**Description** |
|---|---|---|
|\-dryRun |Bool |Run in test mode without performing actual upload, download, or copy operations. |
|\-tempFileDir |String |Folder to save temporary files during multipart download, defaults to `defaultTempFileDir` in the configuration file.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If this value is empty and <code>defaultTempFileDir</code> in the configuration file is also empty, temporary files generated during multipart download will be saved in the same directory as the file being downloaded and end with <code>.tos.temp</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Since temporary files generated during download are saved in this directory, ensure tosutil has write permission for this path. The available space on this path should exceed the size of the object being downloaded.</div><br> |
|\-recover |String |The task ID of the result list file for a resumable upload, download, or copy object task. For details on obtaining the task ID, refer to [View Batch Task Operation List](https://docs.byteplus.com/docs/tos/View-batch-operation-task-list). |
|\-u |Bool |For incremental upload, download, or copying objects, setting this parameter compares the source and target ends. We recommend using this parameter in the following scenarios:<br><br><br>* The target does not exist.<br><br>* The file size on the target differs from that on the source.<br><br>* Execute corresponding operations when the destination's last modification time is earlier than the source's last modification time. |
|\-vchecksum |Bool |Verify data consistency with the CRC64 algorithm when uploading or downloading objects. |
|\-j |Integer |The maximum concurrency for batch tasks defaults to `defaultJobs` in the configuration file, with a default value of 3. |
|\-p |Integer |Maximum concurrency for each shard task, defaulting to `defaultParallels` in the configuration file, with a default value of 1. |
|\-threshold |Integer |The threshold for enabling shard tasks, in bytes. The default value is `defaultBigfileThreshold` from the configuration file.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Supports capacity units. For example, setting 1MB represents 1,048,576 bytes.</div><br> |
|\-nfj |Integer |The maximum concurrency for batch tasks handling regular files or objects (non\-sharded tasks). Defaults to the maximum concurrency of batch tasks. Effective only during batch operations. |
|\-ps |Integer/String |The segment size of each chunk task in bytes, defaulting to `defaultPartSize` from the configuration file.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Supports configuration with capacity units, for example, setting 1MB represents 1,048,576 bytes.</div><br> |
|\-cpd |String |The folder for generating breakpoint record files defaults to `defaultCheckpointDir` in the configuration file. |
|\-acl |String |Predefined access policies that can be specified when uploading or copying objects. Supported values:<br><br><br>* private<br><br>* public\-read<br><br>* public\-read\-write<br><br>* authenticated\-read<br><br>* bucket\-owner\-read<br><br>* bucket\-owner\-full\-control |
|\-meta |String |Custom metadata specified when uploading or copying an object. |
|\-sse |String |The server\-side encryption algorithm used when uploading or copying the object. Supported values:<br><br><br>* aes256<br><br>* Kms<br><br><br>defaults to defaultSse in the configuration file. |
|\-sseKeyId |String |When uploading or copying an object with server\-side encryption using kms, specify the kms key, defaulting to defaultSseKeyId in the configuration file. |
|\-contentType |String |Set the object's Content\-Type when uploading or copying objects. |
|\-contentDisposition |String |Set the object's Content\-Disposition when uploading or copying objects. |
|\-contentEncoding |String |Set the Content\-Encoding of the object when uploading or copying objects. |
|\-contentLanguage |String |Set the object's Content\-Language when uploading or copying the object. |
|\-cacheControl |String |Set the object's Cache\-Control when uploading or copying the object. |
|\-expires |String |Set the object's Expires when uploading or copying, format: YYYYMMDDHHmmSS. |
|\-include |String |Use name matching patterns for files when uploading, downloading, or copying, supporting`?`and`*`as wildcards and # as a separator. |
|\-exclude |String |Supports name matching patterns without files when uploading, downloading, or copying`?`and`*`Use \* as a wildcard and # as a separator. |
|\-timeRange |String |The time range pattern for the file's last modified time when uploading, downloading, or copying, in the format: `YYYYMMDDHHmmSS-YYYYMMDDHHmmSS`. |
|\-at |Bool |List of files in the upload folder whose last access time matches the `-timeRange` parameter. |
|\-ddo |Bool |The folder itself is not uploaded as a separate object during upload. |
|\-dmf |Bool |Setting name matching patterns `-include/-exclude` and time range matching pattern `-timeRange` does not apply to folders. |
|\-o |String |Folder for generating the result list file, defaulting to `defaultOutputDir` in the configuration file. |
|\-bt |String |Type of source bucket when recovering failed replication tasks. Valid values:<br><br><br>* `fns`: flat bucket.<br><br>* `hns`: hierarchical bucket.<br><br><br>If the bucket type is not specified, the bucket type is retrieved from the bucket metadata by default. |
|\-sbt |String |The type of target bucket when resuming failed copy tasks. Valid values:<br><br><br>* `fns`: flat bucket.<br><br>* `hns`: hierarchical bucket.<br><br><br>If the bucket type is not specified, it is obtained from the bucket metadata by default. |
