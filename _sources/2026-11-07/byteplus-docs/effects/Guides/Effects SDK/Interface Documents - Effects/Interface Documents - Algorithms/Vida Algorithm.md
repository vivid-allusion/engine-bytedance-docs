---
title: "Vida Algorithm"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-vida-algorithm"
---

Perform image quality scoring on the input image or video stream.

New algorithm added from V4.4.2.

<span id="57cc9963"></span>
# Technical Specifications


|**Category** |**Supported Formats** |
|---|---|
|Platforms |* Android<br><br>* iOS |
|Input format |RGBA8888 does not support data with padding |
|Model List |Face Score vida_face_model.bytenn Aesthetics vida_aes_model.bytenn Clarity iOS level0_cpu.bytenn Android level0_gpu.bytenn |
|Memory usage |< 83.64M (test device: OppoR11) |
|Detection speed |face <10.48ms, aes <65.5ms, clarity <32.89ms (test device: OppoR11) |


<span id="b67c2d29"></span>
# C interface description

For more detailed interface descriptions, refer to the header file: bef_ai_image_quality_enhancement_vida.h

<span id="5955cae0"></span>
## 1. Create Vida algorithm handle

```C
typedef struct bef_ai_vida_init_config {
Const char * modelPath;  // Model Path
Const char * kernelBinPath;  // Readable/Writable Path
bef_ai_vida_type vidaType;   / /model type, vida type
bef_ai_lens_backend_type backendType;   //Run bachend, for sharpness Algorithm, android select gpu , ios select cpu
    int numThread;  //only make sense when backendType is CPU, default set 2
    float alpha;    // 1.0
    float beta;     //  0.0
Const char * tempDirPath;   // iOS directory where temporary files are stored, only the coreml model takes effect, pass empty is fine
}bef_ai_vida_init_config;

BEF_SDK_API bef_effect_result_t
bef_ai_image_quality_enhancement_vida_create(bef_image_quality_enhancement_handle* handle, bef_ai_vida_init_config* config);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_image_quality_enhancement_handle \* |Handle created by Vida algorithm. |
|config |bef_ai_vida_init_config \* |Config created by Vida algorithm. |


**Return value:** 

Success returns BEF_RESULT_SUC, while failure returns the corresponding error code. For more information, refer to bef_effect_ai_public_define.h

<span id="f6d27721"></span>
## 2. License for Vida

```C
#if defined(__ANDROID__) || defined(TARGET_OS_ANDROID)
#include<jni.h>
BEF_SDK_API bef_effect_result_t
bef_ai_image_quality_enhancement_vida_check_license(JNIEnv* env, jobject context, bef_image_quality_enhancement_handle handle, const char* license_path);
#endif

#ifdef __APPLE__
BEF_SDK_API bef_effect_result_t
bef_ai_image_quality_enhancement_vida_check_license(bef_image_quality_enhancement_handle handle, const char* license_path);
#endif

BEF_SDK_API bef_effect_result_t
bef_ai_image_quality_enhancement_vida_check_online_license(bef_image_quality_enhancement_handle handle, const char* license_path);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_image_quality_enhancement_handle |Created Vida handle. |
|license_path |const unsigned char \* |License file path. |
|env |JNIEnv \* |Android JNI environment. |
|jobject |context |Android context. |


**Return value:** 

Success returns BEF_RESULT_SUC, while failure returns the corresponding error code. For more information, refer to bef_effect_ai_public_define.h

<span id="0c32fbe1"></span>
## 3. Process Vida algorithm

```C
EF_SDK_API bef_effect_result_t
bef_ai_image_quality_enhancement_vida_process(bef_image_quality_enhancement_handle handle, void* data, int width, int height, float* result);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_image_quality_enhancement_handle |Created Vida handle. |
|data |void \* |Buffer first address. |
|width |int |Buffer width. |
|height |int |Buffer height. |
|result |float \* |Return value of Vida. |


**Return value:** 

Success returns BEF_RESULT_SUC, while failure returns the corresponding error code. For more information, refer to bef_effect_ai_public_define.h

<span id="7720a856"></span>
## 4. Destroy handle

```C
BEF_SDK_API bef_effect_result_t
bef_ai_image_quality_enhancement_vida_destory(bef_image_quality_enhancement_handle handle);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_image_quality_enhancement_handle |Created Vida handle. |


**Return value:** 

Success returns BEF_RESULT_SUC, while failure returns the corresponding error code. For more information, refer to bef_effect_ai_public_define.h

<span id="Java interface description"></span>
# Java interface description

**Interface Description**

For more detailed interface descriptions, refer to the file: com.bytedance.labcv.effectsdk.Vida.java

<span id="c3946833"></span>
## 1. Initialize vida handle

```Java
public int init(Context context, VidaInitConfig config, String licensePath, boolean onlineLicense)
```


**Parameters**:


|**Name** |**Type** |**Description** |
|---|---|---|
|context |String |Java context. |
|config |config |Initial configuration for Vida. |
|licensePath |String |License file absolute path. |
|onlineLicense |boolean |License type, offline. Set to false. |


**Return value:** 

Return BEF_RESULT_SUC successfully, otherwise return the corresponding error code.

<span id="92b104ff"></span>
## 2. Process of Vida

```Java
public float process(ByteBuffer buffer, int width, int height)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|buffer |ByteBuffer |Input image data. |
|Width |int |Width of the input image in pixels. |
|Height |int |Height of the input image in pixels. |


**Return value:** 

The return value is the float score.

<span id="0d017830"></span>
## 4. Release Handle

```Java
 int destroy();
```


<span id="FAQ"></span>
## FAQ

<span id="27d7c121"></span>
### 1. If any exception occurs, check if there are any of the following types of logs

A: It is recommended to first look at the following tags output Error type logs:


* **bef_effect_ai**

* **SMASH_E_LOG**

* **EffectSDK**

* **lens**


<span id="615c4baa"></span>
## Error code

Refer to [Error code table].
