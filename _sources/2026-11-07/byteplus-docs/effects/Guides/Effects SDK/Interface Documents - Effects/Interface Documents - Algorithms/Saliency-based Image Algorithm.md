---
title: "Saliency-based Image Algorithm"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-saliency-based-image-algorithm"
---

<span id="7162205d"></span>
# Introduction

Input image, the algorithm outputs a mask representing the saliency of the object in the image. Mask values are 0~ 255, the higher the value, the higher the saliency.

V4.5.2 added this new algorithm. Other name is Object Matting algorithm.

<span id="14e128ab"></span>
# Technical specifications


|Specifications |Description |
|---|---|
|Support platform |Android、iOS |
|Supported image formats |BGRA888、RGBA8888、BRG888、RGB888 |


<span id="1e7ba368"></span>
# C interface description

Detailed interface description View Header File:

`bef_effect_ai_saliency_matting h`

<span id="5cd1a06f"></span>
## 1. Create algorithm handle

```C
BEF_SDK_API
bef_effect_result_t bef_effect_ai_saliency_matting_create(bef_ai_saliency_matting_handle *handle);
```


Function description: Create algorithm handle

**Parameter description:** 


|Parameter name |Parameter type |Parameter description |
|---|---|---|
|handle |bef_ai_saliency_matting_handle\* |Output algorithm handle |


**Return value description:** 

Success returns BEF_RESULT_SUC, failure returns the corresponding error code, please refer to bef_effect_ai_public_define

<span id="61d8136c"></span>
## 2. Check License

```C
BEF_SDK_API
bef_effect_result_t bef_effect_ai_saliency_matting_check_license(bef_ai_saliency_matting_handle handle, const char* licensePath);
```


Function description: Check whether the license is legal

**Parameter description:** 


|Parameter name |Parameter type |Parameter description |
|---|---|---|
|handle |bef_ai_saliency_matting_handle |Handle for license verification |
|licensePath |const char\* |License store file path |


**Return value description:** 

Success returns BEF_RESULT_SUC, failure returns the corresponding error code, please refer to bef_effect_ai_public_define

<span id="2430df93"></span>
## 3. Set algorithm model file

```C
typedef enum{
    BEF_SALIENCY_MATTING_SMALL_MODEL = 0,
    BEF_SALIENCY_MATTING_MEDIUM_MODEL = 1,
    BEF_SALIENCY_MATTING_LARGE_MODEL = 2,
}bef_ai_saliency_matting_model_type;

BEF_SDK_API
bef_effect_result_t bef_effect_ai_saliency_matting_set_model(bef_ai_saliency_matting_handle handle, bef_ai_saliency_matting_model_type type, const char *modelPath);
```


Function description: Load the model according to the given model type, it will check whether there is

**Parameter description:** 


|Parameter name |Parameter type |Parameter description |
|---|---|---|
|handle |bef_ai_saliency_matting_handle |Handle for model initialization |
|type |bef_ai_saliency_matting_model_type |Type of model used |
|modelPath |const char\* |Model file path |


**Return value description:** 

Success returns BEF_RESULT_SUC, failure returns the corresponding error code, please refer to bef_effect_ai_public_define

<span id="22249c60"></span>
## 4. Execute the algorithm

```C
BEF_SDK_API
bef_effect_result_t bef_effect_ai_saliency_matting_detect(bef_ai_saliency_matting_handle handle,
                                            const unsigned char *image,
                                            bef_ai_pixel_format pixelFormat,
                                            int width,
                                            int height,
                                            int stride,
                                            bef_ai_rotate_type rotation,
                                            bef_ai_saliency_matting_ret *result);
```


Function description: perform algorithm processing

**Parameter description:** 


|Parameter name |Parameter type |Parameter description |
|---|---|---|
|handle |bef_ai_saliency_matting_handle |Initialized handle |
|image |unsigned char\* |Input image binary data address |
|pixelFormat |bef_ai_pixel_format |Image format |
|width |int |Input image width |
|height |int |Input image height |
|stride |int |Number of bytes occupied by each line in image data |
|rotation |bef_ai_rotate_type |The direction of image rotation, usually considered head\-up rotation angle of 0 |
|result |bef_ai_saliency_matting_ret\* |Algorithm output result |


