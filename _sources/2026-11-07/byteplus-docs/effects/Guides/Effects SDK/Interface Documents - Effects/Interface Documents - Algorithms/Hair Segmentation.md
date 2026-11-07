---
title: "Hair Segmentation"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-hair-segmentation"
---

The hair segmentation SDK is used to extract hair outlines from an image in real\-time. This stable, low\-consumption and fast SDK supports the simultaneous segmentation of multiple people and is often used in hair dying effects.

<span id="Technical Specifications"></span>
# Technical Specifications


|**Category** |**Supported Formats** |
|---|---|
|Platform |* Android<br><br>* iOS<br><br>* Windows<br><br>* Mac |
|Input format |* RGBA8888<br><br>* BGRA8888<br><br>* BGR888<br><br>* RGB888<br><br>* NV21<br><br>* NV12<br><br>* YUV420P |
|Minimum input size |Short side 128 |
|Memory usage |< 3M (test device: OppoR11) |
|Detected speed |<7ms (test device iPhone7) |


<span id="6ae2606d"></span>
# C Interface Description

For detailed interface description, view header file: bef_effect_ai_hairparser.h

<span id="1. Create A Hair Segmentation Handle"></span>
## 1. Create A Hair Segmentation Handle

```C
BEF_SDK_API bef_effect_result_t  
bef_effect_ai_hairparser_create(bef_effect_handle_t *handle);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The detection handle created for hair segmentation. |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more information, refer to bef_effect_ai_public_define.h.

<span id="2. Initialize Model Parameters from Files"></span>
## 2. Initialize Model Parameters from Files

```C
BEF_SDK_API bef_effect_result_t  
bef_effect_ai_hairparser_init_model(
    bef_effect_handle_t handle,  
    const char* param_path);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The detection handle for hair segmentation. |
|param_path |const char\* |The path of the model file. |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more information, refer to bef_effect_ai_public_define.h.

<span id="3. SDK Parameter Setting"></span>
## 3. SDK Parameter Setting

```C
BEF_SDK_API bef_effect_result_t  
bef_effect_ai_hairparser_set_param(
    bef_effect_handle_t handle,  
    int net_input_width,  
    int net_input_height,
    bool use_tracking,
    bool use_blur);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The detection handle for hair segmentation. |
|net_input_width |int |The width passed by the neural network: HairParser 128. |
|net_input_height |int |The height passed by the neural network: HairParser 224. |
|use_tracking |bool |Input "true" for the internal algorithm parameter. |
|use_blur |bool |Input "true" for the internal algorithm parameter. |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more information, refer to bef_effect_ai_public_define.h.

<span id="4. Get The Output Shape"></span>
## 4. Get The Output Shape

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_hairparser_get_output_shape(
    bef_effect_handle_t handle,
    int* output_width,
    int* output_height,
    int* channel);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The detection handle for hair segmentation. |
|output_width |int\* |The width output by the neural network: HairParser. |
|output_height |int\* |The height output by the neural network: HairParser. |
|channel |int\* |Currently, the neural network only output 1 as the result. |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Channel is the number of return channels. Currently, it only returns 1 which will be expanded in the future.</div>


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more information, refer to bef_effect_ai_public_define.h.

<span id="5. Segmentation"></span>
## 5. Segmentation

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_hairparser_do_detect(
    bef_effect_handle_t handle,
    const unsigned char* src_image_data,
    bef_ai_pixel_format pixel_format,
    int width,
    int height,
    int image_stride,
    bef_ai_rotate_type orient,
    unsigned char* dst_alpha_data,
    bool need_flip_alpha);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The detection handle for hair segmentation. |
|src_image_data |const unsigned char \* |The size of the input image. The image can be any size. |
|pixel_format |bef_ai_pixel_format |The type of the input image. |
|width |int |The width of the input image. |
|height |height |The height of the input image. |
|image_stride |int |The stride of the input image. |
|orient |bef_ai_rotate_type |The rotation angle of the input image. |
|dst_alpha_data |unsigned char\* |The output image. |
|need_flip_alpha |bool |Whether the output image needs to be flipped. |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more information, refer to bef_effect_ai_public_define.h.

<span id="6. Release The Handle"></span>
## 6. Release The Handle

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_hairparser_destroy(bef_effect_handle_t handle);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The detection handle for hair segmentation. |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more information, refer to bef_effect_ai_public_define.h.

<span id="6. Hair Segmentation Authorization"></span>
## 6. Hair Segmentation Authorization

```C
BEF_SDK_API bef_effect_result_t 
bef_effect_ai_hairparser_check_license(
    JNIEnv* env, 
    jobject context, 
    bef_effect_handle_t handle, 
    const char *licensePath);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The detection handle for hair segmentation. |
