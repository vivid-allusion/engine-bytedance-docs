---
title: "iOS (V4.1.0.1) Sample File"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-ios-v4101-sample-file"
---

```Plain
├── BEAppDelegate.h
├── BEAppDelegate.m
├── Info.plist
├── main.m
├── manager
│   ├── BEFeatureConfig.h
│   ├── BEFeatureConfig.m
│   ├── BEFeatureItem.h
│   ├── BEFeatureItem.m
│   ├── BEMainDataManager.h
│   └── BEMainDataManager.m
├── re.h
└── ui
    ├── vc        // ViewController realization
    │   ├── BEMainVC.h
    │   └── BEMainVC.m
    └── view
        ├── BEMainView.h        // Main Page View realization，below are UI codes, too
        ├── BEMainView.m
        ├── adapter
        ├── cell
        ├── content
        └── test
Core/Core        // Package of SDK's C interface, and other common features
├── Algorithm        // Algorithms package interface
│   ├── Base
│   │   ├── BEAlgorithmKey.h
│   │   ├── BEAlgorithmKey.m
│   │   ├── BEAlgorithmTask.h
│   │   ├── BEAlgorithmTask.m
│   │   ├── BEAlgorithmTaskFactory.h
│   │   └── BEAlgorithmTaskFactory.m
│   └── Task        // Includes realization of all algorithms, one class corresponds to one algorithm
├── Core.h
├── Effect        // Special effects package interface
│   ├── BEEffectManager.h
│   └── BEEffectManager.m
├── Lens        // Image quality package interface
│   ├── BEAdaptiveSharpenTask.h
│   ├── BEAdaptiveSharpenTask.m
│   ├── BEImageOpeartion.h
│   ├── BEImageOpeartion.m
│   ├── BEImageQualityProcessManager.h
│   ├── BEImageQualityProcessManager.m
│   ├── BEVideoSRTask.h
│   └── BEVideoSRTask.m
├── Utils        // Utilities package interface
│   ├── BEGLTexture.h
│   ├── BEGLTexture.m
│   ├── BEImageUtils.h        // Utility class for image transform，including interchange functions of buffer, CVPixelBuffer, texture
│   ├── BEImageUtils.m
│   ├── BETimeRecoder.h
│   └── BETimeRecoder.m
├── Info.plist
└── macro.h
Common/Common        // Public packaegs used by special effects, algorithms modules
├── Categories        // ui related，self-customized category
├── Common.h
├── CommonSize.h
├── Info.plist
├── model
├── ui
│   ├── cell
│   │   ├── BEButtonViewCell.h
│   │   ├── BEButtonViewCell.m
│   │   ├── BEMainTabCell.h
│   │   └── BEMainTabCell.m
│   ├── vc
│   │   ├── BEBaseBarVC.h        // inherited from BaseVC，add some common buttons and related realizations
│   │   ├── BEBaseBarVC.m
│   │   ├── BEBaseVC.h        // basic ViewController，packaging calling methods of camera, image, video modes
│   │   ├── BEBaseVC.m
│   │   ├── BEPopoverVC.h        // self-customized popover realization
│   │   └── BEPopoverVC.m
│   └── view
│       ├── BEBaseBarView.h
│       ├── BEBaseBarView.m
│       ├── BEPopoverView.h
│       ├── BEPopoverView.m
│       └── content
├── util        // some common utility classes
│   ├── BEDeviceInfoHelper.h
│   ├── BEDeviceInfoHelper.m
│   ├── BEGLUtils.h
│   ├── BEGLUtils.m
│   ├── BEPreviewSizeManager.h
│   ├── BEPreviewSizeManager.m
│   ├── BEProfileRecordManager.h
│   ├── BEProfileRecordManager.m
│   ├── BETextSizeUtils.h
│   ├── BETextSizeUtils.m
│   ├── bubble_tip
│   ├── gesture        // touching gesture detection tools
│   └── popover
└── videoSource        // packaged image source, supports camera, image, video modes' usages
    ├── BEImageCapture.h        // image analysis
    ├── BEImageCapture.m
    ├── BELocalVideoCapture.h        // video file analysis
    ├── BELocalVideoCapture.m
    ├── BEVideoCapture.h        // camera
    ├── BEVideoCapture.m
    ├── BEVideoSourceConfig.h
    ├── BEVideoSourceConfig.m
    ├── BEVideoSourceProvider.h
    └── BEVideoSourceProvider.m
Algorithm/Algorithm    // UI realization related to algorithm feature
├── Algorithm.h
├── Info.plist
├── model
│   ├── BEAlgorithmConfig.h
│   ├── BEAlgorithmConfig.m
│   ├── BEAlgorithmItem.h
│   ├── BEAlgorithmItem.m
│   ├── BEAlgorithmResourceHelper.h
│   └── BEAlgorithmResourceHelper.m
├── render        // Utility class for rendering detection algorithms output
│   ├── BEAlgorithmRender.h
│   ├── BEAlgorithmRender.m
│   ├── BEAlgorithmRenderHelper.h
│   └── BEAlgorithmRenderHelper.m
├── ui
│   ├── content
│   ├── vc
│   │   ├── BEAlgorithmVC.h        // Algorithms page's ViewController
│   │   ├── BEAlgorithmVC.m
│   │   ├── content
│   │   └── info
│   └── view
│       ├── BEAlgorithmView.h
│       ├── BEAlgorithmView.m
│       └── content
└── widgets
    ├── BEActionView.h
    └── BEActionView.m
Effect/Effect        // UI realization of special effects feature
├── Effect.h
├── Effect.m
├── Info.plist
├── config
│   ├── BEEffectConfig.h
│   ├── BEEffectConfig.m
│   ├── BEStickerConfig.h
│   └── BEStickerConfig.m
├── model
│   ├── BEComposerNodeModel.h
│   ├── BEComposerNodeModel.m
│   ├── BEEffectDataManager.h        // Data related to special effects, e.g. beauty effects & body shaping's material path, default parameters.
│   ├── BEEffectDataManager.m
│   ├── BEEffectItem.h
│   ├── BEEffectItem.m
│   ├── BEEffectResponseModel.h
│   └── BEEffectResponseModel.m
├── ui
│   ├── base        // special effects' base class
│   │   ├── BEEffectBaseView.h
│   │   ├── BEEffectBaseView.m
│   │   ├── vc
│   │   └── view
│   ├── effect        // UI realization of beauty effects & body shaping
│   │   ├── vc
│   │   └── view
│   ├── matting_sticker        // UI realization of background segmentation page
│   │   ├── vc
│   │   └── view
│   ├── qr_scan        // UI realization of QR code scan page
│   │   ├── BEQRScanVC.m
│   │   ├── BEQRScanView.h
│   │   ├── vc
│   │   └── view
│   ├── sticker        // UI realization of stickers/Animoji/AR page
│   │   ├── vc
│   │   └── view
│   └── style_makeup        // UI realization of Advanced makeup set page
│       ├── vc
│       └── view
├── util
│   ├── BEEffectResourceHelper.h
│   ├── BEEffectResourceHelper.m
│   ├── BENetworkUtil.h
│   ├── BENetworkUtil.m
│   ├── BEStickerDownloadTask.h
│   └── BEStickerDownloadTask.m
└── widgets
    ├── BETextSliderView.h
    └── BETextSliderView.m
lens/lens        // UI realization of image quality features
├── Info.plist
├── Lens.h
├── model
│   ├── BELensConfig.h
│   ├── BELensConfig.m
│   ├── BELensResourceHelper.h
│   ├── BELensResourceHelper.m
│   └── BELensType.h
└── ui
    ├── vc
    │   ├── BELensVC.h
    │   └── BELensVC.m
    └── view
        ├── BELensView.h
        └── BELensView.m
```
