---
title: "Effects Interface - C"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-c-api"
---

<span id="C interface"></span>
# C Interface

Effects are a collection of multiple features, including beauty retouching, filters, makeup, stickers and more. Their related interfaces are defined in the header file `bef_effect_ai_api.h`. The effect algorithm supports both texture input and buffer data input. See the relevant section for supported formats.

<span id="1. Create special effects handle"></span>
## 1. Create Effect Handle

```Plain
BEF_SDK_API bef_effect_result_t bef_effect_ai_create( bef_effect_handle_t *handle );
```


**Parameters**


|Parameter Name |Type |Description |
|---|---|---|
|handle |bef_effect_handle_t\* |Pointer to the created effect handle |


**Return Value** Returns `BEF_RESULT_SUC` on success; returns the corresponding error code on failure. See `bef_effect_ai_public_define.h` for details.

<span id="0b72781e"></span>
# 2. Authorize Effect Handle

```Plain
#ifdef __ANDROID__
BEF_SDK_API bef_effect_result_t bef_effect_ai_check_license(
    JNIEnv* env,
    jobject context,
    bef_effect_handle_t handle,
    const char *license_path
);
#else
BEF_SDK_API bef_effect_result_t bef_effect_ai_check_license(
    bef_effect_handle_t handle,
    const char *license_path
);
#endif
```


**Parameters**


|Parameter Name |Type |Description |
|---|---|---|
|env |JNIEnv \* |JNI environment pointer |
|context |jobject |JNI object |
|handle |bef_effect_handle_t |Created effect handle |
|licensePath |const char \* |Path to license file |


**Return Value** Returns `BEF_RESULT_SUC` on success; returns the corresponding error code on failure. See `bef_effect_ai_public_define.h` for details.

<span id="f5fe4d61"></span>
# 3. Initialize Effect Handle

Before subsequent calls to the effect handle, license verification must be completed. Otherwise, all subsequent calls will fail.

```Plain
BEF_SDK_API bef_effect_result_t bef_effect_ai_init( bef_effect_handle_t handle, int width, int height, const char  *strModelDir, const char * deviceName );
```


When initializing the effect handle, ensure `strModelDir` points to the directory containing our deep learning models.

**Parameters**


|Parameter Name |Type |Description |
|---|---|---|
|handle |bef_effect_handle_t |Created effect handle |
|width |int |Width of input texture |
|height |int |Height of input texture |
|strModelDir |const char \* |Directory path of resource files |
|deviceName |const char \* |Device name; pass empty string `""` in most cases |


**Return Value** Returns `BEF_RESULT_SUC` on success; returns the corresponding error code on failure. See `bef_effect_ai_public_define.h` for details. If you need overlay effects (beauty retouching, face reshaping, body retouching, makeup, etc.), you also need to initialize the composer or configure composer to coexist with stickers. Refer to 18. Set whether overlay effects coexist with stickers and 19. Initialize composer.

<span id="40141c9b"></span>
# 4. Set Input Frame Width and Height

```Plain
BEF_SDK_API bef_effect_result_t bef_effect_ai_set_width_height( bef_effect_handle_t handle, int width, int height );
```


**Parameters**


|Parameter Name |Type |Description |
|---|---|---|
|handle |bef_effect_handle_t |Created effect handle |
|width |int |Texture width |
|height |int |Texture height |


**Return Value** Returns `BEF_RESULT_SUC` on success; returns the corresponding error code on failure. See `bef_effect_ai_public_define.h` for details.

<span id="3479cdd0"></span>
# 5. Set Phone Orientation

Set the device rotation angle of the phone. The current rotation angle must be set before processing image data.

```Plain
BEF_SDK_API bef_effect_result_t bef_effect_ai_set_orientation( bef_effect_handle_t handle, bef_ai_rotate_type orientation );
```


**Parameters**


|Parameter Name |Type |Description |
|---|---|---|
|handle |bef_effect_handle_t |Created effect handle |
|orientation |bef_ai_rotate_type |Rotation angle |


