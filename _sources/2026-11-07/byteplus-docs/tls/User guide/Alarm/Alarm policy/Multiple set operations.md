---
title: "Multiple set operations"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Multi-set-operations"
---

The log service alert monitoring task treats a query and analysis result as a set, supporting up to three sets linked for monitoring.

<span id="5bcbe184"></span>
## Precautions


* The monitoring task selects up to the top 1,000 rows from the set operation results for alert triggering.

* When linking three sets for monitoring, the task selects up to the top 100 rows from each query and analysis result for set operations, first operating on the first two sets, then combining that result with the third set.


<span id="fa3327da"></span>
## Working principle

The log service alert monitoring task treats a query and analysis result as a set and supports connecting multiple sets via Cartesian product, left join, and right join to form a result set for alert triggering.


|set operation |Infographic |Description |
|---|---|---|
|Cartesian product |<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f05165666b09bcdbc16b629802003548.png) </span> |Pair each row of data to create a result set with the number of rows multiplied. |
|no merge |<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_0b33b1a1eaa85b178019fa3162029201.png) </span> |Only the first data is used as the query and analysis subject.<br><br>The second data can only be referenced in the content template variables. |
|concatenate |<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_fabdbae2b8db5d0febfa3c65b2d1bc86.png) </span> |Merge the data from each column into one table. The merged table’s column names become **original source name.original column name**. |
|Left join |<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_bee1d392473c2dde0efb0129771ae628.png) </span> |Match data through **specified columns** (such as id). If the **left** table does not have matching rows in the **right** table, the **right** table part in the result set will show **null.**  |
|Right join |<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_bda374a78cafd7c3872b327766ae2bdb.png) </span> |Match data by **specified columns** (such as id). If the **right** table has no matching rows in the **left** table, the **left** table part of that row will appear in the result set **null.**  |
|intranet |<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_9d7751b4f8dcd15a1e61646d70d8ffa9.png) </span> |Match data by **specified columns** (such as id) and keep only the intersecting rows. |
|federation |<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_8850bf43f170236775bf2a0c110a244e.png) </span> |Match data by **specified columns** (such as id) and keep all rows. |
|left criticize |<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_9cebc52e940a4e9ad723ce19da51134d.png) </span> |Delete data from the **left** data source in the **right** data source, meaning the **right** data source is a blacklist of the **left** data source. |
|right strike |<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_9d930589f031a7843da2d0821823e188.png) </span> |Delete data from the **left** data source in the **right** data source, making the **left** data source a blacklist of the **right** data source. |


<span id="ceedd451"></span>
## Set operation example

<span id="7cc35b13"></span>
### Execution statement configuration

The following execution statements are examples only.


* 1 execution statement

   ```SQL
   * | SELECT uid,region
   ```
   

* 2 execution statement

   ```SQL
   * | SELECT uid,region,COUNT(*) AS total GROUP BY uid,region
   ```
   

* Set operations: see each set operation example for details.


<span id="9b45e530"></span>
### Execution statement results

The following results are examples only.


* Result of `1 execution statement`

   
   |uid |region |
   |---|---|
   |10001 |beijing |
   |10002 |shanghai |
   |10003 |guangzhou |
   

* Result of `2 execution statement`

   
   |uid |region |total |
   |---|---|---|
   |10001 |beijing |18 |
   |10002 |shanghai |20 |
   |10004 |shenzhen |19 |
   


<span id="f719111e"></span>
### Set operation results of execution statements

<span id="5f2bc46d"></span>
#### Cartesian product results


|$1.uid |$1.region |$2.uid |$2.region |$2.total |
|---|---|---|---|---|
|10001 |beijing |10001 |beijing |18 |
|10001 |beijing |10002 |shanghai |20 |
|10001 |beijing |10004 |shenzhen |19 |
|10002 |shanghai |10001 |beijing |18 |
|10002 |shanghai |10002 |shanghai |20 |
|10002 |shanghai |10004 |shenzhen |19 |
|10003 |guangzhou |10001 |beijing |18 |
|10003 |guangzhou |10002 |shanghai |20 |
|10003 |guangzhou |10004 |shenzhen |19 |


<span id="07ee2323"></span>
#### Non\-merged results


|$1.uid |$1.region |
|---|---|
|10001 |beijing |
|10002 |shanghai |
|10003 |guangzhou |


<span id="839fec86"></span>
#### Concatenation result


|$1.uid |$1.region |$2.uid |$2.region |$2.total |
|---|---|---|---|---|
|10001 |beijing |10001 |beijing |18 |
|10002 |shanghai |10002 |shanghai |20 |
|10003 |guangzhou |/ |/ |/ |
|/ |/ |10004 |shenzhen |19 |


<span id="158c3f39"></span>
#### Inline result

Set operation: condition is `$1.uid==$2.uid`


|$1.uid/$2.uid |$1.region |$2.region |$2.total |
|---|---|---|---|
|10001 |beijing |beijing |18 |
|10002 |shanghai |shanghai |20 |


<span id="528eeeec"></span>
#### Full join result

Set operation: condition is `$1.uid==$2.uid`


|$1.uid/$2.uid |$1.region |$2.region |$2.total |
|---|---|---|---|
|10001 |beijing |beijing |18 |
|10002 |shanghai |shanghai |20 |
|10003 |guangzhou |/ |/ |
|10004 |/ |shenzhen |19 |


<span id="7915b0b5"></span>
#### Left join result

Set operation: condition is `$1.uid==$2.uid`


|$1.uid |$1.region |$2.region |$2.total |
|---|---|---|---|
|10001 |beijing |beijing |18 |
|10002 |shanghai |shanghai |20 |
|10003 |guangzhou |null |null |


<span id="f08f3956"></span>
#### Right join result

Set operation: condition is `$1.uid==$2.uid`


|$2.uid |$1.region |$2.region |$2.total |
|---|---|---|---|
|10001 |beijing |beijing |18 |
|10002 |shanghai |shanghai |20 |
|10004 |null |shenzhen |19 |


<span id="2afa3909"></span>
#### Left anti join result

Set operation: condition is `$1.uid==$2.uid`


|$1.uid |$1.region |
|---|---|
|10003 |guangzhou |


<span id="d8c4441f"></span>
#### Right semi join

Set operation: condition is `$1.uid==$2.uid`


|$2.uid |$2.region |$2.total |
|---|---|---|
|10004 |shenzhen |19 |
