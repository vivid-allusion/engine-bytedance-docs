---
title: "Bitmap computing (pg_roaringbitmap)"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/computing_bitmap-pg_roaringbitmap"
---

The pg_roaringbitmap extension is an efficient bitmap storage and computing extension.

<span id=".5a6e546w5Y6f55CG"></span>
## Implementation principle

The RoaringBitmap algorithm mainly addresses the fixed space consumption issue of traditional Bitmap. It reduces Bitmap space usage while providing high\-performance bitmap computing. In the most extreme scenarios, traditional bitmap may occupy a large space even when storing only two numbers. For example, storing the numbers 0 and 1,000,000 requires traditional bitmap to pre\-allocate 1,000,001 bits, about 125 KB of space; but Roaringbitmap only requires 8 bytes in this case.

<span id=".57uP5YW4IFJvYXJpbmdCaXRhbXAg566X5rOV"></span>
### Classic RoaringBitmap algorithm

The classic RoaringBitmap algorithm divides each 32\-bit signed integer in the set [\-2147483648, 2147483647] into two parts: high 16 bits + low 16 bits. The high 16 bits serve as the first\-level index for storage and retrieval, while the low 16 bits are the secondary data stored in Containers. Containers have two Types: Array Container and Bitmap Container, as shown below:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_73f0c44ed026870fb054c14be3e978d5.jpeg) </span>

In the above Roaring bitmap, the 4\-byte integer values stored have high 16Bits of 0x0000, 0x0001, 0x0002 respectively:


* High 16 bits 0x0000: stored using an ordered Array Container, containing the first 1000 multiples of 62.

* High 16 bits 0x0001: stored using an ordered Array Container, containing 100 integers in the range [216, 216+100).

* High 16 bits 0x0002: stored using a Bitmap Container, containing 215 even numbers in the range [216, 3×216).


The choice between Array Container and Bitmap Container depends on the number of 16Bit integers stored in the corresponding Container. The details are as follows:


* When the number of 16Bit integers stored in the Container is less than or equal to 4096, the maximum space occupied by a single Container is 4096 \* 16Bit = 8KB, and an array container is used for storage;

* When the number of 16Bit integers stored in the Container is greater than 4096, a Bitmap container is used for storage. The space occupied by a single Bitmap container is fixed at: 216Bit = 8KB.


<span id=".5o-S5Lu26YeH55So55qEIFJvYXJpbmdCaXRtYXA="></span>
### RoaringBitmap used by the extension

The RoaringBitmap used by the Extension adopts an algorithm that adds run container optimization to the classic RoaringBitmap algorithm, optimizing bitmaps with step properties. The details are as follows:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6d49d959b41ebea8efb8e8e2187c3cca.jpeg) </span>

In the above Roaring bitmap, the 4\-byte integer values stored have high 16Bits of 0x0000, 0x0001, 0x0002 respectively:


* High 16Bit 0x0000: stored in an array container ordered array, storing the first 1000 integers that are multiples of 62

* High 16Bit 0x0001: stored in a run container in compressed form, storing three intervals [216, 216 + 100), [216 + 101, 216 + 201), [216 + 300, 216 + 400) totaling 300 integers, with the container occupying only 6Bit.

* High 16Bit 0x0002: stored in a bitmap container, storing 215 even numbers in the range [2×216, 3×216).


<span id=".5a6J6KOF5o-S5Lu2"></span>
## Install extension

Use the following command to install the extension.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="0">tip</div>


<div data-tips="true" data-tips-type="default" data-wrapper-indent="0">A super account is required to create the extension.</div>


```sql
create extension roaringbitmap;
```


<span id=".5L2_55So6K-05piO"></span>
## 

<div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip</div>


<div data-tips="true" data-tips-type="default" data-wrapper-indent="1">A super account is required to create the extension. Instructions</div>


<span id=".5pWw5o2u57G75Z6L"></span>
### Data type


