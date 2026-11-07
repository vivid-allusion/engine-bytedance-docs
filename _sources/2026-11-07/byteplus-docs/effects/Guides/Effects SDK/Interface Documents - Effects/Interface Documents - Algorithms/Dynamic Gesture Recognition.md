---
title: "Dynamic Gesture Recognition"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-dynamic-gesture-recognition"
---

The dynamic gesture SDK recognizes up to 17 types of dynamic gestures, including left and right slips.

<span id="Technical Specifications"></span>
# Technical Specifications


|**Category** |**Supported Formats** |
|---|---|
|Platforms |* Android<br><br>* iOS |
|Input formats |* RGBA8888<br><br>* BGRA8888<br><br>* BGR888<br><br>* RGB888 |
|Memory usage |< 12 MB (test device: Oppo R11) |
|Time consumption |< 5 ms (test device: Oppo R11) |


<span id="C API"></span>
# C API

For details about the API, refer to the bef_effect_ai_dynamic_gesture.h header file.

<span id="1. Create a Handle for the Dynamic Gesture Algorithm"></span>
## 1. Create a Handle for the Dynamic Gesture Algorithm

```C
BEF_SDK_API bef_effect_result_t  
bef_effect_ai_dynamic_gesture_create(bef_effect_handle_t *handle);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The created handle for the dynamic gesture algorithm. |


**Return value:** 

If the request is successful, BEF_RESULT_SUC is returned. If the request fails, an error code is returned. For details, refer to the bef_effect_ai_public_define.h file.

<span id="2. Initialize the Model Parameters from the Model File"></span>
## 2. Initialize the Model Parameters from the Model File

```C
BEF_SDK_API bef_effect_result_t  
bef_effect_ai_dynamic_gesture_init(
    bef_effect_handle_t handle,  
    const char* model_path);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The handle for the dynamic gesture algorithm. |
|model_path |const char\* |The path to the folder where the model file is located. |


**Return value:** 

If the request is successful, BEF_RESULT_SUC is returned. If the request fails, an error code is returned. For details, refer to the bef_effect_ai_public_define.h file.

<span id="3. Set SDK Parameters"></span>
## 3. Set SDK Parameters

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This is a reserved interface that does not support external parameter settings.</div>


<span id="4. Perform Dynamic Gestures"></span>
## 4. Perform Dynamic Gestures

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_dynamic_gesture_detect(
    bef_effect_handle_t handle,
    const unsigned char *image,
    bef_ai_pixel_format pixel_format,
    int image_width,
    int image_height,
    int image_stride,
    bef_ai_rotate_type orientation,
    bef_ai_dynamic_gesture_ret *result);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The handle for the dynamic gesture algorithm. |
|image |const unsigned char\* |The size of the input image. |
|pixel_format |bef_ai_pixel_format |The format of the input image. |
|image_width |int |The width of the input image. |
|image_height |int |The height of the input image. |
|image_stride |int |The stride of the input image. |
|orientation |bef_ai_rotate_type |The rotation angle of the input image. |
|result |bef_ai_dynamic_gesture_ret\* |The return result after algorithm processing. |


**Return value:** 

If the request is successful, BEF_RESULT_SUC is returned. If the request fails, an error code is returned. For details, refer to the bef_effect_ai_public_define.h file.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For details about bef_ai_dynamic_gesture_ret, refer to the bef_effect_ai_dynamic_gesture.h file.</div>


```C
/**
 * @brief The return value of the encapsulation forecast interface
 *
 * @note You can add custom data for different algorithms.
 */
typedef struct {
    int action;
    float action_score;
} bef_ai_dynamic_gesture_info;

/// @brief The detection result.
typedef struct {
    bef_ai_dynamic_gesture_info p_gestures[BEF_MAX_GESTURE_HAND_NUM]; ///< The information of the detected dynamic gestures.    
    int gesture_count;                                                ///< The number of detected dynamic gestures；
} bef_ai_dynamic_gesture_ret;
```


<span id="5. Release the Handle for the Dynamic Gesture Algorithm"></span>
## 5. Release the Handle for the Dynamic Gesture Algorithm

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_dynamic_gesture_release(bef_effect_handle_t handle);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The handle for the dynamic gesture algorithm. |


**Return value:** 

If the request is successful, BEF_RESULT_SUC is returned. If the request fails, an error code is returned. For details, refer to the bef_effect_ai_public_define.h file.

