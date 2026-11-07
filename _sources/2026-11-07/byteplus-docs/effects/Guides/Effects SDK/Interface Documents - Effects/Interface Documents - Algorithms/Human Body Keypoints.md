---
title: "Human Body Keypoints"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-human-body-keypoints"
---

The skeleton keypoint SDK detects 2D keypoints of human skeletons. It detects up to 63 keypoints of a human skeleton and supports only full\-body detection.

<span id="Technical Specifications"></span>
# Technical Specifications


|**Category** |**Supported Formats** |
|---|---|
|Platforms |* Android<br><br>* iOS |
|Input formats |* RGBA8888<br><br>* BGRA8888<br><br>* BGR888,<br><br>* RGB888 |
|Memory usage |< 10 MB (test device: Oppo R11) |
|Time consumption |< 27 ms (test device: Oppo R11) |


<span id="C API"></span>
# C API

For details about the API, refer to the bef_effect_ai_bach_skeleton.h header file.

<span id="1. Create a Handle for the Skeleton Keypoint Algorithm"></span>
## 1. Create a Handle for the Skeleton Keypoint Algorithm

```C
BEF_SDK_API bef_effect_result_t  
bef_effect_ai_bach_skeleton_create(bef_effect_handle_t *handle);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The created handle for the skeleton keypoint algorithm. |


**Return value:** 

If the request is successful, BEF_RESULT_SUC is returned. If the request fails, an error code is returned. For details, refer to the bef_effect_ai_public_define.h file.

<span id="2. Initialize the Model Parameters from the Model File"></span>
## 2. Initialize the Model Parameters from the Model File

```C
BEF_SDK_API bef_effect_result_t  
bef_effect_ai_bach_skeleton_init(
    bef_effect_handle_t handle,  
    const char* model_path);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The handle for the skeleton keypoint algorithm. |
|model_path |const char\* |The path to the folder where the model file is located. |


**Return value:** 

If the request is successful, BEF_RESULT_SUC is returned. If the request fails, an error code is returned. For details, refer to the bef_effect_ai_public_define.h file.

<span id="3. Set SDK Parameters"></span>
## 3. Set SDK Parameters

```C
// Set interface parameters of the int type
BEF_SDK_API bef_effect_result_t
bef_effect_ai_bach_skeleton_set_paramI(
    bef_effect_handle_t handle,
    bef_ai_bach_skeleton_param_type type,
    int value);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The handle for the skeleton keypoint algorithm. |
|type |bef_ai_bach_skeleton_param_type |The type of the skeleton keypoint parameter. |
|value |int |The value of the skeleton keypoint parameter. |


**Return value:** 

If the request is successful, BEF_RESULT_SUC is returned. If the request fails, an error code is returned. For details, refer to the bef_effect_ai_public_define.h file.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For details about bef_ai_bach_skeleton_param_type, refer to the bef_effect_ai_bach_skeleton.h file.</div>


```C
/**
 * @brief Model parameter type
 *
 */
typedef enum {
    BEF_AI_BACH_SKELETON_BODY_MAX_COUNT = 0,     // The maximum number of detected skeletons. The maximum value is 5. The value is of the int type
    BEF_AI_BACH_SKELETON_FORCE_DETECT = 1,       // Set the tracking mode. The value is of the int type.
                                                 //    0: Detection is not compulsory (tracking mode, default value).
                                                 //    1: Detection per frame is compulsory
    BEF_AI_BACH_SKELETON_IMAGE_MODE = 2,         // Set the detection mode. The value is of the int type
                                                 //    0: video mode (detection and tracking, default value) 
                                                 //    1: image mode (no tracking) 
} bef_ai_bach_skeleton_param_type;     
```


<span id="4. Detect Skeleton Keypoints"></span>
## 4. Detect Skeleton Keypoints

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_bach_skeleton_detect(
    bef_effect_handle_t handle,
    const unsigned char *image,
    bef_ai_pixel_format pixel_format,
    int image_width,
    int image_height,
    int image_stride,
    bef_ai_rotate_type orientation,
    bef_ai_bach_skeleton_info *result);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The handle for the skeleton keypoint algorithm. |
|image |const unsigned char\* |The size of the input image. |
|pixel_format |bef_ai_pixel_format |The format of the input image. |
|image_width |int |The width of the input image. |
|image_height |int |The height of the input image. |
|image_stride |int |The stride of the input image. |
|orientation |bef_ai_rotate_type |The rotation angle of the input image. |
|result |bef_ai_bach_skeleton_info\* |The return result after algorithm processing. |


**Return value:** 

If the request is successful, BEF_RESULT_SUC is returned. If the request fails, an error code is returned. For details, refer to the bef_effect_ai_public_define.h file.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For details about bef_ai_bach_skeleton_info, refer to the bef_effect_ai_bach_skeleton.h file.</div>


```C
//  The detection keypoint instance.
typedef struct bef_ai_bach_skeleton_point_info_st {
    float x; // The corresponding columns. Value range: [0, width], float y;
    float y; // The corresponding rows. Value range: [0, height], bool is_detect;
    bool is_detect; // If the value is 0, x and y are meaningless
    float score; // The score of the corresponding point.
} bef_ai_bach_skeleton_point_info;

