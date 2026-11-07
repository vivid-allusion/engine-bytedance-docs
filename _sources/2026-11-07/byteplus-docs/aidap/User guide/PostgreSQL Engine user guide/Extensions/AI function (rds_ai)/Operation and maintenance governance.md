---
title: "Operation and maintenance governance"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Operation_and_maintenance_governance"
---

## Model management

* View, add, and delete models.

* Check whether the default model fully covers the function families such as chat, embedding, and rank.

* Assess compatibility, throughput, and cost differences before switching models.

### Example: Inventory models and verify default routing

**Applicable scenario:**  Before upgrading, switching models, or troubleshooting the "default model not configured" error, first confirm the model directory and default routing. The following queries are read\-only. Routing switch examples are placed in transactions and rolled back, leaving no configuration changes. Configuring the default model requires an environment privileged role or a role granted the corresponding permission.

Example: Inventory models and default routing

```SQL
SELECT model_name, model_id, model_type
FROM rds_ai.list_model()
ORDER BY model_type, model_name;

SELECT function_name, model_name
FROM rds_ai.get_default_model()
ORDER BY function_name;

BEGIN;
SELECT rds_ai.set_default_model(
  'ai_query',
  'doubao-seed-2-1-turbo-260628'
);
SELECT function_name, model_name
FROM rds_ai.get_default_model()
WHERE function_name = 'ai_query';
ROLLBACK;
```

**Typical output:**

```Plain Text
 function_name |          model_name
---------------+------------------------------
 ai_query      | doubao-seed-2-1-turbo-260628
```

**Result interpretation:**  The `list_model()` should contain the models planned for use, with types matching the function family: `chat/llm` corresponds to `ai_query`, `embedding` corresponds to `ai_embed`, and `rank` corresponds to `ai_rank`. The `model_name` in `get_default_model()` being empty means there is no default model for that function family, causing single\-parameter calls to fail.

**Abnormal troubleshooting:**  When the target model does not exist, first register the model or run preset model loading. If the type is incompatible, do not force switching but choose the correct model type. If the model name and ID conflict, first verify existing records and do not delete models currently in use.

## Token usage and quota

* Focus on token persistence statistics and cluster quota management.

* Establish usage views by model, function family, and business scenario.

* For high\-frequency tasks, add caching, rate limiting, or batch processing mechanisms on the business side.

* Token usage persistence and cross\-node quota synchronization should be standard inspection items rather than handled only after excess usage errors occur.

### Example: Configure quota and check synchronization health

**Applicable scenario:**  After changing the instance quota, confirm that the agent has accepted the configuration and determine whether the current reading comes from the cluster snapshot or local degraded statistics. `set_token_quota` modifies the instance\-level quota and must be executed by an environment\-privileged role within the change window. Example values should be replaced with actual strategies.

Example: Token quota and synchronization check

```SQL
SELECT rds_ai.set_token_quota(1000000, 30000000);

SELECT usage_scope, total_tokens, request_count, quota,
       remaining_tokens, usage_percent, cluster_usage_stale
FROM rds_ai.token_usage_day();

SELECT function_name, total_tokens, request_count
FROM rds_ai.token_usage_day_by_function()
WHERE function_name IN (
  'ai_query', 'ai_embed', 'ai_rank', 'ai_retrieve', 'ai_rag'
)
ORDER BY total_tokens DESC, function_name;

SELECT export_enabled, sync_state, quota_available,
       cluster_usage_available, last_error_code, next_retry_at
FROM rds_ai.token_usage_sync_status();
```

**Typical output:**

```Plain Text
 usage_scope | total_tokens | quota   | remaining_tokens | cluster_usage_stale
-------------+--------------+---------+------------------+--------------------
 cluster     | 125000       | 1000000 | 875000           | f

 export_enabled | sync_state | quota_available | cluster_usage_available
----------------+------------+-----------------+------------------------
 t              | healthy    | t               | t
```

**Result interpretation:**  `usage_scope = 'cluster'` and `cluster_usage_stale = false` indicate using fresh cluster snapshot; `healthy`, `quota_available = true`, and `cluster_usage_available = true` indicate normal synchronization link. A quota of `0` means unlimited. The remaining amount and percentage show `NULL` in this case.

**Abnormal troubleshooting:**  `disabled` means export is not enabled. `initializing` means the first synchronization is not complete. When `degraded`, first check the stable error code and the next retry time, then check agent reachability. The nonzero monthly quota must be greater than or equal to the daily quota. Negative values will be rejected.