<span id="6. Configure a License for Dynamic Gesture Recognition"></span>
## 6. Configure a License for Dynamic Gesture Recognition

```C
// The offline licensin detection mode
BEF_SDK_API bef_effect_result_t
bef_effect_ai_dynamic_gesture_check_license(
    bef_effect_handle_t handle,
    const char *licensePath);

// The online licensin detection mode
BEF_SDK_API bef_effect_result_t
bef_effect_ai_dynamic_gesture_check_online_license(
    bef_effect_handle_t handle,
    const char *licensePath);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The handle for the dynamic gesture algorithm. |
|licensePath |const char \* |The string of the license file. |


**Return value:** 

If the request is successful, BEF_RESULT_SUC is returned. If the request fails, an error code is returned. For details, refer to the bef_effect_ai_public_define.h file.

<span id="Java API"></span>
# Java API

**API Description**

For details about the API, refer to the com.bytedance.labcv.effectsdk.DynamicGestureDetect.java file.

<span id="1. Initialize the Handle for the Dynamic Gesture Algorithm"></span>
## 1. Initialize the Handle for the Dynamic Gesture Algorithm

```Java
public int init(
    Context context,
    String modelPath,
    String licensePath,
    boolean onlineLicense)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|context |Context |The application context. |
|modelpath |String |The absolute path of the model file. |
|licensePath |String |The absolute path of the license file. |
|onlineLicense |Boolean |The license type. |


**Return value:** 

If the request is successful, BEF_RESULT_SUC is returned. If the request fails, an error code is returned.

<span id="2. Set SDK Parameters"></span>
## 2. Set SDK Parameters

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This is a reserved interface that does not support external parameter settings.</div>


<span id="3. Perform Dynamic Gestures"></span>
## 3. Perform Dynamic Gestures

```Java
public BefDynamicGestureInfo detect(
    ByteBuffer buffer,
    BytedEffectConstants.PixlFormat pixelFormat,
    int imageWidth,
    int imageHeight,
    int imageStride,
    BytedEffectConstants.Rotation orientation)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|buffer |ByteBuffer |The input image data. |
|pixelFormat |BytedEffectConstants.PixlFormat |The format of the input image. |
|imageWidth |int |The width of the input image. |
|imageHeight |int |The height of the input image. |
|imageStride |int |The stride of the input image. |
|orientation |BytedEffectConstants.Rotation |The rotation angle of the input image. |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For details about the BefDynamicGestureInfo class, refer to the com.bytedance.labcv.effectsdk.BefDynamicGestureInfo.java file. The definition of BefDynamicGestureInfo is the same as that of bef_ai_chroma_keying_ret in C API.</div>


```Java
/**
 * The result of the dynamic gesture algorithm
 */
public class BefDynamicGestureInfo {

  /**
   * Array of Dynamic Gesture
   */
  private GestureInfo[] gestureInfos;

  /**
   * Amount of Gesture
   */
  private int gestureNum;

  public GestureInfo[] getGestureInfos() {
    return gestureInfos;
  }

  public void setGestureInfos(GestureInfo[] gestureInfos) {
    this.gestureInfos = gestureInfos;
  }

  public int getGestureNum() {
    return gestureNum;
  }

  public void setGestureNum(int gestureNum) {
    this.gestureNum = gestureNum;
  }

  public static class GestureInfo {

    private int actionType = 0;
    private float actionScore = 0.0f;

    public int getActionType() {
        return actionType;
    }

    public float getActionScore() {
        return actionScore;
    }

    @Override
    public String toString() {
        return "GestureInfo{" +
                "actionType=" + actionType +
                ", actionType=" + actionType +
                '}';
    }
  }
}
```


**Return value:** 

If the request is successful, the BefDynamicGestureInfo class is returned with the detected dynamic gestures.

<span id="4. Release the Handle for the Dynamic Gesture Algorithm"></span>
## 4. Release the Handle for the Dynamic Gesture Algorithm

```Java
public void release()
```


<span id="FAQ"></span>
## FAQ

<span id="1. Q: What logs do I need to check if an exception occurs?"></span>
### 1. Q: What logs do I need to check if an exception occurs?

A: We recommend that you check for the error logs with the following tags:


* **bef_effect_ai**

* **SMASH_E_LOG**

* **EffectSDK**


<span id="Error Codes"></span>
## Error Codes

For details about the error codes, refer to [Error Codes](https://docs.byteplus.com/99783).
