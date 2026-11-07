---
title: "Delete buckets or objects, or abort multipart uploads (rm)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Delete-a-bucket-object-or-shard-upload-task-rm"
---

You can use the `rm` command to delete buckets or objects, or abort multipart uploads.

<span id=".5Yig6Zmk5qG2"></span>
## Delete buckets

<span id=".5rOo5oSP5LqL6aG5"></span>
### Notes


* Before deleting a bucket, ensure all objects and parts inside are deleted.

* The tool will prompt you for confirmation when deleting resources. The meanings of the input values are as follows:

   * `y`: Confirms deletion.

   * `n`: Cancels deletion; no deletion will be performed.


<span id=".5ZG95Luk5qC85byP"></span>
### Command format


<Tabs>
<Tab zoneid="mtws30cB" title="Linux/macOS">
<TabTitle>Linux/macOS</TabTitle>

&nbsp;

```Bash
./tosutil rm tos://bucket [-f] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
<Tab zoneid="ZjsLut12" title="Windows">
<TabTitle>Windows</TabTitle>

&nbsp;

```Bash
tosutil rm tos://bucket [-f] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
</Tabs>


<span id="SKNYGrSf"></span>
### Parameters

For descriptions of common optional parameters, see [General parameters](https://docs.byteplus.com/docs/tos/Command-format#.6YCa55So5Y-v6YCJ5Y-C5pWw).


|**Parameter** |**Type** |**Description** |
|---|---|---|
|bucket |String |Name of the bucket to delete. |
|\-f |Bool |Force the operation without confirmation prompts. |


<span id=".5L2_55So56S65L6L"></span>
### Example

The following command deletes the **bucketname1** bucket.


* Command


```Plain
./tosutil rm tos://bucketname1
```



* Output


```Plain
Do you want delete bucket [bucketname1] ? Please input (y/n) to confirm:
y
Start at 2022-10-27 11:02:34.953673 +0000 UTC
 
Delete bucket [bucketname1] successfully!
```


<span id=".5Yig6Zmk5a-56LGh"></span>
## Delete objects

<span id=".5ZG95Luk5qC85byP"></span>
### Command format


<Tabs>
<Tab zoneid="FFayWX7VSw" title="Linux/macOS">
<TabTitle>Linux/macOS</TabTitle>

* Delete a single object


```Bash
./tosutil rm tos://bucket/key [-f] [-versionId=xxx] [-fr] [-o=xxx] [-bt=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```



* Delete multiple objects


```Bash
./tosutil rm tos://bucket/[prefix] -r [-f] [-j=1] [-v] [-o=xxx] [-bt=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```



</Tab>
<Tab zoneid="sieUmCyfEA" title="Windows">
<TabTitle>Windows</TabTitle>

* Delete a single object


```Bash
tosutil rm tos://bucket/key [-f] [-versionId=xxx] [-fr] [-o=xxx] [-bt=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```



* Delete multiple objects


```Bash
tosutil rm tos://bucket/[prefix] -r [-f] [-j=1] [-v] [-o=xxx] [-bt=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
</Tabs>


<span id=".5Y-C5pWw6K-05piO"></span>
### Parameters

For descriptions of common optional parameters, see [General parameters](https://docs.byteplus.com/docs/tos/Command-format#.6YCa55So5Y-v6YCJ5Y-C5pWw).


|**Parameter** |**Type** |**Description** |
|---|---|---|
|bucket |String |Bucket name. |
|key |String |Object name. |
|prefix |String |Object name prefix for batch operations. |
|\-r |Bool |Execute batch delete operation. |
|\-f |Bool |Force the operation without asking for confirmation. |
|\-fr |Bool |Generate result list file when deleting an object or aborting a multipart upload. |
|\-j |Integer |The maximum concurrency for batch tasks defaults to `defaultJobs` in the config file. |
|\-v |Bool |Batch delete multiple versions of objects and multiple version delete markers by specified object name prefix. |
|\-versionId |String |Version ID of the single object to be deleted. |
|\-o |String |Folder for generated result list files, default is `defaultOutputDir` in the configuration file. |
|\-bt |String |Type of the bucket. Valid values:<br><br><br>* `fns`: FNS bucket.<br><br>* `hns`: HNS bucket.<br><br><br>If the bucket type is not specified, the type will be obtained from the bucket metadata by default. |


<span id=".5L2_55So56S65L6L"></span>
### Examples

<span id="41649876"></span>
#### Delete a single object

The following command deletes the **object1.png** object in the **bucketname** bucket.


* Command

   ```Plain
   ./tosutil rm tos://bucketname/object1.png
   ```
   

* Output

   ```Plain
   Do you want delete object [object1.png] in the bucket [bucketname]? Please input (y/n) to confirm:
   y
   Start at 2022-10-27 11:03:01.983467 +0000 UTC
    
   Delete object [object1.png] in the bucket [bucketname] successfully, cost [92], request id [76bf485a65668d09635a6566-ac1ea1cc-1oo0f8-DO-cb-tos-bj]
   ```
   


<span id="b69d15b0"></span>
#### Delete multiple objects

The following command deletes objects with the prefix **object** in the **bucketname** bucket.


* Command

   ```Plain
   ./tosutil rm tos://bucketname/object -r
   ```
   

* Output

   ```Plain
   Do you want start to delete objects using the prefix [object] in the bucket [bucketname] ? Please input (y/n) to confirm:
   y
   Start at 2022-10-27 11:03:22.970964 +0000 UTC
    
   [--------------------------------------------------] 100.00% tps:0.00 3/3 159ms
   Succeed count is:   3         Failed count is:    0
   Metrics [max cost:92 ms, min cost:90 ms, average cost:91.00 ms, average tps:18.40]
    
   Task id is: f93dea58-55e6-11ed-9e20-aa665a3c7f26
   ```
   


<span id=".5Yig6Zmk5YiG54mH5LiK5Lyg5Lu75Yqh"></span>
## Abort multipart uploads

<span id=".5ZG95Luk5qC85byP"></span>
### Command format


<Tabs>
<Tab zoneid="Zi20dat3x5" title="Linux/macOS">
<TabTitle>Linux/macOS</TabTitle>

* Abort a multipart upload


```Bash
./tosutil rm tos://bucket/key -m -u=xxx [-f] [-fr] [-o=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```



* Abort multipart uploads in batches


```Bash
./tosutil rm tos://bucket/[prefix] -m -r [-f] [-j=1] [-o=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
<Tab zoneid="OTFBOfuRKa" title="Windows">
<TabTitle>Windows</TabTitle>

* Abort a multipart upload


```Bash
tosutil rm tos://bucket/key -m -u=xxx [-f] [-fr] [-o=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```



* Abort multipart uploads in batches


```Bash
tosutil rm tos://bucket/[prefix] -m -r [-f] [-j=1] [-o=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```



</Tab>
</Tabs>


<span id=".5Y-C5pWw6K-05piO"></span>
### Parameters

For the description of common optional parameters, see [General parameters](https://docs.byteplus.com/docs/tos/Command-format#.6YCa55So5Y-v6YCJ5Y-C5pWw).


|**Parameter** |**Type** |**Description** |
|---|---|---|
|bucket |String |Bucket name. |
|key |String |The object name. |
|prefix |String |Prefix of object names for batch operations. |
|\-r |Bool |Perform batch delete operation. |
|\-f |Bool |Force the operation without confirmation prompts. |
|\-fr |Bool |Generate a result list file when deleting an object or aborting a multipart upload. |
|\-j |Integer |maximum concurrency for batch tasks, default is `defaultJobs` in the configuration file. |
|\-v |Bool |Batch delete multiple versions of objects and multiple version deletion markers by specified object name prefix. |
|\-m |Bool |Delete multipart upload mode. |
|\-u |String |ID of the single multipart upload to be deleted.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can list multipart upload task IDs using the <code>ls</code> command.</div><br> |
|\-o |String |Folder for generating the result list file, defaulting to `defaultOutputDir` in the configuration file. |


<span id=".5L2_55So56S65L6L"></span>
### Examples

<span id="62d90d95"></span>
#### Abort a multipart upload

The following command abort the multipart upload task with task ID **6b2292652f8fedf496f5495a6668**\*\*\*\*.


* Command

   ```Plain
   ./tosutil rm tos://bucketname/InstallationPackage/Postman.app/Contents/Resources/app.asar -m -u=6b2292652f8fedf496f5495a6668****
   ```
   

* Output

   ```Plain
   Do you want to abort the multipart upload [Installation package/Postman.app/Contents/Resources/app.asar] in the bucket [bucketname]? Please input (y/n) to confirm:
   y
   Start at 2022-10-27 11:12:35.619554 +0000 UTC
    
   Abort multipart upload [Installation Package/Postman.app/Contents/Resources/app.asar] in the bucket [bucketname] successfully, took [147], request id [76bf485a67a3bac0635a67a3-ac1ea1cc-1oo0oN-AMU-cb-tos-bj]
   ```
   


<span id="2e62cfdd"></span>
#### Abort multipart uploads in batches


* Command

   ```Plain
   ./tosutil rm tos://bucketname/Visual -m -r
   ```
   

* Output

   ```Plain
   Do you want start to abort multipart uploads using the prefix [Visual] in the bucket [bucketname] ? Please input (y/n) to confirm:
   y
   Start at 2022-10-27 09:52:18.41894 +0000 UTC
    
   [--------------------------------------------------] 100.00% tps:0.00 2/2 137ms
   Succeed count is:   2         Failed count is:    0
   Metrics [max cost:97 ms, min cost:51 ms, average cost:74.00 ms, average tps:14.18]
    
   Task id is: 0b5ee390-55dd-11ed-b7d9-aa665a3c7f26
   ```
   


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more example commands for deletion scenarios, see <a href="https://docs.byteplus.com/docs/tos/Delete-object-example">Deletion examples</a>.</div>
