---
title: "Searching based on high-dimensional vector similarity (pg_vector)"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/searching_based_on_high-dimensional_vector_similarity-pg_vector"
---

## About pg_vector

pg_vector is an extension that provides efficient similarity search capabilities for high\-dimensional vectors. It includes the following features:

* supports vector data types that can store and query vector data.

* supports precise and approximate nearest neighbor search (ANN). Supported distance or similarity metrics include Euclidean distance (L2 norm Euclidean Distance), Manhattan distance (L1 Manhattan Distance), cosine similarity, and inner product.

* supports creating vectors with up to 16,000 dimensions and indexing vectors with up to 2,000 dimensions.

## Extension usage

### Create extension

> **tip**

> A super account is required to create the extension.

```sql
create extension vector;
```

### Query extension version

```sql
select * from pg_available_extensions where name='vector';
```

If your instance version is PostgreSQL 11 and the used extension version is below 0.5.0, upgrade the extension to version 0.5.0 using the following command.

```sql
alter extension vector update to '0.5.0';
```

If your instance version is PostgreSQL 12 or higher, upgrade the extension to version 0.6.2 using the following command.

```sql
alter extension vector update to '0.6.2';
```

If your instance version is PostgreSQL 13 or higher, upgrade the extension to version 0.8.2 using the following command.

```sql
alter extension vector update to '0.8.2';
```

### Delete extension

```sql
drop extension vector;
```

### Data type

pg_vector provides three vector data types (the following examples are based on the vector type).

|Type |comment |Max supported dimension |maximum index build dimension |supported indexes |
|---|---|---|---|---|
|vector |Represents 32\-bit floating\-point vectors |16000 |2000 |btree、ivfflat、hnsw |
|halfvec |Represents a 16\-bit floating point vector |16000 |4000 |btree、ivfflat、hnsw |
|sparsevec |Represents sparse vector, input format is `{index1:value1,index2:value2}/dimensions` |1000000000 (non\-zero dimension 16000) |nonzero dimension 1000 |btree、hnsw |

### Insert&Select

```sql
create table tbl_vector (tc1 vector(3),  tc2 halfvec(3), tc3 sparsevec(3));
insert into tbl_vector values ('[1,2,3]', '[1,2,3]', '{2:1}/3');
select * from tbl_vector;
```

### Vector operators

pg_vector extension implements 14 operators for vector types.

> **warning**

* > Two vectors operated on by operators must have the same dimension.

* > For convenience, pg_vector normalizes the results of Euclidean distance, Manhattan distance, cosine similarity, and inner product operations: the smaller the result, the higher the similarity between the two vectors involved.

|Operators |Note |Examples |
|---|---|---|
|<\-\> |L2 Euclidean distance calculation |select tc1 <\-\> '[1,1,1]' as euclidean_distance from tbl_vector order by euclidean_distance ; |
|<#\> |Inner product operation |select tc1 <#\> '[1,1,1]' as inner_product from tbl_vector order by inner_product ; |
|<=\> |cosine similarity calculation |select tc1 <=\> '[1,1,1]' as cosine_similarity from tbl_vector order by cosine_similarity ; |
|+ |add |select tc1 + '[1,1,1]' from tbl_vector; |
|\- |minus |select tc1 \- '[1,1,1]' from tbl_vector; |
|< |Less than |select \* from tbl_vector where tc1 < '[1,1,1]' ; |
|<= |Less than or equal to |select \* from tbl_vector where tc1 <= '[1,1,1]' ; |
|= |= |select \* from tbl_vector where tc1 = '[1,1,1]' ; |
|<\> |Not equal to |select \* from tbl_vector where tc1 <\> '[1,1,1]' ; |
|\>= |Greater than or equal to |select \* from tbl_vector where tc1 \>= '[1,1,1]' ; |
|\> |greater than |select \* from tbl_vector where tc1 \> '[1,1,1]' ; |
|\* |Bitwise multiplication |select tc1 \* '[2,2,2]' from tbl_vector; |
|<+\> |Calculate Manhattan distance |select tc1 <+\> '[1,1,1]' from tbl_vector; |
|\|\| |Vector concatenation |select tc1 \|\| '[1,1,1]' from tbl_vector; |

