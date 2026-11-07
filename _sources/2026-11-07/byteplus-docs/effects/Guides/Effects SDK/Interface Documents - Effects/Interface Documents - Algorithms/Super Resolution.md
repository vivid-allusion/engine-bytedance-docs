---
title: "Super Resolution"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-video-superresolution"
---

Superresolution refers to the expansion of width and height by twice on the original basis.

<span id="Technical specifications"></span>
# Technical specifications


|**Category** |**Supported Formats** |
|---|---|
|Platform |* Android<br><br>* iOS |
|Resolution |Currently, the resolution needs to be less than 720p |
|Requirements for iOS |* iOS 11 and above<br><br>* iPhone 7 and above devices |
|Requirements for Android |Qualcomm processors are required (Qualcomm 660 and above) |
|Input formats for iOS |PixelBuffer input, support yuv420p and yuv420f, (future support metal texture) |
|Input formats for Android |Texture Input |
|Detected speed |32ms (test processor: Qualcomm 660 OPPO R11 720p input) |


<span id="C interface description"></span>
# C interface description

To learn more about interfaces, refer to **bef_ai_image_quality_enhancement_video_sr.h**

<span id="1. Create handles for superresolution"></span>
## 1. Create handles for superresolution

```C
/**
 * @brief Create effect handle.
 * @param handle      handle that will be created.
 * @return            If succeed return BEF_EFFECT_RESULT_SUC. For other values, refer to bef_effect_ai_public_define.h.
 */
BEF_SDK_API bef_effect_result_t 
bef_ai_image_quality_enhancement_video_sr_create(bef_image_quality_enhancement_handle* handle, const char* dir);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_image_quality_enhancement_handle |Create handles for superresolution. |
|dir |char\* |Read\-write path for Android to save initialized content. |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more details, refer to bef_effect_ai_public_define.h.

<span id="2. Set attributes"></span>
## 2. Set attributes

```C
/**
 *  set the input property 
 * @param handle
 * @param width Input width of the  buffer or texture
 * @param height Input height of the  buffer or texture
 * @return If succeed return BEF_EFFECT_RESULT_SUC. For other values, refer to bef_effect_ai_public_define.h.
 */
BEF_SDK_API bef_effect_result_t
bef_ai_image_quality_enhancement_video_sr_set_width_and_height(bef_image_quality_enhancement_handle handle, int width , int height);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_image_quality_enhancement_handle |Handles of superresolution. |
|width |int |Width input |
|height |int |Height input. |


<span id="3. Authorize supperresolution for picture quality detection"></span>
## 3. Authorize supperresolution for picture quality detection

```C
/** * @param handle Created effect detect handle * Handle created * @param license_path licese path under the dircetory * AP of license in file system * @param result If succeed return BEF_EFFECT_RESULT_SUC. For other values, refer to bef_effect_ai_public_define.h. * */ BEF_SDK_API bef_effect_result_t bef_ai_image_quality_enhancement_video_sr_check_license(bef_image_quality_enhancement_handle handle, const char* license_path);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_image_quality_enhancement_handle |Handle of picture quality. |
|licensePath |const char \* |The string of license file |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more details, refer to bef_effect_ai_public_define.h.

<span id="4. Authorize supperresolution for picture quality detection"></span>
## 4. Process superresolution for picture quality detection

```C
/** * process the input and get the resoult * @param handle * @param input input infomation of texture or pixelbuffer *The input texture for Android is oes texture. When input the texture, you need to input its width and height, and put the texture in input - > data.texture[0]* iOS only supports yuv420, 420f pixelbuffer input, the output is the corresponding format. No manual release is required, and pixelbuffer is placed at input - > data.buffer* @param output output infomation of texture or pixelbuffer * The input texfure for Android is oes texture. When returning width and height of the texture, the result will be placed at output->data.texture[0].* The input of iOS is pixelbuffer， pixelbuffer will be placed at output->data.buffer * @return If succeed return BEF_EFFECT_RESULT_SUC. For other values, refer to bef_effect_ai_public_define.h. */ BEF_SDK_API bef_effect_result_t bef_ai_image_quality_enhancement_video_sr_process(bef_image_quality_enhancement_handle handle, const bef_ai_video_sr_input* input, bef_ai_video_sr_output *output);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_image_quality_enhancement_handle |Handle of picture quality. |
|input |ef_ai_video_sr_input \* |The string of license file. |
|output |bef_ai_video_sr_output \* |The string of license file. |


**input infomation of texture or pixelbuffer**

The input texture for Android is oes texture. When input the texture, you need to input its width and height, and put the texture at input \-\> data.texture[0]. iOS only supports yuv420, 420f pixelbuffer input. Pixelbuffer will be placed at input \-\> data.buffer **output output infomation of texture or pixelbuffer** The output texture for Android is oes texture, and the width and height of the texture will be returned. The texture result will be placed at output\-\>data.texture[0]. The output for iOS is pixelbuffer, which will be placed at ouput \-\>data.buffer in corresponding format. No manual release is required for pixelbuffer. You need to retain the buffer first to prevent the internal memory from recycling pixelbuffer.

