---
title: "Camera Movement"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-camera-movement"
---

The camera movement algorithm can add dynamic lens effects in LIVE and short videos to meet the needs of LIVE/short video users in dance and other scenes.

This algorithm is a new algorithm for V4.4.3.

**Note**

This function **requires opengl 3.0** version, cannot work in opengl 2.0.

Switch to opengl 3.0 example code:

iOS

```C
self.context = [BEGLUtils createContextWithDefaultAPI:kEAGLRenderingAPIOpenGLES3];
```


Android

```Java
mSurfaceView = findViewById(R.id.glview);
ActivityManager am = (ActivityManager) getSystemService(ACTIVITY_SERVICE);
ConfigurationInfo ci = am.getDeviceConfigurationInfo();
if(ci.reqGlEsVersion >= 0x30000)
{
    mSurfaceView.setEGLContextClientVersion(3);
}
else
{
    mSurfaceView.setEGLContextClientVersion(2);
}
```


<span id="0dbb9e21"></span>
# Technical specifications


|**Category** |**Supported Formats** |
|---|---|
|Platforms |* Android<br><br>* iOS |
|Input formats |* Android: RGBA TEXTURE<br><br>* iOS: RGBA Buffer |
|Memory footprint |< 41M (test device OPPO R11) |
|Detection speed |< 25ms (test equipment OPPO R11) |


<span id="f6fb316b"></span>
# C interface description

For the detailed interface description, refer to the header file: bef_ai_image_quality_enhancement_cine_move

```C
BEF_SDK_API
bef_effect_result_t bef_effect_ai_cine_move_create(bef_image_quality_enhancement_handle *handle, int lensType);

//camera parameter，note：version 443 only support BEF_CINE_MOVE_ALG_SNAKE_V8，BEF_CINE_MOVE_ALG_HEART_BEAT_V9，BEF_CINE_MOVE_ALG_BREATH_V10，BEF_CINE_MOVE_ALG_ROT360_V11
typedef enum bef_cine_move_alg_type {
    BEF_CINE_MOVE_ALG_START = 0,
    BEF_CINE_MOVE_ALG_V1,   
    BEF_CINE_MOVE_ALG_V2,    
    BEF_CINE_MOVE_ALG_V3,   
    BEF_CINE_MOVE_ALG_RHYTHMIC_V4,  
    BEF_CINE_MOVE_ALG_CENTER_FOCUS, 
    BEF_CINE_MOVE_ALG_Y_COOR_V6,    
    BEF_CINE_MOVE_ALG_ROT_V7,       
    BEF_CINE_MOVE_ALG_SNAKE_V8 = 8,     // Fluctuation Mode
    BEF_CINE_MOVE_ALG_HEART_BEAT_V9,    // Heartbeat Mode
    BEF_CINE_MOVE_ALG_BREATH_V10,       // Breathing Mode
    BEF_CINE_MOVE_ALG_ROT360_V11,       // POV mode
    BEF_CINE_MOVE_ALG_END
} bef_cine_move_alg_type;
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|Handle |bef_image_quality_enhancement_handle \* |Created algorithm handle. |
|lensType |int |Movement type. |


**Return value:** 

Success returns BEF_RESULT_SUC, while failure returns the corresponding error code. For more information, refer to bef_effect_ai_public_define

<span id="b2204a0e"></span>
## 2. Camera movement algorithm process

```C
BEF_SDK_API
bef_effect_result_t bef_effect_ai_cine_move_detect(bef_image_quality_enhancement_handle handle,
                                                         bool isFirstFrame,
                                                         bool isOpen,
                                                         const bef_ai_cine_move_input* input,
                                                         bef_ai_cine_move_output* output);

// Camera movement input
typedef struct bef_ai_cine_move_input{
    int width;   // Input width
    int height;  // Input height
    int stride; 
    bef_ai_lens_data data;   // Input data
    bef_ai_lens_data_type type; // Input data type，iOS support pixelbuffer，Android support oes texture
} bef_ai_cine_move_input;

