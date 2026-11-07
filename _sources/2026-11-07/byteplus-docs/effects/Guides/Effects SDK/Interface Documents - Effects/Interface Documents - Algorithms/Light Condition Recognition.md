---
title: "Light Condition Recognition"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-light-condition-recognition"
---

Light Detection SDK provides the capability of real\-time detection of 7 light types at certain frames.


|**Type value** |**Type** |
|---|---|
|0 |Indoor warm white |
|1 |indoor cool white |
|2 |indoor low\-light |
|3 |Sunny |
|4 |Cloudy |
|5 |Night |
|6 |Backlight |


<span id="C Interface Description"></span>
# C Interface Description

For detailed interface description, view header file: bef_effect_ai_lightcls.h

<span id="1. Create a light detection handle"></span>
## 1. Create a light detection handle

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_lightcls_create(
        bef_effect_handle_t *handle,
        const char *model_path,
        int fps
);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The created light detection handle. |
|model_path |const char \* |The path of the model file. |
|fps |int |The frame span for detection. One detection every fps frame(s). |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more information, refer to bef_effect_ai_public_define.h.

<span id="2. Detect light"></span>
## 2. Detect light

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_lightcls_detect(
        bef_effect_handle_t handle,
        const unsigned char *image,
        bef_ai_pixel_format pixel_format,
        int image_width,
        int image_height,
        int image_stride,
        bef_ai_rotate_type orientation,
        bef_ai_light_cls_result *result
);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |Light detection handle. |
|image |const unsigned char \* |Model type, currently divided into big and small models. |
|pixel_format |bef_ai_pixel_format |The path of the model file. |
|image_width |int |Image width. |
|image_height |int |Image height. |
|image_stride |int |Image stride. |
|orientation |bef_ai_rotate_type |Image rotation orientation. |
|result |bef_ai_light_cls_result |Detection result. Refer to bef_effect_ai_lightcls.h for more information. |


**Notes:** 

```C++
typedef struct bef_ai_light_cls_result_st { int selected_index; // light type 0～6, respectively indoor warm white, indoor cool white, indoor low-light, sunny, cloudy, night and backlight float prob; // certainty 0～1 } bef_ai_light_cls_result;
```


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more information, refer to bef_effect_ai_public_define.h.

<span id="3. Release the handle"></span>
## 3. Release the handle

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_lightcls_release(
        bef_effect_handle_t handle
);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |Light detection handle. |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more information, refer to bef_effect_ai_public_define.h.

<span id="4. Light detection license"></span>
## 4. Light detection license

```C
// android
BEF_SDK_API bef_effect_result_t
bef_effect_ai_lightcls_check_license(
        JNIEnv* env,
        jobject context,
        bef_effect_handle_t handle,
        const char *licensePath
        );
// ios
BEF_SDK_API bef_effect_result_t
bef_effect_ai_lightcls_check_license(
        bef_effect_handle_t handle,
        const char *licensePath
        );
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |Light detection handle. |
|licensePath |const char \* |The string of license file. |
|context |jobject |Context in Android. |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more information, refer to bef_effect_ai_public_define.h.

<span id="Java Interface Description"></span>
# Java Interface Description

**Interface description**

For a detailed interface description, refer to com.bytedance.labcv.effectsdk.LightClsDetect

<span id="1. Initialize the light detection handle"></span>
## 1. Initialize the light detection handle

```Java
public int init(
    Context context,
    String modelPath,
    String license,
    int fps)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|context |Context |Applying context. |
|modelpath |String |The absolute path of the model file. |
|license |String |The absolute path of the license file. |
|fps |int |The frame span for detection. One detection every fps frame(s). |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail.

<span id="2. Detect light"></span>
## 2. Detect light

```Java
public BefLightclsInfo detectLightCls(
        ByteBuffer buffer,
        BytedEffectConstants.PixlFormat pixlFormat,
        int imageWidth,
        int imageHeight,
        int imageStride,
        BytedEffectConstants.Rotation orientation)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|buffer |ByteBuffer |Parameter type. |
|pixlFormat |BytedEffectConstants.PixlFormat |Parameter value. |
|imageWidth |int |Image width. |
|imageHeight |int |Image height. |
|imageStride |int |Image stride. |
|orientation |BytedEffectConstants.Rotation |Image rotation orientation. |


**Notes:** 

BytedEffectConstants.PixlFormat:

```Java
public enum PixlFormat {
    RGBA8888(0),
    BGRA8888(1),
    BGR888(2),
    RGB888(3),
    BEF_AI_PIX_FMT_YUV420P(5),
    BEF_AI_PIX_FMT_NV12(6),
    BEF_AI_PIX_FMT_NV21(7);
    private int value;
    PixlFormat(int value) {
        this.value = value;
    }
    public int getValue() {
        return value;
    }
}
```


BytedEffectConstants.Rotation:

```Java
public enum Rotation { /** * The image does not need to be rotated. The face in the image is positive */ CLOCKWISE_ROTATE_0(0), /** * The image needs to be rotated 90 degrees clockwise so that the face in the image is positive */ CLOCKWISE_ROTATE_90(1), /** * The image needs to be rotated 180 degrees clockwise so that the face in the image is positive */ CLOCKWISE_ROTATE_180(2), /** * The image needs to be rotated 270 degrees clockwise so that the face in the image is positive */ CLOCKWISE_ROTATE_270(3); public int id = 0; Rotation(int id) { this.id = id; } }
```


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail.

<span id="3. Release the handle"></span>
## 3. Release the handle

```Java
public void release()
```


<span id="FAQ"></span>
## FAQ

<span id="Error code"></span>
## Error code

Refer to the [error code list](https://docs.byteplus.com/99783)
