---
title: "Face Detection and Analysis"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-portrait-sdk"
---

The face detection and analysis SDK can detect keypoints of the face and analyze face attributes, featuring fast detection speed, stable tracking, and low\-performance cost.

<span id="106 Keypoints of the Face"></span>
## 106 Keypoints of the Face

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/2ffaded-1.png) </span>

<span id="280 Keypoints of the Face"></span>
## 280 Keypoints of the Face

More keypoints of the lips, irises, and eyebrows are added to the 106 keypoints.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/5d09b06-2.png) </span>

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/9f0c4d0-3.png) </span>

<span id="Technical Specifications"></span>
# Technical Specifications


|**Category** |**Supported Formats** |
|---|---|
|Platforms |* Android<br><br>* iOS<br><br>* Windows<br><br>* macOS |
|Angles |* Yaw ≤ ±90°<br><br>* pitch ≤ ±90° |
|Input format |* RGBA8888<br><br>* BGRA8888<br><br>* BGR888<br><br>* RGB888<br><br>* NV21<br><br>* NV12<br><br>* YUV420p |
|Memory usage |< 4 MB (on OPPO R11). |
|Faces Number |≤ 10. |
|Face\-to\-screen ratio |A face shall account for more than 1/10 of the short side of the image. |
|Input size |Short side: ≥ 128. |
|Face detection speed |< 2 ms (on iPhone 7) |


<span id="C APIs"></span>
# C APIs

<span id="106/240/280 Face Keypoints Detection"></span>
## 106/240/280 Face Keypoints Detection

For details about the APIs, refer to the header file: bef_effect_ai_face_detect.h.

<span id="Call Example"></span>
### Call Example


1. Initialization:


```C
NSString *faceModel = [resourceBundleName stringByAppendingString:@"/ttfacemodel/tt_face_v5.0.model"];

NSString *faceExtraModel = [resourceBundleName stringByAppendingString:@"/ttfacemodel/tt_face_extra_v8.0.model"];

// Face detection initialization. Input the path of the algorithm model file.
// BEF_DETECT_FULL is used. As a result, the blinking and pouting detection modules will be loaded.
result = bef_effect_ai_face_detect_create(BEF_DETECT_SMALL_MODEL | BEF_DETECT_FULL, faceModel.UTF8String, &amp;faceDetectHandle);

// Check the face detection license.
result = bef_effect_ai_face_check_license(faceDetectHandle, FACE106_LICENSE.UTF8String, FACE106_LICENSE.length);

// Set call parameters.
result = bef_effect_ai_face_detect_setparam(faceDetectHandle, BEF_FACE_PARAM_FACE_DETECT_INTERVAL, 15);


result = bef_effect_ai_face_detect_setparam(faceDetectHandle, BEF_FACE_PARAM_MAX_FACE_NUM, 2);

result = bef_effect_ai_face_detect_add_extra_model(faceDetectHandle,TT_MOBILE_FACE_280_DETECT, faceExtraModel.UTF8String
);
```



2. Face detection:


```C
bef_ai_face_info faceInfo;
// Blinking and pouting detection is not configured. In order to detect blinking and pouting, use the following:
// BEF_DETECT_MODE_VIDEO | BEF_FACE_DETECT | BEF_EYE_BLINK | BEF_MOUTH_POUT|BEF_DETECT_EYEBALL | BEF_BROW_JUMP

bef_effect_result_t ret = bef_effect_ai_face_detect(faceDetectHandle, buffer,
                                                        BEF_AI_PIX_FMT_BGRA8888,
                                                         width, height,
                                                         bytesPerRow,
                                                         [self getDeviceOrientation],
                                                         BEF_DETECT_MODE_VIDEO | BEF_FACE_DETECT,
                                                         &amp;faceInfo);
```



3. Destroying the handle:


```C
 bef_effect_ai_face_detect_destroy(faceDetectHandle);
```


**API Description**

<span id="1. Creating a 106 Face Keypoints Detection Handle"></span>
### 1. Creating a 106 Face Keypoints Detection Handle

