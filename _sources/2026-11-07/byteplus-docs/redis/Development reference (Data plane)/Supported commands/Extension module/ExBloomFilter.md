---
title: "ExBloomFilter"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/exbloom"
---

The ExBloomFilter of Cache for Redis is based on the Scalable Bloom Filter implementation, which has the ability to dynamically expand and maintain the stability of the error rate during the expansion process. This topic introduces the relevant information of the ExBloomFilter extension module of Cache for Redis, including functional principles, applicable scenarios, and specific command syntax.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The instance version must meet the following requirements simultaneously to use the ExBloomFilter module:

   * The database version must be Redis 7.0.

   * The minor version of proxy must be greater than or equal to 1.22.0.

   * The minor version of server must be greater than or equal to 7.17.3.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can view the instance's database version and minor version information under the <strong>Summary</strong> tab. For specific procedures, refer to <a href="https://docs.byteplus.com/en/docs/redis/view-instance">Viewing instance information</a>.   </div>
   

* The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

Bloom is a space\-efficient probabilistic data structure that belongs to [sketches](https://datasketches.apache.org/docs/Background/TheChallenge.html). When processing large\-scale data, it can determine whether an element exists with only a small amount of memory. Compared with traditional Redis data structures that provide similar functions for determining the existence of elements (such as Hash, Set, and String`s Bitset, etc.), ExBloomFilter has significant advantages in memory usage, dynamically expandable, customizable error rates, and maintaining error rate stability when expanding. It is very suitable for business scenarios that need to efficiently determine the existence of large amounts of data and allow a certain error rate. You can directly use the Bloom Filter interface provided by ExBloomFilter to eliminate the need for secondary encapsulation and local implementation of Bloom filter functions.

<span id=".5Yqf6IO95Y6f55CG"></span>
### Function principle

The ExBloomFilter provided by Cache for Redis is based on the Scalable Bloom Filter, which has the ability to dynamically expand and maintain the stability of the error rate during the expansion process.

ExBloomFilter, an implementation of the Scalable Bloom Filter, has the ability to expand dynamically while maintaining the same error rate. The Scalable Bloom Filter is optimized on the basis of Bloom Filter. The following will briefly introduce the basic principles of Bloom Filter and Scalable Bloom Filter.


* **Bloom Filter**

   The Bloom Filter essentially consists of an array of bits and k different hash functions. All bits in the array are initially 0, and the hash function is used to map the enter elements to different locations in the array of bits.

   When an element is added to the Bloom Filter, the system first uses the k hash functions to calculate the k hashes of the element, and then sets the position corresponding to the k hashes in the Bit array to 1. It is important to note that a bit may be shared by different data. That is, different elements may be mapped to the same location after being computed by the hash function, causing these locations to be incorrectly set to 1.

   For example, if a Bloom Filter uses 3 hash functions `(h_1)`, `(h_2)`, and `(h_3)`, when adding element `(x1)` to the Bloom Filter, the values computed by the above 3 hash functions are `(i_1)`, `(i_3)`, and `(i_6)` respectively. When adding element `(x2)`, the values are `(i_6)`, `(i_8)`, and `(i_10)` respectively. Then, the bits with indices `(i_1)`, `(i_3)`, `(i_6)`, `(i_8)`, and `(i_10)` in the bit array are set to 1. The diagram of the positions of `(x1)` and `(x2)` in the bit array is shown below.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_958f242037516be210dac9f4ebdef540.png) </span>

   When querying whether an element is in the Bloom Filter, the system will also use the k hash functions to calculate the k hashes of the element, and then check whether the positions corresponding to the k hashes in the Bit array are all 1. If any of the k positions is 0, then the element is definitely not in the Bloom Filter. If all the k positions are 1, then the element is considered to be in the Bloom Filter.

   For example, when querying whether elements `(y_1)` and `(y_2)` are in the Bloom Filter, first compute via the above 3 hash functions `(h_1)`, `(h_2)`, and `(h_3)`. When querying element `(y_1)`, the values obtained are `(i_2)`, `(i_5)`, and `(i_10)`; when querying element `(y_2)`, the values are `(i_1)`, `(i_6)`, and `(i_8)`. The diagram of the positions of `(y1)` and `(y2)` in the bit array is shown below.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a9ea64000a9fb8f35c4e3095db1cb76e.png) </span>

   As can be seen from the figure above, although `(y2)` is not added to the Bloom Filter, all its positions in the Bit array are 1, so the Bloom Filter determines that the element `(y2)` exists. This is because different elements may be mapped to the same location after being computed by the hash function, causing those locations to be incorrectly set to 1.

   Therefore, Bloom Filter has the possibility of misjudging, which is called the false positive rate. That is, it is possible to determine that elements that are not in the set are in the set, but not to determine that elements in the set are not in the set.

