---
title: "Video Classification"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-video-classification"
---

The Video Classification SDK provides the capability of real\-time classification of video contents in 88 types.

<span id="C Interface Description"></span>
# C Interface Description

For detailed interface description, view header file: bef_effect_ai_video_cls.h

<span id="1. Create A Video Classification Handle"></span>
## 1. Create A Video Classification Handle

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_video_cls_load_model(bef_effect_handle_t handle,
                                   bef_ai_video_cls_model_type type,
                                   const char * strModelPath);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The video classification handle created. |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more information, refer to bef_effect_ai_public_define.h.

<span id="2. Load a model"></span>
## 2. Load a model

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_video_cls_load_model(bef_effect_handle_t handle,
                                   bef_ai_video_cls_model_type type,
                                   const char * strModelPath);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The video classification handle created. |
|type |bef_ai_video_cls_model_type |Model type enumeration. |
|strModelPath |const char \* |Model path. |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more information, refer to bef_effect_ai_public_define.h.

<span id="2. Video Classification"></span>
## 3. Video Classification

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_video_cls_detect(
                             bef_effect_handle_t handle,
                             const unsigned char *image,
                             bef_ai_pixel_format pixel_format,
                             int image_width,
                             int image_height,
                             int image_stride,
                             bef_ai_rotate_type orientation,
                             bool islast,
                             bef_video_cls_ret *video_cls_info
                             );
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |Video classification handle. |
|image |const unsigned char \* |Model type, currently divided into big and small models. |
|pixel_format |bef_ai_pixel_format |The path of the model file. |
|image_width |int |Image width. |
|image_height |int |Image height. |
|image_stride |int |Image stride. |
|orientation |bef_ai_rotate_type |Image rotation orientation. |
|islast |bool |Whether it is the last frame (set "true" every 5 frames). |
|result |Bef _ video _ cls _ rate |The classification result. For more information, refer to bef_video_cls_ret. |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more information, refer to bef_effect_ai_public_define.h.

<span id="3. Release the handle"></span>
## 4. Release the handle

```C
BEF_SDK_API void
bef_effect_ai_video_cls_destroy(
                              bef_effect_handle_t handle
                              );
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |Video classification handle |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more information, refer to bef_effect_ai_public_define.h.

<span id="4. Video Classification License"></span>
## 5. Video Classification License

```C
// android
BEF_SDK_API bef_effect_result_t
bef_effect_ai_video_cls_check_license(
        JNIEnv* env,
        jobject context,
        bef_effect_handle_t handle,
        const char *licensePath
        );
// ios
BEF_SDK_API bef_effect_result_t
bef_effect_ai_video_cls_check_license(
        bef_effect_handle_t handle,
        const char *licensePath
        );
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |Video classification handle. |
|licensePath |const char \* |The string of license file. |
|context |jobject |The corresponding Context in Android. |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more information, refer to bef_effect_ai_public_define.h.

<span id="Java interface description"></span>
# Java interface description

**Interface Description**

For a detailed interface description, refer to com.bytedance.labcv.effectsdk.VideoClassifier

<span id="1. Initialize a Video Classification Handle"></span>
## 1. Initialize a Video Classification Handle

```Java
public int createHandle(
    Context context, String licensePath)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|context |Context |Applying context. |
|license |String |License file path |


**Return value:** 

BEF_RESULT_SUC successfully returned, otherwise the corresponding error code will be returned.

<span id="2. Video classification"></span>
## 2. Video classification

```Java
public BefVideoClsInfo videoClsDetect(
        ByteBuffer buffer,
        BytedEffectConstants.PixlFormat pixlFormat,
        int imageWidth,
        int imageHeight,
        int imageStride,
        BytedEffectConstants.Rotation orientation
        boolean  isLast)
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
|bool |isLast |Whether it is the last frame (set "true" every 5 frames). |


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

Refer to the [error code list](https://docs.byteplus.com/99783).
