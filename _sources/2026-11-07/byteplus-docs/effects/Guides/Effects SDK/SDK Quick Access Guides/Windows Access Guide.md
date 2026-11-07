---
title: "Windows Access Guide"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-windows-access-guide"
---

<span id="Development Environment"></span>
## Qt Demo

The Qt demo is an app that captures camera input and performs real\-time effect rendering. It covers the Effect SDK's wide variety of effects (filters, stickers, beauty makeup, body reshaping, virtual backgrounds, etc.) as well as algorithm capabilities (face recognition, gesture recognition, human segmentation, etc.). The demo also wraps the underlying Effect SDK C interfaces with C++ to help developers integrate the Effect SDK more quickly.

<span id="5053e857"></span>
## Recommended Development Environment


* Qt 5.15.2 (not strictly required)

* Visual Studio 2019

* CMake 3.14

> **Note ⚠️**  On the Windows platform, the Effect SDK depends on the capabilities of the Angle dynamic library, so you need to load and initialize the corresponding components (`libGLESv2.dll` and `libEGL.dll`). See the EffectManager module description below for details. The OpenGL context **must** be created with the Angle library — do not use any other GL context. See the BEFEffectGLContext module for details.


<span id="6349d57b"></span>
## Main Components and Key API Descriptions

<span id="a3ee3fa8"></span>
### EffectManager

Manages `EffectHandle` and loads/initializes the Angle dynamic library symbols.


* `loadEGLDLL` / `unloadEGLDLL` — initialize/deinitialize Angle dynamic library symbols

* `createHandle` / `releaseHandle` — manage the `EffectHandle` object


<span id="77a61183"></span>
### EffectHandle

Wraps the underlying Effect SDK C interfaces and provides effect processing operations. If you need to create multiple `EffectHandle` objects (e.g., simultaneously processing multiple camera video streams), you must enable the `MULTI_HANDLE_USE` macro.


* `setInput` — sets the raw image buffer to be processed; the format **must** be: RGB/RGBA, BGR/BGRA, I420. Synchronous operation; the result can be obtained via `getOutput` after the call completes.

* `getOutput` — gets the processed image buffer; the format is the same as the input format. Buffer memory is managed by the `EffectHandle` object; the caller does not need to free it.

* `updateComposerNodes` / `setFilter` / `setSticker` — set the desired effects.


<span id="d48c3e82"></span>
### BEFEffectGLContext

Provides OpenGL context management.


* `initGLContext` / `releaseGLContext` — initialize/destroy the GL context

* `makeCurrentContext` / `doneCurrentContext` — set the GL context


<span id="b6f1746b"></span>
### BEImageUtil

Provides shader conversion for BGR/BGRA, RGB/RGBA, and I420 formats.


* `transferBufferToTexture` — converts an image in a given format to a GPU texture in a given format

* `transferTextureToTexture` — converts a texture in one format to a texture in another format

* `readPixel` — reads texture content into a CPU buffer


<span id="cbd27b2d"></span>
### BEAlgorithmManager

Wraps the algorithm detection interfaces and provides fast algorithm detection capability.


* `initProcessInfo` / `initResourceFinder` — initialize the algorithm detection module

* `addAlgorithm` / `removeAlgorithm` — enable/disable the algorithm sub\-items to detect

* `processAlgorithm` — run algorithm detection

* `getInputInfo` — set the input buffer

* `getOutputInfo` — get the algorithm detection results


<span id="990c6bb3"></span>
### BELicenseVC.h / license_requester.h

