---
title: "AvaBoost "
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-avaboost-"
---

AvaBoost is an algorithm for facial expression driving, which can output [52\-dimensional expression coefficients] and [face pose matrix] under ARKit system. The algorithm requires an input resolution of 360x640 or higher.

This algorithm is a new algorithm added in V4.5.0.

<span id="f29b0e99"></span>
# Technical specifications


|**Category** |**Supported Formats** |
|---|---|
|Platform |* Android<br><br>* iOS |
|Input formats |RGBA8888、BGRA8888 |
|Memory usage |<23M (test processor: Qualcomm 660 OPPO R11) |
|Detected speed |<37ms (test processor: Qualcomm 660 OPPO R11) |


<span id="ad259974"></span>
# C APIs

Detailed interface description can check header file : bef_effect_ai_avaboost.h

<span id="788f3fa2"></span>
## 1. Create avaboost algorithm handle

```C
BEF_SDK_API
bef_effect_result_t bef_effect_ai_avaboost_create(bef_effect_handle_t *handle);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t \* |Avaboost handle created. |


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned. For details, refer to bef_effect_ai_public_define.h.

<span id="73a43b6e"></span>
## 2. Initializing the avaboost algorithm Handle

```C
BEF_SDK_API
bef_effect_result_t bef_effect_ai_avaboost_init(bef_effect_handle_t handle, const char *modelPath);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |Avaboost handle created. |
|modelPath |const char\* |Avaboost model path |


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned. For details, refer to bef_effect_ai_public_define.h.

<span id="c3fafb53"></span>
## 3. Avaboost algorithm detection

```C
BEF_SDK_API
bef_effect_result_t bef_effect_ai_avaboost_detect(
                  bef_effect_handle_t handle,
                  const unsigned char *image,
                  bef_ai_pixel_format pixel_format,
                  int image_width,
                  int image_height,
                  int image_stride,
                  bef_ai_rotate_type orientation,
                  bef_ai_avaboost_ret* result
);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |Avaboost handle created. |
|image |const unsigned char\* |Input image buffer |
|pixel_format |bef_ai_pixel_format |Input image format |
|image_width |int |Input image width |
|image_height |int |Input image height |
|image_stride |int |Number of input image channels |
|orientation |bef_ai_rotate_type |If the input image is rotated or not. The image is considered not to be rotated when the face is positive |
|result |bef_ai_avaboost_ret\* | |


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned. For details, refer to bef_effect_ai_public_define.h.

<span id="bc42a8d5"></span>
## 4. Avaboost algorithm authorization

```C
/**
 * @brief avaboost授权
 * @param [in] handle Created avaboost handle
 * @param [in] license 
 * @param [in] length  
 * @return If succeed return BEF_RESULT_SUC, other value please refer bef_effect_ai_public_define.h
 */
BEF_SDK_API
bef_effect_result_t bef_effect_ai_avaboost_check_license(bef_effect_handle_t handle, const char *licensePath);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |Avaboost handle created. |
|licensePath |const char\* |Avaboost license path |


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned. For details, refer to bef_effect_ai_public_define.h.

<span id="878aa196"></span>
## 5. Release algorithm handle

```C
BEF_SDK_API
bef_effect_result_t bef_effect_ai_avaboost_release(bef_effect_handle_t handle);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t \* |Avaboost handle created. |


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned. For details, refer to bef_effect_ai_public_define.h.

<span id="b5ed6ec9"></span>
## The expression coefficients output by the algorithm correspond to the blendshape

```Plain
['eyeLookDown_L', 'noseSneer_L', 'eyeLookIn_L', 'browInnerUp', 'eyeSquint_L', 'mouthClose', 'mouthLowerDown_R', 'jawOpen', 'mouthShrugLower', 'mouthLowerDown_L', 'mouthFunnel', 'eyeLookIn_R', 'eyeLookDown_R', 'noseSneer_R', 'mouthRollUpper', 'jawRight', 'mouthDimple_L', 'mouthRollLower', 'mouthSmile_L', 'mouthPress_L', 'mouthSmile_R', 'mouthPress_R', 'mouthDimple_R', 'mouthLeft', 'browDown_R', 'browDown_L', 'mouthFrown_L', 'eyeBlink_L', 'cheekSquint_L', 'browOuterUp_L', 'eyeLookUp_L', 'jawLeft', 'mouthStretch_L', 'mouthStretch_R', 'mouthPucker', 'eyeLookUp_R', 'browOuterUp_R', 'cheekSquint_R', 'eyeBlink_R', 'mouthUpperUp_L', 'mouthFrown_R', 'eyeSquint_R', 'jawForward', 'mouthUpperUp_R', 'cheekPuff', 'eyeLookOut_L', 'eyeLookOut_R', 'eyeWide_R', 'mouthRight', 'eyeWide_L', 'mouthShrugUpper', 'tongueOut']
```


<span id="b564f7aa"></span>
# Java APIs

Detailed interface description can check class: com.effectsar.labcv.effectsdk.AvaBoost.java

<span id="90f2a1d5"></span>
## 1. Initializing the algorithm Handle

```Java
public int init(Context context, String modelPath, String licensePath, boolean onlineLicense)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|context |Context |Context. |
|modelPath |String |Path of the model file. |
|licensePath |String |Path of license file. |
|onlineLicense |boolean |If the online license or not. Usually not use online license |


**Return value:** 

If the request is successful, "BEF_RESULT_SUC" is returned; otherwise, an error code is returned. For details, refer to BytedEffectConstants.BytedResultCode.

<span id="25062be3"></span>
## 2. Avaboost algorithm detection

```Java
public BefAvaBoostInfo detect(ByteBuffer buffer, 
                            EffectsSDKEffectConstants.PixlFormat pixelFormat, 
                            int imageWidth, 
                            int imageHeight, 
                            int imageStride, 
                             orientation)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|buffer |ByteBuffer |Input buffer |
|pixelFormat |EffectsSDKEffectConstants.PixlFormat |Input image format |
|imageWidth |int |Input image width |
|imageHeight |int |Input image height |
|imageStride |int |Number of input image channels |
|orientation |EffectsSDKEffectConstants.Rotation |If the input image is rotated or not. The image is considered not to be rotated when the face is positive |


**Return value:** 

Return the algorithm result `BefAvaBoostInfo` object, about `BefAvaBoostInfo` can refer to com.effectsar.labcv.effectsdk.AvaBoost.java, and its definition is consistent with the C interface bef_ai_avaboost_ret.

<span id="98245727"></span>
## 3. Release algorithm handle

```Java
public void release()
```


<span id="0dbd7765"></span>
# FAQ

<span id="3b1a9d08"></span>
### Which logs should I check when an exception occurs?

You are recommended to check the error type logs output with the following tags:


* **bef_effect_ai**

* **SMASH_E_LOG**

* **EffectSDK**


And then you can conduct detailed troubleshooting via description and solution suggested in [Error Code Table](https://byteplus-docs.readme.io/effects/docs/error-code-table).
