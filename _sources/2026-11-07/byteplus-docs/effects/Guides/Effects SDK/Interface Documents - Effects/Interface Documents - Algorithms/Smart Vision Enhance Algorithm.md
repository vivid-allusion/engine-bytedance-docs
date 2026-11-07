---
title: "Smart Vision Enhance Algorithm"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-smart-vision-enhance-algorithm"
---

On the basis of detecting scene categories, Smart Vision Enhance algorithm enhances the quality of the images captured by the camera.

In the demo, this feature is called One Key Enhance.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Machines below iOS11 do not support the image quality module algorithm except for frame insertion.</div>


<span id="9aa052bf"></span>
# Technical Specifications


|**Category** |**Supported Formats** |
|---|---|
|Platforms |* Android<br><br>* iOS |
|Input formats |* RGBA8888<br><br>* BGRA8888 |
|Memory footprint |< 42M (test device OPPO R11) |
|Detection speed |< 5ms (test equipment OPPO R11) |


<span id="4c1f4cf6"></span>
# C API

For the detailed description, refer to the header file: bef_ai_image_quality_enhancement_onekey_enhance.h

<span id="d6a778d6"></span>
## 1. Create Smart Vision Enhance algorithm handle

```C
BEF_SDK_API bef_effect_result_t
bef_ai_image_quality_enhancement_onekey_enchance_create(bef_image_quality_enhancement_handle* handle, const bef_ai_onekey_enhancement_config* config);

// Version 4.4.3 add new algorithm parameters struct，this structure was not available before version 4.4.3
typedef struct bef_ai_onekey_enhancement_algParamStream {
    int luminance_target_int0;
    int luminance_target_int1;
    float contrast_factor_float;
    float saturation_factor_float;
    float amount_float;
    float ratio_float;
    float noise_factor_float;
    float current_pixel_weight_float;
    int hdr_version_int;
    float luma_trigger_float;
    float over_trigger_float;
    float under_trigger_float;
    int asf_scene_mode_int;
}bef_ai_onekey_enhancement_algParamStream;

// structure is available in every versions
typedef struct bef_ai_onekey_enhancement_config {
    int width;  //input width
    int height; //input height
    const char * kernelBinPath;  //readable and writable path
    bool disableHdr;  //open HDR
    bool oneKeyRecordHdrV2;   //select hdr v1, v2 algorithm
    bool asnycProcess;   //algorithm asynchronous execution switch
    bool disableNightScene;  //algorithm disable Night Scene
    bool disableDayScene;  //algorithm disable Day Scene
    bool disableAsf;  //turn on sharpening
    bef_ai_lens_power_level level;  //iOS does not need to be set
    bef_one_key_scene_strategy_mode sceneMode;
}bef_ai_onekey_enhancement_config;
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_image_quality_enhancement_handle\* |Create smart vision enhance algorithm handle. |
|config |bef_ai_onekey_enhancement_config \* |Configuration parameters when the algorithm is initialized. |


**Return value:** 

Success returns BEF_RESULT_SUC, while failure returns the corresponding error code. For more information, refer to bef_effect_ai_public_define.h

<span id="334bf06d"></span>
## 2. Smart vision enhance algorithm execution

```C
BEF_SDK_API bef_effect_result_t
bef_ai_image_quality_enhancement_onekey_enchance_process(bef_image_quality_enhancement_handle handle,
                                                         const bef_ai_onekey_process_config* config,
                                                         const bef_ai_lens_data* input,
                                                         bef_ai_lens_data *output);

typedef struct bef_ai_onekey_process_config {
    bef_ai_onekey_detect_config detectConfig;
    int width;
    int height;
    bool isFirstFrame;
    int initDecayFrames;//dynamic scene switching over with fade effect (default 30)
    bool isProtectFace;
    int faceNum;
    bef_ai_rect* faceList;
    bef_ai_onekey_enhancement_algParamStream algParamStream; // Version 4.4.3 add new algorithm parameters struct
}bef_ai_onekey_process_config;

