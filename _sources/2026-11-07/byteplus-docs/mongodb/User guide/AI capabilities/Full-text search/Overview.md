---
title: "Overview"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/Overview"
---

This topic introduces the full\-text search feature of Document Database for MongoDB.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Currently, MongoDB 8.3 is in the invitation\-only testing phase. To use the full\-text search feature, <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> to contact technical staff and apply for access.</div>


<span id="lqqAE0sx"></span>
## Feature introduction

Full\-text search is a search method that returns search results based on keyword text matching. Unlike vector search (based on semantic similarity), full\-text search uses tokenization and inverted index technology to perform keyword matching on text fields, supporting fuzzy matching and relevance ranking.

Document Database for MongoDB provides full\-text search capability. You can directly use the MongoDB standard aggregation query syntax (`$search`) to perform full\-text search without maintaining external search systems (such as Elasticsearch).

<span id="irtmDNXz"></span>
## Applicable scenarios

Full\-text search in Document Database for MongoDB is suitable for keyword\-based retrieval scenarios, common examples include the following:


* **Site search**

   Perform keyword searches on content such as documents, products, and articles, supporting fuzzy matching and relevance ranking.

* **Product review search**

   Search user reviews by keywords to quickly locate relevant feedback.

* **System log query**

   Search log text by keywords to quickly locate problem logs.


<span id="uAFBAie0"></span>
## Relevant documents


* [Search feature](https://docs.byteplus.com/en/docs/mongodb/Search_feature?lang=en)

* [Creating full-text index](https://docs.byteplus.com/en/docs/mongodb/create-full-text-index?lang=en)

* [Viewing full-text index](https://docs.byteplus.com/en/docs/mongodb/view-full-text-index?lang=en)

* [Deleting index](https://docs.byteplus.com/en/docs/mongodb/Deleting_index?lang=en)