**Return Value** Returns `BEF_RESULT_SUC` on success; returns the corresponding error code on failure. See `bef_effect_ai_public_define.h` for details.

<span id="a283f792"></span>
# 6. Set Beauty Type

Set resources for beauty retouching (skin smoothing, sharpening).

```Plain
BEF_SDK_API  bef_effect_result_t bef_effect_ai_set_beauty( bef_effect_handle_t handle, const char *strBeautyName );
```


This API is used to configure beauty effects for v2.6 and earlier versions. Starting from v2.7, you **must** use `bef_effect_ai_composer_set_nodes` to configure beauty and other effects.

**Parameters**


|Parameter Name |Type |Description |
|---|---|---|
|handle |bef_effect_handle_t |Created effect handle |
|strBeautyName |const char \* |Path to beauty resource |


**Return Value** Returns `BEF_RESULT_SUC` on success; returns the corresponding error code on failure. See `bef_effect_ai_public_define.h` for details.

<span id="40f28220"></span>
# 7. Set Makeup Type

```Plain
BEF_SDK_API bef_effect_result_t bef_effect_ai_set_buildin_makeup( bef_effect_handle_t handle, const char* strMakeupName );
```


This API is used to configure makeup effects for v2.6 and earlier versions. Starting from v2.7, you **must** use `bef_effect_ai_composer_set_nodes` to configure makeup and other effects.

**Parameters**


|Parameter Name |Type |Description |
|---|---|---|
|handle |bef_effect_handle_t |Created effect handle |
|strMakeupName |const char \* |Path to makeup resource |


**Return Value** Returns `BEF_RESULT_SUC` on success; returns the corresponding error code on failure. See `bef_effect_ai_public_define.h` for details.

<span id="5dc8b3bf"></span>
# 8. Set Face Reshape Type

```Plain
BEF_SDK_API bef_effect_result_t bef_effect_ai_set_reshape_face( bef_effect_handle_t handle, const char *strPath );
```


This API is used to configure face reshaping for v2.6 and earlier versions. Starting from v2.7, you **must** use `bef_effect_ai_composer_set_nodes` to configure face reshaping and other effects.

**Parameters**


|Parameter Name |Type |Description |
|---|---|---|
|handle |bef_effect_handle_t |Created effect handle |
|strPath |const char \* |Path to face reshaping resource |


**Return Value** Returns `BEF_RESULT_SUC` on success; returns the corresponding error code on failure. See `bef_effect_ai_public_define.h` for details.

<span id="dc3c6fda"></span>
# 9. Set Face Reshape Intensity

```Plain
BEF_SDK_API bef_effect_result_t bef_effect_ai_update_reshape_face( bef_effect_handle_t handle, const float fIntensity );
```


This API is used to configure face reshaping intensity for v2.6 and earlier versions. Starting from v2.7, you **must** use `bef_effect_ai_composer_update_node` to configure face reshaping intensity.

**Parameters**


|Parameter Name |Type |Description |
|---|---|---|
|handle |bef_effect_handle_t |Created effect handle |
|fIntensity |const float |Reshaping intensity |


**Return Value** Returns `BEF_RESULT_SUC` on success; returns the corresponding error code on failure. See `bef_effect_ai_public_define.h` for details.

```Plain
BEF_SDK_API bef_effect_result_t bef_effect_ai_update_reshape_face_intensity( bef_effect_handle_t handle, const float eyeIntensity, const float cheekIntensity );
```


**Parameters**


|Parameter Name |Type |Description |
|---|---|---|
|handle |bef_effect_handle_t |Created effect handle |
|eyeIntensity |const float |Eye enlargement intensity |
|cheekIntensity |const float |Face slimming intensity |


**Return Value** Returns `BEF_RESULT_SUC` on success; returns the corresponding error code on failure. See `bef_effect_ai_public_define.h` for details.

<span id="452bbd10"></span>
# 10. Set Split\-Screen Filter

