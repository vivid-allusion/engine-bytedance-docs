---
title: "Overview"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/PostgreSQL-rds_ai"
---

rds_ai is a database **efficient**, **easy\-to\-use**, and **secure** AI capability extension that helps developers quickly build intelligent search, knowledge Q&A, and content understanding applications based on in\-database data.

* **Efficient:**  out\-of\-the\-box support for semantic generation, vectorization, semantic retrieval, text reranking, and RAG for general scenarios, as well as semantic summarization, semantic classification, and semantic extraction for specific task scenarios, without needing to adapt each model interface separately.

* **Ease of use:**  Provides preset models, default models, and dynamic loading of metadata. Developers can configure models, call AI capabilities, and process results using familiar SQL.

* **Secure:**  unified management of keys, access permissions, and network allowlists, with concurrency control, Token usage queries, and Token rate limiting to control model call risks and costs.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5891b7ff453b3ea372bcabc39d99c353.png)

## Capability overview

|**capability** |**Semantic functions** |**Tip** |
|---|---|---|
|Semantic generation |`ai_query` |general generation entry, suitable for question answering, rewriting, polishing, translating, and lightweight reasoning. |
|Semantic vectorization |`ai_embed` |Converting text into vectors is the fundamental capability for vector storage, retrieval, and RAG |
|Semantic search |`ai_retrieve` |Use query vectors to retrieve the most relevant rows from a specified table. |
|text rearrangement |`ai_rank` |Use the rank model to rescore and reorder candidate texts based on relevance to the query, commonly used for secondary precision ranking after search |
|Retrieval augmented generation |`ai_rag` |Organize retrieval and answering into a single database\-side call, suitable for knowledge base and document Q&A. |
|Semantic summarization |`ai_summarize` |Compress long text into shorter, readable summary results. |
|Semantic classification |`ai_classify` |map text to a predefined tag set. |
|semantic extraction |`ai_extract` |Extract unstructured text into structured fields or JSON. |

## Reading order

|**if you want to do now** |**Recommended reading** |
|---|---|
|First successful run of capability |[Quick start](https://docs.byteplus.com/en/docs/aidap/Quick_start) → [Semantic generate (ai_query)](https://docs.byteplus.com/en/docs/aidap/postgresql-rds-ai-semantic-generation-ai-query) |
|Configure model, permissions, and access boundaries |[Configure and access control](https://docs.byteplus.com/en/docs/aidap/Configuration_and_access_control) |
|Generating text vectors |[Semantic vectorization (ai_embed)](https://docs.byteplus.com/en/docs/aidap/postgresql-rds-ai-semantic-vectorization-ai-embed) |
|doing retrieval or knowledge base recall |[Semantic search (ai_retrieve)](https://docs.byteplus.com/en/docs/aidap/postgresql-rds-ai-semantic-retrieval) |
|Perform secondary fine ranking on candidate texts |[Document reranking (ai_rank)](https://docs.byteplus.com/en/docs/aidap/postgresql-rds-ai-text-rearrange-ai-rank) |
|doing question\-answering rag |[Retrieval augmented generation (ai_rag)](https://docs.byteplus.com/en/docs/aidap/postgresql-rds-ai-retrieval-augmented-generation-rag) |
|Perform fixed task semantic understanding |[Semantic summarize (ai_summarize)](https://docs.byteplus.com/en/docs/aidap/postgresql-rds-ai-semantic-summary-ai-summarize) / [Semantic classify (ai_classify)](https://docs.byteplus.com/en/docs/aidap/postgresql-rds-ai-semantic-classify) / [Semantic extract (ai_extract)](https://docs.byteplus.com/en/docs/aidap/postgresql-rds-ai-semantic-extract-ai-extract) |
|View governance, quota, and model running status |[Operation and maintenance governance](https://docs.byteplus.com/en/docs/aidap/Operation_and_maintenance_governance) |
|Check signature and interface grouping |[API reference](https://docs.byteplus.com/en/docs/aidap/postgresql-rds-ai-api-reference) |
|Troubleshoot errors or perform version upgrades |[FAQ and upgrade notes](https://docs.byteplus.com/en/docs/aidap/FAQ_and_upgrade_notes) |

## Key concepts

* **Model**: describes model ID, type, endpoint, and request parsing method.

* **Default model**: Different function families depend on different types of default models. Many calls cannot run directly if missing.

* **API Key**: Model call credentials that must be managed together with model endpoints and proxy strategy.

* **allowlist**: the model endpoint domain name must enter the rds.ai_domain_allowlist to be accessed.
