---
title: "Image Pro Image Generation"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/image-pro-image-generation"
---

Image Pro supports text\-to\-image generation, reference image editing, and masked edits for high\-quality visual creation. Both generation and editing use `las_image_pro` and return Base64\-encoded image data.

# Operator introduction

> Operator ID: `las_image_pro` (the legacy alias `image_pro` is still accepted)

## Core capabilities

* Text\-to\-image: generate realistic, illustration, product, poster, and other image types from text prompts.

* Image editing: modify reference images with a prompt, with an optional mask to identify regions for local edits.

* Parameter control: configure output size, image count, image quality, and output file format.

* Standard APIs: use JSON for generation and multipart file uploads for editing. Both return Base64\-encoded image data.

## Application Scenarios

* E\-commerce product images, product scene images, and marketing assets.

* Advertising posters, social media covers, and campaign visuals.

* Concept art, storyboard images, and style exploration for games, film, animation, and content creation.

* Knowledge illustrations, infographics, and presentation assets for education and office scenarios.

## Effect display

### E\-commerce product marketing image

This example creates a clean, photorealistic product image for an e\-commerce product page or skincare campaign. The prompt defines the product, placement, lighting, color palette, composition, and content restrictions.

* Prompt

   ```text
   Premium commercial product photography for a fictional luxury skincare serum named LUMERA. A clear frosted glass dropper bottle with a simple blank ivory label stands on a glossy pale stone pedestal, surrounded by fresh green leaves and subtle water droplets. Soft morning sunlight, clean white and emerald color palette, realistic reflections, high-end ecommerce advertising, centered composition, crisp details, no people, no extra text, no watermark.
   ```

* Core parameters

   ```json
   {
     "model_name": "las_image_pro",
     "size": "1024x1024",
     "n": 1,
     "quality": "high",
     "output_format": "png"
   }
   ```

* Output

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/fgeh7lpauhz/96912347-9448-4fd6-af8f-e98d1df7c477.png)

### Realistic poster scene

This example generates a realistic city image suitable for a travel poster or campaign visual. The prompt specifies the location, time, weather, people, lighting, photographic style, and text restrictions.

* Prompt

   ```text
   A cinematic realistic travel poster scene of Singapore at blue hour after rain, viewed from a lively waterfront promenade. Modern skyline and Marina Bay architecture reflected on wet pavement, pedestrians with umbrellas, warm street lights, natural atmospheric depth, premium editorial photography, balanced square poster composition, photorealistic, crisp detail, no readable text, no logos, no watermark.
   ```

* Core parameters

   ```json
   {
     "model_name": "las_image_pro",
     "size": "1024x1024",
     "n": 1,
     "quality": "high",
     "output_format": "png"
   }
   ```

* Output

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/fgeh7lpauhz/29d847d6-0a34-4ecc-be8a-0143f4b99b62.png)

## Supported regions

* Asia Pacific(Johor)：ap\-southeast\-1

# Input and output requirements

## Input requirements

|Breakdown item |Detailed requirements |
|---|---|
|Supported input data modalities |Text and image |
|Input format: Text |* Language: Chinese and English.<br><br>* Content: Use a natural\-language prompt that clearly describes the subject, scene, style, composition, and constraints. |
|Input format: Image |For editing, upload up to 16 PNG/JPG images through multipart, each smaller than 50 MB. An optional mask must be a PNG with the same dimensions as the input image; fully transparent areas identify the regions to edit. |
|Input path requirements |No file path is required for generation. For editing, upload the image files directly through the synchronous editing API. |

## Output requirements

|Breakdown item |Detailed requirements |
|---|---|
|Supported output data modalities |Image |
|Output format: Image |* Quantity: Generates 1–10 images per request. The default is 1.<br><br>* Size: Use `size` to specify a supported image size. The actual range follows service\-side parameter validation.<br><br>* Format and quality: `output_format` supports `png` and `jpeg`; `quality` supports `low`, `medium`, and `high`. |
|Output path requirements |The API returns Base64\-encoded image data in `data[].b64_json`. Decode it to save the image file. |

# Billing information