```Plain
BEF_SDK_API bef_effect_result_t bef_effect_ai_switch_color_filter_v2( bef_effect_handle_t handle, const char *leftFilterPath, const char *rightFilterPath, float position );
```


**Parameters**


|Parameter Name |Type |Description |
|---|---|---|
|handle |bef_effect_handle_t |Created effect handle |
|leftFilterPath |const char \* |Left filter resource path |
|rightFilterPath |const char \* |Right filter resource path |
|position |float |Split position |


**Return Value** Returns `BEF_RESULT_SUC` on success; returns the corresponding error code on failure. See `bef_effect_ai_public_define.h` for details.

<span id="293293ef"></span>
# 11. Set Filter

```Plain
BEF_SDK_API bef_effect_result_t bef_effect_ai_set_color_filter_v2( bef_effect_handle_t handle, const char *strPath );
```


**Parameters**


|Parameter Name |Type |Description |
|---|---|---|
|handle |bef_effect_handle_t |Created effect handle |
|strPath |const char \* |Filter resource path |


**Return Value** Returns `BEF_RESULT_SUC` on success; returns the corresponding error code on failure. See `bef_effect_ai_public_define.h` for details.

<span id="5b77e2bf"></span>
# 12. Set Sticker

```Plain
BEF_SDK_API bef_effect_result_t bef_effect_ai_set_effect( bef_effect_handle_t handle, const char *strPath );
```


**Parameters**


|Parameter Name |Type |Description |
|---|---|---|
|handle |bef_effect_handle_t |Created effect handle |
|strPath |const char \* |Sticker resource path |


**Return Value** Returns `BEF_RESULT_SUC` on success; returns the corresponding error code on failure. See `bef_effect_ai_public_define.h` for details.

<span id="4651f612"></span>
# 13. Set Virtual Background Image

This API updates virtual background or green screen background. Before use, configure the virtual/green screen background asset package (refer to section 12 Set Sticker).

```Plain
BEF_SDK_API bef_effect_result_t bef_effect_ai_set_render_cache_texture(
    bef_effect_handle_t handle,
    const char* key,
    const char* path);
```


**Parameters**


|Parameter Name |Type |Description |
|---|---|---|
|handle |bef_effect_handle_t |Effect handle |
|key |const char\* |Key for virtual background, fixed as `"BCCustomBackground"` |
|path |const char\* |Absolute path of input image; SDK parses it into texture |


**Return Value** Returns `BEF_RESULT_SUC` on success; returns error code on failure.

<span id="2c5fd2ab"></span>
# 14. Set Virtual Background Buffer

This API updates virtual background or green screen background. Configure virtual/green screen background before calling.

```Plain
BEF_SDK_API bef_effect_result_t bef_effect_ai_set_render_cache_texture_with_buffer(
    bef_effect_handle_t handle,
    const char* key,
    bef_ai_image* image);
```


**Parameters**


|Parameter Name |Type |Description |
|---|---|---|
|handle |bef_effect_handle_t |Effect handle |
|key |const char\* |Key for virtual background, fixed as `"BCCustomBackground"` |
|image |bef_ai_image\* |Image data containing buffer, width, height, format, etc. |


**Return Value** Returns `BEF_RESULT_SUC` on success; returns error code on failure.

<span id="6078714e"></span>
# 15. Remove Virtual Background

```Plain
BEF_SDK_API bef_effect_result_t  bef_effect_ai_remove_render_cache_external_texture(
    bef_effect_handle_t handle,
    const char* key);
```


**Parameters**


|Parameter Name |Type |Description |
|---|---|---|
|handle |bef_effect_handle_t |Effect handle |
|key |const char\* |Key for virtual background, fixed as `"BCCustomBackground"` |


**Return Value** Returns `BEF_RESULT_SUC` on success; returns error code on failure.

<span id="e6513343"></span>
# 16. Set Virtual Background Texture

New API added in v4.7.1. This API updates virtual background or green screen background. Configure virtual/green screen background before calling.