typedef union bef_ai_lens_data{
    int texture [2]; //If it is a texture, the index of the texture here, the texture of ios currently only supports the texture of metal, android needs oes texture, and the texture is placed in the 0 position
    void * buffer;   //If it is data input, iOS pass the pointer to pixelBuffer
}bef_ai_lens_data;
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_image_quality_enhancement_handle |Smart vision enhance algorithm handle. |
|config |const bef_ai_onekey_process_config \* |Configuration parameters when the algorithm is initialized. |
|input |bef_ai_lens_data \* |Smart vision enhance algorithm input. |
|output |bef_ai_lens_data \* |Smart vision enhance algorithm output. |


**Return value:** 

Success returns BEF_RESULT_SUC, while failure returns the corresponding error code. For more information, refer to bef_effect_ai_public_define.h

<span id="fb4b70c3"></span>
## 3. Release the handle

```C
BEF_SDK_API bef_effect_result_t
bef_ai_image_quality_enhancement_onekey_enchance_destroy(bef_image_quality_enhancement_handle handle);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|Handle |bef_image_quality_enhancement_handle |Smart vision enhance algorithm handle. |


**Return value:** 

Success returns BEF_RESULT_SUC, while failure returns the corresponding error code. For more information, refer to bef_effect_ai_public_define.h

<span id="df9c33a8"></span>
## 4. Smart vision enhance algorithm authorization

```C
//Offline license
BEF_SDK_API bef_effect_result_t
bef_ai_image_quality_enhancement_onekey_enchance_check_license(
    bef_image_quality_enhancement_handle handle, 
    const char* license_path);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_image_quality_enhancement_handle |Smart vision enhance algorithm handle. |
|licensePath |const char \* |License file path. |


**Return value:** 

Success returns BEF_RESULT_SUC, while failure returns the corresponding error code. For more information, refer to bef_effect_ai_public_define

<span id="Java API"></span>
# Java API

**Interface Description**

For the detailed description, refer to the file: com.bytedance.labcv.effectsdk.OneKeyEnhance.java

<span id="9fe96b03"></span>
## 1. Initialize smart vision enhance algorithm handle

```Java
public int create(
    String licensePath, 
    boolean onlineLicense,
    AlgParamStream algParamStream, // Version 4.4.3 add new algorithm parameters struct
    InitConfig config)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|licensePath |String |License file absolute path. |
|onlineLicense |boolean |If it is an online license. |
|algParamStream |AlgParamStream |Algorithm extra parameters. |
|config |InitConfig |Initialize configuration parameters. |


**Return value:** 

Returns BEF_RESULT_SUC successfully, otherwise returns the corresponding error code.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">InitConfig can refer to <code>com.bytedance.labcv.effectsdk.OneKeyEnhance.java</code>, and its definition is consistent with the C interface <code>bef_ai_image_quality_enhancement_onekey_enhance.h</code>.</div>


<div data-tips="true" data-tips-type="warning">AlgParamStream which is added in V4.4.3, can refer to <code>com.effectsar.labcv.effectsdk.OneKeyEnhance.java</code>.</div>


<span id="9fc0b54e"></span>
## 2. Smart vision enhance algorithm processing

```Java
public int process(
    int textureId, 
    AlgParamStream algParamStream, // Version 4.4.3 add new algorithm parameters struct
    ProcessConfig processConfig)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|textureId |int |Input texture ID |
|algParamStream |AlgParamStream |algorithm extra parameters |
|processConfig |ProcessConfig |processing configuration parameters |


For ProcessConfig, refer to `com.bytedance.labcv.effectsdk.OneKeyEnhance.java`, and its definition is consistent with the C interface `bef_ai_image_quality_enhancement_onekey_enhance.h`.

<span id="c058bac0"></span>
## 3. Release the handle

```Java
public void release()
```


<span id="FAQ"></span>
## FAQ

<span id="4f792632"></span>
### 1. If there is any exception, check if there are any of the following types of logs

A: It is recommended to first check the log of the following tag output Error type:


* **bef_effect_ai**

* **SMASH_E_LOG**

* **EffectSDK**
