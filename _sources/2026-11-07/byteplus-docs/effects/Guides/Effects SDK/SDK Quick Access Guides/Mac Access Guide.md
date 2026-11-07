---
title: "Mac Access Guide"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-mac-access-guide"
---

<span id="6ee341ed"></span>
## Mac platform provides a native App demo written in Objective‑C for real‑time camera capture and special effect processing. Its UI and effect capabilities are aligned with the Qt demo on Windows.

Recommended development environment


* Xcode 12+

* MacOS 10.11+

* Cocoapod 1.7.1+


⚠️ Note: The OpenGL context on Mac must be 3.2 Core Profile. When creating NSOpenGLContext, specify `NSOpenGLProfileVersion3_2Core`. For versions 3.2 and above, comprehensive testing must be completed during integration to ensure all assets load correctly.

<span id="2279a24f"></span>
## Main Components & Key API Reference


* **EffectHandle**: Wraps the underlying C interfaces of the Effect SDK and exposes APIs for effect processing.

   * `initEffect` / `releaseEffect`: Manage the lifecycle of EffectHandle instances

   * `setOpenGLContext`: Assign NSOpenGLContext; must be 3.2 Core Profile

   * `updateComposerNodes` / `setFilterPath` / `setStickerPath`: Configure desired effects

   * `processWithBuffer`: Process image buffers

* **BEImageUtils**: Provides conversion between CVPixelBuffer and RGBA/BGRA/I420 formats

   * `transforCVPixelBufferToBuffer`: Convert CVPixelBuffer to buffer

   * `transforBufferToBuffer`: Convert between different buffer formats

* **BERequester / BELicenseCheck**: Demonstrates online authentication, license download and validation. Refer to https://docs.byteplus.com/en/docs/effects/docs\-online\-license\-guide for authentication principles and workflow.

* **BEEffectDataManager**: Manages effect asset packages, including usage of tag fields inside asset bundles. If you have questions about using a specific asset, refer to the implementation in BEEffectDataManager.

* **BEAlgorithmTask**: Base class for algorithm detection tasks (face, gesture etc.)

   * `initWithProvider`: Construct a detection task. Different algorithms require different resource files. Use `BEAlgorithmResourceHelper` in the project to fetch required algorithm resources.

   * `initTask`: Initialize the detection task

   * `process`: Run algorithm inference

   * `setConfig`: Set algorithm parameters. Each algorithm has unique parameter keys defined in its header file.

   * `destroyTask`: Destroy the detection task


<span id="6ac8d157"></span>
## Project Structure


* `EffectManager`: Wraps the underlying SDK C interfaces. Integrators typically call APIs from this module directly.

* `Algorithm`: Encapsulation code for algorithm integration (face detection, gesture detection, etc.)

* `ByteEffects`: UI layer demonstrating consumption of interfaces exposed by Algorithm and EffectManager


<span id="e5a11a2a"></span>
### Integrating only effect features (beauty, filter, makeup, stickers, etc.)

Compile EffectManager into a static library and invoke the EffectHandle APIs. High\-level workflow:

```Plain
// Create beauty effect handle
handle = [[EffectHandle alloc] initWithPath:licenseDirPath modelDir:modelDirPath];

// Assign NSOpenGLContext (must be NSOpenGLProfileVersion3_2Core)
[handle setOpenGLContext];

// Initialize Effect SDK
// Must run under valid GL context: use lockOpenGLContext/unlockOpenGLContext. See demo source code.
[handle initEffect];

// Pass asset package path to enable target effects
[handle updateComposerNodes:@""];

// Feed image buffer for effect processing; returns processed texture
// Demo defaults to BGRA input. For other formats, modify demo or use BEImageUtils for conversion.
// Must run under valid GL context.
[handle processWithBuffer];

// Release handle
// Must run under valid GL context.
[handle releaseEffect];
```


<span id="c0d4f63f"></span>
### Integrating algorithm features (face detection, gesture detection, body keypoints, etc.)

Compile EffectManager and Algorithm into static libraries. Use BEAlgorithmTaskFactory to create detection tasks. High\-level workflow:

```Plain
// Complete Effect SDK initialization as described above

// Create algorithm detection task
tsk = [BEAlgorithmTaskFactory create:[BEAlgorithmKey create:key isTask:YES] provider:[[BEAlgorithmResourceHelper alloc] initWithLicense:licenseDirPath]];

// Initialize task
[tsk initTask];

// Set algorithm configuration
[tsk setConfig:[BEAlgorithmKey create:MOUTH_MASK_KEY isTask:NO] p:[NSNumber numberWithBool:selected]];

// Run detection and retrieve results
result = [tsk process:buffer width:iWidth height:iHeight stride:iWidth*4 format:BEF_AI_PIX_FMT_BGRA8888 rotation:0];
```