```Plain
BEF_SDK_API bef_effect_result_t  bef_effect_ai_set_render_cache_external_texture(
    bef_effect_handle_t handle,
    const char* key,
    int texture,
    int width,
    int height);
```


**Parameters**


|Parameter Name |Type |Description |
|---|---|---|
|handle |bef_effect_handle_t |Effect handle |
|key |const char\* |Key for virtual background, fixed as `"BCCustomBackground"` |
|texture |int |Image texture ID |
|width |int |Texture width |
|height |int |Texture height |


**Return Value** Returns `BEF_RESULT_SUC` on success; returns error code on failure.

<span id="0623436c"></span>
# 17. Set Virtual Background Texture (with Rotation)

New API added in v4.7.1. This API updates virtual background or green screen background. Configure virtual/green screen background before calling.

```Plain
BEF_SDK_API bef_effect_result_t  bef_effect_ai_set_render_cache_external_texture_with_rotation(
    bef_effect_handle_t handle,
    const char* key,
    int texture,
    int width,
    int height,
    bef_ai_rotate_type rotation);
```


**Parameters**


|Parameter Name |Type |Description |
|---|---|---|
|handle |bef_effect_handle_t |Effect handle |
|key |const char\* |Key for virtual background, fixed as `"BCCustomBackground"` |
|texture |int |Image texture ID |
|width |int |Texture width |
|height |int |Texture height |
|rotation |bef_ai_rotate_type |Rotation angle |


**Return Value** Returns `BEF_RESULT_SUC` on success; returns error code on failure.

<span id="5c00655b"></span>
# 18. Run Algorithm Detection

<span id="f22aef9f"></span>
### API supporting texture input

```Plain
BEF_SDK_API bef_effect_result_t bef_effect_ai_algorithm_texture( bef_effect_handle_t handle, unsigned int textureid_src, double timeStamp );
```


**Parameters**


|Parameter Name |Type |Description |
|---|---|---|
|handle |bef_effect_handle_t |Created effect handle |
|textureid_src |unsigned int |Input texture |
|timeStamp |double |Texture timestamp |


**Return Value** Returns `BEF_RESULT_SUC` on success; returns the corresponding error code on failure. See `bef_effect_ai_public_define.h` for details.

<span id="a39b6e70"></span>
### API supporting buffer input

This API does not support parallel rendering. Use `bef_effect_ai_algorithm_texture_with_buffer` if parallel rendering is required.

```Plain
BEF_SDK_API bef_effect_result_t bef_effect_ai_algorithm_buffer(
    bef_effect_handle_t handle,
    const unsigned char *img_in,
    bef_ai_pixel_format fmt_in,
    int image_width,
    int image_height,
    int image_stride,
    double timestamp );
```


**Parameters**


|Parameter Name |Type |Description |
|---|---|---|
|handle |bef_effect_handle_t |Created effect handle |
|img_in |const unsigned char \* |Input buffer |
|fmt_in |bef_ai_pixel_format |Input buffer format |
|image_width |int |Input buffer width |
|image_height |int |Input buffer height |
|timestamp |double |Timestamp |


**Return Value** Returns `BEF_RESULT_SUC` on success; returns the corresponding error code on failure. See `bef_effect_ai_public_define.h` for details.

<span id="65245dd0"></span>
### API supporting both texture and buffer input

This API accepts texture only, buffer only, or both texture and buffer. When passing texture only, its behavior is identical to `bef_effect_ai_algorithm_texture`.

```C
BEF_SDK_API bef_effect_result_t bef_effect_ai_algorithm_texture_with_buffer(bef_effect_handle_t handle,
                                                                             unsigned int texture,
                                                                             const unsigned char *buffer,
                                                                             bef_ai_pixel_format buffer_format,
                                                                             int buffer_width,
                                                                             int buffer_height,
                                                                             int buffer_stride,
                                                                             double timeStamp);
```


**Parameters**


