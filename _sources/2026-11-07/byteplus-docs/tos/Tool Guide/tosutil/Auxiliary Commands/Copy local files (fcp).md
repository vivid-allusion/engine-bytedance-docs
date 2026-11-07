---
title: "Copy local files (fcp)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Copy-local-files-fcp"
---

You can use the `fcp` command to copy local files or folders from the source to the destination.

<span id="a2c79f76"></span>
## Command syntax


* Copy a single file

   
   <Tabs>
   <Tab zoneid="5NHUozVx" title="Linux/macOS">
   <TabTitle>Linux/macOS</TabTitle>
   
   &nbsp;
   
   ```Bash
   ./tosutil fcp file_url1 file_url2|folder_url2 [-dryRun] [-link] [-tempFileDir=xxx] [-useTempFile] [-u] [-vchecksum] [-dfo] [-fsync] [-rbs=1MB] [-wbs=1MB] [-rdio] [-rmmap] [-wdio] [-wmmap] [-ea=xxx] [-sdk=xxx] [-dek=xxx] [-fr] [-o=xxx] [-nftr]
   ```
   
   
   
   
   
   </Tab>
   <Tab zoneid="uASU80Ph" title="Windows">
   <TabTitle>Windows</TabTitle>
   
   &nbsp;
   
   ```Bash
   tosutil fcp file_url1 file_url2|folder_url2 [-dryRun] [-link] [-tempFileDir=xxx] [-useTempFile] [-u] [-vchecksum] [-dfo] [-fsync] [-rbs=1MB] [-wbs=1MB] [-rdio] [-rmmap] [-wdio] [-wmmap] [-ea=xxx] [-sdk=xxx] [-dek=xxx] [-fr] [-o=xxx]
   ```
   
   
   
   
   
   </Tab>
   </Tabs>
   

* Copy a folder

   
   <Tabs>
   <Tab zoneid="rQliH6Wj" title="Linux/macOS">
   <TabTitle>Linux/macOS</TabTitle>
   
   &nbsp;
   
   ```Bash
   ./tosutil fcp fold_url1 fold_url2 -r [-dryRun] [-link] [-tempFileDir=xxx] [-useTempFile] [-u] [-vchecksum] [-dfo] [-fsync] [-rbs=1MB] [-wbs=1MB] [-rdio] [-rmmap] [-wdio] [-wmmap] [-ea=xxx] [-sdk=xxx] [-dek=xxx] [-flat] [-j=1] [-nfj=1] [-include=*.xxx] [-exclude=*.xxx] [-timeRange=time1-time2] [-at] [-dmf] [-o=xxx] [-nftr]
   ```
   
   
   
   
   
   </Tab>
   <Tab zoneid="MHiw8dW1" title="Windows">
   <TabTitle>Windows</TabTitle>
   
   &nbsp;
   
   ```Bash
   tosutil fcp fold_url1 fold_url2 -r [-dryRun] [-link] [-tempFileDir=xxx] [-useTempFile] [-u] [-vchecksum] [-dfo] [-fsync] [-rbs=1MB] [-wbs=1MB] [-rdio] [-rmmap] [-wdio] [-wmmap] [-ea=xxx] [-sdk=xxx] [-dek=xxx] [-flat] [-j=1] [-nfj=1] [-include=*.xxx] [-exclude=*.xxx] [-timeRange=time1-time2] [-at] [-dmf] [-o=xxx]
   ```
   
   
   
   
   
   </Tab>
   </Tabs>
   

* Resume failed tasks

   
   <Tabs>
   <Tab zoneid="NdngYZk8" title="Linux/macOS">
   <TabTitle>Linux/macOS</TabTitle>
   
   &nbsp;
   
   ```Bash
   ./tosutil fcp -recover=xxx [-dryRun] [-link] [-tempFileDir=xxx] [-useTempFile] [-u] [-vchecksum] [-dtf] [-dfo] [-fsync] [-rbs=1MB] [-wbs=1MB] [-rdio] [-rmmap] [-wdio] [-wmmap] [-ea=xxx] [-sdk=xxx] [-dek=xxx] [-j=1] [-nfj=1] [-include=*.xxx] [-exclude=*.xxx] [-timeRange=time1-time2] [-at] [-dmf] [-o=xxx] [-nftr]
   ```
   
   
   
   
   
   </Tab>
   <Tab zoneid="4oAAzPdv" title="Windows">
   <TabTitle>Windows</TabTitle>
   
   &nbsp;
   
   ```Bash
   tosutil fcp -recover=xxx [-dryRun] [-link] [-tempFileDir=xxx] [-useTempFile] [-u] [-vchecksum] [-dtf] [-dfo] [-fsync] [-rbs=1MB] [-wbs=1MB] [-rdio] [-rmmap] [-wdio] [-wmmap] [-ea=xxx] [-sdk=xxx] [-dek=xxx] [-j=1] [-nfj=1] [-include=*.xxx] [-exclude=*.xxx] [-timeRange=time1-time2] [-at] [-dmf] [-o=xxx]
   ```
   
   
   
   
   
   </Tab>
   </Tabs>
   