|**Type name** |roaringbitmap |
|---|---|
|**Usage example** |```sql```<br>```select  '{}'::roaringbitmap;```<br>```select  '  {          }  '::roaringbitmap;```<br>```select  '{        1 }'::roaringbitmap;```<br>```select  '{-1,2,555555,-4}'::roaringbitmap;```<br>```select  '{ -1 ,  2  , 555555 ,  -4  }'::roaringbitmap;```<br>```select  '{ 1 ,  -2  , 555555 ,  -4  }'::roaringbitmap;```<br>```select  '{ 1 ,  -2  , 555555 ,  -4  ,2147483647,-2147483648}'::roaringbitmap;```<br>```select  roaringbitmap('{ 1 ,  -2  , 555555 ,  -4  }');```<br>```select  '{1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,33,34,35,36,37,38,39,40,41,42,43,44,45,46,47,48,49,50,51,52,53,54,55,56,57,58,59,60,61,62,63,64,65,66,67,68,69,70,71,72,73,74,75,76,77,78,79,80,81,82,83,84,85,86,87,88,89,90,91,92,93,94,95,96,97,98,99,100,101,102,103,104,105,106,107,108,109,110,111,112,113,114,115,116,117,118,119,120,121,122,123,124,125,126,127,128,129,130,131,132,133,134,135,136,137,138,139,140,141,142,143,144,145,146,147,148,149,150,151,152,153,154,155,156,157,158,159,160,161,162,163,164,165,166,167,168,169,170,171,172,173,174,175,176,177,178,179,180,181,182,183,184,185,186,187,188,189,190,191,192,193,194,195,196,197,198,199,200,201,202,203,204,205,206,207,208,209,210,211,212,213,214,215,216,217,218,219,220,221,222,223,224,225,226,227,228,229,230,231,232,233,234,235,236,237,238,239,240,241,242,243,244,245,246,247,248,249,250,251,252,253,254,255,256,257,258,259,260,261,262,263,264,265,266,267,268,269,270,271,272,273,274,275,276,277,278,279,280,281,282,283,284,285,286,287,288,289,290,291,292,293,294,295,296,297,298,299,300,301,302,303,304,305,306,307,308,309,310,311,312,313,314,315,316,317,318,319,320,321,322,323,324,325,326,327,328,329,330,331,332,333,334,335,336,337,338,339,340,341,342,343,344,345,346,347,348,349,350,351,352,353,354,355,356,357,358,359,360,361,362,363,364,365,366,367,368,369,370,371,372,373,374,375,376,377,378,379,380,381,382,383,384,385,386,387,388,389,390,391,392,393,394,395,396,397,398,399,400}'::roaringbitmap;```<br> |


<span id="GUC"></span>
### GUC


|**Parameter name** |roaringbitmap.output_format |
|---|---|
|**Parameter description** |character type, used to control the output format of roaringbitmap type, value range: array and bytea, default value is bytea<br><br><br>* array: Return roaringbitmap values as an array format during queries<br><br>* bytea: Return roaringbitmap values as bytea format during queries |
|**Usage** |```sql```<br>```set roaringbitmap.output_format = 'array';```<br>```select  '{-1,2,555555,-4}'::roaringbitmap;```<br>``````<br>```set roaringbitmap.output_format = 'bytea';```<br>```select  '{-1,2,555555,-4}'::roaringbitmap;```<br>``````<br>```set roaringbitmap.output_format = 'array';```<br>```select '\x3a300000030000000000000008000000ffff01002000000022000000240000000200237afcffffff'::roaringbitmap;```<br><br><br>```sql```<br>```sysbench=> set roaringbitmap.output_format = "array";```<br>```SET```<br>```sysbench=> select    '{-1,2,5555555,-4}':: roaringbitmap;```<br>```roaringbitmap```<br>```------------------```<br>```{2,555555,-4,-1}```<br>```(1 row)```<br>``````<br>```sysbench=>```<br>```sysbench=> set roaringbitmap.output_format = 'bytea';```<br>```SET```<br>```sysbench=> select '{-1,2,55555,-4}'::roaringbitmap;```<br>```                                  roaringbitmap```<br>```----------------------------------------------------------------------------------```<br>```\x3a300000030000000000000008000000ffff01002000000022000000240000000200237afcffffff```<br>``````<br>``````<br>```sysbench=>```<br>```sysbench=> select '\x3a300000030000000000000008000000ffff01002000000022000000240000000200237afcffffff'::roaringbitmap;```<br>```                                   roaringbitmap```<br>```-----------------------------------------------------------------------------------```<br>```\x3a300000030000000000000080000000ffff01002000000022000000240000000200237afcfffffff```<br>```(1 row)```<br>``````<br>```sysbench=> set roaringbitmap.output_format = 'array'```<br>```SET```<br>```sysbench=> select '\x3a300000030000000000000008000000ffff01002000000022000000240000000200237afcffffff'::roaringbitmap;```<br>```roaringbitmap```<br>```----------------```<br>```{2,555555,-4,-1}```<br>```(1 row)```<br>``````<br>```sysbench=>```<br> |


