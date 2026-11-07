---
title: "Wildcard Type plugin instructions"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Wildcard_Type_plugin_instructions"
---

This topic describes fundamental operations for Wildcard Type.

<span id="1fafdfc6"></span>
## Background

Wildcard Type, a variant of the Keyword type, is primarily designed to enhance the performance of regex/wildcard queries typically applied to Keyword fields. During indexing, Keyword fields are processed as complete terms, while Wildcard fields employ ngram tokenization (default N=3). That is to say, ABCD is indexed as trigrams ("ABC", "BCD"). Currently, such application also includes 1/2\-length substrings. During query processing, a similar approach is also applied. For example, a search for `test` query is executed as `tes AND est` for initial filtering, followed by exact matching.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Queries with exact matches (term/terms) on Wildcard Type will have lower performance compared to Keyword type. You should determine whether to use Wildcard Type based on actual situations.</div>


<span id="615bf099"></span>
## Supported versions

Currently supports Elasticsearch 7.10.2 or later and OpenSearch 2.9.0 or later.

<span id="6f489422"></span>
## Applicable scenarios


* The document volume is very large (e.g., hundreds of thousands, millions, or more), the field values have high cardinality (mostly unique), and queries starting with `*` will be performed.

* The field length is very large (e.g., several kilobytes or more) and wildcard or regex queries will be performed on it.


<span id="ae8378db"></span>
## Impact


* Memory usage increases compared to the Keyword type.

* Enabling doc value further improves wildcard query performance at the cost of increased storage usage.


<span id="9525e4f2"></span>
## Usage methods


1. Create an index with Wildcard field type.

   ```Java
   PUT logs
   {
     "mappings" : {
       "properties" : {
         "log_line" : {
           "type" :  "wildcard"
         }
       }
     }
   }
   ```
   

2. Perform Wildcard\-type queries on Wildcard fields.

   ```Java
   GET logs/_search
   {
     "query": {
       "wildcard": {
         "log_line": {
           "value": "k*y*fi*",
           "case_insensitive":"true",
           "boost":"2"
         }
       }
     }
   }
   ```
   

   Including:

   * `case_insensitive`: Optional. It specifies case sensitivity during matching. Default: case_sensitive.

   * `boost`: Optional. It modifies the score weight of queries.

   * `value` supports two special wildcard characters.

      * `*` matches any string with length greater than zero.

      * `?` represents any single character (length = 1).

   For more information on Wildcard, refer to [Wildcard field type](https://opensearch.org/docs/latest/field-types/supported-field-types/wildcard/) and [Wildcard query](https://opensearch.org/docs/latest/query-dsl/term/wildcard/).
