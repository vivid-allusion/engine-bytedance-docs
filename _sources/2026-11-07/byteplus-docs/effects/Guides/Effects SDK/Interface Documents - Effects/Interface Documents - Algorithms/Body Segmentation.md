---
title: "Body Segmentation"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-body-segmentation"
---

The body segmentation SDK is used to extract body outlines from an image in real\-time. This stable, low\-consumption and fast SDK supports the simultaneous segmentation of multiple people.

<span id="Technical Specifications"></span>
# Technical Specifications


|**Category** |**Supported Formats** |
|---|---|
|Available platforms |* Android<br><br>* iOS<br><br>* Windows<br><br>* Mac |
|Available input formats |* RGBA8888<br><br>* BGRA8888<br><br>* BGR888<br><br>* RGB888 |
|Minimum input size |Short side 128 |
|Memory usage |< 4M (test device: OppoR11) |
|Speed |<11ms (test device iPhone7) |


<span id="C Interface Description"></span>
# C Interface Description

For detailed interface description, view header file: bef_effect_ai_portrait_matting.h

<span id="1. Create A Body Segmentation Handle"></span>
## 1. Create A Body Segmentation Handle

```C
BEF_SDK_API bef_effect_result_t  
bef_effect_ai_portrait_matting_create(bef_effect_handle_t *handle);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The detection handle created for body segmentation |


**Return value:** 

Returns BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more information, refer to bef_effect_ai_public_define.h

<span id="2. Initialize Model Parameters from Files"></span>
## 2. Initialize Model Parameters from Files

```C
BEF_SDK_API bef_effect_result_t  
bef_effect_ai_portrait_matting_init_model(
    bef_effect_handle_t handle,
    bef_ai_matting_model_type type,
    const char* param_path);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The detection handle for body segmentation. |
|type |bef_ai_matting_model_type |Model type, currently divided into big and small models. |
|param_path |const char\* |The path of the model file. |


**Return value:** 

Returns BEF_RESULT_SUC when succeed, otherwise the corresponding error code will be returned. For more information, refer to bef_effect_ai_public_define.h.

<span id="3.SDK Parameter Setting"></span>
## 3. SDK Parameter Setting

```C
BEF_SDK_API bef_effect_result_t bef_effect_ai_portrait_matting_set_param( bef_effect_handle_t handle, bef_ai_matting_param_type type, int value);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The detection handle for body segmentation. |
|type |bef_ai_matting_param_type |The algorithm parameters used to set the boundary mode, forced prediction and short edge length. |
|value |int |1 by default. |


For more information about bef_ai_matting_param_type, refer to bef_effect_ai_portrait_matting.h.

**It would be better not to modify these set parameters, otherwise there may be effect problems.** 

```C
/* * @brief SDK parameter 
* edge_mode: * Algorithm parameters, used to set the boundary mode  
* - 0: No boundatries 
* - 1: With boundaries 
* - 2: With boundaries. The strategies 2 and 3 are slightly different but with similar effects. Pick anyone you like.  
* fresh_every: 
* Algorithm parameter, used to set the number of forced prediction. 15 is enough. 
* MP_OutputMinSideLen: 
* Return the length of the short side, which needs to be multiples of 16. 128 by default. 
* MP_OutputWidth doesn't have to be set. It is only called before the compliant of GetParam. 
* MP_OutputHeight doesn't have to be set. It is only the interface before the compliant of GetParam. **/ 
enum bef_ai_matting_param_type { 
  BEF_MP_EdgeMode = 0, 
  BEF_MP_FrashEvery = 1, 
  BEF_MP_OutputMinSideLen = 2, 
  BEF_MP_OutputWidth = 3, 
  BEF_MP_OutputHeight = 4, 
};
```


**Return value:** 

Returns BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more information, refer to bef_effect_ai_public_define.h.

<span id="4. Get the Size of the Output Mask"></span>
## 4. Get the Size of the Output Mask

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_portrait_matting_get_output_shape(
    bef_effect_handle_t handle,
    int width,
    int height,
    int *output_width,
    int *output_height);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The detection handle for body segmentation. |
|width |int |The width of the input image. |
|height |int |The height of the input image. |
|output_width |int\* |The width of the output mask. |
|output_height |int\* |The height of the output mask. |


**Return value:** 

Returns BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more information, refer to bef_effect_ai_public_define.h.

<span id="5. Segmentation"></span>
## 5. Segmentation

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_portrait_matting_do_detect(
    bef_effect_handle_t handle,
    const unsigned char* src_image_data,
    bef_ai_pixel_format pixel_format,
    int width,
    int height,
    int image_stride,
    bef_ai_rotate_type orient,
    bool need_flip_alpha,
    bef_ai_matting_ret *ret);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The detection handle for body segmentation. |
|src_image_data |const unsigned char \* |The size of the input image. |
|pixel_format |bef_ai_pixel_format |The type of the input image. |
|width |int |The width of the input image. |
|height |int |The height of the input image. |
|image_stride |int |The stride of the input image |
|orient |bef_ai_rotate_type |The rotation angle of the input image. |
|need_flip_alpha |bool |Whether the output image needs to be flipped. |
|ret |bef_ai_matting_ret\* |The output image. |


**Return value:** 

Returns BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more information, refer to bef_effect_ai_public_define.h.

<span id="6. Release the handle"></span>
## 6. Release the handle

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_portrait_matting_destroy(bef_effect_handle_t handle);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The detection handle for body segmentation. |


**Return value:** 

Returns BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more information, refer to bef_effect_ai_public_define.h.

<span id="6. Body Segmentation License"></span>
## 6. Body Segmentation License

```C
BEF_SDK_API bef_effect_result_t 
bef_effect_ai_portrait_matting_check_license(
    JNIEnv* env, 
    jobject context, 
    bef_effect_handle_t handle, 
    const char *licensePath);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |The detection handle for body segmentation. |
