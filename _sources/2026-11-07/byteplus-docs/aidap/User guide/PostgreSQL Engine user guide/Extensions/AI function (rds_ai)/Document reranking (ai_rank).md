---
title: "Document reranking (ai_rank)"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/postgresql-rds-ai-text-rearrange-ai-rank"
---

1. ## Definition

`rds_ai.ai_rank` uses the registered rank model to score an array of candidate texts based on relevance to the query and returns the results sorted from high to low score, commonly used for secondary precision ranking after vector search.

2. ## Syntax

```SQL
rds_ai.ai_rank(
  query text,
  document text[],
  args jsonb DEFAULT '{}',
  model_name text DEFAULT NULL
) RETURNS TABLE(score_value double precision, text_value text)
```

3. ## Parameter

|**Parameter** |**Type** |**Default value** |**Tip** |
|---|---|---|---|
|`query` |`text` |Null |Query text for reordering, cannot be SQL NULL. |
|`document` |`text[]` |Null |The candidate text array for reranking must be one\-dimensional and contain no Null elements. If the array is empty, an empty response is returned directly. |
|`args` |`jsonb` |`{}` |Rerank parameter object, supporting only the keys `top_n` and `instruct`. `top_n` is a positive integer between 1 and 2,147,483,647 that limits the number of returns. If absent, all candidates are returned. Instruct is a string sent to the model as a rerank instruction with the request. |
|`model_name` |`text` |SQL NULL |Rank model name. It is the `ai_rank` default model if SQL Null, throwing an error when no default model is set. |

4. ## Return

* Returns `TABLE(score_value double precision, text_value text)`. `score_value` is the relevance score given by the model, and `text_value` is the corresponding original candidate text.

* Results are sorted by `score_value` from high to low. Ties are stably sorted by the original index returned by the model in ascending order, returning up to top_n entries.

* Return an empty response when `document` is an empty array.

5. ## Error behavior

* A parameter error occurs if `args` is not a JSON object, contains keys other than `top_n`/`instruct`, or the type or value of `top_n` / `instruct` is invalid.

* An error occurs if `query` is SQL NULL, or `document` is a multi\-dimensional array or contains NULL elements.

* An error occurs if the default model is not configured, `model_name` is an empty string, the model does not exist, or the type is not `rank`.

* Fall back to the global API Key if the dedicated rerank API Key is not configured. An authentication error occurs if both are missing.

* An error occurs if the rerank HTTP request is not 200, the response body is not valid JSON, `results` structure is invalid (not an array, elements not objects, `index` out of bounds/duplicate/invalid, `relevance_score` not numeric), or token extraction fails/is negative.

* Allowlist, timeout, response size, concurrency, and token quota behavior are consistent with other model calls.

6. ## Sample

* Rerank by relevance and take the top 1

```SQL
SELECT *
FROM rds_ai.ai_rank(
  'PostgreSQL 如何创建向量索引？',
  ARRAY['使用 CREATE INDEX 创建索引', 'VACUUM 用于回收空间'],
  '{"top_n":1}'::jsonb
);
```

* Call after configuring the ai_rank default model and dedicated rerank key

```SQL
SELECT rds_ai.set_default_model('ai_rank', 'qwen3-reranker-0.6b');
SELECT rds_ai.set_rerank_apikey('context-search-rerank', 'replace-with-rerank-api-key');

SELECT text_value, score_value
FROM rds_ai.ai_rank(
  '如何回收表空间？',
  ARRAY['VACUUM 用于回收空间', 'CREATE INDEX 创建索引']
);
```

##