Refer to the `BEAlgorithmVC` module in the demo for full algorithm usage examples.

<span id="04f0f55f"></span>
### Debugging the demo source code

Configure the build environment first. The source bundle already contains Effect SDK headers and resources:


* Headers: `include/BytedEffectSDK`

* Libraries: `libs`

* Model files: `ByteEffects/Resource/ModelResource.bundle`

* Beauty assets: `ByteEffects/Resource/ComposeMakeup.bundle`

* Filter assets: `ByteEffects/Resource/FilterResource.bundle`

* Sticker assets: `ByteEffects/Resource/StickerResource.bundle`

> When integrating, use the official SDK archive instead of the library files inside the demo directory for easier troubleshooting.


<span id="adc87267"></span>
#### Build & Run

Run `pod init` in the demo root directory. After pod installation completes, open `ByteEffects.xcworkspace` and configure your developer account AppID before building.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d03f32b33c1c4485aa34e7e3f1ed74cb~tplv-goo7wpa0wc-image.image) </span>

⚠️ Note: The default SDK in the project is built for x86_64. If you are using an M\-series Mac, replace libraries under `libs` with arm64 SDK binaries.

<span id="230c89a4"></span>
## Electron

The Electron demo ships prebuilt EffectManager modules for both Mac and Windows. The API usage is identical to the native demo described above.

Recommended development environment


* Windows: Visual Studio 2019

* Electron: v20.0.2

* Node: v16.16.0


<span id="faca39e4"></span>
### Core Logic

<span id="12bacf2f"></span>
#### Online Authorization & Validation

```Plain
const effectNode = require('../plugin/effect_node/effect_node.node');

// Check license validity. success returns 0; other error codes require license re-download
var licenseStatus = effectNode.checkLicenseStatus(licenseDir + 'license.bag');

// Generate request payload using key and secret
var requestContent = effectNode.getRequestContent(key, secret);

function licenseRequest(content, secret) {
  const {net} = require('@electron/remote');
  const request = net.request({
    headers: {
      'Content-Type': 'application/json',
    },
    method: 'POST',
    url: 'https://cv-tob.bytedance.com/v1/api/sdk/tob_license/getlicense'
  });
  request.write(content);
  request.on('response', (response) => {
    console.log(`**statusCode:${response.statusCode}`);
    if (response.statusCode != 200) {
      // handle error code
    }
    response.on("data", (chunk)=>{
      const jsonObj = JSON.parse(chunk);
      console.log("status_code:", jsonObj.status_code);
      if (jsonObj.status_code != 0) {
        // handle error code
      } else {
        // persist license locally
        var license = effectNode.writeLicenseResult(secret, jsonObj.data, jsonObj.digest, licenseDir + 'license.bag');
      }
    })
  });
  request.end();
  return 0;
}
```


<span id="da5a931a"></span>
#### Effect Processing Logic

```Plain
// Load EGL dynamic library, only required on Windows
effectNode.loadEGLDLL();

// Create EffectHandle instance
effectHandle = effectNode.createEffectObject();

// Initialize handle with license.bag fetched from online authorization
effectHandle.initResource(licenseDir + 'license.bag', modelDir);

// Retrieve native C++ interface for camera frame processing
var effectInterface = effectHandle.effectInterface();

// Pass interface to video capture module if available
// videoCap.setEffectInterface(effectInterface);

// Set asset package path and enable target effects
effectHandle.updateComposerNodes({
  "composerDir": composerNodeDir,
  "tags": tags,
});

// Update effect intensity
effectHandle.updateComposerNodeIntensity(nodePath, key, value);

// Set filter asset and intensity (range: 0.0 - 1.0)
effectHandle.setFilter(filterpath);
effectHandle.setFilterIntensity(value);

// Set sticker asset
effectHandle.setSticker(stickerPath);

// Feed input image buffer
// @param buffer: ArrayBuffer image data
// @param width: image width
// @param height: image height
// @param format: 0 for RGBA, 1 for BGRA
effectHandle.setInput(buffer, width, height, format);

// Get processed output buffer (same format and dimensions as input)
effectHandle.getOutput();

// Set cached render texture, used for virtual background
// @param key: texture identifier
// @param path: absolute file path
effectHandle.setRenderCacheTexture(key, path);

// Toggle synchronous resource loading. Default: async
// @param needLoad: boolean
effectHandle.setNeedLoadResource(needLoad);
```


Refer to preceding demo documentation for full EffectHandle usage details.
