---
title: "What is ContextSearch"
product: "ContextSearch"
product_code: "contextsearch"
source: "https://docs.byteplus.com/en/docs/contextsearch/What_is_ContextSearch"
---

Volcengine ContextSearch leverages Volcengine database’s core engine features combined with AI large model ecosystems and related capabilities to deeply transform the entire search process. It integrates data import, embedding, reranking, fusion search scoring, intent analysis, VLM, and other atomic functions to build an end\-to\-end search pipeline. It supports knowledge bases, image\-to\-image search, video search, and other scenario\-based search functions, providing more accurate and context\-relevant search and answer experiences for both structured and unstructured data.

<span id="2K6ylTqr"></span>
## Product capabilities

<span id="QUQH5udi"></span>
### Scenario\-based capabilities

<span id="Yiit5m4x"></span>
#### Knowledge base RAG

Supports semantic retrieval and completion of retrieved file content to achieve a combined “retrieval + generation” answer. The system automatically selects the most relevant document segments as context input for the large model, delivering traceable and accurate knowledge Q&A capabilities.

<span id="vynCbpU0"></span>
#### Image\-to\-image search

Based on multimodal feature extraction, supports uploading pictures for semantic similarity retrieval, matching visual features, text content (OCR), and image structure information simultaneously. Applicable to scenarios such as product matching, image asset management, and image content search.

<span id="EKiOJR7G"></span>
#### Video search

Split videos into searchable image segments and build an index. Support searching by picture, text, or both. The system returns matching video clips for easy location and playback.

<span id="kFTIF4PU"></span>
### Atomic capability

<span id="OGCUoECf"></span>
#### Embedding capability

Generate high\-quality semantic vectors for multimodal data such as text, pictures, and videos. Support multiple model options, vector index building, and batch import for high\-precision semantic recall, providing foundational support for multimodal retrieval and RAG.

<span id="ao3njxfq"></span>
#### Rerank

Support fine\-ranking of initial recall results based on reranking models by considering semantic relevance, content quality, and business rules to improve match accuracy and ensure higher\-quality top\-K returns.

<span id="oP2sEK91"></span>
#### Intent analysis

Identify user intent and semantically structure queries to understand if users want to find content, execute actions, or get guidance. Extract relevant constraints to optimize retrieval processes and result selection.

<span id="fpV4nRZ4"></span>
#### Query rewriting

Support synonym expansion, structured organization, or compression of user input to generate standardized queries better suited for retrieval, improving recall and relevance while reducing the cost of multiple input modifications by users.

<span id="qZkCqeVS"></span>
#### Document parsing

Support parsing of various document formats. For PDF, DOC, HTML, TXT, and others, it can distinguish multiple layouts and extract logical hierarchy structures such as titles and paragraphs, as well as information like text, tables, images, and code from unstructured documents, outputting in structured format.

<span id="hxeAm1DA"></span>
#### **Image parsing**

Provide image content understanding services for architecture diagrams, analysis charts, and other image data. Based on multimodal large models, it can parse and understand image content and recognize text. It also supports OCR capabilities to extract text information from images for use in image retrieval and Q&A scenarios.

<span id="nWc2nnSZ"></span>
#### Video parsing

Support video content upload and search. The system automatically extracts semantic features to achieve similarity retrieval based on video content.

<span id="t0XVSveY"></span>
#### **Document slicing**

Provide general document slicing services that segment documents based on semantics, paragraph structure, and specified rules to improve subsequent document processing and retrieval efficiency. The output slicing tree can support context completion during retrieval recall.

<span id="Ka3gvSi3"></span>
#### Online search

Support real\-time access to internet content, enabling online retrieval for the latest information. The system parses, filters, and summarizes web content, then integrates it with local search results to provide more comprehensive and timely answers.

<span id="auBcl8a1"></span>
#### **Large model summarization**

Generate summaries of retrieved documents, pictures, or video clips based on the large model, supporting long document compression, key point extraction, and structured output. Automatically generate conclusions, steps, or definitive answers by combining context and user intent, improving the readability of complex content.

<span id="amVRuEbQ"></span>
#### **VLM**

Provide cross\-modal understanding of vision and language, enabling semantic analysis of pictures and video clips, aligning them with text queries for cross\-modal search, description generation, and content comprehension.

<span id="SsOxrcn2"></span>
## **Product advantages**

<span id="V8ucDB3j"></span>
### **Native search**

Achieve unified search methods including full\-text, vector, hybrid, and multimodal by reusing the database’s own query and vector capabilities, suitable for RAG Q&A and multimodal search scenarios.

<span id="DzA2qCp0"></span>
### **Intelligent enhancement**

Completes entity tagging, intent analysis, query rewriting, and reranking based on large models, supports multiple search modes, and significantly improves search relevance and intelligence.

<span id="yJmC51Ar"></span>
### **Visualization capabilities**

Provides built\-in RAG, multimodal search process orchestration and configuration, supports Doubao large models and open\-source models (based on managed GPU and CPU), reducing the threshold for building scenario\-based search.

<span id="QquROVTg"></span>
### Ecosystem compatibility

Compatible with Elasticsearch, OpenSearch, Milvus open\-source ecosystems, and other SQL and NoSQL database ecosystems. No data migration required; enables rapid search solution deployment.

<span id="fmxyauC1"></span>
### Security and control

Supported by numerous BytePlus security features, uses enterprise\-grade API key management and access control to ensure data security and high concurrency application stability.

<span id="Ac3FvHvr"></span>
## Precautions

ContextSearch is not available to individual users. To use it, complete enterprise authentication.