|Parameter Name |Type |Description |
|---|---|---|
|handle |bef_effect_handle_t |Created effect handle |
|texture |unsigned int |Input texture |
|buffer |const unsigned char \* |Input buffer |
|buffer_format |bef_ai_pixel_format |Input buffer format |
|buffer_width |int |Input buffer width |
|buffer_height |int |Input buffer height |
|buffer_stride |int |Input buffer stride |
|timeStamp |double |Timestamp |


**Return Value** Returns `BEF_RESULT_SUC` on success; returns the corresponding error code on failure. See `bef_effect_ai_public_define.h` for details.

<span id="e9004627"></span>
# 19. Run Effect Processing

<span id="05743aa6"></span>
### API supporting texture input

```Plain
BEF_SDK_API bef_effect_result_t bef_effect_ai_process_texture( bef_effect_handle_t handle, unsigned int srcTexture, unsigned int dstTexture, double timeStamp );
```


**Parameters**


|Parameter Name |Type |Description |
|---|---|---|
|handle |bef_effect_handle_t |Created effect handle |
|srcTexture |unsigned int |Input texture |
|dstTexture |unsigned int |Output texture |
|timeStamp |double |Texture timestamp |


**Return Value** Returns `BEF_RESULT_SUC` on success; returns the corresponding error code on failure. See `bef_effect_ai_public_define.h` for details.

<span id="30dfb62b"></span>
# 20. Set Intensity

```Plain
BEF_SDK_API bef_effect_result_t bef_effect_ai_set_intensity( bef_effect_handle_t handle, bef_intensity_type intensityType, float fIntensity );
```


This API is used to set beauty intensity for v2.6 and earlier versions. Starting from v2.7, you **must** use `bef_effect_ai_composer_update_node` to set beauty intensity. This API can be used for filter intensity across all versions.

**Parameters**


|Parameter Name |Type |Description |
|---|---|---|
|handle |bef_effect_handle_t |Created effect handle |
|intensityType |bef_intensity_type |Intensity type |
|fIntensity |float |Intensity range [0.0, 1.0]; set to 0 to disable |


**Return Value** Returns `BEF_RESULT_SUC` on success; returns the corresponding error code on failure. See `bef_effect_ai_public_define.h` for details.

<span id="19c54a25"></span>
# 21. Set Overlay Effects (Beauty, Face Reshape, Makeup)

```Plain
BEF_SDK_API bef_effect_result_t bef_effect_ai_composer_set_nodes( bef_effect_handle_t handle, const char *nodePaths[], int nodeNum );
```


**Parameters**


|Parameter Name |Type |Description |
|---|---|---|
|handle |bef_effect_handle_t |Created effect handle |
|nodePaths |const char \* [] |Array of effect resource paths |
|nodeNum |int |Length of the effect resource path array |


**Return Value** Returns `BEF_RESULT_SUC` on success; returns the corresponding error code on failure. See `bef_effect_ai_public_define.h` for details.

<span id="5725e606"></span>
# 22. Set Effect Intensity (Beauty, Face Reshape, Makeup)

```Plain
BEF_SDK_API bef_effect_result_t bef_effect_ai_composer_update_node( bef_effect_handle_t handle, const char *nodePath, const char *nodeTag, float value );
```


**Parameters**


|Parameter Name |Type |Description |
|---|---|---|
|handle |bef_effect_handle_t |Created effect handle |
|nodePath |const char \* |Path of effect resource |
|nodeTag |const char \* |Key of the effect |
|value |float |Intensity for single node of composer effect |


**Return Value** Returns `BEF_RESULT_SUC` on success; returns the corresponding error code on failure. See `bef_effect_ai_public_define.h` for details.

<span id="9c6317f1"></span>
# 23. Set Whether Overlay Effects Coexist with Stickers

> Note: Available in early SDK versions. This API has no effect from v410 onwards. Use `composer_set_nodes` for overlay scenarios. This function must be called during initialization.


