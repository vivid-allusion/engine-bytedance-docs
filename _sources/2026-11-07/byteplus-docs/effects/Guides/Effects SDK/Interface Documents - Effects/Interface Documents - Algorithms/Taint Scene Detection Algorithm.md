---
title: "Taint Scene Detection Algorithm"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-taint-scene-detection-algorithm"
---

Taint Scene Detection algorithm provides a solution for judging whether the lens is dirty before shooting, preventing low\-quality video or picture caused by dirty lenses, and providing a stronger guarantee for users to shoot.

New algorithm added from V4.4.2.

<span id="ec8d88c6"></span>
# Technical Specifications


|**Category** |**Supported Formats** |
|---|---|
|Platforms |* Android<br><br>* iOS |
|Input formats |BGR888 |
|Memory usage |< 11.99M (test device OPPO R11) |
|Detection speed |< 3.29ms (test device OPPO R11) |


<span id="7b99ddd5"></span>
# C interface description

iOS and Android interfaces are non\- thread safety, need to ensure all algorithm creation, processing and destruction in the single thread.

For more detailed interface description, refer to the header file bef_ai_image_quality_enhancement_taint_detect.h

<span id="af41a8a0"></span>
## 1. Create Taint Scene Detection algorithm handle

```C
BEF_SDK_API bef_effect_result_t
bef_ai_image_quality_enhancement_taint_detect_create(
    bef_image_quality_enhancement_handle *handle, 
    bef_ai_taint_scene_detect_param *param);

typedef struct bef_ai_taint_scene_detect_param {
    int detectFrequency;
    const char* modelPath;
    const char* kernelBinPath;
    bef_ai_lens_backend_type backendType;
    int numThread;    // only make sense when backendType is CPU, default set 2
}bef_ai_taint_scene_detect_param;
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_image_quality_enhancement_handle \* |Created Taint Scene Detection Algorithm handle. |
|config |bef_ai_taint_scene_detect_param \* |Algorithm initialization configuration parameters. |


**Return value:** 

Success returns BEF_RESULT_SUC, while failure returns the corresponding error code. For more information, refer to bef_effect_ai_public_define.h

<span id="f7c8f7f7"></span>
## 2. Process Taint Scene Detection algorithm

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Algorithm input requires the width and height of 224 BGR small image, the small image can not be the lost contents image out of crop, must be a small image out of <strong>scale</strong>.</div>


**switchScene** means that if the algorithm instance is to reuse, the first frame is set to true at the beginning of each detection, and the second frame and beyond is set to false. This is equivalent to resetting the information cached from the previous detection results. If you start one algorithm instance per detection, you don't need to configure this parameter, just set it to false.

```C
BEF_SDK_API bef_effect_result_t
bef_ai_image_quality_enhancement_taint_detect_process(
    bef_image_quality_enhancement_handle handle, 
    bef_ai_taint_scene_detect_buffer *input, 
    float *score);

typedef struct bef_ai_taint_scene_detect_buffer {
    void *inBuffer;
    bool switchScene;
}bef_ai_taint_scene_detect_buffer;
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_image_quality_enhancement_handle |Taint Scene Detection handle. |
|input |bef_ai_taint_scene_detect_buffer \* |Taint Scene Detection algorithm input. |
|score |float \* |Taint Scene Detection probability output. |


**Return value:** 

Success returns BEF_RESULT_SUC, while failure returns the corresponding error code. For more information, refer to bef_effect_ai_public_define.h

<span id="6cd301f0"></span>
## 3. Release handle

```C
BEF_SDK_API bef_effect_result_t
bef_ai_image_quality_enhancement_taint_detect_destroy(
    bef_image_quality_enhancement_handle handle);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_image_quality_enhancement_handle |Taint Scene Detection algorithm handle. |


**Return value:** 

Success returns BEF_RESULT_SUC, while failure returns the corresponding error code. For more information, refer to bef_effect_ai_public_define.h

<span id="ec336a30"></span>
## 4. Taint Scene Detection algorithm authorization

```C
//Offline license detection method
BEF_SDK_API bef_effect_result_t
bef_ai_image_quality_enhancement_taint_detect_check_license(
    bef_image_quality_enhancement_handle handle, 
    const char* licensePath);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_image_quality_enhancement_handle |Taint Scene Detection algorithm handle. |
|licensePath |const char \* |License file path. |


**Return values:** 

Success returns BEF_RESULT_SUC, while failure returns the corresponding error code. For more information, refer to bef_effect_ai_public_define.h

<span id="Java interface description"></span>
# Java interface description

**Interface Description**

For more detailed interfaces description, refer to com.bytedance.labcv.effectsdk.TaintSceneDetect.java

<span id="57832429"></span>
## 1. Initialize Taint Scene Detection handle

```Java
public int init(
    Context context, 
    TaintDetectParam param,
    String licensePath, 
    boolean onlineLicense);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|context |Context |Android context. |
|param |TaintDetectParam |Taint Scene Detection parameters. |
|licensePath |String |License file path. |
|onlineLicense |boolean |Configure online or offline licensing. Set to false if you use offline licensing. |


**Return value:** 

Return BEF_RESULT_SUC successfully, otherwise return the corresponding error code

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">About <code>TaintDetectParam</code> can refer to com.bytedance.labcv.effectsdk.TaintSceneDetect.java, and its definition is consistent with the C interface bef_ai_image_quality_enhancement_taint_detect.</div>


<span id="654d0030"></span>
## 2. Process Taint Scene Detection algorithm

```Java
public float process(
    ByteBuffer buffer);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|buffer |ByteBuffer |Input buffer. |


**Return value:** 

Return Taint Scene Detection probability value.

<span id="6e86faec"></span>
## 3. Release Taint Scene Detection handle

```Java
public void release()
```


<span id="FAQ"></span>
## FAQ

<span id="31f2fa7f"></span>
### 1. If any exception occurs, check if there are any of the following types of logs

A: It is recommended to first look at the following tags output Error type logs:


* **bef_effect_ai**

* **SMASH_E_LOG**

* **EffectSDK**


<span id="7cc9043d"></span>
## Error code

Refer to [Error code table].
