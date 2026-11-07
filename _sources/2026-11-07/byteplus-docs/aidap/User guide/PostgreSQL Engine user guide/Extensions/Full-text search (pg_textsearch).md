---
title: "Full-text search (pg_textsearch)"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/pg_textsearch"
---

This topic introduces how to use the `pg_textsearch` extention to create a BM25 full\-text index and return search results by relevance.

## Function introduction

`pg_textsearch` is a full\-text search extention for PostgreSQL. The extention uses the BM25 algorithm to calculate the relevance between text and search terms, supporting sorting by relevance and returning Top\-K results.

The extention supports the following features:

* Supports creating BM25 indexes for `text`, `text[]` types, text expressions, and JSON text fields.

* Uses PostgreSQL Text Search Configuration to perform tokenization, stemming, and stop\-word processing.

* Configures tokenization methods separately for multilingual data through partial indexes.

## Prerequisites

* Workspaces created after 2026.10.19 support this extension by default. To use this extension in Workspaces created on or before 2026.10.19, restart the Target branch Compute.

* Creating the extension requires a Database account with the appropriate permissions.

* Before creating an index, select the Text Search Configuration based on the text Language. For example, English can use `english`.

* Before using Chinese word segmentation, the `pg_jieba` extension must be loaded.

## Install and uninstall extensions

### Install extension

Execute the following command in the database where full\-text search is required:

```SQL
CREATE EXTENSION pg_textsearch;
```

Execute the following command to Confirm the extension is created and View the extension version:

```SQL
SELECT extname, extversion
FROM pg_extension
WHERE extname = 'pg_textsearch';
```

Query returns `pg_textsearch` and its version number, indicating the extension has been created.

### Uninstall extension

If you have confirmed that `pg_textsearch` extension is no longer needed, you can uninstall the extension by executing the following command in the database where `pg_textsearch` is installed:

```SQL
DROP EXTENSION pg_textsearch;
```

## Create index

### Index syntax and parameters

```SQL
CREATE INDEX index_name
ON table_name USING bm25 (text_column_or_expression)
WITH (
    text_config = 'text_search_configuration',
    k1 = 1.2,
    b = 0.75
);
```

|**Parameter** |**Default value** |**Tip** |
|---|---|---|
|text_config |None, required |PostgreSQL text search configuration name determines how to perform tokenization, stemming, and stop word filtering during indexing and querying.<br><br>common values:<br><br><br>* fill in `english` for English.<br><br>* fill in `public.jiebacfg` when pairing Chinese with `pg_jieba` extention.<br><br>* fill in the corresponding tokenizer’s `schema.cfgname` for other languages or customized configurations. |
|k1 |1.2 |Word frequency saturation parameter, range 0.1~10.0. The larger the value, the more emphasis on word frequency, but the benefit gradually saturates. |
|b |0.75 |Document length normalization parameter, value range 0.0~1.0. `0` means no length normalization, `1` means complete normalization. |

`text_config` must specify a text search configuration that already exists in the current database. You can view the available configuration names with the following SQL:

```SQL
SELECT n.nspname AS schema_name, c.cfgname
FROM pg_ts_config c
JOIN pg_namespace n ON n.oid = c.cfgnamespace
ORDER BY 1, 2;
```

> **warning**

> `text_config`, `k1`, and `b` will all be written into the index metadata. Modifying these requires recreating the index. After modifying the dictionary or PostgreSQL text search configuration (Text Search Configuration), existing BM25 indexes will not automatically re\-tokenize.

### Create an index from expression results.

expression results must be `text` or `text[]` and meet PostgreSQL's immutability (IMMUTABLE) requirement for index expressions. to cover multiple columns, concatenate them into a text expression before creating an index. for queries, expressions used for scoring in ORDER BY must match the index expression:

```SQL
CREATE INDEX articles_title_body_bm25_idx
ON articles USING bm25 (
    (coalesce(title, '') || ' ' || coalesce(body, ''))
)
WITH (text_config = 'english');

SELECT id, title
FROM articles
ORDER BY (coalesce(title, '') || ' ' || coalesce(body, ''))
         <@> to_bm25query('postgres search', 'articles_title_body_bm25_idx')
LIMIT 10;
```

