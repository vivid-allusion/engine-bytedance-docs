---
title: "Set object metadata (setmeta)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Set-object-metadata-setmeta"
---

You can set object metadata using the `setmeta` command.

<span id=".5ZG95Luk5qC85byP"></span>
## Command format


<Tabs>
<Tab zoneid="iLgttpDN" title="Linux/macOS">
<TabTitle>Linux/macOS</TabTitle>

* Set metadata for a single object


```Bash
./tosutil setmeta tos://bucket/key [-versionId=xxx] [-meta=aaa:bbb#ccc:ddd] [-contentType=xxx] [-contentDisposition=xxx] [-contentEncoding=xxx] [-contentLanguage=xxx] [-cacheControl=xxx] [-expires=xxx] [-fr] [-o=xxx] [-bt=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```



* Set metadata for multiple objects


```Bash
./tosutil setmeta tos://bucket/[prefix] -r [-j=1] [-meta=aaa:bbb#ccc:ddd] [-contentType=xxx] [-contentDisposition=xxx] [-contentEncoding=xxx] [-contentLanguage=xxx] [-cacheControl=xxx] [-expires=xxx] [-o=xxx] [-bt=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
<Tab zoneid="8O0cLR80" title="Windows">
<TabTitle>Windows</TabTitle>

* Set single object metadata


```Bash
tosutil setmeta tos://bucket/key [-versionId=xxx] [-meta=aaa:bbb#ccc:ddd] [-contentType=xxx] [-contentDisposition=xxx] [-contentEncoding=xxx] [-contentLanguage=xxx] [-cacheControl=xxx] [-expires=xxx] [-fr] [-o=xxx] [-bt=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```



* Set metadata for multiple objects


```Bash
tosutil setmeta tos://bucket/[prefix] -r [-j=1] [-meta=aaa:bbb#ccc:ddd] [-contentType=xxx] [-contentDisposition=xxx] [-contentEncoding=xxx] [-contentLanguage=xxx] [-cacheControl=xxx] [-expires=xxx] [-o=xxx] [-bt=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
</Tabs>


<span id="4hiQRflv"></span>
## Parameters

For descriptions of general optional parameters, see [general parameters](https://docs.byteplus.com/docs/tos/Command-format#.6YCa55So5Y-v6YCJ5Y-C5pWw).


|**Parameter name** |**Type** |**Description** |
|---|---|---|
|bucket |String |Bucket name. |
|key |String |The object name. |
|prefix |String |The object name prefix for batch operations. |
|\-r |Bool |Perform batch operations to set object metadata. |
|\-j |Integer |Set the maximum concurrency for batch setting of object metadata, defaulting to `defaultJobs` in the configuration file. |
|\-versionId |String |Version number of the single object whose metadata is to be set. |
|\-meta |String |Set custom metadata for the object. |
|\-contentType |String |Set the object's Content\-Type. |
|\-contentDisposition |String |Set the object's Content\-Disposition. |
|\-contentEncoding |String |Set the object's Content\-Encoding. |
|\-contentLanguage |String |Set the Content\-Language of the object. |
|\-cacheControl |String |Set the object's Cache\-Control. |
|\-expires |String |Set the object's Expires in the format: YYYYMMDDHHmmSS. |
|\-fr |Bool |Generate a result manifest file when setting metadata for a single object. |
|\-o |String |The folder for the generated result list file, defaulting to `defaultOutputDir` in the configuration file. |
|\-bt |String |Type of storage bucket. Valid values:<br><br><br>* `fns`: flat bucket.<br><br>* `hns`: hierarchical bucket.<br><br><br>If the storage bucket type is not specified, the type is obtained from the bucket metadata by default. |


<span id=".5L2_55So56S65L6L"></span>
## Example usage

<span id="34c484aa"></span>
### Set metadata for a single object

The following command sets the custom metadata for the **object1.png** object in the **bucketname** bucket to **aaa:bbb#ccc:**  **ddd**.


* command

   ```Plain
   ./tosutil setmeta tos://bucketname/object1.png -meta aaa:bbb#ccc:ddd
   ```
   

* Back

   ```Plain
   Start at 2022-10-27 08:30:54.714864 +0000 UTC
    
   Set object metadata [object1.png] in the bucket [bucketname] successfully, cost [162], request id [d6c8485a41be2c6f635a41be-ac1424b7-1onyHu-SOM-cb-tos-bj]
   ```
   


<span id="fa37216f"></span>
### Batch set object metadata

The following command sets the custom metadata of all objects with the prefix **object** in the **bucketname** bucket to **aaa:bbb#ccc:**  **ddd**。


* Command

   ```Plain
   ./tosutil setmeta tos://bucketname/object -r -meta aaa:bbb#ccc:ddd
   ```
   

* Back

   ```Plain
   Start at 2022-10-27 08:31:45.565285 +0000 UTC
    
   [--------------------------------------------------] 100.00% tps:0.00 3/3 161ms
   Succeed count is:   3         Failed count is:    0
   Metrics [max cost:108 ms, min cost:36 ms, average cost:75.33 ms, average tps:18.63]
    
   Task id is: cac32e78-55d1-11ed-936d-aa665a3c7f26
   ```
