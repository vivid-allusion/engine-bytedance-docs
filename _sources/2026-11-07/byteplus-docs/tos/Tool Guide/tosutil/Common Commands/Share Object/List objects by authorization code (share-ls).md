---
title: "List objects by authorization code (share-ls)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-objects-by-authorization-code-share-ls"
---

You can use the `share-ls` command with an authorization code to query objects in a bucket. The returned object list is sorted in lexicographical order by object name.

<span id=".5ZG95Luk5qC85byP"></span>
## Command format


<Tabs>
<Tab zoneid="fgUsrlFJ" title="Linux/macOS">
<TabTitle>Linux/macOS</TabTitle>

* List objects or list multi\-version objects in the bucket based on the directly entered authorization code


```Bash
./tosutil share-ls authorization_code [-key=xxx] [-s] [-d] [-v] [-marker=xxx] [-versionIdMarker==xxx] [-bf=xxx] [-limit=1] [-bt=xxx] [-et=xxx] [-conf=xxx]
```



* List objects or list multiple versions of objects in the bucket based on the authorization code file path


```Bash
./tosutil share-ls file://authorization_code_file_url [-key=xxx] [-s] [-d] [-v] [-marker=xxx] [-versionIdMarker==xxx] [-bf=xxx] [-limit=1] [-bt=xxx] [-et=xxx] [-conf=xxx]
```





</Tab>
<Tab zoneid="smuosvRZ" title="Windows">
<TabTitle>Windows</TabTitle>

* List objects or list object versions in the bucket based on the directly entered authorization code


```Bash
tosutil share-ls authorization_code [-key=xxx] [-s] [-d] [-v] [-marker=xxx] [-versionIdMarker==xxx] [-bf=xxx] [-limit=1] [-et=xxx] [-conf=xxx]
```



* List objects or list object versions in the bucket based on the file path of the authorization code


```Bash
tosutil share-ls file://authorization_code_file_url [-key=xxx] [-s] [-d] [-v] [-marker=xxx] [-versionIdMarker==xxx] [-bf=xxx] [-limit=1] [-et=xxx] [-conf=xxx]
```





</Tab>
</Tabs>


<span id="1UGdTHYF"></span>
## Parameters

