---
title: "Rerank tuning"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Rerank_tuning"
---

During testing and production, you may find that some query results do not meet your expectations. For these scenarios where adjusting search performance is challenging, Cloud Search provides multiple tuning strategies. This document describes the rerank tuning solution.

<span id="b60c0e85"></span>
## Background

Cloud Search can encapsulate the entire hybrid search process within a single Pipeline. You can start a Rerank model, similar to a vector embedding model, and then configure it in the Search Pipeline.

You can directly use public Rerank models from Cloud Search, such as `cross-encoder`. Alternatively, you can create custom models by implementing the Rerank interface in the model processing. This allows you to develop business\-specific intervention logic for rapid tuning and deployment.


* Public model: select a Rerank model.

* Custom model: click **Create model** and upload the model file.


<span id="ed749e2a"></span>
## Rerank tuning configuration

In the Search Pipeline, add the Rerank model configuration using `response_processors` in the following example.

```JSON
PUT /_search/pipeline/my_pipeline
{
  "description": "Pipeline for reranking with a cross-encoder",
  "response_processors": [
    {
      "remote_rerank": {
        "ml_opensearch": {
          "remote_config": {    
            "method": "POST",
            "url": "http://d-18283223**-serve-svc.r-00g0so8**:8000/v1/rerank",
            "params": { // Mainly injects the token, key, etc., into the http url.
                "token": ""
            },
            "headers" : { // Mainly injects information into the http header, e.g., token and user.
                "Content-Type" : "application/json"
            },
            "advance_request_body" : { // Corresponds to the model in the OpenAI protocol.
                "model" : "cross-encoder/ms-marco-MiniLM-L-6-v2"
            }
          }
        },
        "context": {
          "document_fields": [
            "passage_text"
          ]
        }
      }
    }
  ]
}
```