```C
BEF_SDK_API bef_effect_result_t bef_effect_ai_face_detect_create(
    unsigned long long config,
     const char * strModelPath,
     bef_effect_handle_t *handle
);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|config |long long |Configuration of the face detection algorithm. |
|strModelPath |const char \* |Path of the model file. |
|handle |bef_effect_handle_t |Face detection handle created. |


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned. For details, refer to bef_effect_ai_public_define.h.

**Remarks**

The following face detection algorithm options are available.

● Model type

This option is required. Currently, only the small model type is supported.


|**Symbol** |**Value** |**Description** |
|---|---|---|
|BEF_DETECT_SMALL_MODEL |0x00200000 |Faster detection algorithm. |


● Detection mode setting

Face detection includes video detection and image detection. For image detection, there are normal and advanced modes, where the advanced mode can detect smaller faces but has a slower detection speed. The following table describes four detection modes. If you do not set this option, BEF_DETECT_MODE_VIDEO will be used by default.


|**Symbol** |**Value** |**Description** |
|---|---|---|
|BEF_DETECT_MODE_VIDEO |0x00020000 |Video detection. |
|BEF_DETECT_MODE_IMAGE |0x00040000 |Image detection. |
|BEF_DETECT_MODE_IMAGE_SLOW |0x00080000 |Slow image detection mode, which can detect smaller faces. |
|BEF_DETECT_MODE_VIDEO_SLOW |0x00010000 |Slow video detection mode, which can detect smaller faces. |


● Facial actions to be detected

The following table describes the facial actions that can be detected.


|**Symbol** |**Value** |**Description** |
|---|---|---|
|BEF_FACE_DETECT |0x00000001 |106 face keypoints detection. |
|BEF_EYE_BLINK |0x00000002 |Eye blinking. |
|BEF_MOUTH_AH |0x00000004 |Mouth opening. |
|BEF_HEAD_YAW |0x00000008 |Head shaking. |
|BEF_HEAD_PITCH |0x00000010 |Nodding. |
|BEF_BROW_JUMP |0x00000020 |Eyebrow wiggles. |
|BEF_MOUTH_POUT |0x00000040 |Lips pouting. |
|BEF_DETECT_FULL |0x0000007F |All of the above. |
|When creating the face detection handle, set config to the model type (required) |detection mode (default value: BEF_DETECT_MODE_VIDEO) |facial actions to be detected (required). |


<span id="2. Checking the Face Detection License"></span>
### 2. Checking the Face Detection License

**API for Android**

```C
BEF_SDK_API bef_effect_result_t bef_effect_ai_face_attribute_check_license(
    JNIEnv* env,
    jobject context,
    bef_effect_handle_t handle,
    const char *license_path
);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|env |JNIEnv \* |Java Native Interface (JNI). |
|context |jobject |JNI object. |
|handle |bef_effect_handle_t |Face detection handle created. |
|license_path |const char \* |Path of the license file. |


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned. For details, refer to bef_effect_ai_public_define.h.

**API for iOS**

```C
BEF_SDK_API bef_effect_result_t bef_effect_ai_face_attribute_check_license(
    bef_effect_handle_t handle,
    const char *license_path
);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |Face detection handle created. |
|license_path |const char \* |Path of the license file. |


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned. For details, refer to bef_effect_ai_public_define.h.

<span id="3. Configuring the 240/280 Face Keypoints Detection Model"></span>
### 3. Configuring the 240/280 Face Keypoints Detection Model

```C
BEF_SDK_API bef_effect_result_t bef_effect_ai_face_detect_add_extra_model(
    bef_effect_handle_t handle,
    unsigned long long config,
    const char *param_path
);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |Face detection handle created. |
|config |unsigned long long |Parameters of the 240/280 face keypoints detection model. |
|param_path |const char \* |Path of the model file. |


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned. For details, refer to bef_effect_ai_public_define.h.

**Remarks**

This step uses the 106 face keypoints detection handle created in step 1, and the number of keypoints is increased to 240 or 280.

config can be set to:

```C
  // Config-240, TT_MOBILE_FACE_240_DETECT
  // Config-280, TT_MOBILE_FACE_280_DETECT
  // Config-240 fast mode, TT_MOBILE_FACE_240_DETECT | TT_MOBILE_FACE_240_DETECT_FASTMODE
  // Config-280 fast mode, TT_MOBILE_FACE_280_DETECT | TT_MOBILE_FACE_240_DETECT_FASTMODE
```