Shows how to perform online license verification and license download/validation. For the detailed verification principles and process, see [https://docs.byteplus.com/en/docs/effects/docs-windows-license-guide](https://docs.byteplus.com/en/docs/effects/docs-windows-license-guide)

<span id="bc2eb4e5"></span>
### BEDataManager

Wraps the usage of effect prop package resources, including the use of tag fields inside prop packages. If you are unsure how to use a particular prop, refer to the usage methods inside `BEDataManager`.

Among the components above, except for `BELicenseVC` and `BEDataManager`, the other components are recommended for direct integration into your own project, which can greatly reduce integration development cost.

<span id="4188e1db"></span>
## Project Structure (see Demo source CMakeLists.txt; compile as needed)

```Plain
add_subdirectory(EffectManager) # C++ wrappers of the underlying SDK's C interfaces; general integration can directly use the C++ interfaces provided here
add_subdirectory(Algorithm)     # Provides algorithm (face, gesture, etc.) integration wrapper code
add_subdirectory(app)           # UI part, demonstrates how to use the interfaces wrapped by Algorithm and EffectManager; the UI framework here uses Qt 5.15.2
```


<span id="23ec2be8"></span>
### If you only want to integrate effect\-related features (including beauty, filters, makeup, stickers, etc.)

Compile only `EffectManager`, then call the `EffectHandle` object interfaces inside it. The general flow is:

```Plain
// Create the Effect SDK handle manager
IEffectManager* manager = createEffectManager();
// Create a beauty handle
IEffectHandle* handle = manager->createHandle();
// Pass in the license and model file paths
// The license file is downloaded locally via curl using the interfaces in the licenseManager directory of the demo source code
// The model file differs depending on the props purchased; contact sales to obtain it, or test with the demo model first
handle->initResource();
// Pass in the prop package path and set the effects to enable
// The path must be the absolute path of the prop package; all paths must be UTF-8 encoded
handle->updateComposerNodes();
// Pass in the image buffer for effect processing; supported buffer formats are RGB/RGBA, BGR/BGRA, I420
// Other formats must be converted to these formats before being passed to the Effect SDK
handle->setInput();
// Get the processed image buffer; the returned buffer format matches the input format
handle->getOutput();
// Destroy the Effect SDK handle
handle->releaseHandle();
// Destroy the beauty handle manager
destroyEffectManager(manager);
```


For the detailed flow, refer to the usage of `EffectHandle` in `VideoFilter.cpp` in the demo.

> **Note ⚠️** 


* The prop package path parameter must be a full path, and the string must be UTF\-8 encoded.

> * When using the `IEffectHandle` interfaces, you do not need to consider OpenGL context setup — the `IEffectHandle` object wraps this internally.

> * The `IEffectHandle` object is thread\-safe and can be called from other threads. However, if you want to process multiple video streams simultaneously (e.g., capturing multiple camera video streams at once), it is best to create multiple `IEffectHandle` objects, one per video stream, and enable the `MULTI_HANDLE_USE` macro.

> * Effect processing is time\-consuming, so try not to call effect interfaces on the UI thread to avoid blocking the app UI.


&nbsp;

<span id="37213cde"></span>
### If you want to integrate algorithm\-related features (including face detection, gesture detection, human keypoints, etc.)

Compile `EffectManager` and `Algorithm`. After successfully setting up `EffectManager`, refer to the algorithm\-related processing in "BEAlgorithmVC" in the demo. The general flow is:

```Plain
// Same as the effect processing flow above
// First create and successfully initialize the IEffectManager and IEffectHandle objects
// See the effect processing flow above

// Create the IAlgorithmManager object
IAlgorithmManager* algo_mgr = createAlgorithmManager();

// Initialize the algorithm module with license and model file paths
// Paths must be absolute; all paths must be UTF-8 encoded
algo_mgr->initResourceFinder();
algo_mgr->initProcessInfo();

// Register a render callback into IEffectHandle
// A lambda object is used here as an example
IEffectHandle->setRenderCallback([](){
    // Run algorithm detection in the IEffectHandle render callback
    // Feed the buffer output by IEffectHandle into IAlgorithmManager
    algo_mgr->getInputInfo()->clear();
    algo_mgr->getInputInfo()->m_buffer = input->frame.imageData;
    algo_mgr->getInputInfo()->m_width = input->frame.width;
    algo_mgr->getInputInfo()->m_height = input->frame.height;
    algo_mgr->getInputInfo()->m_bytePerRow = input->frame.width * input->frame.channel;
    algo_mgr->getInputInfo()->m_format = (bef_ai_pixel_format)input->pixelFormat;
    // Fill in the orientation according to the actual input; see the bef_ai_rotate_type comments in the header file
    algo_mgr->getInputInfo()->m_ori = BEF_AI_CLOCKWISE_ROTATE_0;

    // Run algorithm detection
    algo_mgr->processAlgorithm();

    // Get the detection results
    result = algo_mgr->getOutputInfo();
});

// Add the algorithm detection sub-items to run
// See the BE_FEATURE enum type definition
algo_mgr->addAlgorithm();

// Disable the specified detection sub-item
algo_mgr->removeAlgorithm();

// Destroy the IAlgorithmManager object
destroyAlgorithmManager();
```


For the detailed algorithm detection flow, refer to the `BEAlgorithmVC.cpp` module in the demo.

<span id="8385ae5b"></span>
### If you want source\-level debugging of the demo

You also need to compile the `app` module, which requires setting up a Qt 5.15.2 environment.

<span id="bc3c59b5"></span>
## Development Environment

The source directory already contains the Effect SDK development files and resource files:


* Headers: `third/effect_sdk/inc`

* Libraries: `third/effect_sdk/libs`

* Beauty materials: `app/EffectResource/resource/ComposeMakeup`

* Sticker materials: `app/EffectResource/resource/stickers_resource`

* Filter materials: `app/EffectResource/resource/Filter`

* Model files: `app/EffectResource/resource/model`


When integrating on your own, use the SDK's compiled distribution package — do not use the `effect_sdk` library from the demo directory directly, to facilitate follow\-up on future issues.

<span id="931c90d5"></span>
## Compilation and Running

Compilation can use the `build.bat` or `build_64.bat` script in the demo (compile input parameter: Debug or Release, e.g., `./build.bat Debug`). Before compiling, edit the `build.bat` and `build_64.bat` scripts to change the Qt path and VS path to those on your machine. If you are not using VS2019, remember to also modify the cmake parameters:

```Plain
set QtPath="C:\Qt\5.15.2\msvc2019"
set QtBinPath="C:\Qt\5.15.2\msvc2019\bin"
set MS_BUILD="C:\Program Files (x86)\Microsoft Visual Studio\2019\Professional\MSBuild\Current\Bin\MSBuild.exe"
```


```Plain
cmake -G "Visual Studio 16 2019" ../ -A Win32 -DCMAKE_BUILD_TYPE=%BUILD_TYPE% -DPLATFORM=%PLATFORM% -DCMAKE_PREFIX_PATH=%QtPath% -DENABLE_PROFILE=%PROFILE_STATUS%
```


After a successful build, the VS project file `ByteEffects.sln` will be generated in the corresponding directory — open it to compile and debug.

You can also use Qt Creator (version 6.0.0 or above recommended) to directly open the `CMakeLists.txt` in the current directory, then compile and run.

<span id="1d8565e1"></span>
### Choosing 32\-bit or 64\-bit configuration

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f7a5536e1786465087bc3f321b8aff7c~tplv-goo7wpa0wc-image.image) </span>

