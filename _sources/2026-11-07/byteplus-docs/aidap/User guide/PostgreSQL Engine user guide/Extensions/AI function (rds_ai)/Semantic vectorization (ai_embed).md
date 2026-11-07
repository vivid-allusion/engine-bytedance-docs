---
title: "Semantic vectorization (ai_embed)"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/postgresql-rds-ai-semantic-vectorization-ai-embed"
---

1. ## Definition

`rds_ai.ai_embed` calls the registered embedding model to convert input text into a vector, which can be written to a pgvector column or used as a query vector for semantic retrieval.

2. ## Syntax

* Use the default model

```SQL
rds_ai.ai_embed(input text) RETURNS text
```

* Explicitly specify the model

```SQL
rds_ai.ai_embed(
  content text,
  model_name text,
  body_extra text DEFAULT '{}',
  header_extra text DEFAULT '{}'
) RETURNS text
```

3. ## Parameter

|**Parameter** |**Type** |**Default value** |**Decscription** |
|---|---|---|---|
|`input` / `content` |`text` |Null |Text to be vectorized. Single\-parameter overload uses default `ai_embed` model. |
|`model_name` |`text` |Null |Registered embedding model name. |
|`body_extra` |`text` |`{}` |JSON object string merged into the request body, such as `dimensions` (specifying vector dimensions). Actual support and value range depend on the target model. |
|`header_extra` |`text` |`{}` |JSON object string merged into the request header. |

4. ### Return

* `ai_embed` returns `text`, usually a vector literal convertible to pgvector, such as `[1,0,0]`.

* Single\-parameter overload returns SQL NULL when `input` is SQL NULL.

5. ## Error behavior

* An error occurs when the default model is not configured, the explicit model does not exist, or the model type is not embedding.

* An error occurs when `body_extra` or `header_extra` is not a JSON object or cannot be merged with the request template.

* An error occurs if the URL is not in the allowlist, the API Key or proxy configuration is invalid, the connection or total timeout, the HTTP status is unsuccessful, or the response is too large.

* An error occurs when the response cannot be extracted by `json_path` or token extraction expression fails.

* When converting the return value to `vector`, `halfvec`, or `sparsevec`, format or dimension mismatches will cause pgvector to throw an error.

6. ## Sample

* Generate vector using the default model

```SQL
SELECT rds_ai.ai_embed('PostgreSQL supports vector search');
```

* Specify model explicitly and convert to vector

```SQL
SELECT rds_ai.ai_embed(
  'PostgreSQL supports vector search',
  'Doc-Embed'
)::vector;
```