## Metadata and preset models synchronization

* `load_preset_models()`: Responsible for loading platform preset models on demand.

* `load_ai_meta`: Responsible for full AI Meta synchronization.

* After version upgrades, model list abnormalities, or environment recovery, first check if these two capabilities execute normally.

### Example: Restoring preset models and safely triggering meta synchronization

**Applicable scenario:**  New installation of extension 1.4, missing preset models after version upgrades, or the platform has issued a new `rds.ai_meta_json`. Both loading functions require high permissions. Do not copy configuration values containing ciphertext into tickets or logs before execution.

Example: Preset model and platform meta synchronization

```SQL
-- idempotent: Only complete missing preset models and empty default routes
SELECT rds_ai.load_preset_models();

-- only check if configuration exists, do not display configuration content
SELECT nullif(current_setting('rds.ai_meta_json', true), '') IS NOT NULL
       AS meta_configured;

-- execute when meta_configured = true, after verifying the configuration source
SELECT rds_ai.load_ai_meta();
```

**Typical output:**

```Plain Text
 meta_configured
-----------------
 t
(1 row)
```

**Result interpretation:**  `load_preset_models()` can be executed repeatedly and does not overwrite existing non\-empty default routes. `meta_configured = false` means there is currently no platform meta; calling `load_ai_meta()` will safely make no changes. When `true`, the loader will fully verify and apply API Key, proxy, model, and default routes.

**Abnormal troubleshooting:**  JSON format, model fields, duplicate names or IDs, or any ciphertext decryption failure will cause the entire load to roll back. Fix the configuration source first after failure, then retry. Do not directly modify internal tables in `rds_ai_sys`.

## Stability governance suggestions

* Define timeout strategy, retry strategy, and downgrade path.

* Include domain name allowlist, API Key, and default model integrity in configuration inspection.

* Monitor pending/failed status of `auto embed` as separate metrics.

### Example: Complete run parameter and credential metadata inspection in one go

**Applicable scenario:**  When AI request timeout, concurrency congestion, quota synchronization abnormality, or proxy link failure occurs, first collect a configuration snapshot excluding keys and proxy passwords.

Example: Read\-only stability inspection

```SQL
SELECT name, setting, context
FROM pg_settings
WHERE name IN (
  'rds.ai_timeout_msec',
  'rds.ai_connect_timeout_msec',
  'rds.ai_max_concurrent_requests',
  'rds.ai_token_usage_export_enabled',
  'rds.ai_token_usage_export_interval_sec',
  'rds.ai_token_throttle_degraded_policy',
  'rds.ai_auto_embed_max_workers'
)
ORDER BY name;

SELECT key_name FROM rds_ai.get_apikey();
SELECT proxy_url, proxy_user FROM rds_ai.get_proxy_info();
```

**Typical output:**

```Plain Text
 name                                   | setting   | context
----------------------------------------+-----------+-----------
 rds.ai_auto_embed_max_workers          | 4         | postmaster
 rds.ai_connect_timeout_msec            | 1000      | user
 rds.ai_timeout_msec                    | 5000      | user
 rds.ai_token_throttle_degraded_policy  | fail_open | superuser
 rds.ai_token_usage_export_enabled      | on        | sighup
```

**Result interpretation:**  Parameters with `context = 'user'` can be adjusted within the session; `sighup` requires a reload after modifying the configuration; `postmaster` needs a PostgreSQL restart. `get_apikey()` returns only key_name and does not return the key. Proxy queries also do not return the password.

**Abnormal troubleshooting:**  For connection phase failures, first check connect timeout, domain name allowlist, and proxy. If the request is established but the response is slow, check the timeout and concurrency limit. If Auto Embed has no tasks executed for a long time, confirm the worker count is not 0 and cross\-check with subsequent task status queries.

## Cost governance suggestions

* Prefer task\-based functions over unnecessary general generation calls.

* Introduce caching, summary compression, and retrieval trimming for high\-frequency Q&A.

* Establish length thresholds and segmentation strategies for long text processing.

### Example: Locate the function with the highest token usage this month

**Applicable scenario:**  When quota increases rapidly, first calculate the token proportion by public function families, then return to the business side to locate high\-frequency SQL, long input, or repeated calls. Queries are read\-only; when usage is empty, proportion returns `NULL` without causing a division\-by\-zero error.

