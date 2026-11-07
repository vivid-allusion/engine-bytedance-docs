---
title: "Android Access Guide (V4.1.0.1 and later)"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-android-v4101-access-guide"
---

<span id="Android Access Guide"></span>
# Android Access Guide

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">This quick access guide is for <strong>Version</strong> <strong>4.1.0.1 and later</strong>.</div>


<span id="Import SDK into Project"></span>
# Import SDK into Project


1. Decompress `byted_effect_andr.zip`, find file `effect-SDKXXX.aar`

2. Copy it to the main module in the project's (normally project refers to your app) `lib` directory (e.g. copy to directory `app/libs`, if `libs` directory does not exist, you can create a new one manually).

3. Open `build.gradle` in your main module (normally it is the app), and add SDK query path under android.


```Groovy
dependencies {
    //  api fileTree(include: ['*.jar', '*.aar'], dir: 'libs')  // in sample
    implementation fileTree(dir: 'libs', include: ['*.jar', '*.aar'])   // when you accessing
}
```



4. Then, add SDK reference in `dependencies` under your main module's `build.gradle`. SDK reference example: `implementation(name: 'effect-sdkXXX', ext: 'aar')`.

5. Add materials, copy the provided material package (normally the `resource` folder) into project's `assets`.


<span id="Integrate SDK into Code"></span>
# Integrate SDK into Code

The following guide describes the integration process of using Java code packaged in the Android sample. If you use BytePlus Effects SDK's provided C interface for integration, refer to section Developer API Document.

<span id="Before You Start"></span>
## Before You Start


1. Copy project `androidsample`'s `com.bytedance.labcv.core` module into your project, `core` module is the calling package of SDK.


(1). Calling package related to **special effects** is in class `EffectManager`.

(2). Calling package related to **basic algorithms** is in directory `algorithm`.


* `xxxTask` represents packages for different algorithms.


(3). Calling package related to **image quality** is in class `ImageQualityManager`.


2. Apply material copying code `com.bytedance.labcv.demo.task.UnzipTask` and related logic into your own project (without this step, materials cannot be used). For more information, refer to Appendix: instruction on copying materials.

3. If your SDK version is **4.2.1 or later**, you need to change the `_licenseMode` in the EffectLicenseHelper.java to `LICENSE_MODE_ENUM.OFFLINE_LICENSE`, and modify `Config.LICENSE_NAME` to your own trial license matched application ID.


All interfaces above are main interfaces, some code above might be dependent on other code in Sample, you can copy these into your own project.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



1. <div data-tips="true" data-tips-type="warning">Class name changing</div>



<div data-tips="true" data-tips-type="warning"><strong>Starting with version 4.4.3</strong>, <code>com.bytedance.labcv</code> has been changed to <code>com.effectsar.labcv</code> for security compliance reasons.</div>


<div data-tips="true" data-tips-type="warning">All locations of <code>com.bytedance.labcv</code> in the documentation have been changed to <code>com.effectsar.labcv</code> in the sample.</div>


<div data-tips="true" data-tips-type="warning">Include all class names containing the above names in the documentation, as well as the location in the preparation session, please note that replace them with <code>com.effectsar.labcv</code> when searching from sample.</div>



2. <div data-tips="true" data-tips-type="warning">AndroidX project note</div>



<div data-tips="true" data-tips-type="warning">If the main project is an <strong>androidx project</strong>, you need to add <code>android.enableJetifier=true</code> in <strong>gradle.properties</strong>.</div>


<span id="Deploy Procedure"></span>
## Deploy Procedure

Take Special Effects SDK as an example, Special Effects SDK's unified interface package is `EffectManager`, using this SDK can be divided into 3 stages:


1. Initialize Special Effects SDK (Section 1).

2. Use Special Effects SDK for image processing (Section 2).

3. Set parameters for Special Effects SDK, e.g: set beauty effects, stickers, filters (Section 3).


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><strong>All operations of SDK should be in OpenGL threading.</strong> If you want to integrate our SDK into up\-streaming (pushing) SDK, you can directly run in a customized beauty effects interface provided by up\-streaming SDK. Or if you are in the local environment, you should use BytePlus Effects SDK together with <code>GLSurfaceView</code> (in OpenGL environment provided by <code>GLSSurfaceView</code>).</div>


<span id="1. Initialize Special Effects SDK"></span>
### 1. Initialize Special Effects SDK

SDK initialization should be run after OpenGL environment initialization is finished. If you want to run in `onSurfaceCreated` (when you are using up\-streaming SDK), you need to call the following functions:

