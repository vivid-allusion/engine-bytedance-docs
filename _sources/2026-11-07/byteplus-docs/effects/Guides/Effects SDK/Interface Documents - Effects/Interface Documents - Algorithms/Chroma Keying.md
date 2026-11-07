---
title: "Chroma Keying"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-chroma-keying"
---

The chroma keying SDK identifies green screens and green backgrounds for chroma keying.

<span id="Technical Specifications"></span>
# Technical Specifications


|**Category** |**Supported Formats** |
|---|---|
|Platforms |* Android<br><br>* iOS |
|Input formats |* RGBA8888<br><br>* BGRA8888<br><br>* BGR888<br><br>* RGB888 |
|Memory usage |< 42 MB (test device: Oppo R11) |
|Time consumption |< 68 ms (test device: Oppo R11) |


<span id="C API"></span>
# C API

For details about the API, refer to the bef_effect_ai_chroma_keying.h header file.

<span id="1. Create a Handle for the Chroma Keying Algorithm"></span>
## 1. Create a Handle for the Chroma Keying Algorithm

```C
BEF_SDK_API bef_effect_result_t  
bef_effect_ai_chroma_keying_create(bef_effect_handle_t *handle);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The created handle for the chroma keying algorithm. |


**Return value:** 

If the request is successful, BEF_RESULT_SUC is returned. If the request fails, an error code is returned. For details, refer to the bef_effect_ai_public_define.h file.

<span id="2. Initialize the Model Parameters from the Model File"></span>
## 2. Initialize the Model Parameters from the Model File

```C
BEF_SDK_API bef_effect_result_t  
bef_effect_ai_chroma_keying_init(
    bef_effect_handle_t handle,  
    const char* model_path = "");  //This version cannot set model path. please set it to null
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The handle for the chroma keying algorithm. |
|model_path |const char\* |The path to the folder where the model file is located. |


**Return value:** 

If the request is successful, BEF_RESULT_SUC is returned. If the request fails, an error code is returned. For details, refer to the bef_effect_ai_public_define.h file.

<span id="3. Set SDK Parameters"></span>
## 3. Set SDK Parameters

```C
//  Set interface parameters of the float type.
BEF_SDK_API bef_effect_result_t
bef_effect_ai_chroma_keying_set_paramF(
    bef_effect_handle_t handle,
    bef_ai_chroma_keying_param_type type,
    float value);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The handle for the chroma keying algorithm. |
|type |bef_ai_chroma_keying_param_type |The type of the chroma keying parameter. |
|value |float |The value of the chroma keying parameter. |


**Return value:** 

If the request is successful, BEF_RESULT_SUC is returned. If the request fails, an error code is returned. For details, refer to the bef_effect_ai_public_define.h file.

```C
// Set interface parameters of the int type.
BEF_SDK_API bef_effect_result_t
bef_effect_ai_chroma_keying_set_paramI(
    bef_effect_handle_t handle,
    bef_ai_chroma_keying_param_type type,
    int value);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The handle for the chroma keying algorithm. |
|type |bef_ai_chroma_keying_param_type |The type of the chroma keying parameter. |
|value |int |The value of the chroma keying parameter. |


**Return value:** 

If the request is successful, BEF_RESULT_SUC is returned. If the request fails, an error code is returned. For details, refer to the bef_effect_ai_public_define.h file.

**V4.5.0 added new parameter**

```C
// Only V4.5.0 and later version have this parameter
BEF_SDK_API
void bef_effect_ai_chroma_keying_set_processParam(float similar, float smoothness, float correction, float clip_black, float clip_white);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|similar |float |Similarity (influences the intensity of chroma keying, usually only recommend changing this parameter) |
|smoothness |float |Smoothness. With the similar parameter, affecting transitional states such as translucency |
|correction |float |Intensity for excepting green |
|clip_black |float |Do a black and white truncated curve enhancement of the final result mask |
|clip_white |float |Do a black and white truncated curve enhancement of the final result mask |


**Return value:** 

If the request is successful, BEF_RESULT_SUC is returned. If the request fails, an error code is returned. For details, refer to the bef_effect_ai_public_define.h file.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For details about bef_ai_chroma_keying_param_type, refer to the bef_effect_ai_chroma_keying.h file.</div>


```C
/**
 * @brief Parameter Enumeration
 *
 */
