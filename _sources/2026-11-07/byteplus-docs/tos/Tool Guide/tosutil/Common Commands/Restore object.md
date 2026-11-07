---
title: "Restore object"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Restore_object"
---

You can restore archive\-type objects using the restore command.

<span id="17e80e24"></span>
## Considerations


* Restoring files in archive storage incurs data retrieval fees. Restoring files in cold archive or deep cold archive incurs data retrieval and request fees. For details, see [data retrieval fees](https://docs.byteplus.com/docs/tos/docs-data-retrieval-fee) and [request fees](https://docs.byteplus.com/docs/tos/docs-request-fee).

* After the restoration of archive storage, cold archive, or deep cold archive files, a temporary copy will be generated for your access. The copy uses standard storage type and will be billed accordingly during its validity. For details, see [temporary storage capacity fees](https://docs.byteplus.com/docs/tos/docs-temporary-storage-fee).


<span id="7d57d904"></span>
## Command syntax


<Tabs>
<Tab zoneid="e761xarv" title="Linux/macOS">
<TabTitle>Linux/macOS</TabTitle>

* Restore specified object


```Bash
./tosutil restore tos://bucket/key [-f] [-versionId=xxx] [-d=1] [-tier=xxx] [-fr] [-o=xxx] [-bt=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```



* Batch restore objects with the specified prefix


```Bash
./tosutil restore tos://bucket/[prefix] -r [-f] [-j=1] [-v] [-d=1] [-tier=xxx] [-o=xxx] [-bt=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
<Tab zoneid="8LotliNp" title="Windows">
<TabTitle>Windows</TabTitle>

* Restore the specified object


```Bash
tosutil restore tos://bucket/key [-f] [-versionId=xxx] [-d=1] [-tier=xxx] [-fr] [-o=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```



* Batch restore objects with the specified prefix


```Bash
tosutil restore tos://bucket/[prefix] -r [-f] [-j=1] [-v] [-d=1] [-tier=xxx] [-o=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
</Tabs>


<span id="SQKFmMBw"></span>
## Parameters description

For instructions on general optional parameters, see [general parameters](https://docs.byteplus.com/docs/tos/Command-format#.6YCa55So5Y-v6YCJ5Y-C5pWw).


|**Parameter name** |**Type** |**Description** |
|---|---|---|
|bucket |String |The bucket name. |
|key |String |The object name. |
|prefix |String |Object name prefix for batch object recovery operations. |
|\-r |Bools |Execute batch recovery for objects with the specified prefix. |
|\-j |Integer |Maximum concurrency for batch object recovery, default is defaultJobs in the configuration file. |
|\-v |Bools |Batch restore multiple version objects by the specified object name prefix. |
|\-f |Bools |Force operation without confirmation prompt. |
|\-versionId |String |Object version. If not set, the latest version is restored by default. |
|\-d |Integer |Object copy expiration period, default is 1 day. After the object restoration is complete, a copy file will be generated for temporary reading and will be automatically deleted upon expiration. The unit is days. |
|\-tier |Enum |Restore priority supports values `Standard`, `Expedited`, `Bulk`, default is `Standard`. The available restore priorities vary by object type, explained as follows:<br><br><br>* The restore priority for archive storage objects can only be `Standard`, meaning restoration completes within 1 minute.<br><br>* Restore priority options for cold archive objects are as follows:<br><br>   * `Expedited`: fast retrieval, restoration completes within 1 to 5 minutes.<br><br>   * `Standard`: standard retrieval, recovery completed within 2 to 5 hours.<br><br>   * `Bulk`: bulk retrieval, recovery completed within 5 to 12 hours.<br><br>* The recovery priority values for deep cold archive objects are as follows:<br><br>   * `Standard`: standard retrieval, recovery completed within 12 hours.<br><br>   * `Bulk`: bulk retrieval, recovery completed within 48 hours. |
|\-fr |Bools |Generate a restore result file when restoring a single object. |
|\-o |String |The folder for generating the result list file, defaulting to `defaultOutputDir` in the configuration file. |
|\-bt |String |Bucket type. Valid values:<br><br><br>* `fns`: flat bucket.<br><br>* `hns`: hierarchical bucket.<br><br><br>If the bucket type is not specified, the type will be obtained from the bucket metadata by default. |


<span id="727636b9"></span>
## Usage example

<span id="b05d9504"></span>
### **Restore specified object**

The following command restores the image object in the bucket named bucketname, sets the replica retention period to 2 days, and the restore priority to Standard.


* Command

   ```Bash
   ./tosutil restore tos://bucketname/image -d=2 -tier=Standard
   ```
   

* Return

   ```Bash
   Start at 2024-12-11 07:01:03.718647 +0000 UTC
   
   Restore object [image] in the bucket [bucketname] successfully, cost [326], request id [b108015938af3609675938af-baa4376-1tLGiV-RO-cs-tos-front-azc-4]
   ```
   


<span id="d4fe256f"></span>
### **Batch restore objects with specified prefix**

The following command batch restores objects with the prefix Ar, sets the replica retention period to 2 days, and the restore priority to Standard.


* Command

   ```Bash
   ./tosutil restore tos://bucketname/Ar -r -d=2 -tier=Standard
   ```
   

* Return

   ```Bash
   Start at 2024-12-11 07:05:02.002142 +0000 UTC
   
   [--------------------------------------------------] 100.00% tps:0.00 3/3 139ms
   Succeed count is:   3         Failed count is:    0
   Metrics [max cost:89 ms, min cost:35 ms, average cost:62.33 ms, average tps:20.83]
   
   Task id is: 3dea6c5c-b78e-11ef-b734-8a8ce1fde7d0
   ```
