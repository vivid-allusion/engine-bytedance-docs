---
title: "C Interface Access Guide"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-c-interface-access-guide"
---

<span id="Importing SDK to iOS Project"></span>
# Importing SDK to iOS Project

If CocoaPods is used in the project, go to step 2; if not, go to step 1.


1. In the root directory of the project, execute "pod init && pod install" to obtain the Podfile file.

2. Open the iossample folder, and copy the BytedEffectSDK.podspec, libeffect\-SDK.a, and include files to the root directory of your project.

3. Open the Podfile file, and add a new line: pod 'BytedEffectSDK', :path =\> './'.

4. Execute "pod install" and open [Project Name].xcworkspace. BytedEffectSDK exists in the Pods/Development Pods directory.

5. Copy the provided material package (typically the resource folder) to the project.


<span id="Importing SDK to Android Project (in C API Mode)"></span>
# Importing SDK to Android Project (in C API Mode)

<span id="Common Importing"></span>
## Common Importing

If no special cases are taken, use the following methods to integrate.


1. Open the compressed zip: byted_effect_andr.zip, and unzip android_c_sdk.zip

2. Extract the class.jar from the aar file, copy the jar package to the project main module `libs`, and ensure that the main module build.gradle dependencies have api fileTree (include: ['\* .jar'], dir: 'libs')


**EXAMPLE**

```Plain
dependencies {
    implementation fileTree(include: ['*.jar'], dir: 'libs') 
}
```



3. Add libeffect.so under folders arm64\-v8a and armeabi\-v7a to your project.

4. Add the SDK header file under `include` to the project.

5. Add assets, by adding the provided assets package (usually the resource folder) to the project.


<span id="Special cases of importing SDK"></span>
## Special cases of importing SDK

For the following special cases, there are additional operations when importing the SDK.

<span id="The developer has its own lib library and relies on sdk 's libeffect.so in lib, or uses dlopen to load libeffect.so"></span>
### The developer has its own lib library and relies on sdk 's libeffect.so in lib, or uses dlopen to load libeffect.so

In this case, when android loads so, it cannot call the `JNI_OnLoad` interface in the sdk , which leads to some methods in the sdk that cannot be used, and finally causes an execution error.

In response to this situation, we have added the following two interfaces to deal with this problem (from Version 4.3.0):

```C
/**
 * @brief  Active call to effect_sdk's JNI_OnLoad
 * @param vm            Indicates the object address of the Java VM
 * @param reserved      Pass NULL is ok
 * @return              Returns the JNI version used by the current NDK
*/
JNIEXPORT jint BEF_EFFECT_JNI_OnLoad(JavaVM* vm, void* reserved);
/**
 * @brief  Active call to effect_sdk's JNI_OnUnLoad
 * @param vm            Indicates the object address of the Java VM
 * @param reserved      Pass NULL is ok
*/
JNIEXPORT void BEF_EFFECT_JNI_OnUnload(JavaVM *vm, void *reserved);
```


When the developer uses dlopen to load libeffect.so in its own lib, it can refer to the following methods and example code:


1. Use dynamic loading to get the function address of `BEF_EFFECT_JNI_OnLoad` and `BEF_EFFECT_JNI_OnUnload` Function, refer to the following:


```C
typedef void (*JNI_OnLoad_Def)(JavaVM *, void *);
typedef void (*JNI_OnUnload_Def)(JavaVM *, void *); 
// 1.Load libeffect.so 
void * handle = dlopen( libeffect.so ,RTLD_NOW | RTLD_LOCAL) 
if (handle) 
{ 
// 2.Get function addresses of JNI_OnLoad and JNI_OnUnload in the libeffect.so
JNI_OnLoad_Def BEF_EFFECT_JNI_OnLoad_ptr = (JNI_OnLoad_Def)dlsym(handle, "BEF_EFFECT_JNI_OnLoad" ); 
JNI_OnUnload_Def BEF_EFFECT_JNI_OnUnload_ptr = (JNI_OnUnload_Def)dlsym(handle, "BEF_EFFECT_JNI_OnUnload" ); 
} 
```



2. Call `BEF_EFFECT_JNI_OnLoad_ptr` in `JNI_Onload`, and call `BEF_EFFECT_JNI_OnUnload_ptr` in `JNI_OnUnload`.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><code>BEF_EFFECT_JNI_OnLoad_ptr</code> needs to be called in the native interface called by java to take effect (such as <code>JNI_OnLoad</code> interface, or custom jni interface). It cannot be called directly in the thread from the native layer, otherwise it will cause findclass failure.</div>