```Plain
BEF_SDK_API  bef_effect_result_t bef_effect_ai_composer_set_mode( bef_effect_handle_t handle,  int mode,  int orderType);
```


**Parameters**


|Parameter Name |Type |Description |
|---|---|---|
|handle |bef_effect_handle_t |Created effect handle |
|mode |int |Mode: 0 = composer and stickers cannot coexist; 1 = composer and stickers can coexist |
|orderType |int |Render order of effects and stickers; not supported for now |


**Return Value** Returns `BEF_RESULT_SUC` on success; returns the corresponding error code on failure. See `bef_effect_ai_public_define.h` for details.

<span id="8632d76d"></span>
# 24. Initialize Composer

> Note: There are two types of effects in SDK: overlay effects (beauty retouching, face reshaping, body retouching, makeup, etc.) and stickers (stickers, animoji, etc.). In scenarios where overlay effects and stickers cannot coexist (configured via `bef_effect_ai_composer_set_mode`, disabled by default), call this API to initialize composer before using overlay effects. No need to call this API when overlay effects and stickers are enabled to coexist.


```Plain
BEF_SDK_API bef_effect_result_t bef_effect_ai_set_composer( bef_effect_handle_t handle, const char *strPath );
```


**Parameters**


|Parameter Name |Type |Description |
|---|---|---|
|handle |bef_effect_handle_t |Created effect handle |
|strPath |const char \* |Path to composer resource file |


**Return Value** Returns `BEF_RESULT_SUC` on success; returns the corresponding error code on failure. See `bef_effect_ai_public_define.h` for details.

<span id="b7e27e1b"></span>
# 25. Get Face Detection Result

```Plain
BEF_SDK_API  bef_effect_result_t bef_effect_ai_get_face_detect_result(
    bef_effect_handle_t handle,
    bef_ai_face_info* result);
```


**Parameters**


|Parameter Name |Type |Description |
|---|---|---|
|handle |bef_effect_handle_t |Created effect handle |
|result |bef_ai_face_info \* |Pointer to face detection result |


**Return Value** Returns `BEF_RESULT_SUC` on success; returns the corresponding error code on failure. See `bef_effect_ai_public_define.h` for details.

<span id="83f7ae15"></span>
# 26. Face Occlusion Detection

New API added in v4.8.1

```Plain
BEF_SDK_API bef_effect_result_t bef_effect_ai_get_face_occlusion_result(bef_effect_handle_t handle, bef_ai_face_occlusion_info* result);
```


**Parameters**


|Parameter Name |Type |Description |
|---|---|---|
|handle |bef_effect_handle_t |Created face detection handle |
|result |bef_ai_face_occlusion_info\* |Face occlusion result |


<span id="c63d51af"></span>
# 27. Get Hand Detection Result

```Plain
BEF_SDK_API bef_effect_result_t bef_effect_ai_get_hand_detect_result(
    bef_effect_handle_t handle,
    bef_ai_hand_info *result);
```


**Parameters**


|Parameter Name |Type |Description |
|---|---|---|
|handle |bef_effect_handle_t |Created effect handle |
|result |bef_ai_hand_info \* |Pointer to hand detection result |


**Return Value** Returns `BEF_RESULT_SUC` on success; returns the corresponding error code on failure. See `bef_effect_ai_public_define.h` for details.

<span id="9bdf3a8d"></span>
# 28. Get Body Detection Result

```Plain
BEF_SDK_API bef_effect_result_t bef_effect_ai_get_skeleton_detect_result(
    bef_effect_handle_t handle,
    bef_ai_skeleton_result *result);
```


**Parameters**


|Parameter Name |Type |Description |
|---|---|---|
|handle |bef_effect_handle_t |Created effect handle |
|result |bef_ai_skeleton_result \* |Pointer to body detection result |


**Return Value** Returns `BEF_RESULT_SUC` on success; returns the corresponding error code on failure. See `bef_effect_ai_public_define.h` for details.

<span id="1ad088ad"></span>
# 29. Set Touch Event

