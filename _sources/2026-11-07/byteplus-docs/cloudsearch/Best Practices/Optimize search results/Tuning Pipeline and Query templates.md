---
title: "Tuning Pipeline and Query templates"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Tuning_Pipeline_and_Query_templates"
---

You may encounter unexpected query results during testing and production. To address scenarios where tuning search performance is difficult, Cloud Search provides multiple tuning strategies. This article describes how to use Pipeline and Query templates for tuning.

<span id="ee6e2bf2"></span>
## Set semantic weights for a Pipeline

In a hybrid search, the weights for semantic retrieval and full\-text matching are configured through the search pipeline. To modify them, update the original pipeline configuration in dev_tools or through an API. The order must correspond to the sequence of vector retrieval and full\-text matching in the search template. Weights are configured using the `weights` field.

```JSON
PUT _search/pipeline/search_pipeline
{
    "description": "text embedding pipeline for remote inference",
    "request_processors": [
      {
        "remote_embedding": {
          "remote_config": {
            "method": "POST",
            "url": "url",
            "headers": {
              "Content-Type": "application/json"
            },
            "advance_request_body": {
              "model": "model"
            }
          }
        }
      },
      {
        "pre_analyze": {
          "analysis_config": {
            "tokenizer": "ik_smart",
            "filter": [
              "default_dynamic_synonym"
            ]
          }
        }
      }
    ],
    "phase_results_processors": [
      {
        "normalization-processor": {
          "normalization": {
            "technique": "rrf",
            "parameters": {
              "rank_constant": 60
            }
          },
          "combination": {
            "technique": "arithmetic_mean",
            "parameters": {
              "weights": [
                0.2,
                0.8
              ]
            }
          }
        }
      }
    ]
  }
```


<span id="5f076a37"></span>
## Query tuning

Query statements support various tuning options. The following example is a demo of `function_score` tuning combined with hybrid search tuning.

```JSON
{
    "source": {
      "_source": ["post_title","post_content","model_content"],
      "size": 10,
      "query": {
        "hybrid": {
          "queries": [{
              "remote_neural": {
                "post_title_knn": {
                  "query_text": "{{searchVal}}",
                  "k": 1000
                }
              }
            },
            {
              "function_score": {
                "query": {
                  "bool": {
                    "should": [{
                        "match_phrase_prefix": {
                          "post_title": {
                            "query": "{{searchVal}}",
                            "analyzer": "standard"
                          }
                        }
                      },
                      {
                        "match": {
                          "model_content": {
                            "query": "{{searchVal}}",
                            "minimum_should_match": "90%"
                          }
                        }
                      },
                      {
                        "match_phrase_prefix": {
                          "post_title.pinyin": {
                            "query": "{{searchVal}}",
                            "analyzer": "standard"
                          }
                        }
                      }
                    ]
                  }
                },
                "functions": [{
                    "filter": {
                      "match": {
                        "post_title": "游戏"
                      }
                    },
                    "weight": 0.9
                  },
                  {
                    "filter": [{
                      "match": {
                        "post_title": "小说"
                      }
                    }],
                    "weight": 0.7
                  },
                  {
                    "filter": {
                      "term": {
                        "model_content": "攻略"
                      }
                    },
                    "weight": 1.08
                  }, {
                    "script_score": {
                      "script": {
                        "source": " 1.0 +  0.3 * doc['priority'].value"
                      }
                    }
                  }
                ]
              }
            }
          ]
        }
      }
    }
  }
```


Replace the original full\-text matching with function score logic. The `function_score` section contains the original full\-text retrieval logic.


* The `functions` section contains the score adjustment logic. For example, `\"match\": {\"post_title\": \"game\"}` with a `\"weight\": 0.9` means that when the post_title field of a search result matches "game", the total search score is multiplied by 0.9, thus reducing the score. To boost the score, set a weight greater than 1.

* The `Script_score` section defines the overall weighting logic. If a document has a priority field (e.g., signed author \> user\-created), you can set the priority field to 3 for documents by signed authors and 1 for user\-created documents. The scores of matching documents are then adjusted according to the `0.3 * doc['priority'].value` logic.


<span id="jleNwkrb"></span>
## Relevant documentation

Query statements support various query tuning methods, such as Boost and Constant score, which can be combined with hybrid search. For details, refer to the open\-source documentation:


* [Boosting query](https://opensearch.org/docs/latest/query-dsl/compound/boosting/)

* [Constant score query](https://opensearch.org/docs/latest/query-dsl/compound/constant-score/)