Configuration Parameter Reference

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/065302f5327f41a99f3915e8b41fd065~tplv-goo7wpa0wc-image.image) </span>

<span id="606674aa"></span>
# Win32 Demo

The Win32 demo reuses the `EffectManager` module from the Qt demo and uses OpenCV rendering to demonstrate basic effect processing. If you find the Qt demo project too large and difficult to set up for debugging, consider building the Win32 demo instead: run `recource_copy_win.bat` in the demo to copy resources, then open the VS project in `EffectDemo` and compile.

> **Note ⚠️**  Currently the standard Windows product only provides the Qt Demo online. If you need the Win32 Demo, please contact us separately to obtain it.


<span id="3b978bb2"></span>
## Recommended Development Environment


* Visual Studio 2019


<span id="b0ba0994"></span>
## Project Structure


* `EffectManager` — same as in the Qt demo; provides wrappers for the underlying Effect SDK

* `EffectBaseApp` — uses OpenCV to demonstrate the basic beauty effect processing flow


<span id="2b93da36"></span>
## Core Logic Description

```Plain
// Create IEffectManager
IEffectManager*  effectManager = createEffectManager();

// Load and initialize the Angle dynamic library symbols
effectManager->loadEGLDLL();

// Verify the local license; if verification fails, try to pull the latest online license and save it locally
std::string licensePath = appPath + "license/license.bag";
int licenseStatus = effectManager->checkLicenseStatus(licensePath.c_str());
if (licenseStatus != 0) {
    // request license file
    char* authMsg = nullptr;
    int authMsgLen = 0;
    char* license = nullptr;
    int len = 0;
    effectManager->getAuthMessage(&authMsg, &authMsgLen);

    // Replace these with the key/secret you applied for
    std::string key = "biz_license_tool_test_keyd64a6d073fbd42f8979a626572220595";
    std::string secret = "58979358c3e69215762eb5ecc3df7c9e";
    int code = request_license(key.c_str(), secret.c_str(), authMsg, &license, &len);
    if (code == 0) {
        FileUtil::createDirectory(appPath + "license");
        FileUtil::writeToFile(licensePath.c_str(), (unsigned char*)license, len);
        delete[] license;
    }
    effectManager->releaseAuthMessage(authMsg);
}

// Set resource paths
std::string modelDir = appPath + "../../resource/model/";
std::string composerDir = appPath + "../../resource/ComposeMakeup/";
std::string stickerDir = appPath + "../../resource/stickers_resource/";
std::string filterDir = appPath + "../../resource/Filter/";

// Construct and initialize IEffectHandle
IEffectHandle* effectHandle = effectManager->createHandle();
effectHandle->setUsePBO(true);
effectHandle->initResource(licensePath.c_str(), modelDir.c_str());

// Set beauty props
#ifdef TEST_BEAUTY
std::vector<std::string> nodePaths;
std::vector<std::string> tags;

nodePaths.push_back(composerDir + "beauty_IOS_lite");
nodePaths.push_back(composerDir + "beauty_IOS_lite");
nodePaths.push_back(composerDir + "beauty_IOS_lite");
nodePaths.push_back(composerDir + "reshape_lite");
nodePaths.push_back(composerDir + "beauty_IOS_lite");

// Set style makeup
#ifdef TEST_STYLE_MAKEUP
nodePaths.push_back(composerDir + "style_makeup/baicha");
#endif

// Set the tags of beauty prop sub-items
tags.push_back("smooth");
tags.push_back("whiten");
tags.push_back("sharp");
tags.push_back("Internal_Deform_Overall");
tags.push_back("Internal_Deform_Eye");

// Set the style makeup sub-item tag; use an empty string if there is no tag
#ifdef TEST_STYLE_MAKEUP
tags.push_back("");
#endif

// Enable all effects added to nodePaths
effectHandle->updateComposerNodes(nodePaths, tags);

// Set the intensity of different sub-items
// Locate the specific beauty sub-item using "prop package path, prop package tag"
// The tags inside each prop package (if any) may differ; refer to the code inside the 'BEDataManager' object in the Qt demo
// Or check the general API docs: https://cv-api.bytedance.com/doc/openapi/2036/200123
effectHandle->updateComposerNodeIntensity(nodePaths[0].c_str(), tags[0].c_str(), 0.5);
effectHandle->updateComposerNodeIntensity(nodePaths[1].c_str(), tags[1].c_str(), 0.35);
effectHandle->updateComposerNodeIntensity(nodePaths[2].c_str(), tags[2].c_str(), 0.7);
effectHandle->updateComposerNodeIntensity(nodePaths[3].c_str(), tags[3].c_str(), 0.35);
effectHandle->updateComposerNodeIntensity(nodePaths[4].c_str(), tags[4].c_str(), 0.35);

#ifdef TEST_STYLE_MAKEUP
effectHandle->updateComposerNodeIntensity(nodePaths[5].c_str(), "Makeup_ALL", 0.8);
effectHandle->updateComposerNodeIntensity(nodePaths[5].c_str(), "Filter_ALL", 0.5);
#endif

#endif

// Set filter and filter intensity
#ifdef TEST_FILTER
std::string filterPath = filterDir + "Filter_02_14";
effectHandle->setFilter(filterPath.c_str());
effectHandle->setFilterIntensity(0.8);
#endif

// Set sticker
#ifdef TEST_STICKER
std::string stickerPath = stickerDir + "stickers/heimaoyanjing";
effectHandle->setSticker(stickerPath.c_str());
#endif

// Capture camera video source for effect processing
int count = 0;
for (; cv::waitKey(1) != 27; cam >> frame) {
    if (frame.rows == 0 || frame.cols == 0) {
        continue;
    }

    // Set the image buffer to be processed
    // The format must be: BGR/BGRA/RGB/RGBA/I420; other formats must be converted before use
    effectHandle->setInput(imageWidth, imageHeight, frame.data, pixel_format_rgba);
    // Get the processed buffer; the format matches the input format
    unsigned char* data = effectHandle->getOutput();
    cv::Mat framOut(imageHeight, imageWidth, CV_8UC4, data);
    cvtColor(framOut, framOut, cv::COLOR_RGBA2BGR);

    //cvtColor(framOut, framOut, cv::COLOR_RGBA2BGR);
    imshow("EffectBaseApp", framOut);
}

// Destroy IEffectHandle and IEffectManager
effectManager->releaseHandle(effectHandle);
destroyEffectManager(effectManager);
```