* Test read/write performance using a local file

   
   <Tabs>
   <Tab zoneid="59LMzWbB" title="Linux/macOS">
   <TabTitle>Linux/macOS</TabTitle>
   
   &nbsp;
   
   ```Bash
   ./tosutil fcp file_url -dt=xxx [-ds=10MB] [-link] [-tempFileDir=xxx] [-useTempFile] [-dfo] [-fsync] [-rbs=1MB] [-wbs=1MB] [-rdio] [-wdio] [-wmmap] [-nftr]
   ```
   
   
   
   
   
   </Tab>
   <Tab zoneid="EvLk3jc2" title="Windows">
   <TabTitle>Windows</TabTitle>
   
   &nbsp;
   
   ```Bash
   tosutil fcp file_url -dt=xxx [-ds=10MB] [-link] [-tempFileDir=xxx] [-useTempFile] [-dfo] [-fsync] [-rbs=1MB] [-wbs=1MB] [-rdio] [-wdio] [-wmmap]
   ```
   
   
   
   
   
   </Tab>
   </Tabs>
   


<span id="2734e575"></span>
## Parameters


|**Parameter** |**Type** |**Description** |
|---|---|---|
|file_url1<br><br>folder_url1 |String |Local source file/folder path. When it is a source folder, use with the `-r` parameter. |
|file_url2<br><br>folder_url2 |String |Local target file or folder path. |
|\-r |Bool |Recursively copy folders. |
|\-dryRun |Bool |Run in test mode without performing actual operations. |
|\-link |Bool |Copy the real path pointed to by the symbolic link file/folder. |
|\-tempFileDir |String |Folder for saving temporary files during copying. Defaults to the same parent folder as the file being copied. |
|\-useTempFile |Bool |Writes to a temporary file first during copying, then renames it to the final file. |
|\-recover |String |Task ID of the list file for the recovery copy task to be restored. |
|\-u |Bool |Use incremental copy for files. After setting this option, it compares the source and target. It is recommended in the following cases:<br><br><br>* The target does not exist.<br><br>* The file size on the target differs from the source.<br><br>* Execute the operation when the target's last modified time is earlier than the source's last modified time. |
|\-vchecksum |Bool |Verify data consistency during copying using the CRC64 algorithm. |
|\-dfo |Bool |On Linux/MacOS systems, copying does not forcibly overwrite if the local executable is running. |
|\-fsync |Bool |Use fsync to flush disk when copying. |
|\-rbs |String |Buffer size for reading source, in bytes. Defaults to the `readBufferIoSize` setting in the configuration file. |
|\-wbs |String |Set the buffer size for the target write, in bytes. The default is the `writeBufferIoSize` value in the configuration file. |
|\-rdio |Bool |Use direct io when reading the source on Linux/MacOS operating systems. |
|\-rmmp |Bool |On Linux/MacOs operating systems, mmap is used when reading the source end. |
|\-wdio |Bool |Use direct io when writing to the target on Linux/MacOS systems. |
|\-wmmp |Bool |Use mmap for writing the target on Linux/macOS. Setting this ignores the `useTempFile` option. |
|\-ea |String |The algorithm used to encrypt and decrypt local files during copying. Supported values are:<br><br><br>* aes256<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Currently using the aes256 + CTR mode encryption algorithm.</div><br> |
|\-eam |String |The algorithm mode used to encrypt and decrypt local files during copying. Supported values are as follows:<br><br><br>* CTR<br><br>* CBC<br><br><br>The default is CTR. |
|\-sdk |String |When copying, decrypt the source key. If the decryption algorithm is aes256, the length must be 32 characters. |
|\-dek |String |Encrypt the target key during copying; when the encryption algorithm is aes256, the key length must be 32 bytes. |
|\-flat |Bool |Do not include relative parent directories when copying files. |
|\-j |Integer |Maximum concurrency for batch tasks, defaults to `defaultJobs` in the configuration file, default value is 3. |
|\-nfj |Integer |Maximum concurrency for processing small files (less than 1MB) in batch tasks. |
|\-include |String |Match patterns for containing file names when copying; supports`?`and`*`as wildcards and # as a separator. |
|\-exclude |String |When copying, the name matching pattern that does not include files supports`?`and`*`as wildcards and # as a separator. |
|\-timeRange |String |Match pattern for the time range of the file's last modification time when copying, format: `YYYYMMDDHHmmSS-YYYYMMDDHHmmSS`. |
|\-at |Bool |List of files in the folder whose last access time meets the timeRange option. |
|\-ddo |Bool |Folders themselves will not be uploaded as separate objects. |
|\-dmf |Bool |Setting name match mode and time range match mode does not apply to folders. |
|\-dt |String |Type for testing read or write separately. Supported values are as follows:<br><br><br>* source<br><br>* destination |
|\-ds |String |Set the file size for testing single\-stream read or write operations, in bytes. The default is 10MB. |
|\-fr |Bool |Generate a result manifest file when operating a single file. |
|\-o |String |Folder for the generated result list file, defaults to `defaultOutputDir` in the configuration file. |
|\-nftr |Bool |Do not specify file size with the `Truncate` parameter when creating a new file. |


