---
title: "Using the Ngram-Type plugin for fuzzy queries"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Using-ngram-type"
---

opendistro\-ngram\-type is a built\-in plugin of Cloud Search. In fuzzy search scenarios, we recommend that you run wildcard queries by using the Ngram approach, which can find matches at any position in a string. This topic describes how to use the opendistro\-ngram\-type plugin.

<span id="843ffa0b"></span>
## Before you begin

The opendistro\-ngram\-type plugin is not installed by default. If you want to use the plugin, install it in advance. For more information, refer to [Installing built-in plugins](https://docs.byteplus.com/en/docs/cloudsearch/built-in-plugins).

<span id="4c9fdbb3"></span>
## Step 1: Configure mappings

```HTTP
PUT my-index
{
  "mappings": {
    "properties": {
      "my_doc": {
        "type": "ngram",
        "ignore_above":300,
        "null_value": "value1"
      }
    }
  }
}
```



* type: required. Set the field type to **ngram**.

* ignore_above: optional. This parameter specifies the maximum character length of a field. Fields exceeding this length limit cannot be indexed. In this example, the length limit is 300, which indicates that the system does not create indices for fields that contain more than 300 characters.

* null_value: optional. If the value of a field is empty, the field cannot be indexed and queried. In this example, the value is set to value1, which means that if the value of a field is null, value1 is used when the system creates the index.


<span id="93e76397"></span>
## Step 2: Write data to a document

```HTTP
PUT my-index/_doc/1
{
  "my_doc" : "This string can be quite lengthy"
}
```


<span id="3cff08dc"></span>
## Step 3: Query the document

```SQL
GET my-index/_search
{
  "query": {
    "wildcard": {
      "my_doc": {
        "value": "*quite*lengthy",
        "case_insensitive":"true",
        "boost":"1"
      }
    }
  }
}
```



* When the opendistro\-ngram\-type plugin is used, **the system currently supports only wildcard query operators**.

* value: required. This parameter specifies the content of the fuzzy search.

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The following two special wildcard characters can be included in the content of the fuzzy search:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>*</code>: represents any string whose length is greater than 0.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>?</code>: represents any string whose length is greater than 1.   </div>
   

* case_insensitive: optional. This parameter specifies whether to enable case\-sensitive matching. The default value is false, which specifies that case\-sensitive matching is enabled.

* boost: optional. This parameter adjusts the relevance score of the query. The default value is 1.


If the query is successful, information similar to the following is returned:

```JSON
{
  "took" : 180,
  "timed_out" : false,
  "_shards" : {
    "total" : 1,
    "successful" : 1,
    "skipped" : 0,
    "failed" : 0
  },
  "hits" : {
    "total" : {
      "value" : 1,
      "relation" : "eq"
    },
    "max_score" : 9.0,
    "hits" : [
      {
        "_index" : "my-index",
        "_type" : "_doc",
        "_id" : "1",
        "_score" : 9.0,
        "_source" : {
          "my_doc" : "This string can be quite lengthy"
        }
      }
    ]
  }
}
```