Example: Count token proportion by function this month

```SQL
WITH usage AS (
  SELECT function_name, total_tokens, request_count
  FROM rds_ai.token_usage_month_by_function()
  WHERE function_name IN (
    'ai_query', 'ai_embed', 'ai_rank', 'ai_retrieve', 'ai_rag'
  )
), totals AS (
  SELECT sum(total_tokens) AS all_tokens FROM usage
)
SELECT u.function_name, u.total_tokens, u.request_count,
       round(100.0 * u.total_tokens / NULLIF(t.all_tokens, 0), 2)
         AS token_percent
FROM usage AS u
CROSS JOIN totals AS t
ORDER BY u.total_tokens DESC, u.function_name;
```

**Typical output:**

```Plain Text
 function_name | total_tokens | request_count | token_percent
---------------+--------------+---------------+--------------
 ai_query      |      7200000 |         18000 |         72.00
 ai_embed      |      2100000 |        350000 |         21.00
 ai_rag        |       700000 |          2600 |          7.00
```

**Result interpretation:**  A high token proportion combined with low request count usually indicates overly long single inputs or outputs. A high request count and token count simultaneously usually indicate high\-frequency calls. Locate the caller by combining business logs. Do not judge specific SQLs based only on function summaries.

**Optimization suggestions:**  Prioritize compressing context and limiting output length for `ai_query`; prioritize deduplication, batch processing, and avoiding repeated vectorization for `ai_embed`; prioritize tightening recall count, slice length, and rerank scope for `ai_rag`. Observe daily usage and monthly trend continuously after adjustments.

## Typical troubleshooting order

1. Check configuration first: default model, API Key, domain name allowlist.

2. Check resources next: quota, token usage, model accessibility.

3. Finally check data and call chain: slices, recall, RAG prompt, auto embed status.

### Example: Troubleshoot auto embed accumulation or failure

**Applicable scenario:**  The source table already has text, but the vector column has been empty for a long time, or monitoring finds a backlog of Auto Embed tasks. The following queries only read public aggregate status, without exposing source text, primary key, request body, response body, or credentials.

Example: Auto embed task status

```SQL
SELECT mapping_name, target_table, text_column, vector_column,
       model_name, enabled, pending_jobs, running_jobs,
       failed_jobs, latest_error, updated_at
FROM rds_ai.list_auto_embed()
ORDER BY failed_jobs DESC, pending_jobs DESC, mapping_name;
```

**Typical output:**

```Plain Text
 mapping_name | enabled | pending_jobs | running_jobs | failed_jobs | latest_error
--------------+---------+--------------+--------------+-------------+-------------
 docs_embed   | t       |           12 |            2 |           0 |
```

**Result interpretation:**  `pending_jobs` short\-term increase with `running_jobs` greater than 0 usually indicates consumption. A continuous increase with zero running jobs requires checking worker configuration and model availability. When `failed_jobs` is greater than 0, use `latest_error` to identify whether it is a network, authentication, model response, or vector dimension issue. A query returning zero rows means no mapping has been registered yet.

**Recovery operation:**  Aafter fixing the root cause, execute `SELECT rds_ai.enqueue_auto_embed('docs_embed');` on enabled mappings to rescan rows missing vectors. To overwrite existing vectors, `true` must be explicitly passed. This operation can generate a large number of external requests and should evaluate data volume and cost first. Disabling the mapping stops new tasks from being generated but does not replace root cause investigation.

### Full diagnosis example: ai_query reports the default model is not configured

```SQL
SELECT function_name, model_name
FROM rds_ai.get_default_model()
WHERE function_name = 'ai_query';

SELECT key_name FROM rds_ai.get_apikey();

SELECT export_enabled, sync_state, last_error_code
FROM rds_ai.token_usage_sync_status();
```

If the first returns an empty model, first load the preset model or set a compatible default model. If the second returns 0 rows, configure the API Key. If the first two are normal, then check the domain name allowlist, proxy, and timeout configuration. Token sync status is used to determine whether the quota chain is healthy. It is not a sufficient condition for the model request to have succeeded.

## Related document

* [Configure and access control](https://docs.byteplus.com/en/docs/aidap/Configuration_and_access_control)

* [FAQ and upgrade notes](https://docs.byteplus.com/en/docs/aidap/FAQ_and_upgrade_notes)