* **Scalable Bloom Filter**

   As elements continue to be added, the error rate of the filter will become higher and higher, and Scalable Bloom Filter is optimized on the basis of Bloom Filter, which can automatically expand to accommodate the insertion of more elements according to the growth of data volume, while maintaining a relatively stable error rate.

   The Scalable Bloom Filter uses a layered design. When it needs to be expanded, it not only expands the size of a single Bloom Filter, but also adds new layers. Each layer is a separate Bloom Filter.

   The new element is added to the last layer of the Bloom Filter, and the query starts from the last layer until the first layer is queried. For more details, refer to [Scalable Bloom Filter](https://citeseerx.ist.psu.edu/document?repid=rep1&type=pdf&doi=f8b18892d6a105ad802c027decd6a32b8b339dba).


<span id=".6YCC55So5Zy65pmv"></span>
### Applicable scenarios

The ExBloomFilter provided by Cache for Redis is suitable for the following typical scenarios:


* Product advertising recommendation: Record the purchased goods by the user through the Bloom Filter, and check whether the goods are already in the user`s Bloom Filter before recommending new goods to the user, so as to recommend interesting and unpurchased goods to the user.

* Mass data filtering deduplicate: When dealing with massive data (such as crawling web URL, user access logs, etc.), the URL of the web page or the user`s access IP can be added to the Bloom Filter after hashing, and before processing new data, check whether the data is already in the Bloom Filter to avoid duplicate processing and reduce unnecessary network requests and resource waste.


<span id=".5L2_55So5bu66K6u"></span>
## Suggestions for use


* Plan for initial capacity (that is, number of elements to be added) and expected error rate in advance. If the expected capacity far exceeds 100, it is recommended to use the `BF.RESERVE` command to create the ExBloomFilter instead of creating it directly via `BF.ADD`. The reasons are as follows:

   * When adding an element via the `BF. ADD` (or `BF. MADD`) command. If the ExBloomFilter specified by the target key does not exist, Redis will automatically create an ExBloomFilter with an initial capacity of 100 and an upper error rate of 0.01. If your required capacity is much higher than 100, you can only add elements later by expanding. The way ExBloomFilter expands is to increase the number of layers of Bloom Filter, and the capacity of each layer increases accordingly. Continuous expansion will cause the number of layers of ExBloomFilter to increase, which in turn causes query tasks to traverse multiple layers of Bloom Filter, seriously reducing performance.

   * The `BF.RESERVE` command allows you to customize the initial capacity and expected error rate (error_rate) when creating a Bloom Filter. The lower the error rate, the higher the accuracy, the greater the memory usage of ExBloomFilter, and the higher the CPU usage. When the number of elements exceeds the initial capacity value, the error rate will increase.

* Although ExBloomFilter provides the ability to expand, it is recommended to use this only as a safeguard when actually using it, and try to avoid expanding actions. When the actual capacity exceeds the initial capacity, ExBloomFilter can expand to ensure normal business writes and avoid online incidents.

* ExBloomFilter only supports inserting new elements, but cannot delete existing elements, which will cause ExBloomFilter's memory usage to continue to rise. In order to prevent ExBloomFilter from growing and causing OOM (Out Of Memory), it is recommended to pay attention to the following aspects when using:

   * Business data splitting

      When a large amount of data is stored in a single ExBloomFilter, not only will the key be too large to affect the query performance, but most of the query request traffic will be concentrated in the sharding where the key is located, forming a hotspot key or even access skew. Therefore, if the amount of business data is large, it is recommended that you split the business data into multiple ExBloomFilter instances. If you are using instance with sharding cluster enabled, you can distribute the ExBloomFilter to each sharding, balance the memory capacity and traffic, and leverage the advantages of instance with sharding cluster enabled.

   * Regularly rebuild or rotate to switch ExBloomFilter

      If the business allows, you can regularly use the `DEL` command to delete the ExBloomFilter, and then pull the data reconstruction from the back\-end database to control the ExBloomFilter size.

      You can also select to create multiple redundant ExBloomFilters in the early stage of use, and control the size of a single ExBloomFilter by rotating and switching during use, which can avoid the impact of frequent deletion and reconstruction of ExBloomFilters on online business, but creating multiple ExBloomFilters will cause some waste of memory space.


<span id=".5ZG95Luk6K-t5rOV"></span>
## Command syntax

<span id=".5ZG95Luk5YiX6KGo"></span>
### Command list

The commands supported by ExBloomFilter are shown in the following table.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For the command syntax in the following table, the definitions are as follows:</div>



* <div data-tips="true" data-tips-type="tip"><code>UPPERCASE KEYWORD</code>: Command keyword, such as <code>BF.RESERVE</code>.</div>


* <div data-tips="true" data-tips-type="tip"><code>lowercase keyword</code>: Customizable parameter.</div>


* <div data-tips="true" data-tips-type="tip"><code>[]</code>: The content within <code>[]</code> is an optional parameter, and the content outside <code>[]</code> is a required parameter.</div>


* <div data-tips="true" data-tips-type="tip"><code>...</code>：<code>...</code>  are repeatable.</div>




|command |Syntax |Description |
|---|---|---|
|[BF.RESERVE](https://docs.byteplus.com/en/docs/redis/exbloom#bf-reserve) |`BF.RESERVE key error_rate capacity` |Create an empty ExBloomFilter with an initial capacity of `capacity` and an error rate of `error_rate`. |
|[BF.ADD](https://docs.byteplus.com/en/docs/redis/exbloom#bf-add) |`BF.ADD key item` |Add an element to the ExBloomFilter specified by key. |
|[BF.MADD](https://docs.byteplus.com/en/docs/redis/exbloom#bf-madd) |`BF.MADD key item [item ...]` |Add multiple elements to the ExBloomFilter specified by key in batches. |
|[BF.EXISTS](https://docs.byteplus.com/en/docs/redis/exbloom#bf-exists) |`BF.EXISTS key item` |Check whether an element exists in the ExBloomFilter specified by key. |
|[BF.MEXISTS](https://docs.byteplus.com/en/docs/redis/exbloom#bf-mexists) |`BF.MEXISTS key item [item ...]` |Check whether multiple elements exist in the ExBloomFilter specified by key in batches. |
|[BF.INSERT](https://docs.byteplus.com/en/docs/redis/exbloom#bf-insert) |`BF.INSERT key [CAPACITY capacity] [ERROR error_rate] [NOCREATE] ITEMS item [item ...]` |Insert one or more elements to the ExBloomFilter specified by the key, and automatically create if the specified ExBloomFilter does not exist (you can set the initial capacity and expected error rate for the new ExBloomFilter when adding elements), or you can set it to not automatically create when the ExBloomFilter does not exist. |
|[BF.INFO](https://docs.byteplus.com/en/docs/redis/exbloom#bf-info) |`BF.INFO key` |Query the details of the ExBloomFilter specified by key, such as the total number of elements, the total number of filter layers, and the number of elements in each layer, error rate, etc. |


<span id=".5rOo5oSP5LqL6aG5"></span>
### Precautions


* To use the ExBloomFilter feature, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support to apply for usage.

* After the application is completed, accounts with the Administrator role will have all permissions for ExBloomFilter related commands by default. You can also create a new role that allows the use of all ExBloomFilter commands according to business needs (that is, the ACL rule of this role needs to be set to `+@exbloom`). After creating the role, you need to log in to Redis with an account that has this role to use ExBloomFilter related commands. For specific procedures about creating a role, refer to [Creating role](https://docs.byteplus.com/en/docs/redis/create-role).

* The Cache for Redis supports big and hot key analysis for the ExBloomFilter data type. It can help timely discover and analyze the details of hot keys and big keys in the database, providing data references for you to optimize hot keys and big keys. For specific procedures, refer to [Big key analysis](https://docs.byteplus.com/en/docs/redis/big-key-analysis) and [Hot key analysis](https://docs.byteplus.com/en/docs/redis/hot-key-analysis).

* After successfully applying for the use of the ExBloomFilter function, the instance will no longer support any data recovery functions, including:

   * [Recovery from backup set](https://docs.byteplus.com/en/docs/redis/recovery-from-backup-set)

   * [Recovery by point in time](https://docs.byteplus.com/en/docs/redis/recovery-by-time-point)

   * [Recovery from deleted instance](https://docs.byteplus.com/en/docs/redis/restore-deleted-instance)

* A bit in an ExBloomFilter may be shared by different data (that is, different elements may be mapped to the same location after being computed by a hash function). So ExBloomFilter does not provide a command to delete elements that already exist in ExBloomFilter (otherwise it will affect the data of other elements), but you can use the following native Redis command to achieve the purpose of deleting ExBloomFilter.

   
   |command |Syntax |Description |
   |---|---|---|
   |[EXPIRE](https://redis.io/docs/latest/commands/expire/) |`EXPIRE key seconds [NX \| XX \| GT \| LT]` |Set the timeout for ExBloomFilter. ExBloomFilter that exceeds this time will be automatically deleted. |
   |[UNLINK](https://redis.io/docs/latest/commands/unlink/) |`UNLINK key [key ...]` |Asynchronously delete one or more ExBloomFilter. When deleting an ExBloomFilter with the `UNLINK` command, this ExBloomFilter is marked as pending deletion, and the actual delete actions are carried out in the background thread without blocking the current Redis process. |
   |[DEL](https://redis.io/commands/del) |`DEL key [key ...]` |Synchronously delete one or more ExBloomFilters. When deleting ExBloomFilter with the `DEL` command, the delete action immediately blocks the current Redis thread until the memory space corresponding to ExBloomFilter is completely withdrawn. If the amount of ExBloomFilter data to be deleted is too large, it may affect the overall performance of Redis. |
   


<span id="bf-reserve"></span>
### BF.RESERVE


|Category |Description |
|---|---|
|Command syntax |`BF.RESERVE key error_rate capacity` |
|Time complexity |O(1). |
|Command description |Create an empty ExBloomFilter with an initial capacity of `capacity` and an error rate of `error_rate`. |
|Option |* `key`: The name of the key, used to specify the ExBloomFilter as the object of the command call.<br><br>* `error_rate`: The expected error rate, with values ranging from 0 to 1. The smaller the value, the higher the accuracy, the greater the memory usage of ExBloomFilter, and the higher the CPU usage.<br><br>* `capacity`: The initial capacity of the ExBloomFilter, that is, the number of elements expected to be added to the ExBloomFilter.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the actual number of elements added exceeds the <code>capacity</code> value, ExBloomFilter will automatically increase the number of Bloom Filter layers to achieve expansion. Continuous expansion will increase the number of layers of ExBloomFilter, which will cause the query task to traverse multiple layers of Bloom Filter, seriously reducing performance. Therefore, if you are very sensitive to performance, it is strongly recommended to plan the initial capacity and expected error rate in advance, and try to avoid expanding actions.</div><br> |
|Response |* `OK`: Execution succeeded.<br><br>* The corresponding exception information in other cases (such as `invalid arguments`, `exbloom is already exists` and so on). |
|Example |Command example.<br><br>```Bash```<br>```BF.RESERVE testbf 0.01 100```<br><br><br>Response example.<br><br>```Bash```<br>```OK```<br> |


<span id="bf-add"></span>
### BF.ADD


|Category |Description |
|---|---|
|Command syntax |`BF.ADD key item` |
|Time complexity |O (log N), where N represents the number of filter layers for ExBloomFilter. |
|Command description |Add an element to the ExBloomFilter specified by key.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the specified ExBloomFilter does not exist, Redis will automatically create an ExBloomFilter with an initial <code>capacity</code> of 100 and an expected <code>error_rate</code> of 0.01.</div><br> |
|Option |* `key`: The name of the key, used to specify the ExBloomFilter as the object of the command call.<br><br>* `item`: Elements to be added to ExBloomFilter. |
|Response |* `1`: Indicates that the element definitely did not exist before, and adds the element to the ExBloomFilter.<br><br>* `0`: Indicates that the element may already exist, so no add or update operation will be performed.<br><br>* The corresponding exception information in other cases (such as `invalid arguments`, `WRONGTYPE` and so on). |
|Example |Command example.<br><br>```Bash```<br>```BF.ADD testbf test_i1```<br><br><br>Response example.<br><br>```Bash```<br>```1```<br> |


<span id="bf-madd"></span>
### BF.MADD


|Category |Description |
|---|---|
|Command syntax |`BF.MADD key item [item ...]` |
|Time complexity |O (log N), where N represents the number of filter layers for ExBloomFilter. |
|Command description |Add multiple elements to the ExBloomFilter specified by key in batches.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the specified ExBloomFilter does not exist, Redis will automatically create an ExBloomFilter with an initial <code>capacity</code> of 100 and an expected <code>error_rate</code> of 0.01.</div><br> |
|Option |* `key`: The name of the key, used to specify the ExBloomFilter as the object of the command call.<br><br>* `item`: Elements to be added to ExBloomFilter. Multiple elements can be added simultaneously. |
|Response |* `1`: Indicates that the element definitely did not exist before, and adds the element to the ExBloomFilter.<br><br>* `0`: Indicates that the element may already exist, so no add or update operation will be performed.<br><br>* The corresponding exception information in other cases (such as `invalid arguments`, `WRONGTYPE` and so on). |
|Example |Command example.<br><br>```Bash```<br>```BF.MADD testbf test_i1 test_i2 test_i3```<br><br><br>Response example.<br><br>```Bash```<br>```1) 0```<br>```2) 1```<br>```3) 1```<br> |


<span id="bf-exists"></span>
### BF.EXISTS


|Category |Description |
|---|---|
|Command syntax |`BF.EXISTS key item` |
|Time complexity |O (log N), where N represents the number of filter layers for ExBloomFilter. |
|Command description |Check whether an element exists in the ExBloomFilter specified by key. |
|Option |* `key`: The name of the key, used to specify the ExBloomFilter as the object of the command call.<br><br>* `item`: Elements to be queried. |
|Response |* `0`: Indicates that the element definitely does not exist.<br><br>* `1`: Indicates that the element may exist.<br><br>* The corresponding exception information in other cases (such as `invalid arguments`, `WRONGTYPE` and so on). |
|Example |Command example.<br><br>```Bash```<br>```BF.EXISTS testbf test_i1```<br><br><br>Response example.<br><br>```Bash```<br>```1```<br> |


<span id="bf-mexists"></span>
### BF.MEXISTS


|Category |Description |
|---|---|
|Command syntax |`BF.MEXISTS key item [item ...]` |
|Time complexity |O (log N), where N represents the number of filter layers for ExBloomFilter. |
|Command description |Check whether multiple elements exist in the ExBloomFilter specified by key in batches. |
|Option |* `key`: The name of the key, used to specify the ExBloomFilter as the object of the command call.<br><br>* `item`: Elements to be queried. Multiple elements can be queried at the same time. |
|Response |* `0`: Indicates that the element definitely does not exist.<br><br>* `1`: Indicates that the element may exist.<br><br>* The corresponding exception information in other cases (such as `invalid arguments`, `WRONGTYPE` and so on). |
|Example |Command example.<br><br>```Bash```<br>```BF.MEXISTS testbf test_i2 test_i3 test_i4```<br><br><br>Response example.<br><br>```Bash```<br>```1) 1```<br>```2) 1```<br>```3) 0```<br> |


<span id="bf-insert"></span>
### BF.INSERT


|Category |Description |
|---|---|
|Command syntax |`BF.INSERT key [CAPACITY capacity] [ERROR error_rate] [NOCREATE] ITEMS item [item ...]` |
|Time complexity |O (log N), where N represents the number of filter layers for ExBloomFilter. |
|Command description |Insert one or more elements to the ExBloomFilter specified by the key, and automatically create if the specified ExBloomFilter does not exist (you can set the initial capacity and expected error rate for the new ExBloomFilter when adding elements), or you can set it to not automatically create when the ExBloomFilter does not exist. |
|Option |* `key`: The name of the key, used to specify the ExBloomFilter as the object of the command call.<br><br>* `capacity`: The initial capacity of the ExBloomFilter, that is, the number of elements expected to be added to the ExBloomFilter.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This value is ignored when ExBloomFilter already exists.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you need to create an ExBloomFilter without setting the value, Redis will use the default value of 100 as the <code>capacity</code> value for the new ExBloomFilter.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When the actual number of elements added exceeds the <code>capacity</code> value, ExBloomFilter will automatically increase the number of Bloom Filter layers to achieve expansion. Continuous expansion will increase the number of layers of ExBloomFilter, which will cause the query task to traverse multiple layers of Bloom Filter, seriously reducing performance. Therefore, if you are very sensitive to performance, it is strongly recommended to plan the initial capacity and expected error rate in advance, and try to avoid expanding actions.   </div><br>   <br><br>* `error_rate`: The expected error rate, with values ranging from 0 to 1. The smaller the value, the higher the accuracy, the greater the memory usage of ExBloomFilter, and the higher the CPU usage.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This value is ignored when ExBloomFilter already exists.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When ExBloomFilter needs to be created but this value is not set, Redis will use the default value 0.01 as the <code>error_rate</code> value of the newly created ExBloomFilter.   </div><br>   <br><br>* `NOCREATE`: After setting this option, it will not be automatically created when ExBloomFilter does not exist.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The <code>NOCREATE</code>parameter cannot be set at the same time as <code>capacity</code> or <code>error_rate</code>. Otherwise, <code>nil</code> will be returned.   </div><br>   <br><br>* `item`: Elements to be added to ExBloomFilter. Multiple elements can be added simultaneously. |
|Response |* `1`: Indicates that the element definitely did not exist before, and adds the element to the ExBloomFilter.<br><br>* `0`: Indicates that the element may already exist, so no add or update operation will be performed.<br><br>* The corresponding exception information in other cases (such as `invalid arguments`, `WRONGTYPE` and so on). |
|Example |* Command example 1<br><br>   Add 3 elements `test_i1`, `test_i2`, and `test_i3` to `testbf1` (this ExBloomFilter does not exist previously), and simultaneously specify the `capacity` of the newly created ExBloomFilter as 10000 and the `error_rate` as 0.01.<br><br>   ```Bash```<br>```   BF.INSERT testbf1 CAPACITY 10000 ERROR 0.001 ITEMS test_i1 test_i2 test_i3```<br>```   ```<br>   <br><br>   Response example.<br><br>   ```Bash```<br>```   1) 1```<br>```   2) 1```<br>```   3) 1```<br>```   ```<br>   <br><br>* Command example 2<br><br>   Add 3 elements `test_i1`, `test_i2`, and `test_i3` to `testbf2` (this ExBloomFilter does not exist previously), and simultaneously set the `NOCREATE` parameter (that is, do not automatically create when the specified ExBloomFilter does not exist).<br><br>   ```Bash```<br>```   BF.INSERT testbf2 NOCREATE ITEMS test_i1 test_i2 test_i3```<br>```   ```<br>   <br><br>   Response example.<br><br>   ```Bash```<br>```   nil```<br>```   ```<br>    |


<span id="bf-info"></span>
### BF.INFO


|Category |Description |
|---|---|
|Command syntax |`BF.INFO key` |
|Time complexity |O (log N), where N represents the number of filter layers for ExBloomFilter. |
|Command description |Query the details of the ExBloomFilter specified by key, such as the total number of elements, the total number of filter layers, and the number of elements in each layer, error rate, etc. |
|Option |`key`: The name of the key, used to specify the ExBloomFilter as the object of the command call. |
|Response |* If executed successfully, it will return detailed information of ExBloomFilter.<br><br>* The corresponding exception information in other cases (such as `invalid arguments`, `WRONGTYPE` and so on). |
|Example |Command example.<br><br>```Bash```<br>```BF.INFO testbf```<br><br><br>Response example.<br><br>```Bash```<br>```1) total_items:25,num_blooms:2```<br>```2) bytes:16 bits:128 hashes:7 hashwidth:64 capacity:13 items:13 error_ratio:0.01```<br>```3) bytes:64 bits:512 hashes:8 hashwidth:64 capacity:46 items:12 error_ratio:0.005```<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The parameter description of the return result is as follows:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The first line returns the current summary of ExBloomFilter, where:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip"><code>total_items</code>: Total number of elements.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip"><code>num_blooms</code>: Total number of Bloom Filter layers.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The second line and subsequent lines return information for each layer of the Bloom Filter, where:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip"><code>bytes</code>: The number of bytes occupied.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip"><code>bits</code>: The number of bits occupied, where bits = bytes x 8.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip"><code>hashes</code>: The number of hash functions.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip"><code>hashwidth</code>: The width of the hash function.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip"><code>capacity</code>: Capacity.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip"><code>items</code>: The number of elements.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip"><code>error_ratio</code>: Error rate.</div><br> |