**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more information, refer to bef_effect_ai_public_define.h.

<span id="5. Release supperresolution handles for picture quality"></span>
## 5. Release supperresolution handles for picture quality

```C
/**
 * @param handle    handle that will  destroy
 */
BEF_SDK_API bef_effect_result_t 
bef_ai_image_quality_enhancement_vidoe_sr_destory(bef_image_quality_enhancement_handle handle);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_image_quality_enhancement_handle |Handle of picture quality created. |


<span id="518a6468"></span>
## 6. Parameter introduction

```C
typedef struct bef_ai_video_sr_init_config
{
    const char* model_path;     // Path to the model file, please see the description of the algorithm model in the appendix for details
    int model_data_length;      // No need to pass value
    const char* metal_path;     // No need to pass value
    bool enable_mem_pool;       // Whether to use memory pools, used in short video scenarios
    bef_ai_lens_data_type input_type;   // Input is currently only in pixelbuffer format
    bef_ai_lens_data_type output_type;  // The output is two kinds: pixelbuffer or metal texture
    float float_thresh;         // No need to set
    int srType;            // 1.5x use the value 15，2.0x use the value 20
}bef_ai_video_sr_init_config;
```


<span id="Java interface"></span>
# Java interface

<span id="1. Create supperresolution handles for picture quality"></span>
## 1. Create supperresolution handles for picture quality

Create superresolution handles for picture quality.

```Java
public int init(String rwDir, String licensePath){
        int ret = nativeCreate(rwDir, licensePath);
        if (ret != BytedEffectConstants.BytedResultCode.BEF_RESULT_SUC){
            mInited = false;
            return ret;
        }
        mInited = true;
        return ret;
    }
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|rwDir |String |Read\-write path. |
|licensePath |String |License file path |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail.

<span id="2. Create to process superresolution"></span>
## 2. Create to process superresolution

```Java
public BefVideoSRInfo process(int srcTextureId ,int width, int height){
        if (!mInited){
            return null;
        }

        BefVideoSRInfo srInfo  =  new BefVideoSRInfo();
        int ret = nativeProcess(srcTextureId, width, height, srInfo);
        if (ret != BytedEffectConstants.BytedResultCode.BEF_RESULT_SUC) {
            Log.e(BytedEffectConstants.TAG, "nativeVideoSrProcess " + ret);
            return null;
        }
        return srInfo;
    }
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|srcTextureId |int |Source texture. |
|width |int |Width of texture input. |
|height |int |Height of texture input. |


**Return value:** 

Return the result of superresolution when succeed, otherwise return empty.

<span id="3. Release superresolution resource"></span>
## 3. Release superresolution resource

```Java
public void release() {
        if (mInited){
            nativeRelease();
        }
        mInited = false;
    }
```


<span id="406bc0e5"></span>
## 4. Set the value of SR

```Java
public static enum LensVideoAlgType {
        SR_R_TYPE(0),  // 2x SR
        SR_A_TYPE(1),
        SR_G_TYPE(2),
        SR_N_TYPE(3),
        SR_R15_TYPE(4),  // 1.5x SR
        SR_U_UNKNOW(5);
        }
```


<span id="e24aefff"></span>
# Appendix for algorithm model of SR

Android does not need to use the algorithm model because of the difference in implementation with iOS, while iOS must use the algorithmic model.

<span id="29795e97"></span>
## Algorithm model \- iOS specific

**Sample method**

The algorithm relies on the **videovrsr.bundle** file, which needs to be copied to the root directory of the installed app by placing the bundle file under the main project.

If you directly use the **core** file in sample to `initTask` and do not make any other changes, you need to find the model file by default without passing in the path, but it must be placed here.

As shown in the figure:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5538405be1844f29b4696c70a1a19f75~tplv-goo7wpa0wc-image.image" width="568px" /></div>


**About C interfaces**

If you want to pass the path yourself, you can modify the model path parameter.

For version 4.4.0 and above, you can pass the path parameter by modifying the `bef_ai_video_sr_init_config.model_path` in the **BEVideoSRTask.m** file.

As shown in the figure:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/137236b626b74989b01b8dfb18caedf9~tplv-goo7wpa0wc-image.image) </span>

<span id="FAQ"></span>
# FAQ

<span id="1. If there are any exceptions, please check whether there are the following types of logs"></span>
### 1. If there are any exceptions, check whether there are the following types of logs

Answer: Check logs with following tags:


* **bef_effect_ai**

* **SMASH_E_LOG**

* **EffectSDK**


<span id="2. If there is no result, or the result is incorrect"></span>
### 2. If there is no result, or the result is incorrect

Detect whether the OpenGL environment is correct for Android and whether the input texture is correct.

For iOS, use Xcode to check whether the return result of pixelbuffer is correct.
