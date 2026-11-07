---
title: "Body Keypoints"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-body-sdk"
---

The skeleton detection SDK can recognize 18 keypoints of the human skeleton in real time. It supports multi\-person detection, half\-body, side body, and back detection as well as detection of partially blocked objects.

<span id="Keypoints of the Human Skeleton"></span>
## Keypoints of the Human Skeleton

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/f4f4ffe-4804075f9c794f2d8753bd3a3fda38ff_tplv-noop.jpeg) </span>

<span id="Technical Specifications"></span>
# Technical Specifications


|**Category** |**Supported Formats** |
|---|---|
|Platforms |* Android<br><br>* iOS<br><br>* Windows<br><br>* macOS |
|Input format |* RGBA8888<br><br>* BGRA8888<br><br>* BGR888<br><br>* RGB888<br><br>* NV21<br><br>* NV12<br><br>* YUV420p |
|Number of persons |Not limited. Recommended: ≤ 3. |
|Input size |Short side: ≥ 128. |
|Memory usage |< 4 MB (on OPPO R11). |
|Detection speed |< 6 ms (on iPhone 7). |


<span id="C APIs"></span>
# C APIs

For details about the APIs, refer to the header file: bef_effect_ai_hand.h.

<span id="1. Creating a Skeleton Detection Handle"></span>
## 1. Creating a Skeleton Detection Handle

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_skeleton_create(
    const char *model_path,
    bef_effect_handle_t *handle
    );
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|model_path |const char \* |Path of the model file. |
|handle |bef_effect_handle_t \* |Skeleton detection handle created. |


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned. For details, refer to bef_effect_ai_public_define.h.

<span id="2. Checking the Skeleton Detection License"></span>
## 2. Checking the Skeleton Detection License

<span id="2.1. API for Android"></span>
### 2.1. API for Android

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_skeleton_check_license(
    JNIEnv* env,
    jobject context,
    bef_effect_handle_t handle,
    const char *licensePath
    );
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|env |JNIEnv \* |Java Native Interface (JNI). |
|context |jobject |JNI object. |
|handle |bef_effect_handle_t |Skeleton detection handle created. |
|licensePath |const char \* |Path of the license file. |


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned. For details, refer to bef_effect_ai_public_define.h.

<span id="2.2. API for iOS"></span>
### 2.2. API for iOS

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_skeleton_check_license(
    bef_effect_handle_t handle,
    const char *licensePath
    );
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |Skeleton detection handle created. |
|licensePath |const char \* |Path of the license file. |


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned. For details, refer to bef_effect_ai_public_define.h.

<span id="3. Setting the Input Size of the Detection Algorithm"></span>
## 3. Setting the Input Size of the Detection Algorithm

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_skeleton_set_detection_inputsize(
    bef_effect_handle_t handle,
    int width,
    int height
    );
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |Skeleton detection handle created. |
|width |int |Width. |
|height |int |Height. |


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned. For details, refer to bef_effect_ai_public_define.h.

<span id="4. Setting the Input Size of the Tracking Algorithm"></span>
## 4. Setting the Input Size of the Tracking Algorithm

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_skeleton_set_tracking_inputsize(
    bef_effect_handle_t handle,
    int width,
    int height
    );
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |Skeleton detection handle created. |
|width |int |Width. |
|height |int |Height. |


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned. For details, refer to bef_effect_ai_public_define.h.

<span id="5. Setting the Maximum Number of Skeletons to Be Detected"></span>
## 5. Setting the Maximum Number of Skeletons to Be Detected

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_skeleton_set_targetnum(
    bef_effect_handle_t handle,
    int max_skeleton_num
    );
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |Skeleton detection handle created. |
|max_skeleton_num |int |Maximum number of skeletons to be detected. |


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned. For details, refer to bef_effect_ai_public_define.h.

<span id="6. Detecting Skeletons"></span>
## 6. Detecting Skeletons

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_skeleton_detect(
    bef_effect_handle_t handle,
    const unsigned char *image,
    bef_ai_pixel_format pixel_format,
    int image_width,
    int image_height,
    int image_stride,
    bef_ai_rotate_type orientation,
    int *skeleton_info_num,
    bef_skeleton_info **skeleton_info
    );
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |Skeleton detection handle created. |
|image |const unsigned char \* |Data pointer of the input image. |
|pixel_format |bef_ai_pixel_format |Format of the input image. For more information, refer to the Remarks section. |
|image_width |int |Width of the input image, in pixels. |
|image_height |int |Height of the input image, in pixels. |
|image_stride |int |Row stride of the input image, in bytes. |
|orientation |bef_ai_rotate_type |Rotation angle of the input image. For more information, refer to the Remarks section. |
|skeleton_info_num |int |Number of detected skeletons. |
|skeleton_info |bef_skeleton_info \*\* |Detection result. For more information, refer to the Remarks section. |


**Remarks**


1. pixel_format


When using this parameter, refer to bef_ai_pixel_format.

