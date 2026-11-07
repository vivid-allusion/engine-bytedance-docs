---
title: "Semantic search (ai_retrieve)"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/postgresql-rds-ai-semantic-retrieval"
---

1. ## Definition

`rds_ai.ai_retrieve` converts the query text into a query vector, then performs similarity search on the vector column of the specified table to retrieve the most relevant rows by distance.

2. ## Syntax

* Return single text column

```SQL
rds_ai.ai_retrieve(
  question text,
  source_schema text,
  source_table text,
  chunk_col text,
  vector_col text,
  topn integer DEFAULT 10,
  distance_type text DEFAULT 'cosine',
  embed_model text DEFAULT NULL,
  embed_args jsonb DEFAULT '{}'::jsonb
) RETURNS TABLE(chunk text, distance double precision)
```

* Return JSONB composed of multiple columns

```SQL
rds_ai.ai_retrieve(
  question text,
  source jsonb,
  return_cols text[],
  options jsonb DEFAULT '{}'::jsonb
) RETURNS TABLE(payload jsonb, distance double precision)
```

3. ## Parameter

|**Parameter** |**Default value** |**Tip** |
|---|---|---|
|`question` |Null |Text for generating query vectors, which cannot be SQL NULL. |
|`source_schema` |Null |Schema of the source table. |
|`source_table` |Null |Source table name. |
|`chunk_col` |Null |Name of the returned text column. |
|`vector_col` |Null |`vector`, `halfvec`, or `sparsevec` columns used for distance calculation. |
|`topn` |10 |Maximum number of rows returned, must be greater than 0. |
|`distance_type` |`cosine` |Distance type: `cosine`, `l2`, `l1`, or `negative`. |
|`embed_model` |SQL NULL |Embedding model. If NULL, the default `ai_embed` model is parsed. |
|`embed_args` |`{}` |The JSON object of the request body passed to `ai_embed`. |
|`source` |Null |Data source object for JSONB overload, must and can only include `source_schema`, `source_table`, `chunk_col`, and `embed_col`. |
|`return_cols` |Null |Write a one\-dimensional array of non\-empty column names for the payload. No empty or duplicate columns are allowed. |
|`options` |`{}` |Only supports `topn`, `distance_type`, `embed_model`, `embed_args`, and `version`. The current `version` only supports `1.0`. |

4. ## Return

* Table overload returns `chunk text` and `distance double precision`.

* JSONB overload returns `payload jsonb` and `distance double precision`. `payload` consists of columns specified by `return_cols`.

* Results are ordered by distance from smallest to largest. `negative` uses negative inner product distance.

5. ## Error behavior

* An error occurs if the model is not configured, does not exist, is of an incompatible type, or if the embedding return value cannot be converted to the target vector type.

* A parameter error occurs if the data source object, options, topn, distance type, or return columns are invalid.

* An error occurs if the schema, table, column, pgvector extension, or corresponding distance operator does not exist.

* Both overloads are `SECURITY INVOKER`. A permission error occurs if the caller lacks `SELECT` permission on the source column. RLS restricts visible rows.

* Errors for HTTP, allowlist, timeout, response size, concurrency, and token quota propagate according to `ai_embed`'s behavior.

6. ## Sample

* Return single text column

```SQL
SELECT chunk, distance
FROM rds_ai.ai_retrieve(
  question => 'How does vector search work?',
  source_schema => 'public',
  source_table => 'doc_chunks',
  chunk_col => 'content',
  vector_col => 'embedding',
  topn => 2,
  embed_model => 'Doc-Embed'
);
```

* Return multiple business columns

```SQL
SELECT payload, distance
FROM rds_ai.ai_retrieve(
  'How does vector search work?',
  '{"source_schema":"public","source_table":"doc_chunks","chunk_col":"content","embed_col":"embedding"}'::jsonb,
  ARRAY['id', 'content'],
  '{"topn":2,"embed_model":"Doc-Embed"}'::jsonb
);
```
