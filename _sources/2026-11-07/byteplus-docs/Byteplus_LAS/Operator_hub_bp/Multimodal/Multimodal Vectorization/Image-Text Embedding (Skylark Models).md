---
title: "Image-Text Embedding (Skylark Models)"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/image-text-embedding-skylark-models-67f8e3f58049150a"
---

The Image\-Text Embedding operator generates unified embeddings for images, videos, and text, enabling cross\-modal retrieval with Skylark embedding models.

# Operator introduction

> Operator ID: `las_embedding_vision`

## Core capabilities

* Generates unified embeddings for images, videos, and text for cross\-modal retrieval.

* Accepts media through Base64 data or URLs and handles common formats such as JPEG, PNG, MP4, and AVI.

* Returns dense vectors in `float` or `base64` format. Pure\-text input can additionally return sparse embeddings.

* Uses `skylark-embedding-vision-251215` for multimodal embedding.

## Effect display

* Input example

   ![图片](https://las-ai-ap-southeast-1-online-bp.tos-ap-southeast-1.bytepluses.com/operator_cards_serving/public/online/doubao_embedding_vision/cat_ip_adapter.jpeg)

* Output example

   The operator returns the image embedding as a vector. Example:

   ```JSON
   [0.047607422, 0.044433594, ...]
   ```

## Supported regions

* Asia Pacific (Johor): `ap-southeast-1`

# Input and output requirements

## Input requirements

|Breakdown item |Detailed requirements |
|---|---|
|Supported input data modalities |* Image<br><br>* Video<br><br>* Text |
|Input format |Provide an `input` list that follows the [Multimodal Embedding API](https://console.byteplus.com/ark/region:ap-southeast-1/en/docs/modelark/multimodal-vectorization-api). Image and video content supports URL or Base64 input. |
|Model |`skylark-embedding-vision-251215` |
|Input path requirements |Image and video content can be provided in the following forms:<br><br><br>* **URL**: Provide a URL that meets the accessibility requirements of the ModelArk Multimodal Embedding API.<br><br>* **Base64**: Embed Base64\-encoded content directly in the request. |

## Output requirements

|Breakdown item |Detailed requirements |
|---|---|
|Supported output data modalities |Text |
|Dense embedding |`float` or `base64`; 2048 dimensions by default. Models from `skylark-embedding-vision-250615` onward support 1024 or 2048 dimensions. |
|Sparse embedding |Available only for pure\-text input when `sparse_embedding.type` is `enabled`. |
|Output path requirements |No output storage path is required. Embeddings are returned directly in the synchronous API response. |

# Billing information

|Billing item |Unit price |
|---|---|
|Inference service (text input) |0.125 USD per million tokens |
|Inference service (image input) |0.325 USD per million tokens |

# Cautions and prerequisites

|Details |Cautions and prerequisites |
|---|---|
|Authentication |Generate an LAS API Key and configure it as an environment variable. See [Obtain and configure the API Key](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_and_configure_the_API_Key). |
|BaseURL |Select the LAS BaseURL for the region in which the service is deployed. See [Obtain the Base URL](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_the_Base_URL). |

# Rest API call

`POST https://operator.las.ap-southeast-1.bytepluses.com/api/v1/embeddings/multimodal`

## Interface description

Call the operator to generate multimodal embeddings for images, videos, and text.

## Request parameters

**model** string 必选 `Example value: skylark-embedding-vision-251215`

Model name. Supports `skylark-embedding-vision-251215`.

**input** list of object 必选

Content to embed. For the supported item structures, see the `input` parameter in the [Multimodal Embedding API](https://console.byteplus.com/ark/region:ap-southeast-1/en/docs/modelark/multimodal-vectorization-api).

**encoding_format** string `Optional` `Example value: float`

Embedding return format: `float`, `base64`, or `null`. Default: `float`.

**dimensions** integer `Optional` `Example value: 2048`

Output vector dimension. Models from `skylark-embedding-vision-250615` onward support `1024` or `2048`. Default: `2048`.

**instructions** string `Optional`

Inference instruction. If omitted, a default is generated according to the input modality. See [Configuring instructions](https://console.byteplus.com/ark/region:ap-southeast-1/en/docs/modelark/multimodal-vectorization-api).

**sparse_embedding** object `Optional`

Sparse embedding switch for pure\-text input only.

**type** string `Example value: enabled`

`disabled` returns dense embeddings only; `enabled` returns both dense and sparse embeddings.

## Response parameters

**id** string

Unique request ID.

**model** string `Example value: skylark-embedding-vision-251215`

Actual model and version used.

**created** integer

Request creation time as a Unix timestamp in seconds.

**object** string `Example value: list`

Fixed value: `list`.

**data** embedding_result

Embedding output.

**embedding** list of float

Dense embedding for the input content.

**sparse_embedding** list of object

Sparse embedding returned only when `sparse_embedding.type=enabled`. Each item contains `index` and non\-zero `value`.

**object** string `Example value: embedding`

Fixed value: `embedding`.

**usage** token_usage

Token usage for the request.

**prompt_tokens** integer

Number of input tokens.

**total_tokens** integer

Total tokens consumed.

**prompt_tokens_details** tokens_details

Token details by modality.

**text_tokens** integer

Text tokens, including tokens generated from a video timeline and small preset text\-token overhead for media input.

**image_tokens** integer

Tokens for images and video frames.

## Request example

```bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/embeddings/multimodal" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer ${LAS_API_KEY}" \
--data '{
  "model": "skylark-embedding-vision-251215",
  "encoding_format": "float",
  "input": [
    {
      "type": "image_url",
      "image_url": {"url": "https://example.com/cat.jpeg"}
    },
    {
      "type": "text",
      "text": "What is in the image?"
    }
  ]
}'
```

## Response example

```json
{
  "id": "021764041607868c64dcafb5669f61b8aa56083c290255748bdbb",
  "created": 1764041608,
  "model": "skylark-embedding-vision-251215",
  "object": "list",
  "data": {
    "object": "embedding",
    "embedding": [0.0002918243, -0.0189208984, -0.0038146973, "..."]
  },
  "usage": {
    "prompt_tokens": 1335,
    "total_tokens": 1335,
    "prompt_tokens_details": {
      "text_tokens": 23,
      "image_tokens": 1312
    }
  }
}
```

## Error codes

|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|404 |Model.InvalidName |model not found. |Invalid model name. |
