---
title: "Detailed Development Guide - iOS - VE SDK"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-detailed-development-guide-ios-ve-sdk-v.4.0.2"
---

<span id="632528ca"></span>
# Video recording

<span id="aab7f1bb"></span>
## Initialization


* Configure parameters.

* API definition: You can call the **IESMMCameraConfig** API to initialize required parameters before you initialize the camera. For details about the feature of each attribute, see the header file. If you have any questions, leave comments in the file.

* How to use


```objectivec
    _config = [[IESMMCameraConfig alloc] init];
    _config.enableFaceuExposureOptimize = YES;
    _config.cameraPosition        = AVCaptureDevicePositionBack;
    _config.previewModeType       = IESPreviewModePreserveAspectRatio;
     
    _config.videoData          = [HTSVideoData videoData];
     
    _config.capturePreset        = self.curPreset;
    if (_currentPreviewType == VECPCurrentPreViewTypeDuet) {
      self.duetPlayerTimes = [NSMutableArray new];
      _config.captureRatio         = IESMMCaptureRatioAuto;
    } else {
      _config.captureRatio         = self.curRatio;
    }
     
     
    _config.customSwitchAnimation    = NO;
    _config.noDropFirstStartCaptureFrame  = YES;
    _config.dropFrameCount        = 3;
    _config.noNeedEffectFrameCount    = 3;
    _config.enableTapFocus  = YES;
    _config.useSDKGesture = NO;
    _config.enableTapexposure  = YES;
    _config.preferredBackZoomFactor = 1;
    _config.preferredFrontZoomFactor = 1;
     
     
    if (@available(iOS 13.0,*)) {
      _config.preferredRearCameraDeviceTypes = @[AVCaptureDeviceTypeBuiltInTripleCamera,AVCaptureDeviceTypeBuiltInDualWideCamera,AVCaptureDeviceTypeBuiltInDualCamera];
    }
     
    _config.landscapeDetectEnable  = YES;
```



* Create a recording object.

* You can call the **IESMMRecoder** class for recording.

* How to use

* Create a recording object.

   Note: Initialization may take a while. Perform subsequent operations in the **cameraComplete** block.


```objectivec
self.recorder            = [[IESMMRecoder alloc] initWithView:preview
                                   config:self.config
                               cameraComplete:^{
    @strongify(self);
    [self startAuthor];
    [self addObserver];
    [self initProcessBlock];
    [self initMotion];
  }];
```



* Requests the user to grant permissions to access the device.

* How to use


```objectivec
- (void)startAuthor
{
   
  [IESMMCameraDeviceAuthor cameraAuthorzied:^(BOOL authorzied) {
    if (authorzied) {
      [self.recorder startVideoCapture];
      self.isVideoPreviewing = @(YES);
    } else {
      dispatch_async(dispatch_get_main_queue(), ^{
        [VEDToast showInfo:@"Please grant access to the camera."];

      });
    }
  }];
  [IESMMCameraDeviceAuthor microphoneAuthorzied:^(BOOL authorzied) {
    if (authorzied) {
      [self.recorder startAudioCapture];
      self.isAudioPreviewing = @(YES);
       
    } else {
      dispatch_async(dispatch_get_main_queue(), ^{
        [VEDToast showInfo:@"Please grant access to the microphone."];

      });
    }
  }];
   
  // Control by your choice
  [IESMMDeviceAuthor setCustomPlayBackCategoryOption:AVAudioSessionCategoryOptionMixWithOthers];
  [IESMMDeviceAuthor allowMixAudioWithOthersDuringRecord:YES];
   
}
```



* Note: Grant video and audio capture permissions after you grant access to the camera and microphone.

* Start media capture.


```objectivec
[self.recorder startVideoCapture];
[self.recorder startAudioCapture];
```



* Set **ProcessBlock** as required. You do not need to set it for all operations.

* Current original frame


```objectivec
[self.recorder setVideoBufferCallback:^(CVPixelBufferRef _Nonnull pixelBuffer, CMTime pts) {
  }];
```



* Current effect frame


```objectivec
[self.recorder setVideoProcessedBufferCallback:^(CVPixelBufferRef _Nonnull pixelBuffer, CMTime pts) {

  }];
```



* Current audio frame


```objectivec
[self.recorder setAudioBufferCallback:^(CMSampleBufferRef _Nonnull samplebuffer) {

  }];
```



* First frame rendering


```objectivec
[self.recorder setFirstRenderBlock:^{
  }];
```



* **IESCameraAction**: runs change callbacks for different actions.


```objectivec
[self.recorder setIESCameraActionBlock:^(IESCameraAction action, NSError * _Nullable error, id _Nullable data) {
    @strongify(self);
    switch (action) {
      case IESCameraDidStartVideoCapture:
       
        break;
      case IESCameraDidStartAudioCapture:
        NSLog(@"IESflow--IESCameraDidStartAudioCapture");
        break;
      case IESCameraDidStopVideoCapture:
      {
        [self.recorder setTorchOn:NO];
      }
        break;
      case IESCameraDidStartVideoRecord:
      {
        if (self.duetURL) {
          self.durationType = VECPRecordDurationTypeDuet;
          if ([self.recorder multiVideoCurrentPlayPercent] > 0.99) {
            [self.recorder multiVideoSeekToTime:CMTimeMake(0, 1) completeBlock:^(BOOL finished) {
              @strongify(self);
              [self.recorder multiVideoPlay];
            }];
          } else {
            [self.duetPlayerTimes addObject:@(CMTimeGetSeconds(self.recorder.multiVideoCurrentTime))];
            [self.recorder multiVideoPlay];
          }
           
           
        }
      }
        break;
      case IESCameraDidPauseVideoRecord:
         
        [self updateFragment];
        break;
      case IESCameraDidReachMaxTimeVideoRecord:
        [self pauseVideoRecord];
        [self updateFragment];
        break;
      case IESCameraDidChangeCameraDeviceType:
      {
        self.isDeviceChang = YES;
        if (self.recorder.currentCameraPosition == AVCaptureDevicePositionFront) {
          [self.recorder cameraSetZoomFactor:1];
          self.curZoomScal = 1;
        } else {
          NSArray *arr = [self.recorder virtualDeviceSwitchOverVideoZoomFactors];
          NSLog(@"----------%@",arr);
          if (arr.count > 0) {
            [self.recorder cameraSetZoomFactor:2];
            self.curZoomScal = 2;
          } else {
            [self.recorder cameraSetZoomFactor:1];
            self.curZoomScal = 1;
          }
        }
      }
        break;
      case IESCameraDidChangeCameraZoomFactor:
        break;
      default:
        break;
    }
  }];
```



* Duration change callback


```objectivec
[self.recorder setIESCameraDurationBlock:^(CGFloat duration, CGFloat totalDuration) {
    @strongify(self);
     
    NSLog(@"----------------duration:%0.2f-----totalDuration:%0.2f",duration,totalDuration);

    if (self.VECameraDurationBlock) {
      self.VECameraDurationBlock(totalDuration, totalDuration);
    }
  }];
```


<span id="6b21c271"></span>
## Modify camera parameters


* The camera supports different resolutions in front\-facing and rear\-facing modes. Therefore, after you flip the camera between the front\-facing and rear\-facing modes, make sure that the resolution is supported in the current mode. Otherwise, change the resolution to a supported value.


```objectivec
[self.recorder switchCameraSource];
```



* Flash

   * Capture


```objectivec
//  Flash.
@property (nonatomic, assign) IESCameraFlashMode cameraFlashMode;
```



* Video recording


```objectivec
// The flash switch (valid only when isTrochEnable is set to YES).
@property(nonatomic, assign) BOOL torchOn;
```



* Adjust the focal length.

   APIs


```objectivec
- (BOOL)cameraSetZoomFactor:(CGFloat)zoomFactor;

- (BOOL)cameraRampToZoomFactor:(CGFloat)zoomFactor withRate:(CGFloat)rate;

- (CGFloat)currentCameraZoomFactor;
```


Sample code

```objectivec
- (BOOL)cameraSetZoomFactor:(CGFloat)zoomFactor
{
  NSLog(@"---------minZoom:%0.2f---maxZoom:%0.2f----curZoom:%0.2f--%@",self.recorder.minAvailableVideoZoomFactor,self.recorder.maxAvailableVideoZoomFactor,self.recorder.videoZoomFactorUpscaleThreshold,self.recorder.virtualDeviceSwitchOverVideoZoomFactors);

  if ([self.recorder cameraSetZoomFactor:zoomFactor]) {
    self.curZoomScal = self.recorder.currentCameraZoomFactor;
    return YES;
  }
   
  return NO;
}

- (BOOL)cameraRampToZoomFactor:(CGFloat)zoomFactor withRate:(CGFloat)rate;
{
  NSLog(@"---------minZoom:%0.2f---maxZoom:%0.2f----curZoom:%0.2f",self.recorder.minAvailableVideoZoomFactor,self.recorder.maxAvailableVideoZoomFactor,self.recorder.exposureBias);
  if ([self.recorder cameraRampToZoomFactor:zoomFactor withRate:rate]) {
    if (zoomFactor > self.recorder.maxCameraZoomFactor) {
      zoomFactor = self.recorder.maxCameraZoomFactor;
    }
    self.curZoomScal = zoomFactor;
    return YES;
  }
   
  return NO;
}
```



* Focusing


```objectivec
/**
 * @brief The focus point.
 */
- (CGPoint)focusPoint;

/**
 * @brief Tap it to trigger focusing.
 * @param point  The point used for focusing.
 */
- (void)tapFocusAtPoint:(CGPoint)point;
```



* Exposure


```objectivec
/**
 * @brief The exposure point.
 */
- (CGPoint)exposurePoint;

/**
 * @brief Tap it to trigger exposure.
 * @param point The point used for exposure.
 */
- (void)tapExposureAtPoint:(CGPoint)point;
```



* Resolution and aspect ratio


```objectivec
/**
 * @brief Modify the output resolution for live streaming or cropping.
 */
- (void)resetOutputSize:(CGSize)outputSize;

/**
 Switch the camera preset.
 
 Do not block the main thread before the callback is complete. Otherwise, long lag may occur.

 @param preset   The camera preset.
 @param then      The main thread callback.
 */
- (void)resetCapturePreset:(nullable AVCaptureSessionPreset)preset then:(void (^_Nullable)(void))then;

/**
 Asynchronously set the output ratio, and automatically select the preset and output size based on the ratio.
 
 Do not block the main thread before the callback is complete. Otherwise, long lag may occur.
 
 @param ratio  The output ratio.
 @param then  The main thread callback.
 */
- (void)resetCaptureRatio:(IESMMCaptureRatio)ratio then:(void (^_Nullable)(void))then;

/**
 Asynchronously set the output ratio, define the preview and output resolution, and use the default preset.
 
 Do not block the main thread before the callback is complete. Otherwise, long lag may occur.

 @param ratio The image output ratio.
 @param size   The preview and output size (the width is calculated based on the ratio and the height).
 @param then  The main thread callback.
 */
- (void)resetCaptureRatio:(IESMMCaptureRatio)ratio
      preferredSize:(CGSize)size
           then:(void (^_Nullable)(void))then;

/**
 Asynchronously set the output ratio, define the preset, and use the default resolution.
 
 Do not block the main thread before the callback is complete. Otherwise, long lag may occur.
 
 @param ratio    The image output ratio.
 @param preset The camera preset.
 @param then    The main thread callback.
 */
- (void)resetCaptureRatio:(IESMMCaptureRatio)ratio
     preferredPreset:(nullable AVCaptureSessionPreset)preset
           then:(void (^_Nullable)(void))then;

/**
 Asynchronously set the output ratio, and define the preset, preview, and output resolution.
 
 Do not block the main thread before the callback is complete. Otherwise, long lag may occur.

 @param ratio      The image output ratio.
 @param preset   The camera preset. If the parameter is set to nil, the recommended preset will be used.
 @param previewHeight The height of the preview size (the width is calculated based on the ratio).
 @param outputHeight   The height of the output size (the width is calculated based on the ratio).
 @param then                    The main thread callback.
 */
- (void)resetCaptureRatio:(IESMMCaptureRatio)ratio
     preferredPreset:(nullable AVCaptureSessionPreset)preset
      previewHeight:(CGFloat)previewHeight
       outputHeight:(CGFloat)outputHeight
           then:(void (^_Nullable)(void))then;

- (void)resetCaptureRatio:(IESMMCaptureRatio)ratio
     preferredPreset:(nullable AVCaptureSessionPreset)preset
       previewSize:(CGSize)previewSize
        outputSize:(CGSize)outputSize
           then:(void (^_Nullable)(void))then;
```



* Bit rate


```objectivec
+ (int)s_p_exportBitRateWithResolution:(VEExportResolution)resolution fps:(VEExportFPS)fps{
  CGFloat baseBitRate = 0;
  switch (resolution) {
    case VEExportResolutionP540:
      baseBitRate = 4.5;
      break;
    case VEExportResolutionP720:
      baseBitRate = 10.f;
      break;
    case VEExportResolutionP1080:
      baseBitRate = 16.f;
      break;
    case VEExportResolutionP4K:
      baseBitRate = 45.f;
      break;
    default:
      baseBitRate = 10.f;
      break;
  }
  
  CGFloat biteRate = baseBitRate * 1024.0 * 1024.0;
  biteRate = ((fps - 30) / 30.0 * 0.4 + 1.0) * biteRate;
  return (int)biteRate;
}
```



* Exception and interruption handling


```objectivec
- (void)pausePreview
{
  if (self.recorder.status != IESMMCameraStatusIdle) {
    [self pauseVideoRecord];
  }

  if (self.isAudioPreviewing && (self.isAudioPreviewing.boolValue == YES)) {
    [self.recorder stopAudioCapture];
    self.isAudioPreviewing = @(NO);
  }
   
  if (self.isVideoPreviewing && (self.isVideoPreviewing.boolValue == YES)) {
    [self.recorder stopVideoCapture];
    self.isVideoPreviewing = @(NO);
  }
   
}
- (void)resumPreview
{
  if (self.isAudioPreviewing && (self.isAudioPreviewing.boolValue == NO)) {
    [self.recorder startAudioCapture];
    self.isAudioPreviewing = @(YES);
  }
   
  if (self.isVideoPreviewing && (self.isVideoPreviewing.boolValue == NO)) {
    [self.recorder startVideoCapture];
    self.isVideoPreviewing = @(YES);
  }
     
}
- (void)endPreview
{
  if (self.isAudioPreviewing && (self.isAudioPreviewing.boolValue == YES)) {
    [self.recorder stopAudioCapture];
    self.isAudioPreviewing = @(NO);
  }
   
  if (self.isVideoPreviewing && (self.isVideoPreviewing.boolValue == YES)) {
    [self.recorder stopVideoCapture];
    self.isVideoPreviewing = @(NO);
  }
  self.curPreview.hidden = YES;
}
```


<span id="e2ec65e4"></span>
## Capture


* Capture by using the system camera


```objectivec
/**
 * @brief Capture is a process of taking a photo for processing by using the camera. A shutter sound will be generated.
 * @param byUser   Indicates whether the capture is triggered by the user.
 * @param block      The callback after capture is completed.
 */

- (void)captureStillImageByUser:(BOOL)byUser
           completion:(void (^_Nullable)(UIImage *_Nullable processedImage, NSError *_Nullable error))block;
```



* Obtain the current raw frame as the captured photo.


```objectivec
/**
 * @brief Quick capture is a process of capturing the currently previewed frame.
 * @param byUser Indicates whether the capture is triggered by the user.
 * @param block    The callback after capture is completed.
 */

- (void)captureSourcePhotoAsImageByUser:(BOOL)byUser
           completionHandler:
               (void (^_Nullable)(UIImage *_Nullable processedImage, NSError *_Nullable error))block;
```



* Obtain the current effect frame as the captured photo.


```objectivec
/**
 * @brief Quick capture is a process of capturing the currently previewed frame.
 * @param block               The callback after capture is completed.
 * @param isProcessed    YES specifies to take a photo with the current effect. NO specifies to take a photo without the current effect (raw image of the camera).
 */
- (void)captureSourcePhotoAsImageByUser:(BOOL)byUser
           completionHandler:(void (^_Nullable)(UIImage *_Nullable processedImage,
                              NSError *_Nullable error))block
              afterProcess:(BOOL)isProcessed;
```



* Notes:

* The system camera will generate a shutter sound during photo capture by default. You cannot turn off the sound by using scripts. The system determines whether to play the shutter sound based on whether you have muted the shutter. The shutter sound cannot be turned off on mobile phones sold in some countries such as Japan.

* If a photo is not taken by the system camera, only the current frame will be captured. You need to control the flashlight by using scripts to apply the flash effect. Therefore, you can select this feature as needed. We recommend that you use the system camera.


<span id="3b41f4ea"></span>
## Video recording


* Normal recording

   API definition


```objectivec
Start video recording
- (void)startVideoRecord;
Pause video recording
/**
 * @brief Pause video recording.
 * @warning Do not call the startVideoRecord method before pause callback is completed.
 */
- (void)pauseVideoRecord;
/**
 * @brief Cancel video recording and delete all video clips.
 */
- (void)cancelVideoRecord;
```


Sample code

```objectivec
[self.recorder startVideoRecordWithRate:self.recordRate];
[self.recorder pauseVideoRecord];
```



* Multi\-scene recording

   API definition


```objectivec
Start video recording
- (void)startVideoRecord;
Pause video recording
/**
 * @brief Pause video recording.
 * @warning Do not call the startVideoRecord method before pause callback is completed.
 */
- (void)pauseVideoRecord;
/**
 * @brief Cancel video recording and delete all video clips.
 */
- (void)cancelVideoRecord;
/**
 * @brief Delete the last video clip.
 */
- (void)removeLastVideoFragment;

/**
 * @brief Delete all video clips.
 */
- (void)removeAllVideoFragments;
- (void)removeAllVideoFragments:(dispatch_block_t _Nullable)completion;
```


Sample code

```objectivec
[self.recorder startVideoRecordWithRate:self.recordRate];
[self.recorder pauseVideoRecord];
[self.recorder removeLastVideoFragment];
```



* Speed recording

   API definition


```objectivec
- (void)startVideoRecordWithRate:(CGFloat)rate;
```


Sample code

```objectivec
[self.recorder startVideoRecordWithRate:self.recordRate];
[self.recorder pauseVideoRecord];
```


Record a video of the specified duration (The duration of a single video clip is fixed, but you can control the total duration of the video.)

```objectivec
[self.recorder setMaxLimitTime:CMTimeMake(15, 1)];
[self.recorder setMaxLimitTime:CMTimeMake(60, 1)];
[self.recorder setMaxLimitTime:CMTimeMake(3600*24*365, 1)];
```


<span id="bd6f06bf"></span>
## Export


* Set the speed and modify the ratio and resolution.


```objectivec
[self.recorder pauseVideoRecord];
[self.recorder stopAudioCapture];
[self.recorder stopVideoCapture];

HTSVideoData *videoData = [videodata copy];
videoData.canvasSize = videodata.transParam.targetVideoSize;
videoData.transParam.allowFrameReordering = NO; //  We recommend that you set this parameter to NO. Otherwise, transcoding may take a long while.


IESMMTransProcessData *config = [[IESMMTransProcessData alloc] init];
  config.useNewMudule      = YES;
  config.enableMultiTrack   = YES;
  config.exportFps = 30; // The frame rate for video export.
  config.enableOptExportFps = YES;
  config.timeOutPeriod = 4;
  config.infoStickerForceAmazing = YES;
  config.disableEffectGroup = YES;
  config.enableKeyFrameFeature = YES;
  config.infostickerTextureRelease = YES;
  config.disableEffectProcess = NO;
  config.disableExtracFilter = YES;
  config.encodeUseFenceRender = YES;
  config.disableInfoSticker = NO;
  
  @weakify(self);
  [[VECompileTaskManagerSession sharedInstance] transWithVideoData:videoData
                               transConfig:config
                              videoProcess:nil
                              completeBlock:^(IESMMTranscodeRes *result) {
    NSLog(@"------%@",result.mergeUrl);
    @strongify(self);
    if (result.mergeUrl) {
      [self saveVideoToAlbum:result.mergeUrl.path];
      if (exportBlock) {
        exportBlock(nil,result.mergeUrl);
      }
       
    } else {
      NSLog(@"IESflow--%@",result.error.localizedDescription);
      [VECustomerHUD showMessage:@" Export failed." afterDele:3];
    }
  }];
   
  [[VECompileTaskManagerSession sharedInstance] setProgressBlock:^(CGFloat progress) {
    if (progressBlock) {
      progressBlock(progress);
    }
  }];

```



* Quick export


```objectivec
1. Import video data. #import <TTVideoEditor/IESMMAVExporter.h>
2. Create a video. 
- (IESMMAVExporter *)avExport
{
  if (!_avExport) {
    _avExport = [[IESMMAVExporter alloc] init];
    _avExport.presetName = AVAssetExportPresetPassthrough;
    _avExport.disableVideoCompostion = YES;
  }
   
  return _avExport;
}

3. Export the video.

For details about videodata, see the operations for the standard scene in the demo.
[self.avExport exportVideoData:videodata completeBlock:^(NSURL *outUrl, NSError *error) {
            if (outUrl) {
        [self saveVideoToAlbum:outUrl.path];
        if (exportBlock) {
          exportBlock(nil,outUrl);
        }
         
      } else {
        NSLog(@"IESflow--%@",error.localizedDescription);
        [VECustomerHUD showMessage:@"Export failed." afterDele:3];
      }
    }];
```


<span id="a09410d8"></span>
## Add visual effects


* Assets

* Composer

   * [User Guide: iOS VESDK Composer](https://bytedance.feishu.cn/docs/doccnYRkBNgSaVWq6XjUKyuM3xd)

* Add a filter, switch the filter, and modify the intensity


```objectivec
    [self.recorder applyEffect:evalue.sourcePath type:IESEffectFilter];
    IESIndensityParam param = {0};
    param.indensity = evalue.indesty;
    [self.recorder applyIndensity:param type:IESEffectFilter];
```



* Delete a filter


```objectivec
    [self.recorder applyEffect:nil type:IESEffectFilter];
    IESIndensityParam param = {0};
    param.indensity = 0;
    [self.recorder applyIndensity:param type:IESEffectFilter];
```



* Add a sticker

   * Add


```objectivec
[self.recorder applyEffect:evalue.sourcePath type:IESEffectGroup];
```



* Delete


```objectivec
[self.recorder applyEffect:nil type:IESEffectGroup];
```



* Add beauty effects


```objectivec
VEComposerInfo *composer = [[VEComposerInfo alloc] init];
  composer.node = evalue.composerPath;
  composer.tag = evalue.key;
[self.recorder appendComposerNodesWithTags:@[composer]];
```



* Add face shaping effects


```objectivec
VEComposerInfo *composer = [[VEComposerInfo alloc] init];
  composer.node = evalue.composerPath;
  composer.tag = evalue.key;
[self.recorder appendComposerNodesWithTags:@[composer]];
```


<span id="064ad49d"></span>
## Duet


* The Duet feature needs support from asset resource packages. For example, you can use specified resource packages to implement the left/right and up/down layouts on the screen.

   * Initialize Duet parameters


```objectivec
1. Initialize config parameters.
_config.captureRatio         = IESMMCaptureRatioAuto;
 _config.isProcessMultiInput     = YES;
 
2. Initialize the recorder and set resource packages.
 VEComposerInfo *one = [[VEComposerInfo alloc] init];
  one.node      = evalue.sourcePath;
  one.tag       = @"";
   
  if (self.lastDuetTags) {
    [self.recorder replaceComposerNodesWithNewTag:@[one] old:self.lastDuetTags];
  } else {
    [self.recorder appendComposerNodesWithTags:@[one]];
  }
 3. Set the videos for duet.
  [self.recorder setMultiVideoWithVideoURL:self.duetURL
                      rate:1
                  completeBlock:^(NSError *_Nullable error) {
      @strongify(self);
      AVPlayer *player = [self.recorder getMultiPlayer];
      self.periodicTimeObserver =
      [player addPeriodicTimeObserverForInterval:CMTimeMake(1, 2) queue:dispatch_get_main_queue() usingBlock:^(CMTime time) {
        @strongify(self);
        float seconds = time.value / (time.timescale * 1.f);
        if (seconds > 0.f) {
          [self.recorder multiVideoIsReady];
        }
      }];
      [self.recorder setMultiVideoAutoRepeat:NO];
      AVPlayerItem *item = player.currentItem;
      [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(didFinishPlayDuetVideo:) name:AVPlayerItemDidPlayToEndTimeNotification object:item];
    }];
    
    - (void)didFinishPlayDuetVideo:(NSNotification *)noti {
  if ([noti.name isEqualToString:AVPlayerItemDidPlayToEndTimeNotification]) {
    [self pauseVideoRecord];
    self.isDuetComplet = YES;
  }
}

4. Start duet.
[self.recorder startVideoRecordWithRate:1.f];
[self.recorder multiVideoPlay];
```



* Pause duet


```objectivec
[self.recorder pauseVideoRecord];
[self.recorder multiVideoPause];
```



* Delete a duet video clip


```objectivec
[self.recorder removeLastVideoFragment];
// Seek to the last pause time of duet.
[self.recorder multiVideoSeekToTime:CMTimeMake(lastPauseTime * 6000, 6000) completeBlock:^(BOOL finished) {  
    }];
```


<span id="4c83d919"></span>
# Video editing

<span id="722b39cd"></span>
## NLE overview

<span id="6e416070"></span>
### NLE

Distinguished from linear editing introduced in the 20th century, non\-linear editing (NLE) is a method for non\-linear video editing (NLVE) or non\-linear audio editing (NLAE) without destructing the raw data.

<span id="713a9a3f"></span>
### NLE model

NLEPlatform is a library mainly used to:


* Package APIs of the VE SDK.

* Provide the redo and undo capabilities.

* Standardize cross\-device draft protocols.

   The following shows its basic data model:


<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/abe1f0eeab9e4c01a4eab075ed68046a~tplv-em5hxbkur4-noop.image) </span>

A model (**NLEModel**) is a top\-level container and its sub\-nodes are tracks (**NLETrack**).

A track (**NLETrack**) can be considered as a layer (Z\-axis). Different tracks are located at different layers.

A track slot (**NLETrackSlot**) can be considered as a time segment. Except for key\-frame scenes, assets in the same time segment must have the same parameter settings.

An asset description segment (**NLESegment**) describes the secondary processing status of assets, for example, time\-based edit and filter intensity.

Asset metadata (**NLEResourceNode/NLEResourceAV**) describes the (local or remote) URIs of assets as well as preset thresholds.

As shown in figure:


1. A **NLEModel** can have multiple **NLETracks**, and a **NLETrack** can have multiple **NLETrackSlots**.

2. A **NLETrack** uses a **NLETrackSlot** to describe assets or present all its effects such as video effects (**NLEVideoEffect**).