<span id=".5Ye95pWw5ZKM5pON5L2c56ym"></span>
### Functions and operators

<span id=".6L6F5Yqp5Ye95pWw"></span>
#### helper functions

used to generate integer arrays of specified dimensions.

```sql
create or replace function gen_array(dim int4) 
    returns int4[] 
as $$ 
    select array_agg((random()* 1000000)::int4) from generate_series(1, dim) 
$$ 
language sql 
volatile 
cost 1;
```


<span id=".5Ye95pWw5Y-K5pON5L2c56ym"></span>
#### Functions and operators


|**function name** |**operators name** |**Input** |**output** |**Note** |**Example** |
|---|---|---|---|---|---|
|rb_and |& |roaringbitmap, roaringbitmap |roaringbitmap |and |```sql```<br>```select rb_and(rb_build('{1,2,3,4,5}'),rb_build('{4,5,6,7}'));```<br>```select rb_build('{1,2,3,4,5}') & rb_build('{4,5,6,7}');```<br>```select rb_build(gen_array(4)) & rb_build(gen_array(5));```<br>```select rb_build(gen_array(1000)) & rb_build(gen_array(1000));```<br> |
|rb_or |\| |roaringbitmap, roaringbitmap |roaringbitmap |or |```sql```<br>```select rb_or(rb_build('{1,2,3,4,5}'),rb_build('{4,5,6,7}'));```<br>```select rb_build('{1,2,3,4,5}')```<br>``````<br>```select rb_build(gen_array(4))```<br>```select rb_build(gen_array(1000))```<br> |
|rb_xor |# |roaringbitmap, roaringbitmap |roaringbitmap |xor |```sql```<br>```select rb_xor(rb_build('{1,2,3,4,5}'),rb_build('{4,5,6,7}'));```<br>```select rb_build('{1,2,3,4,5}') # rb_build('{4,5,6,7}');```<br>``````<br>```select rb_build(gen_array(4)) # rb_build(gen_array(5));```<br>```select rb_build(gen_array(1000)) # rb_build(gen_array(1000));```<br> |
|rb_andnot |\- |roaringbitmap, roaringbitmap |roaringbitmap |and Non |```sql```<br>```select rb_andnot(rb_build('{1,2,3,4,5}'),rb_build('{4,5,6,7}'));```<br>```select rb_build('{1,2,3,4,5}') - rb_build('{4,5,6,7}');```<br>``````<br>```select rb_build(gen_array(4)) - rb_build(gen_array(5));```<br>```select rb_build(gen_array(1000)) - rb_build(gen_array(1000));```<br> |
|rb_add |\| |roaringbitmap, integer |roaringbitmap |add to bitmap |```sql```<br>```select rb_add(rb_build('{1,2,3,4,5}'), 10);```<br>```select rb_build('{1,2,3,4,5}')```<br>``````<br>```select rb_add(rb_build(gen_array(5), 10);```<br>```select rb_build(rb_build(gen_array(5))```<br> |
||\| |integer, roaringbitmap |roaringbitmap |add to bitmap |```sql```<br>```select rb_add(10, rb_build('{1,2,3,4,5}'));```<br>```select 10```<br>``````<br>```select rb_add(10, rb_build(gen_array(5));```<br>```select 10```<br> |
|rb_remove |\- |roaringbitmap, integer |roaringbitmap |remove integer from bitmap |```sql```<br>```select rb_remove(rb_build('{1,2,3,4,5}'), 3);```<br>```select rb_build('{1,2,3,4,5}') - 3;```<br> |
|rb_contains |@\> |roaringbitmap, roaringbitmap |bool |whether it contains |```sql```<br>```select rb_contains(rb_build('{1,2,3,4,5}'),rb_build('{4,5}'));```<br>```select rb_build('{1,2,3,4,5}') @> rb_build('{4,5}');```<br> |
||@\> |roaringbitmap, integer |bool |whether it contains |```sql```<br>```select rb_contains(rb_build('{1,2,3,4,5}'), 3);```<br>```select rb_build('{1,2,3,4,5}')  @> 3;```<br> |
|rb_containedby |<@ |roaringbitmap, roaringbitmap |bool |exists in |```sql```<br>```select rb_containedby(rb_build('{3,4,5}'),rb_build('{1,2,3,4,5,6}'));```<br>```select rb_build('{3,4,5}') <@ rb_build('{1,2,3,4,5,6}');```<br> |
||<@ |integer, roaringbitmap |bool |exists in |```sql```<br>```select rb_containedby(3, rb_build('{1,2,3,4,5}'));```<br>```select 3 <@ rb_build('{1,2,3,4,5}');```<br> |
|rb_intersect |&& |roaringbitmap, roaringbitmap |bool |whether they intersect |```sql```<br>```select rb_intersect(rb_build('{3,4,5}'),rb_build('{1,2,3,4,5,6}'));```<br>```select rb_build('{3,4,5}') && rb_build('{1,2,3,4,5,6}');```<br> |
|rb_equals |= |roaringbitmap, roaringbitmap |bool |whether equal |```sql```<br>```select rb_equals(rb_build('{3,4,5}'),rb_build('{1,2,3,4,5,6}'));```<br>```select rb_build('{3,4,5}') = rb_build('{1,2,3,4,5,6}');```<br>``````<br>```select rb_equals(rb_build('{3,4,5}'),rb_build('{4,5,3}'));```<br>```select rb_build('{3,4,5}') = rb_build('{4,5,3}');```<br> |
|rb_not_equals |<\> |roaringbitmap, roaringbitmap |bool |not equal |```sql```<br>```select rb_not_equals(rb_build('{3,4,5}'),rb_build('{1,2,3,4,5,6}'));```<br>```select rb_build('{3,4,5}') <> rb_build('{1,2,3,4,5,6}');```<br>``````<br>```select rb_not_equals(rb_build('{3,4,5}'),rb_build('{4,5,3}'));```<br>```select rb_build('{3,4,5}') <> rb_build('{4,5,3}');```<br> |