// Camera movement output
typedef struct bef_ai_cine_move_output{
    bef_ai_lens_data data;   // Output data, will fill the corresponding output part according to the input
    int width;   // Output width
    int height;  // Output height
} bef_ai_cine_move_output;

// Camera movement data 
typedef union bef_ai_lens_data{
    int texture[2]; // If it's a texture, here is the index of the texture. ios textures currently only support metal textures, android requires oes textures and the texture is placed at position 0
    void* buffer;   // If it's a data input, iOS passes in a pointer to the pixelBuffer
}bef_ai_lens_data;
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|Handle |bef_image_quality_enhancement_handle |Algorithm handle. |
|isFirstFrame |bool |Whether the first frame. |
|isOpen |bool |Whether to turn on movement operation processing. |
|Input |bef_ai_cine_move_input \* |Image data input. |
|Output |bef_ai_cine_move_output \* |Algorithm result output. |


**Return value:** 

Success returns BEF_RESULT_SUC, while failure returns the corresponding error code. For more information, refer to bef_effect_ai_public_define

<span id="c1cff759"></span>
## 3. Release the handle

```C
BEF_SDK_API
bef_effect_result_t bef_effect_ai_cine_move_release(bef_image_quality_enhancement_handle handle);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|Handle |bef_image_quality_enhancement_handle |Algorithm handle. |


**Return value:** 

Success returns BEF_RESULT_SUC, while failure returns the corresponding error code. For more information, refer to bef_effect_ai_public_define

<span id="8e8e60bf"></span>
## 4. Camera movement algorithm authorization

```C
BEF_SDK_API
bef_effect_result_t bef_effect_ai_cine_move_check_license(bef_image_quality_enhancement_handle handle, const char *licensePath);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|Handle |bef_image_quality_enhancement_handle |Algorithm handle. |
|LicensePath |const char \* |License file path. |


**Return value:** 

Success returns BEF_RESULT_SUC, while failure returns the corresponding error code. For more information, refer to bef_effect_ai_public_define

<span id="Java Interface Description"></span>
# Java Interface Description

For the detailed interface description, refer to the file: com.effectsar.labcv.effectsdk.CineMove.java

<span id="4c8b874c"></span>
## 1. Initialize the algorithm handle

```Java
public int init(
    Context context, 
    int type, 
    String licensePath, 
    boolean onlineLicense
    )

// Version 4.4.3 only supports fluctuating mode (8) heartbeat mode (9) breathing mode (10) POV mode (11)
public static enum CINE_MOVE_TYPE {

        CINE_MOVE_ALG_SNAKE_V8(8),
        CINE_MOVE_ALG_HEART_BEAT_V9(9),
        CINE_MOVE_ALG_BREATH_V10(10),
        CINE_MOVE_ALG_ROT360_V11(11),
     
    }
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|context |Context |Android context. |
|type |int |Algorithm type. |
|licensePath |String |License file path. |
|onlineLicense |boolean |Whether it is an online license |


**Return value:** 

Successfully returns BEF_RESULT_SUC, otherwise returns the corresponding error code.

<span id="b3d97d52"></span>
## 2.Camera movement algorithm processing

```Java
public int process(
    int inputTexture, 
    PixlFormat pixelFormat, 
    int imageWidth, 
    int imageHeight, 
    int imageStride, 
    boolean isOpen, 
    Integer destTextureId
    )
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|inputTexture |int |Input texture number. |
|pixelFormat |PixlFormat |Input Format. |
|imageWidth |int |Texture width. |
|imageHeight |int |Texture height. |
|imageStride |int |Texture stride. |
|isOpen |boolean |Whether to turn on the algorithm. |
|destTextureId |Integer |Output Texture Number. |


<span id="c7bf8af4"></span>
## 3. Release the algorithm handle

```Java
public void release()
```


<span id="bd4a37d9"></span>
# FAQ

<span id="28648684"></span>
## 1. If there is any exception, check if there are any of the following types of logs

A: It is recommended to first check the log of the following tag output Error type:


* bef_effect_ai

* SMASH_E_LOG

* EffectSDK