<span id="91836fb9"></span>
## Examples

<span id="a00b1bda"></span>
### Copy a single file

The following command copies the **object** file in the  **/Users/Downloads/TOS/tosutil** folder to  **/Users/Downloads/TOS/tosutil/object1**.


* Command

   ```Plain
   ./tosutil fcp /Users/Downloads/TOS/tosutil/object /Users/Downloads/TOS/tosutil/object1
   ```
   

* Output

   ```Plain
   Start at 2023-11-27 04:46:38.577567 +0000 UTC
   
   
   Jobs:          5                   VerifyChecksum: false
   TempFileDir: auto
   
   [---------------------------------------------] 100.00% ?/s 15.09MB/15.09MB 7ms
    
   Copy local file/folder successfully, 15.09MB, n/a, /Users/Downloads/TOS/tosutil/object --> /Users/Downloads/TOS/tosutil/object1, cost [7]
   ```
   


<span id="c2420507"></span>
### Copy a folder

The following command copies all files from the  **/Users/Downloads/TOS/tosutil/folder1** folder to  **/Users/Downloads/TOS/tosutil/folder2**.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This command copies the folder itself; after copying, all files will be inside the <strong>folder2</strong> folder.</div>



* Command

   ```Plain
   ./tosutil fcp /Users/Downloads/TOS/tosutil/folder1  /Users/Downloads/TOS/tosutil/folder2 -r
   ```
   

* Output

   ```Plain
   Start at 2023-11-27 05:02:14.869508 +0000 UTC
   
   
   Jobs:          5                   VerifyChecksum: false
   OutputDir: /Users/bytedance/.tosutil_output
   TempFileDir: auto
   
   [-------------------------------] 100.00% tps:0.00 ?/s 4/4 30.18MB/30.18MB 11ms
   Succeed count is:   4         Failed count is:    0
   Succeed bytes is:   30.18MB
   Metrics [max cost:11 ms, min cost:0 ms, average cost:5.25 ms, average tps:333.33]
   
   Task id is: 2190c0c4-8ce2-11ee-8d1f-b645e1163e54
   ```
   


<span id="bc9ace5a"></span>
### Test file read/write performance

The following command tests the read performance of the **object.mov** file in the  **/Users/Downloads/TOS/tosutil/folder1** folder.


* Command

   ```Plain
   ./tosutil fcp /Users/bytedance/Downloads/TOS/tosutil/180/folder1/object.mov -dt=source
   ```
   

* Output

   ```Plain
   Start at 2023-12-18 09:42:11.792216 +0000 UTC
   
   
   Jobs:          5                   VerifyChecksum: false
   TempFileDir: auto
   
   [---------------------------------------------] 100.00% ?/s 10.00MB/10.00MB 4ms
   
   Detect copy local file/folder successfully, 10.00MB, n/a, /Users/bytedance/Downloads/TOS/tosutil/folder1/object.mov --> [dustbin], cost [4]
   ```
   


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more example commands for upload scenarios, see <a href="https://docs.byteplus.com/docs/tos/Upload-object-example">Upload examples</a>.</div>
