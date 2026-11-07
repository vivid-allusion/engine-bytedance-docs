---
title: "Photo Night Scene Augmentation"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-photo-night-scene-augmentation"
---

Photo Night Scene Augmentation provides multi\-frame image synthesis for night scene enhancement.

<span id="15dc8c97"></span>
# Technical specifications


|**Category** |**Supported Formats** |
|---|---|
|Platforms |* Android<br><br>* iOS |
|Input format |* nv21<br><br>* nv12 |
|Requirements |4 consecutive images or 6 consecutive images, except the last frame ev is \-2, the remaining frames ev is 0, application layer. Refer to the demo camera2 captureBurst method. |


<span id="d41ffaae"></span>
# C interface description

For the detailed interface description, refer toHeader File : bef_ai_image_quality_enhancement_photo_night_scene

<span id="4fca3d7e"></span>
## 1. Create Night Scene Augmentation algorithm handle

```C
BEF_SDK_API bef_effect_result_t  
bef_ai_image_quality_enhancement_photo_night_scene_create(bef_image_quality_enhancement_handle* handle,
        const char* skin_seg_path, int width, int height, int image_number,
        bef_ai_lens_yuv_type type);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|Handle |bef_image_quality_enhancement_handle |Created by night algorithm. |
|skin_seg_path |const char \* |Path of skin segmentation model. |
|Width |int |Width of input frame. |
|Height |int |Height of the input frame. |
|image_number |int |Number of input frames: 4 or 6. |
|Type |bef_ai_lens_yuv_type |Type of input frame: nv21 or nv12. |


**Return value:** 

Success returns BEF_RESULT_SUC, while failure returns the corresponding error code. For more information, refer to bef_effect_ai_public_define

<span id="48cfa504"></span>
## 2. Offline authentication

```C
// model_path set to an empty string
bef_effect_result_t
bef_ai_image_quality_enhancement_photo_night_scene_check_license(JNIEnv* env, jobject context, bef_image_quality_enhancement_handle handle, const char* license_path) 
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|Env |JNIEnv |Java environment. |
|context |jobject |Java context. |
|Handle |bef_image_quality_enhancement_handle |Handle to night scene algorithm. |
|license_path |const char \* |Model file path. |


<span id="c1b774a0"></span>
## 3. Night scene enhancement algorithm process

```C
bef_effect_result_t
bef_ai_image_quality_enhancement_photo_night_scene_process(bef_image_quality_enhancement_handle handle, void** input, int input_size, void **output)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|Handle |bef_image_quality_enhancement_handle |Handle to night scene algorithm. |
|Input |void \*\* |Input buffer array. Each void \* is the address of each frame. |
|input_size |int |The frame number of the input image must be 4 or 6. |
|Output |void \*\* |The address of the output image, explame void \* ret_addr = nullptr; ret_addr the return value is the data of the night scene enhancement frame. |


**Return value:** 

Success returns BEF_RESULT_SUC, while failure returns the corresponding error code. For more information, refer to bef_effect_ai_public_define

<span id="a75efef2"></span>
## 4. Release the handle

```C
BEF_SDK_API void
bef_ai_image_quality_enhancement_photo_night_scene_destroy(bef_image_quality_enhancement_handle handle);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|Handle |bef_image_quality_enhancement_handle |Handle to night scene algorithm. |


<span id="Java Interface description"></span>
# Java Interface description

For the detailed interface description, refer to file: com.bytedance.labcv.effectsdk.PhotoNightScene.java

<span id="ec290905"></span>
## 1. Initialize night handle

```Java
public int init(
    Context context, String license, String skinSegPath,
     int width, int height, int imageNumber, 
     int format, boolean onlineLicense)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|context |Context |Application context. |
|skinSegPath |String |Skin Segmentation Model Path. |
|width |int |Width of input. |
|height |int |Input height. |
|imageNumber |int |Number of input frames. |
|format |BytedEffectConstants.YUV420Type |nv12 or nv21. |
|onlineLicense |boolean |License type. |


**Return value:** 

Successfully returns BEF_RESULT_SUC, otherwise returns the corresponding error code.

<span id="769909b8"></span>
## 2. Night scene process

```Java
public ByteBuffer process(
     ByteBuffer process(ByteBuffer[] input))
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|Input |ByteBuffer [] |Input image. The array needs to be direct_buffer, |


**Return value:** 

ByteBuffer returns a buffer that is consistent with the input type, and must be consistent with the initialization type

<span id="9626ee88"></span>
## 3. Release algorithm handle

```Java
public void destroy()
```


<span id="052ef3c5"></span>
# FAQ

<span id="146ffdcd"></span>
## 1. If there is any exception, check if there are any of the following types of logs

A: It is recommended to first check the log of the following tag output Error type:


* bef_effect_ai

* SMASH_E_LOG

* EffectSDK
