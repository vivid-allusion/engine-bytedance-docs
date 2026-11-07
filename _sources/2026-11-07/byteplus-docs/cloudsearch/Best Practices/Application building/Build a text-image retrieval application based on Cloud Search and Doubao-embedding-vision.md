---
title: "Build a text-image retrieval application based on Cloud Search and Doubao-embedding-vision model"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Build_a_text-image_retrieval_application_based_on_Cloud_Search_and_Doubao-embedding-vision_model"
---

Doubao\-embedding\-vision model maps images and text into a unified vector space to achieve cross\-modal semantic understanding. This topic describes how to use Cloud Search and Doubao\-embedding\-vision model to perform image vectorization, data indexing, and text\-image retrieval, quickly building an application that supports image\-to\-image and text\-to\-image search.

<span id="66tOkoIo"></span>
## Background

Image\-text retrieval is widely used in popular fields such as e\-commerce, advertising, design, and search engines. Common image\-text retrieval includes image\-to\-image and text\-to\-image search, allowing users to quickly find identical or similar images from large image libraries by inputting text descriptions or uploading pictures.

The input text description and picture serve as retrieval targets; features are extracted separately from images and text, the model establishes the correlation between them, and then vector search is conducted over a large image database to return the most relevant result set. The feature extraction part uses the CLIP model, and vector retrieval uses BytePlus Cloud Search for fast search among massive image features.<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f5844f24457019410310919fa4f45754.png) </span>

<span id="Ijv6YBGb"></span>
## Prerequisites

