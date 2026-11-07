---
title: "Semantic generation (ai_query)"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/postgresql-rds-ai-semantic-generation-ai-query"
---

1. ## Definition

`rds_ai.ai_query` calls the registered chat model to generate and return text results based on the input text.

2. ## Syntax

* Use the default model

```SQL
rds_ai.ai_query(input text) RETURNS text
```

* Explicitly specify the model

```SQL
rds_ai.ai_query(
  content text,
  model_name text,
  body_extra text DEFAULT '{}',
  header_extra text DEFAULT '{}'
) RETURNS text
```

3. ## Parameter

|**Parameter** |**Type** |**Default value** |**Tip** |
|---|---|---|---|
|`input` |`text` |Null |Input text when using the default model. This overload is `STRICT`, SQL NULL returns SQL NULL directly. |
|`content` |`text` |Null |Input text when explicitly specifying the model. Non\-empty text is recommended. |
|`model_name` |`text` |Null |Model name registered with type `chat` or `LLM` |
|`body_extra` |`text` |`{}` |JSON object string merged into the request body; can be used to configure `temperature` (control output randomness), `max_tokens` (limit maximum output tokens), `thinking` (control model thinking mode), and other vendor parameters. Actual support and value range depend on the target model. |
|`header_extra` |`text` |`{}` |JSON object string, merged into the request header. Headers with the same name override values in the session GUC and model template. Header names are case\-insensitive. |

4. ## Return

Return `text`, which is the result extracted from the model response according to the `json_path` in the model metadata. The default model overload returns SQL NULL when `input` is SQL NULL.

5. ## Error behavior

* An error occurs when the default model is not configured, the explicit model does not exist, or the model type is incompatible.

* An error occurs when `body_extra` or `header_extra` is not a JSON object or cannot be merged with the request template.

* An error occurs if the URL is not in the allowlist, the API Key/proxy configuration is invalid, the connection or total timeout, the HTTP status is unsuccessful, or the response is too large.

* An error occurs when the response cannot be extracted by `json_path` or token extraction expression fails.

* Wait for available slots when the instance concurrency limit is reached. Requests are rejected and an error is thrown when the day/month token quota is reached.

6. ## Sample

* Use the default model

```SQL
SELECT rds_ai.ai_query('Hello world');
```

* Explicitly specify model and request parameters

```SQL
SELECT rds_ai.ai_query(
  'Hello world',
  'Doc-Chat-Model'
);
```

##
