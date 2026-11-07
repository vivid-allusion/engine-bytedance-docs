---
title: "Vehicle Detection"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-vehicle-detection"
---

Vehicle Detection SDK provides the ability to extract vehicle and license plate information from images in real\-time.

<span id="Technical Specifications"></span>
# Technical Specifications


|**Category** |**Supported Formats** |
|---|---|
|Platforms |* Android<br><br>* iOS<br><br>* Windows<br><br>* Mac |
|Input formats |* RGBA8888<br><br>* BGRA8888<br><br>* BGR888<br><br>* RGB888<br><br>* NV21<br><br>* NV12<br><br>* YUV420P |
|Minimum input size |Short side 128 |
|Memory usage |< 3M (test device: OppoR11) |
|Detected speed |<7ms (test device iPhone7) |


<span id="cad5bfd6"></span>
# C Interface Description

For the detailed interface description, refer to header file: bef_effect_ai_car_detect.h

<span id="1. Create a Vehicle Detection Handle"></span>
## 1. Create a Vehicle Detection Handle

```C
BEF_SDK_API
bef_effect_result_t
bef_effect_ai_car_detect_create_handle(bef_ai_car_handle* handle);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_ai_car_handle |Vehicle detection handle created. |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more information, refer to bef_effect_ai_public_define.h.

<span id="2. Initialize Model Parameters from Files"></span>
## 2. Initialize Model Parameters from Files

```C
BEF_SDK_API
bef_effect_result_t
bef_effect_ai_car_detect_init_model(bef_ai_car_handle handle,
                                           bef_ai_car_model_type modelType,
                                           const char* modelPath);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_ai_car_handle |Vehicle detection handle. |
|modelType |bef_ai_car_model_type |The type of the vehicle detection model. |
|modelPath |const char\* |The path of the model file. |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more information, refer to bef_effect_ai_public_define.h.

<span id="3. SDK Parameter Setting"></span>
## 3. SDK Parameter Setting

```C
BEF_SDK_API
bef_effect_result_t
bef_effect_ai_car_detect_set_paramf(bef_ai_car_handle handle,
                                           bef_ai_car_param_type type,
                                           float value);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_ai_car_handle |Vehicle detection handle. |
|use_tracking |bef_ai_car_param_type |Input "true" for the internal algorithm parameter. |
|use_blur |float |Input "true" for the internal algorithm parameter. |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more information, refer to bef_effect_ai_public_define.h.

<span id="4. Vehicle Detection"></span>
## 4. Vehicle Detection

```C
BEF_SDK_API
bef_effect_result_t
bef_effect_ai_car_detect_detect(bef_ai_car_handle handle,
                                       const unsigned char* image,
                                       bef_ai_pixel_format pixel_format,
                                       int image_width,
                                       int image_height,
                                       int image_stride,
                                       bef_ai_rotate_type orientation,
                                       bef_ai_car_ret* car_info);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_ai_car_handle |Vehicle detection handle. |
|image |const unsigned char\* |The size of the input image. The image can be any size. |
|pixel_format |bef_ai_pixel_format |The type of the input image. |
|image_width |int |The width of the input image. |
|image_height |int |The height of the input image. |
|image_stride |int |The stride of the input image. |
|orientation |bef_ai_rotate_type |The rotation angle of the input image. |
|bef_ai_car_ret |bef_ai_car_ret |Test results. |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more information, refer to bef_effect_ai_public_define.h.

<span id="5. Release the Handle"></span>
## 5. Release the Handle

```C
BEF_SDK_API
bef_effect_result_t bef_effect_ai_car_detect_destroy(bef_ai_car_handle handle);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_ai_car_handle |Vehicle detection handle. |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more information, refer to bef_effect_ai_public_define.h.

<span id="6. Vehicle Detection License"></span>
## 6. Vehicle Detection License

```C
BEF_SDK_API
bef_effect_result_t bef_effect_ai_car_detect_check_license(bef_ai_car_handle handle, const char* licensePath);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_ai_car_handle |Vehicle detection handle. |
|licensePath |const char \* |The string of license file. |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more information, refer to bef_effect_ai_public_define.h.

<span id="Java Interface Description"></span>
# Java Interface Description

**Interface description**

For a detailed interface description, refer to com.bytedance.labcv.effectsdk.CarDetect.java

<span id="1. Initialize the Vehicle Detection Handle"></span>
## 1. Initialize the Vehicle Detection Handle

```Java
public int createHandle(String licensePath);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|licensePath |const char \* |The absolute path of the license file. |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail.

<span id="2. SDK Parameter Setting"></span>
## 2. SDK Parameter Setting

```Java
public int setParam(BytedEffectConstants.CarParamType paramType, float paramValue)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|paramType |BytedEffectConstants.CarParamType |Whether to track. Input "true". |
|paramValue |float |Whether to blur. Input "true". |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail.

<span id="3. Set a Model"></span>
## 3. Set a Model

```Java
public int setModel(BytedEffectConstants.CarModelType modelType, 
                    String modelPath)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|modelType |BytedEffectConstants.CarModelType |Model type. |
|modelPath |String |Model path. |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail.

<span id="4. Vehicle Detection"></span>
## 4. Vehicle Detection

```Java
public BefCarDetectInfo detect(ByteBuffer buffer,
                               BytedEffectConstants.PixlFormat pixel_format,
                               int image_width, 
                               int image_height,
                               int image_stride, 
                               BytedEffectConstants.Rotation orientation)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|buffer |ByteBuffer |Image data. |
|pixel_format |BytedEffectConstants.PixlFormat |Data format. |
|image_width |int |Image width. |
|image_height |int |Image height. |
|image_stride |int |Image stride. |
|orientation |BytedEffectConstants.Rotation |Rotation angle of the image. |


**Return value:** 

Return class BefCarDetectInfo when succeed \- the vehicle detection result.

<span id="5. Release the Vehicle Detection Handle"></span>
## 5. Release the Vehicle Detection Handle

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


<span id="Error code"></span>
## Error code

Refer to the [error code list](https://docs.byteplus.com/99783).