typedef enum {
    BEF_AI_CHROMA_KEYING_METHOD = 0,    // The algorithm key. The value is of the int type.
                                        // Valid values: 0: real-time scheme for the mobile client. This is the default value and is recommended.
                                        //         1: scheme for the server
    BEF_AI_CHROMA_KEYING_CAL_COLOR = 1, // The key for background color calculation. The value is of the int type.
                                        // Valid values: 0: Automatically extract the main color of the entire image.
                                        //         1: Extract the main color accurately on a green screen. This is the default value
                                        //         2: Manually extract the main color. Note: If you use this value, the manually configured background color is returned.
    BEF_AI_CHROMA_KEYING_BG_R = 2,      // // Configure the background color as red. The value is of the int type. Value range: 0 to 255. Default value: 0. 
    BEF_AI_CHROMA_KEYING_BG_G = 3,      // // Configure the background color as green. The value is of the int type. Value range: 0 to 255. Default value: 255. 
    BEF_AI_CHROMA_KEYING_BG_B = 4,      // // Configure the background color as blue. The value is of the int type. Value range: 0 to 255. Default value: 0. 
    BEF_AI_CHROMA_KEYING_BALP = 5,      // adjust intensity，float。
                                        // // Configure the color range. Case 1: If the value is smaller than 0, the color range is automatically adjusted. This case is recommended if chroma_keying_cal_color is set to 1. For example, use the default value of -1.
                                        //            Case 2: If the value ranges from 0 to 1, the color range is manually configured. If chroma_keying_cal_color is set to 2, we recommend that you set the value to 0.6 to 0.7.
    BEF_AI_CHROMA_KEYING_KALP = 6,      // Adjust the strength, which is a sharpness parameter of the float type. Recommended value: 0.15. We recommend that you do not adjust this parameter.
    BEF_AI_CHROMA_KEYING_SMOOTH = 7,    // Configure the smoothing coefficient. The value is of the float type. 
                                        // Case 1: If the value is smaller than 0, no smoothing is enabled. 
                                        // Case 2: If the value is 0, only mask time series smoothing is enabled, and time series smoothing is disabled for color estimation. The value of 0 is recommended. 
                                        // Case 3: If the value ranges from 0 to 1, mask time series smoothing is enabled. The parameter indicates the smoothing strength for background color estimation. The maximum value is limited to 1 in the algorithm.
    BEF_AI_CHROMA_KEYING_SHARPEN = 8,   // mask edge sharpen key，int。
                                        // If the value is smaller than or equal to 0, edge sharpening is disabled. 
                                        //         If the value is greater than or equal to 1, edge sharpening is enabled. Recommended value: 1
    BEF_AI_CHROMA_KEYING_GET_MASK = 9,  // Calculate and return the mask. The value is of the int type. 
                                        // If the value is smaller than or equal to 0, no mask is returned, and only the background color estimate is returned. 
                                        //        f the value is greater than or equal to 1, the mask is calculated, and the background color estimate and value are returned. Default value: 1
} bef_ai_chroma_keying_param_type;
```


<span id="4. Perform Chroma Keying"></span>
## 4. Perform Chroma Keying

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_chroma_keying_detect(
    bef_effect_handle_t handle,
    const unsigned char *image,
    bef_ai_pixel_format pixel_format,
    int image_width,
    int image_height,
    int image_stride,
    bef_ai_rotate_type orientation,
    bef_ai_chroma_keying_ret *result,
    bool soft_process); // V4.5.0 added new excepting green process
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The handle for the chroma keying algorithm. |
|image |const unsigned char\* |The size of the input image. |
|pixel_format |bef_ai_pixel_format |The format of the input image. |
|image_width |int |The width of the input image. |
|image_height |int |The height of the input image. |
|image_stride |int |The stride of the input image. |
|orientation |bef_ai_rotate_type |The rotation angle of the input image. |
|result |bef_ai_chroma_keying_ret\* |The return result after algorithm processing. |
|soft_process |bool |Whether to retain the original screen green, for weak de\-greening, V450 added |


**Return value:** 

If the request is successful, BEF_RESULT_SUC is returned. If the request fails, an error code is returned. For details, refer to the bef_effect_ai_public_define.h file.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For details about bef_ai_chroma_keying_ret, refer to the bef_effect_ai_chroma_keying.h file.</div>


The output result of **Version 4.4.0 and higher than 4.4.0**:

```C
/**
 * @brief The output result
 *
 */
