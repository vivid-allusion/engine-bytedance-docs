---
title: "Skin Segmentation"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-skin-segmentation"
---

The skin segmentation SDK recognizes and segments human skin areas. It is different from the facial segmentation and full\-body segmentation SDKs.

<span id="Technical Specifications"></span>
# Technical Specifications


|**Category** |**Supported Formats** |
|---|---|
|Platforms |* Android<br><br>* iOS |
|Input formats |* RGBA8888<br><br>* BGRA8888<br><br>* BGR888<br><br>* RGB888 |
|Memory usage |< 6 MB (test device: Oppo R11) |
|Time consumption |< 17 ms (test device: Oppo R11) |


<span id="C API"></span>
# C API

For details about the API, refer to the bef_effect_ai_skin_segmentation.h header file.

<span id="1. Create a Handle for the Skin Segmentation Algorithm"></span>
## 1. Create a Handle for the Skin Segmentation Algorithm

```C
BEF_SDK_API bef_effect_result_t  
bef_effect_ai_skin_segmentation_create(bef_effect_handle_t *handle);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The created handle for the skin segmentation algorithm. |


**Return value:** 

If the request is successful, BEF_RESULT_SUC is returned. If the request fails, an error code is returned. For details, refer to the bef_effect_ai_public_define.h file.

<span id="2. Initialize the Model Parameters from the Model File"></span>
## 2. Initialize the Model Parameters from the Model File

```C
BEF_SDK_API bef_effect_result_t  
bef_effect_ai_skin_segmentation_init(
    bef_effect_handle_t handle,  
    const char* model_path);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The handle for the skin segmentation algorithm. |
|model_path |const char\* |The path to the folder where the model file is located. |


**Return value:** 

If the request is successful, BEF_RESULT_SUC is returned. If the request fails, an error code is returned. For details, refer to the bef_effect_ai_public_define.h file.

<span id="3. Set SDK Parameters"></span>
## 3. Set SDK Parameters

```C
// Set interface parameters of the const char * type. 
BEF_SDK_API bef_effect_result_t
bef_effect_ai_skin_segmentation_set_paramF(
    bef_effect_handle_t handle,
    bef_ai_skin_segmentation_param_type type,
    const char* value);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The handle for the skin segmentation algorithm. |
|type |bef_ai_skin_segmentation_param_type |The type of the skin segmentation parameter. |
|value |const char\* |The value of the skin segmentation parameter. |


**Return value:** 

If the request is successful, BEF_RESULT_SUC is returned. If the request fails, an error code is returned. For details, refer to the bef_effect_ai_public_define.h file.

```C
// Set interface parameters of the int type. 
BEF_SDK_API bef_effect_result_t
bef_effect_ai_skin_segmentation_set_paramI(
    bef_effect_handle_t handle,
    bef_ai_skin_segmentation_param_type type,
    int value);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The handle for the skin segmentation algorithm. |
|type |bef_ai_skin_segmentation_param_type |The type of the skin segmentation parameter. |
|value |int |The value of the skin segmentation parameter. |


**Return value:** 

If the request is successful, BEF_RESULT_SUC is returned. If the request fails, an error code is returned. For details, refer to the bef_effect_ai_public_define.h file.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For details about bef_ai_skin_segmentation_param_type, refer to the bef_effect_ai_skin_segmentation.h file.</div>


```C
/**
 * @brief  The model parameter type. 
 *
 */
typedef enum {
    BEF_AI_SKIN_SEG_MODEL_KEY = 0,     // Set the key of the skin segmentation model. The default value is tt_skin_seg. The value of the string type.
    BEF_AI_SKIN_SEG_IS_NEED_FACE = 1,  // Specify whether to load a face model to remove the facial skin. The value is of the int type.
} bef_ai_skin_segmentation_param_type;
```


<span id="4. Perform Skin Segmentation"></span>
## 4. Perform Skin Segmentation

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_skin_segmentation_detect(
    bef_effect_handle_t handle,
    const unsigned char *image,
    bef_ai_pixel_format pixel_format,
    int image_width,
    int image_height,
    int image_stride,
    bef_ai_rotate_type orientation,
    bef_ai_skin_segmentation_ret *result);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The handle for the skin segmentation algorithm. |
