---
title: "Adaptive sharpening"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-adapt-super-resolution"
---

The basic goal of Self\-Adaptation sharpening algorithm:


1. Improve sharpness without enhancing noise level;

2. Improve the traditional sharpening prone to white edge, edge halo artifacts phenomenon.


Version 4.1.0.3 adds algorithm. Note that machines below iOS11 do not support image quality related algorithms except for frame insertion.

<span id="6108fc56"></span>
# Technical specifications


|**Category** |**Supported Formats** |
|---|---|
|Platforms |* Android<br><br>* iOS |
|Support input format |* Android: oes texture<br><br>* iOS: yuv420p, 420f pixelbuffer |
|Memory footprint |< 34M (test device OPPO R11) |
|Detection speed |< 13 ms (test device OPPO R11) |


<span id="17d642f7"></span>
# C Interface Description

For the detailed interface description, refer to header file : bef_ai_image_quality_enhancement_adaptive_sharpen

<span id="703b33d2"></span>
## 1. Create Adaptation sharpening algorithm handle

```C
BEF_SDK_API bef_effect_result_t 
bef_ai_image_quality_enhancement_adaptive_sharpen_create(bef_image_quality_enhancement_handle* handle, const bef_ai_asf_init_config* config);

typedef struct bef_ai_asf_init_config{
    bef_ai_asf_scene_mode scene_mode;   //scene mode
    void* context; //iOS can input metal of outside，if it is nullptr，should build device in the internal lens
#if defined(__ANDROID__) || defined(TARGET_OS_ANDROID)
    bef_ai_lens_power_level level; //iOS do not need set
#endif
    bef_ai_lens_data_type input_type; // the type of input data
    bef_ai_lens_data_type output_type; // the type of output data
    
    int frame_width;//frame width
    int frame_height;//frame height
    float amount;//Sharpening intensity gain, default -1 (invalid value), i.e. no adjustment. Valid value is >0: when set >1, it increases the sharpening intensity, and when set <1, it decreases the sharpening intensity.
    float over_ratio;//Black and white edge tolerance gain, the default -1 (invalid value), that is, no adjustment. Valid value is > 0: when the amount > 1, if it is found that increasing the amount clarity is not significantly increased, it may be necessary to slightly increase the over_ratio, the empirical formula is: over_ratio= 1+ a * (amount -1), where the scale factor a can be adjusted, belongs to 0 ~ 1 range.
    float edge_weight_gamma;//Adjusts the sharpening intensity for the low and mid frequency edges. Default -1 (invalid value), i.e. no adjustment. Valid values are >0
    int diff_img_smooth_enable;//On reduces the edge artifacts from sharpening, but the sharpening intensity will be weaker than when off, default -1 (invalid value), i.e. keep the internal setting, currently set to on. Valid values are 0 or 1, 0 - off, 1 - on

}bef_ai_asf_init_config;
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|Handle |bef_image_quality_enhancement_handle \* |Adaptation sharpening algorithm handle created. |
|Config |bef_ai_asf_init_config \* |Algorithm configuration parameters when initialized. |


**Return value:** 

Success returns BEF_RESULT_SUC, failure returns the corresponding error code. For more information, refer to bef_effect_ai_public_define.

<span id="feed54fa"></span>
## 2. Input parameter property configuration

```C
BEF_SDK_API bef_effect_result_t
bef_ai_image_quality_enhancement_adaptive_sharpen_set_property(bef_image_quality_enhancement_handle handle, const bef_ai_asf_property* config);

typedef struct bef_ai_asf_property{
    bef_ai_asf_scene_mode scene_mode;    //scene mode
    int frame_width;//frame width
    int frame_height;//frame height
    float amount;//Sharpening intensity gain, default -1 (invalid value), i.e. no adjustment. Valid value is >0: when set >1, it increases the sharpening intensity, and when set <1, it decreases the sharpening intensity.
    float over_ratio;//Black and white edge tolerance gain, the default -1 (invalid value), that is, no adjustment. Valid value is > 0: when the amount > 1, if it is found that increasing the amount clarity is not significantly increased, it may be necessary to slightly increase the over_ratio, the empirical formula is: over_ratio= 1+ a * (amount -1), where the scale factor a can be adjusted, belongs to 0 ~ 1 range.
    float edge_weight_gamma;//Adjusts the sharpening intensity for the low and mid frequency edges. Default -1 (invalid value), i.e. no adjustment. Valid values are >0
    int diff_img_smooth_enable;//On reduces the edge artifacts from sharpening, but the sharpening intensity will be weaker than when off, default -1 (invalid value), i.e. keep the internal setting, currently set to on. Valid values are 0 or 1, 0 - off, 1 - on
}bef_ai_asf_property;
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|Handle |bef_image_quality_enhancement_handle |Adaptation sharpening algorithm handle. |
|Config |bef_ai_asf_property \* |input parameter properties. |


**Return value:** 

Success returns BEF_RESULT_SUC, failure returns the corresponding error code. For more information, refer to bef_effect_ai_public_define

<span id="c5cc7450"></span>
## 3. Adaptation sharpening algorithm process

```C
BEF_SDK_API bef_effect_result_t
bef_ai_image_quality_enhancement_adaptive_sharpen_process(bef_image_quality_enhancement_handle handle, const bef_ai_asf_input* input, bef_ai_asf_output *output);

typedef struct bef_ai_asf_input{
    bef_ai_lens_data data;   // input data
    bef_ai_lens_data_type type;// input data format
}bef_ai_asf_input;

typedef struct bef_ai_asf_output{
    bef_ai_lens_data data;   // output data, will fill the corresponding output part according to the input
    bef_ai_lens_data_type type;// output data format
}bef_ai_asf_output;
```


