---
title: "Configuration and access control"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Configuration_and_access_control"
---

## Support scope and dependencies

* Support PostgreSQL 17.

* `rds_ai` depends on `pgcrypto`; retrieval capabilities also rely on `vector`.

## Extension installation and upgrade

The following are examples of installation and upgrade:

```SQL
-- Upgrade when an old version is installed
ALTER EXTENSION rds_ai UPDATE TO '1.4';

-- Requires explicit creation at 1.4
CREATE EXTENSION rds_ai VERSION '1.4' CASCADE;
```

> **tip**

> Predefined models are managed with an on\-demand landing approach. After upgrading, it is recommended to recheck whether the Default model, API Key, and proxy password remain valid.

## Model and default model

|**Concept** |**Tip** |
|---|---|
|Model |Model: describes model ID, type, endpoint, request template, and response parsing method. |
|Default model |Different function families depend on different types of default models, for example, `ai_query` depends on chat model, `ai_embed` depends on embedding model, `ai_rank` depends on rank model. |
|Predefined models |It is recommended to run the platform predefined models first, then add customized models as needed. |

Common model management interfaces:

```SQL
SELECT rds_ai.load_preset_models();
SELECT * FROM rds_ai.list_model();
SELECT * FROM rds_ai.get_default_model();
SELECT rds_ai.set_default_model('ai_query', 'your-chat-model');
```

## API key and credential management

* Manage model access credentials using `set_apikey` / `remove_apikey`.

* Do not expose real API Key in SQL, logs, screenshots, or tickets.

* If a proxy is needed, high\-privilege roles shall configure the proxy Password and verify it again after migration or restoration.

## domain name whitelist and network restrictions

* Model calls validate `rds.ai_domain_allowlist`.

* Both preset model and Customize model endpoint domain names must be explicitly allowed.

* If switching model providers, the whitelist usually needs to be updated accordingly.

An example of whitelist configuration is as follows:

```SQL
ALTER SYSTEM SET rds.ai_domain_allowlist =
  'https://ark.cn-beijing.volces.com/';
SELECT pg_reload_conf();
```

## Role and permission boundary

* **Platform administrators** are responsible for enabling extensions, installing dependencies, configuring instance\-level allowlists, and platform policies.

* **A high\-privilege database role** manages the Model, API Key, Default Model, statistics, and rate limiting.

* **General application users** can call public AI functions, but functions like `ai_retrieve` and `ai_rag`, running with `SECURITY INVOKER`, continue to check table permissions and RLS according to the caller’s identity.

## Pre\-launch checklist

* whether the extension version is correct.

* whether the prebuilt model has been deployed.

* whether the default model is fully configured.

* whether the API Key is available.

* whether the target domain name is entered in the allowlist.

* Whether the caller has the required object permissions.

## Related document

* [Quick start](https://docs.byteplus.com/en/docs/aidap/Quick_start)

* [Operation and maintenance governance](https://docs.byteplus.com/en/docs/aidap/Operation_and_maintenance_governance)

* [API reference](https://docs.byteplus.com/en/docs/aidap/postgresql-rds-ai-api-reference)

* [FAQ and upgrade notes](https://docs.byteplus.com/en/docs/aidap/FAQ_and_upgrade_notes)