The demo logic is simple and easy to understand — it mainly leverages the `EffectManager` module's capabilities. For the specific usage of `EffectManager`, refer to the Qt demo documentation.

&nbsp;

<span id="810129f5"></span>
# C# Demo

Like the Win32 demo, the C# demo reuses the capabilities wrapped by the `EffectManager` module and provides an example of capturing camera video streams with C# for effect processing.

> **Note ⚠️**  Currently the standard Windows product only provides the Qt Demo online. If you need the C# Demo, please contact us separately to obtain it.


<span id="dded49ce"></span>
## Recommended Development Environment


* .Net Core 3.1

* Visual Studio 2019


<span id="3a6e0532"></span>
## Project Structure


* `ByteEffect.cs` — the glue layer wrapping the C++ EffectManager module; see the EffectManager module description in the Qt demo

* `Program.cs` — uses OpenCV to demonstrate the basic beauty effect processing flow


<span id="e72d723d"></span>
## Core Logic Description

```Plain
// Load and initialize the Angle dynamic library symbols
ByteEffect.loadEGLDLL();

var exePath = System.Diagnostics.Process.GetCurrentProcess().MainModule.FileName;
var appDir = Path.GetDirectoryName(exePath);

var licensePath = $@"{appDir}\effect\license\license.bag";
var licensePathPtr = MallocIntPtr(licensePath);

// Verify the license; on failure, pull the latest license locally
var licenseStatus = ByteEffect.checkLicenseFile(licensePathPtr);
if (licenseStatus != 0) {
    Console.WriteLine($@"license error: {licenseStatus}");

    // replace your key and secret
    string key = "biz_license_tool_test_keyb2cc169b1c7340dfaa2c70027acb99f5";
    string secret = "dc5468fe3f3b555cda0d04b9f856f5a3";

    var licenseDir = $@"{appDir}\effect\license\";
    if (!Directory.Exists(licenseDir))
        Directory.CreateDirectory(licenseDir);

    RequestLicenseFile(licensePath, key, secret);
}

// Create the EffectHandle object
IntPtr effectHandle = ByteEffect.createEffectHandle();

var resourceDir = $@"{appDir}\..\..\..\resource";
var modelDirPtr = MallocIntPtr($@"{resourceDir}\model");

var composerPath = $@"{resourceDir}\ComposeMakeup";
var filterPath = $@"{resourceDir}\Filter";
var stickerPath = $@"{resourceDir}\stickers_resource\stickers";

// Initialize the Effect SDK
ByteEffect.initResource(effectHandle, licensePathPtr, modelDirPtr);

// Set filter and filter intensity
#if TEST_FILTER
var filterPathPtr = MallocIntPtr(filterPath + "\\Filter_02_14");
ByteEffect.setFilter(effectHandle, filterPathPtr);
ByteEffect.setFilterIntensity(effectHandle, 0.8f);
FreeIntPtr(filterPathPtr);
filterPathPtr = IntPtr.Zero;
#endif

// Set sticker
#if TEST_STICKER
// only one sticker can exist at the same time
var stickerPathPtr = MallocIntPtr(stickerPath + "\\heimaoyanjing");
ByteEffect.setSticker(effectHandle, stickerPathPtr);
FreeIntPtr(stickerPathPtr);
stickerPathPtr = IntPtr.Zero;

// if you want to reset sticker, you can do like this code
// var emptyPathPtr = MallocIntPtr(stickerPath + "");
// ByteEffect.setSticker(effectHandle, stickerPath + "");
// FreeIntPtr(emptyPathPtr);
#endif

// Set virtual background
#if TEST_VIRTUAL_BACKGROUND
var mattingPathPtr = MallocIntPtr(stickerPath + "\\matting_bg");
var bgPathPtr = MallocIntPtr(resourceDir + "\\bg.png");
var keyPtr = MallocIntPtr(RENDER_CACHE_TETURE_KEY);
ByteEffect.setSticker(effectHandle, mattingPathPtr);
ByteEffect.setRenderCacheTexture(effectHandle, keyPtr, bgPathPtr);
FreeIntPtr(mattingPathPtr);
FreeIntPtr(bgPathPtr);
FreeIntPtr(keyPtr);
mattingPathPtr = IntPtr.Zero;
bgPathPtr = IntPtr.Zero;
keyPtr = IntPtr.Zero;
#endif

// Set beauty
#if TEST_COMPOSER
var beautyPathPtr = MallocIntPtr(composerPath + "\\beauty_IOS_lite");
var reshapePathPtr = MallocIntPtr(composerPath + "\\reshape_lite");

IntPtr[] nodes = new IntPtr[3];
nodes[0] = beautyPathPtr;
nodes[1] = reshapePathPtr;

// Set style makeup
#if TEST_STYLE_MAKEUP
// set style makeup resource
var aidouPathPtr = MallocIntPtr(composerPath + "\\style_makeup\\aidou");
nodes[2] = aidouPathPtr;
ByteEffect.updateComposerNodes(effectHandle, nodes, 3);
#else
ByteEffect.updateComposerNodes(effectHandle, nodes, 2);
#endif

// Set the intensity of different sub-items
// Locate the specific beauty sub-item using "prop package path, prop package tag"
// The tags inside each prop package (if any) may differ; refer to the code inside the 'BEDataManager' object in the Qt demo
// Or check the general API docs: https://cv-api.bytedance.com/doc/openapi/2036/200123
ByteEffect.updateComposerNodeIntensity(effectHandle, beautyPathPtr, "smooth", 0.7f);
ByteEffect.updateComposerNodeIntensity(effectHandle, beautyPathPtr, "whiten", 0.35f);
ByteEffect.updateComposerNodeIntensity(effectHandle, beautyPathPtr, "sharp", 0.7f);
ByteEffect.updateComposerNodeIntensity(effectHandle, reshapePathPtr, "Internal_Deform_Overall", 0.8f);
ByteEffect.updateComposerNodeIntensity(effectHandle, reshapePathPtr, "Internal_Deform_Eye", 0.35f);

// if you want remove composer
// reset intensity
// ByteEffect.updateComposerNodeIntensity(effectHandle, beautyPathPtr, "smooth", 0.0f);
// after reset intensity, if you want remove beauty_IOS_lite, code like this
// and it also remove (smooth, whiten, sharp)
// {
//  //    nodes[0] = reshapePathPtr;
//    ByteEffect.updateComposerNodes(effectHandle, nodes, 1);
//  }
FreeIntPtr(beautyPathPtr);
FreeIntPtr(reshapePathPtr);
beautyPathPtr = IntPtr.Zero;
reshapePathPtr = IntPtr.Zero;
#endif

var window = new Window("EffectDemo");
var image = new Mat();

while (true) {
    capture.Read(image);
    if (image.Empty())
        break;

    Cv2.Flip(image, image, FlipMode.Y);

    // Cv2.CvtColor(image, image, ColorConversionCodes.BGR2RGBA);
    Cv2.CvtColor(image, image, ColorConversionCodes.BGR2BGRA);

    // Set the image buffer to be processed
    // The format must be: BGR/BGRA/RGB/RGBA/I420; other formats must be converted before use
    ByteEffect.setInput(effectHandle, image.Width, image.Height, image.Data, (int)ByteEffect.BytePixelFormat.pixel_format_bgra);

    // Get the processed buffer; the format matches the input format
    IntPtr outImage =  ByteEffect.getOutput(effectHandle);

    var frameOut = new Mat(image.Height, image.Width, MatType.CV_8UC4, outImage);
    Cv2.CvtColor(frameOut, frameOut, ColorConversionCodes.BGRA2BGR);
    // show image
    window.ShowImage(frameOut);

    int flag = Cv2.WaitKey(1);
    if (flag >= 0) {
        break;
    }
}

FreeIntPtr(licensePathPtr);
FreeIntPtr(modelDirPtr);
licensePathPtr = IntPtr.Zero;
modelDirPtr = IntPtr.Zero;

// Destroy Effect SDK resources
ByteEffect.releaseEffectHandle(effectHandle);
ByteEffect.unloadEGLDLL();
```


The demo logic is simple and easy to understand — it mainly leverages the C++ `EffectManager` module's capabilities. For the specific usage of `EffectManager`, refer to the Qt demo documentation.