For the description of common optional parameters, refer to [general parameters](https://docs.byteplus.com/docs/tos/Command-format#.6YCa55So5Y-v6YCJ5Y-C5pWw).


|**Parameter name** |**Type** |**Description** |
|---|---|---|
|authorization_code |String |Authorization code used. |
|file://authorization_code_file_url |String |Path to the authorization code file used. |
|\-key |String |Object name when listing a single object or the prefix for the listed objects. |
|\-s |Bool |Display query results in a simplified format. |
|\-d |Bool |List only objects and subdirectories in the current directory without recursively listing all objects and subdirectories. |
|\-v |Bool |List multi\-version objects in the bucket. If there are historical versions, the results include both the latest and historical objects. |
|\-marker |String |Specify the start position for listing multi\-version objects in the bucket; the results include the latest and historical versions of objects. |
|\-versionIdMarker |String |Starting position for listing multi\-version objects in the bucket, must be used with `-marker`. the returned result includes all objects after the specified parameter, sorted by object name and version ID in dictionary order. |
|\-bf |Enum |Display format for the number of bytes returned when listing objects in the bucket. Supported values:<br><br><br>* `human-readable`<br><br>* `raw` |
|\-limit |Integer |Maximum number of listed results, up to 100,000. |
|\-bt |String |bucket type. Valid values:<br><br><br>* `fns`: flat bucket.<br><br>* `hns`: hierarchical bucket.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the bucket type is not specified, the bucket type will be obtained from the bucket metadata by default when listing files; when listing directories, the bucket type cannot be identified, which may cause request errors.</div><br> |
|\-et |Enum |Specify the encoding type for encoding the returned object names. Currently only `url` is supported. |


<span id=".5L2_55So56S65L6L"></span>
## Example

<span id="0dfcb91b"></span>
### List all objects in a bucket using the authorization code path and extraction code

The following command lists all objects in the **bucketname** bucket. The authorization code path used is  **/tmp/tosutil/authorization_code**.


* Command

   ```bash
   ./tosutil share-ls file:///tmp/tosutil/authorization_code
   ```
   

* Back

   ```plain
   Start at 2022-12-26 11:38:01.418696 +0000 UTC
   
   Listing objects .
   
   Object list:
   key                                               LastModified                  Size      StorageClass        ETag
   tos://bucketname/file/file1.png                   2022-10-27T09:38:41Z          55.98KB   STANDARD            "d411110de34d37ce8ca0ad0e4dd3****"
    
   tos://bucketname/file/file2.png                   2022-10-27T09:38:56Z          74.96KB   STANDARD            "0216c42adc88aadf0078dd6e4139****"
    
   tos://bucketname/file/file3.png                   2022-10-27T09:39:05Z          499B      STANDARD            "8a5f4cb1a4d760e32f9ee51482c3****"
    
   tos://bucketname/object1.png                      2022-10-27T09:37:08Z          55.98KB   STANDARD            "d411110de34d37ce8ca0ad0e4dd3****"
    
   tos://bucketname/object2.png                      2022-10-27T09:37:15Z          56.76KB   STANDARD            "0eaa38cb4273c20a8ec8a6345aeb****"
    
   tos://bucketname/object3.png                      2022-10-27T09:37:21Z          74.96KB   STANDARD            "0216c42adc88aadf0078dd6e4139****"
    
   Total size of bucket is: 319.14KB
   File number is: 6
   The authorized prefix is empty, all the content of bucket can be accessed
   ```
   


<span id="96de15bc"></span>
### List all versions of an object in a bucket using the authorization code path and extraction code

The following command lists all versions of the **object1.png** object in the **bucketname** bucket. The authorization code path used is  **/tmp/tosutil/authorization_code**.


* Command

   ```bash
   ./tosutil share-ls file:///tmp/tosutil/authorization_code -key=object1.png -v -s
   ```
   

* Back

   ```plain
   Start at 2022-10-27 09:40:42.574241 +0000 UTC
    
   Listing versioning objects .
    
   Versioning Object list:
   tos://bucketname/object1.png
    
   Total size of prefix [object1.png] is: 55.98KB
   Versioning file number is: 1
   DeleteMarker number is: 0
   The authorized prefix is empty, all the content of bucket can be accessed
   ```
   


<span id="8b87753f"></span>
### List all objects in a directory within a bucket using the authorization code path and extraction code

The following command lists the objects in the **file** folder of the **bucketname** bucket. The authorization code path used is  **/tmp/tosutil/authorization_code**.


* Command

   ```bash
   ./tosutil share-ls file:///tmp/tosutil/authorization_code -key=file -s
   ```
   

* Back

   ```plain
   Start at 2022-10-27 09:42:54.896663 +0000 UTC
    
   Listing objects .
   
   Object list:
   tos://bucketname/file/file1.png
   tos://bucketname/file/file2.png
   tos://bucketname/file/file3.png
    
   Total size of prefix [file] is: 131.43KB
   File number is: 3
   The authorized prefix is empty, all the content of bucket can be accessed
   ```
   


<span id="5b922a07"></span>
### Use the authorization code and extraction code to list all objects in a specific directory within the bucket

The following command lists objects in the **file** folder within the **bucketname** bucket using the authorization code of the **file** folder. The authorization code used is **xxx**.


* Command

   ```bash
   ./tosutil share-ls xxx -key=file/ -s
   ```
   

* Back

   ```plain
   Start at 2022-10-27 09:42:54.896663 +0000 UTC
    
   Listing objects .
   
   Object list:
   tos://bucketname/file/file1.png
   tos://bucketname/file/file2.png
   tos://bucketname/file/file3.png
    
   Total size of prefix [file/] is: 131.43KB
   File number is: 3
   The authorized prefix is [file/]
   ```