<span id=".5Ye95pWw"></span>
#### Functions


|**function name** |**enter information** |**output** |**Note** |**Example** |
|---|---|---|---|---|
|rb_build |integer[] |roaringbitmap |create bitmap from an integer array |```sql```<br>```set roaringbitmap.output_format = 'array';```<br>``````<br>```select rb_build('{1,2,3,4,5}');```<br>```select rb_build(gen_array(10));```<br> |
|rb_index |roaringbitmap, integer |bigint |Return the index of the integer in the bitmap starting from 0, return \-1 if not found |```sql```<br>```select rb_index(rb_build('{-1,2,-3,4,5}'), 5);```<br>```select rb_index(rb_build(gen_array(10)), 10);```<br> |
|rb_cardinality |roaringbitmap |bigint |return cardinality |```sql```<br>```select rb_cardinality(rb_build('{-1,2,-3,4,5}'));```<br>```select rb_cardinality(rb_build(gen_array(10)));```<br> |
|rb_and_cardinality |roaringbitmap, roaringbitmap |bigint |Return the cardinality after bitmap |```sql```<br>```select rb_and_cardinality(rb_build('{1,2,3,4,5}'),rb_build('{4,5,6,7}'));```<br> |
|rb_or_cardinality |roaringbitmap, roaringbitmap |bigint |bitmap or return cardinality later |```sql```<br>```select rb_or_cardinality(rb_build('{1,2,3,4,5}'),rb_build('{4,5,6,7}'));```<br> |
|rb_xor_cardinality |roaringbitmap, roaringbitmap |bigint |Return cardinality after bitmap xor |```sql```<br>```select rb_xor_cardinality(rb_build('{1,2,3,4,5}'),rb_build('{4,5,6,7}'));```<br> |
|rb_andnot_cardinality |roaringbitmap, roaringbitmap |bigint |Return the cardinality after bitmap and not |```sql```<br>```select rb_andnot_cardinality(rb_build('{1,2,3,4,5}'),rb_build('{4,5,6,7}'));```<br> |
|rb_is_empty |roaringbitmap |bool |whether the bitmap is empty |```sql```<br>```select rb_is_empty(rb_build('{1,2,3,4,5}'));```<br>```select rb_is_empty(rb_build('{}'));```<br> |
|rb_fill |roaringbitmap, range_start bigint, range_end bigint |roaringbitmap |fill bitmap within specified range, excluding range_end |```sql```<br>```select rb_fill(rb_build('{1,2,3,4,5,6,7,8,9}'), 10,  15);```<br> |
|rb_clear |roaringbitmap, range_start bigint, range_end bigint |roaringbitmap |Clear the integers in the specified range of the bitmap, excluding range_end |```sql```<br>```select rb_clear(rb_build('{1,2,3,4,5,6,7,8,9}'), 2, 5);```<br> |
|rb_flip |roaringbitmap, range_start bigint, range_end bigint |roaringbitmap |Invert the specified range, existing values become non\-existent, non\-existing become existing, excluding range_end |```sql```<br>```select rb_flip(rb_build('{1,2,3,4,5,6,7,8,9}'), 2, 15);```<br> |
|rb_range |roaringbitmap, range_start bigint, range_end bigint |roaringbitmap |Return the sub\-bitmap of the specified range, excluding range_end |```sql```<br>```select rb_range(rb_build('{1,2,3,4,5,6,7,8,9}'), 2, 7);```<br> |
|rb_range_cardinality |roaringbitmap, range_start bigint, range_end bigint |bigint |return the cardinality of the specified range sub bitmap, excluding range_end |```sql```<br>```select rb_range_cardinality(rb_build('{1,2,3,4,5,6,7,8,9}'), 2, 7);```<br> |
|rb_min |roaringbitmap |integer |Return the smallest offset in the bitmap, or NULL if the bitmap is empty. |```sql```<br>```select rb_min(rb_build('{67,12,23,4,35,6,7,8,9}'));```<br> |
|rb_max |roaringbitmap |integer |Return the largest offset in the Bitmap; return null if the Bitmap is empty. |```sql```<br>```select rb_max(rb_build('{67,12,23,4,35,6,7,8,9}'));```<br> |
|rb_rank |roaringbitmap, integer |bigint |return the cardinality in the bitmap less than or equal to the specified offset |```sql```<br>```select rb_rank(rb_build('{9,8,7,3,4,5,1,2,6}'), 5);```<br>```select rb_rank(rb_build('{9,8,7,3,4,1,2,6}'), 5);```<br> |
|rb_jaccard_dist |roaringbitmap, roaringbitmap |float8 |return the Jaccard coefficient of two bitmaps; the larger the value, the higher the similarity between the bitmaps |```sql```<br>```select rb_jaccard_dist(rb_build('{1,2,3,4,5}'),rb_build('{4,5,1,2,3}'));```<br>```select rb_jaccard_dist(rb_build('{1,2,3,4,5}'),rb_build('{4,5,6,7}'));```<br>```select  rb_jaccard_dist(rb_build('{1,2,3,4,5}'),rb_build('{9,8,6,7}'));```<br> |
|rb_select |roaringbitmap, bitset_limit bigint,bitset_offset bigint=0,reverse boolean=false,range_start bigint=0,range_end bigint=4294967296 |roaringbitmap |Return the subset [bitset_offset,bitset_offset+bitset_limit) of the range [range_start,range_end) |```sql```<br>```select rb_select(rb_build('{1,2,3,4,5,6,7,8,9}'), 5, 2);```<br>```select rb_select(rb_build('{1,2,3,4,5,6,7,8,9}'), 5, 2, false, 3, 9);```<br>```select rb_select(rb_build('{1,2,3,4,5,6,7,8,9}'), 5, 2, true, 3, 9);```<br> |
|rb_to_array |roaringbitmap |integer[] |convert an integer array to a bitmap |```sql```<br>```select rb_to_array(rb_build('{1,2,3,4,5,6,7,8,9}'));```<br>```select rb_to_array(rb_build(gen_array(10)));```<br> |
|rb_iterate |roaringbitmap |SETOF integer |return the integers in the bitmap as records, opposite to the effect of rb_build_agg |```sql```<br>```select rb_iterate(rb_build('{1,2,3,4,5,6,7,8,9}'));```<br>```select rb_iterate(rb_build(gen_array(10)));```<br> |


