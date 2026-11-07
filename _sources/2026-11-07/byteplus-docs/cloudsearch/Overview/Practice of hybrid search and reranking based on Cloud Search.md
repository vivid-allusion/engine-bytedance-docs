---
title: "Practice of hybrid search and reranking based on Cloud Search"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Practice_of_hybrid_search_and_reranking_based_on_Cloud_Search"
---

Cloud Search supports hybrid search combined with ContextSearch services, such as vector and keyword hybrid search, and also supports reranking (Rerank). This topic explains how to perform hybrid search and reranking.

## Prepare the basic environment

### Initialize the Cloud Search instance

1. Deploy the Cloud Search OpenSearch 2.9.0 instance. For more information, see [Create an instance](https://docs.byteplus.com/docs/cloudsearch/creating-an-instance-2).

   > **tip**

   > If you need to operate via public network later, enable **instance public network access** and **Dashboards public network access** when creating.

2. Enable the Cloud Search related plugin opensearch\-remote\-inference. For the procedure, see [Install a system built-in plugin](https://docs.byteplus.com/docs/cloudsearch/manage-built-in-plugins).

### Use the Doubao\-embedding\-vision model in ContextSearch

1. View the Doubao\-embedding\-vision model call example in the ContextSearch service and get the `model` field value. For detailed steps, see [View an inference service](https://docs.byteplus.com/en/docs/contextsearch/View_an_inference_service).

   Additionally, you can check the token input count per request on the **Monitoring** tab of the inference service.

2. Create and view the API Key used to call the model. For more information, see [Create an API Key](https://docs.byteplus.com/en/docs/contextsearch/Create_an_API_Key).

### Create index and pipeline

1. Log in to Dashboards of the OpenSearch 2.9.0 or later instance created in [Initialize Cloud Search instance](https://docs.byteplus.com/docs/cloudsearch/Practice_of_hybrid_search_and_reranking_based_on_Cloud_Search#4ae93145). Refer to the [Log on to Kibana/Dashboards](https://docs.byteplus.com/docs/cloudsearch/logging-tool) procedure.

2. Create an OpenSearch index named `text_index`. The command example is as follows.

   ```HTTP
   PUT /text_index
   {
     "settings": {
       "index": {
         "number_of_shards": "1",
         "number_of_replicas": "1",
         "refresh_interval": "10s",
         "knn": "true",          # 请勿遗漏该配置，否则可能会导致向量检索失效。
         "indexing": {
           "slowlog": {
             "level": "info",
             "threshold": {
               "index": {
                 "warn": "200ms",
                 "trace": "20ms",
                 "debug": "50ms",
                 "info": "100ms"
               }
             },
             "source": "1000"
           }
         },
         "search": {
           "slowlog": {
             "level": "info",
             "threshold": {
               "query": {
                 "warn": "500ms",
                 "trace": "50ms",
                 "debug": "100ms",
                 "info": "200ms"
               },
               "fetch": {
                 "warn": "200ms",
                 "trace": "50ms",
                 "debug": "80ms",
                 "info": "100ms"
               }
             }
           }
         }
       }
     },
     "mappings": {
       "properties": {
         "text": {
           "type": "text",
           "analyzer": "ik_max_word"
         },
         "text_knn": {
           "type": "knn_vector",
            "dimension": 1024,     # 需要和推理服务中选择的 Embedding 模型的 dimension 一致，即在推理服务查看关联模型时，描述列的 dim 值。
           "method": {
             "engine": "nmslib",
             "space_type": "cosinesimil",
             "name": "hnsw",
             "parameters": {}
           }
         }
       }
     }
   }
   ```

3. Create an insert pipeline to write data into OpenSearch. This example creates a pipeline named `post_embedding`. The command example is as follows.

   > **tip**

   > Note to replace the variables in the **call information** of [Using Doubao\-embedding\-vision model in ContextSearch](https://docs.byteplus.com/docs/cloudsearch/Practice_of_hybrid_search_and_reranking_based_on_Cloud_Search#UnY8Edsl).

   ```HTTP
   PUT _ingest/pipeline/post_embedding
   {
     "description": "model embedding pipeline for community inference",
     "processors": [
       {
         "remote_text_embedding": {
             "remote_config" : {
                  "method" : "POST",
                  "url" : "{embedding_url}",
                  "params" : { },
                  "headers" : {
                      "Content-Type" : "application/json",
                      "Authorization": "Bearer {api—key}" ## 创建的 API Key
                  },
                  "advance_request_body" : {
                      "model" : "{model}"
                  }
             },  # remote_config end
             
             "field_map": {  
                 "text": "text_knn"
                 # 使用 text 字段来生成 text_knn 字段。后续步骤中写入 text 字段的具体值。
             }
          } #remote_text_embedding end
       }
     ]
   }
   ```

4. Create a search pipeline to retrieve data in OpenSearch. This example creates a pipeline named `search_pipeline`. The command example is as follows.

   > **tip**

   > Note to replace the variables in the **call information** of [Doubao\-embedding\-vision model used in ContextSearch](https://docs.byteplus.com/docs/cloudsearch/Practice_of_hybrid_search_and_reranking_based_on_Cloud_Search#UnY8Edsl).

   ```HTTP
   PUT _search/pipeline/search_pipeline
   {
     "description": "Text embedding pipeline for remote inference",
     "request_processors": [
       {
         "remote_embedding": {
           "remote_config": {
             "method": "POST",
             "url": "{embedding_url}",
             "headers": {
               "Content-Type": "application/json",
               "Authorization": "Bearer {api—key}" ## 创建的 API Key
             },
             "advance_request_body": {
               "model": "{model}"
             }
           }
         }
       }
     ],
     "phase_results_processors": [
       {
         "normalization-processor": {
           "normalization": {
             "technique": "min_max"
           },
           "combination": {
             "technique": "arithmetic_mean",
             "parameters": {}
           }
         }
       }
     ]
   }
   ```

## Write test data

Write 100 test records. The command example is as follows.

```Bash
POST /text_index/_bulk?pipeline=post_embedding # Match the Insert Pipeline name created earlier.
{ "index": { "_id": 1 } }
{ "text": "口风琴" }
{ "index": { "_id": 2 } }
{ "text": "电子琴" }
{ "index": { "_id": 3 } }
{ "text": "吉他" }
{ "index": { "_id": 4 } }
{ "text": "钢琴" }
{ "index": { "_id": 5 } }
{ "text": "小提琴" }
{ "index": { "_id": 6 } }
{ "text": "鼓" }
{ "index": { "_id": 7 } }
{ "text": "萨克斯" }
{ "index": { "_id": 8 } }
{ "text": "低音提琴" }
{ "index": { "_id": 9 } }
{ "text": "电子合成器" }
{ "index": { "_id": 10 } }
{ "text": "风琴" }
{ "index": { "_id": 11 } }
{ "text": "竖琴" }
{ "index": { "_id": 12 } }
{ "text": "口琴" }
{ "index": { "_id": 13 } }
{ "text": "电子打击乐器" }
{ "index": { "_id": 14 } }
{ "text": "手风琴" }
{ "index": { "_id": 15 } }
{ "text": "鼓组" }
{ "index": { "_id": 16 } }
{ "text": "电子小号" }
{ "index": { "_id": 17 } }
{ "text": "铜管乐器" }
{ "index": { "_id": 18 } }
{ "text": "木管乐器" }
{ "index": { "_id": 19 } }
{ "text": "打击乐器" }
{ "index": { "_id": 20 } }
{ "text": "电子小号" }
{ "index": { "_id": 21 } }
{ "text": "牙刷" }
{ "index": { "_id": 22 } }
{ "text": "洗发水" }
{ "index": { "_id": 23 } }
{ "text": "漱口水" }
{ "index": { "_id": 24 } }
{ "text": "纸巾" }
{ "index": { "_id": 25 } }
{ "text": "洗衣粉" }
{ "index": { "_id": 26 } }
{ "text": "洗洁精" }
{ "index": { "_id": 27 } }
{ "text": "沐浴露" }
{ "index": { "_id": 28 } }
{ "text": "毛巾" }
{ "index": { "_id": 29 } }
{ "text": "垃圾袋" }
{ "index": { "_id": 30 } }
{ "text": "牙膏" }
{ "index": { "_id": 31 } }
{ "text": "香皂" }
{ "index": { "_id": 32 } }
{ "text": "洗面奶" }
{ "index": { "_id": 33 } }
{ "text": "清洁剂" }
{ "index": { "_id": 34 } }
{ "text": "洗手液" }
{ "index": { "_id": 35 } }
{ "text": "护肤霜" }
{ "index": { "_id": 36 } }
{ "text": "面膜" }
{ "index": { "_id": 37 } }
{ "text": "卫生纸" }
{ "index": { "_id": 38 } }
{ "text": "食品保鲜膜" }
{ "index": { "_id": 39 } }
{ "text": "水杯" }
{ "index": { "_id": 40 } }
{ "text": "器具清洗液" }
{ "index": { "_id": 41 } }
{ "text": "餐具消毒液" }
{ "index": { "_id": 42 } }
{ "text": "保鲜盒" }
{ "index": { "_id": 43 } }
{ "text": "便签纸" }
{ "index": { "_id": 44 } }
{ "text": "《活着》" }
{ "index": { "_id": 45 } }
{ "text": "《百年孤独》" }
{ "index": { "_id": 46 } }
{ "text": "《小王子》" }
{ "index": { "_id": 47 } }
{ "text": "《1984》" }
{ "index": { "_id": 48 } }
{ "text": "《骆驼祥子》" }
{ "index": { "_id": 49 } }
{ "text": "《红楼梦》" }
{ "index": { "_id": 50 } }
{ "text": "《西游记》" }
{ "index": { "_id": 51 } }
{ "text": "《三国演义》" }
{ "index": { "_id": 52 } }
{ "text": "《围城》" }
{ "index": { "_id": 53 } }
{ "text": "《悲惨世界》" }
{ "index": { "_id": 54 } }
{ "text": "《哈利·波特》" }
{ "index": { "_id": 55 } }
{ "text": "《无声告白》" }
{ "index": { "_id": 56 } }
{ "text": "《时间简史》" }
{ "index": { "_id": 57 } }
{ "text": "《追风筝的人》" }
{ "index": { "_id": 58 } }
{ "text": "《平凡的世界》" }
{ "index": { "_id": 59 } }
{ "text": "《三体》" }
{ "index": { "_id": 60 } }
{ "text": "《人类简史》" }
{ "index": { "_id": 61 } }
{ "text": "《安娜·卡列尼娜》" }
{ "index": { "_id": 62 } }
{ "text": "《月亮和六便士》" }
{ "index": { "_id": 63 } }
{ "text": "《未来简史》" }
{ "index": { "_id": 64 } }
{ "text": "北京" }
{ "index": { "_id": 65 } }
{ "text": "上海" }
{ "index": { "_id": 66 } }
{ "text": "广州" }
{ "index": { "_id": 67 } }
{ "text": "深圳" }
{ "index": { "_id": 68 } }
{ "text": "成都" }
{ "index": { "_id": 69 } }
{ "text": "重庆" }
{ "index": { "_id": 70 } }
{ "text": "杭州" }
{ "index": { "_id": 71 } }
{ "text": "武汉" }
{ "index": { "_id": 72 } }
{ "text": "西安" }
{ "index": { "_id": 73 } }
{ "text": "南京" }
{ "index": { "_id": 74 } }
{ "text": "青岛" }
{ "index": { "_id": 75 } }
{ "text": "郑州" }
{ "index": { "_id": 76 } }
{ "text": "福州" }
{ "index": { "_id": 77 } }
{ "text": "厦门" }
{ "index": { "_id": 78 } }
{ "text": "天津" }
{ "index": { "_id": 79 } }
{ "text": "大连" }
{ "index": { "_id": 80 } }
{ "text": "厦门" }
{ "index": { "_id": 81 } }
{ "text": "济南" }
{ "index": { "_id": 82 } }
{ "text": "青岛" }
{ "index": { "_id": 83 } }
{ "text": "昆明" }
{ "index": { "_id": 84 } }
{ "text": "哈尔滨" }
{ "index": { "_id": 85 } }
{ "text": "长沙" }
{ "index": { "_id": 86 } }
{ "text": "广州" }
{ "index": { "_id": 87 } }
{ "text": "合肥" }
{ "index": { "_id": 88 } }
{ "text": "南宁" }
{ "index": { "_id": 89 } }
{ "text": "太原" }
{ "index": { "_id": 90 } }
{ "text": "南昌" }
{ "index": { "_id": 91 } }
{ "text": "狗" }
{ "index": { "_id": 92 } }
{ "text": "猫" }
{ "index": { "_id": 93 } }
{ "text": "狐狸" }
{ "index": { "_id": 94 } }
{ "text": "大象" }
{ "index": { "_id": 95 } }
{ "text": "老虎" }
{ "index": { "_id": 96 } }
{ "text": "狮子" }
{ "index": { "_id": 97 } }
{ "text": "熊" }
{ "index": { "_id": 98 } }
{ "text": "长颈鹿" }
{ "index": { "_id": 99 } }
{ "text": "斑马" }
{ "index": { "_id": 100 } }
{ "text": "鳄鱼" }
```

### Verify the written data

Execute the following command. If data can be queried from the OpenSearch index, the write was successful.

```Bash
GET /text_index/_search
{
    "query": {
        "match_all": {}
    }
}
```

## Retrieve data

### Vector and keyword hybrid search

Perform a hybrid search of vectors and keywords. The command example is as follows.

```Bash
GET /text_index/_search?search_pipeline=search_pipeline # Consistent with the previously created Search Pipeline name
{
    "_source": "text",
    "query": {
        "hybrid": {
            "queries": [
                {
                    "remote_neural": {
                        "text_knn": {
                            "query_text": "电吉他",
                            "k": 10
                        }
                    }
                },
                {
                    "intervals": {
                        "text": {
                            "match": {
                                "query": "电子琴",
                                "ordered": true,
                                "max_gaps": 3
                            }
                        }
                    }
                }
            ]
        }
    }
}
```

The back results are shown in the figure below.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/27f0d59f5e8d42be8a583ceb6e86bcc5~tplv-goo7wpa0wc-image.image)

### Rerank test

1. Deploy the Rerank model. The procedure is similar to [Using the Doubao-embedding-vision model in ContextSearch](https://docs.byteplus.com/docs/cloudsearch/Practice_of_hybrid_search_and_reranking_based_on_Cloud_Search#UnY8Edsl).

   > **tip**

   > This example selects the **inference model** **Qwen/Qwen3\-VL\-Reranker\-2B**. Choose the appropriate model based on business needs.

2. Create an API Key.

   > **tip**

   > The API Key is essential for identity authentication when calling the inference service interface and must be created before formally using the inference service. Please keep your API Key secure.

3. View API Key.

4. Set the API Key environment variable in your local environment. The command example is as follows.

   ```Bash
   export API_KEY="5cad31c3-**************-e5b7d3c9294d"
   ```

5. Use the command line or Pipeline to call the Rerank interface.

   **Call the Rerank API via command line**

View the **Public network call information** or **Private network call information** of the Rerank service, copy it to the command line, and modify parameters. The command example is as follows.

   ```Bash
   curl http://{addr}/v1/rerank \
     -H "Content-Type: application/json" \
     -H "Authorization: Bearer $API_KEY" \
     -X POST \
     -d '{
       "model": "Qwen/Qwen3-VL-Reranker-2B",
       "query": "电子琴",
       "top_n": 7,
       "documents": [
        "口风琴",
        "吉他",
        "北京",
        "牙刷",
        "电脑",
        "显示器",
        "电子琴",
        "电子",
        "鼓"
        ]
     }' | jq .
   ```

   The back results are shown in the figure below.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ec08099c53894197b648115f34db4cfb~tplv-goo7wpa0wc-image.image)

   **Call the Rerank API via pipeline**

1. Create a Rerank Pipeline to retrieve data in OpenSearch. This example creates a pipeline named `search_pipeline_with_rerank`. The command example is as follows.

      > **tip**

      > Replace variables in the call information for the Embedding service and Rerank service in the command.

      ```Bash
      PUT _search/pipeline/search_pipeline_with_rerank
      {
        "description": "text embedding pipeline for remote inference",
        "request_processors": [
          {
            "remote_embedding": {
              "remote_config": {
                "method": "POST",
                "url": "{embedding_url}",
                "headers": {
                  "Content-Type": "application/json"
                },
                "advance_request_body": {
                  "model": "{embedding_model}"
                }
              }
            }
          }
        ],
        "phase_results_processors": [
          {
            "normalization-processor": {
              "normalization": {
                "technique": "min_max"
              },
              "combination": {
                "technique": "arithmetic_mean",
                "parameters": {
                  "weights": [
                    0.3,
                    0.7
                  ]
                }
              }
            }
          }
        ],
        "response_processors": [
          {
            "remote_rerank": {
              "ml_opensearch": {
                "remote_config": {
                  "method": "POST",
                  "url": "{rerank_url}",
                  "params": {
                    "token": "{API_KEY}"
                  },
                  "headers": {
                    "Content-Type": "application/json"
                  },
                  "advance_request_body": {
                    "model": "{rerank_model}"
                  }
                }
              },
              "context": {
                "document_fields": [
                  "text"
                ]
              }
            }
          }
        ]
      }
      ```

   2. Use the Rerank Pipeline. The command example is as follows.

      > **tip**

      > Add ext information in the Query when using it. Set the corresponding question content for `ext.remote_rerank.query_context.query_text`.

      ```Bash
      GET /text_index/_search?search_pipeline=search_pipeline_with_rerank
      {
        "_source": "text",
        "query": {
          "hybrid": {
            "queries": [
              {
                "remote_neural": {
                  "text_knn": {
                    "query_text": "电吉他",
                    "k": 10
                  }
                }
              },
              {
                "intervals": {
                  "text": {
                    "match": {
                      "query": "电子琴",
                      "ordered": true,
                      "max_gaps": 3
                    }
                  }
                }
              }
            ]
          }
        },
        "ext": {
          "remote_rerank": {
            "query_context": {
              "query_text": "哪个答案和电吉他、电子琴最匹配？"
              }
            }
          }
        }
      ```

   The return result is shown in the following figure.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ea126f1c04ef419e9e90a836d98b8b98~tplv-goo7wpa0wc-image.image)
