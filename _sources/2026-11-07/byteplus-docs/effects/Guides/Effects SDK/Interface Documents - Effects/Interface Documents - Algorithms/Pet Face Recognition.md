---
title: "Pet Face Recognition"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-pet-face-recognition"
---

The pet face recognition SDK is equipped with pet classification, pet face landmarks tracking and pet face motion analysis capabilities, featuring fast detection speed, stable tracking, low\-consuming performance, and so on.

<span id="Cat face 82 landmarks index chart"></span>
## Cat face 82 landmarks index chart

<span>![图片](https://p-vcloud.byteimg.com/img/tos-cn-i-0000/740cb42ac8ac459e9069a40a74c08fb2~tplv-noop.jpeg?width=790&height=702) </span>

<span id="Dogface 90 landmarks index chart"></span>
## Dog face 90 landmarks index chart

<span>![图片](https://p-vcloud.byteimg.com/img/tos-cn-i-0000/2fb62efedb534f239bbdb30dd0657141~tplv-noop.png?width=1200&height=1250) </span>

<span id="Dogface 76 landmarks index chart"></span>
## Dog face 76 landmarks index chart

14 landmarks [26\-39] for the ear part are removed from the original 90 landmarks, with other landmarks after NO.40 being postphoned.

<span id="Technical specifications"></span>
# Technical specifications


|**Category** |**Supported Formats** |
|---|---|
|Platforms |* Android<br><br>* iOS<br><br>* Windows<br><br>* Mac |
|Angles |* yaw ≤ ±90°<br><br>* pitch ≤ ±90° |
|Input formats |* RGBA8888<br><br>* BGRA8888<br><br>* BGR888<br><br>* RGB888<br><br>* NV21<br><br>* NV12<br><br>* YUV420P |
|Maximum number of pet faces |10 |
|Minimum input size |Short side 128 |
|Available distance |Face accounts for more than 1/10 of the short side of the picture |
|Detected speed |< 8ms (test devices: OPPO R11, Qualcomm 660) |


<span id="ac9e4db3"></span>
# C Interface description

For the detailed interface description, refer to header file: bef_effect_ai_pet_face.h

**Interface description**

<span id="1. Create a pet face detection handle"></span>
## 1. Create a pet face detection handle

Create a handle for pet face detection.

```C
BEF_SDK_API
bef_effect_result_t
bef_effect_ai_pet_face_create(
    const char * strModelPath,
    long long config,
    unsigned int maxNum,
    bef_effect_handle_t *handle
);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|strModelPath |const char \* |Model path. |
|config |long long config, |The configuration of the pet face detection algorithm. This can be configured to detect cats only, dogs only, or both cats and dogs. |
|max_face_num |unsigned int |The maximum number of pet faces that can be detected. |
|handle |bef_effect_handle_t |Pet face detection handle created. |


**Notes:** 

You can refer to bef_ai_pet_face_config_type for parameters configuration:

Dogs only

```C
detect_config = bef_ai_pet_face_config_type::BEF_DetDog
```


Both cats and dogs

```C
detect_config = bef_ai_pet_face_config_type::BEF_DetDog|bef_ai_pet_face_config_type::BEF_DetCat
```


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more details, refer to bef_effect_ai_public_define.h.

<span id="2. Authorize pet face detection"></span>
## 2. Authorize pet face detection

**Android interface:** 

```C
BEF_SDK_API bef_effect_result_t bef_effect_ai_pet_face_check_license(
        JNIEnv* env,
    jobject context, 
    bef_effect_handle_t handle, 
    const char *license_path
);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|env |JNIEnv \* |JNI environment. |
|context |jobject |JNI object. |
|handle |bef_effect_handle_t |Pet face detection handle created. |
|license_path |const char \* |License file path. |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more details, refer to bef_effect_ai_public_define.h.

**iOS interface:** 

```C
BEF_SDK_API bef_effect_result_t bef_effect_ai_pet_face_check_license(
        bef_effect_handle_t handle,
    const char *license_path
);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |Pet face detection handle created. |
|license_path |const char \* |License file path. |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more details, refer to bef_effect_ai_public_define.h.

<span id="3. Detect the landmarks of pet faces"></span>
## 3. Detect the landmarks of pet faces

```C
BEF_SDK_API
bef_effect_result_t bef_effect_ai_pet_face_detect(
    bef_effect_handle_t handle,
    const unsigned char *image,
    bef_ai_pixel_format pixel_format,
    int image_width,
    int image_height,
    int image_stride,
    bef_ai_rotate_type orientation,
    bef_ai_pet_face_result *p_pet_face_result
);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |Pet face detection handle created. |
|image |const unsigned char \* |Data pointer of input images. |
|pixel_format |bef_ai_pixel_format |Format of input images. |
|image_width |int |Width of input images in pixels. |
|image_height |int |Height of input images in pixels. |
|image_stride |int |Image stride in each row of input images in pixels. |
|orientation |bef_ai_rotate_type |Steering directions of input images. Refer to the bef_rotate_type in bef_effect_ai_public_define.h for more details. |
|p_pet_face_result |bef_ai_pet_face_result \* |To store the result information, you need to allocate good memory externally, and you need to ensure that the space is greater than or equal to the set maximum number of detected pet faces. |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more details, refer to bef_effect_ai_public_define.h.

<span id="4. Delete pet face detection handle"></span>
## 4. Delete pet face detection handle

```C
BEF_SDK_API
bef_effect_result_t bef_effect_ai_pet_face_release(bef_effect_handle_t handle);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |Pet face detection handle created. |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more details, refer to bef_effect_ai_public_define.h.

<span id="Java interface description"></span>
# Java interface description

**Interface description**

The definition of function related to the detection of pet face landmarks is in com.bytedance.labcv.effectsdk. PetFaceD etect.java.

<span id="1. Initialize the pet face detection handle"></span>
## 1. Initialize the pet face detection handle

```Java
public int init(
        Context context, 
    String modelPath, 
    int config, 
    String license
)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|context |Context |Context. |
|modelPath |String |Model path. |
|config |int |Configuration of pet face detection algorithm, config = detectable feature (required. Refer to {@link BytedEffectConstants. PetFaceAction}). |
|license |String |License file. |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail.

<span id="2. Detect the landmarks of pet faces"></span>
## 2. Detect the landmarks of pet faces

```Java
public BefPetFaceInfo detectFace(
    ByteBuffer buffer, 
    BytedEffectConstants.PixlFormat pixel_format, 
    int image_width, 
    int image_height, 
    int image_stride, 
    BytedEffectConstants.Rotation orientation
)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|buffer |ByteBuffer |Image data. |
|pixel_format |BytedEffectConstants.PixlFormat |Format. |
|image_width |int |Width. |
|image_height |int |Height. |
|image_stride |int |Image stride in each row for images. |
|orientation |BytedEffectConstants.Rotation |Image rotation angle. |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail.

<span id="3. Delete pet face detection handle"></span>
## 3. Delete pet face detection handle

```Java
public void release()
```


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail.

<span id="FAQ"></span>
## FAQ

<span id="1. If there are any exceptions, please check whether there are the following types of logs"></span>
### 1. If there are any exceptions, check whether there are the following types of logs

Answer: Check logs with following tags:


* **bef_effect_ai**

* **SMASH_E_LOG**

* **EffectSDK**


<span id="Error code"></span>
## Error code

Refer to [the error code table](https://docs.byteplus.com/99783).
