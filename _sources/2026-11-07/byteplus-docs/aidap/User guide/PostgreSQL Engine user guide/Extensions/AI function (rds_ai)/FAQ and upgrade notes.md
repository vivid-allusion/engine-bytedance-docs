---
title: "FAQ and upgrade notes"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/FAQ_and_upgrade_notes"
---

## FAQ

|**phenomenon** |**Check priority** |**Recommended actions** |
|---|---|---|
|CREATE EXTENSION failed |`pgcrypto`/`vector` dependencies, `shared_preload_libraries`, and current role permissions. |Preload dependencies and preloading before recreating extensions. |
|Default model is empty |Whether `load_preset_models()` has been executed and whether the default model for the corresponding function family is set. |Reload the preset model and check the default model mapping. |
|domain not allowed |Whether `rds.ai_domain_allowlist` covers the current model endpoint. |Reload configuration after updating the allowlist. |
|quota exceeded |Token usage, quota synchronization, and short\-term high concurrent calls. |Check token usage statistics first, then adjust throttling, caching, or quota. |
|Auto embed pending for a long time |Backend processing status, default embedding model, model reachability. |View task status and verify model and network configuration. |
|RAG results are inaccurate |Text slicing, recall quality, rerank, prompt constraints. |Fix the retrieval chain first, then adjust the response generation strategy. |

## Upgrade instructions

Version 1.4 extension adds semantic summarization, semantic classification, semantic extraction, `auto embed`, persistent token usage, full Load AI Meta synchronization, and on\-demand landing of platform preset models.

## Upgrade checklist

1. After upgrading and expanding, reconfirm whether preset models have landed.

2. Check whether the default models for each function family are complete.

3. Check whether the API Key and proxy password are still valid.

4. Check whether the allowlist covers the current model endpoint.

5. If `auto embed` is enabled, check whether the historical backfill and incremental status are normal.

6. Include token usage statistics and quotas in routine inspections.

## Recommended actions after upgrade

* Fixed tasks prioritize migration to semantic summarization, semantic classification, and semantic extraction instead of continuing with general generation simulation.

* New retrieval scenarios prioritize auto\-embed\-managed vector data preparation.

* For high\-frequency invocation scenarios, establish token usage monitoring and cost governance mechanisms as soon as possible.

## Related document

* [Configure and access control](https://docs.byteplus.com/en/docs/aidap/Configuration_and_access_control)

* [Operation and maintenance governance](https://docs.byteplus.com/en/docs/aidap/Operation_and_maintenance_governance)

* [API reference](https://docs.byteplus.com/en/docs/aidap/postgresql-rds-ai-api-reference)
