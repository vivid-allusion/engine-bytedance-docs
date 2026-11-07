---
title: "Gesture Recognition"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-gesture-sdk"
---

The hand gesture recognition SDK supports classification of up to 45 hand gestures as well as keypoints tracking and segmentation, with high stability and low performance cost. It can apply to hand gesture interaction scenarios.

<span id="Keypoints Index of the Hand"></span>
## Keypoints Index of the Hand

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/589ad3d-1.png) </span>

<span id="Technical Specifications"></span>
# Technical Specifications


|**Category** |**Supported Formats** |
|---|---|
|Platforms |* Android<br><br>* iOS<br><br>* Windows<br><br>* macOS |
|Hand gestures |≤ 45. |
|Hands simultaneously tracked |≤ 20. |
|Input format |* RGBA8888<br><br>* BGRA8888<br><br>* BGR888<br><br>* RGB888<br><br>* NV21<br><br>* NV12<br><br>* YUV420p |
|Input size |Short side: ≥ 360. |
|Memory usage |< 6 MB (on OPPO R11). |
|Hand gesture detection speed |< 6 ms (on iPhone 7). |


<span id="C APIs"></span>
# C APIs

The header file is bef_effect_ai_hand.h.

**API Description**

<span id="1. Creating a Hand Gesture Detection Handle"></span>
## 1. Creating a Hand Gesture Detection Handle

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_hand_detect_create(
    bef_ai_hand_sdk_handle *handle,
    unsigned int config
    );
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handler_t |Hand gesture detection handle created. |
|config |unsigned int |Configuration of the hand gesture detection algorithm. This parameter is currently not used. |


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned. For details, refer to bef_effect_ai_public_define.h.

<span id="2. Checking the Hand Gesture Detection License"></span>
## 2. Checking the Hand Gesture Detection License

