---
title: "API reference"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/postgresql-rds-ai-api-reference"
---

This topic summarizes the external interfaces provided by `rds_ai`. The full definitions, parameters, returns, error behaviors, and executable examples of semantic functions are provided on the corresponding capability pages; detailed information on management, configuration, statistics, and rate limiting interfaces is available in this topic.

## Permission conventions

|Permission category |Tip |
|---|---|
|Common user interface |Semantic functions, token usage read\-only interfaces, and `get_apikey`, `get_rerank_apikey`, `get_default_model`, `list_model` functions are granted `PUBLIC` execution permission by default. |
|Delegable management API |Model, credential, default model, token quota, and Auto Embed management APIs are granted by default to high\-privilege roles in the environment, with `GRANT OPTION`. Neon environment is `neon_superuser`, other environments are `pg_rds_superuser`. |
|Superuser interface |Proxy configuration and metadata loading API default is not granted to `PUBLIC` or high\-privilege roles in the above environments. Only superusers are allowed to call. |

All runtime interfaces will refuse execution during extension upgrades. The caller must also have `EXECUTE` permission for the target function.

## Semantic functions

For API details of the following functions, refer to the corresponding subdocuments:

|Functions |Capability |API document |Version |
|---|---|---|---|
|`ai_query` |Semantic generation |[Semantic generation (ai_query)](https://docs.byteplus.com/en/docs/aidap/postgresql-rds-ai-semantic-generation-ai-query) |1.0 |
|`ai_embed` |Vector generation |[Semantic vectorization (ai_embed)](https://docs.byteplus.com/en/docs/aidap/postgresql-rds-ai-semantic-vectorization-ai-embed) |1.0 |
|`ai_retrieve` |Semantic search |[Semantic search (ai_retrieve)](https://docs.byteplus.com/en/docs/aidap/postgresql-rds-ai-semantic-retrieval) |1.3 |
|`ai_rank` |text rearrangement |[Document reranking (ai_rank)](https://docs.byteplus.com/en/docs/aidap/postgresql-rds-ai-text-rearrange-ai-rank) |1.3 |
|`ai_rag` |Retrieval augmented generation |[Retrieval augmented generation (ai_rag)](https://docs.byteplus.com/en/docs/aidap/postgresql-rds-ai-retrieval-augmented-generation-rag) |1.3 |
|`ai_summarize` |Semantic summarization |[Semantic summary (ai_summarize)](https://docs.byteplus.com/en/docs/aidap/postgresql-rds-ai-semantic-summary-ai-summarize) |1.4 |
|`ai_classify` |Semantic classification |[Semantic classification (ai_classify)](https://docs.byteplus.com/en/docs/aidap/postgresql-rds-ai-semantic-classify) |1.4 |
|`ai_extract` |Semantic extraction |[Semantic extraction (ai_extract)](https://docs.byteplus.com/en/docs/aidap/postgresql-rds-ai-semantic-extract-ai-extract) |1.4 |

## Model management interface

### Definition

The model management interface handles registering, querying, and deleting model metadata, as well as limiting the allowed HTTP response size for a single model.

### Syntax

```SQL
rds_ai.add_model(
  model_id text, model_name text, base_url text, model_type text,
  text_template text, json_path text DEFAULT '', token_path text DEFAULT ''
) RETURNS void

rds_ai.list_model()
RETURNS TABLE(
  model_name text, model_id text, model_type text, request_type text,
  request_header rds_ai_sys.http_header[], url text, content_type text,
  text_template text, json_path text, token_path text, max_response_size int
)

rds_ai.remove_model(model_name text) RETURNS void

rds_ai.set_max_response_size(
  model_name_v text, max_response_size_v int
) RETURNS void

rds_ai.load_preset_models() RETURNS void
```

### Parameter

|API |Parameter description |
|---|---|
|`add_model` |`model_id` is the server\-side model ID; `model_name` is the unique name within the database; `base_url` is the endpoint; `model_type` supports `chat`, `llm`, `embedding`, `rank`; `text_template` accepts model ID and input text as two `format()` parameters; `json_path` and `token_path` are SQL templates using the response text as parameters. |
|`list_model` |No parameter. |
|`remove_model` |`model_name`: model name to delete in the database. |
|`set_max_response_size` |`model_name_v`: model name; `max_response_size_v`: maximum allowed bytes for response header and body. `0` means unlimited. |
|`load_preset_models` |No parameter. |

### Return

`add_model`, `remove_model`, `set_max_response_size`, and `load_preset_models` return `void` on success. `list_model` returns all model configurations, including request templates and response extraction templates, but excludes API keys. `load_preset_models` can be called repeatedly, only supplementing missing preset models and default bindings without overwriting existing non\-NULL default bindings.

### Error behavior

* `add_model` throws an error when the required parameter of SQL NULL, name or ID conflict, model type is invalid; the write is transactional atomicity.

* `remove_model` or `set_max_response_size` throws an error if the model is not found. An error occurs if the response size is less than `0`.

* `load_preset_models` refuses execution during extension upgrades. Permission errors are thrown by PostgreSQL if privileges are insufficient.

### Sample

```SQL
SELECT rds_ai.add_model(
  'example-model-id',
  'example-chat-model',
  'https://example.com/v1/chat/completions',
  'chat',
  '{"model":"%s","messages":[{"role":"user","content":"%s"}]}',
  'SELECT %L::jsonb->''choices''->0->''message''->>''content''',
  'SELECT (%L::jsonb->''usage''->>''total_tokens'')::int'
);

SELECT * FROM rds_ai.list_model() ORDER BY model_name;
SELECT rds_ai.set_max_response_size('example-chat-model', 16777216);
SELECT rds_ai.remove_model('example-chat-model');
SELECT rds_ai.load_preset_models();
```

## API Key interface

### Definition

Global API Key is used for general model requests. A dedicated rerank API Key is preferred for `ai_rank` and RAG reranking and falls back to the global API Key if not configured.

### Syntax

```SQL
rds_ai.set_apikey(key_name text, api_key text) RETURNS void
rds_ai.get_apikey() RETURNS TABLE(key_name text)
rds_ai.set_rerank_apikey(key_name text, api_key text) RETURNS void
rds_ai.get_rerank_apikey() RETURNS TABLE(key_name text)
```

### Parameter

|API |Parameter description |
|---|---|
|`set_apikey` |`key_name` is the credential name, `api_key` is the global key to be encrypted and saved. The new value overwrites the existing single credential. |
|`get_apikey` |No parameter. |
|`set_rerank_apikey` |`key_name` is the credential name, and `api_key` is the re\-rank key to be encrypted and saved. New values overwrite existing single credentials. |
|`get_rerank_apikey` |No parameter. |

### Return

Both setters return `void` upon success. Both getters return zero or one row of `key_name`, exposing only non\-sensitive names without returning plaintext or ciphertext keys. Getter returns zero rows when there is no configuration.

### Error behavior

Setter throws error when the parameter is SQL NULL, API Key length reaches or exceeds 4,096 bytes, encryption environment identifier is missing, extension is upgrading, or permissions are insufficient. Getter does not report error if credentials are not configured.

Currently version 1.4 does not have a `remove_apikey` interface. Calling setter again will overwrite the original credentials.

### Sample

```SQL
SELECT rds_ai.set_apikey('ark', 'replace-with-api-key');
SELECT * FROM rds_ai.get_apikey();

SELECT rds_ai.set_rerank_apikey(
  'context-search-rerank',
  'replace-with-rerank-api-key'
);
SELECT * FROM rds_ai.get_rerank_apikey();
```

## Proxy interface

### Definition

The proxy interface maintains an instance\-level HTTP proxy configuration. The password is stored encrypted and is not returned through query interfaces.

### Syntax

```SQL
rds_ai.set_proxy(
  proxy_url text,
  proxy_user text DEFAULT NULL,
  proxy_pwd text DEFAULT NULL
) RETURNS void

rds_ai.unset_proxy() RETURNS void

rds_ai.get_proxy_info()
RETURNS TABLE(proxy_url text, proxy_user text)
```

### Parameter

|API |Parameter description |
|---|---|
|`set_proxy` |`proxy_url` must start with `http://`; `proxy_user` and `proxy_pwd` can be omitted, but if a password is provided, the username must also be provided. |
|`unset_proxy` |No parameter. |
|`get_proxy_info` |No parameter. |

### Return

`set_proxy` and `unset_proxy` return `void` on success. The latter succeeds even if executed repeatedly. `get_proxy_info` returns zero or one row with `proxy_url` and `proxy_user`, without returning the proxy password. It returns zero rows if no configuration exists.

### Error behavior

An error occurs when URL is empty, protocol is invalid, URL reaches 2,048 bytes, user name reaches 512 bytes, password reaches 4,096 bytes, password is provided without user name, extension is upgrading, or permissions are insufficient.

### Sample

```SQL
SELECT rds_ai.set_proxy(
  'http://127.0.0.1:58889',
  'proxy-user',
  'replace-with-proxy-password'
);
SELECT * FROM rds_ai.get_proxy_info();
SELECT rds_ai.unset_proxy();
```

## Default model interface

### Definition

The default model interface maintains default routing for `ai_query`, `ai_embed`, and `ai_rank`.

### Syntax

```SQL
rds_ai.set_default_model(
  p_function_name rds_ai_sys.ai_function_type,
  p_model_name text
) RETURNS void

rds_ai.get_default_model()
RETURNS TABLE(
  function_name rds_ai_sys.ai_function_type,
  model_name text
)
```

### Parameter

* `p_function_name` can only be `ai_query`, `ai_embed`, or `ai_rank`.

* `p_model_name` is the registered and compatible model name. Passing SQL NULL clears the default binding for this function.

### return

`set_default_model` returns `void` on success. `get_default_model` always returns three rows in the order of the three functions above. `model_name` is SQL NULL when unbound.

### Error behavior

An error occurs when the function name is SQL NULL, the model does not exist, the model type is incompatible, permission is insufficient, or during extension upgrades.

### Sample

```SQL
SELECT rds_ai.set_default_model(
  'ai_query',
  'doubao-seed-2-1-turbo-260628'
);
SELECT * FROM rds_ai.get_default_model();
SELECT rds_ai.set_default_model('ai_query', NULL);
```

## Metadata loading interface

### Definition

The metadata loading interface imports the model configuration in the instance GUC into the extension directory and can only be executed by the superuser by default.

### Syntax

```SQL
rds_ai.load_ai_meta() RETURNS void
rds_ai.load_default_models(
  set_default boolean DEFAULT true
) RETURNS void
```

### Parameter

|API |Input |
|---|---|
|`load_ai_meta` |No function parameters. It reads `rds.ai_meta_json`, and supports `api_key`, `rerank_api_key`, `proxy`, `models`, and `default_models`. |
|`load_default_models` |`set_default` defaults to `true`. It reads the compatible parameter rds.`default_model_meta_json`, and sets query/embed default model when `true`. |

### Return

Both interfaces return `void` on success. When the configuration is empty, success returns immediately. `load_ai_meta` atomic application applies all changes this time. Compatible format `load_default_models` does not support `ai_rank` default model.

### Error behavior

An error occurs when JSON structure, field type, or model type is invalid, ciphertext cannot be decrypted, model name or ID conflicts, default model type is incompatible, `set_default` is SQL NULL, insufficient permissions, or during extension upgrade. All changes in a single call roll back with the transaction.

### Sample

```SQL
SELECT rds_ai.load_ai_meta();
SELECT rds_ai.load_default_models();
SELECT rds_ai.load_default_models(set_default => false);
```

## Token usage and quota interface

### Definition

The token usage interface provides cluster or local usage by Asia/Shanghai billing cycle, detailed by function and synchronous healthy status, and atomically updates day/month quotas through the management interface.

### Syntax

```SQL
rds_ai.set_token_quota(
  day_quota bigint, month_quota bigint
) RETURNS void

rds_ai.token_usage_day()
RETURNS TABLE(
  period_start timestamptz, period_end timestamptz, usage_scope text,
  total_tokens bigint, request_count bigint, quota bigint,
  remaining_tokens bigint, usage_percent numeric,
  cluster_snapshot_at timestamptz, cluster_usage_stale boolean
)

rds_ai.token_usage_month()
RETURNS TABLE(
  period_start timestamptz, period_end timestamptz, usage_scope text,
  total_tokens bigint, request_count bigint, quota bigint,
  remaining_tokens bigint, usage_percent numeric,
  cluster_snapshot_at timestamptz, cluster_usage_stale boolean
)

rds_ai.token_usage_day_by_function()
RETURNS TABLE(
  period_start timestamptz, period_end timestamptz, function_name text,
  total_tokens bigint, request_count bigint
)

rds_ai.token_usage_month_by_function()
RETURNS TABLE(
  period_start timestamptz, period_end timestamptz, function_name text,
  total_tokens bigint, request_count bigint
)

rds_ai.token_usage_sync_status()
RETURNS TABLE(
  export_enabled boolean, sync_state text, quota_available boolean,
  cluster_usage_available boolean, last_success_at timestamptz,
  last_failure_at timestamptz, last_error_code text,
  next_retry_at timestamptz
)
```

### Parameter

|API |Parameter |Tip |
|---|---|---|
|`set_token_quota` |`day_quota`, `month_quota` |Both quotas must be greater than or equal to 0. A non\-zero monthly quota must be greater than or equal to the daily quota. Confirmed `0, 0` means day/month unlimited. |
|5 read\-only interfaces |Null |Read the current shared status without modifying metering, quota, or sync checkpoint. |

### Return

|API |Return and behavior |
|---|---|
|`set_token_quota` |Return `void` after successfully synchronizing the agent and installing the new configuration version returned by the agent. |
|`token_usage_day` / `token_usage_month` |Return one row of summary for the current Asia/Shanghai day/month on the billing period. `usage_scope='cluster'` means a fresh agent cluster snapshot plus unconfirmed local increments; otherwise `local`. When quota is unknown or unlimited, `remaining_tokens` and `usage_percent` are SQL NULL. |
|`token_usage_day_by_function` / `token_usage_month_by_function` |Return six AI interfaces per line in a stable order, including zero\-usage interfaces. Each line contains the billing interval, function name, token usage, and request count. |
|`token_usage_sync_status` |Return one row of desensitized status. `sync_state` is `disabled`, `initializing`, `healthy`, or `degraded`. Agent URL, response body, generation, or checkpoint are not exposed. |

### Error behavior

`set_token_quota` throws an Error when encountering negative values, nonzero monthly quotas less than daily quotas, during expansion upgrade, or insufficient permission. When agent is unavailable, rejects requests, or returns invalid content, it throws a `token quota synchronization failed: <stable error code>` error, and does not install unconfirmed local quotas. The read\-only interface throws a precondition status error when expansion is not preloaded or shared status is unavailable.

### Sample

```SQL
-- Requires an environment high-privilege role or delegated EXECUTE permission.
SELECT rds_ai.set_token_quota(1000000, 30000000);

-- The following 5 read APIs are default accessible by ordinary users.
SELECT * FROM rds_ai.token_usage_day();
SELECT * FROM rds_ai.token_usage_month();
SELECT * FROM rds_ai.token_usage_day_by_function();
SELECT * FROM rds_ai.token_usage_month_by_function();
SELECT * FROM rds_ai.token_usage_sync_status();
```

## GUC parameter configuration

|Parameter |Context |Default value |Tip |
|---|---|---|---|
|`rds.ai_domain_allowlist` |`SUSET` |Empty |Model URL prefix allowlist. It rejects calls if empty or unmatched. |
|`rds.ai_timeout_msec` |`USERSET` |`5000` |HTTP total timeout in milliseconds. |
|`rds.ai_connect_timeout_msec` |`USERSET` |`1000` |HTTP connection timeout, in milliseconds. |
|`rds.ai_max_concurrent_requests` |`SIGHUP` |`0` |Maximum HTTP request concurrency for instance\-shared models. `0` means unlimited. |
|`rds.ai_extra_body_params` |`USERSET` |`{}` |JSON object merged into the query/embed request body. Keys with the same name in function parameters take priority. |
|`rds.ai_extra_headers` |`USERSET` |`{}` |Additional HTTP request headers. Function parameters override GUC, and GUC overrides the model template. |
|`rds.ai_rag_query_rewrite` |`USERSET` |`off` |Enable retrieval question rewriting for `ai_rag`. Enabling calls LLM one extra time. |
|`rds.ai_rag_dynamic_truncate_topn` |`USERSET` |`on` |Dynamically trim low\-relevance context based on reranking score cliffs, while retaining at least the first 5 items. |
|`rds.ai_rag_ushape_char_threshold` |`USERSET` |`32768` |Enable U\-shape arrangement when the total number of characters in the reordered context reaches this value. The range is 0 to 2,147,483,647. |
|`rds.ai_rag_rank_score_threshold` |`USERSET` |`0.5` |Accept the minimum upper limit of the rearranged order score, ranging from 0 to 1. Revert to the original vector retrieval order if it is below this value. |
|`rds.ai_token_usage_export_enabled` |`SIGHUP` |`off` |Whether to asynchronously export token usage to the local agent and receive cluster snapshots and quotas. |
|`rds.ai_token_usage_agent_address` |`POSTMASTER` |Platform related |Local agent base URL; Neon default `http://169.254.254.253:29001`, RDS PG default `http://127.0.0.1:8888`. Do not append `/token_usage/v1/heartbeat`. Restart is required after modification. |
|`rds.ai_token_usage_export_interval_sec` |`SIGHUP` |`200` |Token usage export attempt interval, range: 200 to 600 seconds. After missing 3 consecutive intervals, the cluster snapshot is considered expired. |
|`rds.ai_token_throttle_degraded_policy` |`SUSET` |`fail_open` |Policy when cluster usage is unavailable for executing quota: `fail_open` or `fail_closed`. |
|`rds.ai_meta_json` |`SUSET` |Empty |General AI metadata JSON, imported by `load_ai_meta()`. |
|`rds.default_model_meta_json` |`SUSET` |Empty |The legacy default model array format imported by `load_default_models()`. |

Ark attribution\-related `rds.ai_ark_client_request_id` and `rds.ai_ark_domain_name` are compile\-time fixed read\-only parameters. Only SHOW is supported, and they cannot be modified via SET or configuration files. For more deployment and permission details, refer to [Configuration and access control](https://docs.byteplus.com/en/docs/aidap/Configuration_and_access_control).

## Related document

* [Configuration and access control](https://docs.byteplus.com/en/docs/aidap/Configuration_and_access_control)

* [Operation and maintenance governance](https://docs.byteplus.com/en/docs/aidap/Operation_and_maintenance_governance)

* [FAQ and upgrade notes](https://docs.byteplus.com/en/docs/aidap/FAQ_and_upgrade_notes)
