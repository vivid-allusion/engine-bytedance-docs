---
title: "embedding"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/embedding"
---

<span id="overview"></span>
# Overview

The Embedding interface converts unstructured content such as text, images, audio, and video into searchable feature vectors, supporting simultaneous output of dense and sparse vectors.


* The current Embedding service is primarily text\-oriented, with some models supporting multimodal input (text/image/video).

* The interface does not currently handle high\-concurrency requests; requests may be dropped when overloaded.


<span id="request-body-parameters"></span>
# Request Body Parameters


|Parameter |Type |Required |Sub\-parameter |Type |Required |Description |
|---|---|---|---|---|---|---|
|DenseModel |EmbeddingModelOpt |At least one of the two must be selected |ModelName |string |Yes |Model name. |
| | | |ModelVersion |string |No (required for Doubao models) |Model version. |
| | | |Dim |int |No |Dense vector dimension, uses model default when omitted. |
|SparseModel |EmbeddingModelOpt | |ModelName |string |Yes |Model name. |
| | | |ModelVersion |string |No |Model version. |
| | | |Dim |int |No |Output dimension of sparse vectors. |
|Data |[]EmbeddingData |Yes |Text |string |One of three must be selected |Plain text content. |
| | | |Image |interface{} |One of three must be selected |Image or image URL, follows MediaData specification. |
| | | |Video |interface{} |One of three must be selected |Video URL or configuration object, may include frame extraction parameters such as `fps` and `value`. |
| | | |FullModalSeq |interface{} |May be selected independently |Multimodal sequence input. Each element can further set `text`/`image`/`video` fields. |
|ProjectName |string |No | | | |Tenant project name, useful for distinguishing different environments. |


Media Field Description:


|Field |Type |Description |
|---|---|---|
|Text |string |UTF\-8 encoded plain text. |
|Image |interface{} |Can directly fill in image URL, or provide an object with authentication parameters according to MediaData specification. |
|Video |map[string]interface{} |Supports `value` (video URL) and `fps` (frame extraction frequency, default 1, range 0.2\-5.0, minimum 16 frames). |


<span id="model-list"></span>
## Model List


|Model Name |Model Version |Supported Vectorization Types |Default Dense Vector Dimension |Optional Dense Vector Dimensions |Text Truncation Length |Supports Sparse Vectors |Supports Instruction |
|---|---|---|---|---|---|---|---|
|bge\-large\-zh |(default) |text |1024 |1024 |512 |No |Yes |
|bge\-m3 |(default) |text |1024 |1024 |8192 |Yes |No |
|bge\-visualized\-m3 |(default) |text, image, and their combinations |1024 |1024 |8192 |No |No |
|Skylark\-embedding |*240715* |text |2048 |512, 1024, 2048 |4096 |No |Yes |
|Skylark\-embedding\-vision |*250615* |Compatible with *241215* usage. Additionally, supports `full_modal_seq` (text/image/video sequences). |2048 |2048, 1024 |128k |No |Yes |


<span id="response-parameters"></span>
# Response Parameters


|Field |Type |Description |
|---|---|---|
|RequestID |string |Request chain ID. |
|Code |string |Error code. |
|Message |string |Error message. |
|Api |string |API name. |
|Result |EmbeddingResult |Vectorization result, `null` on failure. |


EmbeddingResult Structure:


|Field |Type |Description |
|---|---|---|
|Data |[]Embedding |List of vector results corresponding to the request order. |
|TokenUsage |map[string]interface{} |Token usage statistics by model, including fields such as `prompt_tokens`, `completion_tokens`, `image_tokens`, `total_tokens`, etc. |


Embedding Structure:


|Field |Type |Description |
|---|---|---|
|DenseVectors |[]float32 |Dense vectors. |
|SparseVectors |map[string]float32 |Sparse vectors (keys are tokens, values are weights). |


<span id="example"></span>
# Example

```Go
package main

import (
    "context"
    "encoding/json"
    "fmt"
    "github.com/volcengine/vikingdb-go-sdk/vector"
    "github.com/volcengine/vikingdb-go-sdk/vector/model"
    "os"
    "time"
)

func valuePtr[T any](v T) *T {
    return &v
}

func main() {
    var (
       accessKey = os.Getenv("VIKINGDB_AK")
       secretKey = os.Getenv("VIKINGDB_SK")
       endpoint  = "https://api-vikingdb.vikingdb.ap-southeast-1.bytepluses.com"
       region    = "ap-southeast-1"
    )

    client, err := vector.New(
       vector.AuthIAM(accessKey, secretKey), // IAM auth
       vector.WithEndpoint(endpoint),
       vector.WithRegion(region),
       vector.WithTimeout(time.Second*30),
       vector.WithMaxRetries(3),
    )
    if err != nil {
       fmt.Println("New client failed, err: ", err)
       panic(err)
    }
    ctx := context.Background()

    var (
       text = "vikingdb is a vector database"
    )

    resp, err := client.Embedding().Embedding(ctx, model.EmbeddingRequest{
       DenseModel: &model.EmbeddingModelOpt{
          ModelName:    valuePtr("Skylark-embedding"),
          ModelVersion: valuePtr("240715"),
          Dim:          valuePtr(2048),
       },
       SparseModel: &model.EmbeddingModelOpt{
          ModelName:    valuePtr("bge-m3"),
          ModelVersion: valuePtr("default"),
          Dim:          valuePtr(1024),
       },
       Data: []*model.EmbeddingData{
          {
             Text: &text,
          },
       },
    })

    if err != nil {
       fmt.Println("Embedding failed, err: ", err)
       panic(err)
    }

    jsonData, err := json.Marshal(resp.Result)
    if err != nil {
       fmt.Println("Marshal result failed, err: ", err)
       panic(err)
    }
    fmt.Println(string(jsonData))
}
```
