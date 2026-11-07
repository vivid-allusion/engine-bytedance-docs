---
title: "Sample File Structure - iOS - Magic Template"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-sample-file-structure-sdk-magic-template-1-v.4.0.2"
---

<span id="Overview"></span>
# **Overview**

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/a6c5c0115ca94e3ea0ee61b5c4992773~tplv-em5hxbkur4-noop.image) </span>

<span id="UI source code structure"></span>
# **UI** **source code structure**

```Ruby
UI

├── Categories # General categories

│  ├── NSArray+CSIFAdditions.h

│  ├── NSArray+CSIFAdditions.m

│  ├── UIKit # UIKit categories

│  │  ├── UIButton+CSIFAdditions.h

│  │  ├── UIButton+CSIFAdditions.m

│  │  ├── UIColor+CSIFAdditions.h

│  │  ├── UIColor+CSIFAdditions.m

│  │  ├── UIImage+CSIFAdditions.h

│  │  ├── UIImage+CSIFAdditions.m

│  │  ├── UIImage+MV.h

│  │  ├── UIImage+MV.m

│  │  ├── UIView+CSIFMasonry.h

│  │  ├── UIView+CSIFMasonry.m

│  │  ├── UIView+CSIFUIKit.h

│  │  ├── UIView+CSIFUIKit.m

│  │  ├── UIViewController+CSIFUIKitEmptyPage.h

│  │  └── UIViewController+CSIFUIKitEmptyPage.m

│  ├── UIScrollView+CSIFInfiniteScrolling.h

│  ├── UIScrollView+CSIFInfiniteScrolling.m

│  ├── UIViewController+CSIFGradientView.h

│  └── UIViewController+CSIFGradientView.m

├── Managers #  Management tools

│  ├── CSIFWorksCropEditManager.h

│  └── CSIFWorksCropEditManager.m

├── Resources  #  Resource directories

│  └── TOCResource_default 

├── Scenes # User scenarios

│  ├── Feeds #  The list of templates.

│  │  ├── Models

│  │  │  ├── CSIFCategoryMVTemplatesDataController.h

│  │  │  ├── CSIFCategoryMVTemplatesDataController.m

│  │  │  ├── CSIFMVTemplateTabContentProvider.h

│  │  │  └── CSIFMVTemplateTabContentProvider.m

│  │  ├── Protocols

│  │  │  ├── CSIFSlidePushContextProviderProtocol.h

│  │  │  └── CSIFZoomContextProviderProtocol.h

│  │  ├── ViewModels

│  │  │  ├── CSIFMVTemplatesTransitionDelegate.h

│  │  │  ├── CSIFMVTemplatesTransitionDelegate.m

│  │  │  ├── CSIFZoomPopAnimator.h

│  │  │  ├── CSIFZoomPopAnimator.m

│  │  │  ├── CSIFZoomPushAnimator.h

│  │  │  └── CSIFZoomPushAnimator.m

│  │  ├── Viewcontrollers

│  │  │  ├── CSIFMVTemplatesTabViewController.h

│  │  │  ├── CSIFMVTemplatesTabViewController.m

│  │  │  ├── CSIFSlidingTabViewController.h

│  │  │  ├── CSIFSlidingTabViewController.m

│  │  │  ├── CSIFWaterfallViewController.h

│  │  │  └── CSIFWaterfallViewController.m

│  │  └── Views

│  │    ├── CSIFMVTemplateCollectionViewCell.h

│  │    ├── CSIFMVTemplateCollectionViewCell.m

│  │    ├── CSIFWaterfallCollectionViewLayout.h

│  │    └── CSIFWaterfallCollectionViewLayout.m

│  ├── MaterialEdit # Editing views

│  │  ├── PhotoEdit

│  │  │  ├── Models

│  │  │  │  ├── CSIFFragmentBridgeFragment.h

│  │  │  │  └── CSIFFragmentBridgeFragment.m

│  │  │  ├── Protocols

│  │  │  │  └── CSIFCutSameStylePreviewFragmentProtocol.h

│  │  │  └── Views

│  │  │    ├── CSIFCutSameCropMaskView.h

│  │  │    ├── CSIFCutSameCropMaskView.m

│  │  │    ├── CSIFPlaybackView.h

│  │  │    ├── CSIFPlaybackView.m

│  │  │    ├── CSIFWorksCropEditView.h

│  │  │    └── CSIFWorksCropEditView.m

│  │  ├── TextEdit

│  │  │  ├── Models

│  │  │  ├── ViewController

│  │  │  │  ├── CSIFMVTextEditorViewController.h

│  │  │  │  └── CSIFMVTextEditorViewController.m

│  │  │  └── Views

│  │  │    ├── CSIFMVTextEditorCollectionViewCell.h

│  │  │    ├── CSIFMVTextEditorCollectionViewCell.m

│  │  │    ├── CSIFMVTextEditorInputView.h

│  │  │    ├── CSIFMVTextEditorInputView.m

│  │  │    ├── CSIFMVTextEditorTableViewCell.h

│  │  │    └── CSIFMVTextEditorTableViewCell.m

│  │  └── VideoEdit

│  │    ├── Protocols

│  │    │  └── CSIFCutSameStyleCropEditManagerProtocol.h

│  │    ├── ViewControllers

│  │    │  ├── CSIFVideoEditViewController.h

│  │    │  └── CSIFVideoEditViewController.m

│  │    └── Views

│  │      ├── CSIFCutSameVideoThumbnailCell.h

│  │      ├── CSIFCutSameVideoThumbnailCell.m

│  │      ├── CSIFWorksPreviewVideoEditView.h

│  │      ├── CSIFWorksPreviewVideoEditView.m

│  │      └── VideoRangeSlider

│  │        ├── CSIFSliderLeft.h

│  │        ├── CSIFSliderLeft.m

│  │        ├── CSIFSliderRight.h

│  │        ├── CSIFSliderRight.m

│  │        ├── CSIFVideoRangeSlider.h

│  │        └── CSIFVideoRangeSlider.m

│  ├── PhotoAlbum # Albums

│  │  ├── AlbumTransition

│  │  │  ├── CSIFAlbumTransitionAnimationController.h

│  │  │  ├── CSIFAlbumTransitionAnimationController.m

│  │  │  ├── CSIFAlbumTransitionContextProvider.h

│  │  │  ├── CSIFAlbumTransitionDelegateProtocol.h

│  │  │  ├── CSIFAlbumTransitionInteractionController.h

│  │  │  ├── CSIFAlbumTransitionInteractionController.m

│  │  │  ├── CSIFAlbumZoomTransition.h

│  │  │  ├── CSIFAlbumZoomTransition.m

│  │  │  ├── CSIFAlbumZoomTransitionDelegate.h

│  │  │  └── CSIFAlbumZoomTransitionDelegate.m

│  │  ├── Controllers

│  │  │  ├── CSIFPhotoManager.h

│  │  │  └── CSIFPhotoManager.m

│  │  ├── Models

│  │  │  ├── CSIFAlbumDataModel.h

│  │  │  ├── CSIFAlbumDataModel.m

│  │  │  ├── CSIFAlbumDefinition.h

│  │  │  ├── CSIFAlbumDefinition.m

│  │  │  ├── CSIFAlbumInputData.h

│  │  │  ├── CSIFAlbumInputData.m

│  │  │  ├── CSIFAlbumSectionModel.h

│  │  │  ├── CSIFAlbumSectionModel.m

│  │  │  └── CSIFPhotoAlbumDefine.h

│  │  ├── Protocol

│  │  │  ├── CSIFAlbumConfigProtocol.h

│  │  │  ├── CSIFPhotosProtocol.h

│  │  │  ├── CSIFSelectedAssetsBottomViewProtocol.h

│  │  │  └── CSIFSelectedAssetsViewProtocol.h

│  │  ├── ViewControllers

│  │  │  ├── CSIFAlbumFactoryManager.h

│  │  │  ├── CSIFAlbumFactoryManager.m

│  │  │  ├── CSIFAlbumListViewController.h

│  │  │  ├── CSIFAlbumListViewController.m

│  │  │  ├── CSIFAlbumViewController.h

│  │  │  ├── CSIFAlbumViewController.m

│  │  │  ├── CSIFStudioAlbumViewController.h

│  │  │  ├── CSIFStudioAlbumViewController.m

│  │  │  └── Preview

│  │  │    ├── CSIFAlbumPreviewAndSelectController.h

│  │  │    ├── CSIFAlbumPreviewAndSelectController.m

│  │  │    ├── CSIFAlbumVideoPreviewController.h

│  │  │    └── CSIFAlbumVideoPreviewController.m

│  │  ├── ViewModels

│  │  │  ├── CSIFAlbumAssetListSectionController.h

│  │  │  ├── CSIFAlbumAssetListSectionController.m

│  │  │  ├── CSIFAlbumConfigViewModel.h

│  │  │  ├── CSIFAlbumConfigViewModel.m

│  │  │  ├── CSIFAlbumViewModel.h

│  │  │  ├── CSIFAlbumViewModel.m

│  │  │  ├── CSIFAlbumViewUIConfig.h

│  │  │  └── CSIFAlbumViewUIConfig.m

│  │  └── Views

│  │    ├── AlbumSelectView

│  │    │  ├── CSIFImportSelectBottomView.h

│  │    │  ├── CSIFImportSelectBottomView.m

│  │    │  ├── CSIFImportSelectCollectionViewCell.h

│  │    │  ├── CSIFImportSelectCollectionViewCell.m

│  │    │  ├── CSIFImportSelectView.h

│  │    │  └── CSIFImportSelectView.m

│  │    ├── CSIFAlbumAssetListCell.h

│  │    ├── CSIFAlbumAssetListCell.m

│  │    ├── CSIFAlbumCategorylistCell.h

│  │    ├── CSIFAlbumCategorylistCell.m

│  │    ├── CSIFAlbumContainerProtocol.h

│  │    ├── CSIFAlbumDenyAccessView.h

│  │    ├── CSIFAlbumDenyAccessView.m

│  │    ├── CSIFAlbumGoSettingStrip.h

│  │    ├── CSIFAlbumGoSettingStrip.m

│  │    ├── CSIFAlbumListBlankView.h

│  │    ├── CSIFAlbumListBlankView.m

│  │    ├── CSIFAlbumPhotoPreviewAndSelectCell.h

│  │    ├── CSIFAlbumPhotoPreviewAndSelectCell.m

│  │    ├── CSIFAlbumPreviewAndSelectCell.h

│  │    ├── CSIFAlbumPreviewAndSelectCell.m

│  │    ├── CSIFAlbumRequestAccessView.h

│  │    ├── CSIFAlbumRequestAccessView.m

│  │    ├── CSIFAlbumVCNavView.h

│  │    ├── CSIFAlbumVCNavView.m

│  │    ├── CSIFAlbumVerticalSliderView.h

│  │    ├── CSIFAlbumVerticalSliderView.m

│  │    ├── CSIFAlbumVideoPreviewAndSelectCell.h

│  │    ├── CSIFAlbumVideoPreviewAndSelectCell.m

│  │    ├── CSIFAllowMultiSelectBottomButton.h

│  │    ├── CSIFAllowMultiSelectBottomButton.m

│  │    ├── CSIFCircularProgressView.h

│  │    ├── CSIFCircularProgressView.m

│  │    ├── CSIFFirstCreativeSelectedAssetsBottomView.h

│  │    ├── CSIFFirstCreativeSelectedAssetsBottomView.m

│  │    ├── CSIFImageRightButton.h

│  │    ├── CSIFImageRightButton.m

│  │    ├── CSIFNoEventView.h

│  │    ├── CSIFNoEventView.m

│  │    ├── CSIFReorderableForCollectionViewFlowLayout.h

│  │    └── CSIFReorderableForCollectionViewFlowLayout.m

│  ├── TemplateDetail

│  │  ├── Models

│  │  │  ├── CSIFMVTemplatesContentProvider.h

│  │  │  ├── CSIFMVTemplatesContentProvider.m

│  │  │  └── CSIFMVTemplatesDataControllerProtocol.h

│  │  ├── VIewControllers

│  │  │  ├── CSIFMVTemplateDetailTableViewCell.h

│  │  │  ├── CSIFMVTemplateDetailTableViewCell.m

│  │  │  ├── CSIFMVTemplateDetailViewController.h

│  │  │  ├── CSIFMVTemplateDetailViewController.m

│  │  │  ├── CSIFMVTemplateInteractionViewController.h

│  │  │  ├── CSIFMVTemplateInteractionViewController.m

│  │  │  ├── CSIFMVTemplateVideoPlayViewController.h

│  │  │  ├── CSIFMVTemplateVideoPlayViewController.m

│  │  │  ├── CSIFMVTemplatesDetailTableViewController.h

│  │  │  ├── CSIFMVTemplatesDetailTableViewController.m

│  │  │  ├── CSIFSwipeUpGuideViewController.h

│  │  │  └── CSIFSwipeUpGuideViewController.m

│  │  └── Views

│  │    ├── CSIFLoadingAndVolumeView.h

│  │    └── CSIFLoadingAndVolumeView.m

│  └── WorkPreview

│    ├── Protocols

│    │  └── CSIFCutSameWorksPreviewBottomViewProtocol.h

│    ├── ViewControllers

│    │  ├── CSIFExportViewController.h

│    │  ├── CSIFExportViewController.m

│    │  ├── CSIFWorksPreviewViewController.h

│    │  └── CSIFWorksPreviewViewController.m

│    └── Views

│      ├── CSIFCutSamePlayerControlView.h

│      ├── CSIFCutSamePlayerControlView.m

│      ├── CSIFPlayerControlView.h

│      ├── CSIFPlayerControlView.m

│      ├── CSIFVideoListCell.h

│      ├── CSIFVideoListCell.m

│      ├── CSIFWorksPreviewSegmentsView.h

│      └── CSIFWorksPreviewSegmentsView.m

├── Services #  API services

│  ├── Impls

│  │  ├── CSIFCounterDataViewImpl.h

│  │  ├── CSIFCounterDataViewImpl.m

│  │  ├── CSIFLoadingViewDefaultImpl.h

│  │  ├── CSIFLoadingViewDefaultImpl.m

│  │  ├── CSIFToastImpl.h

│  │  └── CSIFToastImpl.m

│  └── Protocols

│    ├── CSIFBaseServiceContainerProtocol.h

│    └── ServiceProtocols

│      ├── CSIFAlbumViewControllerProtocol.h

│      ├── CSIFWebImageProtocol.h

│      ├── UIKits

│      │  ├── CSIFAlertProtocol.h

│      │  ├── CSIFBubbleProtocol.h

│      │  ├── CSIFCounterDataViewProtocol.h

│      │  ├── CSIFLoadingViewProtocol.h

│      │  └── CSIFToastProtocol.h

│      ├── ViewControllers

│      │  └── CSIFWorksPreviewViewControllerProtocol.h

│      └── WorkflowService

│        └── CSIFSelectAlbumAssetsProtocol.h

├── UIKIts # View files

│  ├── CSIFAlertViewController.h

│  ├── CSIFAlertViewController.m

│  ├── CSIFAnimatedButton.h

│  ├── CSIFAnimatedButton.m

│  ├── CSIFButton.h

│  ├── CSIFButton.m

│  ├── CSIFCornerBarNaviController.h

│  ├── CSIFCornerBarNaviController.m

│  ├── CSIFGradientView.h

│  ├── CSIFGradientView.m

│  ├── CSIFLoadMoreFooter.h

│  ├── CSIFLoadMoreFooter.m

│  ├── CSIFLoadingViewController.h

│  ├── CSIFLoadingViewController.m

│  ├── CSIFMvAmountView.h

│  ├── CSIFMvAmountView.m

│  ├── CSIFNavigationController.h

│  ├── CSIFNavigationController.m

│  ├── CSIFRefreshHeader.h

│  ├── CSIFRefreshHeader.m

│  ├── CSIFTapticEngineManager.h

│  ├── CSIFTapticEngineManager.m

│  ├── ResourceManager

│  │  ├── CSIFColorNameDefines.h

│  │  └── CSIFColorNameDefines.m

│  └── SlidingViewController

│    ├── CSIFSlidingScrollView.h

│    ├── CSIFSlidingScrollView.m

│    ├── CSIFSlidingTabbarProtocol.h

│    ├── CSIFSlidingTabbarView.h

│    ├── CSIFSlidingTabbarView.m

│    ├── CSIFSlidingViewController.h

│    └── CSIFSlidingViewController.m

└── Utils # Tools

  ├── CSIFDeviceAuth.h

  ├── CSIFDeviceAuth.m

  ├── CSIFResponder.h

  └── CSIFResponder.m
```
