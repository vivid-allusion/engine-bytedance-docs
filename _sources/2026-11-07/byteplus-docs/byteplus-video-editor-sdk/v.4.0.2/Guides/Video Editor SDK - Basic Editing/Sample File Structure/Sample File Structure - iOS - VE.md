---
title: "Sample File Structure - iOS - VE"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-sample-file-structure-ios-ve-v.4.0.2"
---

<span id="4dd021b1"></span>
# Overview

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/2cb1c579a4664bbb9907b47b34e85236~tplv-em5hxbkur4-noop.image) </span>

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/f20b7e7aeab9490abdcfeb1664e3947b~tplv-em5hxbkur4-noop.image) </span>

<span id="f88f5f82"></span>
# Video recording

```objectivec
Capture
├── Manager
│  ├── VECapManager+Action.h
│  ├── VECapManager+Action.m
│  ├── VECapManager+Private.h
│  ├── VECapManager.h
│  ├── VECapManager.m
│  ├── VECapProtocol.h
│  └── VEEventCallDefine.h
├── VC
│  ├── VECapBaseViewController+CapLayout.h
│  ├── VECapBaseViewController+CapLayout.m
│  ├── VECapBaseViewController+PrivateForCapVC.h
│  ├── VECapBaseViewController.h
│  ├── VECapBaseViewController.m
│  ├── VECapViewController.h
│  └── VECapViewController.m
├── VEEffectModule
│  ├── Base
│  │  ├── VC
│  │  │  ├── VEEBaseViewController.h
│  │  │  └── VEEBaseViewController.m
│  │  └── View
│  │    ├── VECommonSliderView.h
│  │    ├── VECommonSliderView.m
│  │    ├── VEEBaseView.h
│  │    ├── VEEBaseView.m
│  │    ├── icon_bottombar_reset@3x.png
│  │    ├── icon_bottonbar_dismiss@3x.png
│  │    └── icon_slider_dot@3x.png
│  ├── Filter
│  │  └── View
│  │    ├── VEEFilterView.h
│  │    ├── VEEFilterView.m
│  │    ├── VEEFliteItem.h
│  │    ├── VEEFliteItem.m
│  │    └── icon_fliter@3x.png
│  ├── Sticker
│  │  ├── VC
│  │  │  ├── VEEStickerViewController.h
│  │  │  └── VEEStickerViewController.m
│  │  └── View
│  │    ├── VEEStickerItem.h
│  │    ├── VEEStickerItem.m
│  │    ├── VEEStickerView.h
│  │    ├── VEEStickerView.m
│  │    └── icon_sticker_clear@3x.png
│  └── beauty
│    ├── VC
│    │  ├── VEEBeautyDataSource.h
│    │  ├── VEEBeautyDataSource.m
│    │  ├── VEEBeautyViewController.h
│    │  ├── VEEBeautyViewController.m
│    │  ├── VEEMakeUpSelectBar.h
│    │  ├── VEEMakeUpSelectBar.m
│    │  ├── VEEMakeupViewController.h
│    │  └── VEEMakeupViewController.m
│    └── View
│      ├── VEEBeautyItem.h
│      ├── VEEBeautyItem.m
│      ├── VEEBeautyView.h
│      ├── VEEBeautyView.m
│      └── icon_beauty_compar@3x.png
└── View
  ├── VEBasePreview+gesture.h
  ├── VEBasePreview+gesture.m
  ├── VECPBaseBar.h
  ├── VECPBaseBar.m
  ├── VECPBotomBoxItem.h
  ├── VECPBotomBoxItem.m
  ├── VECPBottomBar.h
  ├── VECPBottomBar.m
  ├── VECPBottomBox.h
  ├── VECPBottomBox.m
  ├── VECPRecordParmView.h
  ├── VECPRecordParmView.m
  ├── VECPRightBar.h
  ├── VECPRightBar.m
  ├── VECPStatusView.h
  ├── VECPStatusView.m
  ├── VECPToolBarBaseView.h
  ├── VECPToolBarBaseView.m
  ├── VECPTopBar.h
  ├── VECPTopBar.m
  ├── VECapBaseCollectionViewCell.h
  ├── VECapBaseCollectionViewCell.m
  ├── VECapBaseView.h
  ├── VECapBaseView.m
  ├── VECapExposureAndFocusView.h
  ├── VECapExposureAndFocusView.m
  ├── VECapPreView.h
  └── VECapPreView.m
```


<span id="25da6d31"></span>
# Video editing