<span id="The developer use lib libraries directly link libeffect.so, such as cmake 's target_link_libraries way"></span>
### The developer use lib libraries directly link libeffect.so, such as cmake 's target_link_libraries way


1. Include the following header file into the project. This header file needs to be named: `bef_effect_jni_manager.h`.


```C
#ifndef bef_effect_jni_manager_h
#define bef_effect_jni_manager_h
#include <jni.h>
#include "bef_effect_ai_public_define.h"

/**
 * @brief Actively call the JNI_OnLoad interface of effect_sdk.
 * @param vm          Object address representing the Java virtual machine.
 * @param reserved    just pass NULL.
 * @return            Returns the JNI version used by the current NDK.
 */
BEF_SDK_API jint BEF_EFFECT_JNI_OnLoad(JavaVM* vm, void* reserved);

/**
 * @brief Actively call the JNI_OnUnload interface of effect_sdk.
 * @param vm          Object address representing the Java virtual machine.
 * @param reserved    just pass NULL.
 */
BEF_SDK_API void BEF_EFFECT_JNI_OnUnload(JavaVM *vm, void *reserved);

#endif //bef_effect_jni_manager_h
```



2. Call `BEF_EFFECT_JNI_OnLoad_ptr` in `JNI_Onload`, and call `BEF_EFFECT_JNI_OnUnload_ptr` in `JNI_OnUnload`.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><code>BEF_EFFECT_JNI_OnLoad_ptr</code> need to be called in the native interface called by java to take effect (such as <code>JNI_OnLoad</code> interface, or custom jni interface), can not be called directly in the thread from the native layer, otherwise it will cause findclass failure.</div>


<span id="Integrating SDK in Code"></span>
# Integrating SDK in Code