`The mask`member in result points to a Memory Space of size: `width`\* `height`\* `sizeof (unsigned char)`. If the `mask`member in the `bef_ai_saliency_matting_ret`structure is NULL, the algorithm will be allocated an appropriate size Memory Space and the result will be written to it. **The user will be responsible for freeing this space.**  If the `mask`member in the structure is not empty, it is assumed that the user has allocated an **appropriate** Memory Space and writes the result directly to the Memory Space pointed to by the `mask`member.

**Return value description:** 

Success returns BEF_RESULT_SUC, failure returns the corresponding error code, please refer to bef_effect_ai_public_define

<span id="275ea086"></span>
## 5. Release handle

```C
BEF_SDK_API
bef_effect_result_t bef_effect_ai_saliency_matting_release(bef_ai_saliency_matting_handle handle);
```


Function description: Release algorithm handle

**Parameter description:** 


|Parameter name |Parameter type |Parameter description |
|---|---|---|
|handle |bef_ai_saliency_matting_handle |Handle to algorithm to release |


**Return value description:** 

Success returns BEF_RESULT_SUC, failure returns the corresponding error code, please refer to bef_effect_ai_public_define

<span id="644b822e"></span>
# Java interface

<span id="3077c03f"></span>
## 1. Initialization algorithm

**Function declaration:** 

```Plain
public int init()
```


**Return value description:** 

Success returns 0, failure returns the corresponding error code, please refer to bef_effect_ai_public_define

<span id="c44e0a3b"></span>
## 2. Check the algorithm License

**Function declaration:** 

```Plain
public int checkLicense(String licensePath)
```


**Function parameter description:** 


|Parameter name |Parameter type |Parameter description |
|---|---|---|
|licensePath |String |Path to license file |


**Return value description:** 

Success returns 0, failure returns the corresponding error code, please refer to bef_effect_ai_public_define

<span id="33d931c8"></span>
## 3. Load model files

Load the model from the path depending on the type of algorithm model

**Function declaration:** 

```Plain
public int setModel(String modelPath, EffectsSDKEffectConstants.SaliencyMattingModelType modleType)
```


**Function parameter description:** 


|Parameter name |Parameter type |Parameter description |
|---|---|---|
|modelPath |String |Path to model file |
|modleType |SaliencyMattingModelType |There are three types of models: large, medium and small. |


**Return value description:** 

Success returns 0, failure returns the corresponding error code, please refer to bef_effect_ai_public_define

<span id="95ba5a7e"></span>
## 4. Execute the algorithm

Execute algorithms based on image data

**Function declaration:** 

```Plain
public MattingMask process(ByteBuffer imgdata, EffectsSDKEffectConstants.PixlFormat pixelformat, int width, int height, int stride, EffectsSDKEffectConstants.Rotation orientation)
```


Function parameter description:


|Parameter name |Parameter type |Parameter description |
|---|---|---|
|imgdata |ByteBuffer |Image data |
|pixelformat |PixlFormat |Pixel format |
|width |int |Image width |
|height |int |Image height |
|stride |int |Data size of each row of pixels in image data |
|orientation |Rotation |Image orientation, usually considered the ground is down, when the head is facing up Rotation is 0 |


**Return value description:** 

Return MattingMask on success, return corresponding error code on failure. For details, please refer to bef_effect_ai_public_define

<span id="89c59e63"></span>
## 5. Release algorithm

Release algorithm resources

**Function declaration:** 

```Plain
public int release()
```


**Return value description:** 

Success returns 0, failure returns the corresponding error code, please refer to bef_effect_ai_public_define

<span id="e0eef156"></span>
## MattingMask class

This class is an inner class of the SaliencyMatting class, used to store the Mask of the algorithm results.


|Attribute name |Type |Description |
|---|---|---|
|width |int |Width |
|height |int |Highly |
|buffer |byte[] |Mask binary data |


<span id="cad495be"></span>
# FAQ

<span id="f7aa3c1c"></span>
### If there is any exception, check if there are any of the following types of logs

A: It is recommended to first check the log of the following tag output Error type:


* bef_effect_ai

* SMASH_E_LOG

* EffectSDK