typedef struct
{
    int width;             // Return the width
    int height;            // Return the height
    unsigned char color_b; // The background color is identified as blue
    unsigned char color_g; // The background color is identified as green
    unsigned char color_r; // The background color is identified as red
    int outputTexture; // The output texture rgb is the original size texture, alpha channel is the blending factor of the original and target image
} bef_ai_chroma_keying_ret;
```


The output result of **Version lower than 4.4.0**:

```C
/**
 * @brief The output result
 *
 */
typedef struct
{
    int width;             // Return the mask width. 
    int height;            //  Return the mask height.
    unsigned char color_b; // The background color is identified as blue.
    unsigned char color_g; // The background color is identified as green.
    unsigned char color_r; // The background color is identified as red.
    uint8_t* mask;         // The mask data for chroma keying
} bef_ai_chroma_keying_ret;
```


<span id="5. Release the Handle for the Chroma Keying Algorithm"></span>
## 5. Release the Handle for the Chroma Keying Algorithm

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_chroma_keying_release(bef_effect_handle_t handle);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The handle for the chroma keying algorithm. |


**Return value:** 

If the request is successful, BEF_RESULT_SUC is returned. If the request fails, an error code is returned. For details, refer to the bef_effect_ai_public_define.h file.

<span id="6. Configure a License for Chroma Keying"></span>
## 6. Configure a License for Chroma Keying

```C
// offline license 
BEF_SDK_API bef_effect_result_t
bef_effect_ai_chroma_keying_check_license(
    bef_effect_handle_t handle,
    const char *licensePath);

// online license
BEF_SDK_API bef_effect_result_t
bef_effect_ai_chroma_keying_check_online_license(
    bef_effect_handle_t handle,
    const char *licensePath);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The handle for the chroma keying algorithm. |
|licensePath |const char \* |The string of the license file. |


**Return value:** 

If the request is successful, BEF_RESULT_SUC is returned. If the request fails, an error code is returned. For details, refer to the bef_effect_ai_public_define.h file.

<span id="Java API"></span>
# Java API

**API Description**

For details about the API, refer to the com.bytedance.labcv.effectsdk.ChromaKeying.java file.

<span id="1. Initialize the Handle for the Chroma Keying Algorithm"></span>
## 1. Initialize the Handle for the Chroma Keying Algorithm

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
// Set interface parameters of the float type. 
public int setParamF(
    BytedEffectConstants.ChromaKeyingParamType paramType,
    float value)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|paramType |BytedEffectConstants.ChromaKeyingParamType |The type of the input parameter. |
|value |float |The value of the input parameter. |