Some stickers rely on touch events. Call this API to pass touch events captured by upper layer to SDK to ensure stickers trigger correctly.

```Plain
BEF_SDK_API  bef_effect_result_t bef_effect_ai_process_touch_event(bef_effect_handle_t handle,
          float x, float y);
```


**Parameters**


|Parameter Name |Type |Description |
|---|---|---|
|handle |bef_effect_handle_t |Created effect handle |
|x |float |X coordinate of touch point, bounded by input image width and height |
|y |float |Y coordinate of touch point, bounded by input image width and height |


**Return Value** Returns `BEF_RESULT_SUC` on success; returns the corresponding error code on failure. See `bef_effect_ai_public_define.h` for details.

<span id="521b6a2f"></span>
# 30. Enable Parallel Rendering

Disabled by default. When enabled, SDK runs algorithm detection and effect rendering on separate threads to accelerate processing.

```Plain
BEF_SDK_API bef_effect_result_t bef_effect_ai_use_pipeline_processor(bef_effect_handle_t handle, bool usePipeline);
```


**Parameters**


|Parameter Name |Type |Description |
|---|---|---|
|handle |bef_effect_handle_t |Created effect handle |
|usePipeline |bool |Enable or disable parallel rendering |


**Return Value** Returns `BEF_RESULT_SUC` on success; returns the corresponding error code on failure. See `bef_effect_ai_public_define.h` for details.

<span id="fed3e3f4"></span>
# 31. Set Parallel Rendering Multi Input

When parallel rendering is enabled, algorithm detection and effect rendering run asynchronously. To support multi\-thread processing, avoid reusing the same texture ID / buffer memory for consecutive frames.


* When disabled: SDK will copy textures/buffers passed from upper layer to avoid interference between frames.

* When enabled: Upper layer manages texture/buffer memory and SDK will not perform copy. (You may maintain a texture array and cycle textures, refer to demo implementation.)


Disabled by default.

> Note: This API has compatibility issues and is deprecated.


```Plain
BEF_SDK_API bef_effect_result_t bef_effect_ai_use_3buffer(bef_effect_handle_t handle, bool use3buffer);
```


**Parameters**


|Parameter Name |Type |Description |
|---|---|---|
|handle |bef_effect_handle_t |Created effect handle |
|use3buffer |bool |Whether to use multi\-input mode |


**Return Value** Returns `BEF_RESULT_SUC` on success; returns the corresponding error code on failure. See `bef_effect_ai_public_define.h` for details.

<span id="56f4577c"></span>
# 32. Clear Parallel Rendering Data

After parallel rendering is enabled, SDK caches the previous frame image for asynchronous algorithm and rendering. When frame continuity is broken (camera switch, pause, etc.), the last frame may flash when playback resumes. Call this API to clear internal SDK cache upon frame discontinuity.

```Plain
BEF_SDK_API bef_effect_result_t bef_effect_ai_clean_pipeline_processor_task(bef_effect_handle_t handle)
```


**Parameters**


|Parameter Name |Type |Description |
|---|---|---|
|handle |bef_effect_handle_t |Created effect handle |


**Return Value** Returns `BEF_RESULT_SUC` on success; returns the corresponding error code on failure. See `bef_effect_ai_public_define.h` for details.

<span id="51471bac"></span>
# 33. Destroy Handle

```Plain
BEF_SDK_API void bef_effect_ai_destroy( bef_effect_handle_t handle );
```


**Parameters**


|Parameter Name |Type |Description |
|---|---|---|
|handle |bef_effect_handle_t |Created effect handle |


**Return Value** Returns `BEF_RESULT_SUC` on success; returns the corresponding error code on failure. See `bef_effect_ai_public_define.h` for details.

<span id="f1f0872d"></span>
# **34. Check Whether the Device Supports Black\-Tech Props (Android Only)** 

New interface added in version 4.7.3.

```Plain
bool bef_effect_ai_gpu_is_support()
```


**Return value:**  Returns `true` if supported; returns `false` if not supported.