3. Asset metadata is stored in **NLEResourceNode/NLEResourceAV.** 


An **NLEModel** is in a tree structure, which can be illustrated using the panels required for editing as follows:

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/608e39216fc94870b6fd955f7510e577~tplv-em5hxbkur4-noop.image) </span>

<span id="15c12cef"></span>
### NLEInterface

NLEInterface is an entrance to VE. You can call NLEInterface to create **NLEEditor** and **NLEModel**, a top\-level container. **NLEEditor** enables you to operate **NLEModel** to implement undo/redo and draft\-related operations.

When you modify data of **NLEModel**, you can call the **commit** method of **NLEEditor** to temporarily save the current operation.

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/a028152a0a004c6c8cbd5d7198b80861~tplv-em5hxbkur4-noop.image) </span>

<span id="304a6961"></span>
## Initialization

**API definition**

```objectivec
@protocol NLEEditorDelegate <NSObject>

- (void)nleEditorDidChange:(NLEEditor_OC *)editor;

@end

//  Provide the redo and undo capabilities and the capability of obtaining NLEModel.
@interface NLEEditor_OC : NSObject

//  The NLE model.
@property (nonatomic, strong) NLEModel_OC *model;

///  Calling the redo, undo, or done method will call back this delegate. Callback is performed after the redo or undo method is completed.
/// BranchListener functions differently. It initiates callback after the branch changes, and callback is performed before the redo or undo method is completed.
/// @param delegate id<NLEEditorDelegate>
- (void)addDelegate:(id<NLEEditorDelegate>)delegate;
```


```objectivec
@interface NLEInterface_OC : NSObject

///  The path of the draft. The system will generate a full path to all assets based on this path.
@property (nonatomic, strong) NSString *draftFolder;

///  If the NLE system cannot find the target resource file, it will call the DataSource method to obtain the file path. You can specify the
/// data source to define queries for some resources, for example, built-in resources.
@property (nonatomic, weak, nullable) id<NLEBundleDataSource> bundleDataSource;

///  Construct NLEEditor.
/// @param veEditor VEEditorSession         The VE operation class.
/// @param videoData HTSVideoData         The Empty data object for VE.
/// @param config VEEditorSessionConfig  Initializes the VE configuration. For more information, see the documentation of VE.
- (NLEEditor_OC*)CreateNLEEditorWithVeConfig:(VEEditorSession*)veEditor
                  videoData:(HTSVideoData *)videoData
                 withConfig:(VEEditorSessionConfig *)config;
                 
/**
 * Reset the view on which the player depends.
 */
- (void)resetPlayerWithViews:(nullable NSArray<UIView *> *)views;
```


```objectivec
@protocol NLEBundleDataSource <NSObject>

- (NSString *)resourcePathForNode:(NLEResourceNode_OC *)resourceNode;

@end
```


**Sample code**

```objectivec
 //  The external API class used to initialize NLE.
self.nle = [[NLEInterface_OC alloc] init];

//  Initialize NLEEditor_OC, and provide the redo and undo capabilities and the capability of obtaining NLEModel.
self.nleEditor = [self.nle CreateNLEEditorWithVeConfig:self.editorSession
                                             videoData:self.videoData
                                            withConfig:self.config];
//  Listen to changes of the redo and undo status.
[self.nleEditor addBranchListener:self];

//  Set an aspect ratio for video preview and view the specified canvas aspect ratio.
[self.nleEditor getModel].canvasRatio = self.canvasConfig.size.width / self.canvasConfig.size.height;
```



* Set a draft path for **NLEInterface_OC**.

   To restore a draft in the future, you can set a draft path. All resource paths specified for NLE can be relative paths. You need to copy the resources to the draft path.


```objectivec
self.nle.draftFolder = @"draft path";
```



* NLEInterface_OC

   **NLEInterface_OC** is an entrance to NLE. **NLEModel_OC**, **NLEEditor_OC**, and some APIs of the VE SDK are encapsulated in it.

* NLEModel_OC

   **NLEModel_OC** is a model class acting as an entrance to all model structure information. You can call this class to add or delete tracks and add or delete slots in a track. All subsequent effects are applied based on this model.


<span id="457fdba1"></span>
## Video\-related features

<span id="d6fb6c79"></span>
### Import pictures/videos

**Feature**

Imports assets selected for editing. The assets will be added to the main track and played in sequence. You can customize the playback duration for pictures.

**API definition**

**NLETrackSlot_OC** describes a slot on a UI track and is time\-related. Start time and end time apply to the entire playback track.

**NLESegmentVideo_OC** indicates a specific video clip in a slot and is time\-related. Start Time and End Time indicate the time for video cropping. For example, if a video lasts for 16s, you can set the video to play from the 3rd second for 4s and make it start from time 0 on the main track.

NLETrackSlot_OC:

startTime: 0s

endTime: 4s

NLESegmentVideo_OC:

startTime: 3s

endTime: 7s

```objectivec
@interface NLEResourceAV_OC : NLEResourceNode_OC
/// The length.
@property (nonatomic, assign) CMTime duration;
/// The width.
@property (nonatomic, assign) uint32_t width;
/// The height.
@property (nonatomic, assign) uint32_t height;
/// Specify whether to enable audio.
@property (nonatomic, assign) BOOL hasAudio;

// Deep clone.
- (NLEResourceAV_OC*)deepClone;

@end
```


```objectivec
@interface NLESegmentVideo_OC : NLESegmentAudio_OC

// Coordinates of four vertexes after video cropping.
@property (nonatomic, strong) NLEStyCrop_OC *crop;

///  Canvas parameters.
@property (nonatomic, strong) NLEStyCanvas_OC *canvasStyle;

/// Video or image resource.
@property (nonatomic, strong) NLEResourceAV_OC *videoFile;

///  Blending resource object. resourceFile indicates the absolute path of the resource file.
@property (nonatomic, strong) NLEResourceNode_OC *blendFile;

/// The opacity of a video, which ranges from 0 to 1.
@property (nonatomic, assign) CGFloat alpha;
```


```objectivec
@interface NLETrackSlot_OC : NLETimeSpaceNode_OC

/// The main video clip. The slot duration is calculated based on the duration of the main clip.
/// Audio: NLESegmentAudio.
/// Video: NLESegmentVideo.
/// Picture: NLESegmentImage.
/// Sticker: NLESegmentSticker.
/// Filter: NLESegmentFilter (added to the entire canvas).
/// Effect: NLESegmentEffect.
/// Time effect: NLESegmentTimeEffect.
@property (nonatomic, strong) NLESegment_OC* segment;

/// The PIN feature enables you to attach stickers to hands and faces. The double-ended PIN feature is supported by VE and effects. A PIN algorithm file must be transferred.
@property (nonatomic, strong, nullable) NLEResourceNode_OC* pinAlgorithmFile;

///  The transition animation. You can add only one transition animation and must put it at the end.
@property (nonatomic, strong, nullable) NLESegmentTransition_OC* endTransition;
```


**Sample code**

```objectivec
//  Construct an NLE resource model.
NLEResourceAV_OC *videoResource = [[NLEResourceAV_OC alloc] init];
videoResource.resourceType = NLEResourceTypeVideo;
//  To restore drafts in the future, you can specify a relative path here.
videoResource.resourceFile = resourcePath;
videoResource.hasAudio = audioTracks.count > 0;
   
//  You can call AVAsset to obtain the following data.
self.duration = videoDuration;
self.width = videoSize.width;
self.height = videoSize.height;
       
CMTime duration = videoResource.duration;

//  NLESegmentVideo_OC indicates an object in a slot. You can set the time for video cropping. For example:      
NLESegmentVideo_OC *videoSegment = [[NLESegmentVideo_OC alloc] init];
videoSegment.videoFile = videoResource;
videoSegment.timeClipStart = CMTimeMake(0 * USEC_PER_SEC, USEC_PER_SEC);
videoSegment.timeClipEnd = duration;
[videoSegment setvolume:1];
       
NLETrackSlot_OC *trackSlot = [[NLETrackSlot_OC alloc] init];
[trackSlot setSegmentVideo:videoSegment];
trackSlot.startTime = CMTimeMake(startTime * USEC_PER_SEC, USEC_PER_SEC);
[trackSlot setLayer:0];


NLETrack_OC *mainTrack = [[NLETrack_OC alloc] init];
//  The layer that corresponds to the drawing layer for VE.
mainTrack.layer = 0;
//   Indicates that the track is the main track.
[mainTrack setMainTrack:YES];

//  Add the main track.
[self.nle.editor.model addTrack:mainTrack];

//  Commit. The NLE system will run the diff algorithm and apply the effect by using the VE SDK.
[self.nle.editor commit];


//  To allow undo on the commit, you can call the done method to save it. Next time you want to undo the commit, you can directly
// call the editor to undo it.
[self.nle.editor done];
```


<span id="5d48c43a"></span>
### Playback

**Feature**

Plays a video. Before you play a video, create an empty UIView, add it to UIViewController, and then pass the view to NLEInterface_OC.

**API definition**

```objectivec
@interface NLEInterface_OC : NSObject

/**
 * @brief Start to play a video.
 */
- (void)start;

/**
 * @brief Pause a video.
 */
- (void)pause;
```


**Sample code**

```objectivec
[self.nle resetPlayerWithViews:@[view]];

//  A commit is required if the model is modified.
[self.nle.editor commit];

//  Start playing.
[self.nle start];
```


<span id="14a0c8b4"></span>
### Add a video clip to the main track

**Feature**

Adds a video clip to the main track. An editor has only one main track. Before you add a video clip to the main track, call **NLETrack_OC** to find it, which is identified by the **isMainTrack** parameter. Then, construct a slot containing the video resource. For details about how to construct a video slot, see section "Import pictures/videos".

**API definition**

```objectivec
@interface NLETrack_OC : NLETimeSpaceNode_OC

///  Indicates whether the track is the main track. Each video has only one main track.
@property (nonatomic, assign, getter=isMainTrack) BOOL mainTrack;

///  Add a video clip to the end.
/// @param objects NLETrackSlot_OC *
- (void)addSlot:(NLETrackSlot_OC *)objects;

///  Add a video clip to the head of the track and automatically adjust the slot time.
/// @param child NLETrackSlot_OC *
- (void)addSlotAtStart:(NLETrackSlot_OC*)child;
```


**Sample code**

```objectivec
NLETrack_OC *mainTrack = [self nle_getMainVideoTrack];
if (!mainTrack) {
    mainTrack = [[NLETrack_OC alloc] init];
    mainTrack.layer = 0;
    [mainTrack setMainTrack:YES];
    [self addTrack:mainTrack];
}
[mainTrack addSlot:slot];
```


<span id="6b12cb32"></span>
### Add overlays

**Feature**

Adds overlays to independent tracks, instead of the main track, so that different video assets can be played in multiple areas on the preview page.

**API definition**

**NLESegmentVideo_OC** describes an overlay video clip.

```objectivec
@interface NLESegmentVideo_OC : NLESegmentAudio_OC

// Coordinates of four vertexes after video cropping.
@property (nonatomic, strong) NLEStyCrop_OC *crop;

///  Canvas parameters.
@property (nonatomic, strong) NLEStyCanvas_OC *canvasStyle;

///  Video or picture resource.
@property (nonatomic, strong) NLEResourceAV_OC *videoFile;

///  Blending resource object. resourceFile indicates the absolute path of the resource file.
@property (nonatomic, strong, nullable) NLEResourceNode_OC *blendFile;

/// The opacity of a video, which ranges from 0 to 1.
@property (nonatomic, assign) CGFloat alpha;
```


**Sample code**

```objectivec
Prolog
//  Information about the asset resource, such as the type, path, time, width, and height.
NLEResourceAV_OC *videoResource = [[NLEResourceAV_OC alloc] init];
[videoResource nle_setupForVideo:res.videoAsset];
videoResource.resourceType = NLEResourceTypeVideo;
videoResource.resourceFile = res.videoAsset.URL.absoluteString.lastPathComponent;
videoResource.duration = duration;

//  Asset clip: Set the sound volume, start time, and end time of the asset clip. The settings are specific to the asset clip.           NLESegmentVideo_OC *videoSegment = [[NLESegmentVideo_OC alloc] init];
videoSegment.videoFile = videoResource;
videoSegment.timeClipStart = CMTimeMake(0 * USEC_PER_SEC, USEC_PER_SEC);
videoSegment.timeClipEnd = duration;
[videoSegment setvolume:1];
            
NLETrackSlot_OC *trackSlot = [[NLETrackSlot_OC alloc] init];
[trackSlot setSegmentVideo:videoSegment];
[trackSlot setScale:0.7];
trackSlot.startTime = CMTimeMake(startTime * USEC_PER_SEC, USEC_PER_SEC);
[trackSlot setLayer:layer];

//  Create an overlay track.
NLETrack_OC *track = [[NLETrack_OC alloc] init];
//  Set the layer of an overlay.
[track setLayer:layer];
track.extraTrackType = NLETrackVIDEO;
[track addSlot:slot];
[[self.vcContext.mediaContext.editor getModel] addTrack:track];

[self.vcContext commitNLE:YES];
```


<span id="0b624ab5"></span>
### Delete videos

**Feature**

Deletes a video by deleting its slot. For an overlay, if its track is empty after the slot is deleted, the track can also be deleted.

**API definition**

```objectivec
@interface NLETrack_OC : NLETimeSpaceNode_OC

///  Remove a slot.
/// @param slot NLETrackSlot_OC *
- (void)removeSlot:(NLETrackSlot_OC *)slot;
```


**Sample code**

```objectivec
track removeSlot:slot];
```


<span id="3c8f3718"></span>
### Speed

**Feature**

Speeds up or down a video or audio clip at a fixed rate.

**API definition**

```objectivec
@interface NLESegmentAudio_OC : NLESegment_OC

///  The DC component of the speed. This variable is also applicable to the curve speed. The end time is calculated based on this variable. When a video is reserved at 1x speed, the speed is equal to –1.0f.
/// Speed is a time-related concept similar to the combination of scale and mirror in space.
- (CGFloat)speed;

- (void)setSpeed:(CGFloat)speed;
```


**Sample code**

```objectivec
[videoSegment setSpeed:speed];
```


**Note**

The speed cannot be set to 0.

<span id="700e7034"></span>
### Rotate, mirror, scale, and translate a video

**Feature**

Because there is a canvas, the video can be rotated, scaled and panned whether it is the main track or the secondary track.

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/f748eb6c66bc4659b8a2939bcf313c28~tplv-em5hxbkur4-noop.image) </span>

The black part is the canvas, the color and background temporarily do not support modification in the editor.

**API definition**

```objectivec
@interface NLETimeSpaceNode_OC : NLENode_OC
/// Counterclockwise rotation based on positive Z-axis, value range 0~359; (positive value: counterclockwise rotation, negative value: clockwise rotation)
- (float)rotation;

/// Counterclockwise rotation based on positive Z-axis, range 0~359; (positive value: counterclockwise rotation, negative value: clockwise rotation)
/// @param rotation float
- (void)setRotation:(float)rotation;

/// Coordinate origin: center of the screen
/// X-axis positive direction: user view: screen left -> screen right
/// Y-axis positive direction: user view: screen bottom -> screen top
/// Z-axis positive direction: user view: screen inside -> screen outside
/// Displacement -1.0f~1.0f
- (float)transformX;

- (void)setTransformX:(float)transformX;

/// Displacement -1.0f~1.0f
- (float)transformY;

- (void)setTransformY:(float)transformY;

/// Displacement (Z-axis) 0~1000; rendering level, the larger the value the more it is displayed on top; value range: 0~1000.
- (int32_t)transformZ;

- (void)setTransformZ:(int32_t)transformZ;

//// For video/picture: 1.0f is the scale of the video/picture when center inside in the canvas
//// For text/paste: 1.0f is a base size for the first rendering of text/paste to VE
/// Instead of relying too much on the scale value, you should focus on its difference
- (float)scale;

- (void)setScale:(float)scale;

@end;
```


**Sample code**

```objectivec
slot.rotation = 180;
[self.vcContext commitNLE:YES];
```


<span id="d675afa8"></span>
### Crop a picture

**Feature**

Rotates a video or picture around its center, zooms in an area on the video or picture, and then crops a picture on the area.

**API definition**

```objectivec
@interface NLEStyCrop_OC : NLENode_OC
///  Normalized coordinates of four vertexes after cropping. The upper left vertex is the origin.
@property (nonatomic, assign) CGFloat lowerLeftX;
@property (nonatomic, assign) CGFloat lowerLeftY;
@property (nonatomic, assign) CGFloat lowerRightX;
@property (nonatomic, assign) CGFloat lowerRightY;
@property (nonatomic, assign) CGFloat upperLeftX;
@property (nonatomic, assign) CGFloat upperLeftY;
@property (nonatomic, assign) CGFloat upperRightX;
@property (nonatomic, assign) CGFloat upperRightY;
```


**Sample code**

```objectivec
//// Create a segment.
NLESegmentVideo_OC *segment = [[NLESegmentVideo_OC alloc] init];

//Add resources to the segment, that is, import pictures or videos to it.
...

//If the cropping data class of the segment is nil, initialize the segment.
if (!segment.crop) {
    segment.crop = [[NLEStyCrop_OC alloc] init];
}
// Save coordinates of four vertexes after video rotation and cropping to the NLE system.
segment.crop.upperLeftX = upperLeftX;
segment.crop.upperLeftY = upperLeftY;
segment.crop.upperRightX = upperRightX;
segment.crop. upperRightY = upperRightY;
segment.crop.lowerLeftX = lowerLeftX;
segment.crop.lowerLeftY = lowerLeftY;
segment.crop.lowerRightX = lowerRightX;
segment.crop. lowerRightY = lowerRightY;

NLETrackSlot_OC *slot = [[NLETrackSlot_OC alloc] init];
[slot setSegmentVideo:segment];

NLETrack_OC *track = [[NLETrack_OC alloc] init];
[track addSlot:slot];

NLEModel_OC *model = self.nle.editor.model;
[model addTrack:track];

// Commit the modification.
[self.nle.editor commit];
// Save the modification.
[self.nle.editor done];
```


<span id="bb82b525"></span>
### Blend video clips

**Feature**

Blends an overlay video clip with the background video clip so that their attributes such as color and brightness match well.

**API definition**

```objectivec
@interface NLESegmentVideo_OC : NLESegmentAudio_OC

///  Blending resource object. resourceFile indicates the absolute path of the resource file.
@property (nonatomic, strong) NLEResourceNode_OC *blendFile;
```


**Sample code**

```objectivec
// Create a segment.
NLESegmentVideo_OC *segment = [[NLESegmentVideo_OC alloc] init];

//Add resources to the segment, that is, import pictures or videos to it.
...

// If blendFile of the segment is nil, initialize the segment.
if (!segment.blendFile) {
    segment.blendFile = [[NLEResourceNode_OC alloc] init];
}
// resourceType of the blending effect is NLEResourceTypeEffect by default.
segment.blendFile.resourceType = NLEResourceTypeEffect;
// The name of the blending effect resource to be applied.
segment.blendFile.resourceName = name;
// The absolute path of the blending effect resource to be applied.
segment.blendFile.resourceFile = sourcePath;
// The opacity of the blending effect, which is a floating-point value ranging from 0 to 1.
segment.alpha = value;

NLETrackSlot_OC *slot = [[NLETrackSlot_OC alloc] init];
[slot setSegmentVideo:segment];

NLETrack_OC *track = [[NLETrack_OC alloc] init];
[track addSlot:slot];

NLEModel_OC *model = self.nle.editor.model;
[model addTrack:track];

// Commit the modification for it to take effect.
[self.nle.editor commit];
// Save the modification.
[self.nle.editor done];
```


<span id="e753aa85"></span>
### Reverse a video

**Feature**

Reverses a video to generate a reversed video file, which will be transferred to the NLE system. This is equivalent to importing a video, except that the source video is reversed.

**API definition**

```objectivec
@interface IESAVAssetReverse : NSObject
- (instancetype)initWithAVAsset:(AVURLAsset *)asset;

- (void)reverseAsset:(ReverseCompleteBlock)completeBlock progressBlock:(void (^)(CGFloat progress))progressBlock;

- (void)cancle;
```


**Sample code**

```objectivec
//  Reverse a video by calling the API of VE.
self.reverseSession = [[IESAVAssetReverse alloc] initWithAVAsset:asset];
[self.reverseSession reverseAsset:^(NSURL * _Nullable ouputUrl, NSError * _Nullable error) {
    if (!error) {
        AVURLAsset *asset1 = [AVURLAsset URLAssetWithURL:ouputUrl options:nil];
        if (complete) {
            complete(asset1);
        }
    }
} progressBlock:process];
```


```objectivec
NLESegmentVideo_OC *segmentVideo = (NLESegmentVideo_OC *)slot.segment;
   
CMTimeRange sourceTimeRange = slot.nle_sourceTimeRange;
NLEResourceAV_OC *videoResource = [[NLEResourceAV_OC alloc] init];
///  Set the basic information of an asset, such as the duration, width, and height.
[videoResource nle_setupForVideo:reversedAsset];
segmentVideo.videoFile = videoResource;
   
BOOL needUpdateTimeRange = segmentVideo.rewind != isReallyReverse;
if (needUpdateTimeRange) {
    // ----s-------e-
    // -s-------e----
    CMTime sourceStart = CMTimeSubtract(segmentVideo.nle_resourceDuration, CMTimeRangeGetEnd(sourceTimeRange));
    CMTime sourceEnd = CMTimeSubtract(segmentVideo.nle_resourceDuration, sourceTimeRange.start);
    segmentVideo.timeClipStart = sourceStart;
    segmentVideo.timeClipEnd = sourceEnd;
}
//  Indicates that the segment is reversed.
segmentVideo.rewind = isReallyReverse;
```


<span id="e1062a87"></span>
### Set the sound volume

**API definition**

```objectivec
@interface NLESegmentAudio_OC : NLESegment_OC

///  Original sound volume = 1.0f, sound volume after audio is muted = 0.0f.
- (float)volume;
```


**Sample code**

```objectivec
NLESegmentAudio_OC *segmentVideo = (NLESegmentAudio_OC *)slot.segment;
segmentVideo.volume = volume;
```


<span id="bda0c727"></span>
### Add a mask to a video

**Feature**

Adds a mask to a video. You can add only one mask to a video on each track and add different masks based on your assets. For example, add a linear, mirror\-like, rectangular, circular, heart\-shaped, or star\-shaped mask.

**API definition**


* Add a sticker


```objectivec
- (void)addOneMaskWithEffectValue:(VEVCMaskConfigModel *)eValue needCommit:(BOOL)commit;
```



* Modify a mask


```objectivec
- (void)updateOneMaskWithEffectValue:(VEVCMaskConfigModel *)eValue needCommit:(BOOL)commit onlyUI:(BOOL)isOnlyUI;
```



* Delete a sticker


```objectivec
- (void)deletCurMaskEffectValueNeedCommit:(BOOL)commit;
```


**Parameters:** 

**VEVCMaskConfigModel** packages the parameters required for a mask.

```objectivec
//  The mask type.
@property (nonatomic, assign) VEMaskEditType type;
// The asset model of the current file, which uses the local source path.
@property (nonatomic, strong) VEEffectValue *curValue;
// The normalized width of the mask.
@property (nonatomic, assign) CGFloat width;
//  The normalized height of the mask.
@property (nonatomic, assign) CGFloat height;
// The maskrotation angle.
@property (nonatomic, assign) CGFloat rotation;
//  The original aspect ratio of the mask SVG.
@property (nonatomic, assign) CGFloat aspectRatio;
//  The normalized radius of each rounded corner.
@property (nonatomic, assign) CGFloat roundCorner;
// The normalized radius of a feather mask.
@property (nonatomic, assign) CGFloat feather;
// The normalized center of the mask.
@property (nonatomic, assign) CGPoint center;
//  The path of the SVG.
@property (nonatomic, copy) NSString *svgFilePath;
// The border size of the video to which the mask is added.
@property (nonatomic, assign) CGSize borderSize;
// Set whether to invert the mask.
@property (nonatomic, assign) BOOL invert;

- (instancetype)initWithBorderSize:(CGSize)borderSize;
```


**Sample code**


* Initialize the model


```objectivec
  self.vcConfigModel = [[VEVCMaskConfigModel alloc] initWithBorderSize:vc.videoView.preview.canvasBorderView.size];
  VEEffectValue *maskValue = self.maskArr[indexPath.row];
  self.vcConfigModel.curValue = maskValue;
  self.vcConfigModel.type = indexPath.row;
  self.vcConfigModel.center = CGPointMake((maskDrawView.config.data.center.x - self.vcConfigModel.borderSize.width * 0.5)/(self.vcConfigModel.borderSize.width * 0.5),-(maskDrawView.config.data.center.y - self.vcConfigModel.borderSize.height * 0.5)/(self.vcConfigModel.borderSize.height * 0.5));
  self.vcConfigModel.width = maskDrawView.config.data.width/self.vcConfigModel.borderSize.width;
  self.vcConfigModel.height = maskDrawView.config.data.height/self.vcConfigModel.borderSize.height;
  CGSize size = combinedPath.bounds.size;
  self.vcConfigModel.aspectRatio = size.width / size.height;
  self.vcConfigModel.roundCorner = maskDrawView.config.data.roundCorner / maskDrawView.config.ui.roundCornerMaxSpace;
  self.vcConfigModel.feather = self.slider.value * 0.01;
  self.vcConfigModel.invert = !self.vcConfigModel.invert;

```



* Add a mask


```objectivec
    [self.vcContext addOneMaskWithEffectValue:self.vcConfigModel needCommit:YES];
    NLETrackSlot_OC* selectSlot = [self curSelectSlot];
  NLEMask_OC *findMask = [[self curSelectSlot] getMask].firstObject;
  if (!findMask) {   
    NLEResourceNode_OC *maskResource = [[NLEResourceNode_OC alloc] init];
    maskResource.resourceId = @(eValue.type).stringValue;
    maskResource.resourceFile = eValue.curValue.sourcePath;
    maskResource.resourceType = NLEResourceTypeMask;
    maskResource.resourceName = eValue.curValue.name;
     
    NLESegmentMask_OC *maskSegment = [[NLESegmentMask_OC alloc] init];
    [maskSegment setEffectSDKMask:maskResource];
    [maskSegment setAspectRatio:eValue.aspectRatio];
    [maskSegment setWidth:eValue.width];
    [maskSegment setHeight:eValue.height];
    [maskSegment setCenterX:eValue.center.x];
    [maskSegment setCenterY:eValue.center.y];
    [maskSegment setRotaion:eValue.rotation];
    [maskSegment setInvert:eValue.invert];
    [maskSegment setFeather:eValue.feather];
    [maskSegment setMaskType:eValue.curValue.mask];
     
    NLEMask_OC *mask = [NLEMask_OC new];
    [mask setSegmentMask:maskSegment];
     
    [selectSlot addMask:mask];
     

    [self.vcContext commitNLE:YES];
    }
```



