---
title: "Enhancements plugin instructions"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/enhancements_plugin_instruction"
---

opensearch\-enhancements and opendistro\-enhancements are system built\-in plugins of Cloud Search. This topic describes how to use these plugins.

<span id="0500da34"></span>
## Background


* In Elasticsearch instances, the plugin name is opendistro\-enhancements.

* In OpenSearch instances, the plugin name is opensearch\-enhancements.

* opensearch\-enhancements includes the Ngram Type field type. For usage, see [Using the Ngram-Type plugin for fuzzy queries](https://docs.byteplus.com/docs/cloudsearch/Using-ngram-type). For fuzzy search scenarios, using Wildcard wildcard query is recommended. For usage, see [Wildcard Type plugin instructions](https://docs.byteplus.com/docs/cloudsearch/Wildcard_Type_plugin_instructions).

* opendistro\-enhancements includes the Flat_Object field type. Flat_Object’s advantage is that for JSON type fields, it does not require defining types for each field. This avoids metadata inflation and simplifies user configuration. This article mainly introduces the basic usage of Flat_Object


<span id="4b4cb401"></span>
## Prerequisites

The Enhancements plugin is not installed by default. Install it in advance if needed. For installation instructions, see [Installing built-in plugins](https://docs.byteplus.com/docs/cloudsearch/manage-built-in-plugins). Currently supports Elasticsearch 7.10.2 or later and OpenSearch 2.9.0 or later.

<span id="5ca076e3"></span>
## Step 1: Set mappings

```JSON
PUT my-index
{
   "mappings": {
      "properties": {
         "issue": {
            "properties": {
               "labels": {
                  "type": "flat_object"
               }
            }
         }
      }
   }
}
```


In `labels`, the `type` is required and should be set to `flat_object`.

<span id="599eb4d1"></span>
## Step 2: Write documents

```JSON
PUT my-index/_doc/2
{
   "issue": {
      "number": 456,
      "labels": {
         "author": "Liu",
         "version": "2.1",
         "backport": [
            "2.0",
            "1.3"
         ],
         "category": {
            "type": "API",
            "level": "enhancement"
         },
         "createdDate": "2023-02-01",
         "comment": [
            [
               "Mike",
               "LGTM"
            ],
            [
               "John",
               "Approved"
            ]
         ],
         "views": 3333,
         "priority": 1.5
      }
   }
}
```


<span id="31beaea4"></span>
## Step 3: Query documents

match + path query

```JSON
POST my-index/_search
{
   "_source": true,
   "query": {
      "match": {
         "issue.labels.version": "2.1"
      }
   }
}
```


On query success, the following similar information is returned.

```JSON
{
   "took": 5251,
   "timed_out": false,
   "_shards": {
      "total": 1,
      "successful": 1,
      "skipped": 0,
      "failed": 0
   },
   "hits": {
      "total": {
         "value": 1,
         "relation": "eq"
      },
      "max_score": 0.46223074,
      "hits": [
         {
            "_index": "my-index",
            "_id": "2",
            "_score": 0.46223074,
            "_source": {
               "issue": {
                  "number": 456,
                  "labels": {
                     "author": "Liu",
                     "version": "2.1",
                     "backport": [
                        "2.0",
                        "1.3"
                     ],
                     "category": {
                        "type": "API",
                        "level": "enhancement"
                     },
                     "createdDate": "2023-02-01",
                     "comment": [
                        [
                           "Mike",
                           "LGTM"
                        ],
                        [
                           "John",
                           "Approved"
                        ]
                     ],
                     "views": 3333,
                     "priority": 1.5
                  }
               }
            }
         }
      ]
   }
}
```


match + query without path

```JSON
POST my-index/_search
{
   "_source": true,
   "query": {
      "match": {
         "issue.labels": "2.1"
      }
   }
}
```


When the query is successful, it returns information similar to the following.

```JSON
{
   "took": 117,
   "timed_out": false,
   "_shards": {
      "total": 1,
      "successful": 1,
      "skipped": 0,
      "failed": 0
   },
   "hits": {
      "total": {
         "value": 1,
         "relation": "eq"
      },
      "max_score": 0.46223074,
      "hits": [
         {
            "_index": "my-index",
            "_id": "2",
            "_score": 0.46223074,
            "_source": {
               "issue": {
                  "number": 456,
                  "labels": {
                     "author": "Liu",
                     "version": "2.1",
                     "backport": [
                        "2.0",
                        "1.3"
                     ],
                     "category": {
                        "type": "API",
                        "level": "enhancement"
                     },
                     "createdDate": "2023-02-01",
                     "comment": [
                        [
                           "Mike",
                           "LGTM"
                        ],
                        [
                           "John",
                           "Approved"
                        ]
                     ],
                     "views": 3333,
                     "priority": 1.5
                  }
               }
            }
         }
      ]
   }
}
```
