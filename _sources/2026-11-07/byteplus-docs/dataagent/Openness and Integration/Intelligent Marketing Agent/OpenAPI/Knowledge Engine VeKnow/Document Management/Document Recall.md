---
title: "Document Recall"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/document-recall"
---

Call this interface to do semantic recall of documents in the specified knowledge base (or doc_ids) based on questions, use document meta information (overview/guide) as vector source, support multi\-channel concurrent recall and fusion, similarity threshold filtering, top_n truncation, return doc_id list and score.

# Interface description

* Interface name: retrieval_document_retrieval_post

* Interface address:/document/retrieval

* Request method: POST

# Request parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|kb_ids |Array |Yes |Knowledge Base ID List |
|doc_ids |Array |No |Optional: Limit the list of recalled document IDs; recall all documents kb_id if not transmitted |
|question |String |Yes |recall query |
|similarity_threshold |Number |No |The similarity threshold, below which documents are discarded |
|top_n |Number |No |Maximum number of documents returned |
|vector_weight |Number |No |Each vector weight, pass through to DocMetaSophonService. Recall |
|enable_overview |Boolean |No |Whether to recall the overview field, open by default |
|enable_guide |Boolean |No |Whether to recall the guide field, open by default |
|channel_fusion |String |No |Multichannel fusion mode: mean (arithmetic average, default)/max |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Object |Yes |Data, see the **data** table below for details |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|total |Number |Yes |number of documents hit |
|docs |Array |No |List of hit documents, in descending order by score, see the **docs** table below |

## docs

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|doc_id |Number |Yes |Document ID |
|file_name |String |No |file name |
|overview |String |No |Document Overview |
|guide |String |No |Document guide |
|keywords |String |No |document keywords |
|score |Number |No |Final score (after channel fusion) |
|per_channel |Object |No |The original score of each channel, the key is the channel name (overview/guide/...) |