<span id="4. Setting Parameters for Face Detection"></span>
### 4. Setting Parameters for Face Detection

```C
BEF_SDK_API bef_effect_result_t bef_effect_ai_face_detect_setparam(
    bef_effect_handle_t handle,
    bef_face_detect_type type,
    float value
);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |Face detection handle created. |
|type |bef_face_detect_type |Required face detection type. For details, refer to bef_face_detect_type. |
|value |float |Specific value. |


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned. For details, refer to bef_effect_ai_public_define.h.

<span id="5. Detecting Face Keypoints"></span>
### 5. Detecting Face Keypoints

The face keypoints detection results are defined in bef_effect_ai_face_detect.h.

```C
// Results of detection of keypoints of the eyes, eyebrows, lips, and irises, by the 280 keypoints detection model:
typedef struct bef_ai_face_ext_info_t {
   int eye_count;                  // Number of eyes detected.
   int eyebrow_count;              // Number of eyebrows detected.
   int lips_count;                 // Number of lips detected.
   int iris_count;                 // Number of irises detected.

   bef_ai_fpoint eye_left[22];        // Keypoints of the left eye.
   bef_ai_fpoint eye_right[22];       // Keypoints of the right eye.
   bef_ai_fpoint eyebrow_left[13];    // Keypoints of the left eyebrow.
   bef_ai_fpoint eyebrow_right[13];   // Keypoints of the right eyebrow.
   bef_ai_fpoint lips[64];            // Keypoints of lips.
   bef_ai_fpoint left_iris[20];       // Keypoints of the left iris.
   bef_ai_fpoint right_iris[20];      // Keypoints of the right iris.
} bef_ai_face_ext_info;


// For 106 keypoints detection:
typedef struct bef_ai_face_106_st {
   bef_ai_rect rect;                // Rectangular face area.
   float score;                  // Confidence.
   bef_ai_fpoint points_array[106]; // Array of keypoints.
   float yaw;                    // Yaw angle (positive right and negative left).
   float pitch;                  // Pitch angle (positive down and negative up).
   float roll;                   // Roll angle (positive right and negative left).
   float eye_dist;               // Distance between the eyes.
   int ID;                       // Face ID, which is unique for each detected face. If a face is lost and detected again, it will have a new face ID.
   unsigned int action;          // Action, which is defined in bef_ai_effect_face_detect.h.
   unsigned int tracking_cnt;
} bef_ai_face_106, *p_bef_ai_face_106;


// @brief detection results:
typedef struct bef_ai_face_info_st {
   bef_ai_face_106 base_infos[BEF_MAX_FACE_NUM];          // Face information detected.
   bef_ai_face_ext_info extra_infos[BEF_MAX_FACE_NUM];    // Extra information about the eyes, eyebrows, lips, and other keypoints.
   int face_count;                                     // Number of faces detected.
} bef_ai_face_info, *p_bef_ai_face_info;
```


Call the following API to detect face keypoints.

```C
BEF_SDK_API bef_effect_result_t bef_effect_ai_face_detect(
    bef_effect_handle_t handle,
    const unsigned char *image,
    bef_ai_pixel_format pixel_format,
    int image_width,
    int image_height,
    int image_stride,
    bef_ai_rotate_type orientation,
    unsigned long long detect_config,
    bef_ai_face_info *p_face_info
);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |Face detection handle created. |
|image |const unsigned char \* |Data pointer of the input image. |
|pixel_format |bef_ai_pixel_format |Format of the input image. |
|image_width |int |Width of the input image, in pixels. |
|image_height |int |Height of the input image, in pixels. |
|image_stride |int |Row stride of the input image, in pixels. |
|orientation |bef_ai_rotate_type |Rotation angle of the input image. For details, refer to bef_rotate_type in bef_effect_ai_public_define.h. |
|detect_config |unsigned long long |Configuration related to face detection, for example, BEF_FACE_DETECT |
|p_face_info |bef_ai_face_info \* |Face detection result. |


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned. For details, refer to bef_effect_ai_public_define.h.

<span id="6. Destroying the Face Detection Handle"></span>
### 6. Destroying the Face Detection Handle