* Modify a mask


```objectivec
    [self.vcContext deletCurMaskEffectValueNeedCommit:YES];
    NLETrackSlot_OC* selectSlot = [self curSelectSlot];
     
    if (!selectSlot) return;
    NLEMask_OC *findMask = [[self curSelectSlot] getMask].firstObject;
    if (!findMask) {
      return;
    }
     
    NLESegmentMask_OC *maskSegment = findMask.segmentMask;
    [maskSegment setAspectRatio:eValue.aspectRatio];
    [maskSegment setWidth:eValue.width];
    [maskSegment setHeight:eValue.height];
    [maskSegment setCenterX:eValue.center.x];
    [maskSegment setCenterY:eValue.center.y];
    [maskSegment setRotaion:eValue.rotation];
    [maskSegment setInvert:eValue.invert];
    [maskSegment setFeather:eValue.feather];
    [maskSegment setRoundCorner:eValue.roundCorner];
    [maskSegment setMaskType:eValue.curValue.mask];
    maskSegment.effectSDKMask.resourceName = eValue.curValue.name;
     
    [self.vcContext commitNLE:commit];
```



* Delete a mask


```objectivec
[self.vcContext updateOneMaskWithEffectValue:self.vcConfigModel needCommit:YES onlyUI:YES];
if (!selectSlot) return;
  NSMutableArray<NLEMask_OC*>* masks = [selectSlot getMask];
  for (NLEMask_OC *mask in masks) {
    [selectSlot removeMask:mask];
  }
  
  [self.vcContext commitNLE:commit];
```


```objectivec
- (NLETrackSlot_OC *)curSelectSlot
{
  NLETrackSlot_OC *slot = nil;
  if (self.vcContext.mediaContext.selectBlendVideoSegment) {
    slot = self.vcContext.mediaContext.selectBlendVideoSegment;
  } else if (self.vcContext.mediaContext.selectMainVideoSegment) {
    slot = self.vcContext.mediaContext.selectMainVideoSegment;
  }
   
  return slot;
}
```


<span id="601079ea"></span>
### Add an In or Out animation

**Feature**

Adds an In, Out, or Combo animation to a video on each main track.

**API definition**

```objectivec
@interface NLEVideoAnimation_OC : NLETimeSpaceNode_OC

///  The video animation asset.
@property (nonatomic, strong) NLESegmentVideoAnimation_OC *videoAnimation;
```


```objectivec
///  The video or animation clip.
@interface NLESegmentVideoAnimation_OC : NLESegment_OC

///  The animation resource.
@property (nonatomic, strong) NLEResourceNode_OC *effectSDKVideoAnimation;

///  The animation duration.
@property (nonatomic, assign) CMTime animationDuration;

@end
```


```objectivec
@interface NLETrackSlot_OC : NLETimeSpaceNode_OC
///  The video animation.
- (NSMutableArray<NLEVideoAnimation_OC*>*)getVideoAnims;

- (void)addVideoAnim:(NLEVideoAnimation_OC *)videoAnim;

- (void)clearVideoAnim;
```


**Sample code**

```objectivec
CMTime cmDuration = CMTimeMake(duration * USEC_PER_SEC, USEC_PER_SEC);

NLEResourceNode_OC *resource = [[NLEResourceNode_OC alloc] init];
resource.resourceFile = inAnimation.sourcePath;
resource.duration = cmDuration;
resource.resourceType = NLEResourceTypeAnimationVideo;
   
NLESegmentVideoAnimation_OC *segmentVideoAnimation = [[NLESegmentVideoAnimation_OC alloc] init];
segmentVideoAnimation.animationDuration = cmDuration;
segmentVideoAnimation.effectSDKVideoAnimation = resource;

NLEVideoAnimation_OC *animation = [[NLEVideoAnimation_OC alloc] init];
animation.videoAnimation = segmentVideoAnimation;
[selectSlot clearVideoAnim];
[selectSlot addVideoAnim:animation];
animation.nle_animationType = animationType;
```


<span id="d7331ab8"></span>
### Add a transition animation

**API definition**

```objectivec
Adds a transition animation between two adjacent slots on a video track.
API definition

Objective-C
/// The transition animation.
@interface NLESegmentTransition_OC : NLESegment_OC

///  Set whether to overlap video clips in a transition animation. If yes, the start time of all video clips following the current video clip will be shifted forward. If no, the timeline is not affected.
@property (nonatomic, assign) BOOL overlap;

///  The total duration of a transition animation.
@property (nonatomic, assign) CMTime transitionDuration;

///  The asset resource of a transition animation.
@property (nonatomic, strong) NLEResourceNode_OC* effectSDKTransition;
```


**Sample code**

```objectivec
NLEResourceNode_OC *transitionResourceNode = [[NLEResourceNode_OC alloc] init];
transitionResourceNode.resourceFile = transition.resourcePath;
transitionResourceNode.resourceType = NLEResourceTypeTransition;
transitionResourceNode.duration = CMTimeMake(transition.duration * USEC_PER_SEC, USEC_PER_SEC);
   
NLESegmentTransition_OC *nleTransition = [[NLESegmentTransition_OC alloc] init];
[nleTransition setOverlap:transition.isOverlap];
[nleTransition setTransitionDuration:CMTimeMake(transition.duration * USEC_PER_SEC, USEC_PER_SEC)];
[nleTransition setEffectSDKTransition:transitionResourceNode];

slot.endTransition = transition;
```


<span id="6016eb91"></span>
### Freeze frame

**Feature**

Select the main track, click freeze frame, draw a frame at the current play time point of the track material, and generate a slot with a length of 3s. After inserting it into the cursor, the original material is split into three parts.

**API Definition**

New method\- \* *(void)videoFreezeForSlot:(NLETrackSlot_OC )slot isMain* :  **(BOOL)main**

```objectivec
@protocol DVECoreVideoProtocol <DVECoreProtocol>

//Copy
// @param slot Slot to be frame-frozen 
//@param main Whether the current track is the main track
- (void)videoFreezeForSlot:(NLETrackSlot_OC *)slot isMain:(BOOL)main;
```


```objectivec
//Copy
// @param slot Slot to be frame-frozen 
//@param main Whether the current track is the main track
- (void)videoFreezeForSlot:(NLETrackSlot_OC *)slot 
                    isMain:(BOOL)main 
{
  if (!slot) {
[DVECustomerHUD showMessage: @"Please select the track to process"];
    return;
  }
   
//The time of the slot corresponding to the timeline, note that the main rail and the secondary rail are not the same
  NLESegmentVideo_OC *segment = (NLESegmentVideo_OC *)slot.segment;
//Pause before freezing
  [self.vcContext.playerService pause];
   
  CMTime currentTime = CMTimeAdd(CMTimeSubtract(self.vcContext.mediaContext.currentTime, slot.startTime), segment.timeClipStart);
   
  CGFloat start = CMTimeGetSeconds(slot.startTime);
  CGFloat end = CMTimeGetSeconds(slot.endTime);
  CGFloat current = CMTimeGetSeconds(self.vcContext.mediaContext.currentTime);
   
  AVAsset *asset = [self.vcContext getAssetWithSlot:slot];
  NSString *slotId = self.vcContext.mediaContext.selectMainVideoSegment.nle_nodeId;
  if (!main) {
    slotId = slot.nle_nodeId;
  }
   
//If the timeline is in the middle of the slot, split it first
  if (fabs(start - current) >= 0.1 && fabs(end - current) >= 0.1) {
    AVURLAsset *copyAsset = [AVURLAsset assetWithURL:[(AVURLAsset *)asset URL]];
    [self.vcContext.mediaContext splitVideoSlot:slotId
                     splitTime:self.vcContext.mediaContext.currentTime
                       asset:copyAsset
                       commit:NO];
  }
  
//Use AVAssetImageGenerator to extract frames
  AVAssetImageGenerator *generator = [[AVAssetImageGenerator alloc] initWithAsset:asset];
//Limit frame extraction time accuracy
  generator.requestedTimeToleranceAfter = kCMTimeZero;
  generator.requestedTimeToleranceBefore = kCMTimeZero;
//Disable automatic rotation of extracted frames
  generator.appliesPreferredTrackTransform = YES;

  dispatch_group_t group = dispatch_group_create();
  dispatch_group_enter(group);
//Extract the frame where the slot is on the current timeline
  __block UIImage *frameImage = nil;
//Limit the range of frame extraction time points to [0, asset.duration]
  currentTime = CMTimeMinimum(CMTimeMaximum(currentTime, kCMTimeZero), asset.duration);
   
  [generator generateCGImagesAsynchronouslyForTimes:@[[NSValue valueWithCMTime:currentTime]]
                  completionHandler:^(CMTime requestedTime,
                            CGImageRef _Nullable image,
                            CMTime actualTime,
                            AVAssetImageGeneratorResult result,
                            NSError * _Nullable error) {
    if (result == AVAssetImageGeneratorSucceeded && image) {
      frameImage = [UIImage imageWithCGImage:image];
    }
    dispatch_group_leave(group);
  }];
   
  dispatch_group_notify(group, dispatch_get_main_queue(), ^{
//Generate the path and write it to the file
    NSString *filePath = [self.draftService.currentDraftPath stringByAppendingPathComponent:[NSString VEUUIDString]];
    [UIImageJPEGRepresentation(frameImage, 1) writeToFile:filePath atomically:YES];
     
    CMTime duration = CMTimeMakeWithSeconds(3, USEC_PER_SEC);
    
//NLE data manipulation
    NLEResourceAV_OC *videoResource = [[NLEResourceAV_OC alloc] init];
    videoResource.resourceType = NLEResourceTypeImage;
    videoResource.width = frameImage.size.width;
    videoResource.height = frameImage.size.height;
    videoResource.resourceFile = filePath.lastPathComponent;
    videoResource.duration = [DVEVideoEditor kDefaultPhotoResourceDuration];

    NLESegmentVideo_OC *videoSegment = [[NLESegmentVideo_OC alloc] init];
    videoSegment.videoFile = videoResource;
    videoSegment.timeClipStart = CMTimeMake(0 * USEC_PER_SEC, USEC_PER_SEC);
    videoSegment.timeClipEnd = duration;

    NLETrackSlot_OC *trackSlot = [[NLETrackSlot_OC alloc] init];
    [trackSlot setSegmentVideo:videoSegment];
    [trackSlot setScale:main ? 1.0 : 0.7];
    [trackSlot setLayer:slot.layer];
    trackSlot.startTime = self.vcContext.mediaContext.currentTime;
     
    NLEModel_OC *model = self.vcContext.nleModel;
    NLETrack_OC *track = [model trackContainSlotId:slotId];
    
//Synchronize data changes to the track area
    [track nle_insertSlot:slot atTime:splitTime];
    [track nle_rescheduleTrackForTransitionChanged];

    NSMutableArray *slotIds = [[NSMutableArray alloc] init];
    for (NLETrackSlot_OC *slot in track.slots) {
      [slotIds addObject:slot.nle_nodeId];
    }
   
    self.vcContext.mediaContext.changedOrderSlots = [slotIds copy];
    
//Submit a commit
    [self.actionService commitNLE:YES];
    
//Set the currently selected slot
    if ([track isMainTrack]) {
      self.vcContext.mediaContext.selectMainVideoSegment = trackSlot;
    } else {
      self.vcContext.mediaContext.selectBlendVideoSegment = trackSlot;
    }
  });
```


<span id="fb207fd7"></span>
### Replace

**Feature**

Select the main track and click "Replace". The album page will appear so that the user can replace the original main track material with local materials. The replacement rules are as follows:


* Image \-\> image: No time limit

* Image \-\> Video: The video length is longer than the length of the currently selected image. (The image length is not necessarily 3s, but any length set by the user.)

* Video \-\> Image: No time limit. The image has the same duration as the video.

* Video \-\> Video: The length is longer than the original video.

   To put it simply, the replacement is unlimited for images. For videos, the new material needs to be longer than the slot of the old material, or the material will be greyed out and become unselectable.


**API definition**

New method \-  **(void)replaceResourceForSlot:albumResource**:

```objectivec
@protocol DVECoreImportServiceProtocol <DVECoreProtocol>

//Replace
//@param slot material slot to be replaced
@param albumResource New Material Resource Model
- (void)replaceResourceForSlot:(NLETrackSlot_OC *)slot
         albumResource:(id<DVEResourcePickerModel>)albumResource;
```


**Sample Code**

```objectivec
//Replace
//@param slot material slot to be replaced
@param albumResource New Material Resource Model
- (void)replaceResourceForSlot:(NLETrackSlot_OC *)slot
         albumResource:(id<DVEResourcePickerModel>)albumResource
{
//Create and configure the resource object, different configurations are required for videos and pictures
    NLEResourceAV_OC *slotResource = [[NLEResourceAV_OC alloc] init];
    if (albumResource.type == DVEResourceModelPickerTypeImage) {
    NSString *imagePath = [self.draftService copyResourceToDraft:albumResource.URL resourceType:NLEResourceTypeImage];
    
    [slotResource nle_setupForPhoto:imagePath width:albumResource.image.size.width height:albumResource.image.size.height duration:slot.duration];
    } else {
    NSString *videoPath = [self.draftService copyResourceToDraft:albumResource.videoAsset.URL resourceType:NLEResourceTypeVideo];
    
    [slotResource nle_setupForVideo:albumResource.videoAsset resourceFilePath:videoPath];
    }
    
//Encapsulate resource objects
    NLESegmentVideo_OC *videoSegment = [[NLESegmentVideo_OC alloc] init];
    videoSegment.videoFile = slotResource;
    videoSegment.timeClipStart = CMTimeMake(0 * USEC_PER_SEC, USEC_PER_SEC);
    videoSegment.timeClipEnd = slot.getDuration;
    
//Give it to the slot to be replaced. The replacement dimension is segment.
    [slot setSegmentVideo:videoSegment];
    
//Generate a commit
    [self.actionService commitNLE:YES];
}
```


<span id="3908f9ab"></span>
### Copy

**Feature**

Select the main track and click copy. Append the copy to the main track and select the new track by default.

**API definition**

New method \-  **(void)copyVideoOrImageSlot** :

```objectivec
@protocol DVECoreVideoProtocol <DVECoreProtocol>

//Copy
// @param slot: slot to be copied
- (void)copyVideoOrImageSlot:(NLETrackSlot_OC *)slot;
```


```objectivec
//Copy
// @param slot: slot to be copied
- (void)copyVideoOrImageSlot:(NLETrackSlot_OC *)slot
{
//Slot deep copy
    NLETrackSlot_OC *newSlot = [slot deepClone:YES];
    
//Get the track where the current slot is located, generally the main track
    NLETrack_OC *track = [self.vcContext.mediaContext.editor.model trackContainSlotId:slot.nle_nodeId];
//Add slot
    [track addSlot:newSlot afterSlot:slot];
    
//Update the playing time of the track area
    [self.vcContext.mediaContext updateTargetOffsetWithTime:newSlot.startTime];
//Change the currently selected slot to a new slot
    self.vcContext.mediaContext.selectMainVideoSegment = newSlot;
    
//Generate a commit
    [self.actionService commitNLE:YES];
}
```


<span id="60695e4f"></span>
## Audio

<span id="24fd1c27"></span>
### Add an audio clip

**Feature**

Adds an audio clip. An independent audio clip is an independent track, and an audio track may contain multiple non\-overlapping slots.

**API definition**

```objectivec
@interface NLESegmentAudio_OC : NLESegment_OC

///  The audio file.
@property (nonatomic, copy) NLEResourceAV_OC* audioFile;
@property (nonatomic, assign, readonly) CMTime duration;

///  Set whether to keep the original audio after the speed is specified. true specifies to keep the original audio. false specifies to change the speed. Default value: false.
- (void)setKeepTone:(bool)KeepTone;
```


**Sample code**

```objectivec
NLETrack_OC *track = [[NLETrack_OC alloc] init];
track.extraTrackType = NLETrackAUDIO;
track.layer = ([self.vcContext.nleEditor.model nle_getMaxTrackLayer:NLETrackAUDIO] + 1);

NLEResourceAV_OC *audioResource = [[NLEResourceAV_OC alloc] init];
[audioResource nle_setupForAudio:asset];
audioResource.resourceName = audioName;
audioResource.resourceFile = asset.URL.absoluteString.lastPathComponent;
   
NLESegmentAudio_OC *audioSegment = [[NLESegmentAudio_OC alloc] init];
audioSegment.audioFile = audioResource;
audioSegment.timeClipStart = CMTimeMake(0 * USEC_PER_SEC, USEC_PER_SEC);
audioSegment.timeClipEnd = [asset duration];;
   
NLETrackSlot_OC *trackSlot = [[NLETrackSlot_OC alloc] init];
[trackSlot setSegmentAudio:audioSegment];
trackSlot.startTime = CMTimeMake(startTime * USEC_PER_SEC, USEC_PER_SEC);
trackSlot.duration = [asset duration];

//  You can add multiple slots to a track, but the time ranges of the slots cannot overlap.  
[track addSlot:trackSlot];
```


**Note**

You can call addSlot to add multiple slots to a track, which means that you can add multiple audio clips to an audio track.

<span id="ddb1b2d4"></span>
### Delete an audio clip

**Feature**

Deletes the target audio slot from the corresponding track, which is similar to deleting a video.

**API definition**

```objectivec
@interface NLETrack_OC : NLETimeSpaceNode_OC

///  Remove a slot.
/// @param slot NLETrackSlot_OC *
- (void)removeSlot:(NLETrackSlot_OC *)slot;
```


**Sample code**

```objectivec
[track removeSlot:slot];
```


<span id="1521c14a"></span>
## Effects

<span id="142624d2"></span>
### Add a local effect

**Feature**

Adds a local effect, which applies to a certain track. The effective period is determined by the **startTime** and **endTime** of the track slot. Videos on other tracks are not affected.Content that is being copied cannot be copied.

**API definition**

**NLEResourceNode_OC** describes the resource path and type of an effect.

**NLESegmentEffect_OC** describes the content of an effect.

```objectivec
/**
 Type of an object to which an effect applies.
 */
typedef NS_ENUM(NSUInteger, NLESegmentEffectApplyTargetType) {
  NLESegmentEffectApplyTargetTypeMainVideo,  // Main video.
  NLESegmentEffectApplyTargetTypeSubVideo,   // Overlay.
  NLESegmentEffectApplyTargetTypeGlobal,    // Global.
};

@interface NLESegmentEffect_OC : NLESegment_OC
/// The effect name.
@property (nonatomic, copy) NSString *effectName;
/// The effect resource object.
@property (nonatomic, strong) NLEResourceNode_OC* effectSDKEffect;
/// The type of an object to which an effect applies.
@property (nonatomic, assign) NLESegmentEffectApplyTargetType applyTargetType;

@end
```


**Sample code**


* **Add a local effect** : Randomly generate a unique ID when you add an effect. It is required for searching for global or local effect objects subsequently.


```objectivec
  NLEModel_OC *model = self.nle.editor.model;
   
   // The effect resource object.
  NLEResourceNode_OC *resEffect = [[NLEResourceNode_OC alloc] init];
  ///resourceId indicates the unique ID of an effect, which is a randomly generated UUID.
  resEffect.resourceId = [[NSUUID UUID] UUIDString];
  /// The absolute path of the effect resource folder.
  resEffect.resourceFile = path;
  /// The effect resource identifier.
  resEffect.resourceType = NLEResourceTypeEffect;
  /// The AMAZING resource identifier.
  resEffect.resourceTag = NLEResourceTagAmazing;
   
   //The effect asset segment.
  NLESegmentEffect_OC *segEffect = [[NLESegmentEffect_OC alloc] init];
  ///The effect displayed on a video clip on a track.
  [segEffect setEffectName:name];
  /// Specify an effect resource object.
  [segEffect setEffectSDKEffect:resEffect];
   
   // Create an effect object.
    NLETrackSlot_OC *effectSlot = [[NLETrackSlot_OC alloc] init];
    /// The time when the effect starts, which is the current time.
  effectSlot.startTime = CMTimeMake(CMTimeGetSeconds(self.vcContext.mediaContext.currentTime) * USEC_PER_SEC, USEC_PER_SEC);
  /// The time when the effect ends. The effect lasts for 3s by default.
  effectSlot.endTime = CMTimeMake((CMTimeGetSeconds(self.vcContext.mediaContext.currentTime) + 3) * USEC_PER_SEC, USEC_PER_SEC);
  [effect setSegmentEffect:segEffect];
 
     // Add the effect to the main track of a video.
   for (NLETrack_OC *track in [model getTracks]) {
    if ([track isMainTrack]) {
        [track addEffect:effect];
        break；
    }
   }

  //  Commit. The NLE system will run the diff algorithm and apply the effect by using the VE SDK.
  [self.nle.editor commit];
  //  To allow undo on the commit, you can call the done method to save it. Next time you want to undo the commit, you can directly
  // call the editor to undo it.
  [self.nle.editor done];
   /// Obtain the unique ID of the effect object.
  return resEffect.resourceId;
```



* **Replace or update a local effect** : Traverse all tracks based on the unique IDs of effects to find the target resource object, and update the resource path, effect name, start time, and end time.


```objectivec
NSString* effectObjID = Unique ID of the effect, which is randomly generated when the effect is added.
  NSString* resPath =  The new path of the effect resource.
  NSString* name =New effect name.
    /// If the effective period of the effect needs to be updated:
  /// CMTime newStart = The new start time;
  /// CMTime newEnd = The new end time;
  NLEModel_OC *model = self.nle.editor.model;
  // Traverse global tracks.
  for (NLETrack_OC *track in [model getTracks]) {

     for(NLETrackSlot_OC* slot in [track getEffect]){
        NLESegment_OC* segment = [slot segment];
        if([segment isKindOfClass:[NLESegmentEffect_OC class]]){
          NLESegmentEffect_OC *segEffect = (NLESegmentEffect_OC*)segment;
          NLEResourceNode_OC *resEffect = segEffect.effectSDKEffect;
          if ([resEffect.resourceId isEqualToString:effectObjID]) {
        resEffect.resourceFile = resPath;
        segEffect.effectName = name;
           // effect.startTime = newStart;
            // effect.endTime = newEnd;
          // Commit. The NLE system will run the diff algorithm and apply the effect by using the VE SDK.
          [self.nle.editor commit];
          //  To allow undo on the commit, you can call the done method to save it. Next time you want to undo the commit, you can directly
          // call the editor to undo it.
          [self.nle.editor done];
          }
        }
      }
 }
```



* **Delete a local (track) effect** : Traverse all tracks based on the unique IDs of effects to find the target effect object, and remove it from the corresponding track.


```objectivec
NSString* effectObjID = Unique ID of the effect, which is randomly generated when the effect is added.
  NLEModel_OC *model = self.nle.editor.model;
  // Traverse global tracks.
  for (NLETrack_OC *track in [model getTracks]) {

     for(NLETrackSlot_OC* slot in [track getEffect]){
        NLESegment_OC* segment = [slot segment];
        if([segment isKindOfClass:[NLESegmentEffect_OC class]]){
          NLESegmentEffect_OC *segEffect = (NLESegmentEffect_OC*)segment;
          NLEResourceNode_OC *resEffect = segEffect.effectSDKEffect;
          if ([resEffect.resourceId isEqualToString:effectObjID]) {
            [track removeEffect:effect];
          //  Commit. The NLE system will run the diff algorithm and apply the effect by using the VE SDK.
          [self.nle.editor commit];
          //  To allow undo on the commit, you can call the done method to save it. Next time you want to undo the commit, you can directly
          // call the editor to undo it.
          [self.nle.editor done];
          return;
          }
        }
      }
 }
```


**Note**

In the sample code, **resourceId** indicates the unique ID of an effect, which is a randomly generated UUID. It is required for searching for global or local effect objects subsequently. You can modify the method for generating a unique ID.

<span id="6a712bc1"></span>
### Add a global effect

**Feature**

Adds a global effect, which applies to an entire video clip. The effective period is determined by the startTime and endTime of the corresponding slot.

**API definition**

**NLETrack_OC** describes an independent track to which a global effect applies.

**NLEResourceNode_OC** describes the resource path and type of an effect.

**NLESegmentEffect_OC** describes the content of an effect. It is similar to **NLESegmentEffect_OC** of a local effect.

**Sample code**


* **Add a global effect** : A global effect applies to an entire video clip. The effective period is determined by the **startTime** and **endTime** of the corresponding slot.


```objectivec
 // The current global editing model.
  NLEModel_OC *model = self.nle.editor.model;
   
   // The effect resource object.
  NLEResourceNode_OC *resEffect = [[NLEResourceNode_OC alloc] init];
  ///resourceId indicates the unique ID of an effect, which is a randomly generated UUID.
  resEffect.resourceId = [[NSUUID UUID] UUIDString];
  /// The absolute path of the effect resource folder.
  resEffect.resourceFile = path;
  /// The effect resource identifier.
  resEffect.resourceType = NLEResourceTypeEffect;
  /// The AMAZING resource identifier.
  resEffect.resourceTag = NLEResourceTagAmazing;
   
   //The effect asset segment.
  NLESegmentEffect_OC *segEffect = [[NLESegmentEffect_OC alloc] init];
  ///The effect displayed on a video clip on a track.
  [segEffect setEffectName:name];
  /// Specify an effect resource object.
  [segEffect setEffectSDKEffect:resEffect];
   
   // Obtain the current maximum layers of effects (layers on a track are displayed from the top down).
  int32_t maxLayer = [model nle_getMaxEffectLayer] + 1;
   /// The effect slot.
  NLETrackSlot_OC *effectSlot = [[NLETrackSlot_OC alloc] init];
  /// The time when the effect starts, which is the current time.
  effectSlot.startTime = CMTimeMake(CMTimeGetSeconds(self.vcContext.mediaContext.currentTime) * USEC_PER_SEC, USEC_PER_SEC);
  /// The time when the effect ends. The effect lasts for 3s by default.
  effectSlot.endTime = CMTimeMake((CMTimeGetSeconds(self.vcContext.mediaContext.currentTime) + 3) * USEC_PER_SEC, USEC_PER_SEC);
  /// Specify an effect clip object.
  [effectSlot setSegmentEffect:segEffect];
  /// Set a slot layer. Slots on the same track are at the same layer.
  effectSlot.layer = maxLayer;
 
  /// Add a track for a global effect.
  NLETrack_OC *effectTrack = [[NLETrack_OC alloc] init];
  [effectTrack addSlot:effectSlot];
  effectTrack.extraTrackType = NLETrackEFFECT;
  // Add a global effect track in the current global editing model.
  [model addTrack:effectTrack];
  //  Commit. The NLE system will run the diff algorithm and apply the effect by using the VE SDK.
  [self.nle.editor commit];
  //  To allow undo on the commit, you can call the done method to save it. Next time you want to undo the commit, you can directly
  // call the editor to undo it.
  [self.nle.editor done];
   /// Obtain the unique ID of the effect object.
  return resEffect.resourceId;
```