```Java
mEffectManager = new EffectManager(this, new EffectResourceHelper(this));
mEffectManager.setOnEffectListener(this);
int ret =  mEffectManager.init();
```


EffectManager Parameter Explanation :

```Java
public EffectManager(Context context, EffectResourceProvider mResourceProvider, EffectLicenseProvider mLicenseProvider)
```



|Parameter |Explanation |
|---|---|
|context |The context object, used to access the application environment information. |
|mResourceProvider |The implementation object of the material resource management interface, used to obtain the required material resource information. |
|mLicenseProvider |The implementation object of the authorization management interface, used to obtain the information related to authorization. |


<span id="2. Use SDK for special effects processing"></span>
### 2. Use SDK for special effects processing

**Supported input data type:** 


|**Supported data type** |**Supported data format** |
|---|---|
|texture |OES，2D |


Calling image processing should be ran in `onDrawFrame` (If you are using up\-streaming SDK, you can call it directly in interface provided by up\-streaming SDK), the corresponding functions are:

```Java
 // Convert input texture to 2D texture with upright face
 ProcessInput input = transToPortrait();
 // Prepare frame buffer texture object
 int dstTexture = mImageUtil.prepareTexture(input.getWidth(), input.getHeight());
 // Conduct special effects operation, output texture is 2D texture with upright face
  boolean ret = mEffectManager.process(input.getTexture(),dstTexture, input.getWidth(),input.getHeight(),input.getSensorRotation(), mImageSourceProvider.getTimestamp());
```


About transToPortrait() method, refer to the Appendix.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If up\-streaming SDK's default input texture is with rotation angles, you need to adjust your code to adapt with up\-streaming SDK. You can refer to the following code, it transforms the texture outputted by Special Effects SDK back to original angles.</div>


```Java
ImageUtil.Transition transition = new ImageUtil.Transition().rotate(mImageSourceProvider.getOrientation()).flip(false, mImageSourceProvider.isFront()).reverse();
int texture = mImageUtil.transferTextureToTexture(dstTexture,BytedEffectConstants.TextureFormat.Texure2D,
                       input.getWidth(), input.getHeight(),transition);    
```


**Process interface parameter documentation:** 


|**Parameter** |**Description** |
|---|---|
|srcTexture |Input texture ID, it is required to be an image with the upright face. If you are using front cameras, mirroring operation needs to be conducted. |
|dstTexture |Output texture ID |
|width |Input texture width |
|height |Input texture height |
|sensorRotation |Phone angle, obtain from phone sensors |
|timeStamp |Current time (for more details, refer to Appendix: obtain timeStamp) |


**Process results：** 

Output of process method is rendered 2D texture.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><strong>It is not recommended to use SDK to handle buffer directly</strong>. SDK needs to take texture to be processed as input. If you need to handle buffer, it is recommended to transform buffer to texture, but it will be more time\-consuming.</div>


<span id="3. SDK parameter settings (e.g. beauty effects, stickers, filters)"></span>
### 3. SDK parameter settings (e.g. beauty effects, stickers, filters)

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">You should set SDK parameters after SDK initialization. Use the same thread as SDK image processing, to avoid possible issues.</div>


<span id="(1) Set beauty effects, face shaping, makeup effects"></span>
#### (1) Set beauty effects, face shaping, makeup effects

Beauty effects, face shaping, and makeup effects's parameters settings are using the same interface. Normally, it takes 2 steps for beauty effects to take effect.


1. Set paths corresponding to materials.

2. Set effects' intensity in materials (usually the default intensity is 0, therefore there will be no effects if step 2 is skipped).


**Interface of setting material path:** 

```Java
/**
 * Set special effects combinations, it supports any combinations of beauty effects, body shaping, face shaping, and makeup effects.
 */
boolean setComposeNodes(String[] nodes);

// Example
mEffectManager.setComposeNodes(new String[]{"beauty_Android_lite"});
mEffectManager.setComposeNodes(new String[]{"reshape_lite"});
```


