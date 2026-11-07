---
title: "Seedream Image Generation"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/seedream-image-generation"
---

`las_seedream` uses Seedream 4.5 and 5.0 on BytePlus to generate images from text prompts, one reference image, or multiple reference images. It supports single\-image, sequential image generation, and SSE streaming output.

# Operator introduction

> Operator ID: `las_seedream`

## Core capabilities

* Text\-to\-image and image\-to\-image: generate images from text and optional reference images.

* Multiple references and sequential generation: blend references into images with consistent subjects or styles, with a configurable maximum output count.

* Output file format: Seedream 5.0 accepts `output_format` values jpeg (default) and png. Omit this parameter for 4.5.

* Streaming: set `stream=true` to receive each complete image result, individual image failures, and final usage.

## Application scenarios

* Advertising creative image generation.

* Product images, posters, and social media assets.

* Character, style, or subject\-consistent image creation.

## Effect display

### Text\-to\-image

This example generates a detailed sustainable\-city concept image directly from text. No reference image is supplied.

* Prompt

   ```text
   A tranquil futuristic rooftop garden at sunrise, a young architect reviewing translucent blueprints beside solar trees and flowering plants, distant sustainable city skyline, warm natural light, cinematic wide-angle composition, realistic materials with subtle editorial illustration polish, rich green, coral, and sky-blue accents, highly detailed, no text, no logos, no watermark.
   ```

* Core parameters

   ```json
   {
     "model": "seedream-5-0-260128",
     "size": "2048x2048",
     "response_format": "url",
     "output_format": "png",
     "stream": false,
     "watermark": false,
     "optimize_prompt_options": {
       "mode": "standard"
     }
   }
   ```

* Output

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/fgeh7lpauhz/6f660350-f5f4-41ce-9910-d91d1bab485a.png)

### Reference\-image generation

This example uses a reference image. It preserves the bottle's main visual characteristics while changing the lighting, background, pedestal, and campaign mood.

* Reference image

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/fgeh7lpauhz/96912347-9448-4fd6-af8f-e98d1df7c477.png)

* Prompt

   ```text
   Using the reference product image, preserve the same clear glass dropper bottle, white cap, blank ivory label, and realistic proportions. Re-stage it as a premium nighttime skincare campaign on a dark green stone pedestal, surrounded by glossy botanical leaves, soft mist and controlled studio spotlights. Add elegant reflections and subtle golden rim light. Keep one bottle centered and fully visible. Photorealistic luxury advertising, no text, no logos, no watermark.
   ```

* Core parameters

   ```json
   {
     "model": "seedream-5-0-260128",
     "image": "data:image/png;base64,<reference_image_data>",
     "size": "2048x2048",
     "response_format": "url",
     "output_format": "png",
     "stream": false,
     "watermark": false,
     "optimize_prompt_options": {
       "mode": "standard"
     }
   }
   ```

* Output

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/fgeh7lpauhz/b26559aa-09c2-4a92-8e80-274b0164c480.png)

## Supported regions

* Asia Pacific(Johor)：ap\-southeast\-1

# Input and output requirements

## Input requirements

|Breakdown item |Detailed requirements |
|---|---|
|Supported input data modalities |* Text<br><br>* Image |
|Input format: Text |Provide a natural\-language prompt that describes the image to generate or how to edit the reference images. |
|Input format: Image |* Format: `jpeg`, `png`, `webp`, `bmp`, `tiff`, `gif`, `heic`, or `heif`.<br><br>* Quantity: Up to 14 reference images.<br><br>* Size: Each image can be up to 30 MB.<br><br>* Dimensions: Each dimension must be greater than 14 px, total pixels must be within `[196, 36,000,000]`, and the aspect ratio must be within `[1/16, 16]`. |
|Input path requirements |Provide accessible image URLs or Base64 data in the `image` parameter. Base64 data must use `data:image/<lowercase-format>;base64,<encoded-data>`. |

## Output requirements

|Breakdown item |Detailed requirements |
|---|---|
|Supported output data modalities |Image |
|Output format: Image |* Quantity: For sequential generation, `max_images` accepts 1 to 15 and defaults to 15. The reference image count plus actual output image count must not exceed 15.<br><br>* Dimensions: Defaults to `2048x2048`. Total pixels must be within `[3,686,400, 16,777,216]`, and the aspect ratio must be within `[1/16, 16]`.<br><br>   * Seedream 4.5 supports 2K and 4K;<br><br>   * Seedream 5.0 supports 2K, 3K, and 4K.<br><br>* Format:<br><br>   * Seedream 5.0 supports `jpeg` (default) and `png`.<br><br>   * Omit `output_format` when using Seedream 4.5. |
|Output path requirements |The API returns image URLs or Base64 data. Set `stream=true` to receive complete image results and final usage over SSE. Generated image URLs are valid for 24 hours. |

