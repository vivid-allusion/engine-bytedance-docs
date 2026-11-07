---
title: "Cloud Search hybrid retrieval + rerank operation example (using Doubao embedding model)"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Cloud_Search_hybrid_retrieval_rerank_operation_example"
---

This topic describes how to use hybrid retrieval, rerank, and other functions through the BytePlus Cloud Search service.

## Principle introduction

In search applications, traditional keyword search has been the main method. It suits scenarios requiring exact match queries, providing low latency and good result explainability. However, keyword search does not consider context and may produce irrelevant results. In recent years, semantic search using vector retrieval technology has become increasingly popular. By converting data objects (text, images, audio, video, etc.) into vectors with machine learning models, vector distance represents the similarity between objects. If the model is highly relevant to the problem domain, it can better understand context and search intent, improving result relevance. Conversely, if the model is less relevant, the effectiveness decreases significantly.

Both keyword search and semantic search have clear advantages and disadvantages. Is it possible to combine their strengths to improve overall search relevance? The answer is no. Simple arithmetic combinations do not achieve the desired effect, mainly for two reasons:

* First, scores for different query types are not on comparable dimensions, so simple arithmetic operations cannot be directly applied.

* Second, in distributed retrieval systems, scoring generally happens at the shard level, requiring global normalization of scores from all shards.

In summary, we need an ideal query type to address these issues, which can execute individual query clauses, collect shard\-level results, and finally normalize and merge all query scores before returning the final result. This is the hybrid search solution.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c1a0eb63a7921f0aac22fe328a72f114.png)

A typical hybrid search query usually involves the following steps:

1. Query stage: use hybrid query clauses to perform keyword search and semantic search.

2. Score normalization and merging phase, which occurs after the query phase.

   1. Since each query type provides scores within different ranges, this phase normalizes the scores of each query clause. Supported normalization methods include `min_max`, `l2`, and `rrf`.

   2. The normalized scores are combined using methods such as `arithmetic_mean`, `geometric_mean`, and `harmonic_mean`.

3. Documents are reordered based on the combined scores and returned to the user.

## Implementation approach

The previous principle introduction shows that implementing a hybrid retrieval application requires at least the following basic technical facilities:

* Full\-text search engine

* Vector search engine

* Machine learning model for vector embedding

* Data pipeline that converts text, audio, video, and other data into vectors

* fused ranking

BytePlus Cloud Search is built on the open\-source Elasticsearch and OpenSearch projects. It has supported mature and comprehensive text retrieval and vector retrieval capabilities since launch. It has also iterated and evolved features for hybrid search scenarios, providing an out\-of\-the\-box hybrid search solution. This article takes image search applications as an example to introduce how to quickly develop a hybrid search application with the BytePlus Cloud Search service solution.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_15bafd9f9740185b79b653cad75748f9.png)

The end\-to\-end process is summarized as follows:

1. Configure and create related objects.

   * Ingestion pipeline: supports automatic model invocation to convert images into vectors and store them in the index.

   * Search pipeline: supports automatically converting text queries into vectors for similarity calculation.

   * k\-NN index: the index that stores vectors.

2. Write dataset data into the OpenSearch instance. OpenSearch automatically invokes machine learning models to convert text into embedding vectors.

3. When the client initiates a hybrid search query, OpenSearch calls the machine learning model to convert the incoming query into an embedding vector.

4. OpenSearch executes hybrid search requests by combining Keyword Search and Semantic Search scores to return search results.

## Prerequisites