The material path is relative to path of `ComposeMakeup.bundle/ComposeMakeup`. For more information on the file structure of material packages, refer to [Resource Package Structure](https://docs.byteplus.com/effects/docs/resource-package-structure-v421-and-later).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">SDK does not save configured materials internally, therefore you need to add all materials path that need to be effective on every calling.</div>


**When setting materials, interface for special effects intensity:** 

```Java
/**
 * Update some nodes' intensity in special effects combination (beauty effects, body shaping, face shaping, makeup effects)
 */
boolean updateComposerNodeIntensity(String node, String key, float intensity);

// Example
mEffectManager.updateComposerNodeIntensity("beauty_Android_lite", "smooth", 0.8f);
mEffectManager.updateComposerNodeIntensity("reshape_lite", "Internal_Deform_Overall", 0.8f);
```


Here is just a simple example.

All beauty, face reshaping, body reshaping, makeup, etc., are using **the same method** of "composerNode", only the **material path** and **key** are different.You need to use key to control which feature's intensity needs to be adjusted (whether it is toning, buffing, or sharpening).

The relation between materials' key and feature can be found in [Functions of Material Keys](doc:functions-of-resource-keys-v421-and-later).

<span id="(2) Set stickers"></span>
#### (2) Set stickers

**Set stickers interface:** 

```Java
/**
 * Turn on/off stickers, if path is empty, turn off stickers
 * @param path: File Path of sticker materials
 */
boolean setSticker(String path);

// Example
mEffectManager.setSticker("baibianfaxing");
```


The sicker path is the relative path to `StickerResource.bundle/stickers` in the materials package.

<span id="(3) Set filters"></span>
#### (3) Set filters

```Java
/**
 * Turn on/off stickers, if path is empty, turn off filters
 *
 * @param path File Path of filter materials
 */
boolean setFilter(String path);

/**
 * Set filter intensity
 *
 * @param intensity intensity parameter value
 */
boolean updateFilterIntensity(float intensity);

// Example
mEffectManager.setFilter("Filter_01_38");
mEffectManager.updateFilterIntensity(0.8f);
```


The filter path is the relative path to `FilterResource.bundle/Filter` in materials package.

<span id="4. Using SDK basic algorithms function"></span>
### 4. Using SDK basic algorithms function

Take face algorithms as an example:

Method calling face algorithms is packaged in `FaceAlgorithmTask`:


1. Algorithm initialization


```Java
public int initTask()
```


Return value indicates initialization result.


2. Algorithm detection


```Java
public BefFaceInfo process(ByteBuffer buffer, int width, int height, int stride, BytedEffectConstants.PixlFormat pixlFormat, BytedEffectConstants.Rotation rotation)
```



3. Algorithm parameter settings


Function for algorithm parameter settings is defined as:

```Java
public void setConfig(AlgorithmTaskKey key, Object p)
```


`key` indicates parameter type, `p` is the parameter value. Type of each algorithm's parameter can be found in algorithm definitions. For example, `key` can use `FACE_280` and `FACE_ATTR`. You can refer to Appendix: Keys and returned values of algorithms.

If you want to use `FaceAlgorithmTask`, you need to register at `AlgorithmTaskFactory`.

```Java
        AlgorithmTaskFactory.register(FaceAlgorithmTask.FACE, new AlgorithmTaskFactory.AlgorithmTaskGenerator<FaceAlgorithmTask.FaceResourceProvider>() {
            @Override
            public AlgorithmTask<FaceAlgorithmTask.FaceResourceProvider, ?> create(Context context, FaceAlgorithmTask.FaceResourceProvider provider) {
                return new FaceAlgorithmTask(context, provider);
            }
        });
```


<span id="Appendix: Instruction on copying materials"></span>
# Appendix: Instruction on copying materials

In Android, built\-in materials is in `asset`, hence the file content in it can not be accessed by path. Therefore, the workaround in Sample is to copy it to private directory at app's first initialization, by using `com.bytedance.labcv.demo.task.UnzipTask`. If the initialization time is too long because too many materials need to be copied, some methods can be referenced below:


1. Only copy some simple materials. For example, put beauty effects, face shaping to builtin.

2. Large\-size materials like stickers can be distributed offline. Only download materials to local when app needs the material. By doing this, you can achieve a smaller package size and faster initialization speed.


<span id="Appendix: obtain timeStamp"></span>
# Appendix: Obtain timeStamp

If you are using camera to collect data, and use `SurfaceTexture` as output data container. You can directly call its `getTimestamp` method:

```Java
long timeStamp = surfaceTexture.getTimestamp();
```


Otherwise use the system method:

```Java
long timeStamp System.currentTimeMillis();
```


<span id="Appendix: ImageSource class"></span>
# Appendix: ImageSource class

There are 3 different classes. The main differences are about the processing and drawing of input texture. Details are listed below.


|**Class** |**Difference** |**Output texture** |
|---|---|---|
|TYPE_CAMERA |Rotate textures based on incoming `srcTextureFormat`, `cameraRotation` and `sensorRotation`. The effect correctness is more easily guaranteed. But the performance is relatively bad since it needs to conduct 2 rotations. |Directions of output and input textures are the same. |
|TYPE_VIDEO |Rotate textures based on incoming `srcTextureFormat` and `videoRotation`. It needs to conduct 1 rotation. |Output texture is upright, which is not necessarily the same as the input texture. |
|TYPE_IMAGE |It does not preprocess textures. Therefore, the input textures must be 2D and face upright. The performance is relatively high. |Directions of input and output textures are the same, no rotation is done. |


<span id="Appendix: convert input texture to 2D texture with upright face"></span>
# Appendix: Convert input texture to 2D texture with upright face

The transToPotrait () method, in the sample code, is located in the implementation layer (BaseGLActivity.java), so it will not be discussed as an Interface, only an example method is given.

It uses the method class of ImageUtil, and a written wrapper `ImageSourceProvider` (in the Common module).

The code is as follow:

```Java
protected ImageSourceProvider mImageSourceProvider;
protected int mSurfaceWidth = 0;
protected int mSurfaceHeight = 0;
//  Texture size after becoming a full member
protected int mTextureWidth = 0;
protected int mTextureHeight = 0;
// ImageUtil is a Program encapsulation class responsible for processing textures. It is strongly associated with GLContext, so before the GL context changes, you need to call the respective destruction function, but the object itself is not destroyed. When you use it again, you will reassociate the current context according to the state of the internal variable Initialization
protected ImageUtil mImageUtil;

...

/** {en} 
 * Change the input texture to a positive 2D texture, and if it is a front camera, it will also mirror and flip
 * @return the input package
 */
protected ProcessInput transToPortrait(){
    if (mImageSourceProvider == null)return null;
    ProcessInput processInput = new ProcessInput();
    mTextureWidth = mImageSourceProvider.getWidth();
    mTextureHeight = mImageSourceProvider.getHeight();
    processInput.setTexture(mImageSourceProvider.getTexture());

    processInput.setSensorRotation(OrientationSensor.getOrientation());
        if (mImageSourceProvider.getOrientation() %180 == 90 || mImageSourceProvider.getTextureFormat() != BytedEffectConstants.TextureFormat.Texure2D){
            if (mImageSourceProvider.getOrientation() %180 == 90){
                mTextureWidth =  mImageSourceProvider.getHeight();
                mTextureHeight =  mImageSourceProvider.getWidth();
            }

            ImageUtil.Transition transition = new ImageUtil.Transition().rotate(mImageSourceProvider.getOrientation()).flip(false, mImageSourceProvider.isFront());

            int texture = mImageUtil.transferTextureToTexture(mImageSourceProvider.getTexture(), mImageSourceProvider.getTextureFormat(), BytedEffectConstants.TextureFormat.Texure2D,
                    mImageSourceProvider.getWidth(), mImageSourceProvider.getHeight(),transition);
            processInput.setTexture(texture);


    }

    processInput.setWidth(mTextureWidth);
    processInput.setHeight(mTextureHeight);

    return processInput;


}
```


<span id="Appendix: keys and returned values of algorithms"></span>
# Appendix: Keys and returned values of algorithms


|**Algorithm** |**Key** |**Returned Value** |
|---|---|---|
|Face Detection |FaceAlgorithmTask#FACE_106 (106 points) FaceAlgorithmTask#FACE_280 (280 points) FaceAlgorithmTask#FACE_ATTR (face attributes) FaceAlgorithmTask#FACE_MASK (face mask) FaceAlgorithmTask#MOUTH_MASK (lip mask) FaceAlgorithmTask#TEETH_MASK (teeth mask) |com.bytedance.labcv.effectsdk.BefFaceInfo |
|Face Verification |FaceVerifyAlgorithmTask.FACE_VERIFY |com.bytedance.labcv.core.algorithm.FaceVerifyAlgorithmTask.FaceVerifyCaptureResult |
|Animoji |AnimojiAlgorithmTask#ANIMOJI |com.bytedance.labcv.effectsdk.BefAnimojiInfo |
|Scene Recognition (C1) |C1AlgorithmTask.C1 |com.bytedance.labcv.effectsdk.BefC1Info |
|Scene Recognition (C2) |C2AlgorithmTask.C2 |com.bytedance.labcv.effectsdk.BefC2Info |
|Vehicle Detection |CarDetectTask.CAR_DETECT CarDetectTask.CAR_RECOG (Vehicle Detection) CarDetectTask.BRAND_RECOG (License Plate Detection) |com.bytedance.labcv.effectsdk.BefCarDetectInfo |
|Concentration Estimation |ConcentrateAlgorithmTask.CONCENTRATION |com.bytedance.labcv.core.algorithm.ConcentrateAlgorithmTask.BefConcentrationInfo |
|Gaze Detection |GazeEstimationTask.GAZE_ESTIMATION |com.bytedance.labcv.effectsdk.BefGazeEstimationInfo |
|Hair Segmentation |HairParserAlgorithmTask.HAIR_PARSER |com.bytedance.labcv.effectsdk.HairParser |
|Gesture Recognition |HandAlgorithmTask.HAND |com.bytedance.labcv.effectsdk.BefHandInfo |
|Head Segmentation |HeadSegmentAlgorithmTask.HEAD_SEGMENT |com.bytedance.labcv.effectsdk.BefHeadSegInfo |
|Distance Estimation |HumanDistanceAlgorithmTask.HUMAN_DISTANCE |com.bytedance.labcv.effectsdk.BefDistanceInfo |
|Light Condition Detection |LightClsAlgorithmTask.LIGHT_CLS |com.bytedance.labcv.effectsdk.BefLightclsInfo |
|Pet Face Detection |PetFaceAlgorithmTask.PET_FACE |com.bytedance.labcv.effectsdk.BefPetFaceInfo |
|Body Segmentation |PortraitMattingAlgorithmTask.PORTRAIT_MATTING |com.bytedance.labcv.effectsdk.PortraitMatting.MattingMask |
|Body Motion Detection |SkeletonAlgorithmTask.SKELETON |com.bytedance.labcv.effectsdk.BefSkeletonInfo |
|Sky Segmentation |SkySegmentAlgorithmTask.SKY_SEGMENT |com.bytedance.labcv.effectsdk.BefSkyInfo |
|Video Classification |VideoClsAlgorithmTask.VIDEO_CLS |com.bytedance.labcv.effectsdk.BefVideoClsInfo |
|Sports Classification |ActionRecognitionAlgorithmTask.ACTION_RECOGNITION |com.bytedance.labcv.effectsdk.BefActionRecognitionInfo |


<span id="0588971d"></span>
# Appendix: Android proguard rules

First, you must confirm **what version of the SDK** is being used.

**Before V4.4.3**

```Plain
-keep class com.bytedance.labcv.effectsdk.** {*;}
-keep class com.bef.effectsdk.* {*;} 
-keep class com.bytedance.labcv.licenselibrary.* {*;}
```


**After V4.4.3 (including V4.4.3)** 

```Plain
-keep class com.effectsar.labcv.effectsdk.** {*;}
-keep class com.bef.effectsdk.* {*;} 
-keep class com.effectsar.labcv.licenselibrary.* {*;}
```


<span id="8dbcd893"></span>
# Appendix: Notes when you upgrade sdk version (for V4.4.2/4.4.3/4.5.0)

For the following versions, there are several situations that need to be noted when upgrading the SDK:

**Version before V4.4.2, upgrade to V4.4.2 or V4.4.3**

Customers who are using the version before V4.4.2, if you upgrade to the V4.4.2 or V4.4.3 version, if the integrated code in your project remains the same, without copying the sample code of the new version, you need to add `mRenderManager.loadLib()` to the `EffectManager`.

Such as:

```Java
 public EffectManager(Context context, EffectResourceProvider mResourceProvider, EffectLicenseProvider mLicenseProvider) {
        mContext = context;
        this.mResourceProvider = mResourceProvider;
        this.mLicenseProvider = mLicenseProvider;
        mRenderManager = new RenderManager();
        mRenderManager.loadLib();  // Need to add this line

    }
```


**V4.4.2 or V4.4.3 upgrade to V4.5.0**

Customers who are using version V4.4.2 or V4.4.3, if you upgrade to version 4.5.0 and later, if the integrated code remains the same, without copying the new version of sample code, when upgrading to version 4.5.0, you need to comment out the code related to `RenderManager.loadLib()`; in `EffectManager`.

Such as:

```Java
   public EffectManager(Context context, EffectResourceProvider mResourceProvider, EffectLicenseProvider mLicenseProvider) {
        mContext = context;
        this.mResourceProvider = mResourceProvider;
        this.mLicenseProvider = mLicenseProvider;
        
        /*Comment out these lines
   *     try {
   *         RenderManager.loadLib();
   *     } catch (UnsatisfiedLinkError e) {
   *         ExternalLibraryLoader externalLibraryLoader = new ExternalLibraryLoader(new SdCardLibrarySource(context));
   *         externalLibraryLoader.loadLib();
   *     }
        */
        
        mRenderManager = new RenderManager();
    }
```
