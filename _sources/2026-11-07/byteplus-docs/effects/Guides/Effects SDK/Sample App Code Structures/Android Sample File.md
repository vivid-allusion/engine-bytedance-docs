---
title: "Android Sample File"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-android-sample-file"
---

The following shows the file structure of the sample (for iOS) 4.0.0.0 and later.

```Plain
.
├── base # UI-related base classes of MVP structures.
├── camera # Camera encapsulation, including camera1 and camera2.
├── core # Encapsulation of SDK APIs, including special effect APIs and algorithm APIs.
│   ├── v3 # Encapsulation of special effect APIs used in demo 3.*. It is now obsolete.
│   │   ├── BaseEffectHelper.java
│   │   ├── ImageEffectHelper.java
│   │   ├── PreviewEffectHelper.java
│   │   └── VideoEffectHelper.java
│   ├── v4 # Encapsulation of SDK APIs used in version 4.*, including special effect APIs and algorithm APIs.
│   │   ├── EffectHelper.java # Output APIs for both special effects and algorithms.
│   │   ├── ResourceHelper.java # Resource path APIs for both special effects and algorithms.
│   │   ├── algorithm # Algorithm APIs.
│   │   │   ├── AlgorithmInterface.java
│   │   │   ├── AlgorithmManager.java # External output APIs for algorithms. If only algorithms are used, you can use this file instead of EffectHelper.java.
│   │   │   ├── AlgorithmRender.java
│   │   │   ├── AlgorithmResourceHelper.java # Algorithm resource path APIs. If only algorithms are used, you can use this file instead of ResourceHelper.java. It contains the model file paths for each algorithm. In the algorithm version, you need to modify the path of the license file in this file.
│   │   │   ├── AlgorithmTask.java # Base classes of algorithm modules.
│   │   │   └── task # Implementation of all algorithm modules. You can delete unnecessary implementation from this file, but if other files (such as AlgorithmManager.java) contain reference to the deleted implementation, you need to delete relevant reference code from these files.
│   │   ├── base # Base classes of the SDK APIs for both algorithms and special effects.
│   │   │   ├── BufferConvert.java # Implementation of conversion of buffers.
│   │   │   ├── ProcessInput.java # Input data types.
│   │   │   ├── ProcessOutput.java # Output data types.
│   │   │   ├── ResourceProvider.java
│   │   │   ├── Task.java
│   │   │   ├── TaskContainer.java
│   │   │   ├── task
│   │   │   └── util
│   │   └── effect # Special effect APIs.
│   │       ├── EffectInterface.java
│   │       ├── EffectManager.java # External output APIs for special effects. If only special effects are used, you can use this file instead of EffectHelper.java.
│   │       ├── EffectRender.java
│   │       ├── EffectResourceHelper.java # Special effect resource path APIs. If only special effects are used, you can use this file instead of ResourceHelper.java. In the special effect version, you need to modify the path of the license file in this file.
│   │       ├── TextureFormatter.java # Implementation of conversion of textures.
│   │       └── task # Implementation of special effect modules.
│   └── video # Implementation related to video recording.
│       ├── EglCore.java
│       ├── EglSurfaceBase.java
│       ├── FullFrameRect.java
│       ├── MediaMuxerManager.java
│       ├── Texture2dProgram.java
│       ├── TextureMovieEncoder.java
│       ├── VideoEncoderCore.java
│       └── WindowSurface.java
├── media # Implementation related to video playback.
│   └── SimplePlayer.java
├── model # UI-related model classes.
│   ├── AlgorithmItem.java
│   ├── AlgorithmItemGroup.java
│   ├── ButtonItem.java
│   ├── CaptureResult.java
│   ├── ComposerNode.java
│   ├── DynamicActionAlgorithmItem.java
│   ├── EffectBackup.java
│   ├── EffectButtonItem.java
│   ├── ExternParam.java
│   ├── FaceVerifyResult.java
│   ├── FilterItem.java
│   └── StickerItem.java
├── opengl # UI-related OpenGL utility classes. This file is used to draw algorithm results.
│   ├── Drawable2d.java
│   ├── Extensions.java
│   ├── FrameBuffer.java
│   ├── GlUtil.java
│   ├── HairMaskProgram.java
│   ├── LineProgram.java
│   ├── MaskProgram.java
│   ├── PointProgram.java
│   ├── PortraitMaskProgram.java
│   ├── Program.java
│   ├── ProgramManager.java
│   ├── ProgramTexture2d.java
│   ├── ProgramTextureOES.java
│   ├── ShaderHelper.java
│   ├── ShaderProgram.java
│   └── TextureRotationUtil.java
├── posteffect
│   └── CustomRenderThread.java
├── presenter # UI-related.
│   ├── DetectPresenter.java
│   ├── EffectPresenter.java # Defaults preset in the demo.
│   ├── FilterPresenter.java # Mappings between all filter names and indexes.
│   ├── ItemGetPresenter.java # Mappings between all item keys and nodes.
│   ├── StickerPresenter.java # Mappings between all stickers and prompts.
│   ├── WelcomePresenter.java
│   └── contract
│       ├── DetectContract.java
│       ├── EffectContract.java
│       ├── FilterContract.java
│       ├── ItemGetContract.java
│       ├── StickerContract.java
│       └── WelcomeContract.java
├── task # Related to demo functions.
│   ├── SavePicTask.java
│   ├── UnzipTask.java
│   ├── facecluster
│   │   ├── FaceClusterHandler.java
│   │   ├── FaceClusterMgr.java
│   │   └── FaceClusterThread.java
│   └── faceverify
│       ├── FaceVerifyThreadHandler.java
│       └── RepeatedVerifyHandler.java
├── ui # Related to UIs.
│   ├── BaseEffectActivity.java
│   ├── DemoApplication.java
│   ├── ImageEffectActivity.java
│   ├── LocalBroadcastReceiver.java
│   ├── PermissionsActivity.java
│   ├── PreviewEffectActivity.java
│   ├── ResourceHelper.java
│   ├── VideoEffectActivity.java
│   ├── WelcomeActivity.java
│   ├── adapter
│   │   ├── AlgorithmButtonRVAdapter.java
│   │   ├── ButtonViewRVAdapter.java
│   │   ├── EffectButtonViewRVAdapter.java
│   │   ├── FaceClusterAdapter.java
│   │   ├── FilterRVAdapter.java
│   │   ├── FragmentVPAdapter.java
│   │   ├── OnPageChangeListenerAdapter.java
│   │   ├── SelectRVAdapter.java
│   │   └── StickerRVAdapter.java
│   ├── fragment
│   │   ├── BaseFeatureFragment.java
│   │   ├── algorithm # Algorithm UIs.
│   │   │   ├── AlgorithmButtonFragment.java
│   │   │   ├── AlgorithmFragment.java
│   │   │   ├── DynamicActionInfoFragment.java
│   │   │   ├── FaceClusterFragment.java
│   │   │   ├── FaceInfoFragment.java
│   │   │   ├── FaceVerifyFragment.java
│   │   │   ├── StudentIdOcrFragment.java
│   │   │   └── ui # Implementation of all algorithm UIs.
│   │   └── effect # Special effect UIs.
│   │       ├── BeautyFaceFragment.java
│   │       ├── EffectFragment.java
│   │       ├── FilterFragment.java
│   │       ├── MakeupOptionFragment.java
│   │       ├── StickerFragment.java
│   │       └── TabStickerFragment.java
│   └── view
│       ├── BrandRecogTip.java
│       ├── ButtonView.java
│       ├── CarRectInfoTip.java
│       ├── GeneralObjectInfoTip.java
│       ├── HandInfoTip.java
│       ├── HumanDistanceTip.java
│       ├── PetFaceInfoTip.java
│       ├── ProgressBar.java
│       ├── PropertyTextView.java
│       ├── ResultTip.java
│       ├── TipManager.java
│       └── VideoButton.java
└── utils # Utility classes related to demo functions.
    ├── AppUtils.java
    ├── BitmapUtils.java
    ├── CommonUtils.java
    ├── Config.java
    ├── DensityUtils.java
    ├── FrameRator.java
    ├── InputSizeManager.java
    ├── RectUtils.java
    ├── ToastUtils.java
    ├── UserData.java
    └── timer_record
        ├── LogTimerRecord.java
        └── TimerRecord.java

```
