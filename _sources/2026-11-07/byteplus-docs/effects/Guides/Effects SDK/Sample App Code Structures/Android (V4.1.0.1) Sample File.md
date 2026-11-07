---
title: "Android (V4.1.0.1) Sample File"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-android-v4101-sample-file"
---

The list below shows the sample file structure for version 4.01.0.0 and later versions.


---



Sample Overall File Structure

```Plain
├── algorithm //Basic algorithm module
├── app // Main page
├── ar // AR module
├── avatar // Avatar module
├── build.gradle
├── ck // 
├── common // General tools package
├── core // SDK calling package
├── effect // Special effects module
├── gradle
├── gradle.properties
├── gradlew
├── gradlew.bat
├── lens // Image quality module
├── library // SDK library
├── local.properties
├── settings.gradle
└── sports // Fitness module


```


File Structure: Special Effects Module

```Plain
 ├── activity
│   ├── BaseEffectActivity.java //Special effects base class
│   ├── BeautyActivity.java //Beauty effects & body shaping
│   ├── MattingStickerActivity.java //Segmentation & stickers
│   ├── QRScanActivity.java //QR code scan 
│   ├── SingleTabStickerActivity.java //Single-tab stickers page
│   ├── StickerActivty.java//Multi-tab stickers
│   └── StyleMakeUpActivity.java// Advanced makeup set
├── adapter
│   ├── EffectButtonRVAdapter.java
│   ├── EffectButtonViewRVAdapter.java
│   ├── FragmentVPAdapter.java
│   ├── OnPageChangeListenerAdapter.java
│   └── SelectItemRVAdapter.java
├── config
│   ├── EffectConfig.java
│   └── StickerConfig.java
├── fragment
│   ├── BeautyFaceFragment.java
│   ├── EffectFragment.java
│   ├── FilterFragment.java
│   ├── MattingStickerFragment.java
│   ├── MultiTabStickerFragment.java
│   ├── SingleTabStickerFrament.java
│   ├── StickerFragment.java
│   └── StyleMakeUpFragment.java
├── gesture // Gesture management
│   ├── BaseGestureDetector.java
│   ├── GestureHelper.java
│   ├── GestureManager.java
│   ├── RotateGestureDetector.java
│   └── TwoFingerGestureDetector.java
├── manager //Data management for special effects node
│   ├── EffectDataManager.java
│   ├── FilterDataManager.java
│   └── StickerDataManager.java
├── model // Data models
│   ├── ComposerNode.java
│   ├── EffectButtonItem.java
│   ├── FilterItem.java
│   └── StickerItem.java
├── qrscan //Scan to download
│   ├── BaseResponse.java
│   ├── DownloadParam.java
│   ├── EncryptParam.java
│   ├── EncryptResult.java
│   └── QRScanResult.java
├── res // Management for path resources
│   └── EffectResourceHelper.java
├── task //Asynchronized task
│   └── DownloadStickerTask.java
├── utils // Utilities
│   ├── Config.java
│   └── NetworkUtils.java
└── view
    ├── ProgressBar.java
    ├── RadioTextView.java
    └── ViewfinderView.java



```


File Structure: Algorithms Module

```Plain
├── activity
│   └── AlgorithmActivity.java //Algorithms page
├── adapter
│   ├── AlgorithmButtonRVAdapter.java
│   └── FaceClusterAdapter.java
├── config
│   └── AlgorithmConfig.java
├── fragment 
│   ├── AlgorithmBoardFragment.java
│   ├── FaceClusterFragment.java
│   ├── FaceInfoFragment.java
│   ├── FaceVerifyFragment.java
│   ├── FaceVerifyInfoFragment.java
│   ├── SkyInfoFragment.java
│   └── StudentIdOcrFragment.java
├── model
│   ├── AlgorithmItem.java
│   └── AlgorithmItemGroup.java
├── render // Algorithms rendering
│   ├── AlgorithmRender.java
│   ├── FaceSegmentProgram.java
│   ├── HairMaskProgram.java
│   ├── LineProgram.java
│   ├── MaskProgram.java
│   ├── PointProgram.java
│   ├── PortraitMaskProgram.java
│   ├── ShaderHelper.java
│   ├── ShaderProgram.java
│   ├── SkyMaskProgram.java
│   └── TextureRotationUtil.java
├── res //  Management for path resources
│   └── AlgorithmResourceHelper.java
├── task // Asynchronized tasks
│   ├── facecluster // Face clustering
│   │   ├── FaceClusterHandler.java
│   │   ├── FaceClusterMgr.java
│   │   └── FaceClusterThread.java
│   └── faceverify // Face verification
│       ├── FaceVerifyResult.java
│       ├── FaceVerifyThreadHandler.java
│       └── RepeatedVerifyHandler.java
├── ui // UI Controls
│   ├── AlgorithmUI.java
│   ├── AlgorithmUIFactory.java
│   ├── AnimojiUI.java
│   ├── BaseAlgorithmUI.java
│   ├── C1UI.java
│   ├── C2UI.java
│   ├── CarUI.java
│   ├── ConcentrationUI.java
│   ├── FaceClusterUI.java
│   ├── FaceUI.java
│   ├── FaceVerifyUI.java
│   ├── GazeEstimationUI.java
│   ├── HairParserUI.java
│   ├── HandUI.java
│   ├── HeadSegUI.java
│   ├── HumanDistanceUI.java
│   ├── LightClsUI.java
│   ├── PetFaceUI.java
│   ├── PortraitMattingUI.java
│   ├── SkeletonUI.java
│   ├── SkySegUI.java
│   ├── StudentIdOcrTestUI.java
│   ├── StudentIdOcrUI.java
│   └── VideoClsUI.java
└── view // Self-customized view
    ├── BrandRecogTip.java
    ├── CarRectInfoTip.java
    ├── HandInfoTip.java
    ├── HumanDistanceTip.java
    ├── PetFaceInfoTip.java
    ├── ResultTip.java
    └── TipManager.java

```


