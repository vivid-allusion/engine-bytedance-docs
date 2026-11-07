---
title: "Video Frame Insertion"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-video-frame-insertion"
---

The frame insertion algorithm is suitable for smooth slow playback/frame rate improvement. The algorithm does not support real\-time camera stream as input, only supports the input method of importing video from album.

<span id="c9e22bf0"></span>
# Technical Specifications


|**Category** |**Supported Formats** |
|---|---|
|Platforms |* Android<br><br>* iOS |
|Input formats |* RGBA8888<br><br>* BGRA8888 |
|Memory footprint |< 42M (test device OPPO R11) |
|Detection speed |< 79ms (test equipment OPPO R11) |


<span id="ddaa1d61"></span>
# Video frame insertion strategy in sample

The frame insertion strategy is for reference only and is consistent with the example in the sample.

Assuming the input video is 20fps, with a frame insertion magnification of 0.5:


|**Frame number** |**1** |**2** |**3** |**4** |**5** |**6** |**7** |**8** |
|---|---|---|---|---|---|---|---|---|
|Original video timestamp (ms) |0 |50 |100 |150 |200 |250 |300 |350 |
|Expected timestamp (ms) |0 |25 |50 |75 |100 |125 |150 |175 |
|Yes frame insertion |No |Yes |No |Yes |No |Yes |No |Yes |
|Use frame number |1 |0.5 frame insertion |2 |0.5 frame insertion |3 |0.5 frame insertion |4 |0.5 frame insertion |


The input video is 20fps, with frame insertion magnification of 0.8:


|**Frame number** |**1** |**2** |**3** |**4** |**5** |**6** |**7** |**8** |
|---|---|---|---|---|---|---|---|---|
|Original video timestamp (ms) |0 |50 |100 |150 |200 |250 |300 |350 |
|Expected timestamp (ms) |0 |40 |80 |120 |160 |200 |240 |280 |
|Yes frame insertion |No |Yes |No |No |No |No |Yes |No |
|Use frame number |1 |0.8 frame insertion |2 |3 |4 |5 |0.8 frame insertion |6 |


Summary: In the case of normal video playback, frame insertion is performed on the position where the expected timestamp position is missing frames.

<span id="fc20d55e"></span>
# C API

For the detailed interface description, refer to header file: bef_ai_image_quality_enhancement_vfi

<span id="610378df"></span>
## 1. Create a handle for the Frame Insertion Algorithm

```C
BEF_SDK_API bef_effect_result_t
bef_ai_image_quality_enhancement_vfi_create(bef_image_quality_enhancement_handle *handle, bef_ai_vfi_init_config* config);

typedef struct bef_ai_vfi_init_config {
Const char * kernelBinPath;//readable and writable path
bef_ai_lens_vfi_type type;//type of frame insertion
bef_ai_lens_power_level level;//iOS need not be set
bef_ai_lens_vfi_data_type dataType;//input/output type of frame insertion input
}bef_ai_vfi_init_config;
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|Handle |bef_image_quality_enhancement_handle \* |Created frame insertion algorithm handle. |
|Config |bef_ai_vfi_init_config \* |Configuration parameters when the algorithm is initialized. |


**Return value:** 

Success returns BEF_RESULT_SUC, failure returns the corresponding error code. For more information, refer to bef_effect_ai_public_define.

<span id="c19652ca"></span>
## 2. Frame insertion algorithm execution

Support texture or buffer input, just select one as input, texture is not used, set to \-1 or 0

```C
BEF_SDK_API bef_effect_result_t
bef_ai_image_quality_enhancement_vfi_process(bef_image_quality_enhancement_handle handle, 
                                                bef_ai_vfi_process_config* config, 
                                                bef_ai_lens_vfi_data *output);

typedef struct bef_ai_vfi_process_config {
    int textureIdP; //Texture id of the first frame
    int textureIdN; //The texture id of the second frame, if the inputFrameNum set by LensVideoVFIParam is 2, this texture ID must be set
    void* buffer;   //buffer of the first frame
    void* backBuffer; //buffer of the second frame
    int width; //width of the input image
    int height; //height of the input image
    int strideW; //stride in the x direction of the input image
    int strideH; //stride in the y direction of the input image
          //Frame flag
                //For each input one frame test case: 0 means the first frame, 1 means to update the frame, 2 means not to update the frame, update timeStamp (for the case of inserting multiple frames between two frames)
                //For each input two frames test case: 0 or 1 means to update the frame, 2 means not to update the frame, update timeStamp (for the case of inserting multiple frames between two frames)
    int flag;
    int open; //frame insertion dynamic switch
    float timeStamp; //frame insertion position between frames, for example: 0.5 means frame insertion in the middle of two frames, 0.1 means frame insertion at a position of 0.1 away from the first frame
    float scaleX; //scaling factor in x direction
    float scaleY; //scaling factor in y direction
}bef_ai_vfi_process_config;