```C
typedef enum {
    BEF_AI_PIX_FMT_RGBA8888, // RGBA 8:8:8:8, 32 bpp (4 channels, 32 bits, RGBA pixel).
    BEF_AI_PIX_FMT_BGRA8888, // BGRA 8:8:8:8, 32 bpp (4 channels, 32 bits, RGBA pixel).
    BEF_AI_PIX_FMT_BGR888,   // BGR 8:8:8, 24 bpp (3 channels, 32 bits, RGB pixel).
    BEF_AI_PIX_FMT_RGB888,   // RGB 8:8:8, 24 bpp (3 channels, 32 bits, RGB pixel).
    BEF_AI_PIX_FMT_GRAY8,    // GRAY, 8 bpp (1 channel, 8 bits, gray pixel). It is not yet supported.
    BEF_AI_PIX_FMT_YUV420P,  // YUV 4:2:0, 12 bpp (3 continuous channels: brightness channel, U channel, and V channel). It is not yet supported.
    BEF_AI_PIX_FMT_NV12,     // YUV 4:2:0, 12 bpp (3 channels: brightness channel and interleaved U and V channels). It is not yet supported.
    BEF_AI_PIX_FMT_NV21      // YUV 4:2:0, 12 bpp (3 channels: brightness channel and interleaved U and V channels). It is not yet supported.
} bef_ai_pixel_format;
```



2. skeleton_info


Skeleton information detected. It requires memory applied for externally. The information amount is subject to skeleton_info_num. When using skeleton_info, refer to bef_skeleton_info.

```C
typedef struct bef_skeleton_info {
    bef_skeleton_point_info      keyPointInfos[BEF_MAX_SKELETON_POINT_NUM];     // Skeleton information detected.
    bef_ai_rect  skeletonRect; // Rectangular skeleton area.
} bef_skeleton_info;
```


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned. For details, refer to bef_effect_ai_public_define.h.

<span id="7. Destroying the Skeleton Detection Handle"></span>
## 7. Destroying the Skeleton Detection Handle

```C
BEF_SDK_API void
bef_effect_ai_skeleton_destroy(bef_effect_handle_t handle);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |Skeleton detection handle created. |


<span id="Java APIs"></span>
# Java APIs

<span id="1. Creating a Skeleton Detection Handle"></span>
## 1. Creating a Skeleton Detection Handle

```Java
public int init(
    Context context,
    String modelPath,
    String licensePath
    );
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|context |Context |Context. |
|modelPath |String |Path of the model file. |
|licensePath |String |Path of the license file. |


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned.

<span id="2. Setting the Input Size of the Detection Algorithm"></span>
## 2. Setting the Input Size of the Detection Algorithm

```Java
public int setDetectionInput(
  int width,
    int height
    );
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|width |int |Width. |
|height |int |Height. |


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned.

<span id="3. Setting the Input Size of the Tracking Algorithm"></span>
## 3. Setting the Input Size of the Tracking Algorithm

```Java
public int setTrackingInput(
    int width,
    int height
    );
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|width |int |Width. |
|height |int |Height. |


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned.

<span id="4. Setting the Maximum Number of Skeletons to Be Detected"></span>
## 4. Setting the Maximum Number of Skeletons to Be Detected

```Java
public int setTargetNum(int num);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|num |int |Maximum number of skeletons to be detected. |


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned.

<span id="5. Detecting Skeletons"></span>
## 5. Detecting Skeletons

```Java
public BefSkeletonInfo detectSkeleton(
    ByteBuffer buffer,
    BytedEffectConstants.PixlFormat pixel_format,
    int image_width,
    int image_height,
    int image_stride,
    BytedEffectConstants.Rotation orientation
    );
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|buffer |ByteBuffer |Image data. |
|pixel_format |BytedEffectConstants.PixlFormat |Format of the image. For more information, refer to the Remarks section. |
|image_width |int |Width of the image, in pixels. |
|image_height |int |Height of the image, in pixels. |
|image_stride |int |Row stride of the image, in bytes. |
|orientation |BytedEffectConstants.Rotation |Rotation angle of the image. For more information, refer to the Remarks section. |


**Remarks**


1. pixel_format


When using this parameter, refer to com.bytedance.labcv.effectsdk.BytedEffectConstants.PixlFormat.

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



2. orientation


When using this parameter, refer to com.bytedance.labcv.effectsdk.BytedEffectConstants.Rotation.

```Java
public enum Rotation {
    /**
     * The image does not need to be rotated.
     */
    CLOCKWISE_ROTATE_0(0),
    /**
     * Rotate the image clockwise by 90°.
     */
    CLOCKWISE_ROTATE_90(1),
    /**
     * Rotate the image clockwise by 180°.
     */
    CLOCKWISE_ROTATE_180(2),
    /**
     * Rotate the image clockwise by 270°.
     */
    CLOCKWISE_ROTATE_270(3);
    public int id = 0;
    Rotation(int id) {
        this.id = id;
    }
}
```


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned.

<span id="6. Destroying the Skeleton Detection Handle"></span>
## 6. Destroying the Skeleton Detection Handle

```Java
public void release();
```


<span id="FAQ"></span>
## FAQ

<span id="1. Which logs should I check when an exception occurs?"></span>
### 1. Which logs should I check when an exception occurs?

You are recommended to check the error type logs output with the following tags:


* **bef_effect_ai**

* **SMASH_E_LOG**

* **EffectSDK**


<span id="2. What should I do if skeleton detection fails?"></span>
### 2. What should I do if skeleton detection fails?

You are recommended to troubleshoot the failure as follows:


* Check whether the skeleton detection handle has been initialized.

* Check whether the skeleton detection handle has been licensed.

* If it has been successfully initialized, check whether the set input image data is complete and whether the types are supported.


<span id="Error Codes"></span>
## Error Codes

For details about the error codes, refer to [Error Code Table](https://byteplus-docs.readme.io/effects/docs/error-code-table).