|licensePath |const char \* |The string of license file. |


**Return value:** 

Returns BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more information, refer to bef_effect_ai_public_define.h.

<span id="Java interface description"></span>
# Java interface description

**Interface Description**

For a detailed interface description,refer to com.bytedance.labcv.effectsdk.PortraitMatting.java

<span id="1. Initialize The Body Segmentation Handle"></span>
## 1. Initialize The Body Segmentation Handle

```Java
  public int init(
      Context context, 
      String modelpath, 
      BytedEffectConstants.PortraitMatting modelType, 
      String licensePath)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|context |Context |Applying context. |
|modelpath |String |The absolute path of the model file. |
|modelType |BytedEffectConstants.PortraitMatting |Model type. |
|licensePath |String |The absolute path of the license file. |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">BytedEffectConstants BEF_PORTAITMATTING_LARGE_MODEL(0), Big models require more time than small models; BEF_PORTAITMATTING_SMALL_MODEL(1); Small models are faster;</div>


**Return value:** 

Returns BEF_RESULT_SUC if successful, otherwise the corresponding error code will be returned.

<span id="2. SDK Parameter Setting"></span>
## 2. SDK Parameter Setting

```Java
  public int setParam(
      BytedEffectConstants.PorraitMattingParamType paramType , 
      int paramValue)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|paramType |BytedEffectConstants.PorraitMattingParamType |Parameter type. |
|paramValue |int |Parameter value. |


Refer to BytedEffectConstants.PorraitMattingParamType for more information.

```Java
public enum PorraitMattingParamType { 
  /** 
  * Algorithm parameters, used to set the boundary mode 
  * - 0: No boundatries 
  * - 1: With boundaries 
  * - 2: With boundaries. The strategies 2 and 3 are slightly different but with similar effects. Pick anyone you like. 
  */ 
  BEF_MP_EdgeMode(0), 
  /** 
  * Algorithm parameter, used to set the number of forced prediction. 15 is enough.  
  */ 
  BEF_MP_FrashEvery(1), 
  /** 
  * Return the length of the short side, which needs to be multiples of 16. 128 by default. 
  */ 
  BEF_MP_OutputMinSideLen(2); 
  private int value; 
  PorraitMattingParamType(int v){
    this.value = v;
  } 
  public int getValue(){
    return value;
  } 
}
```


**Return value:** 

Returns BEF_RESULT_SUC if successful, otherwise the corresponding error code will be returned.

<span id="3. Body Segmentation"></span>
## 3. Body Segmentation

```Java
public MattingMask detectMatting( 
        ByteBuffer imgdata, 
        BytedEffectConstants.PixlFormat pixel_format,  
        int width, 
        int height, 
        int stride, 
        BytedEffectConstants.Rotation orientation, 
        boolean needflipalpha
)
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


For more details of the HairMask class, refer to com.bytedance.labcv.effectsdk.PortraitMatting.java

```Java
/**                                                                                                  

-   The result of body segmentation. Gray scale image.

*/
public class MattingMask
{
private int width;
private int height;
private byte[] buffer;

public byte[] getBuffer() {
  return buffer;
}

public int getWidth() {
  return width;
}

public int getHeight()
{
  return height;
}

@Override
public String toString() {
  return String.format("l: %d w:%d, h:%d", buffer.length, width, height);
}

}
```


**Return value:** 

If successful, returns MattingMask\-body segmentation result: Grayscale images

<span id="4.release the body segmentation handle"></span>
## 4.release the body segmentation handle

```Java
public void release()
```


<span id="FAQ"></span>
## FAQ

<span id="1. If there are any exceptions, please check whether there are the following types of logs."></span>
### 1. If there are any exceptions, check whether there are the following types of logs.

Answer: Check logs with the following tags:


* **bef_effect_ai**

* **SMASH_E_LOG**

* **EffectSDK**


<span id="2. No effect at all after the body segmentation."></span>
### 2. No effect at all after the body segmentation.

Answer: Examine it according to the following steps.


* Make sure that the body segmentation handle has been initialized successfully.

* Make sure that the body segmentation handle has been authorized successfully.

* If the initialization is successful, make sure that the image data is complete and the type is supported.


<span id="3. The data definition of mask output by the body segmentation SDK"></span>
### 3. The data definition of mask output by the body segmentation SDK

Answer: The value in the byte[] output by SDK ranges from 0 to 255. 255 represents the body and 0 the background. The values between 0 and 255 represent the edge of the body.