<span id=".6IGa5ZCI5Ye95pWw"></span>
##### Aggregate functions

```sql
drop table tbl_rb_agg;
create table tbl_rb_agg(id serial, rb roaringbitmap);

insert into tbl_rb_agg(rb) select rb_build('{1,2,3,4,5}');
insert into tbl_rb_agg(rb) select rb_build('{3,4,5,6,7}');
insert into tbl_rb_agg(rb) select rb_build('{4,5,6,7,8,9}');
select * from tbl_rb_agg;
```


```sql
sysbench=> drop table tbl_rb_agg;
DROP TABLE
sysbench=> create table tbl_rb_agg(id serial, rb roaaringbitmap);
CREATE TABLE
sysbench=>
sysbench=> insert into tbl_rb_agg(rb) select rb_build('{1,2,3,4,5}');
INSERT 0 1
sysbench=> insert into tbl_rb_agg(rb) select rb_build('{3,4,5,6,7}');
INSERT 0 1
sysbench=> insert into tbl_rb_agg(rb) select rb_build('{4,5,6,7,8,9}');
INSERT 0 1
sysbench=> select * from tbl_rb_agg;
 id |        rb
 ---+-------------————
  1 |  {1,2,3,4,5}
  2 |  {3,4,5,6,7}
  3 |  {4,5,6,7,8,9}
(3 rows)
```



