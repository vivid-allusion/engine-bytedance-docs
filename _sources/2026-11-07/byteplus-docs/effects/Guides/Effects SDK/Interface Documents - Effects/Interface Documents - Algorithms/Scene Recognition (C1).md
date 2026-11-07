---
title: "Scene Recognition (C1)"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-scene-recognition-c1"
---

The C1 Scene Classification SDK provides the capability of real\-time classification of video contents in 22 types of scenes.

<span id="C Interface Description"></span>
# C Interface Description

For detailed interface description, view header file: bef_effect_ai_c1

<span id="1. Create a scene classification handle"></span>
## 1. Create a scene classification handle

```C
BEF_SDK_API
bef_effect_result_t bef_effect_ai_c1_create(bef_ai_c1_handle *handle, bef_ai_c1_model_type modelType, const char *modelPath)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_ai_c1_handle |The created scene classification handle. |
|modelType |bef_ai_c1_model_type |Model type |
|modelPath |const char \* |Model path. |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more information, refer to bef_effect_ai_public_define.h.

<span id="2. Set parameters"></span>
## 2. Set parameters

```C
BEF_SDK_API
bef_effect_result_t bef_effect_ai_c1_set_param(bef_ai_c1_handle handle, bef_ai_c1_param_type type, float value);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_ai_c1_handle |The created scene classification handle. |
|type |bef_ai_c1_param_type |Parameter type. |
|value |float |Parameter value. |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more information, refer to bef_effect_ai_public_define.h.

<span id="3. Classify scenes"></span>
## 3. Classify scenes

```C
BEF_SDK_API
bef_effect_result_t bef_effect_ai_c1_detect(bef_ai_c1_handle handle,
                                            const unsigned char *image,
                                            bef_ai_pixel_format pixelFormat,
                                            int imageWidth,
                                            int imageHeight,
                                            int imageStride,
                                            bef_ai_rotate_type rotation,
                                            bef_ai_c1_output *result);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_ai_c1_handle |Scene classification handle. |
|image |const unsigned char \* |Model type, currently divided into big and small models. |
|pixelFormat |bef_ai_pixel_format |The path of the model file. |
|imageWidth |int |Image width. |
|imageHeight |int |Image height. |
|imageStride |int |Image stride. |
|orientation |bef_ai_rotate_type |Image rotation orientation. |
|result |bef_ai_c1_output |Classification result. Refer to bef_ai_c1_output for more information. |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more information, refer to bef_effect_ai_public_define.h.

<span id="4. Release the handle"></span>
## 4. Release the handle

```C
BEF_SDK_API
bef_effect_result_t bef_effect_ai_c1_release(bef_ai_c1_handle handle);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_ai_c1_handle |Scene classification handle. |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more information, refer to bef_effect_ai_public_define.h.

<span id="5. Light detection license"></span>
## 5. Light detection license

```C
BEF_SDK_API
bef_effect_result_t bef_effect_ai_c1_check_license(bef_ai_c1_handle handle, const char *licensePath);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_ai_c1_handle |Scene classification handle. |
|licensePath |const char \* |The string of license file. |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more details, refer to bef_effect_ai_public_define.h.

<span id="Java Interface Description"></span>
# Java Interface Description

**Interface description**

For a detailed interface description, refer to com.bytedance.labcv.effectsdk.C1Detect

<span id="1. Initialize a scene classification handle"></span>
## 1. Initialize a scene classification handle

```Java
public int init(BytedEffectConstants.C1ModelType modelType, 
                String modelPath, 
                String licensePath)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|modelType |BytedEffectConstants.C1ModelType |Model type. |
|modelPath |String |Model path. |
|licensePath |String |License file path. |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail.

<span id="2. Classify scenes"></span>
## 2. Classify scenes

```Java
public BefC1Info detect(ByteBuffer buffer,
                        BytedEffectConstants.PixlFormat pixelFormat, 
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
|imageStride |int |Image stride |
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

<span id="3. Set parameters"></span>
## 3. Set parameters

```Java
public int setParam(BytedEffectConstants.C1ParamType paramType, float value)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|paramType |BytedEffectConstants.C1ParamType |Parameter type. |
|value |float |Parameter value. |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail.

<span id="4. Release the handle"></span>
## 4. Release the handle

```Java
public void release()
```


<span id="FAQ"></span>
## FAQ

<span id="Error code"></span>
## Error code

Refer to the [error code list](https://docs.byteplus.com/99783).