// Detection result
typedef struct bef_ai_bach_skeleton_info_st {
    int id;
    int orientation;
    bef_ai_bach_skeleton_point_info keyPointInfos[BEF_AI_MAX_BACH_SKELETON_POINT_NUM];     // Detected body keypoints info
    bef_ai_rect  skeletonRect; // The skeleton rectangular.
} bef_ai_bach_skeleton_info;
```


<span id="5. Release the Handle for the Skeleton Keypoint Algorithm"></span>
## 5. Release the Handle for the Skeleton Keypoint Algorithm

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_bach_skeleton_release(bef_effect_handle_t handle);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The handle for the skeleton keypoint algorithm. |


**Return value:** 

If the request is successful, BEF_RESULT_SUC is returned. If the request fails, an error code is returned. For details, refer to the bef_effect_ai_public_define.h file.

<span id="6. Configure a License for Skeleton Keypoint Detection"></span>
## 6. Configure a License for Skeleton Keypoint Detection

```C
// offline license detection mode
BEF_SDK_API bef_effect_result_t
bef_effect_ai_bach_skeleton_check_license(
    bef_effect_handle_t handle,
    const char *licensePath);

// online license detection mode
BEF_SDK_API bef_effect_result_t
bef_effect_ai_bach_skeleton_check_online_license(
    bef_effect_handle_t handle,
    const char *licensePath);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The handle for the skeleton keypoint algorithm. |
|licensePath |const char \* |The string of the license file. |


**Return value:** 

If the request is successful, BEF_RESULT_SUC is returned. If the request fails, an error code is returned. For details, refer to the bef_effect_ai_public_define.h file.

<span id="Java API"></span>
# Java API

**API Description**

For details about the API, refer to the com.bytedance.labcv.effectsdk.BachSkeletonDetect.java file.

<span id="1. Initialize the Handle for the Skeleton Keypoint Algorithm"></span>
## 1. Initialize the Handle for the Skeleton Keypoint Algorithm

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

```Java
// Set interface parameters of the int type
public int setParamI(
    BytedEffectConstants.BachSkeletonParamType paramType,
    int value)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|paramType |BytedEffectConstants.BachSkeletonParamType |The type of the input parameter. |
|value |int | |


**Return value:** 

If the request is successful, BEF_RESULT_SUC is returned. If the request fails, an error code is returned.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For details about BytedEffectConstants.BachSkeletonParamType, refer to the com.bytedance.labcv.effectsdk.BytedEffectConstants.java file. The definition of BytedEffectConstants.BachSkeletonParamType is the same as that of bef_ai_bach_skeleton_param_type in C API.</div>


<span id="3. Detect Skeleton Keypoints"></span>
## 3. Detect Skeleton Keypoints

```Java
public BefBachSkeletonInfo detect(
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


<div data-tips="true" data-tips-type="warning">For details about the BefBachSkeletonInfo class, refer to the com.bytedance.labcv.effectsdk.BefBachSkeletonInfo.java file. The definition of BefBachSkeletonInfo is the same as that of BefBachSkeletonInfo in C API.</div>


```Java
/**
 * Key detection results of skeleton
 */
public class BefBachSkeletonInfo {

  /**
   * Key points of skeleton
   */
  private Skeleton[] skeletons;

  /**
   * Amount of human
   */

  private int skeletonNum;

  /**
   * Get amount of human
   * @return amount of human
   */
  public int getSkeletonNum() {
    return skeletonNum;
  }

  /**
   * Set amount of human
   * @param skeletonNum
   */
  public void setSkeletonNum(int skeletonNum) {
    this.skeletonNum = skeletonNum;
  }

  /**
   * Get the array of skeleton key points
   * @return array of skeleton key points
   */
  public Skeleton[] getSkeletons() {
    if(skeletons == null)
      return new Skeleton[0];
    return skeletons;
  }

  @Override
  public String toString() {
    return "BefSkeletonInfo{" +
            "skeletons=" + Arrays.toString(skeletons) +
            ", skeletonNum=" + skeletonNum +
            '}';
  }

  /**
   * Key points data of Individual skeleton
   */
  public static class Skeleton
  {
    int id;
    int orientation;
    SkeletonPoint[] keypoints;
    BefFaceInfo.FaceRect skeletonRect;

    public SkeletonPoint[] getKeypoints() {
      if(keypoints == null)
        return new SkeletonPoint[0];
      return keypoints;
    }

    public int getId() {
      return id;
    }

    public int getOrientation() {
      return orientation;
    }

    public BefFaceInfo.FaceRect getSkeletonRect() {
      return skeletonRect;
    }

    @Override
    public String toString() {
      return "Skeleton{" +
              "keypoints=" + Arrays.toString(keypoints) +
              ", skeletonRect=" + skeletonRect +
              '}';
    }
  }

  public static class SkeletonPoint
  {
    float x;
    float y;
    boolean is_detect;
    float score;


    public SkeletonPoint(float x, float y, boolean is_detect, float score)
    {
      this.x = x;
      this.y = y;
      this.is_detect = is_detect;
      this.score = score;
    }

    public void setIs_detect(boolean is_detect) {
      this.is_detect = is_detect;
    }

    public boolean isDetect() {
      return is_detect;
    }

    public float getX() {
      return x;
    }

    public void setX(float x) {
      this.x = x;
    }

    public float getY() {
      return y;
    }

    public void setY(float y) {
      this.y = y;
    }

    public PointF asPoint() {
      return new PointF(x, y);
    }

    public float getScore() { return score; }

    @Override
    public String toString() {
      return "FacePoint{" +
          "x=" + x +
          ", y=" + y +
          ", isdetect=" + String.valueOf(is_detect) +
          '}';
    }
  }

}
```


**Return value:** 

If the request is successful, the BefBachSkeletonInfo class is returned with the detected skeleton keypoints.

<span id="4. Release the Handle for the Skeleton Keypoint Algorithm"></span>
## 4. Release the Handle for the Skeleton Keypoint Algorithm

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