### Index

Usually, the number of vector entries (rows) stored in a single table can reach hundreds of millions. To speed up access to vector type data and similarity calculation, pg_vector provides three index types: btree index, ivfflat index, and hnsw index.

#### Create index

* Create btree index

   ```sql
   drop table tbl_vector;
   create table tbl_vector(id serial, tc1 vector(100));
   insert into tbl_vector (tc1)  select array_agg(random())::vector(100) from generate_series(1.0,100.0) ;
   create index on tbl_vector (tc1);
   ```

   > **tip**

   * > When creating a btree index, the vector dimension must be less than or equal to 674.

   * > In practice, it is recommended to keep the vector dimension for creating btree index at 500 or below to prevent issues such as decreased index scan efficiency due to toast access.

* Create ivfflat index

   ```sql
   drop table tbl_vector ;
   create table tbl_vector(id serial, tc1 vector(5));
   create index tbl_vector_tc1_idx on tbl_vector using ivfflat  (tc1) with (lists = 4);
   ```

   > **tip**

   * > When creating an ivfflat index without specifying opclass, `vector_l2_ops` is used by default.

   * > ivfflat index requires the vector column dimension to be indexed to be less than or equal to 2000.

   * > ivfflat does not support multi\-column indexes.

   * > ivfflat index applies only to order by, not to where filtering. Because where conditions can only be used with bool type or bool expressions, and the ivfflat operators (<\-\>, <=\>, <#\>) do not return bool type values.

   * > During index scanning, recall rate depends on ivfflat.probes and the lists value specified when creating the index. The higher the ivfflat.probes value, the higher the recall rate and the lower the index scan performance; the lower the ivfflat.probes value, the lower the recall rate and the higher the index scan performance. The highest recall rate is achieved by sequential scanning.

* Create hnsw index

   ```sql
   drop table tbl_vector;
   create table tbl_vector(id serial, tc1 vector(5));
   create index tbl_vector_tc1_idx on tbl_vector using hnsw (tc1 vector_l2_ops) with (m = 5, ef_construction = 10);
   ```

   > **tip**

   * > hnsw index requires the dimension of the vector column to be indexed to be less than or equal to 2,000.

   * > hnsw does not support multi\-column indexes.

   * > hnsw index applies only to order by, not to where filtering. Because where conditions can only be used with bool type or bool expressions, and hnsw operators (<\-\>, <=\>, <#\>) do not return bool type values.

* Check the current build progress of the index

   > **tip**

   > This feature is available only in pg_vector instances version 0.6.2 and above.

   ```sql
   vtest=# SELECT phase, round(100.0 * blocks_done / nullif(blocks_total, 0), 1) AS "%" FROM pg_stat_progress_create_index;
                phase              |  %
   --------------------------------+-----
    building index: loading tuples | 8.6
   (1 row)
   ```

#### Index parameters

* ivfflat index parameters

   The following two parameters are used for ivfflat index creation and index scanning, respectively:

   |Parameter |When to use |Description |
   |---|---|---|
   |lists |specified when creating indexes, used during insert |* The minimum value is 1, the maximum value is 32768, and the default value is 100, representing the number of lists the dataset in the index is divided into. The larger the value, the more the dataset is divided, resulting in smaller subsets and faster query efficiency.<br><br>* The lists value should not be too large; it is recommended to set it within 2000. Otherwise, indexing will occupy more memory, which may cause memory shortage and lead to Failed to create the index. |
   |ivfflat.probes |Specified during query, used for index scanning. |The minimum value is 1, the maximum value is 32768, and the default value is 1. It represents the number of lists searched during the current index scan. The larger this value, the more lists are scanned in search, resulting in a higher recall, but the index scan efficiency decreases; conversely, the smaller this value, the fewer lists are scanned, leading to lower recall but improved index scan efficiency. If this value is greater than the lists value specified when creating the index, query optimization will ignore the index and choose a full table scan. At this point, query performance may decrease. |
   |ivfflat.iterative_scan |Specified during query, used for index scanning. |Optional values are "off" or "relaxed_order". If set to "relaxed_order", the index scan range expands during queries, achieving higher recall at the cost of more time. |
   |ivfflat.max_probes |Specified during query, used for index scanning. |minimum value is 1, maximum value is 32768, default value is 32768. ivfflat.iterative_scan takes effect when set to "relaxed_order". During this index scanning process, the maximum number of search lists is max(ivfflat.probes, ivfflat.max_probes). |

* hnsw index parameters

   The following six parameters are used for hnsw index creation and scanning, respectively:

   |Parameter |When to use |Description |
   |---|---|---|
   |m |specified when creating indexes, used during insert |Indicates the number of connections each point needs to establish with other points in the graph. The minimum value of `m` is 2, the maximum value is 100, and the default value is 16. Generally, the larger the value of `m`, the higher the recall rate and the greater the memory consumption. The smaller the value of `m`, the shorter the build time. |
   |ef_construction |specified when creating indexes, used during insert |Represents the size of the dynamic candidate set during index building. The minimum value of `ef_construction` is 4, the maximum value is 1000, and the default value is 64. `ef_construction` must be greater than `m`, typically set to twice the value of `m`. For clustered data, `ef_construction` typically performs better when set to a larger value. The larger the value of `ef_construction`, the slower the index builds. |
   |hnsw.ef_search |Specified during query and used in index scan. |This parameter is used during querying to limit the maximum return record quantity and accuracy. The minimum value of `hnsw.ef_search` is 1, the maximum value is 1000, and the default value is 40. for example, setting the `hnsw.ef_search` value to 40 means the query will only return 40 rows, even if you attempt to query 100 nearest neighbor records.<br><br>usually the larger the `hnsw.ef_search`, the higher the search accuracy, but the longer the time consumed. |
   |hnsw.iterative_scan |Specified during query and used in index scan. |Optional values are "off", "relaxed_order", or "strict_order". If set to "relaxed_order" or "strict_order", the index scan range expands during queries to achieve a higher recall rate but consumes more time. |
   |hnsw.max_scan_tuples |Specified during query, used for index scanning. |minimum value is 1, default value is 20000, limits the maximum tuple quantity accessed during index scan expansion. |
   |hnsw.scan_mem_multiplier |Specified during query, used for index scanning. |minimum value is 1, maximum value is 1000, default value is 1; it sets the multiplier for work_mem used during extended index scans |

   The following three parameters can be used to speed up hnsw index building:

   |Parameter |Description |
   |---|---|
   |max_parallel_workers |set the system's maximum parallel process quantity, default value is 8. |
   |max_parallel_maintenance_workers |Sets the maximum number of parallel workers for a single utility command (such as CREATE INDEX). |
   |maintenance_work_mem |specifies the maximum memory used for maintenance actions (such as VACUUM, create index). |

#### Examples

* Create and use a btree index.

   ```sql
   drop table tbl_vector ;
   create table tbl_vector (id serial, tc1 vector(5));
   insert into tbl_vector (tc1)  select array_agg(random())::vector(5) from generate_series(1.0,5.0) ;
   create index on tbl_vector (tc1);
   select * from tbl_vector order by tc1;
   ```

* Create ivfflat index using `vector_l2_ops` for Euclidean distance similarity search

   ```sql
   drop table tbl_vector ;
   create table tbl_vector(id serial, tc1 vector(5));
   insert into tbl_vector (tc1)  select array_agg(random())::vector(5) from generate_series(1.0,5.0) ;
   create index tbl_vector_tc1_idx on tbl_vector using ivfflat (tc1) with (lists = 4);
   
   -- high recall rate
   set ivfflat.probes = 4;   -- adjust ivfflat.probes to the same value as the index's lists, indicating scanning all lists
   select * from tbl_vector order by tc1 <-> '[0.559782,0.194308,0.454407,0.0176121,0.442676]';
   
   -- low recall rate
   set ivfflat.probes = 1;   -- adjust ivfflat.probes to be less than the index's lists, indicating scanning part of the lists
   select * from tbl_vector order by tc1 <-> '[0.559782,0.194308,0.454407,0.0176121,0.442676]';
   ```

* Createcreate ivfflat index using `vector_cosine`_ops for cosine similarity search

   ```sql
   drop index tbl_vector_tc1_idx;
   create index tbl_vector_tc1_idx on tbl_vector using ivfflat (tc1 vector_cosine_ops) with (lists = 4);
   
   -- high recall rate
   set ivfflat.probes = 4;   -- adjust ivfflat.probes to the same value as the index's lists, indicating scanning all lists
   select * from tbl_vector order by tc1 <=> '[0.559782,0.194308,0.454407,0.0176121,0.442676]';
   
   -- low recall rate
   set ivfflat.probes = 1;   -- adjust ivfflat.probes to be less than the index's lists, indicating scanning part of the lists
   select * from tbl_vector order by tc1 <=> '[0.559782,0.194308,0.454407,0.0176121,0.442676]';
   ```

* Create ivfflat index using vector`_ip_ops for i`nner product similarity search

   ```sql
   drop index tbl_vector_tc1_idx;
   create index tbl_vector_tc1_idx on tbl_vector using ivfflat (tc1 vector_ip_ops) with (lists = 4);
   
   -- high recall rate
   set ivfflat.probes = 4;   -- adjust ivfflat.probes to the same value as the index's lists, indicating scanning all lists
   select * from tbl_vector order by tc1 <#> '[0.559782,0.194308,0.454407,0.0176121,0.442676]';
   
   -- low recall rate
   set ivfflat.probes = 1;   -- adjust ivfflat.probes to be less than the index's lists, indicating scanning part of the lists
   select * from tbl_vector order by tc1 <#> '[0.559782,0.194308,0.454407,0.0176121,0.442676]';
   ```

* Parallel create hnsw index using `max_parallel_workers`, `max_parallel_maintenance_workers`, and `maintenance_work_mem` parameters

   ```sql
   set maintenance_work_mem = '1GB';
   set max_parallel_workers = 4;
   set max_parallel_maintenance_workers = 4;
   drop index IF EXISTS tbl_vector_tc1_idx;
   create index tbl_vector_tc1_idx on tbl_vector using hnsw (tc1 vector_l2_ops) with (m = 10, ef_construction = 20);
   ```

* Create hnsw index using `vector_l2_ops` for Euclidean distance similarity search

   ```sql
   -- high recall rate
   drop index IF EXISTS tbl_vector_tc1_idx;
   create index tbl_vector_tc1_idx on tbl_vector using hnsw (tc1 vector_l2_ops) with (m = 10, ef_construction = 20);
   set hnsw.ef_search = 10;
   select * from tbl_vector order by tc1 <-> '[0.559782,0.194308,0.454407,0.0176121,0.442676]';
   -- low recall rate
   drop index IF EXISTS tbl_vector_tc1_idx;
   create index tbl_vector_tc1_idx on tbl_vector using hnsw (tc1 vector_l2_ops) with (m = 5 , ef_construction = 10);
   set hnsw.ef_search = 10;
   select * from tbl_vector order by tc1 <-> '[0.559782,0.194308,0.454407,0.0176121,0.442676]';
   ```

* Create hnsw index using `vector_cosine_ops` for cosine similarity search

   ```sql
   -- high recall rate
   drop index IF EXISTS tbl_vector_tc1_idx;
   create index tbl_vector_tc1_idx on tbl_vector using hnsw (tc1 vector_cosine_ops) with (m = 10, ef_construction = 20);
   set hnsw.ef_search = 10;
   select * from tbl_vector order by tc1 <=> '[0.559782,0.194308,0.454407,0.0176121,0.442676]';
   -- low recall rate
   drop index IF EXISTS tbl_vector_tc1_idx;
   create index tbl_vector_tc1_idx on tbl_vector using hnsw (tc1 vector_cosine_ops) with (m = 5 , ef_construction = 10);
   set hnsw.ef_search = 10;
   select * from tbl_vector order by tc1 <=> '[0.559782,0.194308,0.454407,0.0176121,0.442676]';
   ```

* Create hnsw index using `vector_ip_ops` for inner product similarity search

   ```sql
   -- high recall rate
   drop index IF EXISTS tbl_vector_tc1_idx;
   create index tbl_vector_tc1_idx on tbl_vector using hnsw (tc1 vector_ip_ops) with (m = 10, ef_construction = 20);
   set hnsw.ef_search = 10;
   select * from tbl_vector order by tc1 <#> '[0.559782,0.194308,0.454407,0.0176121,0.442676]';
   -- low recall rate
   drop index IF EXISTS tbl_vector_tc1_idx;
   create index tbl_vector_tc1_idx on tbl_vector using hnsw (tc1 vector_ip_ops) with (m = 5 , ef_construction = 10);
   set hnsw.ef_search = 10;
   select * from tbl_vector order by tc1 <#> '[0.559782,0.194308,0.454407,0.0176121,0.442676]';
   ```

> **tip**

> The high and low recall rates in the above example codes represent results under the set scenarios; actual cases require adjustment based on the business model

### Aggregate functions

The pg_vector extension provides two aggregate functions for vector types: avg() and sum()

* The avg() function calculates the average value of each dimension of a vector. The usage is shown in the example below:

   ```sql
   drop table tbl_vector ;
   create table tbl_vector(id serial, tc1 vector(5));
   insert into tbl_vector (tc1)  select array_agg(random())::vector(5) from generate_series(1.0,5.0) ;
   
   select avg(tc1) from tbl_vector;
   select id, avg(tc1) from tbl_vector group by id;
   ```

* The sum() function sums each dimension of the vector. The usage is shown in the example below:

   ```sql
   insert into tbl_vector (tc1)  select array_agg(random())::vector(5) from generate_series(1.0,5.0) ;
   select sum(tc1) from tbl_vector;
   select id, sum(tc1) from tbl_vector group by id;
   ```

### Data type conversion

The pg_vector extension provides conversions between vector types and several array types.

|**convert type** |**Examples** |
|---|---|
|convert vector to vector |```sql```<br>```select '[0.802642,0.339995,0.440122,0.476725,0.449537]'::vector;```<br> |
|convert vector to real[] |```sql```<br>```select vector('[0.802642,0.339995,0.440122,0.476725,0.449537]')::real[];```<br> |
|convert real[ ] to vector |```sql```<br>```select '{0.802642,0.339995,0.440122,0.476725,0.449537}'::real[]::vector;```<br> |
|convert int4[ ] to vector |```sql```<br>```select '{1,2,3,4,5}'::int4[]::vector;```<br> |
|Convert double precision[ ] to vector |```sql```<br>```select '{0.864488503430039,0.798674516845495,0.90717526525259,0.756084795109928,0.639521076343954}'::double precision[]::vector;```<br> |
|convert numeric[ ] to vector |```sql```<br>```select '{0.864488503430039,0.798674516845495,0.90717526525259,0.756084795109928,0.639521076343954}'::numeric[]::vector;```<br> |

## Introduction to pg_vector vector operation performance

In the vectorization scenario of RDS for PostgreSQL, a typical case involves storing embeddings vectors processed by large language models (LLM), such as [text-embedding-ada-002](https://platform.openai.com/docs/guides/embeddings) (with a fixed dimension of 1536), and calculating their similarity. This topic references this scenario to verify the impact of different data volumes, thread counts, concurrency levels, indexes, and parameter values on the database TPS and latency.

### Test parameters

|test parameter ||
|---|---|
|test concurrency |6/16 |
|Number of test threads |1/4 |
|test time |60s |
|PostgreSQL instance specification |single AZ with one primary and one standby 32C64G |
|client specification |32 vCPU 128 GiB high\-speed SSD PL0 40 GiB |

### Test process

|Test steps |statement |
|---|---|
|Create extension |```sql```<br>```create extension vector;```<br> |
|creating tables and indexes |```sql```<br>```create table tbl_embedding(id serial, embedding vector(1536));```<br>```-- create l2 index```<br>```create index on tbl_embedding using hnsw (embedding vector_l2_ops) with (m = 16, ef_construction = 64);```<br> |
|Create functions to generate embedding data with specified dimensions |```sql```<br>```create or replace function gen_embeddings(dim int)```<br>```    returns vector```<br>```as $$```<br>```   select array_agg(random())::vector from generate_series(1, dim)```<br>```$$```<br>```language sql```<br>```volatile```<br>```cost 1;```<br> |
|Import 100,000 data entries |```sql```<br>```-- import 100,000 records```<br>```truncate tbl_embedding;```<br>```insert into tbl_embedding(embedding) select gen_embeddings(1536) from generate_series(1, 100000);```<br>```SELECT pg_relation_size('tbl_embedding_embedding_idx');```<br> |
|pg_bench stress test SQL statement: vtest.sql |```sql```<br>```with vtemp as (select gen_embeddings(1536) as ctemp)```<br>```select id from tbl_embedding order by embedding <-> (select ctemp from vtemp) limit 40;```<br> |
|pgbench execution |```shell```<br>```PGPASSWORD=Pass_ABC123 pgbench -c 16 -P 10 -T 60 -r -n -U suser -h postgres12fc1230****.rds-pg.ivolces.com -d testdb -p 5432 -f vtest.sql```<br> |
|Import 200,000 data entries |```sql```<br>```-- import 200,000 records```<br>```truncate tbl_embedding;```<br>```drop index tbl_embedding_embedding_idx;```<br>```insert into tbl_embedding(embedding)```<br>```select gen_embeddings(1536) from  generate_series(1, 200000);```<br> |
|import 400,000 records |```sql```<br>```-- import 400,000 records```<br>```truncate tbl_embedding;```<br>```drop index tbl_embedding_embedding_idx;```<br>```insert into tbl_embedding(embedding)```<br>```select gen_embeddings(1536) from  generate_series(1, 400000);```<br> |
|import 600,000 data records |```sql```<br>```-- Import 600,000 data entries```<br>```truncate tbl_embedding;```<br>```drop index tbl_embedding_embedding_idx;```<br>```insert into tbl_embedding(embedding)```<br>```select gen_embeddings(1536) from  generate_series(1, 600000);```<br> |
|import 800,000 entries |```sql```<br>```-- Import 800,000 data entries```<br>```truncate tbl_embedding;```<br>```drop index tbl_embedding_embedding_idx;```<br>```insert into tbl_embedding(embedding)```<br>```select gen_embeddings(1536) from  generate_series(1, 800000);```<br> |
|import 1 million data entries |```sql```<br>```-- import 1 million records```<br>```Truncate tbl_embedding;```<br>```drop index tbl_embedding_embedding_idx;```<br>```insert into tbl_embedding(embedding)```<br>```select gen_embeddings(1536) from  generate_series(1, 1000000);```<br> |

### The test results are as follows.

#### pgbench performance

|Test data volume |Table data size |index data size |TPS ||latency ||
|---|---|---|---|---|---|---|
||||6 concurrency 1 thread |16 concurrent 4 threads |6 concurrency 1 thread |16 concurrent 4 threads |
|100,000 |795 MB |781 MB |1838 |2299 |3.258 ms |6.871 ms |
|200,000 |1590 MB |1562.5 MB |1683 |2503 |3.559 ms |6.329 ms |
|400,000 |3180 MB |3125 MB |1588 |2487 |3.771 ms |6.368 ms |
|600,000 |4770 MB |4687.5 MB |1564 |2538 |3.829 ms |6.254 ms |
|800,000 |6360 MB |6250 MB |1508 |2537 |3.971 ms |6.256 ms |
|1 million |7950 MB |7812.5 MB |1434 |2533 |4.176 ms |6.275 ms |

#### Impact of hnsw index and ivfflat index on TPS and latency

Impact on TPS and latency when using hnsw index and ivfflat index under single AZ one master one standby 32C64G instance, 6 concurrency 1 thread, and different data volume scenarios.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_118e9038828ddd1b47f7d83b9d030cef.png)

#### Impact of hyperparameters on TPS and latency

Impact on TPS and latency when setting different `hnsw.ef_search` values under single AZ one master one standby 32C64G instance, 600,000 data volume, and 6 concurrency 4 thread scenarios with fixed values for `m` and `ef_construction`.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5fb9495c0b32b2b89dde18c62e8d86fd.png)

## Best practices

[Building an intelligent interactive Q&A system based on RDS for PostgreSQL](https://docs.byteplus.com/en/docs/RDS_for_PG/building_an_intelligent_interactive_qa_system_based_on_pg)
