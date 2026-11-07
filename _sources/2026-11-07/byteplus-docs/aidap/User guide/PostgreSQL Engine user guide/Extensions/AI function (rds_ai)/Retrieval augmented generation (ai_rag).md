---
title: "Retrieval augmented generation (ai_rag)"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/postgresql-rds-ai-retrieval-augmented-generation-rag"
---

1. ## Definition

`rds_ai.ai_rag` sequentially executes question vectorization, vector retrieval, optional reranking, and text generation, and returns an answer based on the retrieved context.

2. ## Syntax

```SQL
rds_ai.ai_rag(
  question text,
  source_schema text,
  source_table text,
  chunk_col text,
  vector_col text,
  topn integer DEFAULT 10,
  distance_type text DEFAULT 'cosine',
  embed_model text DEFAULT NULL,
  embed_args jsonb DEFAULT '{}'::jsonb,
  prompt_model text DEFAULT NULL,
  prompt_args jsonb DEFAULT '{}'::jsonb,
  rank_model text DEFAULT NULL,
  rank_args jsonb DEFAULT '{}'::jsonb
) RETURNS text
```

3. ## Parameter

|**Parameter** |**Type** |**Default value** |**Tip** |
|---|---|---|---|
|`question` |`text` |Null |User question, cannot be SQL NULL. |
|`source_schema` |`text` |Null |Schema where the knowledge table is located. |
|`source_table` |`text` |Null |knowledge table name. |
|`chunk_col` |`text` |Null |Text columns as context. |
|`vector_col` |`text` |Null |Vector column for retrieval. |
|`topn` |`integer` |`10` |Number of candidates retrieved, must be greater than 0. |
|`distance_type` |`text` |`cosine` |`cosine`, `l2`, `l1`, or `negative`. |
|`embed_model` |`text` |SQL NULL |Embedding model. When embed_model is NULL, the `ai_embed` default model is used. |
|`embed_args` |`jsonb` |`{}` |Request body parameters passed to the embedding stage. |
|`prompt_model` |`text` |SQL NULL |The chat/LLM model for generating answers. When NULL, the `ai_query` default model is used. |
|`prompt_args` |`jsonb` |`{}` |Request body parameters passed to the answer generation stage. |
|`rank_model` |`text` |SQL NULL |Optional rerank model. Use the `ai_rank` default model if NULL. |
|`rank_args` |`jsonb` |`{}` |Parameters passed to the rerank stage. |

4. ## Return

Returns a `text` answer. If a rerank model is not provided or configured, a WARNING is issued, and answers are generated in the original vector retrieval order. This function does not return retrieved segments or distances.

5. ## Error behavior

* An error occurs when questions, schema, table names, or column names are empty; when `topn` is non\-positive; or when the distance type or any of three parameter objects are invalid.

* An error occurs when the embedding or prompt default model is missing, the explicit model does not exist, or types are incompatible. Missing available rank default models only trigger warnings and skip re\-ranking.

* The function is `SECURITY INVOKER`. An error occurs if the caller lacks source column permissions. RLS restricts the rows involved in retrieval.

* An error occurs when the vector type/dimension mismatches, table columns do not exist, model response parsing fails, or any required HTTP call fails.

* Waiting occurs when the concurrency limit is reached. Requests for the involved model are rejected when the token quota is reached.

6. ## Sample

Explicitly specify retrieval and generation models

```SQL
SELECT rds_ai.ai_rag(
  question => 'What does PostgreSQL support?',
  source_schema => 'public',
  source_table => 'rag_docs',
  chunk_col => 'content',
  vector_col => 'embedding',
  topn => 2,
  distance_type => 'cosine',
  embed_model => 'Doc-Embed-4',
  embed_args => '{}'::jsonb,
  prompt_model => 'Doc-RAG-Chat',
  prompt_args => '{"temperature":0}'::jsonb,
  rank_model => NULL,
  rank_args => '{}'::jsonb
);
```