* **Replace or update a global effect** : Traverse all tracks based on the unique IDs of effects to find the target slot object, and update the resource path, effect name, start time, and end time.


```objectivec
NSString* effectObjID =  The unique ID of the effect, which is randomly generated when the effect is added.
  NSString* resPath =  The new path of the effect resource.
  NSString* name =New effect name.
  /// If the effective period of the effect needs to be updated:
  /// CMTime newStart = The new start time;
  /// CMTime newEnd = The new end time;
  NLEModel_OC *model = self.nle.editor.model;
  // Traverse global tracks.
  for (NLETrack_OC *track in [model getTracks]) {
      // The effect track.
    if ([track getTrackType] == NLETrackEFFECT) {
      /// The effect slot. Only one slot is available for a global effect.
      NLETrackSlot_OC *slot = track.slots.firstObject;
      NLESegmentEffect_OC* segEffect = (NLESegmentEffect_OC *)slot.segment;
      NLEResourceNode_OC *resEffect = segEffect.effectSDKEffect;
      if ([resEffect.resourceId isEqualToString: effectObjID]) {
        resEffect.resourceFile = resPath;
        segEffect.effectName = name;
        //slot.startTime = newStart；
        //slot.endTime = newEnd；
        break;
      }
    }
   }
  // Commit. The NLE system will run the diff algorithm and apply the effect by using the VE SDK.
  [self.nle.editor commit];
  //  To allow undo on the commit, you can call the done method to save it. Next time you want to undo the commit, you can directly
  // call the editor to undo it.
  [self.nle.editor done];
```



* **Delete a global effect** : Traverse all tracks based on the unique IDs of effects to find the target track, and remove it from the model.


```objectivec
  NSString* effectObjID =  The unique ID of the effect, which is randomly generated when the effect is added.
  NLEModel_OC *model = self.nle.editor.model;
  // Traverse global tracks.
  for (NLETrack_OC *track in [model getTracks]) {
      // The effect track.
    if ([track getTrackType] == NLETrackEFFECT) {
      NLETrackSlot_OC *slot = track.slots.firstObject;/// The effect slot. Only one slot is available for a global effect.
      NLESegmentEffect_OC* segEffect = (NLESegmentEffect_OC *)slot.segment;
      NLEResourceNode_OC *resEffect = segEffect.effectSDKEffect;
      if ([resEffect.resourceId isEqualToString: effectObjID]) {
         ///  Remove the track from the model.
        [model removeTrack:track];
        break;
      }
    }
 }
 
  // Commit. The NLE system will run the diff algorithm and apply the effect by using the VE SDK.
  [self.nle.editor commit];
  //  To allow undo on the commit, you can call the done method to save it. Next time you want to undo the commit, you can directly
  // call the editor to undo it.
  [self.nle.editor done];
```


**Note**

A global effect must be carried in an independent NLETrack_OC object and added to NLEModel_OC as an independent track.

<span id="70575518"></span>
## Sticker

Coordinates of a sticker on the screen are normalized coordinates with the center position of a video as the origin.

Content that is being copied cannot be copied.

In the VE SDK, a sticker can be rotated for up to 360 degrees. The clockwise direction is the positive direction for rotating a sticker.

In NLE, the counterclockwise direction is the positive direction for rotating a sticker.

Click "Add Sticker", select the sticker and confirm to enter the sticker editing interface.


* Bottom function bar

   Split: Split the current sticker fragment into two, each obtaining the time slice before and after the "split point".

   Copy: Copy the current sticker fragment to the new sticker track, the new sticker fragment retains all attributes except the identity

   Animation: Adds an entry, exit, and loop animation to the current sticker clip

   Delete: Delete the current sticker fragment

* Preview editing box

   Mirror image: sticker flips left and right

   Rotate and zoom: Drag and drop buttons to rotate and zoom

   Copy & Delete: the same as above


<span id="51d13571"></span>
### Add an informative sticker

**Feature**

Adds an informative sticker, which may contain an animation such as an animated GIF or a sprite animation.

**API definition**

**NLESegmentInfoSticker_OC** describes an informative sticker.

```objectivec
@interface NLESegmentInfoSticker_OC : NLESegmentSticker_OC

///  The asset resource of an informative sticker.
@property (nonatomic, strong) NLEResourceNode_OC *effectSDKFile;
```


The category corresponding to the sticker fragment is NLETrackSlot_OC, and the "**Copy**", "**Split**" and "**Delete**" of the sticker are all based on NLETrackSlot_OC operations. Some basic operations on NLETrackSlot_OC are packed here.

```objectivec
@protocol DVECoreSlotProtocol <DVECoreProtocol>

- (NLETrackSlot_OC *)splitForSlot:(NLETrackSlot_OC *)slot;

- (NLETrackSlot_OC *)copyForSlot:(NSString *)segmentId needCommit:(BOOL)commit;

- (BOOL)removeSlot:(NSString *)segmentId
    needCommit:(BOOL)commit
    isMainEdit:(BOOL)mainEdit;

- (NLETrackSlot_OC *)addSlot:(NLETrackType)trackType
        resourceType:(NLEResourceType)resourceType
           segment:(NLESegment_OC *)segment
          startTime:(CMTime)startTime
          duration:(CMTime)duration;
```


The corresponding category of sticker "**animation**" is NLEStyStickerAnimation_OC, which is used for entry, exit and loop animation.

NLETrackSlot_OC 》NLESegmentSticker_OC 》NLEStyStickerAnimation_OC

```objectivec
@interface NLEStyStickerAnimation_OC : NLENode_OC

///Is it a loop animation? If yes, use inPath as the animation path
@property (nonatomic, assign) BOOL loop;

///Entry animation duration in microseconds
@property (nonatomic, assign) int32_t inDuration;

///Exit animation duration in microseconds
@property (nonatomic, assign) int32_t outDuration;

///Entry (or loop) animation
@property (nonatomic, strong) NLEResourceNode_OC *inAnimation;

///Exit animation
@property (nonatomic, strong) NLEResourceNode_OC *outAnimation;

@end
```


Sticker "**Mirror**"

```objectivec
@interface NLETimeSpaceNode_OC : NLENode_OC

- (void)setMirror_X:(NSInteger)mirrorx;

@end
```


**Sample code**

```objectivec
//   Create a sticker track.
NLEModel_OC *model = [self.vcContext.mediaContext.editor getModel];
NLETrack_OC *stickerTrack = [[NLETrack_OC alloc] init];
stickerTrack.extraTrackType = NLETrackSTICKER;
stickerTrack.layer = (int)([model nle_getMaxTrackLayer:NLETrackSTICKER] + 1);
[model addTrack:stickerTrack];

//  The asset resource of a sticker.
NLEResourceNode_OC *node = [[NLEResourceNode_OC alloc] init];
[node setResourceFile:path];
[node setResourceType:NLEResourceTypeSticker];
    
NLESegmentInfoSticker_OC *sticker = [[NLESegmentInfoSticker_OC alloc] init];
[sticker setEffectSDKFile:node];

//  Create a slot for placing the sticker and set the start time and end time relative to the track.  
NLETrackSlot_OC *stickerSlot = [[NLETrackSlot_OC alloc] init];
stickerSlot.startTime = CMTimeMake(startTime * USEC_PER_SEC, USEC_PER_SEC);
stickerSlot.endTime = CMTimeMake(endTime * USEC_PER_SEC, USEC_PER_SEC);

//  Set the sticker translation.
stickerSlot.transformX = x;
stickerSlot.transformY = y;

//  Set the sticker scale ratio. Default value: 1.
stickerSlot.scale = 1;

//  Set the sticker rotation degree.
stickerSlot.rotation = 0;
stickerSlot.segment = sticker;
stickerSlot.Mirror_X = NO;
    
[stickerTrack addSlot:stickerSlot];
   
[self.vcContext commitNLE:YES];
```



* Split


```objectivec
- (NLETrackSlot_OC *)splitForSlot:(NLETrackSlot_OC *)slot
{
  if (!slot) { return nil; }
   
  DVEMediaContext *mediaContext = self.vcContext.mediaContext;
  
//Deep copy slot, but ID and Name will be updated
  NLETrackSlot_OC *newSlot = [slot deepClone:YES];
  
//The timeRange of the original slot is updated to "startTime-currentTime"
  slot.endTime = mediaContext.currentTime;
//newSlot's timeRange is updated to "currentTime-endTime"
  newSlot.startTime = mediaContext.currentTime;
   
  NLEModel_OC *model = [mediaContext.editor getModel];
  NLETrack_OC *track = [model trackContainSlotId:slot.nle_nodeId];
//Add newSlot to the track where the "original slot" is located
  [track addSlot:newSlot];
   
  [self.actionService commitNLE:YES];
  mediaContext.selectTextSlotAtCurrentTime = newSlot;
   
  return newSlot;
}
```



* Copy


```objectivec
- (NLETrackSlot_OC *)copyForSlot:(NSString *)segmentId needCommit:(BOOL)commit
{
  NLETrackSlot_OC *slot = nil;
//Currently on the cover editing page
  BOOL isCoverEnable = self.vcContext.nleEditor.model.coverModel.enable;
  if (isCoverEnable) {
    slot = [self.vcContext.nleEditor.model.coverModel slotOf:segmentId];
  } else {
    slot = [self.vcContext.nleEditor.model slotOf:segmentId];
  }
   
  if (!slot) {
    return nil;
  }
   
  NLETrack_OC *track = nil;
  if (isCoverEnable) {
    track = [self p_trackContainSlotId:slot.nle_nodeId array:self.vcContext.nleEditor.model.coverModel.tracks];
  } else {
    track = [self.vcContext.nleEditor.model trackContainSlotId:slot.nle_nodeId];

  }
  if (!track) {
    return nil;
  }
  NLEResourceType resourceType = track.nle_extraResourceType;
   
//Track 
  NLETrackSlot_OC *newSlot = [slot deepClone:YES];
   
  float offset = 0.1f;
  if (resourceType == NLEResourceTypeTextSticker) {
//Offest to the right
    newSlot.transformX += offset;
  } else if (resourceType == NLEResourceTypeSticker) {
//Offset downward
    newSlot.transformY -= offset;
  }
   
  NLEModel_OC *model = [self.vcContext.mediaContext.editor getModel];
// New track
  NLETrack_OC *newTrack = [[NLETrack_OC alloc] init];

  newTrack.extraTrackType = track.extraTrackType;
  newTrack.nle_extraResourceType = resourceType;
  newTrack.layer = (int)([model nle_getMaxTrackLayer:track.extraTrackType] + 1);
//Add newSlot to newTrack
  [newTrack addSlot:newSlot];
   
  if (isCoverEnable) {
    [self.vcContext.nleEditor.model.coverModel addTrack:newTrack];
  } else {
    [model addTrack:newTrack];
  }
  [self.actionService commitNLE:(isCoverEnable ? NO : commit)];
  self.vcContext.mediaContext.selectTextSlotAtCurrentTime = newSlot;
   
  return newSlot;
}
```



* Delete


```objectivec
- (BOOL)removeSlot:(NSString *)segmentId
     needCommit:(BOOL)commit
     isMainEdit:(BOOL)mainEdit
{
  NLETrackSlot_OC *slot = nil;
  if (mainEdit) {
    slot = [self.vcContext.nleEditor.model slotOf:segmentId];
  } else {
    slot = [self.vcContext.nleEditor.model.coverModel slotOf:segmentId];
  }
   
  if (!slot) {
    return NO;
  }
   
  if (mainEdit) {
    NLETrackType trackType = [self.vcContext.nleEditor.model trackContainSlotId:slot.nle_nodeId].extraTrackType;
//Remove the target slot from the track
    [[self.vcContext.mediaContext.editor getModel] nle_removeSlots:@[slot.nle_nodeId] inTrackType:trackType];
  } else {
    NLETrackType trackType = [self p_trackContainSlotId:slot.nle_nodeId array:self.vcContext.nleEditor.model.coverModel.tracks].extraTrackType;
    [self.vcContext.mediaContext.editor.model.coverModel nle_removeSlots:@[slot.nle_nodeId] inTrackType:trackType];
  }
   
  [self.actionService commitNLE:commit];
  self.vcContext.mediaContext.selectTextSlot = nil;
   
  return YES;
}
```



* Set the sticker animation


```objectivec
//Set the sticker animation, the seconds parameter comes from UI settings
- (void)setStickerAnimation:(CGFloat)seconds
{
//Create sticker animation object
  NLEStyStickerAnimation_OC *animation = [[NLEStyStickerAnimation_OC alloc] init];
  
  NLEResourceNode_OC *node = [[NLEResourceNode_OC alloc] init];
  node.name = self.name;
  node.resourceFile = self.path;
  
//Set resource properties for sticker animation objects
  animation.inAnimation = node;
//Set the duration for the sticker animation object
  animation.inDuration = seconds * 1000 * 1000;
  
  NLETrackSlot_OC *slot = self.vcContext.mediaContext.selectTextSlot;
  if (slot) {
    NLESegmentSticker_OC *seg = (NLESegmentSticker_OC *)slot.segment;
//Add animation to segments
    seg.stickerAnimation = animation;
     
    [self.actionService commitNLE:NO];
  }
   
  if (animation.inDuration > 0 || animation.outDuration > 0) {
    [self.vcContext.nle setStickerPreviewMode:slot previewMode:(int)type + 1];
  }
}
```



* Mirror image


```objectivec
- (void)setStickerFilpX:(NSString *)segmentId {
  NLETrackSlot_OC *slot = [self.vcContext.nleEditor.model slotOf:segmentId];
  if (!slot) {
    slot = [self.vcContext.nleEditor.model.coverModel slotOf:segmentId];
  }
  if (!slot) {
    return;
  }
   
//Flip along x = 0.5 axis (flip left and right)
  slot.Mirror_X = ！slot.Mirror_X;
  
  [self.actionService commitNLE:YES];
}
```


<span id="044527e4"></span>
### Add a text sticker

**Feature**

Adds a text sticker to a video to enrich the video description.

You can customize the sticker style, including the font, text color, borders, background color, shadow, alignment, font\-weight (**bold**), and font\-style (italic), and scale, translate, or rotate the sticker.

Other elements, such as swash characters, bubble fonts, and animations (including In, Out, and loop animations), can also be added to a text sticker.

You can add In and Out animations together and specify their time. You can also specify the speed of a loop animation.

**API definition**

**NLEStyleText_OC** describes the text style, such as the text size, font, and color.

**NLESegmentTextSticker_OC** describes the text content.

```objectivec
@interface NLESegmentTextSticker_OC : NLESegmentSticker_OC
/// Enter the text content.
@property (nonatomic, copy) NSString *content;
/// Set the text style.
@property (nonatomic, strong) NLEStyleText_OC *style;
/// Construct an object by using a JSON string.
+ (instancetype)textStickerWithEffectSDKJSONString:(NSString *)effectSDKJSONString;
/// Set the object attribute by using a JSON string.
- (void)setEffectSDKJSONString:(NSString *)effectSDKJSONString;
@end
```


Detailed style definition

```objectivec
@interface NLEStyleText_OC : NLENode_OC

///   Set the font size, measured by the line-height in points. Conversion between pixels (px) and points (pt): px = pt/72 x 300
@property (nonatomic, assign) uint32_t fontSize;

///   Set the background color. Convert the 0xFFFFFFFF format to the AARRGGBB format. A is short for alpha, R for red, G for green, and B for blue.
@property (nonatomic, assign) uint32_t backgroundColor;

///  Set the text outline color, which is represented by an RGBA value. This setting will become invalid when swash characters are used.
@property (nonatomic, assign) uint32_t outlineColor;

///  Set the text color. Convert the 0xFFFFFFFF format to the AARRGGBB format. A is short for alpha, R for red, G for green, and B for blue.
@property (nonatomic, assign) uint32_t textColor;

/// The alignment type.
/*
 AlignType_LEFT = 0;
 AlignType_CENTER = 1;
 AlignType_RIGHT = 2;
 AlignType_TOP = 3;
 AlignType_BOTTOM = 4;
 */
@property (nonatomic, assign) int alignType;
@property (nonatomic, assign) int typeSettingKind; // Set the typesetting type.

/// Set the shadow color. Convert the 0xFFFFFFFF format to the AARRGGBB format. A is short for alpha, R for red, G for green, and B for blue. This setting will become invalid when swash characters are used.
@property (nonatomic, assign) uint32_t shadowColor;

///  Set the blur radius of the shadow. The value is the ratio of the actual radius to the line-height of text. For example, the value 0.1 indicates that the line-height is 10 times the blur radius.
/// A greater value of shadowSmoothing indicates more blurred shadow borders. The value 0 indicates that the shadow is
/// in the same shape as the text. This setting will become invalid when swash characters are used.
@property (nonatomic, assign) float shadowSmoothing;

/// Set the x and y component offsets from the text for the shadow. The value of x or y is the ratio
/// of the offset to the line-height of text. For example, [0.1, -0.1] indicates that the shadow is moved downward and rightward from the text. This setting will become invalid when swash characters are used.
@property (nonatomic, assign) float shadowOffsetX;
@property (nonatomic, assign) float shadowOffsetY;

///  Set whether to display the text in bold.
@property (nonatomic, assign) BOOL bold;

///  Set the font-weight value, which is the ratio of the actual weight to the line-height of the original text. The value ranges from –0.05 to 0.05, for example, 0 (normal), positive value (bold), and negative value (thin).
@property (nonatomic, assign) float boldWidth;

///  Set the italic angle, in degrees. The value ranges from 0 to 45, for example, 0 (normal).
@property (nonatomic, assign) uint32_t italicDegree;

/// Set whether to underline the text. The value true indicates yes.
@property (nonatomic, assign) BOOL underline;

///  Set the underline width, which is the ratio of the actual width to the line-height of text. The value ranges from 0.0 to 1.0.
@property (nonatomic, assign) float underlineWidth;

///  Set the underline offset from the baseline, which is the ratio of the distance between the underline and the baseline to the line-height of text. The value ranges from 0.0 to 1.0.
@property (nonatomic, assign) float underlineOffset;

///  Set the line spacing for typesetting, which is the ratio of the actual spacing to the line-height of text. The value 0 indicates that two adjacent lines are tightly close to each other based on the line-height of text.
@property (nonatomic, assign) float lineGap;

///  Set the character spacing, which is the ratio of the actual spacing to the line-height of text. The value 0 indicates that two adjacent characters in a line are tightly close to each other based on the standard typesetting.
/// A single English letter or a Chinese word is counted as a character.
@property (nonatomic, assign) float charSpacing;

///  Set the inner padding, which is the ratio of the actual padding to the line-height of text. The inner padding is a spacing between an edge of an text box and the corresponding edge of the minimum bounding box of text in the text box.
/// The value 0 indicates that text is tightly enclosed by the text box in the up, down, left, and right directions. The minimum bounding box of text does not incorporate the borders or shadow of text.
/// Therefore, if the inner padding is set to 0 and a specific outline width is set, outlined content will extend out of the text box. If color is filled in the background of the text box, outlined content will also extend out of the background.
/// To control outlined content within the text box, set innerPadding to be greater than or equal to outlineWidth.
@property (nonatomic, assign) float innerPadding;

///  Set whether to outline the text. The value true indicates yes. This setting will become invalid when swash characters are used.
@property (nonatomic, assign) BOOL outline;

///  Set the outline width, which is the ratio of the actual width to the line-height of text. The value 0.1 indicates that the outline width of text is 0.1 times the line-height of text. The maximum value is 0.2. This setting will become invalid when swash characters are used.
@property (nonatomic, assign) float outlineWidth;

///  Set whether to mirror a bubble font over the X-axis. The value true indicates yes.
@property (nonatomic, assign) BOOL shapeFlipX;

///  Set whether to mirror a bubble font over the Y-axis. The value true indicates yes.
@property (nonatomic, assign) BOOL shapeFlipY;

/// Set the color of the text with karaoke effect. This setting will take effect only when the karaoke text effect script is used.
@property (nonatomic, assign) uint32_t KTVColor;

///  Set the outline color of the text with karaoke effect. This setting will take effect only when the karaoke text effect script is used.
@property (nonatomic, assign) uint32_t KTVOutlineColor;

///  Set the shadow color of the text with karaoke effect. This setting will take effect only when the karaoke text effect script is used.
@property (nonatomic, assign) uint32_t KTVShadowColor;

///  Set whether to automatically truncate a line when the specified line width is reached and call setTruncatedPostfix to set the postfix.
@property (nonatomic, assign) BOOL oneLineTruncated;

///  Set whether to fill color in the background of the text box on the sticker. The value true indicates yes.
@property (nonatomic, assign) BOOL background;

/// true  specifies to add shadow to text. This option becomes invalid when swash characters are used.
@property (nonatomic, assign) BOOL shadow;

/// Set the line width for automatic line breaking, which is the ratio of the actual line width to the width of the display window. The value –1 indicates that automatic line breaking is disabled (the line width for automatic line breaking is actually set to 4000 px).
/// In horizontal typesetting, the text automatically wraps around to the next row when reaching the maximum line width. In vertical typesetting, the text automatically wraps around to the next column when reaching the maximum line width. When the value is greater than 0, it is displayed as the ratio of the actual line width to the width of the display window. When the value is less than 0, its format is not limited.
@property (nonatomic, assign) float lineMaxWidth;

@property (nonatomic, strong) NSString *truncatedPostfix;

///  Set the absolute path of the unzipped font file (in TTF, OTF, or TTC format).
/// In iOS, you can leave this parameter unspecified to use the system default font. In Android, you must specify a valid value; otherwise, no font will be applied.
@property (nonatomic, strong) NLEResourceNode_OC *font;

/// Set the absolute path of the unzipped font file (in TTF, OTF, or TTC format) for rollback when
/// the preferred font is not found.
/// In iOS, you can leave this parameter unspecified to use the system default font. In Android, you must specify a valid value; otherwise, no font will be applied.
@property (nonatomic, strong) NLEResourceNode_OC *fallbackFont;

///  Set the absolute path of the bubble font package. The value must be the root directory of the unzipped file. Once a valid bubble font package is used for typesetting, the font size will be automatically adapted to the bubble font-style until the bubbles are filled.
/// The size of a text box is defined by the bubble. Attach the document for creating a bubble font package.
@property (nonatomic, strong) NLEResourceNode_OC *shape;

///  Set the absolute path of the swash character package. The value must be the root directory of the unzipped file.
/// Once a valid swash character package is used for typesetting, the text will be rendered with swash characters, and the shadow and outline parameters will become invalid.
@property (nonatomic, strong) NLEResourceNode_OC *flower;


/// Set whether to use the default color in the swash character package. The value true indicates yes. The text color can be changed even though the default color is used.
/// Changing the text color will cause a specific change of swash characters.
/// Users tend to choose the default initial colors in the swash character package when they use swash characters for the first time. However, this parameter is required for subsequent use and restoration from a draft.
/// This feature is infrequently used in Capcut, and most users still tend to choose the default initial color in the swash character package.
/// Therefore, we recommend that you set useEffectDefaultColor to true when you use this feature on other clients.
@property (nonatomic, assign) BOOL useFlowerDefaultColor;
```


**Sample code**


* Add a sticker


```objectivec
NSDictionary *params = @{
        @"version": @"1",
        @"text": @"Enter text",
        @"background": @YES,
        @"fontSize": @15,
        @"fontPath": fontPath, // Path of a font package.
        @"effectPath": @"", // Path of a swash character package.
        @"useEffectDefaultColor": @NO,
        @"shapePath": @"", // Path of a bubble font package.
        @"textColor": @[@1,@1,@1,@1],
        @"backgroundColor": @[@0,@0,@0,@0],
        @"outlineColor":@[@0,@0,@0,@0],
        @"shadowColor":@[@0,@0,@0,@0],
        @"underlineWidth":@(0.05),
        @"lineMaxWidth":@(-1),
        @"lineGap": @(0.1),
        @"boldWidth":@(0),
        @"italicDegree":@(0),
        @"underlineOffset": @(0.22),
        @"innerPadding":@(0.18),
        @"alignType":@(1),
        @"shadow":@(YES),
        @"charSpacing":@(0),
        @"outline":@(YES),
        @"underline":@(NO),
        @"typeSettingKind":@(0)
    };
    
    CGFloat duration = 3;
    CGFloat startTime = CMTimeGetSeconds(self.vcContext.mediaContext.currentTime);
    CGFloat endTime = startTime + duration;
    
    //  Create a sticker track.
    NLEModel_OC *model = [self.vcContext.mediaContext.editor getModel];
    NLETrack_OC *textTrack = [[NLETrack_OC alloc] init];
    textTrack.extraTrackType = NLETrackSTICKER;
    textTrack.layer = (int)([model nle_getMaxTrackLayer:NLETrackSTICKER] + 1);
    [model addTrack:textTrack];
    
    //  Set the style and content of a text sticker.
    NLEStyleText_OC *styleText = [NLEStyleText_OC textStyleWithJSONString:params.dve_toJsonString];
    NLESegmentTextSticker_OC *segment = [[NLESegmentTextSticker_OC alloc] init];;
    segment.style = styleText;
    segment.content = params[@"text"];
    
    //  Set the start time and end time of a text sticker relative to the track.
    NLETrackSlot_OC *textSlot = [[NLETrackSlot_OC alloc] init];
    textSlot.startTime = CMTimeMake(startTime * USEC_PER_SEC, USEC_PER_SEC);
    textSlot.endTime = CMTimeMake(endTime * USEC_PER_SEC, USEC_PER_SEC);
    textSlot.segment = segment;
    
    [textTrack addSlot:textSlot];
    
    [self.vcContext commitNLE:NO];
```



* Copy text

   Note: **name** in **NLETrackSlot_OC** must be modified.


```objectivec
///  Copy text.
- (NSString *)copyInfoSticker:(NSString *)segmentId isCommit:(BOOL)commit {
  NLETrackSlot_OC *slot = nil;
  // Indicates that the user enters the thumbnail editing screen.
  BOOL isCoverEnable = self.vcContext.nleEditor.model.coverModel.enable;
  if (isCoverEnable) {
    slot = [self.vcContext.nleEditor.model.coverModel slotOf:segmentId];
  } else {
    slot = [self.vcContext.nleEditor.model slotOf:segmentId];
  }
   
  if (!slot) {
    return nil;
  }
   
  if (![slot.segment isKindOfClass:NLESegmentTextSticker_OC.class]) {
    return nil;
  }
   
  // The track.
  NLETrackSlot_OC *newSlot = [slot deepClone];
  //  Modify name.
  newSlot.name = @(newSlot.getID).stringValue;
  //  Shift rightward.
  float offset = 0.1f;
  newSlot.transformX = slot.transformX + offset;
   
  NLEModel_OC *model = [self.vcContext.mediaContext.editor getModel];
  NLETrack_OC *textTrack = [[NLETrack_OC alloc] init];
  textTrack.extraTrackType = NLETrackSTICKER;
  textTrack.nle_extraResourceType = NLEResourceTypeTextSticker;
  textTrack.layer = (int)([model nle_getMaxTrackLayer:NLETrackSTICKER] + 1);
  [textTrack addSlot:newSlot];
   
  if (isCoverEnable) {
    [self.vcContext.nleEditor.model.coverModel addTrack:textTrack];
  } else {
    [model addTrack:textTrack];
  }
  [self.vcContext commitNLE:(isCoverEnable ? NO : commit)];
  self.vcContext.mediaContext.selectTextSlotAtCurrentTime = newSlot;
   
  return [newSlot nle_nodeId];
}
```



