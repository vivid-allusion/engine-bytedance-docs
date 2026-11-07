---
title: "TTL"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/ttl"
---

TTL (Time To Live) refers to the lifespan of data. In ByteHouse Enterprise Edition, TTL can be classified by deletion level and behavior.

<span id="0b1c7b10"></span>
## General concept

TTL by deletion level includes Partition\-level TTL and Row\-level TTL:


* **Partition\-level TTL**: The columns involved in the TTL must be part of the Partition field. Within the same partition, data can perform unified actions (deletion or movement to other disks) when TTL expires.

* **Row\-level TTL**: TTL fields can consist of any columns, and expired data is deleted from the disk during Merge or moved to other disks when all the data contained in parts expires.


TTL by behavior includes Delete TTL and Move TTL:


* **Delete TTL**: Data is deleted when the TTL expires.

* **Move TTL**: Data is moved to other disks or disk groups (Volume) when the TTL expires.


Additionally, there are certain usage restrictions when modifying TTL:


* For Partition\-level TTL, ByteHouse Enterprise Version 2.4 and above support real\-time calculations for both Delete TTL and Move TTL, meaning old data can also be automatically deleted or moved to other disks after modifying the TTL.

* For Row\-level TTL, since the TTL information is stored on the disk, after changing the TTL, it is necessary to execute `Materialize TTL` to update the TTL information of the old parts, which allows the new TTL to take effect.


<span id="c544c0d5"></span>
## Difference contrast

Both Partition\-level TTL and Row\-level TTL can delete or move data, but their behaviors in data deletion and movement differ. Additionally, after users modify the TTL using the Alter command, the behavior of the two types of TTL also differs as detailed in the table below.


| |Partition\-level TTL |Row\-level TTL |
|---|---|---|
|Delete TTL |* Partitions with the same part have the same expiration time, so data can be deleted by partition.<br><br>* When the partition\-level TTL expires, it will `generate DROP RANGE` part to mark all parts under this partition for deletion.<br><br>* Expired data is not accessible for queries. |* Each row of data has its own expiration time, and some data within each part may expire.<br><br>* Expired data is deleted from the disk during Merge.<br><br>* During queries, data in parts that are not promptly deleted is not filtered out; expired data can be queried. |
|Move TTL |* Batch move data under partitions with expired TTL to the target disk. |* During Merge, update the minimum (Min) and maximum (Max) expiration times involved in the TTL of rows, and `record it` to the ttl.txt file under the part directory.<br><br>* After all data in the part expires (current_time \>= max), move the part to the target disk. |
|Modify TTL |* TTL changes can take effect immediately for already existing parts.<br><br>* TTL changes can take effect immediately for newly written parts. |* For already existing parts, `Materialize TTL` must be executed to submit a Mutation to change the `ttl.txt` file of existing parts, enabling the new TTL to take effect for old parts.<br><br>* TTL changes can take effect immediately for newly written parts. |


<span id="208e4267"></span>
## Table engine support

The MergeTree Family table engine supports the above TTL as shown in the table below.


| |Partition\-level TTL<br><br>(Delete) |Partition\-level TTL<br><br>(Move) |Row\-level TTL<br><br>(Delete) |Row\-level TTL<br><br>(Move) |Remark |
|---|---|---|---|---|---|
|MergeTree |Activate by Row\-level TTL |ByteHouse Enterprise Edition Version 2.4.1.970 and above |✅ |✅ |The Partition\-level TTL (Delete) of the MergeTree table will be treated as Row\-level TTL |
|HaMergeTree |✅ |ByteHouse Enterprise Edition, Version 2.4.1.970 and above |✅ |✅ |Recommended to use the partition\-level TTL |
|HaUniqueMergeTree |✅ |ByteHouse Enterprise Edition, Version 2.4.1.970 and above |✅ |✅ |Recommended to use partition\-level TTL |


<span id="747fc758"></span>
## Usage example

<span id="d24caba0"></span>
### Basic syntax

TTL is often configured with cold and hot tiering movement factor strategies, details can be referred to [Cold-hot storage](https://docs.byteplus.com/docs/bytehouse/cold-hot-storage).

Examples are as follows:

```SQL
-- Add TTL when creating a table
CREATE TABLE example_table on cluster xxxx
(
    d Date,
    a Int
)
ENGINE = HaMergeTree(...)
PARTITION BY d
ORDER BY d
TTL d + INTERVAL 1 MONTH DELETE,
    d + INTERVAL 2 WEEK TO DISK 'S3'
SETTINGS index_granularity = 8192, storage_policy = 's3_cold';

-- Edit the TTL policy
ALTER TABLE table_name on cluster cluster_name 
MODIFY TTL toDate(create_date) + toIntervalDay(30) TO DISK 's3';
```


If configured this way, the multi\-level TTL and movement factor strategies will be activated simultaneously. Once data meets the moving conditions of TTL or the hot\-cold factor, a movement from hot data to cold data will be initiated.

<span id="28582c4a"></span>
### Partition\-level TTL and Row\-level TTL

Below are examples of using Partition\-level TTL and Row\-level TTL.

```SQL
Case 1:
PARTITION BY p_date

TTL p_date + interval 10 day -- Partition-level TTL
TTL toDate(x) + interval 10 day -- Row-level TTL: x is not a field of the partition by clause

Case 2:
PARTITION BY toDate(event_time), toHour(event_time)

TTL toDate(event_time) + interval 10 day -- Partition-level TTL, toDate(event_time) is a field in the partition by clause 
TTL event_time + interval 10 day -- Row-level TTL, event_time is not a field of the partition by clause

Case 3:
PARTITION BY event_time
 
TTL toDate(event_time) + INTERVAL 1 MONTH -- Partition-level TTL, event_time is a field of the partition by field
```


<span id="1331b5f6"></span>
### Delete TTL and Move TTL

Below are examples of using Delete TTL and Move TTL.

```SQL
TTL p_date + interval 10 day -- Delete TTL, data with p_date exceeding 10 days will be deleted.
TTL p_date + interval 10 day TO Disk 'disk_s3' -- Move TTL, data with p_date exceeding 10 days will be moved to disk_s3.
TTL event_time + interval 10 hour -- Delete TTL
TTL event_time + interval 10 hour TO Volume 'volume_s3' -- Move TTL
```


Note that a table can only have one Delete TTL, but it can have multiple Move TTLs; a table's TTL can consist of 0 to 1 Delete TTL and 0 to n Move TTLs.

```SQL
TTL p_date + interval 10 day -- Yes, 仅包含1个Delete TTL
TTL p_date + interval 10 day, event_time + interval 10 hour -- Error: only one Delete TTL is allowed
TTL p_date + interval 10 day TO disk 'disk_s3', event_time + interval 10 hour TO Volume 'volume_s3' -- Yes, including 0 Delete TTLs and 2 Move TTLs
TTL p_date + interval 20 day， p_date + interval 10 day TO disk 'disk_s3', event_time + interval 10 hour TO Volume 'volume_s3' -- Yes, including 1 Delete TTL and 2 Move TTLs
```