```Java
// Set interface parameters of the int type.
public int setParamI(
    BytedEffectConstants.ChromaKeyingParamType paramType,
    int value)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|paramType |BytedEffectConstants.ChromaKeyingParamType |The type of the input parameter. |
|value |int |The value of the input parameter. |


**Return value:** 

If the request is successful, BEF_RESULT_SUC is returned. If the request fails, an error code is returned.

**V4.5.0 added new parameter**

```Java
// Only V4.5.0 and later version have this parameter
public int setProcessParam(float similar, float smoothness, float correction, float clip_black, float clip_white)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|similar |float |Similarity (influences the intensity of chroma keying, usually only recommend changing this parameter) |
|smoothness |float |Smoothness. With the similar parameter, affecting transitional states such as translucency |
|correction |float |Intensity for excepting green |
|clip_black |float |Do a black and white truncated curve enhancement of the final result mask |
|clip_white |float |Do a black and white truncated curve enhancement of the final result mask |


**Return value:** 

If the request is successful, BEF_RESULT_SUC is returned. If the request fails, an error code is returned. For details, refer to the bef_effect_ai_public_define.h file.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For details about BytedEffectConstants.ChromaKeyingParamType, refer to the com.bytedance.labcv.effectsdk.BytedEffectConstants.java file. The definition of BytedEffectConstants.ChromaKeyingParamType is the same as that of bef_ai_chroma_keying_param_type in C API.</div>


<span id="3. Perform Chroma Keying"></span>
## 3. Perform Chroma Keying

```Java
public BefChromaKeyingInfo detect(
    ByteBuffer buffer,
    BytedEffectConstants.PixlFormat pixelFormat,
    int imageWidth,
    int imageHeight,
    int imageStride,
    BytedEffectConstants.Rotation orientation,
    boolean soft_process) //V4.5.0 added excepting green process
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
|soft_process |boolean |Whether to retain the original screen green, for weak de\-greening, V450 added |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For details about the BefChromaKeyingInfo class, refer to the com.bytedance.labcv.effectsdk.BefChromaKeyingInfo.java file. The definition of BefChromaKeyingInfo is the same as that of bef_ai_chroma_keying_ret in C API.</div>


The output result of **Version 4.4.0 and higher than 4.4.0**:

```Java
/** * The chroma keying result.  /**
public class BefChromaKeyingInfo {
    private int width;
    private int height;
    private byte color_b;
    private byte color_g;
    private byte color_r;
    private int outputTexture;  // The output texture rgb is the original size texture, alpha channel is the blending factor of the original and target image

    public byte getColor_b() {
        return color_b;
    }

    public byte getColor_g() {
        return color_g;
    }

    public byte getColor_r() {
        return color_r;
    }

    public int getWidth() {
        return width;
    }

    public int getHeight() {
        return height;
    }

    public int getOutputTexture() {  
            return outputTexture;  
    }

    @Override
    public String toString() {
        return String.format("l: %d w:%d, h:%d", mask.length, width, height);
    }
}
```


The output result of **Version lower than 4.4.0**:

```Java
/** * The chroma keying result.  /**
public class BefChromaKeyingInfo {
    private int width;
    private int height;
    private byte color_b;
    private byte color_g;
    private byte color_r;
    private byte[] mask;

    public byte getColor_b() {
        return color_b;
    }

    public byte getColor_g() {
        return color_g;
    }

    public byte getColor_r() {
        return color_r;
    }

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

If the request is successful, the BefChromaKeyingInfo class is returned with the chroma keying result.

<span id="4. Release the Handle for the Chroma Keying Algorithm"></span>
## 4. Release the Handle for the Chroma Keying Algorithm

```Java
public void release()
```


<span id="FAQ"></span>
## FAQ

<span id="1. Q: What logs do I need to check if an exception occurs?"></span>
### 1. Q: What logs do I need to check if an exception occurs?

A. We recommend that you check for the error logs with the following tags:


* **bef_effect_ai**

* **SMASH_E_LOG**

* **EffectSDK**


<span id="Error Codes"></span>
## Error Codes

For details about the error codes, refer to [Error Codes](https://docs.byteplus.com/99783).