* Billing standards

   |Breakdown item |Billing standard description |
   |---|---|
   |Billing items |Input tokens and output tokens. |
   |Billing type |Usage\-based billing in `USD/1K tokens`. |

* Billing details

   |Model |Billing item |Unit price |
   |---|---|---|
   |Image Pro |Input tokens |0.012 USD/1K tokens |
   |Image Pro |Output tokens |0.04 USD/1K tokens |

# Cautions and prerequisites

|Details |Caution and prerequisites |
|---|---|
|Costs |Before calling an operator, you need to understand the model invocation costs associated with using the operator. For details, see [Large model billing](https://docs.byteplus.com/docs/Byteplus_LAS/Large_model_billing). |
|Authentication (API Key) |Before calling an operator, you need to generate an API Key for operator invocation. It is recommended to configure the API Key as an environment variable to ensure safer operator calls. For details, see [Obtain and configure API Key](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_and_configure_the_API_Key). |
|BaseURL |Before calling an operator, you need to determine the BaseURL for operator invocation based on the region where your current LAS service is deployed. This is used to configure the path parameter values for operator calls.<br><br>For details, see [Obtain the Base URL](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_the_Base_URL). The Examples below are for reference only; when making actual calls, replace the path values with those corresponding to your region. |

# Rest API call

## Image Pro Image Generation

### Interface description

Call the Image Pro model to synchronously generate images from a text prompt.

The legacy alias `image_pro` is still accepted. Successful responses return `las_image_pro` in `model`.

### Request parameters

**model_name** string 必选 `Example value: las_image_pro`

Model name. Use `las_image_pro`.

**prompt** string 必选 `Example value: A premium skincare advertisement image, commercial photography style.`

Text prompt used to generate the image. Chinese and English are supported.

**size** string `Optional` `Example value: 1024x1024`

Output image size. Use a supported size enum or width\-by\-height value. The actual range follows service\-side validation.

**n** integer `Optional` `Example value: 1`

Number of images to generate, from 1 to 10. Default: 1.

**quality** string `Optional` `Example value: high`

Image quality: `low`, `medium`, or `high`. Default: `high`.

**output_format** string `Optional` `Example value: png`

Generated image file format: `png` or `jpeg`. Default: `png`.

**output_compression** integer `Optional` `Example value: 90`

Output image compression parameter, from 0 to 100. Applies only when `output_format=jpeg`.

**user** string `Optional` `Example value: user-001`

End\-user identifier for business\-side tracing.

### Response parameters

**model** string `Example value: las_image_pro`

Model name, always returned as `las_image_pro`.

**created** integer `Example value: 1764041608`

Unix timestamp in seconds when the request was created.

**data** list of data_item

Generated image outputs.

**b64_json** string `Example value: <base64>`

Base64\-encoded image data. Decode it to save the image file.

**usage** usage

Usage information for this request.

**generated_images** integer `Example value: 1`

Number of successfully generated images.

**input_tokens** integer `Example value: 128`

Input\-side token usage.

**output_tokens** integer `Example value: 4096`

Output\-side token usage.

**total_tokens** integer `Example value: 4224`

Total token usage for this request.

**input_tokens_details** input_tokens_details

Input token details. Fields may expand as model capabilities evolve.

**text_tokens** integer `Example value: 128`

Text input token usage.

**image_tokens** integer `Example value: 0`

Image input token usage. For text\-only generation, this is usually 0 or omitted.

**output_tokens_details** output_tokens_details

Output token details. Fields may expand as model capabilities evolve.

**image_tokens** integer `Example value: 4096`

Image output token usage.

**text_tokens** integer `Example value: 0`

Text output token usage. For image generation, this is usually 0 or omitted.

**error** error_info

Request\-level error information.

**code** string `Example value: BadRequest`

Error code.

**message** string `Example value: Missing required parameter.`

Error message.

### Examples

#### Request example

```bash
curl --location "${LAS_ENDPOINT}/api/v1/images/generations" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer ${LAS_API_KEY}" \
--data '{
    "model_name": "las_image_pro",
    "prompt": "A premium skincare advertisement image. A transparent glass bottle stands on a light marble surface, with soft morning light and mist in the background, commercial photography style.",
    "size": "1024x1024",
    "n": 1,
    "quality": "high",
    "output_format": "png"
}'
```

#### Response example

```json
{
  "model": "las_image_pro",
  "created": 1764041608,
  "data": [
    {
      "b64_json": "<base64>"
    }
  ],
  "usage": {
    "generated_images": 1,
    "input_tokens": 128,
    "output_tokens": 4096,
    "total_tokens": 4224,
    "input_tokens_details": {
      "text_tokens": 128,
      "image_tokens": 0
    },
    "output_tokens_details": {
      "image_tokens": 4096,
      "text_tokens": 0
    }
  }
}
```

### Error codes

|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|400 |Model.InvalidName |The model name is invalid. |Invalid model name. |
|400 |Parameter.Invalid |The parameter is invalid. |Invalid request parameter. |
|401 |Authorization.Missing |Missing Authorization. |Missing authentication. |
|401 |ApiKey.Invalid |The api key is invalid. |Invalid API key. |
|429 |Server.Busy |Server is Busy, please try again later. |Service busy or rate\-limited. |
|500 |Server.InternalError |General Internal Error |Internal server error. |

## Image Pro Image Editing

### Interface description

Edit uploaded reference images with a prompt, with an optional mask to identify regions for local edits.

Use `POST /api/v1/images/edits` with `multipart/form-data` and `Authorization: Bearer <LAS_API_KEY>`. Set `model` to `las_image_pro`. Upload a single image with `image`, or repeat `image[]` for multiple images. Let the client generate the multipart boundary automatically instead of setting `Content-Type` manually.

### Request parameters

**model** string 必选 `Example value: las_image_pro`

Model name. Use `las_image_pro`.

**image[]**  array 必选 `Example value: input.png`

Input image files uploaded via multipart. Repeat this field for multiple images. Supports up to 16 PNG/JPG files, each smaller than 50 MB. For one image, you can also use `image`.

**prompt** string 必选 `Example value: Replace the background with a garden in soft morning light.`

Instructions for editing the images. Chinese and English are supported.

**mask** string `Optional` `Example value: mask.png`

Binary PNG mask uploaded via multipart. Its dimensions must match the input image. Fully transparent areas (Alpha=0) identify the regions to edit.

**size** string `Optional` `Example value: 1024x1024`

Output image size. Use a supported size enum or width\-by\-height value.

**n** integer `Optional` `Example value: 1`

Number of images to generate, from 1 to 10. Default: 1.

**quality** string `Optional` `Example value: high`

Image quality: `low`, `medium`, or `high`. Default: `high`.

**output_format** string `Optional` `Example value: png`

Generated image format: `png` or `jpeg`. Default: `png`.

**output_compression** integer `Optional` `Example value: 90`

Compression parameter from 0 to 100. Applies only when `output_format=jpeg`.

**user** string `Optional` `Example value: user-001`

End\-user identifier for business\-side tracing.

### Response parameters

The response structure is the same as image generation. `data[].b64_json` contains the Base64\-encoded edited image, and `usage` contains image and token usage.

### Examples

#### Request example

```bash
curl --location "${LAS_ENDPOINT}/api/v1/images/edits" \
--header "Authorization: Bearer ${LAS_API_KEY}" \
--form "model=las_image_pro" \
--form "image[]=@input.png;type=image/png" \
--form "mask=@mask.png;type=image/png" \
--form-string "prompt=Replace the background in the transparent mask area with a garden in soft morning light, preserving the product." \
--form "size=1024x1024" \
--form "n=1" \
--form "quality=high" \
--form "output_format=png"
```

#### Response example

```json
{
  "model": "las_image_pro",
  "created": 1764041608,
  "data": [{"b64_json": "<base64>"}],
  "usage": {
    "generated_images": 1,
    "input_tokens": 1152,
    "output_tokens": 4096,
    "total_tokens": 5248,
    "input_tokens_details": {"text_tokens": 128, "image_tokens": 1024},
    "output_tokens_details": {"image_tokens": 4096, "text_tokens": 0}
  }
}
```

### Error codes

The image editing API uses the same error codes as image generation.
