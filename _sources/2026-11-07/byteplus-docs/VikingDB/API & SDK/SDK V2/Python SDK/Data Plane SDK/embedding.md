---
title: "embedding"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/embeddingv2"
---

<span id="overview"></span>
# Overview

The Embedding interface converts unstructured content such as text, images, audio, and video into retrievable feature vectors, supporting simultaneous output of dense and sparse vectors.


* The current Embedding service is primarily designed for text, with some models supporting multimodal input (text/image/video).

* The interface does not currently support high\-concurrency requests; requests may be dropped when overloaded.


<span id="request-body-parameters"></span>
# Request Body Parameters


|Parameter |Type |Required |Sub\-parameter |Type |Required |Description |
|---|---|---|---|---|---|---|
|dense_model |Optional[EmbeddingModelOpt] |At least one required |name |str |Yes |Model name. |
| | | |version |Optional[str] |No (required for Doubao models) |Model version. |
| | | |dim |Optional[int] |No |Dense vector dimension, uses model default when omitted. |
|sparse_model |Optional[EmbeddingModelOpt] | |name |str |Yes |Model name. |
| | | |version |Optional[str] |No |Model version. |
| | | |dim |Optional[int] |No |Output dimension of sparse vector. |
|data |List[EmbeddingData] |Yes |text |Optional[str] |Choose one |Plain text content. |
| | | |image |Optional[Any] |Choose one |Image or image URL, follows MediaData specification. |
| | | |video |Optional[Any] |Choose one |Video URL or configuration object, may include frame extraction parameters such as `fps`, `value`, etc. |
| | | |full_modal_seq |Optional[List[FullModalData]] |No |Multimodal sequence input. Each element may set `text`/`image`/`video` fields. |
|project_name |Optional[str] |No | | | |Tenant project name, for distinguishing different environments. |


Media Field Description:


|Field |Type |Description |
|---|---|---|
|text |str |UTF\-8 encoded plain text. |
|image |str or Dict[str, Any] |May directly fill in image URL, or provide an object with authentication parameters according to MediaData specification. |
|video |Dict[str, Any] |Supports `value` (video URL) and `fps` (frame extraction frequency, default 1, range 0.2\-5.0, minimum 16 frames). |


<span id="model-list"></span>
## Model List


|Model Name |Model Version |Supported Vectorization Types |Default Dense Vector Dimension |Optional Dense Vector Dimensions |Text Truncation Length |Supports Sparse Vector |Supports instruction |
|---|---|---|---|---|---|---|---|
|bge\-large\-zh |(default) |text |1024 |1024 |512 |No |Yes |
|bge\-m3 |(default) |text |1024 |1024 |8192 |Yes |No |
|bge\-visualized\-m3 |(default) |text, image and their combinations |1024 |1024 |8192 |No |No |
|Skylark\-embedding |*240715* |text |2048 |512, 1024, 2048 |4096 |No |Yes |
|Skylark\-embedding\-vision |*250615* |Compatible with usage of *241215*. Additionally supports full_modal_seq (text/image/video sequences) |2048 |2048, 1024 |128k |No |Yes |


<span id="response-parameters"></span>
# Response Parameters


|Field |Type |Description |
|---|---|---|
|request_id |Optional[str] |Request trace ID. |
|code |Optional[str] |Error code. |
|message |Optional[str] |Error message. |
|api |Optional[str] |API name. |
|result |Optional[EmbeddingResult] |Vectorization result, `None` on failure. |


EmbeddingResult structure:


|Field |Type |Description |
|---|---|---|
|data |List[Embedding] |List of vector results corresponding to request order. |
|token_usage |Dict[str, Any] |Token usage statistics by model, including fields such as `prompt_tokens`, `completion_tokens`, `image_tokens`, `total_tokens`. |


Embedding structure:


|Field |Type |Description |
|---|---|---|
|dense |Optional[List[float]] |Dense vector. |
|sparse |Optional[Dict[str, float]] |Sparse vector (keys are tokens, values are weights). |


<span id="example"></span>
# Example

```python
import os

from vikingdb import IAM
from vikingdb.vector import EmbeddingModelOpt, EmbeddingRequest, VikingVector

auth = IAM(ak=os.environ["VIKINGDB_AK"], sk=os.environ["VIKINGDB_SK"])
client = VikingVector(
    host=os.environ["VIKINGDB_HOST"],
    region=os.environ["VIKINGDB_REGION"],
    auth=auth,
    scheme="https",
)

embedding = client.embedding()
request = EmbeddingRequest(
    data=[{"text": "VikingDB provides a managed vector database."}],
    dense_model=EmbeddingModelOpt(
        name="Skylark-embedding",
        version="240715",
        dim=2048,
    ),
    sparse_model=EmbeddingModelOpt(
        name="bge-m3",
        version="default",
        dim=1024,
    ),
)
response = embedding.embedding(request)

if response.result:
    print(f"embedding dense_dim={len(response.result.data[0].dense or [])}, sparse_len={len(response.result.data[0].sparse or [])}")
    print(f"token_usage={response.result.token_usage}")
```