|image |const unsigned char\* |The size of the input image. |
|pixel_format |bef_ai_pixel_format |The format of the input image. |
|image_width |int |The width of the input image. |
|image_height |int |The height of the input image. |
|image_stride |int |The stride of the input image. |
|orientation |bef_ai_rotate_type |The rotation angle of the input image. |
|result |bef_ai_skin_segmentation_ret\* |The return result after algorithm processing. |


**Return value:** 

If the request is successful, BEF_RESULT_SUC is returned. If the request fails, an error code is returned. For details, refer to the bef_effect_ai_public_define.h file.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For details about bef_ai_skin_segmentation_ret, refer to the bef_effect_ai_skin_segmentation.h file.</div>


```C
/** * @brief The output result. /**

typedef struct
{
    int width;             // returned mask width
    int height;            // returned mask height
    uint8_t* mask;         // data for mask of skin segmentation
} bef_ai_skin_segmentation_ret;
```


<span id="5. Release the Handle for the Skin Segmentation Algorithm"></span>
## 5. Release the Handle for the Skin Segmentation Algorithm

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_skin_segmentation_release(bef_effect_handle_t handle);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The handle for the skin segmentation algorithm. |


**Return value:** 

If the request is successful, BEF_RESULT_SUC is returned. If the request fails, an error code is returned. For details, refer to the bef_effect_ai_public_define.h file.

<span id="6. Configure a License for Skin Segmentation"></span>
## 6. Configure a License for Skin Segmentation

```C
// offline license
BEF_SDK_API bef_effect_result_t
bef_effect_ai_skin_segmentation_check_license(
    bef_effect_handle_t handle,
    const char *licensePath);

// online liecense
BEF_SDK_API bef_effect_result_t
bef_effect_ai_skin_segmentation_check_online_license(
    bef_effect_handle_t handle,
    const char *licensePath);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The handle for the skin segmentation algorithm. |
|licensePath |const char \* |The string of the license file. |


**Return value:** 

If the request is successful, BEF_RESULT_SUC is returned. If the request fails, an error code is returned. For details, refer to the bef_effect_ai_public_define.h file.

<span id="Java API"></span>
# Java API

**API Description**

For details about the API, refer to the com.bytedance.labcv.effectsdk.SkinSegmentation.java file.

<span id="1. Initialize the Handle for the Skin Segmentation Algorithm"></span>
## 1. Initialize the Handle for the Skin Segmentation Algorithm

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
// Set interface parameters of the string type.
public int setParamF(
    BytedEffectConstants.SkinSegmentationParamType paramType,
    String value)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|paramType |BytedEffectConstants.SkinSegmentationParamType |The type of the input parameter. |
|value |String |The value of the input parameter. |


```Java
// Set interface parameters of the int type
public int setParamI(
    BytedEffectConstants.SkinSegmentationParamType paramType,
    int value)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|paramType |BytedEffectConstants.SkinSegmentationParamType |The type of the input parameter. |
|value |int |The value of the input parameter. |


**Return value:** 

If the request is successful, BEF_RESULT_SUC is returned. If the request fails, an error code is returned.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For details about BytedEffectConstants.SkinSegmentationParamType, refer to the com.bytedance.labcv.effectsdk.BytedEffectConstants.java file. The definition of BytedEffectConstants.SkinSegmentationParamType is the same as that of bef_ai_skin_segmentation_param_type in C API.</div>


<span id="3. Perform Skin Segmentation"></span>
## 3. Perform Skin Segmentation

```Java
public BefSkinSegInfo detect(
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


<div data-tips="true" data-tips-type="warning">For details about the BefSkinSegInfo class, refer to the com.bytedance.labcv.effectsdk.BefSkinSegInfo.java file. The definition of BefSkinSegInfo is the same as that of bef_ai_skin_segmentation_ret in C API.</div>


```Java
/** * The result of the skin segmentation algorithm. /**
public class BefSkinSegInfo {
    private int width;
    private int height;
    private byte[] mask;

    public byte[] getMask() {
        return mask;
    }

    public int getWidth() {
        return width;
    }

    public int getHeight() {
        return height;
    }

    @Override
    public String toString() {
        return String.format("l: %d w:%d, h:%d", mask.length, width, height);
    }
}
```


**Return value:** 

If the request is successful, the BefSkinSegInfo class is returned with the skin segmentation result.

<span id="4. Release the Handle for the Skin Segmentation Algorithm"></span>
## 4. Release the Handle for the Skin Segmentation Algorithm

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