typedef union bef_ai_lens_vfi_data{
    int texture; // If it is a texture, the index of the texture here, the texture of ios currently only supports the texture of metal, android needs the oes texture, and the texture is placed in the 0 position
    void* buffer;   // If it is data input, iOS pass the pointer to pixelBuffer
}bef_ai_lens_vfi_data;
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_image_quality_enhancement_handle |Frame insertion algorithm handle. |
|Config |const bef_ai_vfi_process_config \* |Configuration parameters when the algorithm is initialized. |
|output |bef_ai_lens_vfi_data \* |Frame insertion algorithm output. |


**Return value:** 

Success returns BEF_RESULT_SUC, failure returns the corresponding error code. For more information, refer to bef_effect_ai_public_define.

<span id="c55e2ebd"></span>
## 3. Release the handle

```C
BEF_SDK_API bef_effect_result_t
bef_ai_image_quality_enhancement_vfi_destroy(bef_image_quality_enhancement_handle handle);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|Handle |bef_image_quality_enhancement_handle |Handle to the frame insertion algorithm. |


**Return value:** 

Success returns BEF_RESULT_SUC, failure returns the corresponding error code. For more information, refer to bef_effect_ai_public_define.

<span id="d7cca6bd"></span>
## 4. Frame insertion algorithm authorization

```C
//Offline license detection method
BEF_SDK_API bef_effect_result_t
bef_ai_image_quality_enhancement_vfi_check_license(
    bef_image_quality_enhancement_handle handle, 
    const char* license_path);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_image_quality_enhancement_handle |Frame insertion algorithm handle. |
|licensePath |const char \* |License file string. |


**Return value:** 

Success returns BEF_RESULT_SUC, failure returns the corresponding error code. For more information, refer to bef_effect_ai_public_define.

<span id="Java interface description"></span>
# Java interface description

**Interface Description**

Refer to the file for detailed interface description: com.bytedance.labcv.effectsdk.VideoFI.java

<span id="f4dbce99"></span>
## 1. Initialize the frame insertion handle

```Java
public int create(String rwDir, BytedEffectConstants.ImageQualityVfiType algoType, BytedEffectConstants.ImageQualityVfiDataType dataType,
                       int inputFrame, BytedEffectConstants.ImageQulityPowerLevel level)

public enum ImageQualityVfiType {
    IMAGE_QUALITY_VFI_TYPE_UM(0), // Add frames
    IMAGE_QUALITY_VFI_TYPE_COVER(1); // Frame Fusion
};

public enum ImageQualityVfiDataType {
    IMAGE_QUALITY_VFI_DATA_TYPE_BUFFER_RGBA8888(0),
    IMAGE_QUALITY_VFI_DATA_TYPE_TEXTURE_RGBA8(1);
}

public enum ImageQulityPowerLevel {
    POWER_LEVEL_DEFAULT (0),
    POWER_LEVEL_LOW (1),
    POWER_LEVEL_NORMAL (2),
    POWER_LEVEL_HIGH (3),
    POWER_LEVEL_AUTO (4);
}
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|rwDir |String |Frame insertion algorithm output file path. |
|algoType |ImageQualityVfiType |Frame insertion algorithm type. |
|dataType |ImageQualityVfiDataType |Input category is texture or buffer. |
|inputFrame |int |Frame insertion algorithm input frame number. |
|level |ImageQulityPowerLevel |Frequency level used. |


**Return value:** 

Returns BEF_RESULT_SUC successfully, otherwise returns the corresponding error code.

<span id="177d3e53"></span>
## 2. Frame insertion algorithm processing

```Java
public int processTexture(
    int textureIdP, 
    int textureIdN, 
    int width, 
    int height, 
    int flag, 
    float scaleX, 
    float scaleY, 
    float timeStamp);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|textureIdP |int |First frame texture number. |
|textureIdN |int |second frame texture number. |
|width |int |Input image width. |
|height |int |Input image height. |
|Flag |int |Frame flag. |
|scaleX |float |x\-direction scaling factor. |
|scaleY |float |y\-direction scaling factor. |
|timeStamp |float |Frame insertion. |


<span id="ccbaf652"></span>
## 3. Release the frame insertion handle

```Java
public void destroy()
```


<span id="FAQ"></span>
## FAQ

<span id="20c3329a"></span>
### 1. If there is any exception, check if there are any of the following types of logs

A: It is recommended to first check the log of the following tag output Error type:


* **bef_effect_ai**

* **SMASH_E_LOG**

* **EffectSDK**