```C
BEF_SDK_API void bef_effect_ai_face_detect_destroy(
    bef_effect_handle_t handle
);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |Face detection handle created. |


<span id="Face Attribute Detection"></span>
## Face Attribute Detection

For details about the APIs, refer to the header file: bef_effect_ai_face_attribute.h.

<span id="1. Creating a Face Attribute Detection Handle"></span>
### 1. Creating a Face Attribute Detection Handle

```C
BEF_SDK_API bef_effect_result_t bef_effect_ai_face_attribute_create(
    unsigned long long config,
    const char * strModelPath,
    bef_effect_handle_t *handle
);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|config |unsigned long long |Configuration of the face attribute detection algorithm. |
|strModelPath |const char \* |Path of the model file. |
|handle |bef_effect_handle_t \* |Face attribute detection handle created. |


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned. For details, refer to bef_effect_ai_public_define.h.

<span id="2. Checking the Face Attribute Detection License"></span>
### 2. Checking the Face Attribute Detection License

**API for Android**

```C
BEF_SDK_API bef_effect_result_t bef_effect_ai_face_attribute_check_license(
    JNIEnv* env,
    jobject context,
    bef_effect_handle_t handle,
    const char *license_path
);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|env |JNIEnv \* |Java Native Interface (JNI). |
|context |jobject |JNI object. |
|handle |bef_effect_handle_t |Face detection handle created. |
|license_path |const char \* |Path of the license file. |


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned. For details, refer to bef_effect_ai_public_define.h.

**API for iOS**

```C
BEF_SDK_API bef_effect_result_t bef_effect_ai_face_attribute_check_license(
    bef_effect_handle_t handle,
    const char *license_path
);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |Face detection handle created. |
|license_path |const char \* |Path of the license file. |


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned. For details, refer to bef_effect_ai_public_define.h.

<span id="637813d1"></span>
### **3. Face Occlusion Detection**

4.8.1 New API

```C
BEF_SDK_API bef_effect_result_t bef_effect_ai_get_face_occlusion_info(bef_effect_handle_t handle, bef_ai_face_occlusion_info *p_occ_info);
```



|**Name** |**Parameter Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |Created face detection handle |
|p_occ_info |bef_ai_face_occlusion_info\* |Face occlusion result |


<span id="3. Setting Parameters for Face Attribute Detection"></span>
### 4. Setting Parameters for Face Attribute Detection

```C
BEF_SDK_API bef_effect_result_t bef_effect_ai_face_attribute_setparam(
    bef_effect_handle_t handle,
    bef_ai_face_attribute_param_config_type type,
    float value
);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |Face detection handle created. |
|type |bef_face_detect_type |Required face detection type. For details, refer to bef_face_detect_type. |
|value |float |Specific value. |


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned. For details, refer to bef_effect_ai_public_define.h.

<span id="4. Detecting Face Attributes"></span>
### 5. Detecting Face Attributes

The face attribute detection results are defined in the header file: bef_effect_ai_face_attribute.h.

```C
 BEF_FACE_ATTRIBUTE_AGE          = 0x00000001,     //Age.
 BEF_FACE_ATTRIBUTE_GENDER       = 0x00000002,     //Gender.
 BEF_FACE_ATTRIBUTE_EXPRESSION   = 0x00000004,     //Expression.
 BEF_FACE_ATTRIBUTE_ATTRACTIVE   = 0x00000008,     //Attractiveness.
 BEF_FACE_ATTRIBUTE_HAPPINESS    = 0x00000010,     //Level of happiness.
} bef_ai_face_attribute_types;

typedef enum {
 BEF_FACE_ATTRIBUTE_ForceDetect = 0x10000000,     //Raw data without smoothing, which is used when there are drastic changes between two adjacent frames, for example, when resetting the cache or switching the camera.
                               //It prevents loss of face ID when the camera is changed.
} bef_ai_face_attribut_config;