```objectivec
VEStudio
├── EditContext
│  ├── Core
│  │  ├── DVEActionEditor.h
│  │  ├── DVEActionEditor.m
│  │  ├── DVEAnimationEditor.h
│  │  ├── DVEAnimationEditor.m
│  │  ├── DVEAudioEditor.h
│  │  ├── DVEAudioEditor.m
│  │  ├── DVEDraftEditor.h
│  │  ├── DVEDraftEditor.m
│  │  ├── DVEEffectEditor.h
│  │  ├── DVEEffectEditor.m
│  │  ├── DVEFilterEditor.h
│  │  ├── DVEFilterEditor.m
│  │  ├── DVEMaskEditor.h
│  │  ├── DVEMaskEditor.m
│  │  ├── DVEPreviewEditor.h
│  │  ├── DVEPreviewEditor.m
│  │  ├── DVEStickerEditor.h
│  │  ├── DVEStickerEditor.m
│  │  ├── DVETextEditor.h
│  │  ├── DVETextEditor.m
│  │  ├── DVETransitionEditor.h
│  │  ├── DVETransitionEditor.m
│  │  ├── DVEVideoEditor.h
│  │  └── DVEVideoEditor.m
│  ├── DVEBundleDataSource.h
│  ├── DVEBundleDataSource.m
│  ├── NLEEditor_OC+doneAdd.h
│  ├── NLEEditor_OC+doneAdd.m
│  ├── Protocol
│  │  ├── DVECoreActionImp.h
│  │  ├── DVECoreAnimationImp.h
│  │  ├── DVECoreAudioImp.h
│  │  ├── DVECoreDratfImp.h
│  │  ├── DVECoreEffectImp.h
│  │  ├── DVECoreFilterImp.h
│  │  ├── DVECoreImp.h
│  │  ├── DVECoreMaskImp.h
│  │  ├── DVECorePreviewImp.h
│  │  ├── DVECoreStickerImp.h
│  │  ├── DVECoreTextImp.h
│  │  ├── DVECoreTransitionImp.h
│  │  └── DVECoreVideoImp.h
│  ├── VECanvasConfig.h
│  ├── VECanvasConfig.m
│  ├── VEDataCache.h
│  ├── VEDataCache.m
│  ├── VEVCContext+Private.h
│  ├── VEVCContext.h
│  └── VEVCContext.m
├── Manager
│  ├── VEVCCommonDefine.h
│  ├── VEVCManagerProtocol.h
│  ├── VEVideoCutManager+AmazingFeature.h
│  ├── VEVideoCutManager+AmazingFeature.m
│  ├── VEVideoCutManager+Audio.h
│  ├── VEVideoCutManager+Audio.m
│  ├── VEVideoCutManager+Canvas.h
│  ├── VEVideoCutManager+Canvas.m
│  ├── VEVideoCutManager+Cut.h
│  ├── VEVideoCutManager+Cut.m
│  ├── VEVideoCutManager+PicInPic.h
│  ├── VEVideoCutManager+PicInPic.m
│  ├── VEVideoCutManager+Private.h
│  ├── VEVideoCutManager+Regulate.h
│  ├── VEVideoCutManager+Regulate.m
│  ├── VEVideoCutManager+Sticker.h
│  ├── VEVideoCutManager+Sticker.m
│  ├── VEVideoCutManager+Text.h
│  ├── VEVideoCutManager+Text.m
│  ├── VEVideoCutManager+VideoData.h
│  ├── VEVideoCutManager+VideoData.m
│  ├── VEVideoCutManager.h
│  └── VEVideoCutManager.m
├── Provider
│  ├── VECutDataProvider.h
│  ├── VECutDataProvider.m
│  ├── VEResourcePicker.h
│  └── VEResourcePicker.m
├── VC
│  ├── Adapter
│  │  ├── VEMaskEditAdpter.h
│  │  ├── VEMaskEditAdpter.m
│  │  ├── VEStickerEditAdpter.h
│  │  └── VEStickerEditAdpter.m
│  ├── VEVCViewController.h
│  ├── VEVCViewController.m
│  ├── VEVideoCutBaseViewController+Private.h
│  ├── VEVideoCutBaseViewController+layout.h
│  ├── VEVideoCutBaseViewController+layout.m
│  ├── VEVideoCutBaseViewController.h
│  └── VEVideoCutBaseViewController.m
└── View
  ├── DVECommonSliderView.h
  ├── DVECommonSliderView.m
  ├── DVEPickerView
  │  ├── DVEPickerBaseCell.h
  │  ├── DVEPickerBaseCell.m
  │  ├── DVEPickerCategoryBaseCell.h
  │  ├── DVEPickerCategoryBaseCell.m
  │  ├── DVEPickerCategoryTabView.h
  │  ├── DVEPickerCategoryTabView.m
  │  ├── DVEPickerCollectionViewCell.h
  │  ├── DVEPickerCollectionViewCell.m
  │  ├── DVEPickerOverlayView.h
  │  ├── DVEPickerOverlayView.m
  │  ├── DVEPickerUIConfigurationProtocol.h
  │  ├── DVEPickerView.h
  │  ├── DVEPickerView.m
  │  └── DVEPickerViewModels.h
  ├── DVEUIHelper.h
  ├── DVEUIHelper.m
  ├── Modules
  │  ├── Animation
  │  │  ├── VEVCAnimationBar.h
  │  │  ├── VEVCAnimationBar.m
  │  │  ├── VEVCAnimationItem.h
  │  │  └── VEVCAnimationItem.m
  │  ├── Audio
  │  │  ├── VEVCAudioBar.h
  │  │  ├── VEVCAudioBar.m
  │  │  ├── VEVCAudioCell.h
  │  │  ├── VEVCAudioCell.m
  │  │  ├── VEVCAudioPlayer.h
  │  │  ├── VEVCAudioPlayer.m
  │  │  ├── VEVCAudioSelectView.h
  │  │  ├── VEVCAudioSelectView.m
  │  │  ├── VEVCAudioSourceView.h
  │  │  ├── VEVCAudioSourceView.m
  │  │  ├── VEVCLocalAudioView.h
  │  │  ├── VEVCLocalAudioView.m
  │  │  ├── VEVCOnlineAudioView.h
  │  │  └── VEVCOnlineAudioView.m
  │  ├── Crop
  │  │  ├── AVAsset+DVE.h
  │  │  ├── AVAsset+DVE.m
  │  │  ├── DVECropBar.h
  │  │  ├── DVECropBar.m
  │  │  ├── DVECropDefines.h
  │  │  ├── DVECropDefines.m
  │  │  ├── DVECropEditLayer.h
  │  │  ├── DVECropEditLayer.m
  │  │  ├── DVECropEditView.h
  │  │  ├── DVECropEditView.m
  │  │  ├── DVECropGridView.h
  │  │  ├── DVECropGridView.m
  │  │  ├── DVECropPreview.h
  │  │  ├── DVECropPreview.m
  │  │  ├── DVECropRulerView.h
  │  │  ├── DVECropRulerView.m
  │  │  ├── DVEVideoPlayer.h
  │  │  ├── DVEVideoPlayer.m
  │  │  ├── DVEVideoToolBar.h
  │  │  └── DVEVideoToolBar.m
  │  ├── Filter
  │  │  ├── VEVCFilterBar.h
  │  │  ├── VEVCFilterBar.m
  │  │  ├── VEVCFilterItem.h
  │  │  └── VEVCFilterItem.m
  │  ├── Mask
  │  │  ├── VEVCMaskBar.h
  │  │  ├── VEVCMaskBar.m
  │  │  ├── VEVCMaskConfigModel.h
  │  │  ├── VEVCMaskConfigModel.m
  │  │  ├── VEVCMaskItem.h
  │  │  └── VEVCMaskItem.m
  │  ├── MixedEffect
  │  │  ├── DVEMixedEffectBar.h
  │  │  ├── DVEMixedEffectBar.m
  │  │  ├── DVEMixedEffectItem.h
  │  │  ├── DVEMixedEffectItem.m
  │  │  ├── DVEMixedEffectSlider.h
  │  │  └── DVEMixedEffectSlider.m
  │  ├── PicInPic
  │  │  ├── VEVCPicInPicBar.h
  │  │  └── VEVCPicInPicBar.m
  │  ├── Regulate
  │  │  ├── VEVCRegulateBar.h
  │  │  ├── VEVCRegulateBar.m
  │  │  ├── VEVCRegulateItem.h
  │  │  └── VEVCRegulateItem.m
  │  ├── SpecialEffects
  │  │  ├── Models
  │  │  │  ├── DVEEffectsCategoryModel.h
  │  │  │  ├── DVEEffectsCategoryModel.m
  │  │  │  ├── DVEEffectsModel.h
  │  │  │  └── DVEEffectsModel.m
  │  │  └── View
  │  │    ├── DVEEffectsActionObjectBar.h
  │  │    ├── DVEEffectsActionObjectBar.m
  │  │    ├── DVEEffectsBar.h
  │  │    ├── DVEEffectsBar.m
  │  │    ├── DVEEffectsBarBottomView.h
  │  │    ├── DVEEffectsBarBottomView.m
  │  │    ├── DVEEffectsBoarderView.h
  │  │    ├── DVEEffectsBoarderView.m
  │  │    ├── DVEEffectsCategoryCell.h
  │  │    ├── DVEEffectsCategoryCell.m
  │  │    ├── DVEEffectsItemCell.h
  │  │    ├── DVEEffectsItemCell.m
  │  │    ├── DVEEffectsPickerUIDefaultConfiguration.h
  │  │    └── DVEEffectsPickerUIDefaultConfiguration.m
  │  ├── Sticker
  │  │  ├── VEVCStickerBar.h
  │  │  ├── VEVCStickerBar.m
  │  │  ├── VEVCStickerItem.h
  │  │  └── VEVCStickerItem.m
  │  ├── Text
  │  │  ├── DVEFlowerText
  │  │  │  ├── DVBTextTemplatePickerCell.h
  │  │  │  ├── DVBTextTemplatePickerCell.m
  │  │  │  ├── DVEFlowerTextClearCell.h
  │  │  │  ├── DVEFlowerTextClearCell.m
  │  │  │  ├── DVETextTemplatePickerCategoryCell.h
  │  │  │  ├── DVETextTemplatePickerCategoryCell.m
  │  │  │  ├── DVETextTemplatePickerUIDefaultConfiguration.h
  │  │  │  ├── DVETextTemplatePickerUIDefaultConfiguration.m
  │  │  │  └── Models
  │  │  │    ├── DVBTextTemplateCategoryModel.h
  │  │  │    ├── DVBTextTemplateCategoryModel.m
  │  │  │    ├── DVBTextTemplateModel.h
  │  │  │    └── DVBTextTemplateModel.m
  │  │  ├── VEVCTextBar.h
  │  │  ├── VEVCTextBar.m
  │  │  ├── VEVCTextParm.h
  │  │  ├── VEVCTextParm.m
  │  │  └── VEVCTextStyle
  │  │    ├── VEVCTextBaseCell.h
  │  │    ├── VEVCTextBaseCell.m
  │  │    ├── VEVCTextBaseStyleCell.h
  │  │    ├── VEVCTextBaseStyleCell.m
  │  │    ├── VEVCTextColorCell.h
  │  │    ├── VEVCTextColorCell.m
  │  │    ├── VEVCTextCommonItem.h
  │  │    ├── VEVCTextCommonItem.m
  │  │    ├── VEVCTextFontCell.h
  │  │    ├── VEVCTextFontCell.m
  │  │    ├── VEVCTextStyleView.h
  │  │    └── VEVCTextStyleView.m
  │  ├── Transition
  │  │  ├── VEVCTransitionBar.h
  │  │  ├── VEVCTransitionBar.m
  │  │  ├── VEVCTransitionItem.h
  │  │  └── VEVCTransitionItem.m
  │  ├── VEPopSelectView
  │  │  ├── VEPopSelectItem.h
  │  │  ├── VEPopSelectItem.m
  │  │  ├── VEPopSelectView.h
  │  │  └── VEPopSelectView.m
  │  ├── VEVCBarManager.h
  │  ├── VEVCBarManager.m
  │  ├── VEVCSecondaryBar
  │  │  ├── VEVCSecondaryBar+Cut.h
  │  │  ├── VEVCSecondaryBar+Cut.m
  │  │  ├── VEVCSecondaryBar+Sticker.h
  │  │  ├── VEVCSecondaryBar+Sticker.m
  │  │  ├── VEVCSecondaryBar+StickerPrivate.h
  │  │  ├── VEVCSecondaryBar+private.h
  │  │  ├── VEVCSecondaryBar.h
  │  │  └── VEVCSecondaryBar.m
  │  ├── canvas
  │  │  ├── VEVCCanvasBar.h
  │  │  └── VEVCCanvasBar.m
  │  ├── cut
  │  │  ├── VEVCCutBar.h
  │  │  └── VEVCCutBar.m
  │  └── speed
  │    ├── VEVCCuverItem.h
  │    ├── VEVCCuverItem.m
  │    ├── VEVCCuverSpeedBar.h
  │    ├── VEVCCuverSpeedBar.m
  │    ├── VEVCSpeedBar.h
  │    └── VEVCSpeedBar.m
  ├── VECanvasVideoBorderView.h
  ├── VECanvasVideoBorderView.m
  ├── VEVCBaseBar.h
  ├── VEVCBaseBar.m
  ├── VEVCBaseView.h
  ├── VEVCBaseView.m
  ├── VEVCBottomBar.h
  ├── VEVCBottomBar.m
  ├── VEVCModuleItem.h
  ├── VEVCModuleItem.m
  ├── VEVCPreview.h
  ├── VEVCPreview.m
  ├── VEVCTopBar.h
  ├── VEVCTopBar.m
  ├── VEVCTopVideoView.h
  ├── VEVCTopVideoView.m
  ├── VEVCVideoToolBar.h
  └── VEVCVideoToolBar.m
```