|**function name** |**Input** |**output** |**Note** |**Example** |
|---|---|---|---|---|
|rb_or_agg |roaringbitmap |roaringbitmap |or aggregate |```sql```<br>```select rb_or_agg(rb)  from tbl_rb_agg;```<br> |
|rb_or_cardinality_agg |roaringbitmap |bigint |or aggregate and return its cardinality |```sql```<br>```select rb_or_cardinality_agg(rb)  from tbl_rb_agg;```<br> |
|rb_and_agg |roaringbitmap |roaringbitmap |and aggregation |```sql```<br>```select rb_and_agg(rb)  from tbl_rb_agg;```<br> |
|rb_and_cardinality_agg |roaringbitmap |bigint |and aggregate return its cardinality |```sql```<br>```select rb_and_cardinality_agg(rb)  from tbl_rb_agg;```<br> |
|rb_xor_agg |roaringbitmap |roaringbitmap |xor aggregation |```sql```<br>```select rb_xor_agg(rb)  from tbl_rb_agg;```<br> |
|rb_xor_cardinality_agg |roaringbitmap |bigint |xor aggregate and return its cardinality |```sql```<br>```select rb_xor_cardinality_agg(rb)  from tbl_rb_agg;```<br> |
|rb_build_agg |integer |roaringbitmap |construct bitmap from an integer set, opposite effect of rb_iterate |```sql```<br>```select rb_build_agg(id)  from tbl_rb_agg;```<br> |