* Split text


```objectivec
-(void)splitText:(id<DVEBarComponentProtocol>)component
{
  DVELogInfo(@"split one text track ");
  NLETrackSlot_OC* slot = self.vcContext.mediaContext.selectTextSlot;
  //  Determine whether a track can be split.
  BOOL res = [self canSplitWithSlot:slot];
  if (!res) {
    return;
  }
   
  NSString *newSegId = [self.vcContext.textEditor splitTextForSlot:slot];
  [self.parentVC.stickerEditAdatper addEditBoxForSticker:newSegId isText:YES];
}

///  Split text.
/// @param slot: the slot in which the text is to be split.
- (NSString*)splitTextForSlot:(NLETrackSlot_OC*)slot
{
    if (!slot) { return nil; }
    // Add a new slot and modify the end time of the old slot.
    NLETrackSlot_OC* newSlot = [slot deepClone];
    newSlot.name = @(newSlot.getID).stringValue;
    slot.endTime = self.vcContext.mediaContext.currentTime;
    newSlot.startTime = self.vcContext.mediaContext.currentTime;
    
    NLEModel_OC *model = [self.vcContext.mediaContext.editor getModel];
    NLETrack_OC *textTrack = [model trackContainSlotId:slot.nle_nodeId];
    [textTrack addSlot:newSlot];
    
    [self.vcContext commitNLE:YES];
    self.vcContext.mediaContext.selectTextSlotAtCurrentTime = newSlot;
    
    return [newSlot nle_nodeId];
}
```



* Delete a sticker


```objectivec
- (void)removeInfoSticker:(NSString * )segmentId isCommit:(BOOL)commit isMainEdit:(BOOL)mainEdit {
  NLETrackSlot_OC *slot = nil;
    if (mainEdit) {
        slot = [self.vcContext.nleEditor.model slotOf:segmentId];
    } else {
        slot = [self.vcContext.nleEditor.model.coverModel slotOf:segmentId];
    }
    if (!slot) {
        return;
    }
    if (mainEdit) {
        [[self.vcContext.mediaContext.editor getModel] nle_removeSlots:@[slot.nle_nodeId] inTrackType:NLETrackSTICKER];
    } else {
        [self.vcContext.mediaContext.editor.model.coverModel nle_removeSlots:@[slot.nle_nodeId] inTrackType:NLETrackSTICKER];
    }
    [self.vcContext commitNLE:commit];
    self.vcContext.mediaContext.selectTextSlot = nil;
}
```


<span id="4c2e7238"></span>
### Bubble

**Feature**

Add bubble fonts to text.

**API definition**

**NLEResourceNode_OC** describes a bubble font package.

```objectivec
@interface NLEStyleText_OC : NLENode_OC

///  Set the absolute path of the bubble font package. The value must be the root directory of the unzipped file. Once a valid bubble font package is used for typesetting, the font size will be automatically adapted to the bubble font-style until the bubbles are filled.
/// The size of a text box is defined by the bubble.
@property (nonatomic, strong) NLEResourceNode_OC *shape;

@end

@interface NLEResourceNode_OC : NLENode_OC
/// The resource ID.
@property (nonatomic, copy) NSString *resourceId;
//  The path of the resource package.
@property (nonatomic, copy) NSString *resourceFile;
/// The resource name.
@property (nonatomic, copy) NSString *resourceName;
/// The resource type.
@property (nonatomic, assign) uint32_t width;
@property (nonatomic, assign) uint32_t height;

@property (nonatomic, assign) NLEResourceType resourceType;
/// The resource tags.
@property (nonatomic, assign) NLEResourceTag resourceTag;
/// The resource duration.
@property (nonatomic, assign) CMTime duration;

// Deep clone.
- (NLEResourceNode_OC*)deepClone;

@end


Sample code
Add bubble fonts.

```


**Sample Code**


* Add a sticker


```objectivec
NLEResourceNode_OC *resNode = [[NLEResourceNode_OC alloc] init];
resNode.resourceId = @""; //  The resource ID.
resNode.resourceFile = @""; // Resource path.
resNode.resourceType = NLEResourceTypeBubble;

NLETrackSlot_OC* slot = self.vcContext.mediaContext.selectTextSlot;
NLESegmentTextSticker_OC *textSeg = (NLESegmentTextSticker_OC *)slot.segment;
NLEStyleText_OC *style = textSeg.style;
style.shape = resNode;
[self.vcContext.stickerEditor updateTextStickerWithParm:self.curParm segmentID:self.segmentId isCommit:NO isMainEdit:self.isMainEdit];
```


Call the following method containing the NLE API to modify the style:

```objectivec
- (void)updateTextStickerWithParm:(DVETextParm *)parm
            segmentID:(NSString *)segId
             isCommit:(BOOL)commit
            isMainEdit:(BOOL)mainEdit {
  NLETrackSlot_OC *slot = nil;
  if (mainEdit) {
    slot = [self.vcContext.nleEditor.model slotOf:segId];
  } else {
    slot = [self.vcContext.nleEditor.model.coverModel slotOf:segId];
  }
   
  if (!slot) {
    return;
  }
  //  Obtain the converted dictionary.
  NSDictionary *params = [self convertTextParamToDic:parm slot:slot];
   
  //  Record text in the NLE system.
  NSString *text = [params valueForKey:@"text"];

  NLEStyleText_OC *styleText = [NLEStyleText_OC textStyleWithJSONString:params.dve_toJsonString];
   
  if (styleText.flower.resourceFile.length > 0) {
    NSString *relativePath = [self.vcContext.draftEditor copyResourceToDraft:[NSURL fileURLWithPath:styleText.flower.resourceFile] resourceType:NLEResourceTypeFlower];
    styleText.flower.resourceFile = relativePath;
  }
  if (styleText.font.resourceFile.length > 0) {
    NSString *relativePath = [self.vcContext.draftEditor copyResourceToDraft:[NSURL fileURLWithPath:styleText.font.resourceFile] resourceType:NLEResourceTypeFont];
    styleText.font.resourceFile = relativePath;
  }
   
  NLESegmentTextSticker_OC *segment = (NLESegmentTextSticker_OC *)slot.segment;
  segment.style = styleText;
  segment.content = VEOptionsStringValue(text, @"");
   
  [self.vcContext commitNLE:commit];
}
```


<span id="a65baf97"></span>
### Add a picture sticker

**Feature**

Adds a picture as a sticker.

**API definition**

```objectivec
/// Picture sticker.
@interface NLESegmentImageSticker_OC : NLESegmentSticker_OC

/// Crop a picture.
@property (nonatomic, strong) NLEStyCrop_OC *crop;

/// Picture file.
@property (nonatomic, strong) NLEResourceNode_OC *imageFile;
```


**Sample code**

```objectivec
//   Create a sticker track.
NLEModel_OC *model = [self.vcContext.mediaContext.editor getModel];
NLETrack_OC *stickerTrack = [[NLETrack_OC alloc] init];
stickerTrack.extraTrackType = NLETrackSTICKER;
stickerTrack.layer = (int)([model nle_getMaxTrackLayer:NLETrackSTICKER] + 1);
[model addTrack:stickerTrack];

//  The asset resource of a sticker.
NLEResourceNode_OC *node = [[NLEResourceNode_OC alloc] init];
[node setResourceFile:path];
[node setResourceType:NLEResourceTypeSticker];
    
NLESegmentImageSticker_OC *sticker = [[NLESegmentImageSticker_OC alloc] init];
sticker.imageFile = node;

//  Create a slot for placing the sticker and set the start time and end time relative to the track.  
NLETrackSlot_OC *stickerSlot = [[NLETrackSlot_OC alloc] init];
stickerSlot.startTime = CMTimeMake(startTime * USEC_PER_SEC, USEC_PER_SEC);
stickerSlot.endTime = CMTimeMake(endTime * USEC_PER_SEC, USEC_PER_SEC);

//  Set the sticker translation.
stickerSlot.transformX = x;
stickerSlot.transformY = y;

//  Set the sticker scale ratio. Default value: 1.
stickerSlot.scale = 1;

//  Set the sticker rotation degree.
stickerSlot.rotation = 0;
stickerSlot.segment = sticker;
stickerSlot.Mirror_X = NO;
    
[stickerTrack addSlot:stickerSlot];
   
[self.vcContext commitNLE:YES];
```


<span id="8f3307bf"></span>
## Canvas

<span id="7ad2a701"></span>
### Adjust canvas aspect ratio

**Feature**

Adjusts the aspect ratio of an entire video.

**API definition**

```objectivec
@interface NLEModel_OC : NLETimeSpaceNode_OC

///  Set the canvas aspect ratio, which is the ratio of the screen width to the screen height and is 16:9 by default when the desktop editor is in landscape.
@property (nonatomic, assign) float canvasRatio;
```


**Sample code**

```objectivec
self.nle.editor.model.canvasRatio = width / height;
```


<span id="53b07d97"></span>
### Set canvas style

**Feature**

Sets canvas parameters for a video, for example, sets whether to use a picture or a pure color as the background.

**API definition**

```objectivec
@interface NLESegmentVideo_OC : NLESegmentAudio_OC

/// Canvas parameters.
@property (nonatomic, strong) NLEStyCanvas_OC *canvasStyle;
```


**Sample code**

```objectivec
@interface NLEStyCanvas_OC : NLENode_OC
///  The canvas type. The default color is used.
@property (nonatomic, assign) NLECanvasType canvastype;

///  The canvas color. This field is valid only when type is set to COLOR. The value is in ARGB format, and the default color is black.
@property (nonatomic, assign) uint32_t   color;

///  The blur radius of the canvas background. This field is valid only when type is set to VIDEO_FRAME. The value ranges from 1 to 14, and the default value is 0 (not blurred).
@property (nonatomic, assign) float     BlurRadius;

///  The gradient start color of the canvas. This field is valid only when type is set to GRADIENT_COLOR.
@property (nonatomic, assign) uint32_t     StartColor;

///  The gradient end color of the canvas. This field is valid only when type is set to GRADIENT_COLOR.
@property (nonatomic, assign) uint32_t     EndColor;

///  Set whether to enable anti-aliasing. The default value is false.
@property (nonatomic, assign) bool     Antialiasing;

///  The background image of the canvas. This field is valid only when type is set to IMAGE.
@property (nonatomic, strong) NLEResourceNode_OC *imageSource;
```


<span id="c4c446fc"></span>
### Canvas Background

**Feature**

The canvas function is used to replace the background of previewing materials with the following types:

Solid color: replace with different colour

Image type: replace with a local image or image resources provided by CK

Video frame type: replace with the material itself processed by Gaussian blur

**API Definition**

The CanvasStyle attribute in NLESegmentVideo describes the canvas for this segment:

```objectivec
@interface NLESegmentVideo_OC : NLESegmentAudio_OC

.....
///Canvas parameters
@property (nonatomic, strong) NLEStyCanvas_OC *canvasStyle;

....

@end
```


NLEStyCanvas_OC is defined as follows, where NLECanvasType represents four types: solid color, picture, video frame, gradient.

**Image formats that image type Canvas currently supports include JPG, PNG, JPEG.** 

```objectivec
typedef NS_ENUM(NSUInteger, NLECanvasType){
NLECanvasColor = 0,//Canvas type is color
NLECanvasImage = 1,//Canvas type is image
NLECanvasVideoFrame = 2,//Canvas type is video frame
NLECanvasGradientColor = 3,//Canvas type is gradient
};

@interface NLEStyCanvas_OC : NLENode_OC

///Canvas type, default color
@property (nonatomic, assign) NLECanvasType canvasType;

///This field will only take effect when the canvas color type = COLOR, ARGB format, default black
@property (nonatomic, assign) uint32_t   color;

///This field only takes effect when the canvas background blur radius type = VIDEO_FRAME; blur level 1-14, 0 is not blur; default 0
@property (nonatomic, assign) float blurRadius;

///This field only takes effect when the canvas gradient start color type = GRADIENT_COLOR
@property (nonatomic, assign) uint32_t startColor;

///This field will only take effect when the canvas gradient ends with color type = GRADIENT_COLOR
@property (nonatomic, assign) uint32_t endColor;

///Anti-aliasing-performance loss, default false
@property (nonatomic, assign) bool antialiasing;
@property (nonatomic, assign) uint32_t   borderColor;
@property (nonatomic, assign) uint32_t   borderWidth;

///This field will only take effect when the canvas background image type = IMAGE
@property (nonatomic, strong) NLEResourceNode_OC *imageSource;

@end
```


**Sample Code**

Change the canvas of the selected slot to the solid color type, and specify the canvas of the color value:

```objectivec
- (void)applyCanvasColorWithValue:(NSNumber *)value {
//Get the slot corresponding to the current timeline
  NLETrackSlot_OC *slot = self.vcContext.mediaContext.mappingTimelineVideoSegment.slot;
  NLESegmentVideo_OC *segment = (NLESegmentVideo_OC *)slot.segment;
  [self p_applyCanvasColorWithSegment:segment value:value];
}

- (void)p_applyCanvasColorWithSegment:(NLESegmentVideo_OC *)segment
                value:(NSNumber *)value {
  if (!segment.canvasStyle) {
    segment.canvasStyle = [[NLEStyCanvas_OC alloc] init];
  }
// Set the canvas type
  segment.canvasStyle.canvasType = NLECanvasColor;
//Assign hexadecimal color numbers, such as 0xFFFFFF
  segment.canvasStyle.color = [value unsignedIntValue];
  [self.actionService commitNLE:YES];
}
```


Change the canvas of the selected slot to the image type, and specify the canvas of the image path:

```objectivec
- (void)applyCanvasStyleWithValue:(DVEEffectValue *)value {
//Get the slot corresponding to the current timeline
  NLETrackSlot_OC *slot = self.vcContext.mediaContext.mappingTimelineVideoSegment.slot;
  NLESegmentVideo_OC *segment = (NLESegmentVideo_OC *)slot.segment;
  [self p_applyCanvasStyleWithSegment:segment value:value];
}

- (void)p_applyCanvasStyleWithSegment:(NLESegmentVideo_OC *)segment
                value:(DVEEffectValue *)value {
  if (!segment.canvasStyle) {
    segment.canvasStyle = [[NLEStyCanvas_OC alloc] init];
  }
// Set the canvas type
  segment.canvasStyle.canvasType = NLECanvasImage;
  if (!segment.canvasStyle.imageSource) {
    segment.canvasStyle.imageSource = [[NLEResourceNode_OC alloc] init];
  }
  segment.canvasStyle.imageSource.resourceId = value.identifier;
  segment.canvasStyle.imageSource.resourceName = value.name;
//Set the path of the canvas style resource package or the path of the custom style picture
  segment.canvasStyle.imageSource.resourceFile = value.sourcePath;
  [self.actionService commitNLE:YES];
}
```


Change the canvas of the selected slot to the video frame type, and specify the canvas of the blur value:

```objectivec
- (void)applyCanvasBlurWithBlurRadius:(float)blurRadius {
//Get the slot corresponding to the current timeline
  NLETrackSlot_OC *slot = self.vcContext.mediaContext.mappingTimelineVideoSegment.slot;
  NLESegmentVideo_OC *segment = (NLESegmentVideo_OC *)slot.segment;
  [self p_applyCanvasBlurWithSegment:segment blurRadius:blurRadius];
}

- (void)p_applyCanvasBlurWithSegment:(NLESegmentVideo_OC *)segment
             blurRadius:(float)blurRadius {
  if (!segment.canvasStyle) {
    segment.canvasStyle = [[NLEStyCanvas_OC alloc] init];
  }
// Set the canvas type
  segment.canvasStyle.canvasType = NLECanvasVideoFrame;
//Gaussian blur radius,
  segment.canvasStyle.blurRadius = blurRadius;
  [self.actionService commitNLE:YES];
}
```


Change the canvas of the selected slot to the solid color type, which can be taken as the default setting of canvas background:

```objectivec
- (void)p_cancelApplyCanvas {
  NLETrackSlot_OC *slot = self.vcContext.mediaContext.mappingTimelineVideoSegment.slot;
  NLESegmentVideo_OC *segment = (NLESegmentVideo_OC *)slot.segment;
  if (segment) {
//Cancel the canvas operation, here reset a new default canvasStyle
    segment.canvasStyle = [[NLEStyCanvas_OC alloc] init];
  }
  [self.actionService commitNLE:YES];
}
```


Apply the canvas of the currently selected slot to all slots on the main track:

```objectivec
- (void)applyStyCanvasToAllTracks {
//Get the main track
  NLETrack_OC *mainTrack = [self.nleEditor.nleModel nle_getMainVideoTrack];
   
  NSArray<NLETrackSlot_OC *> *slots = [mainTrack slots];
  for (NLETrackSlot_OC *slot in slots) {
    NLESegmentVideo_OC *segment = (NLESegmentVideo_OC *)slot.segment;
//Determine the type of canvas currently applied
    switch (self.canvasSubType) {
      case DVEModuleTypeBackgroundSubTypeCanvasColor: {
//Apply the canvas color and pass in the color value
        [self p_applyCanvasColorWithSegment:segment value:[self.colorContentView currentSelectedColorValue]];
        break;
      }
      case DVEModuleTypeBackgroundSubTypeCanvasStyle: {
//Apply the canvas image and upload it to the canvas picture path
        [self p_applyCanvasStyleWithSegment:segment value:[self.styleContentView currentSelectedValue]];
        break;
      }
      case DVEModuleTypeBackgroundSubTypeCanvasBlur: {
//Apply canvas blur, pass in blur value
        [self p_applyCanvasBlurWithSegment:segment blurRadius:[self.blurContentView currentSelectedBlurRadius]];
        break;
      }
      default:
        break;
    }
  }
}
```


<span id="991d831f"></span>
## Filter

<span id="73adb8d5"></span>
### Add a local filter to a video clip

**Feature**

Adds a local filter to a video clip, that is, to a specific slot.

**API definition**

```objectivec
@interface NLESegmentFilter_OC : NLESegment_OC

/// The filter intensity, brightness, contrast, saturation, sharpening, highlight, and color temperature.
@property (nonatomic, assign) float intensity;

///  The filter name to be displayed.
@property (nonatomic, copy) NSString *filterName;

///  The filter resource.
@property (nonatomic, copy) NLEResourceNode_OC *effectSDKFilter;
```


**Sample code**

```objectivec
NLEResourceNode_OC *resFilter = [[NLEResourceNode_OC alloc] init];
resFilter.resourceId = info.featureID;
resFilter.resourceFile = info.path;
resFilter.resourceType = type;
resFilter.resourceTag = NLEResourceTagAmazing;
   
NLESegmentFilter_OC *segFilter = [[NLESegmentFilter_OC alloc] init];
[segFilter setEffectSDKFilter:resFilter];
[segFilter setFilterName:name];
[segFilter setIntensity:info.intensity];
   
NLEFilter_OC *filter = [[NLEFilter_OC alloc] init];
[filter setSegmentFilter:segFilter];
   
[selectSlot addFilter:filter];
```


<span id="ae2c48b9"></span>
### Add a filter to the entire canvas

**Feature**

Adds a filter to the entire canvas. The filter has an independent track and takes effect for all video clips and overlays within its effective period.

Click the filter button in the bottom bar to set the global filter and generate a filter track slot with a length of 3 seconds. A filter slot allows one filter effect to be set, allowing multiple filter slots to perform effect superposition.

**Add filter**: Create and add a filter effect to the filter slot.

**Delete**: Delete the adjustment slot selected in the track.

**Switch filter**: Switch to another filter effect.


|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/946da4e18a2d4f02981a55161b776279~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3defebd6103046648232a57a7117cbbe~tplv-goo7wpa0wc-image.image) </span> |
|---|---|


**Structural adjustment**

The structure of the filter and adjustment track is defined as follows:

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/7390ea7f10a741d8801075cc44929b28~tplv-em5hxbkur4-noop.image) </span>


* track \-\-\> slot \-\-\> filters( NLEFilter\-\-\> mainSegment = NLESegmentFilter() )

* Filter, adjustment track names are recorded on the filterName field of mainSegment in the slot.

* The items of the Filter array are NLEFilter type. NLEFilter has a segment under NLESegmentFilter.

* Related fields of NLESegmentFilter for filter and adjustment:

   * "intensity" is recorded in fields of intensity,

   * "adjustment" and "adjustment name" are recorded in fields of filterName.

   * Material resource paths are recorded in the fields of resourceFile of the effectSDKFilter.

* An adjustment slot has several NLEFilters, representing multiple adjustment options (Brightness, hue, exposure, etc. are all in the same filter.)

* One NLEFilter for one filter slot, representing a global filter.


**API definition**

```objectivec
@interface NLESegmentFilter_OC : NLESegment_OC

///  The filter intensity, brightness, contrast, saturation, sharpening, highlight, and color temperature.
@property (nonatomic, assign) float intensity;

///  The filter name to be displayed.
@property (nonatomic, copy) NSString *filterName;

///  The filter resource.
@property (nonatomic, copy) NLEResourceNode_OC *effectSDKFilter;
```


Adjustment Filters are stored in the Filter array of NLETrackSlot. The Filter array is an attribute of NLETrackSlot. A slot can store multiple adjustment Filters. However, since the global filter slot has only one filter effect, only one Filter is stored in the Filter array.

**Relevant interfaces of NLETrackSlot are defined as follows:** 

```objectivec
@interface NLETrackSlot_OC : NLETimeSpaceNode_OC
@property (nonatomic, strong) NLESegment_OC* segment;
///Filters, adjustments
- (NSMutableArray<NLEFilter_OC*>*)getFilter;
- (void)addFilter:(NLEFilter_OC *)filter;
- (void)clearFilter;
- (void)removeFilter:(NLEFilter_OC *)filter;
@end
```


**Sample code**

```objectivec
NLEModel_OC *model = [self.vcContext.mediaContext.editor getModel];
NLETrack_OC *filterTrack = [[NLETrack_OC alloc] init];

NLETrack_OC *mainTrack = [model nle_getMainVideoTrack];
NLETrackSlot_OC *trackSlot = [[NLETrackSlot_OC alloc] init];

NLEResourceNode_OC *resource = [[NLEResourceNode_OC alloc] init];
//  The resource ID, which is required for downloading the resource. It can be left unspecified.
resource.resourceId = info.featureID;
resource.resourceFile = info.path;
resource.resourceType = NLEResourceTypeFilter;
// Indicates that the resource format is Amazing Feature.
resource.resourceTag = NLEResourceTagAmazing;
   
NLESegmentFilter_OC *segFilter = [[NLESegmentFilter_OC alloc] init];
[segFilter setEffectSDKFilter:resource];
[segFilter setFilterName:name];
[segFilter setIntensity:info.intensity];

[trackSlot setSegment:segFilter];
trackSlot.startTime = kCMTimeZero;
trackSlot.duration = [mainTrack getMaxEnd];
[filterTrack addSlot:trackSlot];
   
[model addTrack:filterTrack];
```



* Add or update filter slots

   If the user clicks "Add" without selecting a filter track, a new filter track will be added.


```objectivec
///Add a filter to the global filter slot
/// @param info build filter information Model
///@param name Filter name
/// @param resourceTag resource adjustment type（amazing or normal）
/// @param commit submit NLE（undo after submission）
- (void)addGlobalNLEFilter:(DVEFilterEditorModel*)info
                      name:(NSString *)name
               resourceTag:(NLEResourceTag)resourceTag
                needCommit:(BOOL)commit{
   
  NSString *relativePath = [self.draftService copyResourceToDraft:[NSURL fileURLWithPath:info.resPath] resourceType:NLEResourceTypeFilter];
   
  NLEModel_OC *model = [self.vcContext.mediaContext.editor getModel];

  NLEResourceNode_OC *resource = [[NLEResourceNode_OC alloc] init];
  resource.resourceId = info.identifier;
  resource.resourceFile = relativePath;
  resource.resourceType = NLEResourceTypeFilter;
  resource.resourceTag = resourceTag;
   
  NLESegmentFilter_OC *segFilter = [[NLESegmentFilter_OC alloc] init];
  [segFilter setEffectSDKFilter:resource];
  [segFilter setFilterName:name];
  [segFilter setIntensity:info.intensity];
   
  NLEFilter_OC *filter = [[NLEFilter_OC alloc] init];
  filter.segmentFilter = segFilter;
   
  NLESegmentFilter_OC *mainSegFilter = [[NLESegmentFilter_OC alloc] init];
  mainSegFilter.filterName = name;

  NLETrackSlot_OC *trackSlot = [[NLETrackSlot_OC alloc] init];
  [trackSlot setSegment:mainSegFilter];
  [trackSlot addFilter:filter];
  trackSlot.startTime = self.vcContext.mediaContext.currentTime;
  trackSlot.duration = CMTimeMake(3 * USEC_PER_SEC, USEC_PER_SEC);
//Find a filter track that has a space to insert a new slot
  NLETrack_OC *filterTrack = nil;
  NSArray<NLETrack_OC *> *trackArray = [model nle_allTracksOfType:NLETrackFILTER resourceType:NLEResourceTypeFilter];
  for (NLETrack_OC *track in trackArray) {
    BOOL isContainSlot = YES;
    for (NLETrackSlot_OC *slot in track.slots) {
//If there is an overlap with the slot on the track, the isContainSlot is set to NO
      if (CMTimeRangeContainsTime(trackSlot.nle_targetTimeRange, slot.startTime) || CMTimeRangeContainsTime(trackSlot.nle_targetTimeRange, slot.endTime) ||
        CMTimeRangeContainsTime(slot.nle_targetTimeRange, trackSlot.startTime) ||
        CMTimeRangeContainsTime(slot.nle_targetTimeRange, trackSlot.endTime)) {
        isContainSlot = NO;
        break;
      }
    }
    if (isContainSlot == YES) {
      filterTrack = track;
      break;
    }
  }
//If no track can be found to insert a slot, create a new track
  if (!filterTrack) {
    filterTrack = [[NLETrack_OC alloc] init];
    filterTrack.extraTrackType = NLETrackFILTER;
    filterTrack.nle_extraResourceType = NLEResourceTypeFilter;
    [model addTrack:filterTrack];
  }
  [filterTrack addSlot:trackSlot];
  [self.actionService commitNLE:commit];
  self.vcContext.mediaContext.selectFilterSegment = trackSlot;
}
```