/*
*@brief examples of facial expressions:
**/
typedef enum {
 BEF_FACE_ATTRIBUTE_ANGRY = 0,                   //Anger.
 BEF_FACE_ATTRIBUTE_DISGUST = 1,                 //Disgust.
 BEF_FACE_ATTRIBUTE_FEAR = 2,                    //Fear.
 BEF_FACE_ATTRIBUTE_HAPPY = 3,                   //Happiness.
 BEF_FACE_ATTRIBUTE_SAD = 4,                     //Sadness.
 BEF_FACE_ATTRIBUTE_SURPRISE = 5,                //Surprise.
 BEF_FACE_ATTRIBUTE_NEUTRAL = 6,                 //Calm.
 BEF_FACE_ATTRIBUTE_NUM_EXPRESSION = 7           //Number of facial expressions supported.
}bef_ai_face_attribute_expression_type;

/*
*@brief structure of a single face attribute:
**/
typedef struct bef_ai_face_attribute_info {
 float age;                          // Possible age. The value range is from 0 to 100.
 float boy_prob;                     // Probability of being male. The value range is from 0.0 to 1.0.
 float attractive;                   // Level of attractiveness. The value range is from 0 to 100.
 float happy_score;                  // Level of happiness. The value range is from 0 to 100.
 bef_ai_face_attribute_expression_type exp_type;            // Possible expression.
 float exp_probs[BEF_FACE_ATTRIBUTE_NUM_EXPRESSION];    // Probability of each possible expression, without smoothing.
} bef_ai_face_attribute_info;
```


Face attributes are recognized based on detection of the 106 keypoints.

Single\-face detection and multi\-face detection use different APIs. The API for single\-face detection is defined as follows:

```C
BEF_SDK_API bef_effect_result_t bef_effect_ai_face_attribute_detect(
    bef_effect_handle_t handle,
    const unsigned char *image,
    bef_ai_pixel_format pixel_format,
    int image_width,
    int image_height,
    int image_stride,
    const bef_ai_face_106 *ptr_base_info,
    unsigned long long config,
    bef_ai_face_attribute_info *ptr_face_attribute_info
);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |Face detection handle created. |
|image |const unsigned char \* |Data pointer of the input image. |
|pixel_format |bef_ai_pixel_format |Format of the input image. |
|image_width |int |Width of the input image, in pixels. |
|image_height |int |Height of the input image, in pixels. |
|image_stride |int |Row stride of the input image, in pixels. |
|ptr_base_info |const bef_ai_face_106 \* |Face detection result. |
|config |unsigned long long |Configuration of face detection. |
|ptr_face_attribute_info |bef_ai_face_attribute_info \* |Face detection result. |


**Returned Value**

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned. For details, refer to bef_effect_ai_public_define.h.

The API for multi\-face detection is defined as follows:

```C
BEF_SDK_API bef_effect_result_t bef_effect_ai_face_attribute_detect_batch(
    bef_effect_handle_t handle,
    const unsigned char *image,
    bef_ai_pixel_format pixel_format,
    int image_width,
    int image_height,
    int image_stride,
    const bef_ai_face_106 *ptr_base_info,
    int face_count,
    unsigned long long config,
    bef_ai_face_attribute_result *ptr_face_attribute_result
);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |Face detection handle created. |
|image |const unsigned char \* |Data pointer of the input image. |
|pixel_format |bef_ai_pixel_format |Format of the input image. |
|image_width |int |Width of the input image, in pixels. |
|image_height |int |Height of the input image, in pixels. |
|image_stride |int |Row stride of the input image, in pixels. |
|ptr_base_info |const bef_ai_face_106 \* |Face detection result. |
|face_count |int |Number of faces detected. |
|config |unsigned long long |Configuration of face detection. |
|ptr_face_attribute_result |bef_ai_face_attribute_result \* |Face attribute detection result. |


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned. For details, refer to bef_effect_ai_public_define.h.

<span id="5. Destroying the Face Attribute Detection Handle"></span>
### 6. Destroying the Face Attribute Detection Handle

```C
BEF_SDK_API void bef_effect_ai_face_attribute_destroy(
    bef_effect_handle_t handle
);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |Face detection handle created. |


<span id="Java APIs"></span>
# Java APIs

android_sdk.aar in the package is a collection of Java APIs transferred from the C layer through the JNI. It contains all detection models, materials, and other resources required by the SDK.

During Android development, you can directly use the .aar package for easier use of the SDK.