<span id="API for Android"></span>
### API for Android

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_hand_check_license(
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
|handle |bef_effect_handle_t |Hand gesture detection handle created. |
|licensePath |const char \* |Character string of the license file. |


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned. For details, refer to bef_effect_ai_public_define.h.

<span id="API for iOS"></span>
### API for iOS

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_hand_check_license(
    bef_effect_handle_t handle,
    const char *licensePath
    );
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |Hand gesture detection handle created. |
|licensePath |const char \* |Character string of the license file. |


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned. For details, refer to bef_effect_ai_public_define.h.

<span id="3. Configuring the Model File"></span>
## 3. Configuring the Model File

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_hand_detect_setmodel(
    bef_effect_handle_t handle,
    bef_ai_hand_model_type type,
    const char * strModelPath);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_ai_hand_sdk_handle |Hand gesture detection handle created. |
|type |bef_ai_hand_model_type |Model file type. For more information, refer to the Remarks section. |
|strModelPath |const char \* |Path of the model file. |


**Remarks**


1. type


When using this parameter, refer to bef_ai_hand_model_type.

```C
typedef enum {
    BEF_HAND_MODEL_DETECT = 0x0001,       // Hand detection (required).
    BEF_HAND_MODEL_BOX_REG = 0x0002,      // Hand box detection (required).
    BEF_HAND_MODEL_GESTURE_CLS = 0x0004,  // Hand gesture classification (optional).
    BEF_HAND_MODEL_KEY_POINT = 0x0008,    // Hand keypoints (optional).
    BEF_HAND_MODEL_SEGMENT = 0x0010,    // Visible segment (optional).
} bef_ai_hand_model_type;
```


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned. For details, refer to bef_effect_ai_public_define.h.

<span id="4. Setting Parameters"></span>
## 4. Setting Parameters

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_hand_detect_setparam(
    bef_effect_handle_t handle,
    bef_ai_hand_param_type type,
    float value
    );
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_ai_hand_sdk_handle |Hand gesture detection handle created. |
|type |bef_ai_hand_param_typ |Parameter type. For more information, refer to the Remarks section. |
|value |float |Path of the model file. |


**Remarks**


1. type


When using this parameter, refer to bef_ai_hand_param_type.

```C
typedef enum {
    BEF_HAND_REFRESH_FRAME_INTERVAL = 1,      // Refresh frame intervals. This is not yet supported.
    BEF_HAND_MAX_HAND_NUM = 2,                // Maximum number of hands. The default value is 1, and the upper limit is 2.
    BEF_HAND_DETECT_MIN_SIDE = 3,             // Length of the shortest side. The default value is 192.
    BEF_HAND_CLS_SMOOTH_FACTOR = 4,           // Classification smoothing factor. The default value is 0.7. The larger the value, the more stable the classification.
    BEF_HAND_USE_ACTION_SMOOTH = 5,           // Whether to enable classification smoothing. The default value of 1 indicates enable, and 0 indicates disable.
    BEF_HAND_ALGO_LOW_POWER_MODE = 6,         // Algorithm degraded mode. It is not used by default.
    BEF_HAND_ALGO_AUTO_MODE = 7,              // Algorithm degraded mode. It is not used by default.
    // If HAND_ALGO_AUTO_MODE is used, use the following parameters to set the thresholds for algorithm degraded mode.
    BEF_HAND_ALGO_TIME_ELAPSED_THRESHOLD = 8, // Elapsed time threshold. The default value is 20 ms.
    BEF_HAND_ALGO_MAX_TEST_FRAME = 9,         // Number of times the test algorithm is executed during runtime. The default value is 150.
    BEF_HAND_IS_USE_DOUBLE_GESTURE = 10,      // Whether to use two-handed gestures. The default value is true.
    BEF_HNAD_ENLARGE_FACTOR_REG = 11,         // Zoom ratio of the initial input box of the regression model.
    BEF_HAND_NARUTO_GESTURE = 12,             // Whether to support Naruto hand signs. The default value is false. If it is set to true, 45 hand gestures, including the Naruto hand signs, will be supported.
} bef_ai_hand_param_type;
```


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned. For details, refer to bef_effect_ai_public_define.h.

<span id="5. Detecting Hand Gestures"></span>
## 5. Detecting Hand Gestures

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_hand_detect(
    bef_ai_hand_sdk_handle handle,
    const unsigned char *image,
    bef_ai_pixel_format pixel_format,
    int image_width,
    int image_height,
    int image_stride,
    bef_ai_rotate_type orientation,
    unsigned long long detection_config,
    bef_ai_hand_info *p_hand_info,
    int delayframecount
    );
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handler_t |Hand gesture detection handle created. |
|image |const unsigned char \* |Data pointer of the input image. |
|pixel_format |bef_ai_pixel_format |Format of the input image. |
|image_width |int |Width of the input image, in pixels. |
|image_height |int |Height of the input image, in pixels. |
|image_stride |int |Row stride of the input image, in bytes. |
|orientation |bef_ai_rotate_type |Rotation angle of the input image. For more information, refer to the Remarks section. |
|detection_config |unsigned long long |Detection model requested. For more information, refer to the Remarks section. |
|p_hand_info |bef_ai_hand_info |Storage result information. Externally allocated memory. |
|delayframecount |int |Delay of the output result. For more information, refer to the Remarks section. |


**Remarks**


1. orientation


For details, refer to bef_ai_rotate_type in bef_effect_ai_public_public_define.h.


2. detection_config


Detection model requested. It is the bitwise AND operation of hand_model_type. Currently, only HAND_MODEL_GESTURE_CLS and HAND_MODEL_KEY_POINT are available.


3. delayframecount


Delay of the output result. The algorithm will return the detection result after the specified number of frames. The larger the value, the more stable the result. The default value is 4.

**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned. For details, refer to bef_effect_ai_public_define.h.

<span id="6. Destroying the Hand Gesture Detection Handle"></span>
## 6. Destroying the Hand Gesture Detection Handle

```C
BEF_SDK_API void
bef_effect_ai_hand_detect_destroy(bef_ai_hand_sdk_handle handle);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_ai_hand_sdk_handle |Hand gesture detection handle created. |


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned. For details, refer to bef_effect_ai_public_define.h.

<span id="Java APIs"></span>
# Java APIs

For definitions of the functions related to hand gesture detection, refer to com.bytedance.labcv.effectsdk.HandDetect.java.

<span id="1. Initializing the Hand Gesture Detection Handle"></span>
## 1. Initializing the Hand Gesture Detection Handle

```Java
public int createHandle(
    Context context,
    String licensePath
    );
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|context |Context |Context. |
|licensePath |String |Path of the license file. |


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned.

<span id="2. Configuring the Model File"></span>
## 2. Configuring the Model File

```Java
public int setModel(
    BytedEffectConstants.HandModelType modelType,
    String modelPath)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|modelType |BytedEffectConstants.HandModelType |Model type. For more information, refer to the Remarks section. |
|modelPath |String |Path of the license file. |


**Remarks**


1. modelType


When using this parameter, refer to com.bytedance.labcv.effectsdk.BytedEffectConstants.HandModelType.

```Java
public enum HandModelType {
    /**
     * Hand detection (required).
     */
    BEF_HAND_MODEL_DETECT(0x0001),
    /**
     * Hand position detection (required).
     */
    BEF_HAND_MODEL_BOX_REG(0x0002),
    /**
     * Hand gesture classification (optional).
     */
    BEF_HAND_MODEL_GESTURE_CLS(0x0004),
    /**
     * Hand keypoints (optional).
     */
    BEF_HAND_MODEL_KEY_POINT(0x0008);
    private int value;
    HandModelType(int value) {
        this.value = value;
    }
    public int getValue() {
        return value;
    }
}
```


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned.

<span id="3. Setting Parameters"></span>
## 3. Setting Parameters

```Java
public int setParam(
    BytedEffectConstants.HandParamType paramType,
    float paramValue)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|paramType |BytedEffectConstants.HandParamType |Parameter type. For more information, refer to the Remarks section. |
|paramValue |float |Parameter value. |


**Remarks**


1. paramType


When using this parameter, refer to com.bytedance.labcv.effectsdk.BytedEffectConstants.HandParamType.

```Java
public enum HandParamType {
    /**
     * Maximum number of hands. The default value is 1, and the upper limit is 2.
     */
    BEF_HAND_MAX_HAND_NUM(2),
    /**
     * Length of the shortest side. The default value is 192.
     */
    BEF_HAND_DETECT_MIN_SIDE(3),
    /**
     * Classification smoothing factor. The default value is 0.7. The larger the value, the more stable the classification.
     */
    BEF_HAND_CLS_SMOOTH_FACTOR(4),
    /**
     * Whether to enable classification smoothing. The default value of 1 indicates enable, and 0 indicates disable.
     */
    BEF_HAND_USE_ACTION_SMOOTH(5),
    /**
     * Algorithm degraded mode. It is used on low-end phone models to reduce the runtime of the algorithm, but it has a lower detection accuracy. The default value is 0, indicating that degraded mode is not used. The value 1 indicates that degraded mode is used.
     */
    BEF_HAND_ALGO_LOW_POWER_MODE(6),
    /**
     * Auto algorithm degraded mode. It takes effect when BEF_HAND_ALGO_TIME_ELAPSED_THRESHOLD is exceeded; otherwise, it does not take effect.
     * The default value is 0, indicating that degraded mode is not used. The value 1 indicates that auto degraded mode is used.
     */
    BEF_HAND_ALGO_AUTO_MODE(7),
    /**
     * Elapsed time threshold. The default value is 15 ms.
     */
    BEF_HAND_ALGO_TIME_ELAPSED_THRESHOLD(8),
    /**
     * Number of times the test algorithm is executed during runtime. The default value is 150.
     */
    BEF_HAND_ALGO_MAX_TEST_FRAME(9),
    /**
     * Whether to use two-handed gestures. The default value is true.
     */
    BEF_HAND_IS_USE_DOUBLE_GESTURE(10),
    /**
     * Zoom ratio of the initial input box of the regression model.
     */
    BEF_HNAD_ENLARGE_FACTOR_REG(11),
    /**
     * Whether to support Naruto hand signs. The default value is false. If it is set to true, 45 hand gestures, including the Naruto hand signs, will be supported.
     */
    BEF_HAND_NARUTO_GESTUER(12);
    private int value;
    HandParamType(int value) {
        this.value = value;
    }
    public int getValue() {
        return value;
    }
}
```


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned.

<span id="4. Detecting Hand Gestures"></span>
## 4. Detecting Hand Gestures

```Java
public BefHandInfo detectHand(
    ByteBuffer buffer,
    BytedEffectConstants.PixlFormat pixel_format,
    int image_width,
    int image_height,
    int image_stride,
    BytedEffectConstants.Rotation orientation,
    int detectconfig,
    int delayFrameCount
    );
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|buffer |ByteBuffer |Parameter type. For more information, refer to the Remarks section. |
|pixel_format |BytedEffectConstants.PixlFormat |Format of the image. For more information, refer to the Remarks section. |
|image_width |int |Width of the image, in pixels. |
|image_height |int |Height of the image, in pixels. |
|image_stride |int |Row stride of the image, in bytes. |
|orientation |BytedEffectConstants.Rotation |Rotation angle of the image. For more information, refer to the Remarks section. |
|detectconfig |int |Detection model requested. For more information, refer to the Remarks section. |
|delayFrameCount |int |Delay of the output result. For more information, refer to the Remarks section. |


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



3. detectconfig


When using this parameter, refer to com.bytedance.labcv.effectsdk.BytedEffectConstants.HandModelType. Perform the AND operation on the enumerated variables of the required function.


4. delayFrameCount


Delay of the output result. The algorithm will return the detection result after the specified number of frames. The larger the value, the more stable the result. The default value is 4.

**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned.

<span id="5. Destroying the Hand Gesture Detection Handle"></span>
## 5. Destroying the Hand Gesture Detection Handle

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


<span id="2. What should I do if hand gesture recognition fails?"></span>
### 2. What should I do if hand gesture recognition fails?

You are recommended to troubleshoot the failure as follows:


* Check whether the hand gesture detection handle has been initialized.

* Check whether the hand gesture detection handle has been licensed.

* If it has been successfully initialized, check whether the set input image data is complete and whether the types are supported.


<span id="Error Codes"></span>
## Error Codes

For details about the error codes, refer to [Error Code Table](https://byteplus-docs.readme.io/effects/docs/error-code-table).

<span id="6. Hand Gestures"></span>
## 6. Hand Gestures

Refer to [Hand Gesture List](https://bytedance.feishu.cn/docx/doxcnxFGScTn1EjEPvGRhTknpIc).