jsonb fields can also be indexed through expressions:

```SQL
CREATE INDEX events_description_bm25_idx
ON events USING bm25 ((data ->> 'description'))
WITH (text_config = 'english');
```

### Create text[] index

`text[]` elements are first joined by spaces into one logical document, then tokenized and scored using BM25 collectively; tokenizers are not called on each element independently. array element boundaries serve as whitespace boundary hints, suitable for large documents with application\-predefined segments such as paragraphs, titles, or message blocks, but do not guarantee each element occupies an exclusive internal chunk:

```SQL
CREATE TABLE chunked_documents (
    id bigserial PRIMARY KEY,
    content_chunks text[] NOT NULL
);

CREATE INDEX chunked_documents_bm25_idx
ON chunked_documents USING bm25 (content_chunks)
WITH (text_config = 'english');
```

### Create Chinese BM25 index

Chinese content usually requires explicitly selecting a Chinese tokenizer configuration. `pg_textsearch` determines the tokenization rules for indexing and querying through PostgreSQL text search configuration. It is recommended to use the pg_jieba extention for Chinese search and specify the `public.jiebacfg` tokenization rule when creating a BM25 index. You can use the following command to load the `pg_jieba` extention:

```SQL
CREATE EXTENSION IF NOT EXISTS pg_jieba CASCADE;
```

Create a BM25 index using `pg_jieba` as the Chinese tokenizer:

```SQL
CREATE INDEX chinese_documents_bm25_idx
ON chinese_documents USING bm25 (content)
WITH (text_config = 'public.jiebacfg');
```

## Query

### Automatic recognition index

In standard SQL, the search text can be directly written to the right of `<@>`, and the planner will automatically recognize the BM25 index based on the column or expression on the left.

```SQL
SELECT id, content
FROM documents
ORDER BY content <@> 'postgres database'
LIMIT 10;
```

The syntax of automatic recognition index querying is concise and suitable for single table, regular index, and fixed query text conventional Top\-K queries. Explicitly specify the index in the following complex scenarios:

* Partial index

* `DO`, functions, or stored procedures in PL/pgSQL

* Prepared statement or search terms come from parameters, subqueries, or other dynamic expressions

* Multiple BM25 indexes exist on the same column, requiring elimination of index selection ambiguity

* The expression is complex, or SQL needs to explicitly bind a specific index

### Explicitly specify index

```SQL
SELECT id, content
FROM documents
ORDER BY content <@> to_bm25query(
    'postgres database',
    'documents_content_bm25_idx'
)
LIMIT 10;
```

PL/pgSQL and prepared statements are recommended to always use the explicit form:

```SQL
PREPARE search_documents(text, int) AS
SELECT id, content
FROM documents
ORDER BY content <@> to_bm25query($1, 'documents_content_bm25_idx')
LIMIT $2;
```

### Score display

Since the index returns results in ascending order, the output of `<@>` is the negative BM25 score:

```SQL
SELECT id,
       content <@> to_bm25query('database', 'documents_content_bm25_idx')
           AS sort_score,
       -(content <@> to_bm25query('database', 'documents_content_bm25_idx'))
           AS bm25_score
FROM documents
ORDER BY sort_score
LIMIT 10;
```

### Chinese search

```SQL
SELECT id, content,
       content <@> '云数据库全文检索' AS score
FROM chinese_documents
ORDER BY content <@> '云数据库全文检索'
LIMIT 10;
```

The index and query must use compatible tokenization configurations

When using the `pg_jieba` extention with the default jiebacfg configuration, ASCII spaces in the query text may be parsed as extra tokens, causing unexpected recall; for Chinese search, it is recommended to write continuously or first check actual tokens with `to_tsvector('public.jiebacfg', query_text)` When Chinese, English, or other languages share the same table, it is recommended to create a `partial index` for each language and explicitly bind the corresponding language index through `to_bm25query()`.

### Partial index

Partial index only saves rows that satisfy the predicate. When using a `partial index`, the filtering condition used to create the index must be included in the query’s WHERE clause, and the index must be explicitly specified through `to_bm25query()`. For example, if the index uses `WHERE lang = 'zh'`, the query should also include `WHERE lang = 'zh'`.