```Java
com.bef.effectsdk.OpenGLUtils                //Some commonly used OpenGL ES.
com.bytedance.labcv.effectsdk.RenderManager    //API related to filters/beautification.
com.bytedance.labcv.effectsdk.FaceDetect    //API related to face detection.
com.bytedance.labcv.effectsdk.BefFaceInfo    //Definitions of face detection results.

com.bytedance.labcv.effectsdk.HandDetect    //API related to hand detection.
com.bytedance.labcv.effectsdk.BefHandInfo    //Definitions of hand detection results.
com.bytedance.labcv.effectsdk.BefBytedEffecctConstants // Constants of the SDK.
```


<span id="106/240/280 Face Keypoints Detection"></span>
## 106/240/280 Face Keypoints Detection

<span id="Call Example"></span>
### Call Example

```Java
// Initialize the 106 face keypoints detection handle.
ret = mFaceDetector.init(context, path,BEF_DETECT_SMALL_MODEL | BEF_DETECT_FULL, ResourceHelper.getLicensePath(LICENSE_NAME));

// Configure the 280 face keypoints detection model.
ret = mFaceDetector.initExtra(context, path, BytedEffectConstants.BEF_MOBILE_FACE_280_DETECT);
// Detect face keypoints.
BefFaceInfo faceInfo = mFaceDetector.detectFace(resizeInputBuffer,PixlFormat.RGBA8888,
       width, height, width * 4,
       rotation);
```


**API Description**

Functions related to face keypoints detection are defined in com.bytedance.labcv.effectsdk.FaceDetect.java. The following describes the typical face detection process.

<span id="1. Initializing the 106 Face Keypoints Detection Handle"></span>
### 1. Initializing the 106 Face Keypoints Detection Handle

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
|modelPath |String |Path of the model file. |
|config |int |Configuration of the face detection algorithm |
|license |String |License file. |


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned. For details, refer to BytedEffectConstants.BytedResultCode.

**Remarks**

Set config to the model type (required; only BytedEffectConstants.BEF_DETECT_SMALL_MODEL is available)

```Java
| Detection mode (default value: BEF_DETECT_MODE_IMAGE. For details, refer to {@link BytedEffectConstants.DetectMode})

| Facial actions to be detected (required; refer to {@link BytedEffectConstants.FaceAction}).
```


<span id="2. Configuring the 240/280 Keypoints Detection Model"></span>
### 2. Configuring the 240/280 Keypoints Detection Model

```Java
public int initExtra(
    Context context,
    String extraModelpath,
    int extraType
)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|context |Context |Context. |
|extraModelpath |String |Path of the model file. |
|extraType |int |Configuration of the algorithm. |


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned. For details, refer to BytedEffectConstants.BytedResultCode.

**Remarks**

Four extraType options are available:


* Config\-240, BEF_MOBILE_FACE_240_DETECT

* Config\-280, BEF_MOBILE_FACE_280_DETECT

* Config\-240 fast mode, BEF_MOBILE_FACE_240_DETECT | BEF_DETECT_FACE_240_DETECT_FASTMODE

* Config\-280 fast mode, BEF_MOBILE_FACE_280_DETECT | BEF_DETECT_FACE_240_DETECT_FASTMODE


If the 280 keypoints detection model, which is provided in our demo, is used, extraType shall be set to BEF_MOBILE_FACE_280_DETECT.

<span id="3. Setting Parameters of Face Keypoints Detection"></span>
### 3. Setting Parameters of Face Keypoints Detection

```Java
public int setDetectParam(
    int paramType ,
    int paramValue
)
```


**Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|paramType |int |Parameter Type |
|paramValue |int |Parameter value |


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned. For details, refer to BytedEffectConstants.BytedResultCode.

<span id="099c24e8"></span>
### 4. Face Occlusion Detection

New API added in version 4.8.1

```Java
public BefFaceInfo getFaceOcclusionResult ()
```


**Return Value** Returns `BefFaceInfo` containing face occlusion information upon success.

<span id="4. Configuring Face Detection"></span>
### 5. Configuring Face Detection

```Java
public void setFaceDetectConfig(int mFaceDetectConfig)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|mFaceDetectConfig |int |Configuration of face detection. |


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned. For details, refer to BytedEffectConstants.BytedResultCode.

