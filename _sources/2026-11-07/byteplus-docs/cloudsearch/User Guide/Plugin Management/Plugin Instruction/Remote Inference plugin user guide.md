---
title: "Remote Inference plugin user guide"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Remote_Inference_plugin_user_guide"
---

This topic describes the usage information related to the Remote Inference plugin.

## Background

`opensearch-remote-inference` is a vector enhancement plugin developed by the Cloud Search team, offering four operators: dense vector (`remote_embedding`), sparse vector (`sparse_encoding`), rerank (`remote_rerank`), and multimodal (`remote_multimodal_embedding`). When performing data read and write operations, you can use the corresponding operators in this plugin to automatically convert data types such as text and images into various vectors like dense vectors and sparse vectors. The `opensearch-remote-inference` plugin is ready to use out of the box. You do not need to understand the underlying complex algorithms and vectorization processes to use the plugin’s intelligent semantic read and write capabilities, significantly reducing the integration cost and complexity of related functions.

## Prerequisites

* The instance must be OpenSearch version 2.9.0. For specific procedures, refer to [Create an instance](https://docs.byteplus.com/docs/6465/1117829).

* The `opensearch-remote-inference` plugin is installed. For specific procedures, refer to [Manage system built-in plugins](https://docs.byteplus.com/docs/6465/1117832) to install plugins.

   > **说明**

   > The `opensearch-remote-inference` plugin is updating continuously. Some parameter configurations have version restrictions. Update the plugin to the latest version to use these features. For specific procedures, refer to [View system built\-in plugins](https://docs.byteplus.com/docs/6465/1288505) to check the extension version.

* Checked model service call examples in ContextSearch service and obtained values for `url` and `model` fields. For detailed steps, see [View an inference service](https://docs.byteplus.com/en/docs/86958/1904516).

## Usage methods

> **Execute the following code to create an index.说明**

BytePlus Cloud Search has introduced the DiskANN algorithm into OpenSearch, enabling lower\-cost vector storage and retrieval at larger data scales. We recommend using the DiskANN vector engine when creating an index. For details, see [Use DiskANN vector engine](https://docs.byteplus.com/docs/6465/1553583).

:::

```JSON
PUT multimodel_index 
{ 
    "mappings": { 
      "properties": { 
        "title": { 
          "type": "text" 
        }, 
        "summary_image": { 
          "type": "keyword" 
        }, 
        "abstract_knn": { 
          "type": "knn_vector", 
          "dimension": 2048, 
          "method": { 
            "name": "diskann", 
            "space_type": "cosinesimil", 
            "engine": "diskann", 
            "parameters": { 
              "R": 32, 
              "L": 32 
            } 
          } 
        } 
      } 
    }, 
    "settings": { 
      "index": { 
        "refresh_interval": "10s", 
        "number_of_shards": "1", 
        "knn": "true", 
        "number_of_replicas": "1" 
      } 
    } 
} 
```

3. execute the following command to write sample data.

   ```JSON
   PUT multimodel_index/_doc/1?pipeline=multimodal_embedding 
   { 
   ```

"title": "The sky is very blue, the sea is very deep",

"summary_image": "https://ark\-project.tos\-cn\-beijing.volces.com/images/view.jpeg"

}

POST multimodel_index/_doc/2?pipeline=multimodal_embedding

{

"summary_image": "https://ark\-project.tos\-cn\-beijing.volces.com/images/view.jpeg"

}

POST multimodel_index/_doc/3?pipeline=multimodal_embedding

{

"title": "test_text"

}

```Plain Text

4. execute the following code to create search pipeline. 
:::tip 
the parameters in the code below are explained as follows: 

* `description`: set the `search pipeline` description information. 
* `request_processors`: specify the configuration parameters for the `remote_multimodal_embedding` operator. For detailed explanations of each parameter in the `remote_multimodal_embedding` operator, see [Query search pipeline configuration parameters](/docs/6465/1588139#69695eb6.)
::: 
```JSON 
PUT _search/pipeline/multimodel_search_embedding 
{ 
  "description": "text embedding pipeline for remote inference", 
  "request_processors": [ 
    { 
      "remote_multimodal_embedding": { 
        "remote_config": { 
          "method": "POST", 
          "url": "https://ark.cn-beijing.volces.com/api/v3/embeddings/multimodal", 
          "params": {}, 
          "headers": { 
            "Content-Type": "application/json", 
"Authorization": "Bearer {API KEY}"    // API KEY obtained from Ark platform 
          }, 
          "advance_request_body": { 
            "model": "doubao-embedding-vision-241215" 
          } 
        } 
      } 
    } 
  ] 
} 
```

5. Execute the following command to query data.

   ```JSON
   GET multimodel_index/_search?search_pipeline=multimodel_search_embedding 
   { 
     "size": 10, 
     "_source": { 
       "includes": ["title", "summary_image"] 
     }, 
     "query": { 
       "remote_multimodal_neural": { 
         "abstract_knn": { 
           "query_text": "blue", 
           "query_image": "https://ark-project.tos-cn-beijing.volces.com/images/view.jpeg", 
           "k": 10 
         } 
       } 
     } 
   } 
   ```

`}\></Tabs.TabPane\>

**Dense Vector (remote_embedding)**

{`<span

**Sparse Vector (sparse_encoding)**

{`<span

**Re\-ranking (remote_rerank)**

{`<span

);

```Plain Text

<span id="8085f268"></span>

## Parameter configuration

<span id="bc97d139"></span>

### Dense vector (`remote_embedding`)

<span id="000fc7e0"></span>

#### Set parameters for the ingest pipeline write configuration

:::tip 
When creating a write ingest pipeline using the dense vector (`remote_embedding`) operator, you can configure the parameters listed below in the operator's `processors.remote_embedding` field according to your business needs. 
:::

````mixin-react
const properties = ({ 
columns:[ 
  { 
"title": "Name", 
    "dataIndex": "name" 
  }, 
  { 
"title": "Type", 
    "dataIndex": "type" 
  }, 
  { 
"title": "Required?", 
    "dataIndex": "required" 
  }, 
  { 
"title": "Parameter Description", 
    "dataIndex": "example", 
    "render": (val) => <RenderMd content={val} /> 
  }, 
  { 
"title": "Supported extension version", 
    "dataIndex": "title", 
    "render": (val) => <RenderMd content={val} /> 
  } 
], 
data:[ 
  { 
    "name": "remote_config", 
    "key": "0-0", 
"title": "See the supported extension versions for each parameter.", 
"example": "Configuration information for the remote service.", 
"required": "Yes" 
    "type": "Object", 
    "children": [ 
      { 
        "name": "method", 
        "key": "0-0-0", 
"title": "All versions." 
"example": "method to request remote service, e.g., `POST`, `GET`, etc.", 
"required": "Yes", 
        "type": "String" 
      }, 
      { 
        "name": "url", 
        "key": "0-0-1", 
"title": "all Versions.", 
"example": "the address for requesting remote services, e.g. \n`https://example_url.com`.", 
"required": "Yes", 
        "type": "String" 
      }, 
      { 
        "name": "headers", 
        "key": "0-0-2", 
"title": "all versions.", 
"example": "headers information for requesting remote service.\ne.g., you can add the following code in headers to specify the data format and verification information for requests or responses.\n```JSON\n{\n        "Content-Type": "application/json",\n        "Authorization": "auth_demo"\n}\n```", 
"required": "No", 
        "type": "JSONMap", 
        "children": [] 
      }, 
      { 
        "name": "params", 
        "key": "0-0-3", 
"title": "All versions." 
"example": "URL parameter information for requesting remote services.", 
"required": "No", 
        "type": "JSONMap", 
        "children": [] 
      }, 
      { 
        "name": "advance_request_body", 
        "key": "0-0-4", 
"title": "All versions." 
"example": "Request the body information of the remote service.\nE.g., you can add the following code in the body to specify the model information.\n```JSON\n{\n        "model": "model_demo"\n}\n```", 
required: No 
        "type": "JSONMap" 
      }, 
      { 
        "name": "timeout", 
        "key": "0-0-5", 
"title": "2.9.0.0-24.10.31 and later versions." ", 
"example": "Timeout configuration for requesting remote services.", \nSupports the following common time units: `d` (days), `h` (hours), `m` (minutes), `s` (seconds), `ms` (milliseconds), etc.", The default is `5s`.", \nFor more information on supported time units, refer to [Unit](https://docs.opensearch.org/docs/latest/api-reference/units/).", ", 
required: No 
        "type": "String" 
      } 
    ] 
  }, 
  { 
    "name": "field_map", 
    "key": "0-1", 
"title": "all versions." ", 
"example": "specify the mapping relationship between the input text field and the vector field generated by the model transformation." "\ne.g., you can establish a mapping between the text field and the vector field using the following code.", "\n```JSON\n{\n        // map the title field to the title_knn field\n        "title": "title_knn",\n        // chunks is a nested field\n        // the text field in chunks maps to the text_knn field\n        "chunks": {\n                "text": "text_knn"\n        }\n}\n```", 
required": "Yes", 
    "type": "JSONMap", 
    "children": [] 
  }, 
  { 
    "name": "batch_size", 
    "key": "0-2", 
"title": "Version 2.9.0.0-24.10.31 and above.", ", 
"example": "The number of data items carried in a single request to the remote service, default is 1.", ", 
"required": "No", 
    "type": "Integer" 
  }, 
  { 
    "name": "sliced_norm_dim", 
    "key": "0-3", 
"title": "version 2.9.0.0-25.1.0 and above.", ", 
"example": "specify the compressed dimension.", ", 
"required": "No", 
    "type": "Integer" 
  }, 
  { 
    "name": "max_tokens", 
    "key": "0-4", 
"title": "Version 2.9.0.0-25.7.0 and above." ", 
"example": "Specify the maximum tokens; exceeding tokens will be automatically truncated, and the truncated result will be vectorized." ", 
"required": "No", 
    "type": "Integer" 
  } 
] 
}); 
return <Table border={{ cell: true, wrapper: true }} pagination={false} {...properties} />;
```

#### query search pipeline configuration parameters

> **说明**

> when using the dense vector (`remote_embedding`) operator in the query search pipeline, you can configure the parameters listed below in the operator's `processors.remote_embedding` field according to business needs.

```mixin-react
const properties = ({ 
columns:[ 
  { 
"title": "Name", 
    "dataIndex": "name" 
  }, 
  { 
"title": "Type", 
    "dataIndex": "type" 
  }, 
  { 
"title": "Required?", 
    "dataIndex": "required" 
  }, 
  { 
"title": "Parameter Description", 
    "dataIndex": "example", 
    "render": (val) => <RenderMd content={val} /> 
  }, 
  { 
"title": "Supported extension version", 
    "dataIndex": "title", 
    "render": (val) => <RenderMd content={val} /> 
  } 
], 
data:[ 
  { 
    "name": "remote_config", 
    "key": "0-0", 
"title": "See the supported extension versions for each parameter.", 
"example": "Configuration information for the remote service.", 
"required": "Yes" 
    "type": "Object", 
    "children": [ 
      { 
        "name": "method", 
        "key": "0-0-0", 
"title": "All versions." 
"example": "method to request remote service, e.g., `POST`, `GET`, etc.", 
"required": "Yes", 
        "type": "String" 
      }, 
      { 
        "name": "url", 
        "key": "0-0-1", 
"title": "all Versions.", 
"example": "address of the remote service request, e.g., \n`https://example_url.com`.", 
required: No 
        "type": "String" 
      }, 
      { 
        "name": "headers", 
        "key": "0-0-2", 
"title": "all versions.", 
"example": "headers information for requesting remote service.\ne.g., you can add the following code in headers to specify the data format and verification information for requests or responses.\n```JSON\n{\n        "Content-Type": "application/json",\n        "Authorization": "auth_demo"\n}\n```", 
"required": "No", 
        "type": "JSONMap", 
        "children": [] 
      }, 
      { 
        "name": "params", 
        "key": "0-0-3", 
"title": "All versions." 
"example": "URL parameter information for requesting remote services.", 
"required": "No", 
        "type": "JSONMap", 
        "children": [] 
      }, 
      { 
        "name": "advance_request_body", 
        "key": "0-0-4", 
"title": "All versions." 
"example": "Request the body information of the remote service.\nE.g., you can add the following code in the body to specify the model information.\n```JSON\n{\n        "model": "model_demo"\n}\n```", 
required: No 
        "type": "JSONMap" 
      }, 
      { 
        "name": "timeout", 
        "key": "0-0-5", 
"title": "2.9.0.0-24.10.31 and later versions." ", 
"example": "Timeout configuration for requesting remote services.", \nSupports the following common time units: `d` (days), `h` (hours), `m` (minutes), `s` (seconds), `ms` (milliseconds), etc.", The default is `5s`.", \nFor more information on supported time units, refer to [Unit](https://docs.opensearch.org/docs/latest/api-reference/units/).", ", 
required: No 
        "type": "String" 
      } 
    ] 
  }, 
  { 
    "name": "sliced_norm_dim", 
    "key": "0-1", 
"title": "Version 2.9.0.0-25.1.0 and above.", ", 
"example": "specify the compressed dimension.", ", 
"required": "No", 
    "type": "Integer" 
  }, 
  { 
    "name": "support_fields", 
    "key": "0-2", 
"title": "Versions 2.9.0.0-25.7.0 and above." ", 
"example": "Specify supported fields, wildcards allowed. Example:\n```JSON\n{\n        \"support_fields\": [\"field1\", \"field2*\"]\n}\n```", 
"required": "No", 
    "type": "List" 
  } 
] 
}); 
return <Table border={{ cell: true, wrapper: true }} pagination={false} {...properties} />;
```

### Sparse vector (`sparse_encoding`)

#### write ingest pipeline configuration parameters

> **说明**

> When creating an ingest pipeline that uses the sparse vector (`sparse_encoding`) operator, you can configure the parameters in the table below in the operator's `processors.sparse_encoding` field according to your business needs.

```mixin-react
const properties = ({ 
columns:[ 
  { 
"title": "Name", 
    "dataIndex": "name" 
  }, 
  { 
"title": "Type", 
    "dataIndex": "type" 
  }, 
  { 
"title": "Required?", 
    "dataIndex": "required" 
  }, 
  { 
"title": "Parameter Description", 
    "dataIndex": "example", 
    "render": (val) => <RenderMd content={val} /> 
  }, 
  { 
"title": "Supported extension version", 
    "dataIndex": "title", 
    "render": (val) => <RenderMd content={val} /> 
  } 
], 
data:[ 
  { 
    "name": "remote_config", 
    "key": "0-0", 
"title": "See the supported extension versions for each parameter.", 
"example": "Configuration information for the remote service.", 
"required": "Yes" 
    "type": "Object", 
    "children": [ 
      { 
        "name": "method", 
        "key": "0-0-0", 
"title": "All versions." 
"example": "method to request remote service, e.g., `POST`, `GET`, etc.", 
"required": "Yes", 
        "type": "String" 
      }, 
      { 
        "name": "url", 
        "key": "0-0-1", 
"title": "all Versions.", 
"example": "the address for requesting remote services, e.g. \n`https://example_url.com`.", 
"required": "Yes", 
        "type": "String" 
      }, 
      { 
        "name": "headers", 
        "key": "0-0-2", 
"title": "all versions.", 
"example": "headers information for requesting remote service.\ne.g., you can add the following code in headers to specify the data format and verification information for requests or responses.\n```JSON\n{\n        "Content-Type": "application/json",\n        "Authorization": "auth_demo"\n}\n```", 
"required": "No", 
        "type": "JSONMap", 
        "children": [] 
      }, 
      { 
        "name": "params", 
        "key": "0-0-3", 
"title": "All versions." 
"example": "URL parameter information for requesting remote services.", 
"required": "No", 
        "type": "JSONMap", 
        "children": [] 
      }, 
      { 
        "name": "advance_request_body", 
        "key": "0-0-4", 
"title": "All versions." 
"example": "Request the body information of the remote service.\nE.g., you can add the following code in the body to specify the model information.\n```JSON\n{\n        "model": "model_demo"\n}\n```", 
required: No 
        "type": "JSONMap" 
      }, 
      { 
        "name": "timeout", 
        "key": "0-0-5", 
"title": "2.9.0.0-24.10.31 and later versions." ", 
"example": "Timeout configuration for requesting remote services.", \nSupports the following common time units: `d` (days), `h` (hours), `m` (minutes), `s` (seconds), `ms` (milliseconds), etc.", The default is `5s`.", \nFor more information on supported time units, refer to [Unit](https://docs.opensearch.org/docs/latest/api-reference/units/).", ", 
required: No 
        "type": "String" 
      } 
    ] 
  }, 
  { 
    "name": "field_map", 
    "key": "0-1", 
"title": "all versions." ", 
"example": "specify the mapping relationship between the input text field and the vector field generated by the model transformation." "\ne.g., you can establish a mapping between the text field and the vector field with the following code." "\n```JSON\n{\n        // map the title field to title_sparse field\n        "title": "title_sparse",\n\n        // chunks is a nested field\n        // the text field in chunks maps to title_sparse field\n        "chunks": {\n                "text": "title_sparse"\n        }\n}\n```," 
required": "Yes", 
    "type": "JSONMap", 
    "children": [] 
  }, 
  { 
    "name": "batch_size", 
    "key": "0-2", 
"title": "Version 2.9.0.0-24.10.31 and above.", ", 
"example": "The number of data items carried in a single request to the remote service, default is 1.", ", 
"required": "No", 
    "type": "Integer" 
  }, 
  { 
    "name": "sliced_norm_dim", 
    "key": "0-3", 
"title": "version 2.9.0.0-25.1.0 and above.", ", 
"example": "specify the compressed dimension.", ", 
"required": "No", 
    "type": "Integer" 
  } 
] 
}); 
return <Table border={{ cell: true, wrapper: true }} pagination={false} {...properties} />;
```

#### Query search pipeline configuration parameters

> **说明**

> You can configure the parameters in the table below in the `processors.sparse_encoding` field of the `sparse_encoding` operator in the query search pipeline according to business needs.

```mixin-react
const properties = ({ 
columns:[ 
  { 
"title": "Name", 
    "dataIndex": "name" 
  }, 
  { 
"title": "Type", 
    "dataIndex": "type" 
  }, 
  { 
"title": "Required?", 
    "dataIndex": "required" 
  }, 
  { 
"title": "Parameter Description", 
    "dataIndex": "example", 
    "render": (val) => <RenderMd content={val} /> 
  }, 
  { 
"title": "Supported extension version", 
    "dataIndex": "title", 
    "render": (val) => <RenderMd content={val} /> 
  } 
], 
data:[ 
  { 
    "name": "remote_config", 
    "key": "0-0", 
"title": "See the supported extension versions for each parameter.", 
"example": "Configuration information for the remote service.", 
"required": "Yes" 
    "type": "Object", 
    "children": [ 
      { 
        "name": "method", 
        "key": "0-0-0", 
"title": "All versions." 
"example": "method to request remote service, e.g., `POST`, `GET`, etc.", 
"required": "Yes", 
        "type": "String" 
      }, 
      { 
        "name": "url", 
        "key": "0-0-1", 
"title": "all Versions.", 
"example": "address of the remote service request, e.g., \n`https://example_url.com`.", 
required: No 
        "type": "String" 
      }, 
      { 
        "name": "headers", 
        "key": "0-0-2", 
"title": "all versions.", 
"example": "headers information for requesting remote service.\ne.g., you can add the following code in headers to specify the data format and verification information for requests or responses.\n```JSON\n{\n        "Content-Type": "application/json",\n        "Authorization": "auth_demo"\n}\n```", 
"required": "No", 
        "type": "JSONMap", 
        "children": [] 
      }, 
      { 
        "name": "params", 
        "key": "0-0-3", 
"title": "All versions." 
"example": "URL parameter information for requesting remote services.", 
"required": "No", 
        "type": "JSONMap", 
        "children": [] 
      }, 
      { 
        "name": "advance_request_body", 
        "key": "0-0-4", 
"title": "All versions." 
"example": "Request body information for remote services.\nE.g., you can add the following code in the body to specify the model information.\n```JSON\n{\n        "model": "model_demo"\n}\n```", 
required: No 
        "type": "JSONMap" 
      }, 
      { 
        "name": "timeout", 
        "key": "0-0-5", 
"title": "2.9.0.0-24.10.31 and later versions." ", 
"example": "Timeout configuration for requesting remote services.", \nSupports the following common time units: `d` (days), `h` (hours), `m` (minutes), `s` (seconds), `ms` (milliseconds), etc.", The default is `5s`.", \nFor more information on supported time units, refer to [Unit](https://docs.opensearch.org/docs/latest/api-reference/units/).", ", 
required: No 
        "type": "String" 
      } 
    ] 
  }, 
  { 
    "name": "sliced_norm_dim", 
    "key": "0-1", 
"title": "Version 2.9.0.0-25.1.0 and above.", ", 
"example": "specify the compressed dimension.", ", 
"required": "No", 
    "type": "Integer" 
  }, 
  { 
    "name": "support_fields", 
    "key": "0-2", 
"title": "Versions 2.9.0.0-25.7.0 and above." ", 
"example": "Specify supported fields, wildcards allowed. Example:\n```JSON\n{\n        \"support_fields\": [\"field1\", \"field2*\"]\n}\n```", 
"required": "No", 
    "type": "List" 
  } 
] 
}); 
return <Table border={{ cell: true, wrapper: true }} pagination={false} {...properties} />;
```

### Multimodal (`remote_multimodal_embedding`)

#### write ingest pipeline configuration parameters

> **说明**

> When creating a write ingest pipeline using the multimodal (`remote_multimodal_embedding`) operator, you can configure the parameters in the following table in the operator's `processors.remote_multimodal_embedding` field according to business needs.

```mixin-react
const properties = ({ 
columns:[ 
  { 
"title": "Name", 
    "dataIndex": "name" 
  }, 
  { 
"title": "Type", 
    "dataIndex": "type" 
  }, 
  { 
"title": "Required?", 
    "dataIndex": "required" 
  }, 
  { 
"title": "Parameter Description", 
    "dataIndex": "example", 
    "render": (val) => <RenderMd content={val} /> 
  }, 
  { 
"title": "Supported extension version", 
    "dataIndex": "title", 
    "render": (val) => <RenderMd content={val} /> 
  } 
], 
data:[ 
  { 
    "name": "remote_config", 
    "key": "0-0", 
"title": "See the supported extension versions for each parameter.", 
"example": "Configuration information for the remote service.", 
"required": "Yes" 
    "type": "Object", 
    "children": [ 
      { 
        "name": "method", 
        "key": "0-0-0", 
"title": "version 2.9.0.0 to 25.3.0 and above.", 
"example": "Method to request remote service, e.g., `POST`, `GET`, etc.", 
"required": "Yes", 
        "type": "String" 
      }, 
      { 
        "name": "url", 
        "key": "0-0-1", 
"title": "Version 2.9.0.0-25.3.0 and above.", 
"example": "The address to request the remote service, e.g., \n`https://example_url.com`.", 
"required": "Yes", 
        "type": "String" 
      }, 
      { 
        "name": "headers", 
        "key": "0-0-2", 
"title": "version 2.9.0.0 to 25.3.0 and above.", 
"example": "Request headers information for remote services.\nFor example, you can add the following code in headers to specify the data format and verification information for requests or responses.\n```JSON\n{\n        \"Content-Type\": \"application/json\",\n        \"Authorization\": \"auth_demo\"\n}\n```", 
"required": "No", 
        "type": "JSONMap", 
        "children": [] 
      }, 
      { 
        "name": "params", 
        "key": "0-0-3", 
"title": "version 2.9.0.0 to 25.3.0 and above.", 
"example": "URL parameter information for requesting remote services.", 
"required": "No", 
        "type": "JSONMap", 
        "children": [] 
      }, 
      { 
        "name": "advance_request_body", 
        "key": "0-0-4", 
"title": "version 2.9.0.0 to 25.3.0 and above.", 
"example": "Request the body information of the remote service.\nFor example, you can add the following code in the body to specify the model information.\n```JSON\n{\n        "model": "model_demo"\n}\n```", 
required: No 
        "type": "JSONMap" 
      }, 
      { 
        "name": "timeout", 
        "key": "0-0-5", 
"title": "version 2.9.0.0-25.3.0 and above." ", 
"example": "Timeout configuration for requesting remote services.", \nSupports the following common time units: `d` (days), `h` (hours), `m` (minutes), `s` (seconds), `ms` (milliseconds), etc.", The default is `5s`.", \nFor more information on supported time units, refer to [Unit](https://docs.opensearch.org/docs/latest/api-reference/units/).", ", 
required: No 
        "type": "String" 
      } 
    ] 
  }, 
  { 
    "name": "field_map", 
    "key": "0-1", 
"title": "Version 2.9.0.0-25.3.0 and above.", ", 
"example": "Specify the mapping between the input text fields and the vector fields generated through model transformation.", "\nFor example, you can use the following code to store the vector data converted from the text field (`title`) and picture field (`summary_image`) into the vector field (`abstract_knn`).", \n```JSON\n{\n        "text": "title",\n        "image": "summary_image",\n        "embedding": "abstract_knn"\n}\n```", 
required": "Yes", 
    "type": "JSONMap", 
    "children": [] 
  } 
] 
}); 
return <Table border={{ cell: true, wrapper: true }} pagination={false} {...properties} />;
```

#### Query search pipeline configuration parameters

> **说明**

> When using the multimodal (`remote_multimodal_embedding`) operator in a search pipeline query, you can configure the parameters in the operator's `request_processors.remote_multimodal_embedding` field according to business needs.

```mixin-react
const properties = ({ 
columns:[ 
  { 
"title": "Name", 
    "dataIndex": "name" 
  }, 
  { 
"title": "Type", 
    "dataIndex": "type" 
  }, 
  { 
"title": "Required?", 
    "dataIndex": "required" 
  }, 
  { 
"title": "Parameter Description", 
    "dataIndex": "example", 
    "render": (val) => <RenderMd content={val} /> 
  }, 
  { 
"title": "Supported extension version", 
    "dataIndex": "title", 
    "render": (val) => <RenderMd content={val} /> 
  } 
], 
data:[ 
  { 
    "name": "remote_config", 
    "key": "0-0", 
"title": "See the supported extension versions for each parameter.", 
"example": "Configuration information for the remote service.", 
"required": "Yes" 
    "type": "Object", 
    "children": [ 
      { 
        "name": "method", 
        "key": "0-0-0", 
"title": "version 2.9.0.0 to 25.3.0 and above.", 
"example": "Method to request remote service, e.g., `POST`, `GET`, etc.", 
"required": "Yes", 
        "type": "String" 
      }, 
      { 
        "name": "url", 
        "key": "0-0-1", 
"title": "Version 2.9.0.0-25.3.0 and above.", 
"example": "Address to request remote service, e.g., \n`https://example_url.com`.", 
required: No 
        "type": "String" 
      }, 
      { 
        "name": "headers", 
        "key": "0-0-2", 
"title": "version 2.9.0.0 to 25.3.0 and above.", 
"example": "Request headers information for remote services.\nFor example, you can add the following code in headers to specify the data format and verification information for requests or responses.\n```JSON\n{\n        \"Content-Type\": \"application/json\",\n        \"Authorization\": \"auth_demo\"\n}\n```", 
"required": "No", 
        "type": "JSONMap", 
        "children": [] 
      }, 
      { 
        "name": "params", 
        "key": "0-0-3", 
"title": "version 2.9.0.0 to 25.3.0 and above.", 
"example": "URL parameter information for requesting remote services.", 
"required": "No", 
        "type": "JSONMap", 
        "children": [] 
      }, 
      { 
        "name": "advance_request_body", 
        "key": "0-0-4", 
"title": "version 2.9.0.0 to 25.3.0 and above.", 
"example": "Request the body information of the remote service.\nFor example, you can add the following code in the body to specify the model information.\n```JSON\n{\n        "model": "model_demo"\n}\n```", 
required: No 
        "type": "JSONMap" 
      }, 
      { 
        "name": "timeout", 
        "key": "0-0-5", 
"title": "version 2.9.0.0-25.3.0 and above." ", 
"example": "Timeout configuration for requesting remote services.", \nSupports the following common time units: `d` (days), `h` (hours), `m` (minutes), `s` (seconds), `ms` (milliseconds), etc.", The default is `5s`.", \nFor more information on supported time units, refer to [Unit](https://docs.opensearch.org/docs/latest/api-reference/units/).", ", 
required: No 
        "type": "String" 
      } 
    ] 
  } 
] 
}); 
return <Table border={{ cell: true, wrapper: true }} pagination={false} {...properties} />;
```

### rerank (`remote_rerank`)

#### Query search pipeline configuration parameters

> **说明**

> When creating a query search pipeline using the rerank (`remote_rerank`) operator, you can configure the parameters in the table below under the operator's `response_processors.remote_rerank` field according to your business needs.

```mixin-react
const properties = ({ 
columns:[ 
  { 
"title": "Name", 
    "dataIndex": "name" 
  }, 
  { 
"title": "Type", 
    "dataIndex": "type" 
  }, 
  { 
"title": "Required?", 
    "dataIndex": "required" 
  }, 
  { 
"title": "Parameter Description", 
    "dataIndex": "example", 
    "render": (val) => <RenderMd content={val} /> 
  }, 
  { 
"title": "Supported extension version", 
    "dataIndex": "title", 
    "render": (val) => <RenderMd content={val} /> 
  } 
], 
data:[ 
  { 
    "name": "ml_opensearch.remote_config", 
    "key": "0-0", 
"title": "See the supported extension versions for each parameter.", 
"example": "Configuration information for the remote service.", 
"required": "Yes" 
    "type": "Object", 
    "children": [ 
      { 
        "name": "method", 
        "key": "0-0-0", 
"title": "All versions." 
"example": "method to request remote service, e.g., `POST`, `GET`, etc.", 
"required": "Yes", 
        "type": "String" 
      }, 
      { 
        "name": "url", 
        "key": "0-0-1", 
"title": "all Versions.", 
"example": "address of the remote service request, e.g., \n`https://example_url.com`.", 
required: No 
        "type": "String" 
      }, 
      { 
        "name": "headers", 
        "key": "0-0-2", 
"title": "all versions.", 
"example": "headers information for requesting remote service.\ne.g., you can add the following code in headers to specify the data format and verification information for requests or responses.\n```JSON\n{\n        "Content-Type": "application/json",\n        "Authorization": "auth_demo"\n}\n```", 
"required": "No", 
        "type": "JSONMap", 
        "children": [] 
      }, 
      { 
        "name": "params", 
        "key": "0-0-3", 
"title": "All versions." 
"example": "URL parameter information for requesting remote services.", 
"required": "No", 
        "type": "JSONMap", 
        "children": [] 
      }, 
      { 
        "name": "advance_request_body", 
        "key": "0-0-4", 
"title": "All versions." 
"example": "Request the body information of the remote service.\nE.g., you can add the following code in the body to specify the model information.\n```JSON\n{\n        "model": "model_demo"\n}\n```", 
required: No 
        "type": "JSONMap" 
      }, 
      { 
        "name": "timeout", 
        "key": "0-0-5", 
"title": "2.9.0.0-24.10.31 and later versions." ", 
"example": "Timeout configuration for requesting remote services.", \nSupports the following common time units: `d` (days), `h` (hours), `m` (minutes), `s` (seconds), `ms` (milliseconds), etc.", The default is `5s`.", \nFor more information on supported time units, refer to [Unit](https://docs.opensearch.org/docs/latest/api-reference/units/).", ", 
required: No 
        "type": "String" 
      } 
    ] 
  }, 
  { 
    "name": "context", 
    "key": "0-1", 
"title": "See the supported extension versions for each parameter.", ", 
"example": "Index information." ", 
"required": "No", 
    "type": "Object", 
    "children": [ 
      { 
        "name": "document_fields", 
        "key": "0-1-0", 
"title": "all versions." ", 
"example": "Extract relevant data from specific fields in the indexed document, and send this data along with other related information (e.g., query questions) to a remote service for re-ranking." e.g., when `document_fields` is set to `text_representation`, it means ES will get the results for reranking from the `text_representation` field. ", 
"required": "Yes", 
        "type": "String[]", 
        "children": [] 
      } 
    ] 
  } 
] 
}); 
return <Table border={{ cell: true, wrapper: true }} pagination={false} {...properties} />;
```

#### Query statement configuration parameters

> **说明**

> When using the rerank (`remote_rerank`) operator in your query statement, you can configure the parameters below in the operator’s `ext.remote_rerank` field according to business needs.

```mixin-react
const properties = ({ 
columns:[ 
  { 
"title": "Name", 
    "dataIndex": "name" 
  }, 
  { 
"title": "Type", 
    "dataIndex": "type" 
  }, 
  { 
"title": "Required?", 
    "dataIndex": "required" 
  }, 
  { 
"title": "Parameter Description", 
    "dataIndex": "example", 
    "render": (val) => <RenderMd content={val} /> 
  }, 
  { 
"title": "Supported extension version", 
    "dataIndex": "title", 
    "render": (val) => <RenderMd content={val} /> 
  } 
], 
data:[ 
  { 
    "name": "query_context", 
    "key": "0-0", 
"title": "See the supported extension versions for each parameter.", 
"example": "Configuration information for the remote service.", 
"required": "Yes" 
    "type": "Object", 
    "children": [ 
      { 
        "name": "query_text", 
        "key": "0-0-0", 
"title": "All versions." 
"example": "Query sentences that require reordering will be used together with the search results from OpenSearch for reranking.", 
"required": "Yes", 
        "type": "String" 
      } 
    ] 
  }, 
  { 
    "name": "appending_contexts", 
    "key": "0-1", 
"title": "Version 2.9.0.0-24.10.31 and above.", 
"example": "Retrieve data from specified fields and send this data along with OpenSearch query results to a remote service for reranking to produce a final result better suited to your needs.\nFor example, you can pass the information `[\"I like fish.\", \"He likes fish too.\"]` in `appending_contexts`; these two texts will be used together with OpenSearch query results for reranking.", 
"required": "No", 
    "type": "String[]", 
    "children": [] 
  }, 
  { 
    "name": "rerank_prompt", 
    "key": "0-2", 
"title": "version 2.9.0.0-25.1.0 and above.", 
"example": "Retrieve related data from specified fields in the query results and format it, then send the formatted result to a remote server for reranking.\nFor example, you can pass the message \n`This is {{text1}} \\n That is {{text2}} Ending.` in `rerank_prompt`, the instance will replace `text1` and `text2` with values obtained from the specified query result fields, and then rerank the formatted outcome.", ", 
"required": "No", 
    "type": "String" 
  }, 
  { 
    "name": "keep_previous_score", 
    "key": "0-3", 
"title": "version 2.9.0.0-25.7.0 and above." ", 
"example": "Whether to retain the score before reordering. Return example:\n```JSON\n{\n        \"_score\": \"0.7439\",\n        \"fields\": {\n            \"previous_score\": [\n                1.0\n            ]\n      }\n}\n```", 
"required": "No", 
    "type": "Boolean" 
  }, 
  { 
    "name": "min_score", 
    "key": "0-4", 
"title": "Version 2.9.0.0-25.7.0 and above." ", 
"example": "Specify the score threshold for reordered return; only scores above this threshold will be returned." ", 
"required": "No", 
    "type": "String" 
  } 
] 
}); 
return <Table border={{ cell: true, wrapper: true }} pagination={false} {...properties} />;
```

## More use cases

[Practice of hybrid search and reranking based on Cloud Search](https://docs.byteplus.com/docs/6465/1397593)