If the user clicks "Add" while selecting a filter slot, a filter type will be changed or switched.

```objectivec
///Update the intensity of the global filter
/// @param identifier unique identifier for filters
///@param intensity filter intensity value
/// @param commit submit NLE（undo after submission）
- (void)updateGlobalNLEFilter:(NSString *)identifier 
                    intensity:(CGFloat)intensity 
                   needCommit:(BOOL)commit {
  if (!identifier) return;

  NLEModel_OC *model = [self.vcContext.mediaContext.editor getModel];
  if(model.getTracks.count == 0) return;
   
  NLETrack_OC *filterTrack = nil;
  for (NLETrack_OC *track in [model getTracks]) {
    if ([track getTrackType] == NLETrackFILTER) {
      filterTrack = track;
      break;
    }
  }
  if (!filterTrack) return;
   
  for (NLETrackSlot_OC *slot in filterTrack.slots) {
    NLESegmentFilter_OC *segFilter = [slot getFilter].firstObject.segmentFilter;
    NLEResourceNode_OC *resFilter = [segFilter getResNode];
//If it is an existing filter Filter, update the intensity
    if ([resFilter.resourceId isEqualToString:identifier]) {
      [segFilter setIntensity:intensity];
      break;
    }
  }
  [self.actionService commitNLE:commit];
}

///Switch to another global filter
/// @param info build filter information Model
///@param name filter name
/// @param resourceTag resource adjustment type（amazing or normal）
/// @param commit submit NLE（undo after submission）
- (void)changeGlobalNLEFilter:(DVEFilterEditorModel*)info 
                         name:(NSString *)name
                  resourceTag:(NLEResourceTag)resourceTag
                   needCommit:(BOOL)commit{
  NLETrackSlot_OC *selectSlot = self.vcContext.mediaContext.selectFilterSegment;
  if (!selectSlot) return;
   
  NSString *relativePath = [self.draftService copyResourceToDraft:[NSURL fileURLWithPath:info.resPath] resourceType:NLEResourceTypeFilter];

  NLEResourceNode_OC *resource = [[NLEResourceNode_OC alloc] init];
  resource.resourceId = info.identifier;
  resource.resourceFile = relativePath;
  resource.resourceType = NLEResourceTypeFilter;
  resource.resourceTag = resourceTag;
   
  NLESegmentFilter_OC *segFilter = [[NLESegmentFilter_OC alloc] init];
  [segFilter setEffectSDKFilter:resource];
  [segFilter setFilterName:name];
  [segFilter setIntensity:info.intensity];
   
  NLEFilter_OC *filter = [[NLEFilter_OC alloc] init];
  filter.segmentFilter = segFilter;
   
  NLESegmentFilter_OC *mainSegment = (NLESegmentFilter_OC *)selectSlot.segment;
  mainSegment.filterName = name;
//Clear the original filter Filter, set a new filter effect
  [selectSlot clearFilter];
  [selectSlot addFilter:filter];
  [self.actionService commitNLE:commit];
}
```



* Delete global filter slot


```objectivec
///Delete the global filter Filter
/// @param identifier unique identifier for filters
/// @param commit submit NLE（undo after submission）
- (void)deleteGlobalNLEFilter:(NSString *)identifier 
                   needCommit:(BOOL)commit {
  if (!identifier) return;
  NLETrackSlot_OC *slot = self.vcContext.mediaContext.selectFilterSegment;
  if (!slot) return;

  NLEModel_OC *model = [self.vcContext.mediaContext.editor getModel];
  NLETrack_OC *filterTrack = [model trackContainSlotId:slot.nle_nodeId];
  if (!filterTrack) return;
   
  [filterTrack removeSlot:slot];
  if (filterTrack.slots.count == 0) {
    [model removeTrack:filterTrack];
  }
  [self.actionService commitNLE:commit];
}
```


<span id="9682a96d"></span>
## Adjustment

<span id="85c805af"></span>
### Adjust a video clip

**Feature**

Adjusts a specific video clip, that is, a specific slot.

**API definition**

```objectivec
@interface NLESegmentFilter_OC : NLESegment_OC

///  The filter intensity, brightness, contrast, saturation, sharpening, highlight, and color temperature.
@property (nonatomic, assign) float intensity;

///  The filter name to be displayed.
@property (nonatomic, copy) NSString *filterName;

///  The filter resource.
@property (nonatomic, copy) NLEResourceNode_OC *effectSDKFilter;
```


<span id="ae0fa6c9"></span>
### Adjust the entire canvas

**Feature**

Adjusts the entire canvas. The adjustment has an independent track and takes effect for all video clips and overlays within its effective period.

Click the adjustment button in the bottom bar to set the global adjustment and generate an adjustment track slot with a length of 3 seconds. An adjustment slot allows multiple adjustment effects to be set, allowing multiple adjustment slots to perform effect superposition.

Add adjustment: Create a new adjustment slot and set the adjustment effect.

Adjustment: Update the adjustment effect of the existing adjustment slot or add a new adjustment effect.

Delete: Delete the adjustment slot selected in the track.

Reset: Reset the parameters of all effects in the adjustment.


|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3ae7cac64c364019970553c18eb47348~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/70f87598ba584dde909c0ce14fcfdc39~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/173715e5902441b18a28e6f0ab963045~tplv-goo7wpa0wc-image.image) </span> |
|---|---|---|


**Structural Adjustment**

The structure of the filter and adjustment track is defined as follows:

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/c7b17bb361cf43e492241c6472e6b615~tplv-em5hxbkur4-noop.image) </span>


* track \-\-\> slot \-\-\> filters( NLEFilter\-\-\> mainSegment = NLESegmentFilter() )

* Filter, adjustment track names are recorded on the filterName field of mainSegment in the slot

* The items in the Filter array are NLEFilter type. NLEFilter has a segment under NLESegmentFilter.

* Related fields of NLESegmentFilter for filter and adjustment:

   * "intensity" is recorded in fields of intensity,

   * "adjustment" and "adjustment name" are recorded in fields of filterName.

   * Material resource paths are recorded in the fields of resourceFile of the effectSDKFilter.

* An adjustment slot has several NLEFilters, representing multiple adjustment options (Brightness, hue, exposure, etc. are all in the same filter.)

* One NLEFilter for one filter slot, representing a global filter.


**API definition**

```objectivec
@interface NLESegmentFilter_OC : NLESegment_OC

///  The filter intensity, brightness, contrast, saturation, sharpening, highlight, and color temperature.
@property (nonatomic, assign) float intensity;

///  The filter name to be displayed.
@property (nonatomic, copy) NSString *filterName;

///  The filter resource.
@property (nonatomic, copy) NLEResourceNode_OC *effectSDKFilter;
```


Adjustment Filters are stored in the Filter array of NLETrackSlot. The Filter array is an attribute of NLETrackSlot. A slot can store multiple adjustment Filters.

**Relevant interfaces of NLETrackSlot** are defined as follows:

```objectivec
@interface NLETrackSlot_OC : NLETimeSpaceNode_OC
@property (nonatomic, strong) NLESegment_OC* segment;
///Filters, adjustments
- (NSMutableArray<NLEFilter_OC*>*)getFilter;
- (void)addFilter:(NLEFilter_OC *)filter;
- (void)clearFilter;
- (void)removeFilter:(NLEFilter_OC *)filter;
@end
```


**Sample code**

```objectivec
NLEModel_OC *model = [self.vcContext.mediaContext.editor getModel];
NLETrack_OC *filterTrack = [[NLETrack_OC alloc] init];

NLETrack_OC *mainTrack = [model nle_getMainVideoTrack];
NLETrackSlot_OC *trackSlot = [[NLETrackSlot_OC alloc] init];

NLEResourceNode_OC *resource = [[NLEResourceNode_OC alloc] init];
//  The resource ID, which is required for downloading the resource. It can be left unspecified.
resource.resourceId = info.featureID;
resource.resourceFile = info.path;
resource.resourceType = NLEResourceTypeAdjust;
// Indicates that the resource format is Amazing Feature.
resource.resourceTag = NLEResourceTagAmazing;
   
NLESegmentFilter_OC *segFilter = [[NLESegmentFilter_OC alloc] init];
[segFilter setEffectSDKFilter:resource];
[segFilter setFilterName:name];
[segFilter setIntensity:info.intensity];

[trackSlot setSegment:segFilter];
trackSlot.startTime = kCMTimeZero;
trackSlot.duration = [mainTrack getMaxEnd];
[filterTrack addSlot:trackSlot];
   
[model addTrack:filterTrack];
```



* Add or update adjustment slots

   If the user clicks "Add" without selecting a global filter or adjustment track, a new filter or adjustment track will be added.


```objectivec
///Add adjustment: Create a new adjustment slot and set the adjustment effect.
/// @param info information adjustment Model
/// @param name resource adjustment name
/// @param resourceTag resource adjustment type（amazing or normal）
/// @param commit submit NLE（you can undo it after submission）
- (void)addGlobalNLEFilterForNewSlot:(DVERegulateEditModel*)info
                                name:(NSString *)name
                         resourceTag:(NLEResourceTag)resourceTag
                          needCommit:(BOOL)commit{
  NSString *relativePath = [self.draftService copyResourceToDraft:[NSURL fileURLWithPath:info.resPath] resourceType:NLEResourceTypeAdjust];
  NLEModel_OC *model = [self.vcContext.mediaContext.editor getModel];

  NLEResourceNode_OC *resource = [[NLEResourceNode_OC alloc] init];
  resource.resourceId = info.identifier;
  resource.resourceFile = relativePath;
  resource.resourceType = NLEResourceTypeAdjust;
  resource.resourceTag = resourceTag;
   
  NLESegmentFilter_OC *segFilter = [[NLESegmentFilter_OC alloc] init];
  [segFilter setEffectSDKFilter:resource];
  [segFilter setFilterName:name];
  [segFilter setIntensity:info.intensity];
   
  NLEFilter_OC *filter = [[NLEFilter_OC alloc] init];
  [filter setSegmentFilter:segFilter];
   
  NLESegmentFilter_OC *mainSegFilter = [[NLESegmentFilter_OC alloc] init];
  mainSegFilter.filterName = [self newNameForAdjustSlot];
   
  NLETrackSlot_OC *trackSlot = [[NLETrackSlot_OC alloc] init];
  trackSlot = [[NLETrackSlot_OC alloc] init];
  trackSlot.startTime = self.vcContext.mediaContext.currentTime;
  trackSlot.duration = CMTimeMake(3 * USEC_PER_SEC, USEC_PER_SEC);
  [trackSlot addFilter:filter];
  [trackSlot setSegment:mainSegFilter];
  
//Find a filter track that has a space to insert a new slot
  NLETrack_OC *filterTrack = nil;
  NSArray<NLETrack_OC *> *trackArray = [model nle_allTracksOfType:NLETrackFILTER resourceType:NLEResourceTypeAdjust];
  for (NLETrack_OC *track in trackArray) {
    BOOL isContainSlot = YES;
    for (NLETrackSlot_OC *slot in track.slots) {
//If there is an overlap with the slot on the track, the isContainSlot is set to NO
      if (CMTimeRangeContainsTime(trackSlot.nle_targetTimeRange, slot.startTime) || CMTimeRangeContainsTime(trackSlot.nle_targetTimeRange, slot.endTime) ||
        CMTimeRangeContainsTime(slot.nle_targetTimeRange, trackSlot.startTime) ||
        CMTimeRangeContainsTime(slot.nle_targetTimeRange, trackSlot.endTime)) {
        isContainSlot = NO;
        break;
      }
    }
    if (isContainSlot == YES) {
      filterTrack = track;
      break;
    }
  } 
//If no track can be found to insert a slot, create a new track
  if (!filterTrack) {
    filterTrack = [[NLETrack_OC alloc] init];
    filterTrack.extraTrackType = NLETrackFILTER;
    filterTrack.nle_extraResourceType = NLEResourceTypeAdjust;
    [model addTrack:filterTrack];
  }
  [filterTrack addSlot:trackSlot];
   
  [self.actionService commitNLE:commit];
  self.vcContext.mediaContext.selectFilterSegment = trackSlot;
}
```


If the user clicks "Add" while selecting an adjustment slot, an adjustment effect will be changed or added.

```objectivec
///Update the effect intensity of the existing adjustment slot.
/// @param identifier unique identifier for resource adjustment 
/// @param intensity adjust resource intensity
/// @param commit submit NLE（undo after submission）
- (void)updateGlobalNLEFilter:(NSString *)identifier
                    intensity:(CGFloat)intensity
                   needCommit:(BOOL)commit
{
  if (!identifier) return;
  NLETrackSlot_OC *slot = self.vcContext.mediaContext.selectFilterSegment;
  if (!slot) return;
  for (NLEFilter_OC *filter in [slot getFilter]) {
    NLESegmentFilter_OC *segFilter = filter.segmentFilter;
    NLEResourceNode_OC *resFilter = [segFilter getResNode];
//Find the corresponding adjustment Filter and update its intensity
    if ([resFilter.resourceId isEqualToString:identifier]) {
      [segFilter setIntensity:intensity];
    }
  }
  [self.actionService commitNLE:commit];
}

///Add an adjustment effect to the existing adjustment slot.
/// @param info information adjustment Model
/// @param name resource adjustment name
/// @param resourceTag resource adjustment type（amazing or normal）
///@param slot selected adjustment slot
/// @param commit submit NLE（undo after submission）
- (void)addGlobalNLEFilterForExistSlot:(DVERegulateEditModel*)info
                 name:(NSString *)name
              resourceTag:(NLEResourceTag)resourceTag
             forSelectSlot:(NLETrackSlot_OC *)slot
              needCommit:(BOOL)commit{
   
  NSString *relativePath = [self.draftService copyResourceToDraft:[NSURL fileURLWithPath:info.resPath] resourceType:NLEResourceTypeAdjust];
  NLEResourceNode_OC *resource = [[NLEResourceNode_OC alloc] init];
  resource.resourceId = info.identifier;
  resource.resourceFile = relativePath;
  resource.resourceType = NLEResourceTypeAdjust;
  resource.resourceTag = resourceTag;
   
  NLESegmentFilter_OC *segFilter = [[NLESegmentFilter_OC alloc] init];
  [segFilter setEffectSDKFilter:resource];
  [segFilter setFilterName:name];
  [segFilter setIntensity:info.intensity];
   
  NLEFilter_OC *filter = [[NLEFilter_OC alloc] init];
  [filter setSegmentFilter:segFilter];
   
///Add an adjustment effect to the existing adjustment slot.
  [slot addFilter:filter];
   
  [self.actionService commitNLE:commit];
  self.vcContext.mediaContext.selectFilterSegment = slot;
}
```



* Delete Global Adjustment Slot


```objectivec
- (void)deleteSelectRegulateSegment
{
  if (self.vcContext.mediaContext.selectFilterSegment) {
    NLETrackSlot_OC *regulateSlot = self.vcContext.mediaContext.selectFilterSegment;
    NLEModel_OC *model = [self.vcContext.mediaContext.editor getModel];
    NLETrack_OC *regulateTrack = [model trackContainSlotId:regulateSlot.nle_nodeId];
    [regulateTrack removeSlot:regulateSlot];
    
//After deleting the slot, if the track has no slot, delete the track
    if (regulateTrack.slots.count == 0) {
      [model removeTrack:regulateTrack];
    }
    [self.actionService commitNLE:YES];
  }
  [self.vcContext.playerService seekToTime:self.vcContext.mediaContext.currentTime isSmooth:NO];
}
```



* Reset all parameters


```objectivec
///Reset all current adjustment parameters
/// @param commit submit NLE（undo after submission）
- (void)resetAllRegulateNeedCommit:(BOOL)commit
{
  NLETrackSlot_OC *slot = nil;
  if (self.vcContext.mediaContext.selectBlendVideoSegment) {
    slot = self.vcContext.mediaContext.selectBlendVideoSegment;
  } else if (self.vcContext.mediaContext.selectMainVideoSegment) {
    slot = self.vcContext.mediaContext.selectMainVideoSegment;
  } else if(self.vcContext.mediaContext.selectFilterSegment) {
    slot = self.vcContext.mediaContext.selectFilterSegment;
  }
  if (slot) {
    NSArray<NLEFilter_OC*>* filters = [slot getFilter];
    for (NLEFilter_OC *filter in filters) {
      NLESegmentFilter_OC *segFilter = filter.segmentFilter;
      [segFilter setIntensity:0];
    }
  }
  [self.actionService commitNLE:commit];
}
```


<span id="fe50d75a"></span>
## Undo and redo

**Feature**

Determines whether undo and redo are supported, and performs undo and redo. To allow undo on a specific operation or a series of operations, call both the commit and done methods. What is the difference between commit and done? After a model is modified, you can call the commit method to request the NLE system to run the diff algorithm for effect updates. You can call the commit method multiple times. The done method saves all modifications made between the last and current calls of the done method. Therefore, you can call the undo method only after the done method is completed.

**API definition**

```objectivec
@interface NLEEditor_OC : NSObject
/// git reset HEAD^
///  Undo the last operation. If YES is returned, the undo is successful.
- (BOOL)undo;

///  Redo the last operation. If YES is returned, the redo is successful.
- (BOOL)redo;
```


**Sample code**

```objectivec
// undo
if ([self.nle.editor canUndo]) {
    [self.nle.editor undo];
}

//  redo
if ([self.nle.editor canRedo]) {
    [self.nle.editor redo];
}
```


**Note**

While you drag the slider to adjust intensity, the system calls only the commit method to update the effect. When you drop the slider or the sliding ends, the system calls the done method to save the final status.

<span id="a955fc75"></span>
## Draft

**Feature**

Saves model data and redo/undo data so that you can directly perform undo and redo when restoring data from the draft.

**API definition**

```objectivec
@interface NLEEditor_OC : NSObject
/**
 * Store information and obtain a JSON string.
 */
- (NSString *)store;
```


**Sample code**

```objectivec
NSString *json = [self.nle.editor store];
NSError *error;
[json writeToFile:self.cacheFile atomically:YES encoding:NSUTF8StringEncoding error:&error]
```


<span id="2f4fb6d0"></span>
## Text template

**Feature**

Adds a text template to a video. The template contains animations. You can modify paragraphs in the template, and scale, translate, or rotate the template.

The following shows the configuration file **text_template_hot.json** of a text template:

```JSON
{
    "name":" XXX",   // Template name.
    "path": "template/ XXX",    //Template path.
    "icon":"template/94c2b3f17183adf5db9adb74ed92858f.gif",   // Template thumbnail.
    "dep": [{   // Resources the template depends on.
        "type": "fonts",  
        "resourceId": "6740499317733200388",
        "path": "template/6740499317733200388/DFPLiJinHei.TTF"
    }, {
        "type": "fonts",
        "resourceId": "6852190696930021902",
        "path": "template/6852190696930021902/FZLiuBingSenLiShu.TTF"
    }]
}
```


**API definition**

**NLESegmentTextTemplate_OC** describes content of the text template.

```objectivec
@interface NLESegmentTextTemplate_OC : NLESegment_OC
///  The resource object.
@property (nonatomic, strong) NLEResourceNode_OC* effectSDKFile;

///  The font and sticker resources used in the text template.
@property (nonatomic, copy) NSArray<NLEResourceNode_OC *> *fontResList;

///  Text assets of the text template.
@property (nonatomic, copy) NSArray<NLETextTemplateClip_OC *> * _Nullable textClips;

///  The resource type.
- (NLEResourceType)getType;
///  Deep clone.
- (NLESegmentTextTemplate_OC *)deepClone;

///Add text.
/// You need to manually add text content.
/// @param textClip: the content of the text.
- (void)addTextClip:(NLETextTemplateClip_OC *)textClip;

/// Delete all text asset.
- (void)clearTextClips;

/// Delete the specified text asset.
/// @param textClip: the content of the text.
- (void)removeTextClip:(NLETextTemplateClip_OC *)textClip;
@end
```



* Add a sticker


```objectivec
- (NSString*)addTemplateWithPath:(NSString *)path
          depResModels:(NSArray<DVETextTemplateDepResourceModelProtocol> *)depResModels
           needCommit:(BOOL)commit
           completion:(nullable void(^)(void))completion {
  NSInteger resDuration = 3;
  //  The resource.
  NLEResourceNode_OC *resEffect = [[NLEResourceNode_OC alloc] init];
  resEffect.resourceId = [[NSUUID UUID] UUIDString];
  resEffect.resourceFile = path;
  resEffect.resourceType = NLEResourceTypeTextTemplate;
  resEffect.resourceTag = NLEResourceTagNormal;
  resEffect.duration = CMTimeMakeWithSeconds(resDuration, USEC_PER_SEC);
   
  //  Add dependencies for the resource: font.
  NSMutableArray *mFonts = [[NSMutableArray alloc] initWithCapacity:depResModels.count];
  for (id<DVETextTemplateDepResourceModelProtocol> m in depResModels) {
    NLEResourceNode_OC *tmp = [[NLEResourceNode_OC alloc] init];
    tmp.resourceId = m.resourceId;
    tmp.resourceFile = m.path;
    [mFonts addObject:tmp];
  }
   
  //  Initialize the segment.
  NLESegmentTextTemplate_OC *segment = [[NLESegmentTextTemplate_OC alloc] init];
  [segment setEffectSDKFile:resEffect];
  segment.fontResList = mFonts;
   
  //  Initialize the slot.
  CMTime currentTime = self.vcContext.mediaContext.currentTime;
  CMTime startTime = CMTimeMake(CMTimeGetSeconds(currentTime) * USEC_PER_SEC, USEC_PER_SEC);
  NSInteger endSecond = MIN((CMTimeGetSeconds(currentTime) + resDuration), CMTimeGetSeconds(self.vcContext.mediaContext.duration));
  CMTime endTime = CMTimeMake(endSecond * USEC_PER_SEC, USEC_PER_SEC);
   
  int32_t layer = (int32_t)([[self.vcContext.mediaContext.editor getModel] nle_getMaxEffectLayer] + 1);
   
  NLETrackSlot_OC *textSlot = [[NLETrackSlot_OC alloc] init];
  textSlot.segment = segment;
  textSlot.startTime = startTime;
  textSlot.endTime = endTime;
  textSlot.duration = CMTimeMakeWithSeconds(resDuration, USEC_PER_SEC);
  textSlot.layer = MAX(0, layer);
  textSlot.name = segment.effectSDKFile.resourceId;
  [textSlot setSegmentTextTemplate:segment];
   
    return [self addTemplateWithSeg:segment
                    slot:textSlot
                 needCommit:commit
                 completion:completion];
}
```



* Copy text

   Note: The **deepClone**: method is used


```objectivec
- (NSString *)copyTextTemplateWithIsCommit:(BOOL)commit {
  NLETrackSlot_OC* slot = self.vcContext.mediaContext.selectTextSlot;
  if (!slot) {
    return nil;
  }
  if (![slot.segment isKindOfClass:[NLESegmentTextTemplate_OC class]]) {
    return nil;
  }
   
  //  The track logic.
  NLETrackSlot_OC *textSlot = [slot deepClone:YES];
  //  Shift rightward.
  float offset = 0.1f;
  textSlot.transformX = slot.transformX + offset;
     
  return [self addTemplateWithSeg:(NLESegmentTextTemplate_OC*)textSlot.segment
                slot:textSlot
             needCommit:commit
             completion:nil];
}
```


Call the following method to add or copy a template:

```objectivec
///  Associate a segment with a slot and call the NLE API.
- (NSString *)addTemplateWithSeg:(NLESegmentTextTemplate_OC *)segment
              slot:(NLETrackSlot_OC *)slot
           needCommit:(BOOL)commit
           completion:(nullable void(^)(void))completion {
  if (!segment || !slot) {
    return nil;
  }

  NLEModel_OC *model = [self.vcContext.mediaContext.editor getModel];
  NLETrack_OC *textTrack = [[NLETrack_OC alloc] init];
  textTrack.extraTrackType = NLETrackSTICKER;
  textTrack.nle_extraResourceType = NLEResourceTypeTextTemplate;
  textTrack.layer = (int)([model nle_getMaxTrackLayer:NLETrackSTICKER] + 1);
  [model addTrack:textTrack];
   
  self.trackSlot = slot;
  [textTrack addSlot:slot];
   
  [self.vcContext commitNLE:NO];
   
  //  Show the preview window without closing the template panel.
  [DVEComponentViewManager sharedManager].enable = NO;
  self.vcContext.mediaContext.selectTextSlotAtCurrentTime = slot;
  [DVEComponentViewManager sharedManager].enable = YES;
  //  Preview the template.
  [self.vcContext.nle setStickerPreviewMode:slot previewMode:4];
   
  /*
   If the text template exceeds the duration of the video clip on the main track, updatevideoData will be triggered. The VE SDK will
   modify the ID of infosticker. The internal sticker ID update will be added to the stickerRecoverEvent
   block to inform you. However, this occurs in the callback after updatevideoData is completed.
   Therefore, you are unable to obtain the text template information immediately after you call the commit method.
   */
  @weakify(self);
  [self.vcContext.editManager updateCurVideoDataWithCompleteBlock:^(NSError * _Nullable error) {
    @strongify(self);
    dispatch_async(dispatch_get_main_queue(), ^{
      //  Obtain real-time data.
      NLETextTemplateInfo *info = [self.vcContext.mediaContext.nle textTemplateInfoForSlot:slot];
      segment.textClips = nil; // clear
      for (NLETextTemplateSubInfo *sub in info.textInfos) {
        [self p_addText:sub toTextTemplate:segment];
      }
       
      [self.vcContext commitNLE:YES];
      if (completion) {
        completion();
      }
    });
  }];
   
  return slot.name;
}

- (void)p_addText:(NLETextTemplateSubInfo *)textInfo
  toTextTemplate:(NLESegmentTextTemplate_OC *)textTemplate {
    NLETextTemplateClip_OC *clip_oc = [[NLETextTemplateClip_OC alloc] init];
    clip_oc.content = textInfo.text;
    clip_oc.index = textInfo.index;
    [textTemplate addTextClip:clip_oc];
}
```



* Modify text content

   Note: The template contains multiple paragraphs. Therefore, when you modify text, specify a corresponding index.


```objectivec
- (void)updateText:(NSString *)text atIndex:(NSUInteger)index isCommit:(BOOL)commit {
    NLETrackSlot_OC *slot = self.vcContext.mediaContext.selectTextSlot;
    if (!slot) return;
     
    if (![slot.segment isKindOfClass:[NLESegmentTextTemplate_OC class]]) {
    return;
    }
    
    NLESegmentTextTemplate_OC *textTemplate = (NLESegmentTextTemplate_OC *)slot.segment;
    
    [self p_updateText:text atIndex:index forTextTemplate:textTemplate];
    [self.vcContext commitNLE:commit];
    //  Preview the template.
    [self.vcContext.nle setStickerPreviewMode:slot previewMode:4];
}

- (void)p_updateText:(NSString *)text
       atIndex:(NSUInteger)index
   forTextTemplate:(NLESegmentTextTemplate_OC *)textTemplate {
    NSArray *clips = [textTemplate textClips];
    for (NLETextTemplateClip_OC *textClip in clips) {
        if (textClip.index == index) {
          textClip.content = text;
          break;
        }
    }
}
```



