---
title: "Windows Sample File"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-windows-sample-file"
---

The following shows the file structure of the sample (for Windows) **4.3.0 and later**.

```json

│  build.bat                       
│  build_64.bat
│  CMakeLists.txt
│  CMakeLists.txt.user
│  
├─Algorithm
│  │  AlgorithmDefine.h
│  │  BEAlgorithmManager.cpp                        // Algorithm related process
│  │  BEAlgorithmManager.h
│  │  BEProcessOutput.h                                        // Algorithm related output
│  │  be_util.cpp
│  │  be_util.h
│  │  CMakeLists.txt
│  │  IAlgorithmManager.h                                // Algorithm module related interfaces
│  │  
│  └─AlgorithmTask                                                
│          BEAlgorithmTask.cpp                        // Algorithm process task basic classes
│          BEAlgorithmTask.h
│          BEC1AlgorithmTask.cpp                // c1 algorithm
│          BEC1AlgorithmTask.h
│          BEC2AlgorithmTask.cpp                // c2 algorithm
│          BEC2AlgorithmTask.h
│          BEFaceAlgorithmTask.cpp                // Face keypoint algorithm
│          BEFaceAlgorithmTask.h
│          BEFaceAttrAlgorithmTask.cpp        // Face arribute algorithm
│          BEFaceAttrAlgorithmTask.h
│          BEFaceImageAlgorithmTask.cpp  
│          BEFaceImageAlgorithmTask.h
│          BEFaceVerifyAlgorithmTask.cpp  
│          BEFaceVerifyAlgorithmTask.h
│          BEGazeEstimationAlgorithmTask.cpp        // Gaze estimation algorithm
│          BEGazeEstimationAlgorithmTask.h
│          BEHairParseAlgorithmTask.cpp                        // Hair segmentation algorithm
│          BEHairParseAlgorithmTask.h
│          BEHandAlgorithmTask.cpp                                // Hand detection algorithm, gesture detection algorithm
│          BEHandAlgorithmTask.h
│          BEHeadSegAlgorithmTask.cpp                        // Head segmentation algorithm
│          BEHeadSegAlgorithmTask.h
│          BELightClsAlgorithmTask.cpp                        // Light detection algorithm
│          BELightClsAlgorithmTask.h
│          BEPetFaceAlgorithmTask.cpp                        // Pet face detection algorithm
│          BEPetFaceAlgorithmTask.h
│          BEPortraitMattingAlgorithmTask.cpp        // Matting algorithm
│          BEPortraitMattingAlgorithmTask.h
│          BESkeletonAlgorithmTask.cpp                        // Body keypoint algorithm
│          BESkeletonAlgorithmTask.h
│          BETask.cpp
│          BETask.h
│          BETaskFactory.cpp
│          BETaskFactory.h
│          BETaskKey.cpp
│          BETaskKey.h
│          BEVideoClsAlgorithmTask.cpp                        // Video clus algorithm
│          BEVideoClsAlgorithmTask.h
│          
├─app
│  │  app.rc
│  │  CMakeLists.txt
│  │  
│  ├─resource
│  │  └─qml
│  │          AlgorithmContainer.qml                        // Algorithm UI layout
│  │          AlgorithmListView.qml                                // Algorithm list UI
│  │          BeautyListItem.qml                                // Beauty Effect list layout
│  │          BESwitch.qml
│  │          ContentContainer.qml                                
│  │          EffectContainer.qml                                // Effect related container layout
│  │          FaceAlgorithmListView.qml                        // Face detection algorithm list view
│  │          FaceAlgorithmView.qml                                // Face detection algorithm output UI
│  │          FaceAttrAlgorithmView.qml                        // Face attribute algorithm output UI
│  │          FaceVerifyAlgorithmView.qml                
│  │          FaceVerifyImageView.qml                        
│  │          FilterList.qml                                                // Filter list
│  │          GazeEstimationAlgorithmView.qml                // Gaze estimation algorithm output UI
│  │          HandAlgorithmView.qml                                        // Gesture detection algorithm output UI
│  │          LicenseInputView.qml                                        // License input
│  │          LightClsAlgorithmView.qml                                // Light detection algorithm output UI
│  │          main.qml                                                                
│  │          MakeupList.qml                                                // Makeup list
│  │          OperateButton.qml
│  │          PetFaceAlgorithmView.qml                                // Pet face detection algorithm output UI
│  │          PicQualityContainer.qml                                
│  │          PopupTips.qml
│  │          PopupTipsModal.qml
│  │          ProfileShowContainer.qml                                // Performance related date output UI
│  │          ResizeItem.qml
│  │          RightContainer.qml                                        
│  │          RoundCornorButton.qml
│  │          SettingWindow.qml                                                // Setting view
│  │          StickerListView.qml                                        // Sticker list view layout
│  │          StyleText.qml
│  │          TabAnimoji.qml                                                // Avatar tab 
│  │          TabBeautyEffects.qml                                        // Beauty & Body Effects tab
│  │          TabBeautyEffectsPro.qml                                // Beauty & Body Effects Pro tab
│  │          TabBlurBackground.qml                                
│  │          TabNovelSticker.qml                                        // Advanced Sticker tab
│  │          TabSticker.qml                                                // Sticker tab
│  │          TabStyleMakeup.qml                                        // Advanced Makeup Set tab
│  │          TabVirtualBackground.qml                                // Virtual Background tab
│  │          TextButton.qml
│  │          TextLinearButton.qml
│  │          VideoCXAlgorithmView.qml                                // Video clus c1 c2 algorithm output UI
│  │          WindowTitle.qml
│  │          
│  └─source
│      ├─camera
│      │      VideoFilter.cpp                                                // Camera processing including switching camera, camera resolution, etc.
│      │      VideoFilter.h
│      │      VideoSurface.cpp                                                // videosurface receive and process camera original video frame
│      │      VideoSurface.h
│      │      
│      ├─licenseManager                                                                // License related code
│      │      license_check.cpp
│      │      license_check.h
│      │      license_requester.cpp
│      │      license_requester.h
│      │      misc.h
│      │      
│      ├─main
│      │      main.cpp
│      │      ModuleHelper.cpp                                                // Module loading
│      │      ModuleHelper.h
│      │      
│      ├─model
│      │      bedatamanager.cpp                                                // Resource management class, associated resource id, resource path, resource key and other data
│      │      bedatamanager.h
│      │      BEResourceModel.cpp                                        // Resource ID and type define
│      │      BEResourceModel.h
│      │      BEResourceProvider.cpp                                // Resource path management
│      │      BEResourceProvider.h
│      │      
│      ├─renderHelper                                                                // Rendering related code, basically the rendering output of algorithms
│      │      be_program.cpp
│      │      be_program.h
│      │      be_render.cpp
│      │      be_render.h
│      │      be_render_define.h
│      │      be_render_helper.cpp
│      │      be_render_helper.h
│      │      
│      └─viewController                                                                // Every modules' viewController，communicating with qml layer
│              BEAlgorithmVC.cpp                                        // Algorithm related
│              BEAlgorithmVC.h
│              BEBeautyEffectVC.cpp                                        // Effect process VC
│              BEBeautyEffectVC.h
│              BEFaceAttrInfoVC.cpp                                        // Face attribute VC
│              BEFaceAttrInfoVC.h
│              BEFaceDetectInfoVC.cpp                                // Face detection VC
│              BEFaceDetectInfoVC.h
│              BEGazeEstimationInfoVC.cpp                        // Gaze estimation VC
│              BEGazeEstimationInfoVC.h
│              BEHandDetectInfoVC.cpp                                // Hand detection VC
│              BEHandDetectInfoVC.h
│              BELicenseVC.cpp                                                // License detection and download VC
│              BELicenseVC.h
│              BELightClassifyInfoVC.cpp                        // Light detection VC
│              BELightClassifyInfoVC.h
│              BEMainVC.cpp
│              BEMainVC.h
│              BEPetfaceInfoVC.cpp                                        // Pet face detection VC
│              BEPetfaceInfoVC.h
│              BEProfileVC.cpp                                                // Performance VC
│              BEProfileVC.h
│              BEVCManager.cpp                                                // viewcontroller management class
│              BEVCManager.h
│              BEVideoInfoVC.cpp                                        // video cluster c1 c2 VC
│              BEVideoInfoVC.h
│              
├─EffectManager
│  │  be_util.cpp
│  │  be_util.h
│  │  CMakeLists.txt
│  │  EffectHandle.cpp                                                                // effect process，packaged bef_effect_handle_t related most of effect processing，including composer resources, stickers, filters interfaces calling
│  │  EffectHandle.h
│  │  EffectManager.cpp                                                                // effecthandle management，including loading dependenced third party libs
│  │  EffectManager.h
│  │  EffectManagerDefine.h                                                        
│  │  IEffectManager.h                                                                // EffectManager module interfaces classes
│  │  PBOReader.h                                                                        // pbo reading texture
│  │  
│  └─utils                                                                                        // effect utils, related context, format transfer, package rendering thread, etc
│          BEFColorConverter.cpp
│          BEFColorConverter.h
│          BEFEffectGLContext.cpp
│          BEFEffectGLContext.h
│          BEFEffectThread.cpp
│          BEFEffectThread.h
│          BEFPlatformDefine.h
│          
└─third  // third party libs

```
