---
title: "Calculate object and part size and quantity (du)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Calculate-object-and-sharding-size-and-quantity-du"
---

You can use the `du` command to calculate the total size and quantity of all objects and multipart upload tasks (including unmerged parts) under an entire bucket or bucket prefix.

<span id="93e27621"></span>
## Considerations

If you need to calculate a large number of objects (in the millions), this command may take a long time to execute. If you must calculate object size and quantity, it is recommended to calculate by directory.

<span id="dd1f7067"></span>
## Command syntax


<Tabs>
<Tab zoneid="Vh9nFReXN2" title="Linux/macOS">
<TabTitle>Linux/macOS</TabTitle>

&nbsp;

```Bash
./tosutil du tos://bucket[/prefix] [-d] [-m] [-v] [-bf=xxx] [-bt=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
<Tab zoneid="zXtHL8P2tp" title="Windows">
<TabTitle>Windows</TabTitle>

&nbsp;

```Bash
tosutil du tos://bucket[/prefix] [-d] [-m] [-v] [-bf=xxx] [-bt=xxx] [-e=xxx] [-re=xxx] [-i=xxx] [-k=xxx] [-t=xxx] [-conf=xxx]
```





</Tab>
</Tabs>


<span id="1f45fda3"></span>
## Parameters

For descriptions of general optional parameters, see [general parameters](https://docs.byteplus.com/docs/tos/Command-format#.6YCa55So5Y-v6YCJ5Y-C5pWw).


|**Parameter name** |**Type** |**Description** |
|---|---|---|
|bucket |String |The bucket name specified for calculating. |
|prefix |String |Object name prefix specified for calculation. |
|\-v |Bool |Calculate the total size and quantity of the latest and historical versions for all objects simultaneously (if any). |
|\-m |Bool |Calculate the total size and total number of all shard upload tasks (unmerged shards) simultaneously. |
|\-d |Bool |Directory mode (delimiter is`/`), only counts objects and subdirectories in the current directory without recursively counting all objects and subdirectories. |
|\-bf |Enum |Display format of byte count in the calculation results of total size and total number. Supported values:<br><br><br>* `human-readable`<br><br>* `raw` |
|\-bt |String |Type of bucket. Valid values:<br><br><br>* `fns`: flat bucket.<br><br>* `hns`: hierarchical bucket.<br><br><br>If the bucket type is not specified, it defaults to the type obtained from the bucket metadata. |


<span id="57d0c731"></span>
## Example

<span id="d8cec549"></span>
### Calculate all objects

The following command calculates the number and size of all objects in the **bucketname** bucket.


* Command

   ```Bash
   ./tosutil du tos://bucketname
   ```
   

* Return

   The following return indicates that the **bucketname** bucket contains 53 objects totaling 2.37MB; 45 are STANDARD storage, 2 are IA (infrequent access), 1 is INTELLIGENT_TIERING, and 5 are COLD_ARCHIVE.

   ```Bash
   Start at 2023-11-22 08:39:45.972388 +0000 UTC
   
   Calculating objects .
   
   Storage class                   Object number                   Object size
   ---------------------------------------------------------------------------------------------
   STANDARD                        45                              1.90MB
   IA                              2                               80.78KB
   INTELLIGENT_TIERING             1                               67.90KB
   COLD_ARCHIVE                    5                               323.43KB
   ---------------------------------------------------------------------------------------------
   
   Total object number:            53                  Total object size:              2.37MB
   
   End at 2023-11-22 08:39:46.97474 +0000 UTC, 1002 ms elapsed
   ```
   


<span id="8f0049b5"></span>
#### Calculate separately for the latest and historical versions

The following command calculates the number and size of the latest and historical versions of all objects in the **bucketname** bucket.


* Command

   ```Bash
   ./tosutil du tos://bucketname -v
   ```
   

* Return

   The following return shows the **bucketname** bucket contains 58 objects totaling 2.37MB; 53 are latest versions and 5 are historical versions.

   ```Bash
   Start at 2023-11-22 08:40:21.750155 +0000 UTC
   
   Calculating versioning objects .
   
   Storage class                   Object number(all)              Object size(all)
   ---------------------------------------------------------------------------------------------
   STANDARD                        50                              1.99MB
   IA                              2                               80.78KB
   INTELLIGENT_TIERING             1                               67.90KB
   COLD_ARCHIVE                    5                               323.43KB
   ---------------------------------------------------------------------------------------------
   
   Storage class                   Object number(latest)           Object size(latest)
   ---------------------------------------------------------------------------------------------
   STANDARD                        45                              1.90MB
   IA                              2                               80.78KB
   INTELLIGENT_TIERING             1                               67.90KB
   COLD_ARCHIVE                    5                               323.43KB
   ---------------------------------------------------------------------------------------------
   
   Storage class                   Object number(historical)       Object size(historical)
   ---------------------------------------------------------------------------------------------
   STANDARD                        5                               90.59KB
   IA                              0                               0B
   INTELLIGENT_TIERING             0                               0B
   COLD_ARCHIVE                    0                               0B
   ---------------------------------------------------------------------------------------------
   
   Total latest object number:     53                  Total latest object size:       2.37MB
   Total historical object number: 5                   Total historical object size:   90.59KB
   Total object number:            58                  Total object size:              2.45MB
   Total delete marker number:     6
   
   End at 2023-11-22 08:40:22.756633 +0000 UTC, 1006 ms elapsed
   ```