Chinese content can use `public.jiebacfg` to create a language\-specific index provided that the `pg_jieba` extention is installed:

```SQL
CREATE INDEX documents_zh_bm25_idx
ON documents USING bm25 (content)
WITH (text_config = 'public.jiebacfg')
WHERE lang = 'zh';

SELECT id, content
FROM documents
WHERE lang = 'zh'
ORDER BY content <@> to_bm25query('数据库', 'documents_zh_bm25_idx')
LIMIT 10;
```

Other languages can use the corresponding PostgreSQL text search configuration to create independent indexes:

```SQL
CREATE INDEX documents_en_bm25_idx
ON documents USING bm25 (content)
WITH (text_config = 'english')
WHERE lang = 'en';

SELECT id, content
FROM documents
WHERE lang = 'en'
ORDER BY content <@> to_bm25query('database', 'documents_en_bm25_idx')
LIMIT 10;
```

## Performance tuning recommendations

### pg_textsearch.default_limit

`ORDER BY ...` `LIMIT n` is the `recommended` query form of `pg_textsearch`. When the planner can safely push down `LIMIT`, Block\-Max WAND maintains only Top\-K candidates and skips posting blocks that cannot enter Top\-K, usually greatly reducing scoring volume and significantly improving performance.

```SQL
SELECT id, content
FROM documents
ORDER BY content <@> 'database system'
LIMIT 20;
```

When the planner cannot safely push down SQL LIMIT (for example, in some Prepared Statement scenarios), the initial internal Top\-K batch size of BM25 scanning is determined by `pg_textsearch.default_limit`. Therefore, an excessively high `pg_textsearch.default_limit` may increase scoring cost and ultimately degrade query performance.

Recommendations:

* Always write explicit `LIMIT` in online Top\-K retrieval to clearly specify the maximum number of returned rows and provide conditions for Top\-K pushdown optimization.

* When the planner cannot safely push down `LIMIT`, adjust `default_limit` to a value close to the `LIMIT` commonly used by the business.

* After adjusting `default_limit`, use representative queries and `EXPLAIN (ANALYZE, BUFFERS)` to compare execution plans, query time consumption, and filtered row counts.

```SQL
SHOW pg_textsearch.default_limit;

BEGIN;
SET LOCAL pg_textsearch.default_limit = 500;

SELECT id, content
FROM documents
ORDER BY content <@> 'database system';

COMMIT;
```

If you want to modify the default for a business account, set it by role after evaluation:

```SQL
ALTER ROLE app_user SET pg_textsearch.default_limit = 500;
```

### Query writing and filtering conditions

Prioritize writing retrieval as `ORDER BY ...` `<@> ...` `LIMIT n`。 Writing only the `where` condition cannot trigger BM25 Top\-K sorting or enable Block\-Max WAND pruning according to Top\-K.

```SQL
SELECT id, content
FROM documents
ORDER BY content <@> to_bm25query('database system', 'documents_content_bm25_idx')
LIMIT 20;
```

If the query includes highly selective filter conditions, a standard B\-tree index can be created for the filter column, or a `partial index` can be created based on stable conditions. The planner might choose a B\-tree/Bitmap path to filter rows first, then calculate BM25 row by row for fewer rows and sort; this plan does not use BM25 index scan or Block\-Max WAND. The actual cost should be compared through `explain (analyze, buffers)` with BM25 index scan followed by filtering:

```SQL
CREATE INDEX documents_category_id_idx ON documents (category_id);

SELECT id, content
FROM documents
WHERE category_id = 123
ORDER BY content <@> to_bm25query('database system', 'documents_content_bm25_idx')
LIMIT 20;
```

When the filter is above the BM25 index scan, `pg_textsearch` expands the initial candidate set based on the filtering selectivity and automatically doubles the internal Top\-K and rescoring if results after filtering are insufficient until the SQL `limit` is satisfied, candidates are exhausted, or the internal limit is reached. `pg_textsearch.filtered_seed` is enabled by default, and `pg_textsearch.filtered_seed_margin` defaults to `3`. As long as there are enough matching rows, manually expanding the candidate set with subqueries is usually unnecessary; manual truncation of candidates may miss qualified results ranked after the cutoff point.

