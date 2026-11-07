---
title: "iOS Access Guide (V4.1.0.1 and later)"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-ios-v4101-access-guide"
---

<span id="iOS Access Guide"></span>
# iOS Access Guide

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">This quick access guide is for <strong>Version</strong> <strong>4.1.0.1 and later</strong>.</div>


<span id="Importing SDK to Project"></span>
# Importing SDK to Project

If CocoaPods is used in the project, go to step 2; if not, go to step 1.


1. In the root directory of the project, execute `pod init && pod install` to obtain the Podfile file.

2. Open the iossample folder, and copy the **BytedEffectSDK.podspec**, **libeffect\-SDK.a**, and **include** folder files to the root directory of your project.


Note: From **V4.4.3**, BytedEffectSDK.podspec changes to **EffectsARSDK.podspec**


3. Open the Podfile file, and add a new line: `pod 'BytedEffectSDK', :path => './'.`

4. Execute `pod install` and open [Project Name].xcworkspace. **BytedEffectSDK** exists in the **Pods/Development** Pods directory.

5. Copy the provided material package (typically the resource folder) to the project. Also, you need to check with your Copy Bundle Resource in the project of Xcode. The location is in this image:


<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/16902352878f487e926fcffc686d6575~tplv-em5hxbkur4-noop.image?width=1684&height=1626) </span>

<span id="Integrating SDK in Code"></span>
# Integrating SDK in Code

This section describes how to integrate the SDK with the Objective\-C code encapsulated in the sample. For details on how to use the C APIs provided in the CV SDK for integration in your project, refer to [Developer API Document](doc:c-api).

<span id="Before You Start"></span>
## Before You Start


1. Copy files in `Core/Core` directory of project `iossample` into your own project.