A TOS bucket and folder for storing pictures have been created. In this example, the bucket name is `doc-test`, the Endpoint domain node is `tos-cn-beijing.ivolces.com`, and the image storage path is `picture/image_temp`. For details, see [Create a bucket](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket) and [Create a folder](https://docs.byteplus.com/en/docs/tos/docs-creating-a-folder). Picture access permissions must be set to public read or use a signed URL.

<span id="s5UAw1zg"></span>
## Create resources

<span id="RYinvwTk"></span>
### Create an OpenSearch instance

Create an OpenSearch 2.9.0 version instance. For more information, see [Create an instance](https://docs.byteplus.com/en/docs/cloudsearch/creating-an-instance-2).

This topic uses 10 million pictures as an example, adopting the DiskANN + RaBitQ indexing scheme, and recommends the following instance specifications.


|Test scenario |Product |Parameter |Recommended Specification |
|---|---|---|---|
|picture scale: 10 million images.<br><br>embedding model: Doubao\-vision\-embedding, 2048 dimensions. |Cloud Search |Dedicated master node |3 \* ex.x2.large (4c8g20G PL0) |
|||Data node |3 \* es.x8.xlarge (8c64g + 800G FlexPL) |
|||Dashboard |1 \* kibana.x2.medium (2c4g) |


<span id="NDPj7uBj"></span>
### Use the Doubao\-embedding\-vision model in ContextSearch


1. View the Doubao\-embedding\-vision model call example in the ContextSearch service and get the `model` field value. For detailed steps, see [View an inference service](https://docs.byteplus.com/en/docs/contextsearch/View_an_inference_service).

   Additionally, you can check the token input count per request on the **Monitoring** tab of the inference service.

2. Create and view the API Key used to call the model. For more information, see [Create an API Key](https://docs.byteplus.com/en/docs/contextsearch/Create_an_API_Key).


<span id="S3QmZLTv"></span>
## Deploy image and text search application

<span id="QShRBNQ6"></span>
### Create an OpenSearch index


1. Log on to the instance visualization tool Dashboards. For detailed steps, see [Log on to Kibana/Dashboards](https://docs.byteplus.com/en/docs/cloudsearch/logging-tool).

2. In the left navigation bar, select **Management \> Dev Tools**.

3. In Dev Tools, create an OpenSearch index with the following code.

   ```HTTP
   PUT imagesearch
   {
       "settings": {
           "index": {
               "default_pipeline": "multimodal_remote_embedding",
               "refresh_interval": "60s",
               "knn": "true"
           },
           "knn.algo_param.diskann.store_strategy": "MEMORY",
           "knn.algo_param.diskann.distance_strategy": "MULTI_BITS",
           "knn.algo_param.diskann.sl": 200,
           "number_of_replicas": 0,
           "number_of_shards": "3"
       },
       "mappings": {
           "properties": {
               "id": {
                 "type": "keyword"
               },
               "vector_source_image": {
                  "type": "keyword"
               },
               "description": {
                   "type": "text"
               },
               "vector": {
                    "type": "knn_vector",
                    "dimension": 2048,
                     "method": {
                       "name": "diskann",
                       "space_type": "cosinesimil",
                       "engine": "diskann",
                       "parameters": {
                         "R": 64,
                         "L": 32,
                         "quant_type": "rabitq",
                         "rabitq_centers": 64
                       }
                     }
               }
           }
       }
   }
   ```
   

4. Configure DiskANN + RaBitQ vector engine cluster with the following code.

   ```HTTP
   PUT _cluster/settings
   {
     "persistent": {
       "index.knn.algo_param.diskann.store_strategy": "MEMORY",
       "index.knn.algo_param.diskann.distance_strategy": "MULTI_BITS",
       "index.knn.algo_param.diskann.sl": 200
     }
   }
   ```
   

   For details, see [Using the DiskANN vector engine](https://docs.byteplus.com/en/docs/6465/1553583).


<span id="8u0hRe5e"></span>
### create ingest pipeline

To create an ingest pipeline, specify the Image Embedding model to convert the designated field (picture information) into a vector and embed it back.

Execute the following command to create an ingest pipeline with the ID `image_remote_embedding`.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">When creating an ingest pipeline, fill in the following information:</div>



* <div data-tips="true" data-tips-type="default"><code>Authorization</code>: Set it to the API Key you created for calling the model.</div>


* <div data-tips="true" data-tips-type="default"><code>model</code>: Set it to the value of the <code>model</code> field obtained from the <strong>Call information</strong> of the Doubao\-embedding\-vision model service.</div>


* <div data-tips="true" data-tips-type="default">The definition in <code>field_map</code> indicates that the <code>description</code> field and <code>vector_source_image</code> picture content will be vectorized and stored in the <code>vector</code> field.</div>



```HTTP
PUT _ingest/pipeline/multimodal_remote_embedding
{
    "description": "image/text embedding pipeline for remote inference",
    "processors": [
        {
            "remote_multimodal_embedding": {
                "remote_config": {
                    "method": "POST",
                    "url": "https://ark.cn-beijing.volces.com/api/v3/embeddings/multimodal",
                    "params": {

                    },
                    "headers": {
                        "Content-Type": "application/json",
                        "Authorization": "Bearer API KEY"
                    },
                    "advance_request_body": {
                        "model": "ep-xxx-xxx"
                    }
                },
                "field_map": {
                    "text": "description",
                    "image": "vector_source_image",
                    "embedding": "vector"
                }
            }
        }
    ]
}
```


For multiple vectorized fields, refer to the following code.

```HTTP
PUT _ingest/pipeline/multimodal_remote_embedding
{
    "description": "image/text embedding pipeline for remote inference",
    "processors": [
        {
            "remote_multimodal_embedding": {
                "remote_config": {
                    "method": "POST",
                    "url": "https://ark.cn-beijing.volces.com/api/v3/embeddings/multimodal",
                    "params": {

                    },
                    "headers": {
                        "Content-Type": "application/json",
                        "Authorization": "Bearer API KEY"
                    },
                    "advance_request_body": {
                        "model": "ep-xxx-xxx"
                    }
                },
                "field_map": {
                    "text": "description",
                    "image": "vector_source_image",
                    "embedding": "vector"
                }
            }
        },
        {
            "remote_multimodal_embedding": {
                "remote_config": {
                    "method": "POST",
                    "url": "https://ark.cn-beijing.volces.com/api/v3/embeddings/multimodal",
                    "params": {

                    },
                    "headers": {
                        "Content-Type": "application/json",
                        "Authorization": "Bearer API KEY"
                    },
                    "advance_request_body": {
                        "model": "ep-xxx-xxx"
                    }
                },
                "field_map": {
                    "text": "description_2",
                    "image": "vector_source_image_2",
                    "embedding": "vector_2"
                }
            }
        }
    ]
}
```


<span id="9ViUu6lu"></span>
### Create a search pipeline

Execute the following command to create the search pipeline.

```HTTP
PUT _search/pipeline/multimodal_embedding_search_pipeline
{
  "description": "image/text embedding pipeline for remote inference",
  "request_processors": [
    {
      "remote_multimodal_embedding": {
         "remote_config":
                {
                    "method": "POST",
                    "url": "https://ark.cn-beijing.volces.com/api/v3/embeddings/multimodal",
                    "params": {},
                    "headers":
                    {
                        "Content-Type": "application/json",
                        "Authorization": "Bearer API KEY"
                    },
                    "advance_request_body":
                    {
                        "model": "ep-xxx-xxx"
                    }
                }
      }
    }
  ]
}
```


<span id="KQ0uWw8Z"></span>
## Verify results

<span id="fuIPuuQS"></span>
### Write data

Execute the following command to write images from the TOS Bucket into the `imagesearch` index.

```HTTP
POST _bulk
{ "index" : { "_index" : "imagesearch" } }
{ "id": "0a655b1f2c18632a534796bbf46a4ff7", "vector_source_image" : "https://doc-test.tos-cn-beijing.volces.com/picture/image_temp/0a655b1f2c18632a534796bbf46a4ff7.jpg","description":"图片中商品描述" }
{ "index" : { "_index" : "imagesearch" } }
{ "id": "0a6854edd10ed7bf0aea33f49f6bf340", "vector_source_image" : "https://doc-test.tos-cn-beijing.volces.com/picture/image_temp/0a6854edd10ed7bf0aea33f49f6bf340.jpg", "description":"图片中商品描述" }
```


Execute the following command to check the written data.

```HTTP
GET imagesearch/_search
{
  "query": {
    "match_all": {}
  }
}
```


<span id="KtJyuUcc"></span>
### Search data

Supports queries through the search pipeline, kNN, or Java client.


<Tabs>
<Tab zoneid="PnUukEsQYw" title="query through search pipeline">
<TabTitle>query through search pipeline</TabTitle>

Support passing text or picture as search criteria during query:


* `query_text`: text query content.

* `query_image`: picture query content, supports the following two formats:

   * Publicly accessible picture URL.

   * Base64 encoded picture, format: `data:image/{picture format};base64,{picture Base64 encoding}`.


`query_text` and `query_image` can be used separately or together.

```HTTP
GET imagesearch/_search?search_pipeline=multimodal_embedding_search_pipeline
{
  "size": 20, 
  "_source": {
    "includes": ["id", "description", "vector_source_image"]
  },
  "query": {
    "remote_multimodal_neural": {
      "vector": {                  
        "query_text": "文字检索内容",    
        "query_image": "https://doc-test-1.tos-cn-beijing.volces.com/images/000000039769.jpg",
        "k": 20
      }
    }
  }
}
```



</Tab>
<Tab zoneid="Sp7QfbAX7R" title="query through kNN">
<TabTitle>query through kNN</TabTitle>

```HTTP
GET imagesearch/_search
{
  "size": 20, 
  "_source": {
    "includes": ["id", "description", "vector_source_image"]
  },
  "query": {
    "knn": {
      "vector": {                  
        "vector": [1.0,2.0,3.0,...,8.0],
        "k": 20
      }
    }
  }
}
```



</Tab>
<Tab zoneid="PZpMTPpkjA" title="query through Java client">
<TabTitle>query through Java client</TabTitle>

Set the default search pipeline for the index.

```HTTP
PUT /imagesearch/_settings
{
  "settings": {
    "search.default_pipeline": "multimodal_embedding_search_pipeline"
  }
}
```


Create a `search_template`.

```HTTP
PUT _scripts/multimodal_search_template
{
    "script": {
        "lang": "mustache",
        "source": {
            "_source": {
                "includes": [
                    "id",
                    "description",
                    "item_info"
                ]
            },
            "size": "{{size}}",
            "from": "{{from}}",
            "query": {
                "remote_multimodal_neural": {
                    "vector": {
                        "query_text": "{{keyword}}",
                        "query_image": "{{image}}",
                        "k": "{{k}}"
                    }
                }
            }
        }
    }
}
```


Add maven dependencies.

```XML
<dependency>
    <groupId>org.opensearch.client</groupId>
    <artifactId>opensearch-rest-high-level-client</artifactId>
    <version>2.9.0</version>
</dependency>
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-core</artifactId>
    <version>2.15.2</version>
</dependency>
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.12.7.2</version>
</dependency>
```



</Tab>
</Tabs>


The example code is as follows.


<Tabs>
<Tab zoneid="N7sjjnXN" title="Query using search pipeline">
<TabTitle>Query using search pipeline</TabTitle>

```Java
import org.apache.http.HttpHost;
import org.apache.http.auth.AuthScope;
import org.apache.http.auth.UsernamePasswordCredentials;
import org.apache.http.client.CredentialsProvider;
import org.apache.http.conn.ssl.NoopHostnameVerifier;
import org.apache.http.impl.client.BasicCredentialsProvider;
import org.apache.http.nio.conn.ssl.SSLIOSessionStrategy;
import org.apache.http.ssl.SSLContextBuilder;
import org.opensearch.action.search.SearchRequest;
import org.opensearch.action.search.SearchResponse;
import org.opensearch.client.*;
import org.opensearch.script.ScriptType;
import org.opensearch.script.mustache.SearchTemplateRequest;
import org.opensearch.script.mustache.SearchTemplateResponse;

import javax.net.ssl.SSLContext;
import java.util.Arrays;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class Main {
    RestHighLevelClient initRestHighLevelClientWithCA(List<HttpHost> hosts, String user, String password) throws Exception {
        if (hosts == null || hosts.isEmpty()) {
            throw new IllegalArgumentException("invalid empty hosts");
        }
        // add more parameters check here

        // identity information related
        final CredentialsProvider provider = new BasicCredentialsProvider();
        provider.setCredentials(AuthScope.ANY, new UsernamePasswordCredentials(user, password));

        SSLContext sslContext = new SSLContextBuilder().loadTrustMaterial(null, (x509Certificates, s) -> true).build();  // skip SSL certificate verification


        RestClientBuilder builder = RestClient.builder(hosts.toArray(new HttpHost[0]))
                .setHttpClientConfigCallback(httpClientBuilder -> httpClientBuilder
                        .setDefaultCredentialsProvider(provider)  // set authentication credentials
                        .setSSLStrategy(new SSLIOSessionStrategy(sslContext, NoopHostnameVerifier.INSTANCE))
                )  // skip HostName verification
                .setRequestConfigCallback(requestBuilder -> requestBuilder
                        .setConnectionRequestTimeout(5000)  // get max wait time for connection from the pool, adjust according to actual conditions
                        .setSocketTimeout(60000)  // request timeout, adjust according to actual conditions
                        .setConnectTimeout(5000));  // connection timeout, adjust according to actual situation

        return new RestHighLevelClient(builder);
    }
    public static void main(String[] args) throws Exception {
        RestHighLevelClient client = new Main().initRestHighLevelClientWithCA(Arrays.asList(new HttpHost("{host}", 9200, "https")), "{username}", "{password}");
        SearchTemplateRequest searchTemplateRequest = new SearchTemplateRequest();
        searchTemplateRequest.setRequest(new SearchRequest().indices("imagesearch"));
        searchTemplateRequest.setScriptType(ScriptType.STORED);
        searchTemplateRequest.setScript("multimodal_search_template");
        Map<String, Object> paramMap = new HashMap<String, Object>() {{
            put("from", 0);
            put("size", 20);
            put("keyword", "猫"); // Leave fields not participating in search empty, e.g., ""
            put("image", "https://doc-test-1.tos-cn-beijing.volces.com/images/000000039769.jpg");
            put("k", 20);
        }};

        searchTemplateRequest.setScriptParams(paramMap);
        SearchTemplateResponse searchTemplateResponse = client.searchTemplate(searchTemplateRequest, RequestOptions.DEFAULT);
        client.close();
        SearchResponse response = searchTemplateResponse.getResponse();
        Arrays.stream(response.getHits().getHits()).forEach(item -> {
            System.out.println(item);
        });
    }
}
```



</Tab>
<Tab zoneid="UmizUB6f" title="Query using kNN">
<TabTitle>Query using kNN</TabTitle>

```Java
import com.fasterxml.jackson.databind.JsonNode;
import com.fasterxml.jackson.databind.ObjectMapper;
import org.apache.http.HttpHost;
import org.apache.http.auth.AuthScope;
import org.apache.http.auth.UsernamePasswordCredentials;
import org.apache.http.client.CredentialsProvider;
import org.apache.http.conn.ssl.NoopHostnameVerifier;
import org.apache.http.impl.client.BasicCredentialsProvider;
import org.apache.http.nio.conn.ssl.SSLIOSessionStrategy;
import org.apache.http.ssl.SSLContextBuilder;
import org.opensearch.action.search.SearchRequest;
import org.opensearch.action.search.SearchResponse;
import org.opensearch.client.*;
import org.opensearch.index.query.WrapperQueryBuilder;
import org.opensearch.script.ScriptType;
import org.opensearch.script.mustache.SearchTemplateRequest;
import org.opensearch.script.mustache.SearchTemplateResponse;
import org.opensearch.search.builder.SearchSourceBuilder;

import javax.net.ssl.SSLContext;
import java.util.*;

public class Main {
    private static final ObjectMapper objectMapper = new ObjectMapper();
    RestHighLevelClient initRestHighLevelClientWithCA(List<HttpHost> hosts, String user, String password) throws Exception {
        if (hosts == null || hosts.isEmpty()) {
            throw new IllegalArgumentException("invalid empty hosts");
        }
        // add more parameters check here

        // identity information related
        final CredentialsProvider provider = new BasicCredentialsProvider();
        provider.setCredentials(AuthScope.ANY, new UsernamePasswordCredentials(user, password));

        SSLContext sslContext = new SSLContextBuilder().loadTrustMaterial(null, (x509Certificates, s) -> true).build();  // skip SSL certificate verification


        RestClientBuilder builder = RestClient.builder(hosts.toArray(new HttpHost[0]))
                .setHttpClientConfigCallback(httpClientBuilder -> httpClientBuilder
                        .setDefaultCredentialsProvider(provider)  // set authentication credentials
                        .setSSLStrategy(new SSLIOSessionStrategy(sslContext, NoopHostnameVerifier.INSTANCE))
                )  // skip HostName verification
                .setRequestConfigCallback(requestBuilder -> requestBuilder
                        .setConnectionRequestTimeout(5000)  // get max wait time for connection from the pool, adjust according to actual conditions
                        .setSocketTimeout(60000)  // request timeout, adjust according to actual conditions
                        .setConnectTimeout(5000));  // connection timeout, adjust based on actual conditions

        return new RestHighLevelClient(builder);
    }
    public static void main(String[] args) throws Exception {
        System.out.println("Hello world!");

        RestHighLevelClient client = new Main().initRestHighLevelClientWithCA(Arrays.asList(new HttpHost("xxx", 9200, "https")), "xxx", "xxx");
        // query original vector by doc id field
        SearchRequest searchRequest1 = new SearchRequest();
        SearchSourceBuilder searchSourceBuilder1 = new SearchSourceBuilder();
        searchSourceBuilder1.query(new WrapperQueryBuilder(
                "{\n" +
                        "    \"term\": {\n" +
                        "      \"id\": \"0a655b1f2c18632a534796bbf46a4ff7\"\n" +
                        "    }\n" +
                        "  }"
        ));
        searchRequest1.indices("imagesearch").source(searchSourceBuilder1);
        SearchResponse docRes = client.search(searchRequest1, RequestOptions.DEFAULT);
        String docJson = Arrays.stream(docRes.getHits().getHits()).findFirst().get().getSourceAsString();
        JsonNode docJsonRoot = objectMapper.readTree(docJson);
        // query vector
        List<Double> vecList = new ArrayList<>();
        for (JsonNode vecNode : docJsonRoot.get("vector")) {
            vecList.add(vecNode.asDouble());
        }

        // direct knn query
        SearchRequest searchRequest = new SearchRequest();
        SearchSourceBuilder searchSourceBuilder = new SearchSourceBuilder();
        searchSourceBuilder.query(new WrapperQueryBuilder(String.format("{\n" +
                "    \"knn\": {\n" +
                "      \"vector\": {\n" +
                "        \"vector\": " + objectMapper.writeValueAsString(vecList) + ",\n" +
                "        \"k\": 20\n" +
                "      }\n" +
                "    }\n" +
                "}")

        ));
        searchRequest.indices("imagesearch").source(searchSourceBuilder);
        SearchResponse responseKnn = client.search(searchRequest, RequestOptions.DEFAULT);
        System.out.println(responseKnn);
    }
} 
```



</Tab>
</Tabs>


<span id="Sxrk1iTO"></span>
### Adjust the number of shards as data volume increases

When the amount of data in an index continues to grow and more shards are needed, you can use the `_reindex` API to migrate data to a new index and configure more shards for the new index.


1. Obtain the original index `settings` and `mappings`.

   ```HTTP
   GET /{原索引名称}/_settings?pretty
   
   GET /{原索引名称}/_mapping?pretty
   ```
   

2. Create a new index based on the obtained `settings` and `mappings`. When creating, only keep necessary configurations; do not copy system\-generated settings such as `creation_date`, `uuid`, and `version`. Modify `number_of_shards` according to business needs.

   ```HTTP
   PUT /新索引名称
   {
     "settings": {
       "index": {
         "number_of_shards": 60,
         ...
       }
       ...
     },
     "mappings": { ... }  # 复制原索引的 mapping
   }
   ```
   

3. Use the `_reindex` API to migrate data from the original index to the new index.

   ```HTTP
   POST /_reindex?wait_for_completion=false
   {
     "source": {
       "index": "{原索引名称}"
     },
     "dest": {
       "index": "{新索引名称}"
     }
   }
   ```
   

4. After migration is complete, count the documents in both the original and new indices.

   ```HTTP
   GET /{原索引名称}/_count
   {
     "query": {
       "match_all": {}
     }
   }
   
   GET /{新索引名称}/_count
   {
     "query": {
       "match_all": {}
     }
   }
   ```
   

   If the document counts in both indices match, the data migration is complete.

5. After confirming the business switch is complete and data validation is correct, delete the original index.

   ```HTTP
   DELETE /{原索引名称}
   ```
   

6. Add the same alias to the new index as the original index, allowing the application to access data without modifying the index name.

   ```HTTP
   POST /_aliases
   {
     "actions": [
       { "add": { "alias": "{原索引名称}", "index": "{新索引名称}" } }
     ]
   }
   ```