* Split text

   This is similar to splitting text.


```objectivec
- (void)splitTextTemplate:(id<DVEBarComponentProtocol>)component {
  DVELogInfo(@"split one text template track");
  NLETrackSlot_OC* slot = self.vcContext.mediaContext.selectTextSlot;
  BOOL res = [self canSplitWithSlot:slot];
  if (!res) {
    return;
  }
   
  NSString *newSegId = [self.vcContext.textEditor splitTextForSlot:slot];
  [self.parentVC.stickerEditAdatper addEditBoxForSticker:newSegId isText:YES];
}

///  Split text.
/// @param slot: the slot in which the text is to be split.
- (NSString*)splitTextForSlot:(NLETrackSlot_OC*)slot
{
    if (!slot) { return nil; }
    //  Add a new slot and modify the end time of the old slot.
    NLETrackSlot_OC* newSlot = [slot deepClone];
    newSlot.name = @(newSlot.getID).stringValue;
    slot.endTime = self.vcContext.mediaContext.currentTime;
    newSlot.startTime = self.vcContext.mediaContext.currentTime;
    
    NLEModel_OC *model = [self.vcContext.mediaContext.editor getModel];
    NLETrack_OC *textTrack = [model trackContainSlotId:slot.nle_nodeId];
    [textTrack addSlot:newSlot];
    
    [self.vcContext commitNLE:YES];
    self.vcContext.mediaContext.selectTextSlotAtCurrentTime = newSlot;
    
    return [newSlot nle_nodeId];
}
```



* Delete a sticker


```objectivec
[[self.vcContext.mediaContext.editor getModel] nle_removeSlots:@[segmentId] inTrackType:NLETrackSTICKER];
[self.vcContext commitNLE:YES];
self.vcContext.mediaContext.selectTextSlot = nil;
```


<span id="78a5895b"></span>
## Text animation

**Feature**

Adds an animation to text. To add an animation to text, tap **Add Text** to go to the text input screen and tap the **Animation** tab to go to the animation settings screen.

Animation type: You can add an In, Out, or loop animation.

Animations: You can select a specific animation from the list.

Animation duration: You can control the animation duration with a scroll bar.

**API definition**


* Set an animation


```objectivec
@interface NLESegmentSticker_OC : NLESegment_OC
```


/// Sticker animation

@property (nonatomic, strong) NLEStyStickerAnimation_OC \*stickerAnimation;

```Plain Text
@end
```


```objectivec
@interface DVEVCContext : NSObject
```



* (void)commitNLE:(BOOL)commit;


```Plain Text
@end
```



* Preview the animation


```objectivec
@interface NLEInterface_OC : NSObject
```


/// Set the preview mode of the animation.

/// If 0 is returned, the setting is successful. If any other value is returned, the setting fails.

/// @param slot NLETrackSlot: the sticker slot.

/// @param previewMode: the preview mode. The value 0 specifies to disable the preview mode. The value 1 specifies to preview the In animation. The value 2 specifies to preview the Out animation. The value 3 specifies to preview the loop animation. The value 4 specifies to preview the entire sticker.


* (NSInteger)setStickerPreviewMode:(NLETrackSlot_OC \*)slot previewMode:(int)previewMode;


```Plain Text
@end
```

**Sample code**

   *   Create a view 

```objectivec
- (DVETextAnimationView *)textAnimationView {
  if (!_textAnimationView) {
    _textAnimationView = [[DVETextAnimationView alloc] init];
    _textAnimationView.frame = CGRectMake(0, 0, VE_SCREEN_WIDTH, 171 + 120);
    _textAnimationView.backgroundColor = [UIColor clearColor];
    _textAnimationView.delegate = self;
  }
  return _textAnimationView;
}
```


   * Add a view

```objectivec
[self.contentView addSubview:self.textAnimationView];
```


   * Process data

```objectivec
- (void)textAnimationView:(DVETextAnimationView *)ta_view didChangeAnimationWithType:(DVETextAnimationType)ta_type {
  if (!_textAnimation) {
    _textAnimation = [[NLEStyStickerAnimation_OC alloc] init];
  }
  NLETrackSlot_OC *slot = [self.vcContext.nleEditor.model slotOf:self.segmentId];
  if (!slot) {
    slot = [self.vcContext.nleEditor.model.coverModel slotOf:self.segmentId];
  }
   
  if (ta_type == DVETextAnimationTypeIn || ta_type == DVETextAnimationTypeOut) {
    NLEResourceNode_OC *inNode = [[NLEResourceNode_OC alloc] init];
    inNode.name = ta_view.inAnimation.name;
    inNode.resourceFile = ta_view.inAnimation.path;
    int32_t inDuration = ta_view.inDuration * 1000 * 1000;
    _textAnimation.inAnimation = inNode;
    _textAnimation.inDuration = inDuration;
    _textAnimation.loop = NO;
    NLEResourceNode_OC *outNode = [[NLEResourceNode_OC alloc] init];
    outNode.name = ta_view.outAnimation.name;
    outNode.resourceFile = ta_view.outAnimation.path;
    int32_t outDuration = ta_view.outDuration * 1000 * 1000;
    _textAnimation.outAnimation = outNode;
    _textAnimation.outDuration = outDuration;
    _textAnimation.loop = NO;
  }
  if (ta_type == DVETextAnimationTypeLoop) {
    NLEResourceNode_OC *node = [[NLEResourceNode_OC alloc] init];
    node.name = ta_view.loopAnimation.name;
    node.resourceFile = ta_view.loopAnimation.path;
    int32_t duration = ta_view.loopDuration * 1000 * 1000;
    _textAnimation.inAnimation = node;
    _textAnimation.inDuration = duration;
    _textAnimation.loop = YES;
  }
  [self textAnimationDidChange];
  if (_textAnimation.inDuration > 0 || _textAnimation.outDuration > 0) {
    [self.vcContext.nle setStickerPreviewMode:slot previewMode:(int)ta_type];
  }
}
```

<span id="416a0fb6"></span>
## Voice change
**Feature**
Applies various voice change filters to video or audio tracks with voice.
Currently, the following voice change filters are supported: cute girl, aged man, female, male, and monster
**API definition**
As an attribute of **NLETrackSlot**, **NLEFilter** indicates a voice change filter.
```objectivec
@interface NLETrackSlot_OC : NLETimeSpaceNode_OC
.....
///  Set a voice change filter.
- (void)setAudioFilter:(NLEFilter_OC* __nullable)filter;

- (NLEFilter_OC*)audioFilter;

- (void)clearAudioFilter;

....

@end
```

```objectivec
@interface NLEFilter_OC : NLETimeSpaceNode_OC
/// The video clip filter.
@property (nonatomic, strong) NLESegmentFilter_OC* segmentFilter;

/// Deep clone.
- (NLEFilter_OC*)deepClone;
                              
@end
```

```objectivec
@interface NLESegmentFilter_OC : NLESegment_OC
...
///  The voice change filter name to be displayed.
@property (nonatomic, copy) NSString *filterName;

///  TheVoice change resource.
@property (nonatomic, copy) NLEResourceNode_OC *effectSDKFilter;
...
@end
```

**Sample code**

* Apply or switch to another voice change filter

```objectivec
///  Apply a voice change filter.
/// @param slot: the audio/video slot.
/// @param sourcePath: the resource path.
/// @param sourceName: the resource name.
- (NSString*)audioChangeForSlot:(NLETrackSlot_OC *)slot sourcePath:(NSString*)sourcePath sourceName:(NSString*)sourceName
{
  if (!slot) { return nil; }
  
  NLEResourceNode_OC* node = [[NLEResourceNode_OC alloc] init];
  node.resourceFile = sourcePath;
  node.resourceName = sourceName;
  node.resourceType = NLEREsourcetypeVoiceChangerFilter;
   
  NLESegmentFilter_OC* seg = [[NLESegmentFilter_OC alloc] init]; 
  seg.effectSDKFilter = node;
  seg.filterName = sourceName;
  
  NLEFilter_OC* filter = [[NLEFilter_OC alloc] init];
  filter.segmentFilter = seg;
  
  slot.audioFilter = filter;
   
  [self.vcContext commitNLE:YES];
   
  return node.nle_nodeId;

}
```


* Cancel the voice change

```objectivec
///  Remove a voice change filter.
/// @param slot: the audio/video slot.
- (void)removeAudioChangeForSlot:(NLETrackSlot_OC *)slot
{
  if (!slot) { return; }
  slot.audioFilter = nil;
  [self.vcContext commitNLE:YES];

}
```

<span id="fa7a2fab"></span>
## Audio speed
**Feature**
Speeds up or down an audio when the speed change icon is tapped. You can drag the scroll bar to set the speed for the selected track, select or clear the pitch check box to determine whether to change the pitch after speed change, and adjust the speed on the speed panel. When the speed exceeds 5x, the pitch will change automatically.
**API definition**
Call the **changeAudioSpeed** method to change the audio speed.
```objectivec
@protocol DVECoreAudioProtocol <DVECoreProtocol>
//...
// Change the audio speed.
- (void)changeAudioSpeed:(CGFloat)speed slot:(NLETrackSlot_OC *)slot shouldKeepTone:(BOOL)shouldKeepTone;
```

NLESegmentAudio_OC: audio clip
```objectivec
@interface NLESegmentAudio_OC : NLESegment_OC
//...
/// The duration after speed change.
@property (nonatomic, assign, readonly) CMTime duration;
///   The audio speed parameter. The value 2 indicates that the audio is to be played at 2x speed. It cannot be set to 0.
@property (nonatomic, assign) CGFloat absSpeed;
///   The audio speed parameter. The value 2 indicates that the audio is to be played at 2x speed. It cannot be set to 0.
- (void)setAbsSpeed:(CGFloat)absSpeed
/// Set whether to keep the original audio after the speed is specified. true specifies to keep the original audio. false specifies to change the speed. Default value: false.
- (void)setKeepTone:(bool)KeepTone;

@end
```

**Sample code**

* Audio speed

```objectivec
/// Change the audio speed.
/// @param slot: the audio slot.
/// @param speed: the audio speed.
/// @param shouldKeepTone: indicates whether to keep pitch.
- (void)changeAudioSpeed:(CGFloat)speed slot:(NLETrackSlot_OC *)slot shouldKeepTone:(BOOL)shouldKeepTone
{
  if (!slot) return;
  if (![slot.segment isKindOfClass:[NLESegmentAudio_OC class]]) return;
  NLESegmentAudio_OC *audioSegment = (NLESegmentAudio_OC *)slot.segment;
  NLETrack_OC *track = [self.vcContext.mediaContext.editor.model trackContainSlotId:slot.nle_nodeId];
  // Update the speed.
  [audioSegment setAbsSpeed:speed > 0? speed : audioSegment.absSpeed];
  [audioSegment setKeepTone:shouldKeepTone];
  slot.endTime = CMTimeAdd([audioSegment getDuration], slot.startTime);
  // If the audio slot overlaps with other slots on the same track, modify the track.
  for (NLETrackSlot_OC *trackSlot in track.slots) {
    if (![trackSlot.nle_nodeId isEqualToString:slot.nle_nodeId]
      && CMTimeRangeContainsTime(slot.nle_targetTimeRange, trackSlot.startTime)) {
      NLETrack_OC *newTrack = [[NLETrack_OC alloc] init];
      newTrack.extraTrackType = NLETrackVIDEO;
      newTrack.layer = [self.vcContext.mediaContext.editor.model nle_getMaxTrackLayer:NLETrackVIDEO] + 1;
      [track removeSlot:slot];
      [newTrack addSlot:slot];
      [self.vcContext.mediaContext.editor.model addTrack:newTrack];
      break;
    }
  }
  [self.vcContext commitNLE:YES];
  // Notify the editor of the track update.
  [self.vcContext.mediaContext notifyEditorChanged];
  // Move the timeline to the start position of the audio slot.
  [self.vcContext.mediaContext updateTargetOffsetWithTime:slot.startTime];
}
```

The methods in NLE for setting Speed and KeepTone are as follows:
```objectivec
///   The audio speed parameter. The value 2 indicates that the audio is to be played at 2x speed. It cannot be set to 0.
- (void)setAbsSpeed:(CGFloat)absSpeed
{
  self.cppSegmentAudio->setAbsSpeed(absSpeed);
}
- (void)setKeepTone:(bool)KeepTone
{
  self.cppSegmentAudio->setKeepTone(KeepTone);
}
```

<span id="9e5b3fc4"></span>
## Enable or disable original sound
**Feature**
Enables or disables the original sound of all video clips on the main track after a user taps the corresponding button.
**API definition**
**NLESegmentVideo_OC** describes a video clip on a track. A specific field indicates whether the track is muted or not, to determine whether to enable original sound.
```objectivec
- (bool)hasEnableAudio;

- (void)setEnableAudio:(bool)enableAudio;
```

**Sample code**
```objectivec
- (void)toggleOriginalSoungButton:(UIButton *)button
{
  _button.selected = !_button.selected;
  [[NSNotificationCenter defaultCenter] postNotificationName:@"toggleOriginalSoungButton"
                            object:nil];
  BOOL isTurnOffAudio = _button.selected;
   // 1. Obtain the current NLEModel.
  NLEModel_OC *model = _context.editor.model;
  // 2. Obtain the main track.
  NLETrack_OC *mainTrack = [model nle_getMainVideoTrack];

  if (!mainTrack) {
    return;
  }
   // 3. Traverse all slots and set whether to enable the original sound of segments.
  for (NLETrackSlot_OC *slot in mainTrack.slots) {
    NLESegmentVideo_OC *segment = (NLESegmentVideo_OC *)slot.segment;
    [segment setEnableAudio:!isTurnOffAudio];
  }

  mainTrack.volume = isTurnOffAudio ? 0 : 1;
  [_context.editor commit];
  // Save
  [_context.editor done];
}
```

**VE logic**
```objectivec
IESMMAudioVolumeConfig *volumeConfig = [IESMMAudioVolumeConfig new];
 volumeConfig.volume = volume;
 IESMMAudioFilter *filter = [[IESMMAudioFilter alloc] init];
  filter.type   = IESAudioFilterTypeVolume;
  filter.config  = config;
  filter.startTime = kCMTimeInvalid;
  filter.duration = kCMTimeInvalid;
  [self.veEditor setAudioFilter:filter forVideoAssets:@[asset]];
```

<span id="c0a0b56f"></span>
## Audio fade-in and fade-out
**Feature**
Sets an audio fade-in and fade-out effect with specific duration for an audio track.
**API description**
NLESegmentAudio_OC
```objectivec
- (void)setFadeInLength:(CMTime)fadeInLength;

///  Fade-in.
- (CMTime)fadeInLength;

- (void)setFadeOutLength:(CMTime)fadeOutLength;

/// Fade-out.
- (CMTime)fadeOutLength;
```

**API call example**
```objectivec
- (NLETrackSlot_OC *)updateCurSlot
{
  NLETrackSlot_OC *curSlot = nil;
  self.isMainTrack = NO;
  if (self.vcContext.mediaContext.selectAudioSegment) {
    curSlot = self.vcContext.mediaContext.selectAudioSegment;
  } else {
    if (self.vcContext.mediaContext.selectMainVideoSegment) {
      self.isMainTrack = YES;
      curSlot = self.vcContext.mediaContext.selectMainVideoSegment;
    } else if (self.vcContext.mediaContext.selectBlendVideoSegment) {
      curSlot = self.vcContext.mediaContext.selectBlendVideoSegment;
    }
  }
   
  return curSlot;
}
- (void)fadeInSliderChanged:(id)slider
{
  NLETrackSlot_OC *curSlot = [self updateCurSlot];
   
   
  if ([curSlot.segment isKindOfClass:[NLESegmentAudio_OC class]]) {
    NLESegmentAudio_OC *segment = (NLESegmentAudio_OC *)(curSlot.segment);
    [segment setFadeInLength:CMTimeMake(self.fadeInSlider.value * 1000, 1000)];
    [self.vcContext commitNLE:YES];
  }
}

- (void)fadeOutSliderChanged:(id)slider
{
  NLETrackSlot_OC *curSlot = [self updateCurSlot];
   
   
  if ([curSlot.segment isKindOfClass:[NLESegmentAudio_OC class]]) {
    NLESegmentAudio_OC *segment = (NLESegmentAudio_OC *)(curSlot.segment);
    [segment setFadeOutLength:CMTimeMake(self.fadeOutSlider.value * 1000, 1000)];
    [self.vcContext commitNLE:YES];
  }
}
```

**VE logic**
```objectivec
IESMMAudioFadeConfig *config = [IESMMAudioFadeConfig new];
config.fadeInDuration = inDuration;
config.fadeOutDuration = outDuration;
config.fadeInCurve = IESMMAudioFadeCurveLine;
config.fadeOutCurve = IESMMAudioFadeCurveLine;

IESMMAudioFilter *filter = [[IESMMAudioFilter alloc] init];
  filter.type   = IESAudioFilterTypeFade;
  filter.config  = config;
  filter.startTime = kCMTimeInvalid;
  filter.duration = kCMTimeInvalid;
[self.veEditor setAudioFilter:filter forAudioAssets:@[asset]];
```

<span id="f7e0ec6f"></span>
## Audio recording
**Feature**
Creates audio recording clips, which are also audio resources. You can add multiple audio recording tracks and add multiple audio recording clips to the same track.
**API definition**
You can call **VEAudioRecorder** to create an audio recording object.
```objectivec
@interface VEAudioRecorder : IESMMObject

/**
  Set the block for obtaining the audio waveform and volume in real time.
 */
@property (nonatomic, copy, nullable) IESLVWaveformResultBlock waveResultBlock;

@property (nonatomic, readonly) BOOL isRecording;

@property (nonatomic, readonly) NSTimeInterval recordDuration;

- (instancetype)initWithWaveformConfig:(IESWaveformConfig *_Nullable)waveConfig;

/**
  Asynchronously call the prepareSync API for preparation.

  @param completeBlock Preparation completion block.
 */
- (void)prepare:(IESLVCompleteBlock)completeBlock;

/**
  Prepare for audio recording: Call the setCategory method to set the device category, which may take about 50 to 100 ms.
 */
- (void)prepareSync;

/**
  Start audio recording. Call this method after prepare or prepareSync is complete. You need to call this method only once after initialization is completed.
 */
- (void)startRecord;
- (void)startRecordWithPrivacyCert:(nullable id)privacyCert;

/**
  Pause audio recording. The system temporarily stops writing data to the audio file but still collects data. To stop audio recording, call the stop method.
 */
- (void)pauseRecord;

/**
  Stop audio recording. The system generates an available audio file.

  @param completeBlock URL of the audio file.
 */
- (void)stopRecord:(IESLVStopBlock _Nullable)completeBlock;
- (void)stopRecord:(IESLVStopBlock _Nullable)completeBlock withPrivacyCert:(nullable id)privacyCert;

/**
  Reset the duration after audio recording stops.
 */
- (void)resetDuration;

@end
```

**Sample code**

* Construct an audio recording object

```objectivec
#define timelineWidthPerFrame (50.0)
#define wavePerSecondsCount (timelineWidthPerFrame * 0.5)
  
  
  IESWaveformConfig* config = [IESWaveformConfig new];
  config.waveType = WaveformTypeMAX;
  config.durationPerFrame = 1 / wavePerSecondsCount; //Frame rate.
  config.pointPersec = wavePerSecondsCount; // Number of points returned per second during audio recording.
   
  VEAudioRecorder* recorder = [[VEAudioRecorder alloc] initWithWaveformConfig:config];
  @weakify(self);
  recorder.waveResultBlock = ^(NSArray * _Nonnull volumeArray) {
  //// Callback for a point array of a waveform.
    @strongify(self);
    [self audioRecorderRecording:volumeArray];
  };
```


* Add an audio recording track

```objectivec
- (NLETrack_OC*)addRecorderTrack
{
  NLETrack_OC *track = [[NLETrack_OC alloc] init];
  track.extraTrackType = NLETrackAUDIO;
  track.layer = (int)([self.vcContext.nleEditor.model nle_getMaxTrackLayer:NLETrackAUDIO] + 1);
  [[self.vcContext.mediaContext.editor getModel] addTrack:track];
  return track;
}
```


* Construct an audio recording clip

```objectivec
- (NLETrackSlot_OC*)addRecorderSlot:(NSString *)audioName startTime:(CMTime)startTime toTrack:(NLETrack_OC*)track
{
  
  NLEResourceAV_OC *audioResource = [[NLEResourceAV_OC alloc] init];
  audioResource.resourceName = audioName;        ///Audio recording name.
  audioResource.resourceType = NLEResourceTypeRecord;  /// The resource type.
  audioResource.resourceFile = [self recordFilePath];  /// The path of the audio recording file.
   
  NLESegmentAudio_OC *audioSegment = [[NLESegmentAudio_OC alloc] init];
  audioSegment.audioFile = audioResource;
  audioSegment.timeClipStart = CMTimeMake(0, USEC_PER_SEC);
   
  NLETrackSlot_OC *trackSlot = [[NLETrackSlot_OC alloc] init];
  [trackSlot setSegmentAudio:audioSegment];
  trackSlot.startTime = startTime;
   
  [track addSlot:trackSlot];
   
  track.endTime = trackSlot.endTime;
  self.vcContext.mediaContext.recordingTrack = track;//Trigger an update on the track display.
   
  [self.vcContext.mediaContext updateTargetOffsetWithTime:startTime];//Update the current display.
   
  return trackSlot;
}
```


* Start audio recording

```objectivec
NSError *setCategoryError = nil;
  BOOL success = [[AVAudioSession sharedInstance] setCategory:AVAudioSessionCategoryRecord error:&setCategoryError];
  if (!success) {
    [DVECustomerHUD showMessage:@"Failed to launch the recorder."];
    self.recorder = nil;
    return;
  }
  @weakify(self);
  [self.recorder prepare:^(BOOL success, NSError * _Nullable error) {
    @strongify(self);
    if(success){
      [self audioRecorderDidStart];
    }else{
      [[AVAudioSession sharedInstance] setCategory:AVAudioSessionCategoryPlayback error:nil];
      [DVECustomerHUD showMessage:@"Recording failed."];
    }
  }];
```


* Update an audio recording clip

```objectivec
-(void)updateRecorderSlot:(NLETrackSlot_OC*)slot time:(NSTimeInterval)time toTrack:(NLETrack_OC*)track wavePoints:(NSArray*)points
{
  NLESegmentAudio_OC *audioSegment = (NLESegmentAudio_OC*)[slot segment];

  CMTime newTime = CMTimeMake(time * NSEC_PER_SEC, NSEC_PER_SEC);
  audioSegment.nle_wavePoints = points;
  audioSegment.timeClipEnd = newTime;
  slot.duration = newTime;
   
  NLEResourceAV_OC *audioResource = audioSegment.audioFile;
  audioResource.duration = newTime;
   
  track.endTime = slot.endTime;
   
  self.vcContext.mediaContext.recordingTrack = self.vcContext.mediaContext.recordingTrack;
   
  [self.vcContext.mediaContext updateTargetOffsetWithTime:slot.endTime];

}
```


* Stop audio recording

```objectivec
@weakify(self);
  [self.recorder stopRecord:^(NSURL * _Nullable fileUrl, NSError * _Nullable error) {
    @strongify(self);
    [self audioRecorderDidFinishRecording:fileUrl success:( error == nil && fileUrl != nil)];
    self.recorder = nil;
    [[AVAudioSession sharedInstance] setCategory:AVAudioSessionCategoryPlayback error:nil];
  }];
```

<span id="405ee1b5"></span>
## Curve speed change
**Feature**
Speeds up or down a video clip at a variable rate (described through a curve), so that the video speed varies at different time points.
**Related concepts**
Segment point or trim point: anchor point in the coordinate system of the asset time. For example, for a 10s video, PointA(0.5, 2.0) indicates that the 5th second is played at 2x speed. Note that the editing panel for curve speed change deals with the time points before the speed change.
Sequence point: anchor point in the coordinate system of the playback time. For example, for a 10s video whose actual playback duration decreases to 4s after curve speed change, PointA(0.5, 2.0) indicates that the 2nd second is played at a 2x speed. Note that after the curve speed change, VE obtains the play progress based on sequence points and that the **seekTo** method deals with the time points after the speed change.
**API definition**
```objectivec
// NLESegmentAudio+iOS.h

// Set a speed change point. x corresponds to a time point before speed change.
/// 1. x ranges from 0 to 1, indicating the play progress of the player. y ranges from 0.1 to 10, indicating the number of times that the updated speed is as much as the original speed.
// points indicate an array obtained after CGPoint is converted into NSValue.
// The value nil indicates that the speed change points are to be cleared.
- (void)setCurveSegPoints:(NSArray<NSValue *> *)points;
// Obtain a speed change point. x corresponds to a time point before speed change.
- (NSArray<NSValue *> *)getCurveSegPoints;
//  Obtain the average speed after speed change.
- (CGFloat)avgCurveSpeed;
//  Obtain the duration without curve speed change, in microseconds.
- (int64_t)getDurationWithoutCurveSpeed;
```

**Sample code**
```objectivec
//  Update the speed change point of a video clip on the main track.
- (void)updateVideo:(NLETrackSlot_OC *)slot curveSpeedPoint:(NSArray *)points shouldCommit:(BOOL)commit {
  if (![slot.segment isKindOfClass:NLESegmentVideo_OC.class]) {
    return;
  }
  //  Obtain a video clip
  NLESegmentVideo_OC *videoSegment = (NLESegmentVideo_OC *)slot.segment;
  NLETrack_OC *videoTrack = [self.editor.model nle_getMainVideoTrack];
  //  Determine whether the video clip is on the main track.
  BOOL isInMainTrack = NO;
  for (NLETrackSlot_OC *childSlot in videoTrack.slots) {
    if ([childSlot.nle_nodeId isEqualToString:slot.nle_nodeId]) {
      isInMainTrack = YES;
      break;
    }
  }
  if (!isInMainTrack) {
    return;
  }
  // Update the speed change point.
  [videoSegment setCurveSegPoints:points];

  //  Update the end time of the slot.
  slot.endTime = CMTimeAdd(slot.startTime, videoSegment.duration);
   
  [videoTrack nle_rescheduleTrackForTransitionChanged];
  [self notifyEditorChangedWithCommit:commit];
}
```


* Curved speed change calculator class

