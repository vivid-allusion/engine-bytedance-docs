---
title: "List resources under the account (ls)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-the-resources-under-the-account-ls"
---

You can use the `ls` command to list resource information under the account, including buckets, objects within buckets, and multipart upload tasks in buckets.

<span id=".5YiX5Li-5qG2"></span>
## List buckets

<span id=".5ZG95Luk5qC85byP"></span>
### Command format


<Tabs>
<Tab zoneid="wVHjQSHoPZ" title="Linux/macOS">
<TabTitle>Linux/macOS</TabTitle>

&nbsp;

```Bash
./tosutil ls [-s] [-limit=1] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
<Tab zoneid="c5JwCCk5SG" title="Windows">
<TabTitle>Windows</TabTitle>

&nbsp;

```Bash
tosutil ls [-s] [-limit=1] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
</Tabs>


<span id=".5Y-C5pWw6K-05piO"></span>
### Parameters

For the description of common optional parameters, see [general parameters](https://docs.byteplus.com/docs/tos/Command-format#.6YCa55So5Y-v6YCJ5Y-C5pWw).


|**Parameter name** |**Type** |**Description** |
|---|---|---|
|\-s |Bool |Display query results in a simplified format, returning only bucket names. |
|\-limit |Integer |Maximum number of results to list, default is 1000. |


<span id=".5L2_55So56S65L6L"></span>
### Example

<span id="93be70db"></span>
#### List all buckets


* Command

   ```Plain
   ./tosutil ls
   ```
   

* Return

   ```Plain
   Start at 2022-10-27 09:29:45.79638 +0000 UTC
   Bucket                   CreationDate                  Location
   tos://db-storage         2022-07-28T06:53:37Z          cn-beijing
    
   tos://tosutil            2022-07-05T09:40:35Z          cn-beijing
   
   Bucket number is: 2
   ```
   


<span id="1c0ef587"></span>
#### List all buckets in a concise format


* Command

   ```Plain
   ./tosutil ls -s
   ```
   

* Return

   ```Plain
   Start at 2022-10-27 09:29:45.79638 +0000 UTC
   tos://db-storage
   tos://tosutil
   Bucket number is: 2
   ```
   


<span id=".5YiX5Li-5qG25YaF5a-56LGh5oiW5YiX5Li-5qG25YaF5aSa54mI5pys5a-56LGh"></span>
## List objects in a bucket or list multiple versions of objects in a bucket

<span id=".5ZG95Luk5qC85byP"></span>
### Command format


<Tabs>
<Tab zoneid="ixpqbd1tqG" title="Linux/macOS">
<TabTitle>Linux/macOS</TabTitle>

&nbsp;

```Bash
./tosutil ls tos://bucket[/prefix] [-s] [-d] [-v] [-marker=xxx] [-versionIdMarker=xxx] [-bf=xxx] [-limit=1] [-bt=xxx] [-et=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
<Tab zoneid="slwJGjN7dT" title="Windows">
<TabTitle>Windows</TabTitle>

&nbsp;

```Bash
tosutil ls tos://bucket[/prefix] [-s] [-d] [-v] [-marker=xxx] [-versionIdMarker=xxx] [-bf=xxx] [-limit=1] [-bt=xxx] [-et=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
</Tabs>


<span id=".5Y-C5pWw6K-05piO"></span>
### Parameters

For the description of common optional parameters, see [general parameters](https://docs.byteplus.com/docs/tos/Command-format#.6YCa55So5Y-v6YCJ5Y-C5pWw).


|**Parameter name** |**Type** |**Description** |
|---|---|---|
|bucket |String |Name of the bucket specified when listing. |
|prefix |String |Specify the prefix of the target object when listing. |
|\-s |Bool |Display query results in a concise format. |
|\-d |Bool |Lists only objects and subdirectories in the current directory, not recursively listing all objects and subdirectories. |
|\-v |Bool |List multiple versions of objects in the bucket. If there are historical versions, the result includes both the latest and historical versions. |
|\-marker |String |Specify the starting point for listing objects in the bucket; the results return all objects after this parameter sorted by object name in dictionary order. |
|\-versionIdMarker |String |List the starting positions of multiple versioned objects in the bucket, must be used with the `-marker` parameter.<br><br>The result returns all objects after this parameter, sorted by object name and version number in lexicographical order. |
|\-bf |Enum |Display format for byte size in object listing results within buckets. Supported values:<br><br><br>* `human-readable`<br><br>* `raw` |
|\-limit |Integer |Maximum number of listed results, default is 1000. |
|\-bt |String |Type of storage bucket. Valid values:<br><br><br>* `fns`: flat bucket.<br><br>* `hns`: hierarchical bucket.<br><br><br>If the bucket type is not specified, the bucket type is obtained from the bucket metadata by default. |
|\-et |Enum |Specify the encoding type for encoding the returned object names. Currently supports only `url`. |


<span id=".5L2_55So56S65L6L"></span>
### Example

<span id="9ad4500c"></span>
#### List the first 1000 objects in a bucket

The following command lists all objects in the **`bucketname`** bucket.


* command

   ```Plain
   ./tosutil ls tos://bucketname
   ```
   

* return

   ```Plain
   Start at 2022-10-27 09:39:39.710781 +0000 UTC
    
   Listing objects .
    
   Folder list:
   tos://bucketname/file/
    
   Object list:
   key                                               LastModified                  Size      StorageClass        ETag
   tos://bucketname/file/file1.png                   2022-10-27T09:38:41Z          55.98KB   STANDARD            "d411110de34d37ce8ca0ad0e4dd3****"
    
   tos://bucketname/file/file2.png                   2022-10-27T09:38:56Z          74.96KB   STANDARD            "0216c42adc88aadf0078dd6e4139****"
    
   tos://bucketname/file/file3.png                   2022-10-27T09:39:05Z          499B      STANDARD            "8a5f4cb1a4d760e32f9ee51482c3****"
    
   tos://bucketname/object1.png                      2022-10-27T09:37:08Z          55.98KB   STANDARD            "d411110de34d37ce8ca0ad0e4dd3****"
    
   tos://bucketname/object2.png                      2022-10-27T09:37:15Z          56.76KB   STANDARD            "0eaa38cb4273c20a8ec8a6345aeb****"
    
   tos://bucketname/object3.png                      2022-10-27T09:37:21Z          74.96KB   STANDARD            "0216c42adc88aadf0078dd6e4139****"
    
   Total size of bucket is: 319.14KB
   Folder number is: 1
   File number is: 6
   ```
   


<span id="1bd34e84"></span>
#### List all versions of the specified object

the following command lists all versions of the **object1.png** object in the **bucketname** bucket.


* command

   ```Plain
   ./tosutil ls -s tos://bucketname/object1.png -v
   ```
   

* return

   ```Plain
   Start at 2022-10-27 09:40:42.574241 +0000 UTC
    
   Listing versioning objects .
    
   Folder list:
   tos://bucketname/file/
    
   Versioning Object list:
   tos://bucketname/file/file1.png
   tos://bucketname/file/file2.png
   tos://bucketname/file/file3.png
   tos://bucketname/object1.png
   tos://bucketname/object2.png
   tos://bucketname/object3.png
   tos://bucketname/screenshot-20220521-154619.png
   tos://bucketname/screenshot-20220521-154719.png
   tos://bucketname/screenshot-20220608-152001.png
    
   DeleteMarker list:
   tos://bucketname/screenshot-20220521-154619.png
   tos://bucketname/screenshot-20220521-154719.png
   tos://bucketname/screenshot-20220608-152001.png
    
   Total size of prefix [object1.png] is: 506.84KB
   Folder number is: 1
   Versioning file number is: 9
   DeleteMarker number is: 3
   ```
   


<span id="2fa8ef03"></span>
#### List objects in the folder

the following command lists objects in the **file** folder within the **bucketname** bucket.


* command

   ```Plain
   ./tosutil ls -s tos://bucketname/file
   ```
   

* return

   ```Plain
   Start at 2022-10-27 09:42:54.896663 +0000 UTC
    
   Listing objects .
    
   Folder list:
   tos://bucketname/file/
    
   Object list:
   tos://bucketname/file/file1.png
   tos://bucketname/file/file2.png
   tos://bucketname/file/file3.png
    
   Total size of prefix [file] is: 131.43KB
   Folder number is: 1
   File number is: 3
   ```
   


<span id=".5YiX5Li-5qG25YaF5YiG54mH5LiK5Lyg5Lu75Yqh"></span>
## List multipart upload tasks in the bucket

<span id=".5ZG95Luk5qC85byP"></span>
### Command format


<Tabs>
<Tab zoneid="miADrRJT5B" title="Linux/macOS">
<TabTitle>Linux/macOS</TabTitle>

&nbsp;

```Bash
./tosutil ls tos://bucket[/prefix] [-s] [-d] -m [-uploadIdMarker=xxx] [-marker=xxx] [-limit=1] [-et=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
<Tab zoneid="IjaEkZ098z" title="Windows">
<TabTitle>Windows</TabTitle>

&nbsp;

```Bash
tosutil ls tos://bucket[/prefix] [-s] [-d] -m [-uploadIdMarker=xxx] [-marker=xxx] [-limit=1] [-et=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
</Tabs>


<span id=".5Y-C5pWw6K-05piO"></span>
### Parameters

see [general parameters](https://docs.byteplus.com/docs/tos/Command-format#.6YCa55So5Y-v6YCJ5Y-C5pWw) for descriptions of common optional parameters.


|**Parameter name** |**Type** |**Description** |
|---|---|---|
|bucket |String |Specify the bucket name when listing. |
|prefix |String |Specify the object name prefix when listing. |
|\-s |Bool |Display query results in a simplified format. |
|\-d |Bool |only list objects and subdirectories in the current directory, not recursively. |
|\-uploadIdMarker |String |Specify the starting point for listing multipart upload tasks in the bucket; must be used together with `-marker`.<br><br>The results return all multipart upload tasks after this parameter, sorted by object name and UploadId in dictionary order. |
|\-limit |Integer |The maximum number of listing results, default is 1000. |
|\-et |Enum |Specify the encoding type for encoding returned object names. Currently, only `url` is supported. |
|\-m |Bool |Represents listing multipart upload tasks within the bucket. |


<span id=".5L2_55So56S65L6L"></span>
### Example usage

the following command queries multipart upload tasks in the **bucketname** bucket.


* Command


```Plain
./tosutil ls tos://bucketname -m
```



* Returns


```Plain
Start at 2022-10-27 10:01:16.253119 +0000 UTC
 
Listing multipart uploads .
 
Upload list:
Key                                               Initiated                     StorageClass        UploadId
tos://bucketname/Visual Studio Code.app/Contents/Frameworks/Electron Framework.framework/Versions/A/Electron Framework
                                                  2022-10-27T10:00:11Z          STANDARD            6b229265e5bcef1437b2485a56ab****
 
tos://bucketname/installation package/Postman-osx-8.12.4-x64.zip
                                                  2022-10-27T10:01:08Z          STANDARD            6b22926509948cb9e10f485a56e4****
 
tos://bucketname/installation package/VSCode-darwin-universal (1).zip
                                                  2022-10-27T10:01:08Z          STANDARD            6b229265c48609aa37b2485a56e4****
 
tos://bucketname/installation package/draw.io-universal-16.5.1.dmg
                                                  2022-10-27T10:01:08Z          STANDARD            6b2292654a1ce26510f94a5a56e4****
 
tos://bucketname/installation package/go1.17.5.darwin-amd64 (1).pkg
                                                  2022-10-27T10:01:08Z          STANDARD            6b2292656a550d73e10f485a56e4****
 
tos://bucketname/Installation Package/node-v14.18.1.pkg
                                                  2022-10-27T10:01:09Z          STANDARD            6b229265ddf1d388e10f485a56e5****
 
tos://bucketname/Installation Package/Unconfirmed 442045.crdownload
                                                  2022-10-27T10:01:09Z          STANDARD            6b229265b3475a44e10f485a56e5****
 
tos://bucketname/Installation Package/Unconfirmed 610983.crdownload
                                                  2022-10-27T10:01:12Z          STANDARD            6b2292655bccfae610f94a5a56e8****
 
Folder number is: 0
Upload number is: 8
```
