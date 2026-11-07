---
title: "Extension release note"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Extension_release_note"
---

This topic introduces the version release information of some extensions provided by the AI Native BaaS for Supabase.

## pg_textsearch

For detailed usage information about pg_textsearch, refer to [Full-text search (pg_textsearch)](https://docs.byteplus.com/en/docs/aidap/pg_textsearch).

|**Version** |**Release date** |**Updates** |
|---|---|---|
|1.4.0 |2026.10.19 |**New features**<br><br>First release of the pg_textsearch extension. |

## pgvector

For detailed usage information about pgvector, refer to [Searching based on high-dimensional vector similarity (pgvector)](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-pg_vector).

|**Version** |**Release date** |**Updates** |
|---|---|---|
|0.8.2_20260715 |2026.08.24 |**New features**<br><br><br>* Added complete lifecycle management for HNSW RaBitQ shared\-cache DSA `slot`, optimizing shared cache recycling mechanism.<br><br>* Extended the maximum dimension of `vector` and quantization types: vector upper limit increased from `16000` to `64000`, SQ8 upper limit `8000`, SQ16 upper limit `4000`, RaBitQ + fp32/none upper limit `64000`.<br><br>* Added Extended RaBitQ: HNSW and IVFFlat support `'ex4'` / `'ex8'` two reranking modes, reserving 4 / 8 bits residual encoding per dimension. The reranking source is extended encoding coexisting with 1\-bit code in the index, enabling distance reconstruction without reference to FP32, reducing heap traffic and query latency for cold/large indexes. `ex4` maximum dimension `12000`, `ex8` maximum dimension `7000`.<br><br>* Added IVFFlat bitmap\-assisted scalar pre\-filtering capability, targeting scenarios of “scalar predicate + `order by` vector distance `limit k`”. After enabling, the scalar index bitmap path first constructs the TID member set and pushes down the IVFFlat scan, filtering out unmatched candidates before vector distance calculation and reranking. |
|0.8.2_20260615 |2026.07.16 |**New features**<br><br><br>* Merged community `0.8.2` related changes.<br><br>* Added RaBitQ binary quantization indexing capability. HNSW and IVFFlat can build quantization indexes via `rabitq_enable`, supporting two refinement modes: `rabitq_refine_type='none'` and `'fp32'`.<br><br>* Added SQ8 / SQ16 scalar quantization opclass, covering HNSW and IVFFlat for L2, inner product, and cosine distance metrics. Supports int8 / int16 quantization encoding on `vector` columns to reduce index computation and storage costs.<br><br>* Added basic capability for HNSW RaBitQ cross\-backend shared scan cache by sharing RaBitQ code cache through DSM / DSA; uses backend\-local cache if sharing conditions are not met.<br><br>* Added `ivfflat.rabitq_infilter` filter\-aware scan planning. IVFFlat RaBitQ incorporates filtering judgments into candidate processing paths under safe filtering conditions to reduce invalid candidate reranking and heap fetching. |
|0.8.0 |2026.01.15 |**New features**<br><br><br>* Released the pgvector extensions to support similarity search for high\-dimensional vectors. |

## rds_ai

For detailed usage information about rds_ai, refer to [AI (rds_ai)](https://docs.byteplus.com/en/docs/aidap/rds-ai).

|**Version** |**Release date** |**Updates** |
|---|---|---|
|1.4 |2026.10.19 |**New features**<br><br><br>* Added `ai_summarize` (semantic summarization), `ai_classify` (semantic classification), and `ai_extract` (semantic extraction capabilities). |
|1.3 |2026.08.24 |**New features**<br><br><br>* Added `ai_retrieve` (semantic retrieval), `ai_rank` (text ranking), and `ai_rag` (retrieval\-augmented generation) AI functions. The` ai_rank `interface rescoring and sorting candidate texts by relevance, accompanied by separate rerank API Key management interfaces `rds_ai.set_rerank_apikey` / `rds_ai.get_rerank_apikey`.<br><br>* Preset models: Built\-in chat/embed/rank models, users can use them immediately by setting the api\-key without manually configuring add_model.<br><br>* Added call statistics `rds_ai.rds_ai_stat_detail`, enabling token usage, call count, and failed calls viewing by interface or model. |
|1.2 |2026.07.16 |**New features**<br><br><br>* Strengthened model type validation. `models[*].type` strictly requires lowercase `chat` / `embedding` to prevent model type configuration errors from the source; legacy values are only normalized for compatibility in upgrade scripts.<br><br>* Tightened the permission model for trusted extensions. Clarified the boundary between `rds_ai` (user interface) and `rds_ai_sys` (internal implementation), authorizing by usage—public execution interfaces (`ai_query` / `ai_embed` / `list_model` / `get_apikey`) are open to ordinary users; management/statistics/token interfaces are granted to environment privileged roles (Neon environment as `neon_superuser`, otherwise `pg_rds_superuser`) with grant option for delegation as needed. |
|1.1 |2026.06.20<br><br> |**New features**<br><br><br>* Added batch metadata import capability.<br><br>   * `rds.ai_meta_json` GUC parameter: centralized configuration of API Key, proxy, model list, and default model.<br><br>   * `rds_ai.load_ai_meta()`: loads JSON metadata of API Key, proxy, model list, and default model into system tables at once. |
|1.0 |2026.04.21 |**New features**<br><br><br>* Released rds_ai extension, supporting external LLM services invocation in SQL, providing two core interfaces: `rds_ai.ai_query` (text / dialogue generation) and `rds_ai.ai_embed` (vectorization). |