* Created an OpenSearch 2.9.0 or later instance. For more information, see [Create an instance](https://docs.byteplus.com/en/docs/cloudsearch/creating-an-instance-2).

* Installed opensearch\-remote\-inference, opensearch\-intervention, and opensearch\-enhancements plugins in the created instance. For more information, see [Managing built-in plugins](https://docs.byteplus.com/en/docs/cloudsearch/manage-built-in-plugins).

* Created two inference services, selecting an Embedding model and a Rerank model respectively.

   > **tip**

   > In this example, the Embedding model uses Doubao\-embedding\-vision, and the Rerank model uses Qwen/Qwen3\-VL\-Reranker\-2B. Please choose the appropriate model according to actual needs.

### Use Embedding and Rerank models in ContextSearch

1. View examples of calling Embedding and Rerank models in the ContextSearch service and obtain the value of the `model` field. For detailed steps, see [View an inference service](https://docs.byteplus.com/en/docs/contextsearch/View_an_inference_service).

   > **tip**

   > In this example, the Embedding model uses Doubao\-embedding\-vision, and the Rerank model uses Qwen/Qwen3\-VL\-Reranker\-2B. Please choose the appropriate model according to actual needs.

   Additionally, you can check the token input count per request on the **Monitoring** tab of the inference service.

2. Create and view the API Key used to call the model. For more information, see [Create an API Key](https://docs.byteplus.com/en/docs/contextsearch/Create_an_API_Key).

### Log on to OpenSearch Dashboards

Log on to Dashboards within the created instance. For more information, see [Public network access to Kibana/Dashboards](https://docs.byteplus.com/en/docs/cloudsearch/logging-tool).

### Create OpenSearch index

Select **Dev Tools** in the left navigation bar of OpenSearch Dashboards.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_febf9129f00eadb9f79315874f00247e.png)

Create an index named `text_index` with the following content.

```HTML
PUT /text_index
{
  "settings": {
    "index": {
      "number_of_shards": "1",
      "number_of_replicas": "1",
      "refresh_interval": "10s",
      "knn": "true",          # 注意使用该配置，否则可能会导致向量检索失效
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
         "dimension": 4096,     ## 需要和推理服务中选择的 embedding 模型 dimension 一致。 
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

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fba305d4f25043b1b02c06ce114e0629~tplv-goo7wpa0wc-image.image)

If you need to modify to DiskANN configuration, refer to [using DiskANN vector engine](https://docs.byteplus.com/en/docs/6465/1553583).

### Create OpenSearch Embedding Pipeline

#### Create OpenSearch Insert Pipeline

Create a Pipeline named `post_embedding` in Dev Tools to write data into OpenSearch. The Pipeline content is as follows. Please replace the field values according to the comments.

```HTML
PUT _ingest/pipeline/post_embedding
{
  "description": "model embedding pipeline for community inference",
  "processors": [
    {
      "remote_text_embedding": {
          "remote_config" : {
               "method" : "POST",
               "url" : "http://ark.cn-beijing.volces.com/api/v3/embeddings", ## 豆包 Embedding 服务固定 URL
               "params" : { },
               "headers" : {
                   "Content-Type" : "application/json",
                   "Authorization": "Bearer {api—key}" ## 创建的 API Key
               },
               "advance_request_body" : {
                   "model" : "ep-xxxxxxx-xxxxxx" ## 上一步 Embedding 推理服务调用信息中"model"字段的值
               }
          }, 
          
          "field_map": {  
              "text": "text_knn"
          }
       } 
    }
  ]
}
```

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/99c851d92b8b47f89ff87afb5c322a74~tplv-goo7wpa0wc-image.image)

#### Create OpenSearch Search Pipeline

Create a Pipeline named `search_pipeline` in Dev Tools to retrieve data from OpenSearch. The Pipeline content is as follows. Please replace the field values according to the comments.

```HTML
PUT _search/pipeline/search_pipeline
{
    "description": "text embedding pipeline for remote inference",
    "request_processors": [
      {
        "remote_embedding": {
          "remote_config": {
            "method": "POST",
            "url" : "https://ark.cn-beijing.volces.com/api/v3/embeddings",
               "params" : { },
               "headers" : {
                   "Content-Type" : "application/json",
                   "Authorization": "Bearer {api—key}" ##创建的api-key
               },
               "advance_request_body" : {
                   "model" : "ep-xxxxxxx-xxxxxx" ##上一步embedding推理服务调用信息中的model字段值
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

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f55429870ccd49a1870db6c43d247450~tplv-goo7wpa0wc-image.image)

## Write test data

Write 100 test data entries in Dev Tools.

```HTTP
POST /text_index/_bulk?pipeline=post_embedding # 与前文创建的 insert pipeline 一致
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

Query data from the OpenSearch index. Finding data indicates write success.

```Bash
GET /text_index/_search
{
    "query": {
      "match_all": {}
    }
}
```

## ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/273411a76d8b406d9bb4fc200b4243f6~tplv-goo7wpa0wc-image.image)

## Data retrieval test

### Vector + keyword hybrid search

Test vector + keyword hybrid search effect. Example:

```HTTP
GET /text_index/_search?search_pipeline=search_pipeline # 注意与创建的 Search Pipeline 保持一致
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

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2c455bd7794543d29c680b66123c3618~tplv-goo7wpa0wc-image.image)

### Rerank test

Export API Key to local environment variables.

```Bash
export API_KEY="5cad31c3-**************-e5b7d3c9294d"
```

#### Rerank API call

Rerank API calls support command\-line invocation and OpenSearch Pipeline invocation.

**Call via command line**

Execute the public network information call command in the command\-line tool to call the Rerank interface.   For detailed steps, see [View an inference service](https://docs.byteplus.com/en/docs/contextsearch/View_an_inference_service).

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

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7f9823ce438e4f69b5603cf66ae60b6e~tplv-goo7wpa0wc-image.image)

**Call via OpenSearch Rerank Pipeline**

1. Create a rerank pipeline named `search_pipeline_with_rerank` in Dev Tools, including embedding and rerank models, for querying data in OpenSearch. The pipeline content is as follows; remember to replace field values according to comments.

   ```HTTP
   PUT _search/pipeline/search_pipeline_with_rerank
   {
     "description": "text embedding pipeline for remote inference",
     "request_processors": [
       {
            "remote_embedding": {
             "remote_config": {
               "method": "POST",
               "url" : "https://ark.cn-beijing.volces.com/api/v3/embeddings",
                  "params" : { },
                  "headers" : {
                      "Content-Type" : "application/json",
                      "Authorization": "Bearer {api-key}" ## 创建的 API Key
                  },
                  "advance_request_body" : {
                      "model" : "ep-xxxxx-xxxxx" ## Embedding 推理服务调用信息中"model"字段的值
                  }
             }
           }
       }
     ]
     ,
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
     ]
     ,
     "response_processors": [
       {
         "remote_rerank": {
           "ml_opensearch": {
             "remote_config": {
               "method": "POST",
               "url": "{rerank_url}",## Rerank 服务调用信息中"url"字段的值
               "params": {
                 "token": "{api_key}" ## 创建的 API Key
               },
               "headers": {
                 "Content-Type": "application/json"
               },
               "advance_request_body": {
                 "model": "{rerank_model}"## Rerank 服务调用信息中"model"字段的值
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

2. Use the OpenSearch rerank pipeline for queries.

   ```HTML
   GET /text_index/_search?search_pipeline=search_pipeline_with_rerank  ## 创建的 Rerank Pipeline 名称
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
           "query_text": "哪个答案和电吉他、电子琴最匹配？" ## 设置提问内容
           }
         }
       }
     }
   ```

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/604dd035a3ae4940b25fc1198ad9e8d4~tplv-goo7wpa0wc-image.image)