2. To use the video capture and drawing APIs provided in the sample (This step is not required if the streaming or image processing functions are available in your project), copy the files under the `Common/Common` directory to your project. For more information, refer to [Appendix: instruction on copying materials](https://docs.byteplus.com/effects/docs/android-v4101-access-guide#appendix-instruction-on-copying-materials).

3. If your SDK version is **4.2.1**, need to change the `LICENSE_MODE` in the BEEffectLicenseHelper.mm to `OFFLINE_LICENSE`, and modify `LICENSE_NAME` in the Config.h to your own trial license matched bundle ID.

4. If your SDK version is **4.2.3 and later**, need to change the `LICENSE_MODE` in the BELicenseHelper.mm to `OFFLINE_LICENSE`, and modify `LICENSE_NAME` in the Config.h to your own trial license matched bundle ID.


The code mentioned above may have dependencies on other code in the sample. You may copy the dependent code to your project as well. You can refer to [Sample App Code Structure](https://docs.byteplus.com/effects/docs/ios-v4101-sample-file) for information about other code features.

<span id="Deploy Procedure"></span>
## Deploy Procedure

SDK‘s packaged interface are mainly in `Core` module. Every feature (e.g. special effects, algorithms, image quality) has a unique packaged interface, which can be used separately.

<span id="Using Special Effects"></span>
### Using Special Effects

Special Effects SDK's unified interface package is `BEEffectManager`, using this SDK can be divided into 3 stages:


1. Initialize Special Effects SDK (Section 1).

2. Use Special Effects SDK for image processing (Section 2).

3. Set parameters for Special Effects SDK, e.g: set beauty effects, stickers, filters (Section 3).


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">All operations of SDK should be dependent on OpenGL threading. Ensure that all function calls of the SDK are in the same GIContext.</div>


<span id="1. Initialize SDK"></span>
#### 1. Initialize SDK

Methods of initializing SDK：

```objectivec
- (instancetype)initWithResourceProvider:(id<BEEffectResourceProvider>)provider;
```


BytePlus Effects SDK's usage depends on openGL environment, before calling SDK functions, call function to set the context:

```objectivec
[EAGLContext setCurrentContext:context];
```


If there is no GIContext in your project, you can use the code below to create:

```objectivec
EAGLContext *context = [[EAGLContext alloc] initWithAPI:kEAGLRenderingAPIOpenGLES3];
```


<span id="2. Use SDK for image processing"></span>
#### 2. Use SDK for image processing

SDK's handling methods are mainly `BEEffectManager#processTexture:outputTexture:width:height:rotate:timeStamp`,

```objectivec
/// @brief SDK handling
/// @param texture input texture
/// @param outputTexture output texture
/// @param width width
/// @param height height
/// @param rotate algorithm detection angle
/// @param timeStamp time stamp
- (bef_effect_result_t)processTexture:(GLuint)texture outputTexture:(GLuint)outputTexture width:(int)width height:(int)height rotate:(bef_ai_rotate_type)rotate timeStamp:(double)timeStamp;
```


It can only handle 2D texture and transfer the result into the input 2D texture's `outputTexture`. If 2D texture cannot be obtained directly in the current project, you can use `BEImageUtils` to change the format. This class can be used for format changing between `CVPixelBuffer`, `Texture` and `Buffer`. For more information, refer to [Appendix：BEImageUtils Usage](doc:ios-v4101-access-guide#appendix%EF%BC%9Abeimageutils-usage).

**EXAMPLE**

```objectivec
id<BEGLTexture> texture = [self.imageUtils transforCVPixelBufferToTexture:pixelBuffer];
// obtain corresponding OpenGL texture
int inputTexture = texture.texture;
// obtain corresponding texture's width and height
int inputWidth = texture.width;
int inputHeight = texture.height;
```


This function also needs a parameter `timeStamp`, the time for the current frame. You can refer to [Appendix: obtain timeStamp](doc:ios-v4101-access-guide#appendix%EF%BC%9Atimestamp-obtain) on how to obtain it.

Output of the function is 2D texture, if there is no existing texture, you can use `BEImageUtils` to create.

**EXAMPLE**

```objectivec
BEPixelBufferGLTexture *outputTexture = [self.imageUtils getOutputPixelBufferGLTextureWithWidth:texture.width height:texture.height format:BE_BGRA];
// obtain corresponding OpenGL texture
int outTexture = outputTexture.texture;
// obtain corresponding CVPixelBuffer
CVPixelBufferRef outputPixelBuffer = outputTexture.pixelBuffer;
```


When you are testing the deployment, it is recommended using `BEImageUtils` to transform to `BECVPixelBuffer`. Therefore, you can supervise the input & output of the SDK, troubleshoot possible issues.

<span id="3. SDK parameter settings (e.g. beauty effects, sticker, filters)"></span>
#### 3. SDK parameter settings (e.g. beauty effects, sticker, filters)

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">You should set SDK parameters after SDK initialization. Use the same thread as SDK image processing to avoid possible issues.</div>


<span id="(1) Set Beauty effects, face shaping, makeup effects"></span>
##### (1) Set Beauty effects, face shaping, makeup effects

Beauty effects, face shaping and makeup effects's parameters settings are using the same interface. Normally, it takes 2 steps for beauty effects to make effect.


1. Set paths corresponding to materials.

2. Set effects' intensity in materials (usually the default intensity is 0, therefore there will be no effects if step 2 is skipped).


**Interface of setting material path:** 

```objectivec
/// @brief set special effects materials
/// @details: Set all ComposeMakeup.bundle's features，including beauty effects, body shaping, face shaping and makeup effects.
/// @param nodes: Path of special effects materials relative to ComposeMakeup.bundle/ComposeMakeup
- (void)updateComposerNodes:(NSArray<NSString *> *)nodes;

/// @brief set special effects materials
/// @details: Set all ComposeMakeup.bundle's features，including beauty effects, body shaping, face shaping and makeup effects.
/// @param nodes: Path of special effects materials relative to ComposeMakeup.bundle/ComposeMakeup
/// @param tags: Every speical effects materials corresponds a tag, tag contains some configuration passed to SDK materials. 
- (void)updateComposerNodes:(NSArray<NSString *> *)nodes withTags:(NSArray<NSString *> *)tags;

// Example
[self.manager updateComposerNodes:[NSArray arrayWithObject:@"beauty_IOS_lite"]];
```


The material path is relative to path of `ComposeMakeup.bundle/ComposeMakeup`. For more information on the file structure of material packages, refer to [Resource Package Structure](doc:resource-package-structure-v421-and-later).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">SDK does not save configured materials internally, therefore you need to add all materials paths which need to be effective on every calling.</div>


**When setting materials, interface for special effects intensity:** 

```objectivec
/// @brief Update some nodes' intensity in speical effects combination
/// @param node: Path of special effects materials relative to ComposeMakeup.bundle/ComposeMakeup
/// @param key: Feature key of materials
/// @param intensity: Value from 0-1
- (void)updateComposerNodeIntensity:(NSString *)node key:(NSString *)key intensity:(float)intensity;

// Example
[self.manager updateComposerNodeIntensity:@"beauty_IOS_lite" key:@"whiten" intensity:0.8];
```


Take beauty effects materials as an example, you need to use key to control which feature's intensity needs to be adjusted (whether it is toning, buffing or sharpening). The relation between materials' key and feature can be found in [Functions of Material Keys](doc:functions-of-resource-keys-v421-and-later).

<span id="(2) Set stickers"></span>
##### (2) Set stickers

**Set stickers interface:** 

```objectivec
/// @brief set stickers path
/// @details File Path of sticker materials relative to StickerResource.bundle，when path is null, sticker is off
/// @param path: relative path of sticker
- (void)setStickerPath:(NSString*) path;

// Example
[self.manager setStickerPath:@"baibianfaxing"];
```


The sticker path is the relative path to `StickerResource.bundle/stickers` in the materials package.

<span id="(3) Set filters"></span>
##### (3) Set filters

**Filters setting interface:** 

```objectivec
/// @brief set filters path
/// @details File path of filters relative to FilterResource.bundle/Filter，when path is null, filter is off
/// @param path relative path of filter
- (void)setFilterPath:(NSString *) path;

/// @brief setting filter intensity
/// @param intensity: Value from 0-1
- (void)setFilterIntensity:(float)intensity;

// Example
[self.manager setFilterPath:@"/Filter_01_38"];
[self.manager setFilterIntensity:0.8];
```


The filter path is the relative path to `FilterResource.bundle/Filter` in materials package.

<span id="Using Algorithms"></span>
### Using Algorithms

Algorithms code is packaged under `Core/Core/Algorithm`, each algorithm is packaged individuallyl, and does not have dependencies on each other. For example, package for face detection is `BEFaceAlgorithmTask`, package for gesture recognition is `BEHandAlgorithmTask`. There is a base class `BEAlgorithmTask` defining all algorithms' unified interface. We take face detection as an example to describe the deployment procedure.

<span id="1. Algorithm Initialization"></span>
#### 1. Algorithm Initialization

Algorithms initialization function is defined in `BEAlgorithmTask`.

```objectivec
- (instancetype)initWithProvider:(id<BEAlgorithmResourceProvider>)provider;
```


`BEAlgorithmResourceProvider` provides some resource information to algorithms (e.g. model files). Different algorithms have different resources, hence has its unique definition. The definition of face detection shows in below:

```objectivec
@protocol BEFaceResourceProvider <BEAlgorithmResourceProvider>

- (const char *)faceModel;
- (const char *)faceExtraModel;
- (const char *)faceAttrModel;

@end
```


`ResourceProvider` defined by each algorithm can be found in the corresponding header file. When you are using the algorithm, you need to have a class to realize such protocol. Normally, you can use `BEAlgorithmResourceHelper` in your project, this class realizes all algorithms' `ResourceProvider`.

The contents above describe creating instance for algorithms. After that, you need to call initialization function to finish the initialization.

```objectivec
/// @brief algorithm initialization
- (int)initTask;
```


Returned value tells initialization result.

<span id="2. Algorithm Detection"></span>
#### 2. Algorithm Detection

Algorithm detection function is also defined in `BEAlgorithmTask`.

```objectivec
/// @brief Algorithm calling
/// @param buffer buffer
/// @param width width
/// @param height height
/// @param stride stride，normally width * 4
/// @param format format
/// @param rotation rotation
- (id)process:(const unsigned char *)buffer width:(int)width height:(int)height stride:(int)stride format:(bef_ai_pixel_format)format rotation:(bef_ai_rotate_type)rotation;
```


All algorithms detection function is this, it needs to be inputted with a buffer and some information. If there is only `CVPixelBuffer` in your current project, you can use `BEImageUtils` to transform.

```objectivec
BEBuffer *buffer = [self.imageUtils transforCVPixelBufferToBuffer:pixelBuffer outputFormat:BE_BGRA];
unsigned char *inputBuffer = buffer.buffer;
int width = buffer.width;
int height = buffer.height;
int stride = buffer.bytesPerRow;
```


Result of algorithm detection is an id in base statement, hence the different between each algorithm. For example, result of face detection is `BEFaceAlgorithmResult`. The detection result of each algorithm can be found in its corresponding header file.

<span id="3. Algorithm Parameter Setting"></span>
#### 3. Algorithm Parameter Setting

Function defines algorithm parameter setting:

```objectivec
/// @brief Set algorithm parameter
/// @param key: paramter key
/// @param p: paramter value
- (void)setConfig:(BEAlgorithmKey *)key p:(NSObject *)p;
```


Key is the type of parameter, p is the parameter value. Parameter type of each algorithm can be seen in algorithm's definition. For face detection:

```objectivec
@interface BEFaceAlgorithmTask : BEAlgorithmTask

+ (BEAlgorithmKey *)FACE_106;
+ (BEAlgorithmKey *)FACE_280;
+ (BEAlgorithmKey *)FACE_ATTR;
+ (BEAlgorithmKey *)FACE_MASK;
+ (BEAlgorithmKey *)MOUTH_MASK;
+ (BEAlgorithmKey *)TEETH_MASK;

@property (nonatomic, assign) unsigned long long initConfig;
@property (nonatomic, assign) unsigned long long detectConfig;
@property (nonatomic, assign) int maxFaceNum;

@end
```


It has keys of `FACE_280`, `FACE_ATTR`. We can use `setConfig:p` function to set if turn on 280 keypoints detection:

```objectivec
[self.algorithmTask setConfig:BEFaceAlgorithmTask.FACE_280 p:[NSNumber numberWithBool:YES]];
```


The code above means turn on 280 keypoints detection in face detection algorithm.

<span id="Appendix: Using video capture, drawing interface in Sample"></span>
# Appendix: Using video capture, drawing interface in Sample

`Common` module provides `BEVideoSourceProvider` interface，it can achieve camera data capturing, output of video image streams，every mode has an unique class. The call\-back proxy of `BEVideoCapture` is `BEVideoCaptureDelegate`. Call\-back methods of different modes are different, details will be discussed below.

<span id="Camera Preview Mode"></span>
### Camera Preview Mode

Interface corresponding to camera preview mode is `BEVideoCapture`. Inside, it uses system's `AVFoundation` feature to capture camera data.

**Initialize instance:** 

```objectivec
_capture = [[BEVideoCapture alloc] init];
_capture.delegate = self;
```


Using camera preview mode, the required proxy method is:

```objectivec
/// @brief output CMSampleBufferRef call-back
- (void)videoCapture:(id<BEVideoSourceProtocol>)source didOutputSampleBuffer:(CMSampleBufferRef)sampleBuffer withRotation:(int)rotation;
```


<span id="Image Processing Mode"></span>
### Image Processing Mode

Interface corresponding to image processing mode is `BEImageCapture`. Inside, it simulates image's buffer to a video streaming to output by using `NSTimer`

**Initialize instance:** 

```objectivec
_capture = [[BEImageCapture alloc] initWithImage:self.image];
_capture.delegate = self;
```


Using image processing mode, the required proxy method is:

```objectivec
/// @brier output buffer call-back
/// @param source source
/// @param buffer buffer
/// @param width width
/// @param height height
/// @param bytesPerRow bytesPerRow
/// @param format buffer format
/// @param timeStamp time stamp
- (void)videoCapture:(id<BEVideoSourceProtocol>)source didOutputBuffer:(unsigned char *)buffer width:(int)width height:(int)height bytesPerRow:(int)bytesPerRow format:(OSType)format timeStamp:(double)timeStamp;
```


<span id="Video Processing Mode"></span>
### Video Processing Mode

Interface corresponding to video processing mode is `BELocalVideoCapture`. Inside, it decodes local videos to `CMSampleBuffer` to output by using `AVAssetReader`.

**Initialize instance:** 

```objectivec
_capture = [[BELocalVideoCapture alloc] initWithAsset:self.asset];
_capture.delegate = self;
```


Using video processing mode, the required proxy method is:

```objectivec
/// @brief output CMSampleBufferRef call-back
- (void)videoCapture:(id<BEVideoSourceProtocol>)source didOutputSampleBuffer:(CMSampleBufferRef)sampleBuffer withRotation:(int)rotation;
```


<span id="Handling & Drawing Output"></span>
### Handling & Drawing Output

In `Common`, `BEGLView` is used to inherit `GLKView`. Inside, it uses `openGL` to draw textures. If there is no method that draws CV SDK output image to the screen in your project, you can use this class. The method of drawing textures is shown below:

```objectivec
- (void)renderWithTexture:(unsigned int)name
                     size:(CGSize)size
                  flipped:(BOOL)flipped
      applyingOrientation:(int)orientation
                  fitType:(int)fitType;
```


<span id="Appendix：timeStamp Obtain"></span>
# Appendix: Obtain timeStamp

If you are using SDK to handle `CMSampleBufferRef` output by the camera, you can obtain by doing:

```objectivec
CMTime sampleTime = CMSampleBufferGetPresentationTimeStamp(sampleBuffer);
double timeStamp = (double)sampleTime.value/sampleTime.timescale;
```


Otherwise, obtain by doing:

```objectivec
double timeStamp = [[NSDate date] timeIntervalSince1970]];
```


<span id="Appendix：BEImageUtils Usage"></span>
# Appendix: BEImageUtils Usage

<span id="Create empty texture"></span>
### Create empty texture

**Code:** 

```objectivec
BEPixelBufferGLTexture *outputTexture = [self.imageUtils getOutputPixelBufferGLTextureWithWidth:texture.width height:texture.height format:BE_BGRA];
// Obtain corresponding OpenGL texture
int outTexture = outputTexture.texture;
// Obtain corresponding CVPixelBuffer
CVPixelBufferRef outputPixelBuffer = outputTexture.pixelBuffer;
```


<span id="Transform CVPixelBuffer to 2D texture"></span>
### Transform CVPixelBuffer to 2D texture

**Code:** 

```objectivec
id<BEGLTexture> texture = [self.imageUtils transforCVPixelBufferToTexture:pixelBuffer];
// Obtain corresponding OpenGL texture
int inputTexture = texture.texture;
// Obtain corresponding texture's height & width
int inputWidth = texture.width;
int inputHeight = texture.height;
```


<span id="Transform CVPixelBuffer to buffer"></span>
### Transform CVPixelBuffer to buffer

**Code:** 

```objectivec
BEBuffer *buffer = [self.imageUtils transforCVPixelBufferToBuffer:pixelBuffer outputFormat:BE_BGRA];
unsigned char *inputBuffer = buffer.buffer;
int width = buffer.width;
int height = buffer.height;
int stride = buffer.bytesPerRow;
```


<span id="Appendix：About GLThread example in the sample"></span>
# Appendix: About GLThread example in the sample

An explanation and example of the gl threads in one or two page views is given in sample for reference. It's in the `BEBaseVC.mm`.

```Plain
//    There are two threads in a page that need gl environment, namely SDK thread off-screen rendering and GLKView main thread rendering  
    //  So the same requires two shared glContext for each thread.
    //  Another problem is that if two threads and two glContext, when the second SDK is destroyed,
    //  If the first SDK is calling process, it will cause the environment to crash, so the second page needs to reuse the glContext of the previous page.  

    if (self.glContext == nil) {
        self.glContext = [BEGLUtils createContextWithDefaultAPI:kEAGLRenderingAPIOpenGLES3 sharegroup:self.glView.context.sharegroup];
    } else {
        self.glView.context = [BEGLUtils createContextWithDefaultAPI:kEAGLRenderingAPIOpenGLES3 sharegroup:self.glContext.sharegroup];
    }
    
    if ([EAGLContext currentContext] != self.glContext) {
        [EAGLContext setCurrentContext:self.glContext];
    }
```


<span id="Appendix：About must required head files for Swift bridge"></span>
# Appendix: About required head files for Swift bridge

When using Swift to bridge the OC code in our sample, the following header files must be imported:

```Plain
#import "BEEffectManager.h"
#import "BEEffectResourceHelper.h"
#import "BELicenseHelper.h"
```


If there is other module code that needs to be used, such as BEImageUtils, you can introduce other header files along with it.
