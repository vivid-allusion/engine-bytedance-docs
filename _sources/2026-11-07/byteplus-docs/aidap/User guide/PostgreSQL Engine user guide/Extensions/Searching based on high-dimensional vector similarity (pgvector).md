---
title: "Searching based on high-dimensional vector similarity (pgvector)"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/PostgreSQL-pg_vector"
---

## About pgvector

pgvector is an extension that provides efficient similarity search capabilities for high\-dimensional vectors. It includes the following features:

* supports vector data types that can store and query vector data.

* supports precise and approximate nearest neighbor search (ANN). Supported distance or similarity metrics include Euclidean distance (L2 norm Euclidean Distance), Manhattan distance (L1 Manhattan Distance), cosine similarity, and inner product.

* Supports creating vectors with up to 64,000 dimensions and indexing vectors with up to 64,000 dimensions.

* Supports quantized indexes (scalar quantization and RaBitQ), achieving lower memory usage and faster search speeds by reducing vector storage precision while maintaining high recall rates.

   > **tip**

   > Quantized indexing capability is only available in version 0.8.2.

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

### Extension release note

For the functions provided by pgvector in different versions, refer to the [Extension release note](https://docs.byteplus.com/en/docs/aidap/Extension_release_note#tLivqMBu).

### Upgrade the extension

The following command upgrades the pgvector extension to the latest version.

```SQL
ALTER EXTENSION vector UPDATE;
```

> **tip**

> If your workspace was created on or after 2026.07.17, the default vector extension version is 0.8.2, so no manual upgrade is needed.

> If your workspace was created before 2026.07.17, you can only use version 0.8.0 of the extension. If you need to use version 0.8.2 of the vector extension in these workspaces, please [submit a ticket](https://console.byteplus.com/workorder/create) to contact us for workspace upgrade, then execute the above command to upgrade the vector extension.

### Delete extension

```sql
drop extension vector;
```

## Data type

pgvector provides three vector data types (the following examples are based on the vector type).

|Type |Comment |Max supported dimension |maximum index build dimension |supported indexes |
|---|---|---|---|---|
|vector |Represents 32\-bit floating\-point vectors |* Extension version 0.8.2_20260615 and earlier: 16000.<br><br>* Extension version 0.8.2_20260715 and later: 64000.<br><br><br> |* Extension versions 0.8.2_20260615 and earlier: 2000.<br><br>* Extension version 0.8.2_20260715 and later versions:<br><br>   * RaBitQ none/fp32: 64000<br><br>   * RaBitQ ex4: 12000<br><br>   * RaBitQ ex8: 7000<br><br>   * SQ8: 8000<br><br>   * SQ16: 4000 |btree, ivfflat, hnsw |
|halfvec |Represents a 16\-bit floating point vector |16000 |4000 |btree, ivfflat, hnsw |
|sparsevec |Represents sparse vector, input format is `{index1:value1,index2:value2}/dimensions` |1000000000 (non\-zero dimension 16000) |nonzero dimension 1000 |btree, hnsw |

> **tip**

> The maximum dimension for building an index depends on the quantization type. The 64000\-dimensional index is only applicable to vector + RaBitQ none/fp32. The normal HNSW/IVFFlat supports 2000 dimensions, RaBitQ ex4 supports 12000 dimensions, RaBitQ ex8 supports 7000 dimensions, SQ8 supports 8000 dimensions, and SQ16 supports 4000 dimensions.

### Insert&Select

```sql
create table tbl_vector (tc1 vector(3),  tc2 halfvec(3), tc3 sparsevec(3));
insert into tbl_vector values ('[1,2,3]', '[1,2,3]', '{2:1}/3');
select * from tbl_vector;
```

## Vector operators

pgvector extension implements 14 operators for vector types.

> **warning**

* > Two vectors operated on by operators must have the same dimension.

* > For convenience, pgvector normalizes the results of Euclidean distance, Manhattan distance, cosine similarity, and inner product operations: the smaller the result, the higher the similarity between the two vectors involved.

* > Manhattan distance (L1) ANN is only supported by native HNSW index; IVFFlat, SQ8/SQ16, and RaBitQ ANN do not support L1.

|Operators |Decscription |Examples |
|---|---|---|
|<\-\> |L2 Euclidean distance calculation |select tc1 <\-\> '[1,1,1]' as euclidean_distance from tbl_vector order by euclidean_distance ; |
|<#\> |Negative inner product calculation |SELECT tc1 <#\> '[1,1,1]' AS nagative_inner_product FROM tbl_vector ORDER BY nagative_inner_product; |
|<=\> |Cosine distance calculation |SELECT tc1 <=\> '[1,1,1]' AS cosine_distance FROM tbl_vector ORDER BY cosine_distance; |
|+ |add |select tc1 + '[1,1,1]' from tbl_vector; |
|\- |minus |select tc1 \- '[1,1,1]' from tbl_vector; |
|< |Less than |select \* from tbl_vector where tc1 < '[1,1,1]' ; |
|<= |Less than or equal to |select \* from tbl_vector where tc1 <= '[1,1,1]' ; |
|= |= |select \* from tbl_vector where tc1 = '[1,1,1]' ; |
|<\> |Not equal to |select \* from tbl_vector where tc1 <\> '[1,1,1]' ; |
|\>= |Greater than or equal to |select \* from tbl_vector where tc1 \>= '[1,1,1]' ; |
|\> |greater than |select \* from tbl_vector where tc1 \> '[1,1,1]' ; |
|\* |Element\-wise multiplication |select tc1 \* '[2,2,2]' from tbl_vector; |
|<+\> |Calculate Manhattan distance on L1 |select tc1 <+\> '[1,1,1]' from tbl_vector; |
|\|\| |Vector concatenation |select tc1 \|\| '[1,1,1]' from tbl_vector; |

## Index

Usually, the number of vector entries (rows) stored in a single table can reach hundreds of millions. To speed up access to vector type data and similarity calculation, pgvector provides three index types: btree index, ivfflat index, and hnsw index.

Since version 0.8.2, pgvector has added support for quantized indexes, including scalar quantization (SQ8, SQ16) and binary quantization (RaBitQ). Quantized indexes reduce memory usage and accelerate retrieval by lowering the vector storage precision, suitable for large\-scale vector search scenarios with some tolerance for recall accuracy.

### Create index

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

   * > The ivfflat index core is used for KNN ORDER BY. Queries can include regular WHERE filters; distance expressions can also be written as boolean conditions, but the ivfflat opclass itself does not act as a regular WHERE predicate index.

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

   * > hnsw index core is used for KNN ORDER BY. Queries can include regular WHERE filters; the distance expression can also be written as a boolean condition, but the hnsw opclass itself does not serve as a regular WHERE predicate index.

* Create btree index

   ```sql
   drop table tbl_vector;
   create table tbl_vector(id serial, tc1 vector(100));
   insert into tbl_vector (tc1)  select array_agg(random())::vector(100) from generate_series(1.0,100.0) ;
   create index on tbl_vector (tc1);
   ```

   > **tip**

   * > Do not use btree indexes of vector type for ANN/KNN similarity search.

   * > When creating a btree index, under the current 8KB page configuration, vectors with dimensions less than or equal to 672 can be indexed; dimensions of 673 and above exceed the size limit for a single btree index record.

   * > In practice, it is recommended to keep the vector dimension for creating btree index at 500 or below to prevent issues such as decreased index scan efficiency due to toast access.

* Check the current build progress of the index

   > **tip**

   > This feature is available only in pgvector instances version 0.6.2 and above.;

   ```sql
   vtest=# SELECT phase, round(100.0 * blocks_done / nullif(blocks_total, 0), 1) AS "%" FROM pg_stat_progress_create_index;
                phase              |  %
   --------------------------------+-----
    building index: loading tuples | 8.6
   (1 row)
   ```

## Using quantized index

Pgvector 0.8.2 introduces quantized index features, supporting the following two quantization Types:

* **Scalar quantization**: compresses original 32\-bit floating\-point vectors into 8\-bit (SQ8) or 16\-bit (SQ16) integer representations, significantly reducing index memory usage and improving search speed while maintaining a high recall rate.

* **Binary quantization (RaBitQ)** : binarize vectors to binary representation, achieving minimal memory usage and fastest retrieval speed through extreme compression. RaBitQ also supports IVFFlat in\-filter mode for conditional filtering during index scanning.

Quantized indexes apply to the following scenarios:

* The large volume of vector data and limited memory resources require reducing the memory usage of indexes.

* For those sensitive to search latency and willing to trade some recall accuracy for faster search speed.

* Requires high throughput ANN search on large datasets.

### Prerequisites

Before using quantized indexes, confirm the following conditions:

|**Condition** |**Decscription** |
|---|---|
|Workspace version |Workspaces created on or after 2026.07.17, or workspaces created before 2026.07.17 but upgraded by submitting a ticket. |
|Extension version |Upgrade the extension to version 0.8.2 |
|Account privileges |Extension upgrade and index create actions require execution with a high\-privilege account. |

### Use scalar quantization (SQ8/SQ16)

Scalar quantization reduces index memory by compressing 32\-bit float vectors into low\-precision integers (8\-bit or 16\-bit). SQ8 and SQ16 both support L2 Euclidean distance, inner product, and cosine similarity calculations.

#### Create SQ8 quantization index

Use HNSW index combined with SQ8 quantization:

```SQL
-- Create test table;
CREATE TABLE tbl_sq_test(id serial, embedding vector(1536));

-- Insert test data
INSERT INTO tbl_sq_test (embedding)
  SELECT array_agg(random())::vector(1536)
  FROM generate_series(1, 1536) AS g1, generate_series(1, 10000) AS g2
  GROUP BY g2;

-- Create SQ8 quantized HNSW index (L2 distance)
CREATE INDEX idx_sq8_l2 ON tbl_sq_test USING hnsw (embedding sq8_vector_l2_ops);

-- Create SQ8 quantized HNSW index (cosine distance)
CREATE INDEX idx_sq8_cosine ON tbl_sq_test USING hnsw (embedding sq8_vector_cosine_ops);

-- Create SQ8 quantized HNSW index (inner product)
CREATE INDEX idx_sq8_ip ON tbl_sq_test USING hnsw (embedding sq8_vector_ip_ops);
```

Query using SQ8 quantized index:

> The vector queried in the example is pseudocode; replace it with the complete 1536\-dimensional vector for actual queries.

```SQL
-- l2 distance query
SELECT id FROM tbl_sq_test ORDER BY embedding <->'[1,2,3,...,1536]' LIMIT 10;
 
-- Cosine distance query
SELECT id FROM tbl_sq_test ORDER BY embedding <=> '[1,2,3,...,1536]' LIMIT 10; 

-- Negative inner product query
SELECT id FROM tbl_sq_test ORDER BY embedding <#> '[1,2,3,...,1536]' LIMIT 10; 
```

#### Create an SQ16 quantized index

The use of SQ16 quantization is similar to SQ8, with precision between SQ8 and the original 32\-bit float:

```SQL
-- Create SQ16 quantized HNSW index (cosine distance)
CREATE INDEX ON tbl_sq_test USING hnsw (embedding sq16_vector_cosine_ops);

-- Create SQ16 quantized IVF index (inner product)
CREATE INDEX ON tbl_sq_test USING ivfflat (embedding sq16_vector_ip_ops) WITH (lists = 1000);
```

Query using SQ16 quantized index:

> The vector queried in the example is pseudocode; replace it with the complete 1536\-dimensional vector for actual queries.

```SQL
-- L2 distance query
SELECT id FROM tbl_sq_test ORDER BY  embedding <-> '[0.1, 0.2, ...]'  LIMIT 10;

-- Cosine distance query
SELECT id FROM tbl_sq_test ORDER BY  embedding <=> '[0.1, 0.2, ...]'  LIMIT 10;

-- Negative inner product query
SELECT id FROM tbl_sq_test ORDER BY  embedding <#> '[0.1, 0.2, ...]'  LIMIT 10;
```

### Use binary quantization (RaBitQ)

RaBitQ is an efficient binary quantization method that achieves extreme compression by binarizing vectors into compact binary representations. RaBitQ supports L2 Euclidean distance, inner product, and cosine similarity distance calculations. Enable it via the index parameter `rabitq_enable=true`.

#### Refine

The RaBitQ quantized search process is a 1\-bit coarse ranking + fine ranking to achieve high recall rate. Currently supports 4 refine types: `none`, `fp32`, `ex4`, `ex8`. The following is a detailed explanation:

|**Rerank type** |**Description** |**Index size** |**Index parameters** |
|---|---|---|---|
|none |Only rough sorting, no fine sorting; recall rate is low but speed is fastest |Small |`rabitq_refine_type = 'none'` |
|fp32 |Rough ranking is followed by precise ranking through returning to the table to query the original vector (fp32). Its advantage is saving space, and its disadvantage is extra lookup overhead. |Small |`rabitq_refine_type = 'fp32'`<br><br> |
|ex4<br><br>> **tip**<br><br><br>> Only extension version 0.8.2_20260715 and later support this.<br> |Store an additional 4\-bit ex_code in the index, with precise ranking performed by ex_code after coarse ranking. The speed is faster than fp32 but uses extra index space. |Medium |`rabitq_refine_type = 'ex4'` |
|ex8<br><br>> **tip**<br><br><br>> Only extension version 0.8.2_20260715 and later support this.<br> |The index additionally stores an 8\-bit ex_code; after coarse ranking, precise ranking is performed using the ex_code. The speed is faster than fp32 but uses more additional index space. |Big |`rabitq_refine_type = 'ex8'`<br><br> |

#### Create RaBitQ quantized index

> **warning**

> Using RabitQ quantization algorithm requires data in the table; RabitQ IVFFlat can be built on an empty table but will use random centroids, resulting in reduced recall. Using RabitQ quantization algorithm requires data in the table; suitable for large data volumes. It is recommended to create RabitQ index after the table contains more than 10,000 entries.

**Prepare the test table and data:**

```SQL
DROP TABLE IF EXISTS items CASCADE;

CREATE TABLE items (
  id serial,
  embedding vector(1536)
);

INSERT INTO items (embedding)
SELECT array_agg(random() ORDER BY d)::vector(1536)
FROM generate_series(1, 1536) AS d
CROSS JOIN generate_series(1, 10000) AS g
GROUP BY g;
```

**Create RabitQ quantized index:**

```SQL
-- HNSW + RaBitQ, default fp32 fine-tuning (recommended starting configuration)
CREATE INDEX ON items USING hnsw (embedding vector_l2_ops)
  WITH (rabitq_enable = true);  

-- Create non-refined sorting index, recall rate generally over 80%
CREATE INDEX ON items USING hnsw (embedding vector_l2_ops)
  WITH (rabitq_enable = true, rabitq_refine_type = 'none'); 
  
 -- Create fp32 fine-tuning index, with a recall rate above 90%
 CREATE INDEX ON items USING hnsw (embedding vector_cosine_ops)
   WITH (m = 16, ef_construction = 128,
            rabitq_enable = true, rabitq_refine_type = 'fp32',
            rabitq_nc = 16);
                    
  -- Create ex4 fine-tuning index, with a recall rate above 90%
  CREATE INDEX ON items USING hnsw (embedding vector_cosine_ops)
    WITH (m = 16, ef_construction = 128,
              rabitq_enable = true, rabitq_refine_type = 'ex4',
              rabitq_nc = 16);    
              
   -- Create ex8 refined sorting index, recall rate can reach over 90%
   CREATE INDEX items_embedding_ivf_ex_idx
   ON items USING ivfflat (embedding vector_l2_ops)
   WITH (
     lists = 1000,
     rabitq_enable = true,  
     rabitq_refine_type = 'ex8'
     );
     
   -- IVFFlat + RaBitQ, l2 distance
   CREATE INDEX ON items USING ivfflat (embedding vector_l2_ops)
     WITH (lists = 1000, rabitq_enable = true, rabitq_refine_type = 'fp32');
     
   -- IVFFlat + RaBitQ, cosine distance
   CREATE INDEX ON items USING ivfflat (embedding vector_cosine_ops)
     WITH (lists = 1000, rabitq_enable = true);
```

**Query using RaBitQ quantized index:**

> The vector queried in the example is pseudocode; replace it with the complete 1536\-dimensional vector for actual queries.

```SQL
-- Query: operators must match operator classes (use <-> for l2, <=> for cosine, <#> for negative inner product)
SET hnsw.ef_search = 170;
SELECT id FROM items ORDER BY embedding <-> '[0.1, 0.2, ...]' LIMIT 10;
```

#### Use IVFFlat in\-filter

IVFFlat in\-filter function is limited to RaBitQ quantization. This function allows conditional filtering during IVFFlat RaBitQ index scanning to optimize approximate nearest neighbor search performance under high filter rates.

**Create IVFFlat + RaBitQ index**

```SQL
-- Create a test table with scalar filter columns
CREATE TABLE tbl_rabitq_filter (
    id serial,
    category int,
    embedding vector(1536)
);

-- Insert test data
INSERT INTO tbl_rabitq_filter (category, embedding)
SELECT
    (random() * 10)::int,
    array_agg(random() ORDER BY d)::vector(1536)
FROM generate_series(1, 100000) AS g
CROSS JOIN generate_series(1, 1536) AS d
GROUP BY g;

-- Create IVFFlat + RaBitQ index (L2 distance)
CREATE INDEX idx_rabitq_ivfflat
ON tbl_rabitq_filter
USING ivfflat (embedding vector_l2_ops)
WITH (lists = 100, rabitq_enable = true);
```

**Use in\-filter to optimize conditional approximate nearest neighbor queries**

> The vector queried in the example is pseudocode; replace it with the complete 1536\-dimensional vector for actual queries.

```SQL
-- Configure IVFFlat in-filter parameters
SET ivfflat.probes = 10;
SET ivfflat.rabitq_infilter = on;

-- Ann query with filter conditions
SELECT id, category
FROM tbl_rabitq_filter
WHERE category = 5
ORDER BY embedding <-> '[1,2,3,...,1536]'::vector
LIMIT 10;
```

#### Using IVFFlat pre\-filter

IVFFlat pre\-filter function supports RaBitQ quantization / native IVF index use (0.8.2_20260715 and later versions). This function allows conditional filtering before IVFFlat KNN search, optimizing approximate nearest neighbor search performance under high filtering conditions.

**Use pre\-filter to optimize approximate nearest neighbor queries with conditions**

> **tip**

* > The vector queried in the example is pseudocode; replace it with the complete 1536\-dimensional vector for actual queries.

* > When using pre\-filter, the filter condition must have an available scalar index to generate Bitmap Index Scan.

```SQL
-- Configure IVFFlat pre-filter parameters
SET ivfflat.probes = 10;
SET ivfflat.prefilter = on;

-- Ann query with filter conditions
SELECT id, category
FROM tbl_rabitq_filter
WHERE category = 5
ORDER BY embedding <-> '[1,2,3,...,1536]'::vector
LIMIT 10;
```

**Explain example**

```SQL
Custom Scan (VectorPrefilterScan) on tbl_rabitq_filter
  -> Index Scan using idx_rabitq_ivfflat 
  -> Bitmap Index Scan using idx_rabitq_category
```

### Quantized index parameter description

The following is a summary of functions and parameters related to quantized indexes.

|**Parameter** |**When to use** |**Default** |**Range / values** |**Scope** |**Tip** |
|---|---|---|---|---|---|
|`rabitq_enable` |Specify when creating the index, used during insert. |false |true / false |hnsw, ivfflat |Enable RaBitQ binary quantization.<br><br> |
|`rabitq_refine_type` |Specified when creating the index. |fp32 |none / fp32/ ex4 / ex8 |hnsw, ivfflat<br><br> |RabitQ precise ranking strategy. none = no precise ranking, fp32 = true distance precise ranking, ex4/ex8 = 4/8\-bit extended RabitQ. |
|`rabitq_rerank_in_table`<br><br> |Specified during create index. |true<br><br> |true / false<br><br> |ivfflat only |rabitq_rerank_in_table = true means fp32 rerank fetches the original vector from the heap during table lookup, resulting in a smaller index but with table lookup overhead. |
|`rabitq.enabled_by_default`<br><br> |GUC specified by SET before query; not CREATE INDEX reloption. |off<br><br> |on / off |hnsw, ivfflat |When enabled, if the user does not specify a quantization type, the RabitQ quantization index is created by default.<br><br>> **tip**<br><br><br>> Supported from version 0.8.2_20260715 and later.<br> |
|`rabitq_nc` |Specified when creating the index and used during insert. |16 |1 – 256 |only hnsw |Global number of centroids; |
|`rabitq.query_bits` |Specified during query. |8 |1 – 8 |hnsw, ivfflat |Query quantization precision; the higher it is, the higher the recall, with a slight decrease in throughput. |
|`rabitq.epsilon`<br><br> |Specified during query. |1.9 |0.0 – 4.0 |hnsw, ivfflat |Lazy precise ranking error bound multiplier; the larger it is, the looser, more candidates are collected, and the higher the recall |

Summary of distance operators (opclass) supported by each quantization method:

|**Quantization method** |**L2 distance** |**Cosine similarity** |**Inner product (dot product)**  |
|---|---|---|---|
|SQ8 |`sq8_vector_l2_ops` |`sq8_vector_cosine_ops` |`sq8_vector_ip_ops` |
|SQ16 |`sq16_vector_l2_ops` |`sq16_vector_cosine_ops` |`sq16_vector_ip_ops` |
|RaBitQ |`vector_l2_ops + rabitq_enable=true` |`vector_cosine_ops + rabitq_enable=true` |`vector_ip_ops + rabitq_enable=true` |

> **tip**

> Scalar quantization (SQ8/SQ16) and binary quantization (RaBitQ) do not support approximate nearest neighbor Search based on Manhattan distance (L1 Manhattan Distance).

### rabitq_last_scan_stats() function

`rabitq_last_scan_stats()` function provides statistics of the most recent RaBitQ index scan, helping users evaluate index scan efficiency and recall quality.

> **tip**

* > `rabitq.track_scan_stats` default disable; statistics results will not be displayed when disabled.

* > Returns the last completed RaBitQ scan from the most recent SQL on the current connection; returns an empty result if no RaBitQ scan occurred in the last SQL.

**Return field description**

|**Field** |**Type** |**Description** |
|---|---|---|
|indexname |text |Index name used for this scan, excluding schema. |
|am |text |Index access method, with values `hnsw` or `ivfflat`. |
|mode |text |RaBitQ scan mode:<br><br><br>* `rabitq_approx` indicates using approximate distance only.<br><br>* `rabitq_refined` means that fp32, ex4, or ex8 refined sort is enabled. |
|candidates_scanned |bigint |Number scanned and entered candidate processing during coarse ranking phase.<br><br><br>* Number of nodes accessed at layer 0 in HNSW.<br><br>* Number of valid candidates passing pre\-filtering in IVFFlat. |
|candidates_refined |bigint |Number of candidates extracted from the candidate set for exact distance calculation attempts. |
|heap_fetches |bigint |RaBitQ heap tuple acquisition count during fine ranking or built\-in filtering process. |
|limit_hit |boolean |Whether to stop scanning topk results due to internal restrictions, equivalent to `limit_cause <> 'none'`. |
|limit_cause |text |Stop reason:<br><br><br>* `none`: No internal limitations caused the scan to stop.<br><br>* `scan_tuples`: The number of HNSW elements visited at level 0 has reached hnsw.max_scan_tuples.<br><br>* `mem`: HNSW scan temporary memory exceeds the allowed value: work_mem × hnsw.scan_mem_multiplier.<br><br>* `probe_limit`: All allowed inverted lists (ivfflat.probes) for the current query have been fully scanned. |
|nodes_visited |bigint |* HNSW total nodes visited, including upper\-level navigation and layer 0.<br><br>* `0` in IVFFlat. |
|probes_visited |bigint |* Actual number of probe/list accesses for IVFFlat.<br><br>* `0` for HNSW. |
|bounded_pool_used |boolean |* IVFFlat indicates whether the candidate pool with capacity limit is actually used.<br><br>* `false` in HNSW. |
|pool_capacity |bigint |IVFFlat bounded candidate pool capacity; records the maximum capacity used during multiple scans. `0` when unused. |
|pool_replacements |bigint |The number of times the IVFFlat candidate pool, once full, replaces the worst candidate with a better new candidate. |
|pool_rejections |bigint |Number of times new candidates were rejected after the IVFFlat bounded candidate pool was full because they were not good enough. |
|pool_shortfall_replay |boolean |When IVFFlat bounded pool candidates are exhausted but more results are needed, whether the same probes are rescanned unbounded |
|work_mem_fallback |boolean |Whether IVFFlat switched to spillable tuplesort/unbounded storage path due to work_mem memory limit (insufficient work_mem causing use of temporary files and performance degradation). |
|adjacency_pool_used |boolean |HNSW RaBitQ shared\-cache adjacency pool hit; non\-HNSW shared\-cache adjacency path is false. |
|adjacency_epoch_mismatch |boolean |Whether to fallback to regular adjacency reading when HNSW adjacency pool epoch mismatches. |
|adjacency_fallbacks |bigint |HNSW adjacency pool misses or fallbacks count. |

**Examples**

> The vector queried in the example is pseudocode; replace it with the complete 1536\-dimensional vector for actual queries.

```SQL
SET rabitq.track_scan_stats = on;

SELECT id
FROM items
ORDER BY embedding <-> $$[1,2,3]$$::vector
LIMIT 10;

SELECT * FROM rabitq_last_scan_stats();
```

## Index parameters

### ivfflat index parameters

The following parameters are used respectively for ivfflat index creation and index scan:

   |**Parameter** |**When to use** |**Default** |**Range** |**Decscription** |
   |---|---|---|---|---|
   |`lists` |Specify when creating an index. |100<br><br> |1 – 32768 |Indicates the number of lists the dataset in the index is divided into. The larger this value, the faster the query efficiency. The lists value should not be too large; for vectors in the tens of millions, it is recommended to set it below 2000. |
   |`ivfflat.probes` |Specified during query, used for index scanning. |1 |1 – lists |Number of lists searched during this index scan. The larger this value, the more lists are scanned in search, resulting in a higher recall, but the index scan efficiency decreases. |
   |`ivfflat.iterative_scan` |Specified during query, used for index scanning. |off |off / relaxed_order |If set to "relaxed_order", the index scan range expands during queries, achieving higher recall at the cost of more time. |
   |`ivfflat.max_probes` |Specified during query, used for index scanning. |32768 |1 – 32768 |Maximum number of lists scanned when querying IVF index. Effective when `ivfflat.iterative_scan` is set to "relaxed_order". |
   |`ivfflat.prefilter`<br><br>> **tip**<br><br><br>> Supported in version 0.8.2_20260715 and later.<br> |Specified during query, used for index scanning. |off |on / off |Enable pre\-filter mode for IVFFlat index, allowing WHERE condition filtering before index scanning. |
   |`ivfflat.prefilter_max_candidate_ratio`<br><br>> **tip**<br><br><br>> Supported in 0.8.2_20260715 and later versions.<br> |Specified during query and used in index scan. |0.30 |0.0 – 1.0 |Upper limit of the scalar candidate ratio allowed in pre\-filter. |
   |`ivfflat.prefilter_max_membership_mem`<br><br>> **tip**<br><br><br>> Supported in version 0.8.2_20260715 and later.<br> |Specified during query, used for index scanning. |0 KB (using work_Memory) |0 – MAX_KILOBYTES |pre\-filter membership Memory budget, disabled Later pre\-filter when exceeded.<br><br> |
   |`ivfflat.rabitq_infilter`<br><br>> **tip**<br><br><br>> Supported from version 0.8.2_20260615 and later.<br> |Specified during query, used for index scanning. |off |on / off<br><br> |Enable in\-filter mode for IVFFlat index, allowing WHERE condition filtering during index scanning. Only supported by RaBitQ. |
   |`ivfflat.rabitq_refine_ratio`<br><br>> **tip**<br><br><br>> Supported from version 0.8.2_20260615 and later.<br> |Specified during query, used for index scanning. |3.0 |1.0 – 1000.0 |Enable `ivfflat.rabitq_bounded_pool` limits IVF pure vector LIMIT queries to ratio × LIMIT_K candidates at most. |
   |`ivfflat.rabitq_bounded_pool`<br><br>> **tip**<br><br><br>> Supported from version 0.8.2_20260615 and later.<br> |Specified during query, used for index scanning. |on |on / off<br><br> |Whether to use a bounded candidate pool for IVF pure vector LIMIT query. Enabling reduces the number of candidates entering the final ranking, thus improving throughput. |

### hnsw index parameters

The following parameters are used for hnsw index creation and scanning:

   |**Name** |**When to use** |**Default** |**Range** |**Description** |
   |---|---|---|---|---|
   |`m` |Specified when creating indexes, used during insert |16 |2 \- 100 |Indicates the number of connections each point needs to establish with other points in the graph. Generally, the larger the m, the higher the recall rate, but the greater the memory consumption. |
   |`ef_construction` specified during query, used during index scan. |Specified when creating indexes, used during insert |64 |4 \- 1000 |Represents the size of the dynamic candidate set during index building. ef_construction must be greater than or equal to 2 \* m, typically set to twice the value of m. |
   |`hnsw.ef_search` |Specified during query, used for index scanning. |40 |1 \- 1000 |Usually the larger the hnsw.ef_search, the higher the search accuracy, but the longer the time consumed. |
   |`hnsw.iterative_scan` |Specified during query, used for index scanning. |off |off / relaxed_order/ strict_order |If set to "relaxed_order" or "strict_order", the index scan range expands during queries. |
   |`hnsw.max_scan_tuples` |Specified during query, used for index scanning. |20000 |1\-INT_MAX |Limits the maximum tuple quantity accessed during index scan expansion. |
   |`hnsw.scan_mem_multiplier` |Specified during query, used for index scanning. |1 |1 \- 1000 |It sets the multiplier for work_mem used during extended index scans. |
   |`hnsw.prefetch_neighbors`<br><br> |Specified during query, used for index scanning. |on |on / off |Prefetch neighbor pages during search. |

   The following three parameters can be used to speed up hnsw index building:

   |Name |Description |
   |---|---|
   |`max_parallel_workers` |set the system's maximum parallel process quantity, default value is 8. |
   |`max_parallel_maintenance_workers` |Sets the maximum number of parallel workers for a single utility command (such as CREATE INDEX). |
   |`maintenance_work_mem` |specifies the maximum memory used for maintenance actions (such as VACUUM, create index). |

## Examples

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

## Aggregate functions

The pgvector extension provides two aggregate functions for vector types: `avg()` and `sum()`.

*  `avg()` function calculates the average value of each dimension of a vector. The usage is shown in the example below:

   ```sql
   drop table tbl_vector ;
   create table tbl_vector(id serial, tc1 vector(5));
   insert into tbl_vector (tc1)  select array_agg(random())::vector(5) from generate_series(1.0,5.0) ;
   
   select avg(tc1) from tbl_vector;
   select id, avg(tc1) from tbl_vector group by id;
   ```

* `sum()` function sums each dimension of the vector. The usage is shown in the example below:

   ```sql
   insert into tbl_vector (tc1)  select array_agg(random())::vector(5) from generate_series(1.0,5.0) ;
   select sum(tc1) from tbl_vector;
   select id, sum(tc1) from tbl_vector group by id;
   ```

## Data type conversion

The pgvector extension provides conversions between vector types and several array types.

|**convert type** |**Examples** |
|---|---|
|convert vector to vector |```sql```<br>```select '[0.802642,0.339995,0.440122,0.476725,0.449537]'::vector;```<br> |
|convert vector to real[] |```sql```<br>```select vector('[0.802642,0.339995,0.440122,0.476725,0.449537]')::real[];```<br> |
|convert real[ ] to vector |```sql```<br>```select '{0.802642,0.339995,0.440122,0.476725,0.449537}'::real[]::vector;```<br> |
|convert int4[ ] to vector |```sql```<br>```select '{1,2,3,4,5}'::int4[]::vector;```<br> |
|Convert double precision[ ] to vector |```sql```<br>```select '{0.864488503430039,0.798674516845495,0.90717526525259,0.756084795109928,0.639521076343954}'::double precision[]::vector;```<br> |
|convert numeric[ ] to vector |```sql```<br>```select '{0.864488503430039,0.798674516845495,0.90717526525259,0.756084795109928,0.639521076343954}'::numeric[]::vector;```<br> |

## Introduction to pgvector vector operation performance

In vectorization scenarios, a typical case is storing embeddings vectors processed by large language models (LLM), such as [text-embedding-ada-002](https://platform.openai.com/docs/guides/embeddings), with a fixed dimension of 1,536, and calculating their similarity. This topic references this scenario to verify the impact of different data volumes, thread counts, concurrency levels, indexes, and parameter values on the database TPS and latency.

### test parameter

|test parameter ||
|---|---|
|test concurrency |6/16 |
|Number of test threads |1/4 |
|test time |60s |
|PostgreSQL instance specification |single AZ with one primary and one standby 32C64G |
|client specification |32 vCPU 128 GiB high\-speed SSD PL0 40 GiB |

### Test process

|Test steps |Statement |
|---|---|
|Create extension |```sql```<br>```create extension vector;```<br> |
|creating tables and indexes |```sql```<br>```create table tbl_embedding(id serial, embedding vector(1536));```<br>```-- create l2 index```<br>```create index on tbl_embedding using hnsw (embedding vector_l2_ops) with (m = 16, ef_construction = 64);```<br> |
|Create functions to generate embedding data with specified dimensions |```sql```<br>```create or replace function gen_embeddings(dim int)```<br>```    returns vector```<br>```as $$```<br>```   select array_agg(random())::vector from generate_series(1, dim)```<br>```$$```<br>```language sql```<br>```volatile```<br>```cost 1;```<br> |
|Import 100,000 data entries |```sql```<br>```-- import 100,000 records```<br>```truncate tbl_embedding;```<br>```insert into tbl_embedding(embedding) select gen_embeddings(1536) from generate_series(1, 100000);```<br>```SELECT pg_relation_size('tbl_embedding_embedding_idx');```<br> |
|pg_bench stress test SQL statement: vtest.sql |```sql```<br>```with vtemp as (select gen_embeddings(1536) as ctemp)```<br>```select id from tbl_embedding order by embedding <-> (select ctemp from vtemp) limit 40;```<br> |
|pgbench execution |```shell```<br>```PGPASSWORD=<your-password> pgbench -c 16 -P 10 -T 60 -r -n -U suser -h postgres12fc1230****.rds-pg.ivolces.com -d testdb -p 5432 -f vtest.sql```<br> |
|Import 200,000 data entries |```sql```<br>```-- import 200,000 records```<br>```truncate tbl_embedding;```<br>```drop index tbl_embedding_embedding_idx;```<br>```insert into tbl_embedding(embedding)```<br>```select gen_embeddings(1536) from  generate_series(1, 200000);```<br> |
|import 400,000 records |```sql```<br>```-- import 400,000 records```<br>```truncate tbl_embedding;```<br>```drop index tbl_embedding_embedding_idx;```<br>```insert into tbl_embedding(embedding)```<br>```select gen_embeddings(1536) from  generate_series(1, 400000);```<br> |
|Import 600,000 data records |```sql```<br>```-- Import 600,000 data entries```<br>```truncate tbl_embedding;```<br>```drop index tbl_embedding_embedding_idx;```<br>```insert into tbl_embedding(embedding)```<br>```select gen_embeddings(1536) from  generate_series(1, 600000);```<br> |
|import 800,000 entries |```sql```<br>```-- Import 800,000 data entries```<br>```truncate tbl_embedding;```<br>```drop index tbl_embedding_embedding_idx;```<br>```insert into tbl_embedding(embedding)```<br>```select gen_embeddings(1536) from  generate_series(1, 800000);```<br> |
|import 1 million data entries |```sql```<br>```-- import 1 million records```<br>```Truncate tbl_embedding;```<br>```drop index tbl_embedding_embedding_idx;```<br>```insert into tbl_embedding(embedding)```<br>```select gen_embeddings(1536) from  generate_series(1, 1000000);```<br> |

### The test results are as follows.

#### pgbench performance

|Test data volume |Table data size |index data size |TPS ||latency ||
|---|---|---|---|---|---|---|
||||6 concurrency 1 thread |16 concurrency 4 threads |6 concurrency 1 thread |16 concurrency 4 threads |
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

## pgvector quantization performance introduction

* Test specifications: Intel Xeon Platinum 8336C, 16c64g specifications, 32GB shared_buffers

* Test benchmark: VectorDBBench, 50K \- 10M data sets, TopK=100

### 1536D / 50K / COSINE

![](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0ed8f7a15bb2c38ad82aaef4b62fbc22.png)

### 768D / 1M / COSINE

![](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_33081fc70dae72a4e3bf0891fcbbc2fa.png)

### 1536D / 5M / COSINE

![](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ce99a6bb83cba2171737902fc36f7d92.png)

### 768D / 10M / COSINE

![](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c5e8742d4d78584e8060ed74c9042d53.png)
