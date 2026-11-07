---
title: "Mac Sample File"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-mac-sample-file-structure"
---

The following shows the file structure of the sample (for Mac) **4.3.0 and later**.

```json

├── Algorithm
│   ├── Algorithm
│   │   ├── Algorithm.h                         // Define of algorithm key
│   │   ├── Algorithm.m
│   │   ├── AlgorithmTask
│   │   │   ├── BEAlgorithmKey.h                
│   │   │   ├── BEAlgorithmKey.m
│   │   │   ├── BEAlgorithmTask.h               // Algorithm task base implementation
│   │   │   ├── BEAlgorithmTask.m
│   │   │   ├── BEC1AlgorithmTask.h             // c1 algorithm
│   │   │   ├── BEC1AlgorithmTask.m
│   │   │   ├── BEC2AlgorithmTask.h             // c2 algorithm
│   │   │   ├── BEC2AlgorithmTask.m
│   │   │   ├── BEFaceAlgorithmTask.h           // Face detection algorithm
│   │   │   ├── BEFaceAlgorithmTask.m
│   │   │   ├── BEFaceVerifyAlgorithmTask.h     // Face verify algorithm
│   │   │   ├── BEFaceVerifyAlgorithmTask.m
│   │   │   ├── BEGazeEstimationTask.h          // Gaze estimation algorithm
│   │   │   ├── BEGazeEstimationTask.m
│   │   │   ├── BEHairParserAlgorithmTask.h     // Hair segmentation algorithm
│   │   │   ├── BEHairParserAlgorithmTask.m
│   │   │   ├── BEHandAlgorithmTask.h           // Hand detection algorithm
│   │   │   ├── BEHandAlgorithmTask.m
│   │   │   ├── BEHeadSegmentAlgorithmTask.h    // Hair segmentation algorithm
│   │   │   ├── BEHeadSegmentAlgorithmTask.m
│   │   │   ├── BELightClsAlgorithmTask.h       // Light detection algorithm
│   │   │   ├── BELightClsAlgorithmTask.m
│   │   │   ├── BEPetFaceAlgorithmTask.h        // Pet face detection algorithm
│   │   │   ├── BEPetFaceAlgorithmTask.m
│   │   │   ├── BEPortraitMattingAlgorithmTask.h    // Matting algorithm
│   │   │   ├── BEPortraitMattingAlgorithmTask.m
│   │   │   ├── BESkeletonAlgorithmTask.h           // Body keypoint algorithm
│   │   │   ├── BESkeletonAlgorithmTask.m
│   │   │   ├── BEVideoClsAlgorithmTask.h           // Video clus algorithm
│   │   │   └── BEVideoClsAlgorithmTask.m
│   │   ├── BEAlgorithmResourceHelper.h
│   │   ├── BEAlgorithmResourceHelper.m
│   │   ├── BEAlgorithmResult.h                     // Define of algorithm result
│   │   ├── BEAlgorithmResult.m
│   │   ├── BEAlgorithmTaskFactory.h
│   │   ├── BEAlgorithmTaskFactory.m
│   │   └── BEUtil.h
│   └── Algorithm.xcodeproj
├── ByteEffects
│   ├── AppDelegate.h
│   ├── AppDelegate.m
│   ├── common
│   │   ├── BELocaleManager.h               // Local language setting
│   │   ├── BELocaleManager.m
│   │   ├── BENotify.h                      // Message notification define
│   │   ├── BETextSizeUtils.h
│   │   ├── BETextSizeUtils.m
│   │   ├── CommonDef.h
│   │   ├── license_manager                 // Related code of online license 
│   │   │   ├── BELicenseCheck.h
│   │   │   ├── BELicenseCheck.m
│   │   │   ├── BERequester.h
│   │   │   ├── BERequester.mm
│   │   │   ├── base64.cpp
│   │   │   ├── base64.h
│   │   │   ├── license_requester.cpp
│   │   │   ├── license_requester.h
│   │   │   └── misc.h
│   │   └── videoSource                     // Camera Capture
│   │       ├── BELocalVideoCapture.h
│   │       └── BELocalVideoCapture.m
│   ├── config
│   │   ├── BEEffectConfig.h
│   │   ├── BEEffectConfig.m
│   │   ├── BEStickerConfig.h
│   │   └── BEStickerConfig.m
│   ├── main.m
│   ├── manager
│   │   ├── BEFeatureConfig.h
│   │   ├── BEFeatureConfig.m
│   │   ├── BEFeatureItem.h
│   │   ├── BEFeatureItem.m             
│   │   ├── BEProfileManger.h               // Performance related data management
│   │   └── BEProfileManger.m
│   ├── model
│   │   ├── BEComposerNodeModel.h           // Composer effects material definition and configuration
│   │   ├── BEComposerNodeModel.m
│   │   ├── BEEffectDataManager.h           // Effect resource data manager
│   │   ├── BEEffectDataManager.m
│   │   ├── BEEffectItem.h                  // Effect item definition
│   │   ├── BEEffectItem.m
│   │   ├── BEEffectResponseModel.h         // Basic algorithms, stickers and other data definitions
│   │   ├── BEEffectResponseModel.m
│   │   ├── BEResourceHelper.h              // Resource Management Implementation
│   │   └── BEResourceHelper.m
│   ├── render
│   │   ├── BEAlgorithmRender.h             // Algorithm rendering related code
│   │   ├── BEAlgorithmRender.m
│   │   ├── BEAlgorithmRenderHelper.h
│   │   └── BEAlgorithmRenderHelper.m
│   ├── ui
│   │   ├── vc
│   │   │   ├── BEMainVC.h                  // Main view controller
│   │   │   ├── BEMainVC.m
│   │   │   └── content
│   │   │       ├── BEAlgorithmInfoVC.h     // Algorithm data view controller, such as human face keypoints, gestures info view
│   │   │       ├── BEAlgorithmInfoVC.m
│   │   │       ├── BEAlgorithmVC.h          // Algorithm tab page
│   │   │       ├── BEAlgorithmVC.m        
│   │   │       ├── BECameraTopVC.h         // camera viewing top floating UI
│   │   │       ├── BECameraTopVC.m
│   │   │       ├── BECameraVC.h            // camera preview view controller
│   │   │       ├── BECameraVC.m
│   │   │       ├── BEEffectVC.h            // Effect features corner view controller
│   │   │       ├── BEEffectVC.m
│   │   │       ├── BELicenseVC.h           // License input view controller
│   │   │       ├── BELicenseVC.m
│   │   │       ├── BEProfileVC.h           // Performance showing view controller
│   │   │       ├── BEProfileVC.m
│   │   │       └── beauty
│   │   │           ├── BEBeautyHeaderVC.h      // Beauty & body effect header
│   │   │           └── BEBeautyHeaderVC.m
│   │   └── view
│   │       ├── BEMainView.h            // Main page view
│   │       ├── BEMainView.m
│   │       ├── BETitleBarView.h        // Title Bar view
│   │       ├── BETitleBarView.m
│   │       ├── BEVersionLabel.h        // Version label view
│   │       ├── BEVersionLabel.m
│   │       ├── GLView
│   │       │   ├── BEGLView.h          // camera image drawing on glview
│   │       │   └── BEGLView.m
│   │       ├── components                      // Basic UI components
│   │       │   ├── BEActionTitleCell.h
│   │       │   ├── BEActionTitleCell.m
│   │       │   ├── BEBtnImageInfo.h
│   │       │   ├── BEButtonView.h
│   │       │   ├── BEButtonView.m
│   │       │   ├── BEExpandButton.h
│   │       │   ├── BEExpandButton.m
│   │       │   ├── BEIntensityView.h
│   │       │   ├── BEIntensityView.m
│   │       │   ├── BEPropertyTextView.h
│   │       │   ├── BEPropertyTextView.m
│   │       │   ├── BEScroller.h
│   │       │   ├── BEScroller.m
│   │       │   ├── BESelectImageView.h
│   │       │   ├── BESelectImageView.m
│   │       │   ├── BESelectItemCell.h
│   │       │   ├── BESelectItemCell.m
│   │       │   ├── BESelectItemView.h
│   │       │   ├── BESelectItemView.m
│   │       │   ├── BESliderCell.h
│   │       │   ├── BESliderCell.m
│   │       │   ├── BESliderView.h
│   │       │   ├── BESliderView.m
│   │       │   ├── BETextButton.h
│   │       │   ├── BETextButton.m
│   │       │   ├── BETitleButton.h
│   │       │   ├── BETitleButton.m
│   │       │   ├── BETosatView.h
│   │       │   └── BETosatView.m
│   │       ├── content
│   │       │   ├── BECameraContainerView.h             //camera preview container
│   │       │   ├── BECameraContainerView.m
│   │       │   ├── BEEffectCompareBtn.h                // Compare button
│   │       │   ├── BEEffectCompareBtn.m
│   │       │   ├── BEEffectContainerView.h             // Effect container view
│   │       │   ├── BEEffectContainerView.m
│   │       │   ├── BEEffectResetBtn.h                  // Reset button
│   │       │   ├── BEEffectResetBtn.m
│   │       │   ├── advancedSticker                     // Advanced Sticker UI
│   │       │   │   ├── BEAdvancedStickerView.h 
│   │       │   │   └── BEAdvancedStickerView.m
│   │       │   ├── algorithm
│   │       │   │   ├── BEAlgorithmContainerView.h      // Algorithm container
│   │       │   │   ├── BEAlgorithmContainerView.m
│   │       │   │   ├── BEAlgorithmContentView.h
│   │       │   │   ├── BEAlgorithmContentView.m
│   │       │   │   ├── BEFaceActionView.h              // Face action
│   │       │   │   ├── BEFaceActionView.m
│   │       │   │   ├── BEFaceAttrView.h                // Face attribute
│   │       │   │   ├── BEFaceAttrView.m
│   │       │   │   ├── BEFaceInfoView.h                // Face info
│   │       │   │   ├── BEFaceInfoView.m
│   │       │   │   ├── BEFaceVerifyImageView.h         // Face verify image
│   │       │   │   ├── BEFaceVerifyImageView.m
│   │       │   │   ├── BEFaceVerifyInfoView.h          // Result of face verify
│   │       │   │   ├── BEFaceVerifyInfoView.m
│   │       │   │   ├── BEGazeEstimationView.h          // Result of gaze estimation
│   │       │   │   ├── BEGazeEstimationView.m
│   │       │   │   ├── BEHandInfoView.h                // Result of hand detection
│   │       │   │   ├── BEHandInfoView.m
│   │       │   │   ├── BEImageUpdateBtn.h              // Image update button
│   │       │   │   ├── BEImageUpdateBtn.m
│   │       │   │   ├── BELightClsView.h                // Result of light detection 
│   │       │   │   ├── BELightClsView.m
│   │       │   │   ├── BEPetFaceActionView.h           // Pet face action algorithm
│   │       │   │   ├── BEPetFaceActionView.m
│   │       │   │   ├── BEPetFaceInfoView.h             // Pet face info
│   │       │   │   ├── BEPetFaceInfoView.m
│   │       │   │   ├── BEVideoCXXInfoView.h            // Result of c1 c2 video
│   │       │   │   └── BEVideoCXXInfoView.m
│   │       │   ├── avatarDrive                         // Avatar view 
│   │       │   │   ├── BEAvatarDriveView.h
│   │       │   │   └── BEAvatarDriveView.m
│   │       │   ├── backgroundBlur                      // Background blur view
│   │       │   │   ├── BEBackgroundBlurView.h
│   │       │   │   └── BEBackgroundBlurView.m
│   │       │   ├── beauty                              
│   │       │   │   ├── BEBeautyContentDelegate.h
│   │       │   │   ├── BEBeautyContentScrollView.h
│   │       │   │   ├── BEBeautyContentScrollView.m
│   │       │   │   ├── BEBeautyContentView.h
│   │       │   │   ├── BEBeautyContentView.m
│   │       │   │   ├── BEBeautyFaceView.h             // Baautyview
│   │       │   │   ├── BEBeautyFaceView.m
│   │       │   │   ├── BEBeautyHeaderView.h           // Beauty & Face reshape header view
│   │       │   │   ├── BEBeautyHeaderView.m
│   │       │   │   ├── BEBeautyView.h
│   │       │   │   ├── BEBeautyView.m
│   │       │   │   ├── beautyBody                      // Body reshape view
│   │       │   │   │   ├── BEBeautyBodyView.h
│   │       │   │   │   └── BEBeautyBodyView.m
│   │       │   │   ├── makeup
│   │       │   │   │   ├── BEColorListView.h           // Color chosen list view (Beauty & Body Effect pro)
│   │       │   │   │   ├── BEColorListView.m
│   │       │   │   │   ├── BEFilterView.h              // Filter view
│   │       │   │   │   ├── BEFilterView.m
│   │       │   │   │   ├── BEMakeupBlusherView.h       // Makeup - blush
│   │       │   │   │   ├── BEMakeupBlusherView.m
│   │       │   │   │   ├── BEMakeupDelegate.h
│   │       │   │   │   ├── BEMakeupEyeBrowView.h       // Makeup - Brow
│   │       │   │   │   ├── BEMakeupEyeBrowView.m
│   │       │   │   │   ├── BEMakeupEyeLightView.h      // Makeup - Eyelight
│   │       │   │   │   ├── BEMakeupEyeLightView.m
│   │       │   │   │   ├── BEMakeupEyeShadowView.h     // Makeup - Eye shadow
│   │       │   │   │   ├── BEMakeupEyeShadowView.m
│   │       │   │   │   ├── BEMakeupEyelashView.h       // Makeup - Eyelash
│   │       │   │   │   ├── BEMakeupEyelashView.m
│   │       │   │   │   ├── BEMakeupFacialView.h        // Makeup - Contour
│   │       │   │   │   ├── BEMakeupFacialView.m
│   │       │   │   │   ├── BEMakeupHairView.h          // Makeup - HairDye
│   │       │   │   │   ├── BEMakeupHairView.m
│   │       │   │   │   ├── BEMakeupLipsView.h          // Makeup - Lipstick
│   │       │   │   │   ├── BEMakeupLipsView.m
│   │       │   │   │   ├── BEMakeupPlumpView.h         // Makeup - Aegyo-sal
│   │       │   │   │   ├── BEMakeupPlumpView.m
│   │       │   │   │   ├── BEMakeupPupilView.h         // Makeup - Pupil
│   │       │   │   │   ├── BEMakeupPupilView.m
│   │       │   │   │   ├── BEMakeupView.h
│   │       │   │   │   └── BEMakeupView.m
│   │       │   │   └── reshape
│   │       │   │       ├── BEBeautyReshapeBrowView.h       // Face shaping - Brow
│   │       │   │       ├── BEBeautyReshapeBrowView.m
│   │       │   │       ├── BEBeautyReshapeDelegate.h
│   │       │   │       ├── BEBeautyReshapeEyeView.h        // Face shaping - Eye
│   │       │   │       ├── BEBeautyReshapeEyeView.m
│   │       │   │       ├── BEBeautyReshapeFaceView.h       // Face shaping - Face
│   │       │   │       ├── BEBeautyReshapeFaceView.m
│   │       │   │       ├── BEBeautyReshapeMouthView.h      // Face shaping - mouth
│   │       │   │       ├── BEBeautyReshapeMouthView.m
│   │       │   │       ├── BEBeautyReshapeNoseView.h       // Face shaping -Nose
│   │       │   │       ├── BEBeautyReshapeNoseView.m
│   │       │   │       ├── BEBeautyReshapeView.h
│   │       │   │       └── BEBeautyReshapeView.m
│   │       │   ├── public                                  // Public components
│   │       │   │   ├── BEAlgorithmPickerView.h
│   │       │   │   ├── BEAlgorithmPickerView.m
│   │       │   │   ├── BEBeautyItemCell.h
│   │       │   │   ├── BEBeautyItemCell.m
│   │       │   │   ├── BEBeautyTitleCell.h
│   │       │   │   ├── BEBeautyTitleCell.m
│   │       │   │   ├── BEColorItemCell.h
│   │       │   │   ├── BEColorItemCell.m
│   │       │   │   ├── BEColorItemView.h
│   │       │   │   ├── BEColorItemView.m
│   │       │   │   ├── BEContentBaseView.h
│   │       │   │   ├── BEContentBaseView.m
│   │       │   │   ├── BEEffectSwitchTabView.h
│   │       │   │   ├── BEEffectSwitchTabView.m
│   │       │   │   ├── BEEffectTitleCollectionViewCell.h
│   │       │   │   ├── BEEffectTitleCollectionViewCell.m
│   │       │   │   ├── BEStickerPickView.h
│   │       │   │   ├── BEStickerPickView.m
│   │       │   │   ├── NSCollectionViewItem+BEAdd.h
│   │       │   │   └── NSCollectionViewItem+BEAdd.m
│   │       │   ├── sticker                             // Sticker view
│   │       │   │   ├── BEStickerContentView.h
│   │       │   │   ├── BEStickerContentView.m
│   │       │   │   ├── BEStickerView.h
│   │       │   │   └── BEStickerView.m
│   │       │   ├── style_makeup                        // Advance Makeup view
│   │       │   │   ├── BEStyleMakeupContentView.h
│   │       │   │   ├── BEStyleMakeupContentView.m
│   │       │   │   ├── BEStyleMakeupView.h
│   │       │   │   └── BEStyleMakeupView.m
│   │       │   └── virtualBackground                   // Virtual Background
│   │       │       ├── BESelectImageBtn.h
│   │       │       ├── BESelectImageBtn.m
│   │       │       ├── BEVirtualBackgroundView.h
│   │       │       └── BEVirtualBackgroundView.m
│   │       └── license                                 // License related view
│   │           ├── BELicenseInputView.h
│   │           ├── BELicenseInputView.m
│   │           ├── BELicenseView.h
│   │           └── BELicenseView.m
├── ByteEffects.xcodeproj
├── ByteEffects.xcworkspace
├── BytedEffectSDK.podspec
├── EffectManager
│   ├── EffectManager
│   │   ├── EffectHandle.h                          // Packaged the effect related processing interfaces
│   │   ├── EffectHandle.m
│   │   ├── EffectManager.h
│   │   ├── EffectManager.m
│   │   └── utils
│   │       ├── BEImageUtils.h                      // Image transfer util classes, including usual image format transfer
│   │       ├── BEImageUtils.m
│   │       └── BEUtil.h
│   └── EffectManager.xcodeproj
├── include
│   └── BytedEffectSDK                              // effect_sdk header file folder
├── libs
│   └── libeffect.dylib                             // effect_sdk iib file
├── third_include
└── third_lib

```