```SQL
SHOW pg_textsearch.filtered_seed;
SHOW pg_textsearch.filtered_seed_margin;

BEGIN;
SET LOCAL pg_textsearch.filtered_seed = on;
SET LOCAL pg_textsearch.filtered_seed_margin = 3;

EXPLAIN (ANALYZE, BUFFERS)
SELECT id, content
FROM documents
WHERE category_id = 123
ORDER BY content <@> to_bm25query(
    'database system', 'documents_content_bm25_idx'
)
LIMIT 20;

ROLLBACK;
```

### Tokenization configuration and document granularity

Token configuration directly affects token quantity, inverted index length, and scoring quality. Use `text_config` consistent with the data language to avoid indexing Chinese content with English configuration or mixing multilingual content in the same index for scoring. For multilingual tables, it is recommended to split Partial Index by language. See [creating a Chinese BM25 index](https://docs.byteplus.com/en/docs/330/123441#fTcodSUB) and [Chinese search](https://docs.byteplus.com/en/docs/330/123441#uwYPM79b) sections for examples in Chinese.

Extra\-large documents increase costs for single\-line tokenization, writing, and scoring. If the business naturally has boundaries like paragraphs, titles, body blocks, or message fragments, consider using `text[]` to store pre\-segmented content. `pg_textsearch` first joins array elements with spaces, then tokenizes and chunks uniformly using the same rules as ordinary `text`. Element boundaries can provide extra blank chunk hints for languages without spaces but do not independently tokenize each element or guarantee exclusive internal chunk.

## Common parameter references

View current parameter values:

```SQL
SELECT name, setting, unit, context, vartype, boot_val, reset_val
FROM pg_settings
WHERE name LIKE 'pg_textsearch.%'
ORDER BY name;
```

|**Parameter** |**Default value** |**Value range** |**Effective scope** |**Tip** |
|---|---|---|---|---|
|`pg_textsearch.default_limit` |1000 |1~100000 |User/session |when no safe pushdown SQL `LIMIT` is obtained, use as the initial internal top\-k batch size for BM25 scanning. batch size may double after exhaustion, up to a maximum of 100000. |
|`pg_textsearch.filtered_seed` |on |on / off |User/session |Estimate and expand the initial internal Top\-K based on the filter selection rate, reducing fallback recalculation of filter queries. |
|`pg_textsearch.filtered_seed_margin` |3 |1~1000 |user/session |Used to calculate the initial candidate depth for filtered queries; the larger the value, the deeper the initial scoring, which usually reduces fallback occurrences. |
|`pg_textsearch.compress_segments`<br><br> |on<br><br> |on / off |User/session |Control whether to compress posting blocks for newly generated segments. Changes only affect new segments. |
|`pg_textsearch.memtable_cache_enabled` |on<br><br> |on / off |User/session |Check whether to use shared memory to derive cache reads from memtable; after disable, it forces reading the on\-disk memtable chain, and read\-only standby instances automatically bypass the cache. |

## Limits and notes

* Phrase position matching is not natively supported yet; you can first use BM25 for over\-recall, then apply `ILIKE` or business logic for post\-filtering.

* During write peaks, index maintenance operations may cause write latency fluctuations; prioritize initial bulk data import before building the index.

* BM25 document count, average document length, and IDF statistics for partitioned tables are maintained by partition; cross\-partition scores may not share the same scoring scale.

* A single token inherits PostgreSQL `tsvector` 2047\-byte length limit; tokens exceeding this length are ignored.

* Extra\-large documents are uniformly chunked and tokenized; languages without spaces may have words cut off at internal chunk boundaries. Applications can pre\-split into `text[]` and use corresponding tokenizers; spaces inserted between array elements provide extra chunk boundary hints, but elements are still connected into a single logical document and not tokenized independently per element.

* Automatic index syntax detection does not apply to `partial index`, and explicit index names should be used in PL/pgSQL, prepared statements, and some dynamic expression scenarios.