|licensePath |const char \* |The string of license file. |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more information, refer to bef_effect_ai_public_define.h.

<span id="Java Interface Description"></span>
# Java Interface Description

**Interface Description**

For a detailed interface description, refer to com.bytedance.labcv.effectsdk.HairParser.java

<span id="1. Initialize The Hair Segmentation Handle"></span>
## 1. Initialize The Hair Segmentation Handle

```Java
public int init(
    Context context,
    String modelpath, 
    String licensePath)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|context |Context |Applying context. |
|modelpath |const char \* |The absolute path of the model file. |
|licensePath |const char \* |The absolute path of the license file. |


**Return value:** 

Return BEF_RESULT_SUC when succeed, otherwise the corresponding error code will be returned.

<span id="2. SDK Parameter Setting"></span>
## 2. SDK Parameter Setting

```Java
public int setParam(
    int width,
    int height,
    boolean useTracking,
    boolean useBlur)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|width |int |The width of the input image. |
|height |int |The height of the input image. |
|useTracking |boolean |Whether to track. Input "true". |
|useBlur |boolean |Whether to blur. Input "true". |


**Return value:** 

Return BEF_RESULT_SUC when succeed, otherwise the corresponding error code will be returned.

<span id="3. Hair Segmentation"></span>
## 3. Hair Segmentation

```Java
public HairMask parseHair(
    ByteBuffer imgdata,
    BytedEffectConstants.PixlFormat pixel_format,
    int width,
    int height,
    int stride,
    BytedEffectConstants.Rotation orientation,
    boolean needFlipAlpha)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|imgdata |ByteBuffer |Input the image data. |
|pixel_format |BytedEffectConstants.PixlFormat |Input the data format. |
|width |int |Input image width. |
|height |int |Input the image height. |
|stride |int |Input the image stride. |
|orientation |BytedEffectConstants.Rotation |Input the rotation angle of the image. |
|needFlipAlpha |boolean |Whether the output image needs to be flipped. |


For more details of the HairMask class, refer to com.bytedance.labcv.effectsdk.HairParser.java.

```Java
/** * Hair segmentation result  */ public class HairMask { private int width; private int height; private byte[] buffer; private int channel; public byte[] getBuffer() { return buffer; } public int getWidth() { return width; } public int getHeight() { return height; } @Override public String toString() { return String.format("l: %d w:%d, h:%d", buffer.length, width, height); } } private long mNativePtr; private boolean inited = false;
```


```Java
**Return** When succeed return class HairMask-hair segmentation result  ## 4\.release the hair segmentation handle ```java public void release()
```


<span id="FAQ"></span>
## FAQ

<span id="1. If there are any exceptions, please check whether there are the following types of logs."></span>
### 1. If there are any exceptions, check whether there are the following types of logs.

Answer: Check logs with the following tags:


* **bef_effect_ai**

* **SMASH_E_LOG**

* **EffectSDK**


<span id="2. No effect at all after the hair segmentation."></span>
### 2. No effect at all after the hair segmentation.

Answer: Examine it according to the following steps.


* Make sure that the hair segmentation handle has been initialized successfully.

* Make sure that the hair segmentation handle has been authorized successfully.

* If the initialization is successful, make sure that the image data is complete and the type is supported.


<span id="Error code"></span>
## Error code

Refer to the [error code list](https://docs.byteplus.com/99783).