<span id="5. Detecting Face Keypoints"></span>
### 6. Detecting Face Keypoints

```Java
public BefFaceInfo detectFace(
    ByteBuffer buffer,
    PixlFormat pixel_format,
    int image_width,
    int image_height,
    int image_stride,
    Rotation orientation
)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|buffer |ByteBuffer |Image data. |
|pixel_format |PixlFormat |Format of the image data. |
|image_width |int |Width of the image. |
|image_height |int |Height of the image. |
|image_stride |int |Row stride of the image. |
|orientation |Rotation |Rotation angle of the image. |


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned. For details, refer to BytedEffectConstants.BytedResultCode.

<span id="6. Destroying the Face Keypoints Detection Handle"></span>
### 7. Destroying the Face Keypoints Detection Handle

```Java
public void release()
```


<span id="Face Attribute Detection"></span>
## Face Attribute Detection

APIs for face attribute detection are defined in com.bytedance.labcv.effectsdk.FaceDetect.java. The following describes the commonly used APIs.

**API Description**

<span id="1. Initializing the Face Attribute Detection Handle"></span>
### 1. Initializing the Face Attribute Detection Handle

```Java
public int initAttri(
    Context context,
    String faceAttriModelPath,
    String faceAttrLicense
)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|context |Context |Context. |
|faceAttriModelPath |String |Path of the face attribute detection model file. |
|faceAttrLicense |String |Face attribute detection license file. |


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned. For details, refer to BytedEffectConstants.BytedResultCode.

<span id="2. Setting Parameters for Face Attribute Detection"></span>
### 2. Setting Parameters for Face Attribute Detection

```Java
public void setAttriDetectConfig(int attriConfig)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|attriConfig |Context |Parameters for face attribute detection. |


**Return value**

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned. For details, refer to BytedEffectConstants.BytedResultCode.

<span id="3. Detecting Face Attributes"></span>
### 3. Detecting Face Attributes

The API is the same as the face keypoints detection API.

```Java
public BefFaceInfo detectFace(
    ByteBuffer buffer,
    PixlFormat pixel_format,
    int image_width,
    int image_height,
    int image_stride,
    RenderManager.Rotation orientation
)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|buffer |ByteBuffer |Image data. |
|pixel_format |PixlFormat |Format of the image data. |
|image_width |int |Width of the image. |
|image_height |int |Height of the image. |
|image_stride |int |Row stride of the image. |
|orientation |Rotation |Rotation angle of the image. |


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned. For details, refer to BytedEffectConstants.BytedResultCode.

<span id="4. Destroying the Face Attribute Detection Handle"></span>
### 4. Destroying the Face Attribute Detection Handle

```Java
public void release()
```


<span id="FAQ"></span>
## FAQ

<span id="1. Which logs should I check when an exception occurs?"></span>
### 1. Which logs should I check when an exception occurs?

You are recommended to check the error type logs output with the following tags:


* **bef_effect_ai**

* **SMASH_E_LOG**

* **EffectSDK**


And then you can conduct detailed troubleshooting via description and solution suggested in [Error Code Table](https://byteplus-docs.readme.io/effects/docs/error-code-table).

<span id="2. Why does the detectFace API that I use in Android to recognize the data converted from Bitmap to ByteBuffer return the error code -37 (invalid image data)?"></span>
### 2. Why does the detectFace API that I use in Android to recognize the data converted from Bitmap to ByteBuffer return the error code \-37 (invalid image data)?

Make sure that buffer memory is allocated by using ByteBuffer.allocateDirect(). At the JNI layer, the native pointers of image data are directly obtained through the function API. If ByteBuffer.allocate() is used, JVM heap memory will be allocated, and as a result, the JNI will fail to access native memory.

<span id="3. Why does detectFace return the error code -107 (invalid configuration)?"></span>
### 3. Why does detectFace return the error code \-107 (invalid configuration)?

Make sure that the initialized bef_effect_ai_face_detect_create and bef_effect_ai_face_detect have the same config settings.

<span id="Error Codes Table"></span>
## Error Codes Table

For details about the error codes, refer to [Error Code Table](https://byteplus-docs.readme.io/effects/docs/error-code-table).