# Billing information

* Billing standards

   |Breakdown item |Billing standard description |
   |---|---|
   |Billing item |Successful image generation, billed by the number of generated images and the selected model. |
   |Billing type |Usage\-based billing in `USD/image`. |
   |Unit price |Unit prices vary by model. For details, see Billing details. |

* Billing details

   |Model |Unit price |
   |---|---|
   |Seedream 4.5 |0.048 USD/image |
   |Seedream 5.0 |0.042 USD/image |

# Cautions and prerequisites

|Details |Caution and prerequisites |
|---|---|
|Costs |Before calling an operator, you need to understand the model invocation costs associated with using the operator. For details, see [Large model billing](https://docs.byteplus.com/docs/Byteplus_LAS/Large_model_billing). |
|Authentication (API Key) |Before calling an operator, you need to generate an API Key for operator invocation. It is recommended to configure the API Key as an environment variable to ensure safer operator calls. For details, see [Obtain and configure API Key](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_and_configure_the_API_Key). |
|BaseURL |Before calling an operator, you need to determine the BaseURL for operator invocation based on the region where your current LAS service is deployed. This is used to configure the path parameter values for operator calls.<br><br>For details, see [Obtain the Base URL](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_the_Base_URL). The Examples below are for reference only; when making actual calls, replace the path values with those corresponding to your region. |

# Rest API call

## Image Generation

### Interface description

Use Seedream 4.5 and 5.0 for text\-to\-image, image\-to\-image, multiple references, and sequential generation. Call `POST /api/v1/images/generations`: by default it returns JSON in the same HTTP request; with `stream=true`, the same URL returns image generation events through SSE.

The current BytePlus integration supports `seedream-4-5-251128` and `seedream-5-0-260128`. Seedream 5.0 Pro is not supported. The 5.0 version described here corresponds to Seedream 5.0 Lite in the official capability table; call it with the integrated model ID `seedream-5-0-260128`.

See the [BytePlus image generation API](https://docs.byteplus.com/en/docs/ModelArk/image-generation-api) for parameters and the [official capability table](https://docs.byteplus.com/en/docs/ModelArk/seedream-4-0-5-0) for model version mappings.

HTTP request failures use an `error` object with `message`, `type`, and nullable `param` and `code`. The Error Codes section groups common failures by HTTP status; use the actual `error.code/message`. For individual sequential failures, read `data[].error`; for streaming, read `image_generation.partial_failed` or error events.

#### Models and output dimensions

|Model |model |size presets |Output file format |
|---|---|---|---|
|Seedream 4.5 |`seedream-4-5-251128` |`2K`, `4K` |`output_format` is not configurable |
|Seedream 5.0 |`seedream-5-0-260128` |`2K`, `3K`, `4K` |`jpeg` (default), `png` |

`size` also accepts `widthxheight` in pixels and defaults to `2048x2048`. Both models require total pixels in [3,686,400, 16,777,216] and an aspect ratio in [1/16, 16], including both boundaries. Both constraints must be met. With a preset, describe the aspect ratio or purpose in the prompt and let the model choose actual dimensions. The pixel limit applies to width multiplied by height, rather than to either dimension alone.

#### Streaming output

Set `stream=true` on the same image generation endpoint. Each SSE message contains a JSON event in its `data` field. Handle individual image results, image failures, and final usage by event type. The response example expands events in reception order for readability.

|Event type |Meaning and handling |
|---|---|
|`image_generation.partial_succeeded` |One image succeeded. Includes `image_index`, `size`, and either `url` or `b64_json`, depending on `response_format`. |
|`image_generation.partial_failed` |One image failed. Includes `image_index` and `error.code/message`. Continue reading subsequent events. |
|`image_generation.completed` |Request completion event containing final `usage`. Use `usage.generated_images` for successful output count and billing. Completion does not mean that every image succeeded. |
|Request\-level error |A failed request may return an error event containing only `error.code/message`. Authentication and parameter failures can also return HTTP errors. |

Image events include `type`, `model`, and `created`, a Unix timestamp in seconds. `image_index` starts at 0 and identifies an image in individual image events. See the [official streaming response](https://docs.byteplus.com/en/docs/ModelArk/image-generation-streaming-responses) for the protocol. SSE returns each complete image result; it does not send pixel or Base64 chunks of the same image.

### Event fields

|Field |Type |Description |
|---|---|---|
|type |string |Individual image success, image failure, or completion event type; see the event table above. A request\-level error event may contain only error. |
|model |string |Model ID in an image event. |
|created |integer |Request or event creation time as a Unix timestamp in seconds. |
|image_index |integer |Zero\-based image index, used to identify the image in success and failure events. |
|url |string |Successful image download URL, returned with `response_format=url`. Valid for 24 hours after generation; save the image promptly. |
|b64_json |string |Successful image Base64 string, returned with `response_format=b64_json`. |
|size |string |Actual successful image dimensions in pixels, formatted as `widthxheight`. |
|usage |object |Final usage in `image_generation.completed`. Billing uses the successful image count. |
|error |object |Code and message for an individual image failure or request\-level error. |

### Streaming request example

Use the same URL and headers as the main request example, send the JSON body below, and read the response as SSE.

```json
{
  "model": "seedream-5-0-260128",
  "prompt": "Generate two images in a consistent style of an orange cat traveling by the sea: walking at sunrise, then resting at sunset.",
  "size": "2048x2048",
  "output_format": "png",
  "response_format": "url",
  "sequential_image_generation": "auto",
  "sequential_image_generation_options": {
    "max_images": 2
  },
  "stream": true,
  "optimize_prompt_options": {
    "mode": "standard"
  },
  "watermark": true
}
```

### Streaming response example

For readability, the SSE events below are collected into an array in reception order. The actual API returns separate SSE messages, each with a JSON event in data. This example has two successful images; final usage comes from the completed event.

```json
[
  {
    "type": "image_generation.partial_succeeded",
    "model": "seedream-5-0-260128",
    "created": 1764041608,
    "image_index": 0,
    "url": "<image_1_url>",
    "size": "2048x2048"
  },
  {
    "type": "image_generation.partial_succeeded",
    "model": "seedream-5-0-260128",
    "created": 1764041609,
    "image_index": 1,
    "url": "<image_2_url>",
    "size": "2048x2048"
  },
  {
    "type": "image_generation.completed",
    "model": "seedream-5-0-260128",
    "created": 1764041610,
    "usage": {
      "generated_images": 2,
      "output_tokens": 32768,
      "total_tokens": 32768
    }
  }
]
```

Read through `image_generation.completed` for final `usage`. If the connection ends without a completion event, treat the request as incomplete. Return Data and the main response example below describe the default non\-streaming JSON response.

### Request parameters

**model** string 必选 `Example value: seedream-4-5-251128`

Required full model ID. Supported values: `seedream-4-5-251128`, `seedream-5-0-260128`. Seedream 5.0 Pro is not supported; `seedream-5-0-260128` corresponds to Seedream 5.0 Lite in the official capability table.

**prompt** string 必选 `Example value: A super-realistic orange cat wearing sunglasses by the sea at sunset.`

Required text prompt in Chinese or English. The recommended length is at most 300 Chinese characters or 600 English words; this is a recommendation.

**image** string / array `Optional` `Example value: https://example.com/ref.png`

Omit for text\-to\-image. For image\-to\-image, provide an accessible image URL, Base64 string, or an array of these, with up to 14 reference images. Base64 must use `data:image/<lowercase-format>;base64,<encoded-data>`. Formats: jpeg, png, webp, bmp, tiff, gif, heic, heif. Each image must be at most 30 MB, have both dimensions greater than 14 px, total pixels in [196, 36,000,000], and an aspect ratio in [1/16, 16].

**size** string `Optional` `Example value: 2048x2048`

Default: `2048x2048`. Presets: `2K/4K` for 4.5 and `2K/3K/4K` for 5.0. Also accepts `widthxheight`. Both total pixels and aspect ratio must meet the limits above.

**response_format** string `Optional` `Example value: url`

Default: `url`, returning download URLs valid for 24 hours after generation. `b64_json` returns image Base64 strings.

**output_format** string `Optional` `Example value: png`

Configurable only for Seedream 5.0. Default: `jpeg`; values: `jpeg`, `png`. Controls the image file format independently of `response_format`. Omit for 4.5.

**sequential_image_generation** string `Optional` `Example value: auto`

Default: `disabled`, generating one image. With `auto`, the model determines whether to generate an image set and its actual size from the prompt.

**sequential_image_generation_options** sequential_image_generation_options `Optional`

Takes effect only with `sequential_image_generation=auto`. If omitted, the default output count limit applies.

**max_images** integer `Optional` `Example value: 2`

Maximum output count. Default: 15; range: [1, 15], inclusive. The actual count may be lower. Input reference image count plus actual output image count must not exceed 15.

**stream** boolean `Optional` `Example value: false`

Default: `false`, returning JSON after generation finishes. `true` enables SSE at the same URL for single\-image or sequential generation. See Streaming output above for events and examples.

**watermark** boolean `Optional` `Example value: true`

Default: `true`, adding an AI\-generated watermark in the lower\-right corner. `false` disables the watermark.

**optimize_prompt_options** optimize_prompt_options `Optional`

Prompt optimization settings. The default mode is `standard` when omitted.

**mode** string `Optional` `Example value: standard`

Default: `standard`. Integrated 4.5 and 5.0 models support only standard optimization; `fast` is not supported.

### Response parameters

**model** string `Example value: seedream-4-5-251128`

Actual model ID used to generate images.

**created** integer `Example value: 1764041608`

Request or event creation time as a Unix timestamp in seconds.

**data** list of data_item

Output image list. An individual failure in sequential generation can appear as an error in its corresponding item.

**url** string `Example value: <image_url>`

Successful image download URL, returned with `response_format=url`. Valid for 24 hours after generation; save the image promptly.

**b64_json** string `Example value: <base64_image>`

Successful image Base64 string, returned with `response_format=b64_json`.

**size** string `Example value: 2048x2048`

Actual successful image dimensions in pixels, formatted as `widthxheight`.

**error** image_error

Individual image failure in sequential generation, containing code and message. Check successful images and final successful output count as well.

**code** string `Example value: <error_code>`

Error code as returned by the service. Request\-level HTTP errors are listed below.

**message** string `Example value: <error_message>`

Error message for troubleshooting.

**type** string `Example value: invalid_request_error`

HTTP error category, such as invalid_request_error, authentication_error, rate_limit_error, or server_error. Upstream image errors may omit it.

**param** string `Example value: model`

Parameter associated with an HTTP error; may be null. Upstream image errors may omit it.

**usage** image_usage

Request usage. Successfully generated image count determines LAS image billing; token fields report usage statistics.

**generated_images** integer `Example value: 1`

Number of successfully generated images, excluding failures. Sequential generation is billed by this count; reference image inputs are free.

**output_tokens** integer `Example value: 16384`

Image output tokens, calculated by rounding the sum of output image width multiplied by height, divided by 256.

**total_tokens** integer `Example value: 16384`

Input tokens are not calculated for the current models, so this equals `output_tokens`.

**error** image_error

Error details for an HTTP request failure or no successful images. A failed request can return only `error`; successful responses do not need this field.

**code** string `Example value: <error_code>`

Error code as returned by the service. Request\-level HTTP errors are listed below.

**message** string `Example value: <error_message>`

Error message for troubleshooting.

**type** string `Example value: invalid_request_error`

HTTP error category, such as invalid_request_error, authentication_error, rate_limit_error, or server_error. Upstream image errors may omit it.

**param** string `Example value: model`

Parameter associated with an HTTP error; may be null. Upstream image errors may omit it.

### Examples

#### Request example

```bash
curl --location "${LAS_ENDPOINT}/api/v1/images/generations" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer ${LAS_API_KEY}" \
--data '{
  "model": "seedream-4-5-251128",
  "prompt": "A super-realistic orange cat wearing sunglasses by the sea at sunset.",
  "size": "2048x2048",
  "response_format": "url"
}'
```

#### Response example

This is a non\-streaming success example. Sequential failures can appear in `data[].error`. Content moderation rejection of one image allows subsequent generation to continue; an internal service error may stop remaining generation. A request with no successful images can return a top\-level `error`.

```json
{
  "model": "seedream-4-5-251128",
  "created": 1764041608,
  "data": [
    {
      "url": "<image_url>",
      "size": "2048x2048"
    }
  ],
  "usage": {
    "generated_images": 1,
    "output_tokens": 16384,
    "total_tokens": 16384
  }
}
```

### Error codes

|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|400 |null / as returned |Invalid request |Invalid request body, parameters, or upstream model request. |
|401 |invalid_api_key |Authentication failed |Missing or invalid authentication credentials. |
|403 |null / as returned |Forbidden |The account does not have permission. |
|404 |null / as returned |model not found |No callable model mapping was found. |
|413 |null |Request body exceeds the limit |The request body exceeds the configured size limit. |
|415 |null |Content\-Type must be application/json |The request Content\-Type is unsupported. |
|429 |null / as returned |Rate limit exceeded |Request rate or concurrency exceeds a limit; read the returned message. |
|500 |null / as returned |Internal server error |Server or upstream error; read the returned message. |