When you play a video clip after speed change, you can call the NLECurveSpeedCalculator_OC class to convert a time point after speed change into a time point before speed change for processing on the editing panel for curved speed change. The header file is defined as follows:
```objectivec
@interface NLECurveSpeedCalculator_OC: NSObject

/// segment points -> sequence points
+ (NSArray<NSValue *> *)segmentPToSequenceP:(NSArray<NSValue *> *)segPoints;

- (instancetype)initWithSeqPoints:(NSArray<NSValue *> *)seqPoints;
- (instancetype)initWithSegPoints:(NSArray<NSValue *> *)segPoints;

/**
 * Average speed.
 */
- (double)getAveCurveSpeedRatio;

/**
 * @param seqDurationUs  The duration of the asset after speed change, in microseconds.
 */
- (double)getSpeedRatioBySeqDelta:(int64_t)sequenceDeltaUs seqDurationUs:(int64_t)seqDurationUs;

/**
 * @param seqDurationUs The duration of the asset after speed change.
 */
- (int64_t)sequenceDelToSegmentDel:(int64_t)sequenceDeltaUs seqDurationUs:(int64_t)seqDurationUs;

/**
 * @param seqDurationUs  Duration of the asset after speed change.
 */
- (int64_t)segmentDelToSequenceDel:(int64_t)segmentDeltaUs seqDurationUs:(int64_t)seqDurationUs;

///  Generate a start point, two control points, and an end point of a third-order Bezier curve.
/// @param points: two normalized coordinate points.
+ (NSArray<NSValue *>*)generateThirdBezierPathPoints:(NSArray<NSValue *>*)points;

///  Generate all points of the Bezier curve.
/// @param points: four points of the Bezier curve.
+ (NSArray<NSValue *>*)generateBezierPathLookupTable:(NSArray<NSValue *>*)points;

///  Calculate points of a fitted Bezier curve at the current progress.
/// @param points: the start point, two control points, and end point of a third-order Bezier curve.
/// @param progress: the processing progress. Valid range: [0, 1].
+ (NSArray<NSValue *>*)recursiveCalculateCubePoint:(NSArray<NSValue *>*)points progress:(float)progress;

///  Find the coordinates of a point on a Bezier curve based on coordinates of the left and right CGPoints, the duration of the Bezier curve, and the offset of the target point from the X-axis.
/// @param left CGPoint,
/// @param right CGPoint,
/// @param duration  The duration corresponding to the entire Bezier curve on the X-axis.
/// @param offset       The offset of the point to be calculated from the X-axis.
+ (CGPoint)getBezierPointsWithLeft:(CGPoint)left right:(CGPoint)right duration:(int64_t)duration offet:(int64_t)offset;

///  Find the coordinates of points on a fitted Bezier curve at the current time t by using the preceding formula.
/// @param t: the current time. Value range: [0,1].
/// @param start: the start point.
/// @param control1: Control point 1.
/// @param control2: Control point 2.
/// @param end: the end point.
+ (CGPoint)calculateCubePointWithT:(float)t start:(CGPoint)start control1:(CGPoint)control1 control2:(CGPoint)control2 end:(CGPoint)end;

@end
```

**API call example**
```objectivec
//  Update the current point.
- (void)setCurrentPoints:(NSArray<NSValue *> *)currentPoints {
  if (_currentPoints != currentPoints) {
    self.currentTransFomedPoints = [self transferedPointsFromOriginPoints:currentPoints];
    if (currentPoints.count > 1) {
      //  Update the conversion tool.
      self.transUtil = [[NLECurveSpeedCalculator_OC alloc] initWithSegPoints:currentPoints];
    } else {
      self.transUtil = nil;
    }
    _currentPoints = currentPoints;
  }
}


 //  Convert the current time at which an asset is played into the original time of the asset.
  int64_t transTime = [self.transUtil sequenceDelToSegmentDel:currentIntTime seqDurationUs:self.seqDurationUs];
 //  Convert the original time of an asset into a time point after speed change.
 [self.transUtil segmentDelToSequenceDel:videoTime seqDurationUs:self.seqDurationUs];
```

<span id="6c235bd3"></span>
## Thumbnail
**Feature**
Edits the thumbnail of a produced video, and calls the VE API to use the thumbnail as the first frame of the video.
Uses a frame of the video previewed on the main editing screen or a cropped picture in the album as the thumbnail background, and adds text stickers to the background to obtain the final thumbnail.
**API definition**
**NLEVideoFrameModel_OC** describes the thumbnail editing model.
```objectivec
@interface NLEVideoFrameModel_OC : NLETimeSpaceNode_OC

/// The thumbnail editing snapshot, which is a picture.
@property (nonatomic, strong) NLEResourceNode_OC *snapshot;
/// The edited background, which can be a pure color, gradient colors, a picture, or a video frame.
@property (nonatomic, strong) NLEStyCanvas_OC *coverMaterial;
/// Set the timestamp of a video frame. This field is valid only when timeNLEStyCanvasType is set to NLECanvasTypeVideoFrame.
@property (nonatomic, assign) int64_t videoFrameTime;
/// Set the canvas aspect ratio, which is the ratio of the screen width to the screen height and is 16:9 by default when the desktop editor is in landscape.
@property (nonatomic, assign) float canvasRatio;

- (NSArray<NLETrack_OC *> *)tracks;

- (void)addTrack:(NLETrack_OC *)track;

- (void)removeTrack:(NLETrack_OC *)track;

- (NLEVideoFrameModel_OC *)deepClone;

@end
```

**Sample code**
Set whether to create a thumbnail editing model. **enable** is set to **NO** by default. After thumbnail editing starts, set **enable** to **YES**.
In the thumbnail editing model, the first frame of the video is selected as the thumbnail by default.
```objectivec
// Here, self holds an NLEEditor_OC object.
NLEModel_OC *editModel = [self.nleEditor getModel];
if (!editModel.coverModel) {
    editModel.coverModel = [[NLEVideoFrameModel_OC alloc] init];
    editModel.coverModel.coverMaterial = [[NLEStyCanvas_OC alloc] init];
    editModel.coverModel.coverMaterial.canvasType = NLECanvasVideoFrame;
    editModel.coverModel.videoFrameTime = 0;
    editModel.coverModel.enable = YES;
}
```


* Change the resource type to pictures from the album

```objectivec
NLEModel_OC *editModel = [self.nleEditor getModel];
NLEVideoFrameModel_OC *coverModel = editModel.coverModel;
NLEStyCanvas_OC *coverMaterial = coverModel.coverMaterial;
coverMaterial.canvasType = NLECanvasImage;
if (! coverMaterial.imageSource) {
    coverMaterial.imageSource = [[NLEResourceNode_OC alloc] init];
}
// Save the picture path to resourceNode.
coverMaterial.imageSource.resourceFile = imagePath;
[self.vcContext commitNLE:NO];
```


* Add a text sticker track

```objectivec
// Set the start time of the text sticker, which starts from 0 on the thumbnail editing screen.
CGFloat startTime = 0;
// Set the duration of the text sticker, which is the maximum duration of the entire track on the thumbnail editing screen.
CGFloat duration = [[self.nleEditor getModel] getMaxTargetEnd];
// Set the end time of the text sticker.
CGFloat endTime = startTime + duration;
   
NLETrack_OC *textTrack = [[NLETrack_OC alloc] init];
textTrack.extraTrackType = NLETrackSTICKER;
textTrack.nle_extraResourceType = NLEResourceTypeTextSticker;

// Adding a text sticker track on the thumbnail editing screen is similar to adding one to the NLEModel, except that coverModel is used here.

// Convert the text JSON parameter dictionary into strings.
NSDictionary *jsonDict = @{
    @"version": @"1",
    @"text": @" Enter text ",
    @"background": @YES,
    @"fontSize": @15,
};
NSData *jsonData = [NSJSONSerialization dataWithJSONObject:jsonDict options:0 error:&error];
NSString * paramString = [[NSString alloc] initWithData:jsonData encoding:NSUTF8StringEncoding];
NLEStyleText_OC *styleText = [NLEStyleText_OC textStyleWithJSONString:paramsString];
NLESegmentTextSticker_OC *segment = [[NLESegmentTextSticker_OC alloc] init];
segment.style = styleText;
// The text content displayed on the text sticker.
segment.content = @"";

NLETrackSlot_OC *textSlot = [[NLETrackSlot_OC alloc] init];
textSlot.startTime = CMTimeMake(startTime * USEC_PER_SEC, USEC_PER_SEC);
textSlot.endTime = CMTimeMake(endTime * USEC_PER_SEC, USEC_PER_SEC);
textSlot.duration = CMTimeMake(duration * USEC_PER_SEC, USEC_PER_SEC);
textSlot.segment = segment;

[textTrack addSlot:textSlot];

// Obtain the top layer of a sticker track in coverModel.
NSMutableArray<NLETrack_OC *> *result = [NSMutableArray array];
for (NLETrack_OC *track in [coverModel tracks]) {
    if (track.extraTrackType == NLETrackSTICKER || track.getTrackType == NLETrackSTICKER) {
        [result addObject:track];
    }
}

[result sortUsingComparator:^NSComparisonResult(NLETrack_OC * _Nonnull obj1, NLETrack_OC * _Nonnull obj2) {
    if (obj1.layer > obj2.layer) {
        return NSOrderedDescending;
    } else {
        return NSOrderedAscending;
    }
}];

NSInteger layerMax = -1;
for (NLETrack_OC *track in result) {
    if (track.layer > layerMax) {
        layerMax = track.layer;
    }
}
textTrack.layer = (int)(layerMax + 1);

[coverModel addTrack:textTrack];
[self.vcContext commitNLE:NO];
```


* Delete a text sticker track

```objectivec
// Delete a text sticker track from coverModel.
NSArray<NLETrack_OC *> *tracks = [coverModel tracks];
for (NLETrack_OC *track in tracks) {
    if (track.extraTrackType == NLETrackSTICKER) {
        [cover removeTrack:track];
    }
}
[self.vcContext commitNLE:NO];
```


* Call the VE API to extract a video frame and save the path of the extracted picture to the snapshot in **coverModel**.

```objectivec
// When resources of the thumbnail editing model are pictures of the album, the frame extraction time is 0. When resources of the thumbnail editing model are video frames, the frame extraction time is the videoFrameTime of the thumbnail editing model.
CGFloat atTime = 0;
if (coverModel.coverMaterial.canvasType == NLECanvasVideoFrame) {
    atTime = coverModel.videoFrameTime * 1.0 / USEC_PER_SEC;
}

// The size of the extracted picture.
CGSize size = CGSizeMake(200, 200);

// Call the VE API by using the NLEInterface_OC object.
[self.vcContext.videoManager getProcessedPreviewImageAtTime:time
                           preferredSize:size    
                           compeletion:^(UIImage * image, NSTimeInterval atTime) {
      if (image) {
        // Set the snapshot path.
        NSString *snapshotPath = @"";
        [UIImageJPEGRepresentation(image, 1) writeToFile:snapshotPath atomically:YES];
        coverModel.snapshot.resourceFile = snapshotPath;
      }
}];
```


* Exit the thumbnail editing screen, save the thumbnail editing model, and set **enable** to **NO**.

```objectivec
coverModel.enable = NO;
[self.vcContext commitNLE:YES];
```

<span id="e670f0bf"></span>
## Full-screen preview
**Feature**
In the editing interface, click the "Enter Full Screen" button in the toolbar to enter the full-screen state and play automatically.
Drag the progress bar to preview the screen showing the location of the progress.
Release the progress bar and continue playing if it was playing before dragging the progress bar. Otherwise, it is paused.

| | | \
|![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a42d2db602644dbf8bb020221d8f9d9d~tplv-goo7wpa0wc-image.image =300x) |\
| |![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8299e816fae14da584ce8784e8f27958~tplv-goo7wpa0wc-image.image =300x) |\
| | |
|---|---|

**API definition**
Full-screen preview basically reuses PreView on the editing interface. The main interfaces of DVEPreView are as follows:
```objectivec
@interface DVEPreview : UIView<DVECoreActionNotifyProtocol>
@property (nonatomic, weak) DVEVCContext *vcContext;
@property (nonatomic, strong) DVECanvasVideoBorderView *canvasBorderView;

///Whether gestures are displayed in the canvas box
/// @param enableGesture whether gestures are available or not
- (void)showCanvasBorderEnableGesture:(BOOL)enableGesture;

///Whether to disable gestures
/// @param disable Whether disable gestures or not
- (void)disableGesture:(BOOL)disable;

///Hide canvas frame
- (void)hideCanvasBorder;
```

DVE PreViewController is defined as follows:
```objectivec
@property (nonatomic, copy) dispatch_block_t closeBlock;
@property (nonatomic, weak) DVEVCContext *vcContext;
@property (nonatomic, weak) DVEPreview *preview;
@property (nonatomic, assign) BOOL isPlayed; //Whether the main editing interface is playing video
@property (nonatomic, weak) UIViewController *parentVC;

- (instancetype)initWithContext:(DVEVCContext *)vcContext
            preview:(DVEPreview *)preview
            isPLayed:(BOOL)isPlayed
            parentVC:(UIViewController *)parentVC
           closeBlock:(dispatch_block_t)closeBlock;
```

**Sample Code**

* Enable fullscreen

```objectivec
DVEPreviewViewController *vc = [[DVEPreviewViewController alloc] initWithContext:self.vcContext preview:self.preview isPLayed:YES parentVC:self.parentVC closeBlock:^{
    [self addSubview:self.preview];
    [self updatePreviewSize];
  }];
  vc.modalPresentationStyle = UIModalPresentationFullScreen;
  [self.parentVC presentViewController:vc animated:NO completion:^{
     
  }];
```


* Disable fullscreen

```objectivec
- (UIButton *)closeButton
{
  if (!_closeButton) {
    ...
    [[_closeButton rac_signalForControlEvents:UIControlEventTouchUpInside] subscribeNext:^(__kindof UIControl * _Nullable x) {
      @strongify(self);
      CMTime time = CMTimeMake(self.vcContext.playerService.currentPlayerTime * USEC_PER_SEC, USEC_PER_SEC);
//The main video track moves to the specified time position
      [self.vcContext.mediaContext updateTargetOffsetWithTime:time];
//If the previously recorded video canvas is selected, the check box for the video canvas is displayed
      if (!self.canvasBorderHidden) {
        [self.preview showCanvasBorderEnableGesture:YES];
      }
//Call the callback event of closing the full screen preview with external settings
      [self dismissViewControllerAnimated:NO completion:^{
        if(self.closeBlock){
          self.closeBlock();
        }
      }];
//Restore the sticker editable box in PreView
      [self restoreStickerEditBox];
    }];
  }
  return _closeButton;
}
```

<span id="f6170a6b"></span>
## Keyframe
<span id="26ad0362"></span>
### Overview
You can set all the supported effect parameters in each keyframe to achieve simultaneous movements or changes of these parameters between two keyframes.
![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/33b38c8124564ecf83c660ed3fd7f87a~tplv-goo7wpa0wc-image.image)
<span id="d3468fc3"></span>
### Non-linear edit (NLE) data model
A keyframe object is inherited from an NLETrackSlot object and is specified in the KeyframeList parameter of the NLETrackSlot object. A keyframe is similar to a snapshot at a specific point in time in an asset fragment. You can add multiple keyframes in one asset fragment. The point in time of a keyframe is indicated by the StartTime parameter in the keyframe object. This point in time is relative to the beginning of the fragment instead of the absolute position on the timeline.
![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/59a3a52209c84267b2f9ef777ce6b69d~tplv-goo7wpa0wc-image.image)
<span id="fcf92adc"></span>
### Supported functions

1. Canvas movement, zooming, and rotation
2. Volume adjustment
3. Mask
4. Reversal
5. Fragment slot movement, cutting, and adjustment
6. Linear speed change and curved speed change
7. Filters and adjustment
8. Texts and stickers

<span id="b652691f"></span>
### Classes related to keyframe
DVEKeyFrameEditor
```Plain Text
/// Determine whether the specified slot has a keyframe.
/// @param slot: Specifies the slot.
-(BOOL)hasKeyframe:(NLETrackSlot_OC*)slot;

/// Specify the time range of the current keyframe.
-(CMTime)currentKeyframeTimeRange;

/// Update the keyframe information of the current slot.
- (void)refreshAllKeyFrameIfNeedWithSlot:(NLETrackSlot_OC *)slot;
```

NLETrackSlot+iOS
```Plain Text
/// Determine whether to add or modify a keyframe.
/// @param startTime: The current position on the timeline.
/// @param timeRange: The time range of the current keyframe.
/// @param forceAdd: Specifies whether to forcibly add a keyframe. If you're actively adding a keyframe at the UI layer, set this parameter to true. If you want a keyframe to be automatically added after the properties of a slot are modified, set this parameter to false.
-(NSString *)addOrUpdateKeyframe:(CMTime)startTime timeRange:(CMTime)timeRange forceAdd:(BOOL)forceAdd;

/// Remove the keyframe that is closest to a specified position on the timeline.
/// @param startTime: The corresponding position on the timeline of the keyframe.
/// @param timeRange: The time range of the current keyframe.
-(BOOL)removeKeyframe:(CMTime)startTime timeRange:(CMTime)timeRange;

/// Adjust the position of a keyframe.
/// @param timeRange: The time range of the current keyframe.
-(void)adjustKeyFrame:(CMTime)timeRange;

/// Adjust the position of a keyframe while setting the time range of the keyframe to 0.
-(void)adjustKeyFrame;
```

NLEInterface
```Plain Text
/// Enable keyframe callback in the VE SDK for iOS.
- (void)enableKeyFrameCallback;

/// Register keyframe callback.
/// @param listener <#listener description#>
- (void)addKeyFrameListener:(id<NLEKeyFrameCallbackProtocol>)listener;


/// Update keyframe information to a specified slot.
/// @param AllKeyFrameInfo: The keyframe information.
/// @param pts: The position of the keyframe on the timeline.
/// @param slot: The slot to which you want to update the keyframe information.
- (NLETrackSlot_OC*)refreshAllKeyFrameInfo:(NLEAllKeyFrameInfo *)allKeyFrameInfo
                pts:(NSInteger)pts
                     inSlot:(NLETrackSlot_OC*)slot;


/// Obtain all the keyframe information at a specified position on the timeline.
/// @param time: Timestamp.
- (NLEAllKeyFrameInfo*)allKeyFrameInfoAtTime:(CMTime)time;
```

<span id="10777b38"></span>
### Procedure
<span id="6179e874"></span>
#### 1. Enable keyframe callback in the VE SDK for iOS
```Plain Text
/// Define properties for the NLE interface.
@property (nonatomic, weak) id<DVENLEInterfaceProtocol> nle;
/// Call the NLE interface by using a DI container.
DVEAutoInject(self.vcContext.serviceProvider, nle, DVENLEInterfaceProtocol)
/// Enable keyframe callback.
[self.nle enableKeyFrameCallback];
```

<span id="64c62165"></span>
#### 2. Register keyframe callback (taking a slot with a filter as an example)
Register callback in a DVEFilterEditor object.
```Plain Text
- (instancetype)initWithContext:(DVEVCContext *)context
{
  if(self = [super init]) {
    self.vcContext = context;
    [self.nle addKeyFrameListener:self];
  }
  return self;
}
```

Implement keyframe callback:

1. Obtain the currently selected slot with a filter.
2. Update the keyframe information to the slot.
3. Perform callback of the updated slot through keyFrameDelegate. The filter value at the current point in time is needed for slider-based update in the filter panel.

```Plain Text
- (void)nleDidChangedWithPTS:(CMTime)time keyFrameInfo:(NLEAllKeyFrameInfo *)info {
   
   
  NLETrackSlot_OC *slot = [self.vcContext.mediaContext currentBlendVideoSlotWithFilter];
  if(!slot) return;
   
  slot = [self.nle refreshAllKeyFrameInfo:info pts:self.vcContext.playerService.currentPlayerTime * USEC_PER_SEC inSlot:slot];
  if (self.keyFrameDelegate &&
    [self.keyFrameDelegate respondsToSelector:@selector(filterKeyFrameDidChangedWithSlot:)]) {
    [self.keyFrameDelegate filterKeyFrameDidChangedWithSlot:slot];
  }
}
```

<span id="6d2258c2"></span>
#### 3. Automatically add a keyframe after data modification (taking a slot with a filter as an example)
Before you commit an operation to change the filter value, call the addOrUpdateKeyframe interface to check the keyframes in the slot. To automatically add a keyframe, set the forceAdd parameter to NO.
```Plain Text
- (void)updatePartlyNLEFilter:(NSString *)identifier intensity:(CGFloat)intensity forSlot:(NLETrackSlot_OC *)slot needCommit:(BOOL)commit {
  if (!slot) return;
  NLEFilter_OC *findFilter = nil;
  NSMutableArray<NLEFilter_OC*>* filters = [slot getFilter];
  for (NLEFilter_OC *filter in filters) {
    NLESegmentFilter_OC *segFilter = filter.segmentFilter;
    NLEResourceNode_OC *resFilter = segFilter.effectSDKFilter;
    if ([resFilter.resourceId isEqualToString:identifier]) {
      findFilter = filter;
      [segFilter setIntensity:intensity];
      break;
    }
  }
   
  [slot addOrUpdateKeyframe:CMTimeMake(self.vcContext.playerService.currentPlayerTime * USEC_PER_SEC, USEC_PER_SEC)
          timeRange:[self.keyFrameEditor currentKeyframeTimeRange] forceAdd:NO];
   
  [self.actionService commitNLE:commit];
}
```

<span id="147fe6dd"></span>
#### Reverse, change the speed of, or adjust a slot
Before you commit an operation on a slot such as reversal, speed change, or duration adjustment, call the adjustKeyFrame interface to adjust the positions of the keyframes in the slot.
```Plain Text
- (void)reverseSlot:(NLETrackSlot_OC *)slot
          withAsset:(AVURLAsset *)asset
       forMainTrack:(BOOL)forMainTrack
    isReallyReverse:(BOOL)isReallyReverse
{
    NLETrack_OC *videoTrack = [self.nleEditor.nleModel trackContainSlotId:slot.nle_nodeId];
    if (![slot.segment isKindOfClass:NLESegmentVideo_OC.class]) {
        return;
    }
    // copy resource
    NSString *relativePath = [self.draftService copyResourceToDraft:asset.URL resourceType:NLEResourceTypeVideo];
    
    NLESegmentVideo_OC *segmentVideo = (NLESegmentVideo_OC *)slot.segment;
    
    CMTimeRange sourceTimeRange = slot.nle_sourceTimeRange;
    NLEResourceAV_OC *videoResource = [[NLEResourceAV_OC alloc] init];
    [videoResource nle_setupForVideo:asset];
    videoResource.resourceFile = relativePath;
    if (isReallyReverse) {
        segmentVideo.reversedAVFile = videoResource;
    } else {
        segmentVideo.videoFile = videoResource;
    }
    
    BOOL needUpdateTimeRange = segmentVideo.rewind != isReallyReverse;
    if (needUpdateTimeRange) {
        // ----s-------e-
        // -s-------e----
        CMTime sourceStart = CMTimeSubtract(segmentVideo.nle_resourceDuration, CMTimeRangeGetEnd(sourceTimeRange));
        CMTime sourceEnd = CMTimeSubtract(segmentVideo.nle_resourceDuration, sourceTimeRange.start);
        segmentVideo.timeClipStart = sourceStart;
        segmentVideo.timeClipEnd = sourceEnd;
    }
    
    if (forMainTrack) {
        [videoTrack nle_rescheduleTrackForTransitionChanged];
    }
    
    [segmentVideo setRewind:isReallyReverse];
    [slot adjustKeyFrame];
    
    self.vcContext.mediaContext.didReversedSlotID = slot.nle_nodeId;
}
```

<span id="98fc212b"></span>
#### Split a slot
You can split a slot for effect comparison. Before you split a slot, call the adjustKeyFrame interface and set a time range for the current keyframe.
```Plain Text
- (NLETrackSlot_OC *)splitForSlot:(NLETrackSlot_OC *)slot
{
    if (!slot) { return nil; }
    
    DVEMediaContext *mediaContext = self.vcContext.mediaContext;
    
    CMTime leftDuration = CMTimeSubtract(mediaContext.currentTime, slot.startTime);
    float scale = CMTimeGetSeconds(slot.duration) == 0 ? 0 : CMTimeGetSeconds(leftDuration) / CMTimeGetSeconds(slot.duration);
    
    NLEModel_OC *model = self.nleEditor.nleModel;
    NLETrack_OC *track = [model trackContainSlotId:slot.nle_nodeId];
    
    [slot adjustKeyFrame:[self.keyFrameEditor currentKeyframeTimeRange]];
    NLETrackSlot_OC *newSlot = [track splitFromTime:CMTimeGetSeconds(mediaContext.currentTime) * USEC_PER_SEC];
    
    newSlot.startTime = mediaContext.currentTime;
    
    [self p_updateStickerAnimationDuration:scale slot:slot];
    [self p_updateStickerAnimationDuration:1 - scale slot:newSlot];
    
    [self.actionService commitNLE:YES];
    mediaContext.selectTextSlotAtCurrentTime = newSlot;
    
    return newSlot;
}
```

<span id="a3ef046e"></span>
### Actively add or delete a keyframe
To actively add a keyframe in a specified slot, call the addOrUpdateKeyframe interface and set the forceAdd parameter to YES. To delete a keyframe, call the removeKeyframe interface.
```Plain Text
-(void)actionKeyframe
{
  NLETrackSlot_OC* slot = [self currentSupportKeyframeSlot];
  CMTime time = CMTimeMake(self.vcContext.playerService.currentPlayerTime * USEC_PER_SEC, USEC_PER_SEC);
  if(self.keyframeButton.selected){
    if([slot addOrUpdateKeyframe:time timeRange:[self.keyFrameEditor currentKeyframeTimeRange] forceAdd:YES]){
      [self.actionService commitNLE:YES message:DVEEditorDoneEventAddKeyframe];
      [self showRemoveKeyframe];
    }
  }else{
    if([slot removeKeyframe:time timeRange:[self.keyFrameEditor currentKeyframeTimeRange]]){
      [self.actionService commitNLE:YES message:DVEEditorDoneEventRemoveKeyframe];
      [self showAddKeyframe];
    }
  }
}
```

<span id="82febc2f"></span>
#### Obtain the parameter values of a keyframe by calling the NLE interface
To actively update UI effects, you can obtain the information about the keyframe at a specified position on the timeline.
```Python
- (void)refreshMaskForKeyFrameIfNeed:(NLETrackSlot_OC*)slot {

    if (!slot || [slot getMask].count == 0) {
        return;
    }
    NLEAllKeyFrameInfo *keyFrameInfo = [self.nle keyFrameInfoAtTime:self.vcContext.mediaContext.currentTime];
    [self nleDidChangedWithPTS:self.vcContext.mediaContext.currentTime keyFrameInfo:keyFrameInfo];
}
```


```
