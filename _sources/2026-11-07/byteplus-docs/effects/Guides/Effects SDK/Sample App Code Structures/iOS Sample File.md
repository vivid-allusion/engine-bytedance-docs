---
title: "iOS Sample File"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-ios-sample-file"
---

The following shows the file structure of the sample (for iOS) 4.0.0.0 and later.

```Plain
.
├── BEAppDelegate.h
├── BEAppDelegate.m
├── BELog.h
├── BEMacro.h # Macro definition file.
├── BERuseableForm # Related to UIs and list generation.
│   ├── BEForm.h
│   ├── BEForm.m
│   ├── BEFormDescriptor.h
│   ├── BEFormDescriptor.m
│   ├── BEFormDescriptorDelegate.h
│   ├── BEFormRowDescriptor.h
│   ├── BEFormRowDescriptor.m
│   ├── BEFormSectionDescriptor.h
│   ├── BEFormSectionDescriptor.m
│   ├── BEFormViewCoordinator.h
│   └── BEFormViewCoordinator.m
├── Categories # UI-related custom categories.
│   ├── NSArray+BEAdd.h
│   ├── NSArray+BEAdd.m
│   ├── NSString+BEAdd.h
│   ├── NSString+BEAdd.m
│   ├── UICollectionViewCell+BEAdd.h
│   ├── UICollectionViewCell+BEAdd.m
│   ├── UIResponder+BEAdd.h
│   ├── UIResponder+BEAdd.m
│   ├── UITableViewCell+BEAdd.h
│   ├── UITableViewCell+BEAdd.m
│   ├── UIView+BEAdd.h
│   ├── UIView+BEAdd.m
│   ├── UIViewController+BEAdd.h
│   └── UIViewController+BEAdd.m
└── Record
    ├── Models # Models related to demo functions.
    │   ├── BEAlgorithmItem.h
    │   ├── BEAlgorithmItem.m
    │   ├── BEButtonItem.h
    │   ├── BEButtonItem.m
    │   ├── BEComposerNodeModel.h
    │   ├── BEComposerNodeModel.m
    │   ├── BEDynamicActionModel.h
    │   ├── BEDynamicActionModel.m
    │   ├── BEEffectBackup.h
    │   ├── BEEffectBackup.m
    │   ├── BEEffectItem.h
    │   ├── BEEffectItem.m
    │   ├── BEEffectResponseModel.h
    │   ├── BEEffectResponseModel.m
    │   ├── BEModelProvider.h
    │   └── BEModelProvider.m
    ├── Utils # Utility classes related to demo functions.
    │   ├── BEAnimationUtils.h
    │   ├── BEAnimationUtils.m
    │   ├── BEBeautyPickerCommonDefines.h
    │   ├── BEBeautyPickerCommonDefines.m
    │   ├── BECloseableProtocol.h
    │   ├── BEDeviceInfoHelper.h
    │   ├── BEDeviceInfoHelper.m
    │   ├── BEEffectPickerDataStore.h
    │   ├── BEEffectPickerDataStore.m
    │   ├── BEEffectSectionFormViewCoordinator.h
    │   ├── BEEffectSectionFormViewCoordinator.m
    │   ├── BEGlobalData.h
    │   ├── BEGlobalData.m
    │   ├── BEModernEffectPickerControlFactory.h
    │   ├── BEModernEffectPickerControlFactory.m
    │   ├── BEPropertyListSectionFormViewCoordinator.h
    │   ├── BEPropertyListSectionFormViewCoordinator.m
    │   ├── BEStudioConstants.h
    │   ├── BEStudioConstants.m
    │   ├── BETextSizeUtils.h
    │   ├── BETextSizeUtils.m
    │   ├── BEVideoCapture.h # Video capture classes, including camera capture, image capture, video capture, and other methods.
    │   └── BEVideoCapture.m
    ├── manager # Demo data, including special effects, sticker-prompt mappings, demo defaults, etc.
    │   ├── BEEffectDataManager.h
    │   └── BEEffectDataManager.m
    ├── sdk # Encapsulation of SDK APIs, including special effect APIs and algorithm APIs.
    │   ├── BEFrameProcessor.h # Output APIs for both special effects and algorithms.
    │   ├── BEFrameProcessor.m
    │   ├── BERender.h # Implementation of OpenGL drawing, conversion of data types, etc.
    │   ├── BERender.mm
    │   ├── BERenderHelper.h # Implementation of OpenGL drawing.
    │   ├── BERenderHelper.m
    │   ├── BEResourceHelper.h # Resource path APIs for special effects and algorithms.
    │   ├── BEResourceHelper.m
    │   ├── BETimeRecoder.h # Implementation of time recording.
    │   ├── BETimeRecoder.m
    │   ├── algorithm # Algorithm APIs.
    │   │   ├── BEAlgorithmManager.h # External output APIs for algorithms. If only algorithms are used, you can use this file instead of BEFrameProcessor.
    │   │   ├── BEAlgorithmManager.m
    │   │   ├── BEAlgorithmTask.h# Base classes of algorithm modules.
    │   │   ├── BEAlgorithmTask.m
    │   │   └── task # Implementation of all algorithm modules. You can delete unnecessary implementation from this file, but if other files (such as BEAlgorithmManager) contain reference to the deleted implementation, you need to delete relevant reference code from these files.
    │   ├── base # Base classes of the SDK APIs for both algorithms and special effects.
    │   │   ├── BEProcessOutput.h # Input or output data types.
    │   │   ├── BEProcessOutput.m
    │   │   ├── BETask.h
    │   │   ├── BETask.m
    │   │   ├── task
    │   │   │   ├── BEBufferConvertTask.h # Implementation of conversion of buffers.
    │   │   │   ├── BEBufferConvertTask.m
    │   │   │   ├── BETextureConvertTask.h # Implementation of conversion of textures.
    │   │   │   └── BETextureConvertTask.m
    │   │   └── util
    │   └── effect # Special effect APIs.
    │       ├── BEEffectManager.h # External output APIs for special effects. If only special effects are used, you can use this file instead of BEFrameProcessor.
    │       ├── BEEffectManager.m
    │       └── task # Implementation of special effect modules.
    └── ui # Related to UIs.
        ├── algorithm # Algorithm UIs.
        │   ├── cell
        │   ├── ui # Implementation of all algorithm UIs.
        │   ├── vc
        │   └── view
        ├── effect # Special effect UIs.
        │   ├── cell
        │   ├── vc
        │   └── view
        ├── home
        │   ├── vc
        │   └── view
        └── widgets # UI-related implementation of widgets.
            ├── BEActionView.h
            ├── BEActionView.m
            ├── BEButtonView.h
            ├── BEButtonView.m
            ├── BEButtonViewCell.h
            ├── BEButtonViewCell.m
            ├── BECategoryView.h
            ├── BECategoryView.m
            ├── BEEffectSwitchTabView.h
            ├── BEEffectSwitchTabView.m
            ├── BEModernBasePickerView.h
            ├── BEModernBasePickerView.m
            ├── BEModernBasePickerViewCell.h
            ├── BEModernBasePickerViewCell.m
            ├── BEModernFaceBeautyPickerCell.h
            ├── BEModernFaceBeautyPickerCell.m
            ├── BEModernFaceCollectionViewCell.h
            ├── BEModernFaceCollectionViewCell.m
            ├── BEPropertyTextView.h
            ├── BEPropertyTextView.m
            ├── BETextSliderView.h
            └── BETextSliderView.m

```
