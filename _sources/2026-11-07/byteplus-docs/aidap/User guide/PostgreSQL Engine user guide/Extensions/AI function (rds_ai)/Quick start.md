---
title: "Quick start"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Quick_start"
---

## What problems does this topic address

* Which minimum configurations should be completed when first using rds_ai

* How to run a SQL example that can be verified successfully within minutes

* If failed, which document to prioritize for further troubleshooting

## Prerequisites

* The instance has installed `pgcrypto`; the retrieval scenario also requires `vector`

* Prepared usable model access credentials and allowed the corresponding model domain name to visit

> **tip**

> The preloaded model will not be retained automatically after new installation or upgrading from 1.3 Before the first call, it is recommended that a high\-privilege role first Execute `SELECT rds_ai.load_preset_models();`

## minimum steps

1. **create extension**: execute `CREATE EXTENSION rds_ai CASCADE;`.

2. **load preset models**: execute `SELECT rds_ai.load_preset_models();`.

3. **configure domain name whitelist**: allow the domain name where the current model endpoint is located.

4. **configure API key**: write access credentials using `rds_ai.set_apikey()`.

5. **confirm default model**: check the default model of `ai_query` using `rds_ai.get_default_model()`.

6. **initiate call**: execute a minimal `ai_query` request.

```SQL
CREATE EXTENSION rds_ai CASCADE;

SELECT rds_ai.load_preset_models();

ALTER SYSTEM SET rds.ai_domain_allowlist =
  'https://ark.cn-beijing.volces.com/';
SELECT pg_reload_conf();

SELECT rds_ai.set_apikey('ark', 'replace-with-real-api-key');
SELECT * FROM rds_ai.get_default_model();
SELECT rds_ai.ai_query('你好');
```

## success indicator

* the model corresponding to `ai_query` in `get_default_model()` is not empty.

* `ai_query` returns model text instead of default model empty, authentication failure, or network access error.

* Do not re\-explain instance\-level basic configuration when continuing to enter later ability pages.

## Minimum troubleshooting path

|**If you encounter** |**Prioritize** |
|---|---|
|Extension creation failed |[Configure and access control](https://docs.byteplus.com/en/docs/aidap/Configuration_and_access_control) → [FAQ and upgrade notes](https://docs.byteplus.com/en/docs/aidap/FAQ_and_upgrade_notes) |
|Default model is empty |[Configure and access control](https://docs.byteplus.com/en/docs/aidap/Configuration_and_access_control) |
|Domain not allowed / authentication failed |[Configure and access control](https://docs.byteplus.com/en/docs/aidap/Configuration_and_access_control) → [FAQ and upgrade notes](https://docs.byteplus.com/en/docs/aidap/FAQ_and_upgrade_notes) |
|Want to continue retrieval or RAG |[Semantic retrieval (ai_embed / ai_retrieve)](https://docs.byteplus.com/en/docs/aidap/postgresql-rds-ai-semantic-retrieval) → [Retrieval augmented generation (ai_rag)](https://docs.byteplus.com/en/docs/aidap/postgresql-rds-ai-retrieval-augmented-generation-rag) |

## Related document

* [Configure and access control](https://docs.byteplus.com/en/docs/aidap/Configuration_and_access_control)

* [Semantic generation (ai_query)](https://docs.byteplus.com/en/docs/aidap/postgresql-rds-ai-semantic-generation-ai-query)

* [FAQ and upgrade notes](https://docs.byteplus.com/en/docs/aidap/FAQ_and_upgrade_notes)
