---
title: "Knowledge base quota description"
product: "VikingDB Knowledge Engine"
product_code: "RAG_Cloud"
source: "https://docs.byteplus.com/en/docs/RAG_Cloud/Knowledge_base_quota_description"
---

<span id="6544b087"></span>
## Knowledge base quota limits

> The Knowledge Base feature offers different capabilities depending on your service plan. This document provides a comprehensive reference for the quota limits, supported document types and specifications, and API rate limits for both the Pro and Standard versions. Use this guide to understand the operational boundaries and plan your implementation accordingly. To increase the quota for Pro version users, contact a Sales representative or customer service. The Standard version does not currently support quota increases.



|**Category** |**Description** |**Pro version** |**Standard version** |
|---|---|---|---|
|Number of knowledge bases |Maximum number of knowledge bases that can be created per account |200 ||
|Number of documents |Maximum number of documents that can be uploaded per knowledge base |3,000,000 |500 |
|Number of audio and video files |Maximum number of audio and video files that can be uploaded per knowledge base |1,000 |Not supported |
|Document addition API calls |Maximum number of document addition API calls supported per day |Unlimited |300 times/day |
|Slice addition/edit API calls |Maximum number of slice addition/edit API calls supported per day |Unlimited |2,000 times/day |
|Online retrievals |Maximum number of online retrievals supported per day |Unlimited |300 times/day |
|Number of slices |Maximum number of slices supported per document |100,000 ||
|CPU quota |Maximum CPU quota supported per knowledge base |100 CU |Not supported |
|QPS limit |The maximum retrieval QPS per knowledge base is proportional to its allocated CPU cores; typically, 1 CPU core supports approximately 100 QPS. |10,000 QPS maximum |1 QPS |
|Vector dimension |Maximum supported vector dimension, which depends on the selected vectorization model |4096 dimensions ||
|Vectorization model |Supported vectorization models |Multiple vectorization models are provided; for details, see [Embedding model and index algorithm comparison table](https://docs.byteplus.com/docs/209/collection_create#3d008a9c) |Only the bge\-large\-zh\-and\-m3 model is supported; model switching is not currently available |
|Maximum slice length |Maximum supported slice length, which depends on the selected vectorization model |8000 tokens ||
|Number of tags |Maximum number of tags supported per knowledge base |180 |Not supported |
|Number of retrieval tag values |Maximum number of values for a single tag per retrieval |1024 |Not supported |
|Number of documents uploaded per batch |Maximum number of documents per batch for local uploads via the frontend; for larger\-scale uploads, using TOS import is recommended. |100 ||
|Document upload and processing speed |The document processing speed for a single knowledge base depends on the size of the uploaded document and the text vectorization model. |Approximately 80,000 per day (small files) ||
|Number of items retrieved |Maximum number of text fragments supported for retrieval |1,000 ||
|Rerank API model rate limit |Maximum throughput supported by the Rerank model API |150,000 tokens/second ||


<span id="a920ca54"></span>
## Supported document types and specifications


|**Document types** |**Document formats** |**Pro version** |**Standard version** |
|---|---|---|---|
|Unstructured documents |.pdf |350 MB ||
||.doc |350 MB ||
||.docx |350 MB ||
||.pptx |200 MB ||
||.ppt |200 MB ||
||.md |10 MB ||
||.txt |10 MB ||
||.faq.xlsx |50 sheets, total number of rows in the file: 30,000 ||
||.jpeg, .png, .webp, .bmp |Single file size must not exceed 8 MB<br><br><br>* Aspect ratio (width/height): limited to the range [1/100, 100]<br><br>* Side length limited to the range [10, 6,000] pixels<br><br>> If the limit is exceeded, please change the image format and re\-upload |Not supported |
|Structured documents |.jsonl |30,000 rows, with no more than 65,535 characters per row ||
| |.csv |50 sheets, total number of rows in the file: 30,000, number of table fields: 380 ||
| |.xlsx |50 sheets, total number of rows in the file: 30,000, number of table fields: 380 ||
| |.html |350 MB ||


<span id="a8bede5f"></span>
## API rate limit description

The following API rate limits are based on **account_id** and apply to both Pro and Standard versions:


|**API** |**Rate limit** |
|---|---|
|/api/knowledge/collection/info |50 QPS |
|/api/knowledge/collection/list |50 QPS |
|/api/knowledge/doc/add |300 QPS |
|/api/knowledge/doc/info |50 QPS |
|/api/knowledge/doc/list |50 QPS |
|/api/knowledge/point/add |10 QPS |
|/api/knowledge/point/update |10 QPS |
|Other APIs |Shared rate limit 50 QPS |
