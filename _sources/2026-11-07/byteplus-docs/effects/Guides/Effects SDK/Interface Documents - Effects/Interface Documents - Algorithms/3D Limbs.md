---
title: "3D Limbs"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-3d-limbs"
---

3D body keypoint algorithm can drive the virtual character, etc., in short video/shooting scenes can achieve relatively novel effects.

V4.4.3 adds a new algorithm.

<span id="128495b8"></span>
# Technical specifications


|**Category** |**Supported Formats** |
|---|---|
|Platforms |* Android<br><br>* iOS |
|Input formats |* RGBA8888<br><br>* BGRA8888<br><br>* RGB888<br><br>* BGR888 |
|Memory footprint |< 23M (test device OPPO R11) |
|Detection speed |< 37 ms (test device OPPO R11) |


<span id="3D Skeleton Keypoints description"></span>
# 3D Skeleton Keypoints description

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/1ebd34d-3D.png) </span>


* For each image frame, the SDK outputs a 3+24x4 dimensional vector.

* The first 3 dimensions represent the displacement of the virtual image. The coordinate system is X\-\>right, Y\-\>up, Z\-\>back,

* The last 24x4 dimensions represent the 24 joint rotation quaternions in the coordinate system X\-\>left, Y\-\>up, Z\-\>front.


<span id="aca4ef1b"></span>
# C Interface Description

For the detailed interface description, refer to header file: bef_effect_ai_3d_skeleton

<span id="a2a6e6b4"></span>
## 1. Create 3D limbs handle

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_3d_skeleton_create(bef_ai_3d_skeleton_handle *handle);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|Handle |bef_ai_3d_skeleton_handle \* |Created 3d limbs algorithm handle. |


**Return value:** 

Success returns BEF_RESULT_SUC, while failure returns the corresponding error code. For more information, refer to bef_effect_ai_public_define

<span id="d381615c"></span>
## 2. Load the 3D limbs algorithm model

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_3d_skeleton_load_model(bef_ai_3d_skeleton_handle handle, const char* modelPath);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_ai_3d_skeleton_handle |3d limbs algorithm handle. |
|modelPath |const char \* |3D limbs algorithm model path. |


**Return value:** 

Success returns BEF_RESULT_SUC, while failure returns the corresponding error code. For more information, refer to bef_effect_ai_public_define

<span id="67e10982"></span>
## 3. Set 3D limbs algorithm parameters

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_3d_skeleton_set_param(bef_ai_3d_skeleton_handle handle, bef_ai_3d_skeleton_param_type type, float value);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_ai_3d_skeleton_handle |3D limbs algorithm handle. |
|Type |bef_ai_3d_skeleton_param_type |3D limbs algorithm parameter type. |
|value |float |3D limbs algorithm parameter value. |


**Return value:** 

Success returns BEF_RESULT_SUC, while failure returns the corresponding error code. For more information, refer to bef_effect_ai_public_define

<span id="333e42b0"></span>
## 4. 3D limbs algorithm detection

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_3d_skeleton_detect(bef_ai_3d_skeleton_handle handle, bef_ai_skeleton_3d_args* args, bef_ai_skeleton3d_ret* ret);

typedef struct bef_ai_skeleton_3d_args{
    const unsigned char *image;
    bef_ai_pixel_format pixel_format;
    int image_width;
    int image_height;
    int image_stride;
    bef_ai_rotate_type rotation;
    float points2d[AI_3D_SKELETON_MAX_TARGET_NUM*AI_3D_SKELETON_INPUT_KEYPOINT2D_NUM*2]; // 2D skeleton keypoints position
    int point_valid[AI_3D_SKELETON_MAX_TARGET_NUM*AI_3D_SKELETON_INPUT_KEYPOINT2D_NUM]; // 2D skeleton keypoints is valid or not
    int keypoint_num; // Number of 2D skeleton keypoints
    int target_num; // Number of targets
}bef_ai_skeleton_3d_args;

typedef struct bef_ai_skeleton3d_ret {
    bef_ai_skeleton3d_target targets[AI_3D_SKELETON_MAX_TARGET_NUM]; // list of targets
    int target_num; // Number of targets
    float focal_length; // Camera focal length
    int tracking; // Whether the next frame is in tracking mode or detect mode, in detect mode, you need to input the 2D key point coordinates of the human body to get the bbox of the human body, in tracking mode, the bbox of the human body is calculated from the 3D key point results of the previous frame
}bef_ai_skeleton3d_ret;
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_ai_3d_skeleton_handle |3D limbs algorithm handle. |
|Args |bef_ai_skeleton_3d_args \* |Algorithm input parameter. |
|RET |bef_ai_skeleton3d_ret \* |Algorithm return value. |


**Return value:** 

Success returns BEF_RESULT_SUC, while failure returns the corresponding error code. For more information, refer to bef_effect_ai_public_define

<span id="70c9dde9"></span>
## 5. 3D limbs algorithm authorization

```C
BEF_SDK_API bef_effect_result_t bef_effect_ai_3d_skeleton_check_license(bef_ai_3d_skeleton_handle handle, const char *licensePath);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_ai_3d_skeleton_handle |3D limbs algorithm handle. |
|licensePath |const char \* |License file path. |


**Return value:** 

Success returns BEF_RESULT_SUC, while failure returns the corresponding error code. For more information, refer to bef_effect_ai_public_define

<span id="86d73de9"></span>
## 6. 3D limbs algorithm release handle

```C
BEF_SDK_API void
bef_effect_ai_3d_skeleton_release(bef_ai_3d_skeleton_handle handle);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_ai_3d_skeleton_handle |3D limbs algorithm handle. |


**Return value:** 

Success returns BEF_RESULT_SUC, while failure returns the corresponding error code. For more information, refer to bef_effect_ai_public_define

<span id="Java Interface Description"></span>
# Java Interface Description

For the detailed interface description, refer to the file: com.effectar.labcv.effectsdk.Skeleton3dDetect.java

<span id="69f81437"></span>
## 1. Initialize 3D limbs handle

```Java
public int init(Context context, String licensePath, boolean onlineLicense,  String modelPath);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|context |Context |Android context. |
|licensePath |String |License file path. |
|onlineLicense |boolean |Configure online or offline licensing. |
|modelPath |String |Avatar 3D algorithm model path. |


**Return value:** 

Successfully returns BEF_RESULT_SUC, otherwise returns the corresponding error code.

<span id="400d0d44"></span>
## 2. 3D limbs algorithm parameter settings

```Java
public int setParam(int type, float value);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|type |int |Parameter setting type. |
|value |float |Parameter setting value. |


**Return value:** 

Successfully returns BEF_RESULT_SUC, otherwise returns the corresponding error code.

<span id="280f1066"></span>
## 3. 3D limbs algorithm processing

```Java
public int detectSkeleton3d(InputParam param);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|Param |InputParam |Algorithm input parameters. |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">InputParam can refer to com.effectar.labcv.effectsdk.Skeleton3dDetect.java, and its definition is consistent with the C interface bef_effect_ai_3d_skeleton.</div>


**Return value:** 

Successfully returns BEF_RESULT_SUC, otherwise returns the corresponding error code.

<span id="eb646735"></span>
## 4. Release 3D limbs algorithm handle

```Java
public void release()
```


<span id="6055306d"></span>
# FAQ

<span id="e3096664"></span>
## 1. If there is any exception, check if there are any of the following types of logs

A: It is recommended to first check the log of the following tag output Error type:


* bef_effect_ai

* SMASH_E_LOG

* EffectSDK