**Parameter:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|Handle |bef_image_quality_enhancement_handle |Adaptation sharpening algorithm handle. |
|Config |bef_ai_asf_input \* |Adaptation sharpening algorithm input. |
|Input |bef_ai_asf_output \* |Adaptation sharpening algorithm output |


**Return value:** 

Success returns BEF_RESULT_SUC, failure returns the corresponding error code. For more information, refer to bef_effect_ai_public_define

<span id="38eea926"></span>
## 4. Release the handle

```C
BEF_SDK_API bef_effect_result_t 
bef_ai_image_quality_enhancement_adaptive_sharpen_destory(bef_image_quality_enhancement_handle handle);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|Handle |bef_image_quality_enhancement_handle |Adaptation sharpening algorithm handle. |


**Return value:** 

Success returns BEF_RESULT_SUC, failure returns the corresponding error code. For more information, refer to bef_effect_ai_public_define

<span id="b3558a84"></span>
## 5. Adaptation sharpening algorithm authorization

```C
BEF_SDK_API bef_effect_result_t 
bef_ai_image_quality_enhancement_adaptive_sharpen_check_license(bef_image_quality_enhancement_handle handle, const char* license_path);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|Handle |bef_image_quality_enhancement_handle |Adaptation sharpening algorithm handle |
|licensePath |const char \* |License file path. |


**Return value:** 

Success returns BEF_RESULT_SUC, failure returns the corresponding error code. For more information, refer to bef_effect_ai_public_define

<span id="Java Interface description"></span>
# Java Interface description

For the detailed interface description, refer to file: com.bytedance.labcv.effectsdk.AdaptiveSharpen.java

<span id="2703645f"></span>
## 1. Initialize Adaptation Sharpen Handle

```Java
public int init(
    String licensePath, 
    int maxHeight, 
    int maxWidth, 
    int mode, 
    int level, 
    float amount, 
    float overRatio, 
    float edgeWeightGamma, 
    int diffImgSmoothEnable, 
    boolean onlineLicense)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|licensePath |String |Absolute path to authorization file. |
|maxHeight |int |Video Height. |
|maxWidth |int |video width. |
|mode |int |Scene mode |
|Level |int |Incoming frequency setting level, the default is auto level (default refers to the adjustment with the system, low is the use of low frequency, normal is the use of frequency, high is the use of high frequency, auto is the sdk internal automatic adjustment according to the model. |
|Amount |float |Sharpening intensity gain, default \-1 (invalid value), that is, no adjustment. Valid values are \> 0: When set to \> 1, the sharpening intensity will increase, and when set to < 1, the sharpening intensity will decrease. |
|overRatio |float |Tolerance gain for black and white edges, default \-1 (invalid value), i.e. not adjusted. |
|edgeWeightGamma |float |Adjust the sharpening intensity of the medium and low frequency edges, default \-1 (invalid value), that is, no adjustment. Valid values are \> 0. |
|diffImgSmoothEnable |int |After turning on, the edge artifacts caused by sharpening will be reduced, but the sharpening intensity will be weaker than when it is turned off. The default is \-1 (invalid value), that is, the internal setting is kept, and the current setting is turned on. Valid values are 0 or 1,0\-\-off, 1\-\-on. |
|onlineLicense |boolean |License type. |


**Return value:** 

Successfully returns BEF_RESULT_SUC, otherwise returns the corresponding error code.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">It is only recommended that the business side adjust two parameters: amount and over_ratio.</div>


<span id="833c273b"></span>
## 2. Set input parameter properties

```Java
public int setProperty(
    int sceneMode, 
    int powerLevel, 
    int frameWidth, 
    int frameHeight, 
    float amount, 
    float overRatio, 
    float edgeWeightGamma, 
    int diffImgSmoothEnable)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|sceneMode |int |Scene mode. |
|powerLevel |int |Incoming frequency setting level, the default is auto level (default refers to the adjustment with the system, low is the use of low frequency, normal is the use of frequency, high is the use of high frequency, auto is the sdk internal automatic adjustment according to the model. |
|frameHeight |int |Video height |
|frameWidth |int |video width. |
|Amount |float |Sharpening intensity gain, default \-1 (invalid value), that is, no adjustment. Valid values are \> 0: When set to \> 1, the sharpening intensity will increase, and when set to < 1, the sharpening intensity will decrease. |
|overRatio |float |Tolerance gain for black and white edges, default \-1 (invalid value), i.e. not adjusted. |
|edgeWeightGamma |float |Adjust the sharpening intensity of the medium and low frequency edges, default \-1 (invalid value), that is, no adjustment. Valid values are \> 0. |
|diffImgSmoothEnable |int |After turning on, the edge artifacts caused by sharpening will be reduced, but the sharpening intensity will be weaker than when it is turned off. The default is \-1 (invalid value), that is, the internal setting is kept, and the current setting is turned on. Valid values are 0 or 1,0\-\-off, 1\-\-on. |


<span id="8e085557"></span>
## 3. Adaptation sharpening algorithm processing

```Java
public int process(
    int srcTextureId, 
    Integer destTextureId)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|srcTextureId |int |Enter texture number |
|srcTextureId |Integer |Output texture number |


<span id="a06c791b"></span>
## 4. Release Adaptation Sharpening Handles

```Java
public void release()
```


<span id="49fae2b7"></span>
# FAQ

<span id="ff93536e"></span>
## 1. If there is any exception, check if there are any of the following types of logs

A: It is recommended to first check the log of the following tag output Error type:


* bef_effect_ai

* SMASH_E_LOG

* EffectSDK