This section describes how to use C APIs (or AAR APIs provided in Android) to integrate the SDK and how to set SDK parameters related to beautification effects. For more information about the algorithm APIs and other APIs, refer to [C API](https://byteplus-docs.readme.io/effects/docs/c-api) and [Portrait SDK](https://byteplus-docs.readme.io/effects/docs/portrait-sdk).

The SDK only has image processing functions and does not support OpenGL processing or drawing. If these are not required, you can simply use some of the encapsulation code in the sample.

<span id="Before You Start"></span>
## Before You Start


1. Make sure video capture and image rendering are available in the project. The CV SDK only renders a specific frame, and both its input and output are textures. (There are APIs for buffer processing, which convert buffers to textures before processing them.)

2. Make sure that the project has an OpenGL environment. All functions related to the SDK will be called in the OpenGL thread. For more information, refer to **OpenGL Environment** .

3. Make sure that the material package has been added to the project. For details on how to copy materials to an Android project, refer to **Copying Materials** .


<span id="Procedure"></span>
## Procedure

Import the beautification functions in the CV SDK in three steps:


1. Initializing the SDK.

2. Using the SDK for Image Processing.

3. Set SDK parameters related to beautification effects, stickers, and filters.


<span id="Initializing the SDK"></span>
### Initializing the SDK

Call the following functions to initialize the SDK.

```C
bef_effect_handle_t _handle;
int ret = 0;
// Create an SDK instance.
ret = bef_effect_ai_create(&amp;_handle);
// Verify the SDK license. The handle needs to be called; otherwise, the verification will fail.
ret = bef_effect_ai_check_license(_handle, self.licensePath);
// Specify whether to enable parallel rendering (enabled by default).
ret = bef_effect_ai_use_pipeline_processor(_handle, usePipeline);
// Initialize the SDK. Set the fourth parameter to the path of the model file (ModelResource.bundle in the material package), and set the other parameters by referring to the example.
ret = bef_effect_ai_init(_handle, 10, 10, [[self.provider modelDirPath] UTF8String], "");
// Set the beautification mode. You can call the function by referring to the example.
ret = bef_effect_ai_composer_set_mode(_handle, 1, 0);
```


<span id="Using the SDK for Image Processing"></span>
### Using the SDK for Image Processing

**Supported types of input data:** 


|**Data Type** |**Data Format** |
|---|---|
|buffer (not recommended) |RGBA, BGRA, and YUV |
|texture |2D |


The SDK has two types of image processing APIs, which support buffer input and texture input, respectively. **Texture input is recommended** . If the project can only provide buffers, you are recommended to convert the buffers to textures before processing them. Directly providing buffers as input to the SDK will affect the performance.

<span id="Processing Input Textures"></span>
#### Processing Input Textures

Call the following functions to process input textures.

```C
int ret;
// Set the width of the image. If the size of images processed in two adjacent frames are different, an error may occur.
ret = bef_effect_ai_set_width_height(_handle, width, height);
// Set the rotation angle of the image. Generally, you can use the rotation angle of the mobile phone provided by the system.
ret = bef_effect_ai_set_orientation(_handle, orientation);
// Configure algorithm processing of the image. Call this function to perform face detection.
// Only texture and timeStamp are required. For example, you can directly call bef_effect_ai_algorithm_texture_with_buffer(_handle, texture, NULL, 0, 0, 0, 0, timeStamp);
// The other parameters are related to a buffer. In some cases, using both textures and buffers as the input can facilitate the process. However, in most cases, only texture input is required.
ret = bef_effect_ai_algorithm_texture_with_buffer(_handle, texture, buffer, format, width, height, bytesPerRow, timeStamp);
// Configure special effects. Call this function to configure beautification effects.
// The input and output textures should have the same width and height, and the input texture object and output texture object cannot share the same texture.
ret = bef_effect_ai_process_texture(_handle, inputTexture, outputTexture, timeStamp);
```


<span id="Processing Input Buffer"></span>
#### Processing Input Buffer

```C
int ret;
// Set the width of the image. If the size of images processed in two adjacent frames are different, an error may occur.
ret = bef_effect_ai_set_width_height(_handle, width, height);
// Set the rotation angle of the image. Generally, you can use the rotation angle of the mobile phone provided by the system.
ret = bef_effect_ai_set_orientation(_handle, orientation);
// Configure algorithm processing of the image. Call this function to perform face detection.
ret = bef_effect_ai_algorithm_buffer(_handle, buffer, format, width, height, bytesPerRow, timeStamp);
// Configure special effects. Call this function to configure beautification effects.
// The processing results are saved in outputBuffer. Make sure that the memory size of outputBuffer matches the given image width, height, and format.
ret = bef_effect_ai_process_buffer(_handle, inputBuffer, inputFormat, width, height, bytesPerRow, outputBuffer, outputFormat, timeStamp);
```


<span id="Setting SDK Parameters (Related to Beautification Effects, Stickers, and Filters)"></span>
### Setting SDK Parameters (Related to Beautification Effects, Stickers, and Filters)

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Call the APIs for setting SDK parameters after the SDK is initialized, and use the APIs in the same thread as the image processing SDK to avoid possible issues.</div>


<span id="Face Beautification, Body Beautification, and Makeup Effects"></span>
#### Face Beautification, Body Beautification, and Makeup Effects

Use the same API to configure face beautification, body shaping, and makeup effects. Generally, two steps are required to make a beautification effect take effect.


1. Set the material path.

2. Set the effect's intensity. The default value is 0, meaning no effect, and it will be used if you do not configure this setting.


**API for setting the material path:** 

```C
// Set the material.
bef_effect_result_t result = bef_effect_ai_composer_set_nodes(_handle, (const char **)nodesPath, count);
```


nodesPath is an array of character strings, where each line specifies the absolute path of a material on the device.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The configured materials will not be saved in the SDK. You need to add the paths of all materials to take effect each time you call this method.</div>


**API for setting the effect's intensity:** 

```C
// Set the intensity of an effect in the material.
bef_effect_result_t result = bef_effect_ai_composer_update_node(_handle, (const char *)node, (const char *)key, intensity);
```


node specifies the absolute path of the material on the device.

For example, in order to update the intensity of a face beautification effect, use a key to specify whether the specific function is skin whitening, skin smoothing, or sharpening. For more information, refer to the **Functions of Material Keys** .

<span id="Stickers"></span>
#### Stickers

**API for setting stickers:** 

```C
// Set stickers.
bef_effect_result_t result = bef_effect_ai_set_effect(_handle, (const char *)path);
```


path specifies the absolute path of the stickers on the device.

<span id="Filters"></span>
#### Filters

**API for setting filters:** 

```C
// Setting the Path of Filters
bef_effect_result_t result = bef_effect_ai_set_color_filter_v2(_handle, path);

// Setting the Intensity of Filters
result = bef_effect_ai_set_intensity(_handle, BEF_INTENSITY_TYPE_GLOBAL_FILTER_V2, intensity);
```


path specifies the absolute path of the filters on the device.