File Structure: Common Modules

```Plain
├── adapter
│   └── ButtonViewRVAdapter.java
├── base 
│   ├── BaseBarGLActivity.java //GLActivity with top banner
│   └── BaseGLActivity.java //Base packaged with GLSurfaceView
├── config
│   └── ImageSourceConfig.java
├── fragment
│   └── BoardButtonFragment.java
├── imgsrc // Data source: image, video, camera
│   ├── ImageSourceProvider.java
│   ├── TextureHolder.java
│   ├── bitmap //Image source
│   │   └── BitmapSourceImpl.java
│   ├── camera //Camera source
│   │   ├── Camera1.java
│   │   ├── Camera2.java
│   │   ├── Camera2BlackList.java
│   │   ├── CameraInterface.java
│   │   ├── CameraListener.java
│   │   ├── CameraProxy.java
│   │   ├── CameraSourceImpl.java
│   │   ├── RectUtils.java
│   │   └── focus
│   └── video //Video source
│       ├── EglCore.java
│       ├── EglSurfaceBase.java
│       ├── FullFrameRect.java
│       ├── MediaMuxerManager.java
│       ├── SimplePlayer.java
│       ├── Texture2dProgram.java
│       ├── TextureMovieEncoder.java
│       ├── VideoEncodeHelper.java
│       ├── VideoEncoderCore.java
│       ├── VideoReSampleList.java
│       ├── VideoSourceImpl.java
│       └── WindowSurface.java
├── model // Data models
│   ├── BubbleConfig.java
│   ├── ButtonItem.java
│   ├── CaptureResult.java
│   ├── EffectType.java
│   ├── ProcessInput.java
│   └── ProcessOutput.java
├── task
│   └── SavePicTask.java
├── utils 
│   ├── BitmapUtils.java
│   ├── CommonUtils.java
│   ├── DensityUtils.java
│   ├── FileUtils.java
│   ├── FrameRator.java
│   ├── PreferenceUtils.java
│   ├── PreviewSizeManager.java
│   └── ToastUtils.java
└── view //Self-customized view
    ├── BubbleTipManager.java
    ├── ButtonView.java
    ├── PropertyTextView.java
    ├── SwitchView.java
    └── bubble
        ├── BubblePopupWindow.java
        ├── BubbleRelativeLayout.java
        └── BubbleWindowManager.java

```


File Structure: Core Modules

```Plain
.
├── algorithm //Calling package for basic algorithms
│   ├── AnimojiAlgorithmTask.java
│   ├── C1AlgorithmTask.java
│   ├── C2AlgorithmTask.java
│   ├── CarAlgorithmTask.java
│   ├── ConcentrateAlgorithmTask.java
│   ├── FaceAlgorithmTask.java
│   ├── FaceClusterAlgorithmTask.java
│   ├── FaceVerifyAlgorithmTask.java
│   ├── GazeEstimationAlgorithmTask.java
│   ├── HairParserAlgorithmTask.java
│   ├── HandAlgorithmTask.java
│   ├── HeadSegAlgorithmTask.java
│   ├── HumanDistanceAlgorithmTask.java
│   ├── LightClsAlgorithmTask.java
│   ├── PetFaceAlgorithmTask.java
│   ├── PortraitMattingAlgorithmTask.java
│   ├── SkeletonAlgorithmTask.java
│   ├── SkySegAlgorithmTask.java
│   ├── StudentIdOcrAlgorithmTask.java
│   ├── VideoClsAlgorithmTask.java
│   ├── base
│   │   ├── AlgorithmResourceProvider.java
│   │   ├── AlgorithmTask.java
│   │   └── AlgorithmTaskKey.java
│   └── factory
│       ├── AlgorithmTaskFactory.java
│       └── AlgorithmTaskKeyFactory.java
├── avatar
│   ├── AvatarInterface.java
│   └── AvatarResourceProvider.java
├── effect // Package for calling special effects
│   ├── EffectManager.java
│   └── EffectResourceProvider.java
├── lens // Package for calling image quality
│   ├── ImageQualityInterface.java
│   ├── ImageQualityManager.java
│   ├── ImageQualityResourceProvider.java
│   └── util
│       └── ImageQualityUtil.java
├── opengl // opengl related
│   ├── Drawable2d.java
│   ├── Extensions.java
│   ├── GlUtil.java
│   ├── Program.java
│   ├── ProgramManager.java
│   ├── ProgramTexture2d.java
│   └── ProgramTextureOES.java
└── util // Public Utilities
    ├── ImageUtil.java // Image Processing Ulitilities
    ├── LogUtils.java // Log
    ├── OrientationSensor.java // Gravitational sensor
    └── timer_record // Performance log
        ├── LogTimerRecord.java
        └── TimerRecord.java

```
