---
title: "FAQ - VE"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-faq-ve-v.4.0.2"
---

<span id="fc0b7e6c"></span>
## 1. The assets have no effects.


* Ensure that the app ID matches the license.

* Ensure that the asset resource package matches the license.

* Ensure that the license is not expired.

* Ensure that the specified asset path is correct.

* If the initialization is successful, check whether the corresponding file exists in the asset path of the beauty effects.

* Check whether the asset path is correctly set.


<span id="ef093b33"></span>
## 2. The audio and video lengths are inconsistent.

**Android**


1. After you call the **editor.initWithCanvas()**  method, run the following code:

   * editor.setTrackDurationType(TETrackType_Video, 0, TETrackDurationType_Fixed);

2. Add audio assets by using the addAudioTrack method:

   * public int addAudioTrack(String file, int trimIn, int trimOut, int sequenceIn, int sequenceOut, boolean isCycle, boolean needPrepare)

   * **After you set needPrepare to true, play the video again after you call the preceding method.** 

      For example,

   * If the recorded video is shorter than the BGM to be added, assume that the length of the video is 10s and that of the BGM is 15s, run the following code:


```Java
//  If the BGM is longer than the video, ensure that the trimOut of the audio asset is the same as the video length, that is 10s. trimOut cannot be set to -1.
editor.addAudioTrack(path, 0, 10*1000 , 0, 10*1000 ,  false , true )
```


Parameter description:

```PHP
/**
 * Add BGM
 * If needPrepare is set to true, after you call the API, the engine will be in the prepared state {@link VEState}
 * Note:  If you call this API to add a BGM, you can adjust the start time for playing the added BGM and the BGM play speed.
 * (trimOut-trimIn) / (sequenceOut - sequenceIn) != 1 : plays the BGM at a specified speed.
 *
 * @param file                     The full path of the BGM.
 * @param trimIn               The trimIn of the BGM, in milliseconds.
 * @param trimOut            The trimOut of the BGM, in milliseconds.
 * @param sequenceIn      The playback start time, in milliseconds.
 * @param sequenceOut  The playback end time, in milliseconds.
 * @param isCycle              Specifies whether to play the BGM throughout the video in loop mode.
 * @param needPrepare   Specifies whether the added BGM may change the overall length. If yes, set it to true. Then, play the video again from the start after the BGM is added.
 * @return                          Non-negative value: the trackindex that is added. Negative value: Failed to add ({@link VEResult}).
 * @since 2.1.0
 */
public int addAudioTrack(String file, int trimIn, int trimOut, int sequenceIn, int sequenceOut, boolean isCycle, boolean needPrepare)
```


**iOS**

Customize the audio clip length when you add the audio clip. That is, set the clipRang value of the audio clip.

```objectivec
// 1. Modify clipRang 
- (void)addAudioResource:(NSURL *)audioUrl audioName:(NSString *)audioName startTime:(NSTimeInterval)startTime Duration:(NSTimeInterval)duration
{
  AVURLAsset *asset = [AVURLAsset assetWithURL:audioUrl];
   
  //  NLE
  [self addAudioTrack:asset
    targetStartTime:self.mediaContext.currentTime
       audioName:audioName
        Duration:duration];

  IESMMVideoDataClipRange *clipRang = IESMMVideoDataClipRangeMakeV2(0, duration, self.editManager.currentPlayerTime, 0);
   
  [self.editManager hotAppendAudioAsset:asset withRange:clipRang];
   
  [self updateVideoDataMaxTrack];
}
// 2. Modify rang for NLE.
- (void)addAudioTrack:(AVURLAsset *)asset
   targetStartTime:(CMTime)targetStartTime
      audioName:(NSString *)audioName
       Duration:(NSTimeInterval)duration
{
  NSTimeInterval startTime = CMTimeGetSeconds(targetStartTime);
   
  NLETrack_OC *track = [[NLETrack_OC alloc] init];
  track.extraTrackType = NLETrackAUDIO;

  NLEResourceAV_OC *audioResource = [[NLEResourceAV_OC alloc] init];
  [audioResource setupForAudioWithAsset:asset];
  audioResource.name = audioName;
  audioResource.resourceFile = asset.URL.absoluteString.lastPathComponent;
   
  NLESegmentAudio_OC *audioSegment = [[NLESegmentAudio_OC alloc] init];
  audioSegment.audioFile = audioResource;
  audioSegment.timeClipStart = CMTimeMake(0 * USEC_PER_SEC, USEC_PER_SEC);
  audioSegment.timeClipEnd = CMTimeMake(duration * USEC_PER_SEC, USEC_PER_SEC);;
   
  NLETrackSlot_OC *trackSlot = [[NLETrackSlot_OC alloc] init];
  [trackSlot setSegmentAudio:audioSegment];
  trackSlot.startTime = CMTimeMake(startTime * USEC_PER_SEC, USEC_PER_SEC);
  trackSlot.duration = CMTimeMake(duration * USEC_PER_SEC, USEC_PER_SEC);
   

  [self.mediaContext addSlotsWithSlots:@[trackSlot] assets:@[asset] inTrack:track];
  [[self.mediaContext.editor getModel] addTrack:track];
   
  [self.slotMap setValue:asset forKey:trackSlot.slotID];

  [self commitNLE:YES];
}
```


<span id="b3ec06ed"></span>
## 3. The package is too large. How do I reduce its size?

**Android**


* If you cannot find the **model** files (under the **assets/model** directory) delivered along with the SDK, you can choose not to enclose these files in the APK to reduce the APK size.


```Java
android {
    buildTypes {
        release {
            aaptOptions {
                ignoreAssetsPattern '!model:'
            }
        }

        debug {
            aaptOptions {
                ignoreAssetsPattern '!model:'
            }
        }
        
    }
}
```



* The assets are distributed from the server end and can be downloaded when necessary.


**iOS**


* The assets are distributed from the server end and can be downloaded when necessary.

* The SDK uses the static library loading method.


<span id="e4872e1b"></span>
## 4. How do I hide the asset adding button in the track area?

**Android**

In EditToBActivity, call trackPanel.findViewById(R.id.ivAdd).setVisibility(View.GONE);

**iOS**

Set addButton to hide the button.

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/c6996aae570e43e7979fb429d0413ed2~tplv-em5hxbkur4-noop.image) </span>

<span id="679eb762"></span>
## 5. How do I set the capture, preview, and export resolutions?

**Android**


1. During initialization, you can make the following configurations:


```Java
// The capture and preview resolutions  
  // Set video recording.
    VEVideoEncodeSettings videoEncodeSettings = new VEVideoEncodeSettings.Builder(VEVideoEncodeSettings.USAGE_RECORD)
            .setVideoRes(720, 1280) // Video recording resolution.
            .build();

    // Set the preview resolution and policy.
    VEPreviewSettings previewSettings = new VEPreviewSettings.Builder()
            .setRenderSize(new VESize(720, 1280)) // Set the preview resolution, which is the render size of the SDK.
            .blockRenderExit(true)
            .enableCheckStatusWhenStopPreview(true)
            .build();  
```



2. To change the preview aspect ratio (such as 3:4 and 1:1), perform the following steps:


```Java
   VEDisplaySettings settings = new VEDisplaySettings.Builder()
                /**
                 *  Set the aspect ratio, that is, video height/width. For example, Width/Height = 18:9, then Ratio = 9.0f / 18 = 0.5f
                 */
               .setDisplayRatio(height * 1.0f / width)
               .build();
    // 1. Preview the result.
    recorder.setDisplaySettings(settings);
    // 2. Set the output video resolution, that is the resolution of the video to be exported.
    recorder.changeVideoOutputSize( 720 , 720 );
```


**iOS**

Perform the following steps to set the aspect ratio and resolution:

```objectivec
1. Configure for initialization.
_config = [[IESMMCameraConfig alloc] init];
_config.capturePreset        = AVCaptureSessionPreset1920x1080;//Set the resolution.
_config.captureRatio         = IESMMCaptureRatio9_16; //Set the aspect ratio.
2. Adjust the resolution.
For details, see Demo.
- (void)dealResolutionWithValue:(VEBarValue *)barValue
[self.recorder resetCapturePreset:self.curPreset then:^{}];
3. Adjust the aspect ratio.
For details, see Demo.
- (void)dealRatioWithValue:(VEBarValue *)barValue
[self ratioWithCommand:self.curRatio orientation:self.preDeviceOrientation];
4. Configure the export parameters.
For details, see Demo.
- (void)exportVideoWithVideoData:(HTSVideoData *)videodata Progress:(void (^_Nullable )(CGFloat progress))progressBlock resultBlock:(void (^)(NSError *error,id result))exportBlock
videoData.canvasSize = videodata.transParam.targetVideoSize;//Set this parameter.
```


<span id="5718c06e"></span>
## 6. The track area display is inconsistent with the slider. What can I do?

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/8ec67caf258b4dcfa8dc1cb0883e9352~tplv-em5hxbkur4-noop.image) </span>

The frame thumbnail displayed in the track area is a preview effect of a time point. Due to scaling, not all frames are displayed on the track. Frame thumbnails are displayed intermittently. Therefore, the video changes are not always displayed in thumbnails. You can pinch to zoom for higher precision.

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/5cc45f38bef649d6abf8bb97458a5969~tplv-em5hxbkur4-noop.image) </span>

<span id="324205fc"></span>
## 7. How do I add watermarks?

**Android**

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/c32f73791a654ac8b2f2575af9bd10f2~tplv-em5hxbkur4-noop.image) </span>

**iOS**


1. Add a common watermark, that is, a static image.


```Java
// Initialize the watermark.
UIImage *image = [UIImage imageNamed:@"logo"];
CGSize imageSize = CGSizeMake(image.size.width / config.outputSize.width, image.size.height / config.outputSize.height);
CGRect frame                  = CGRectMake(0.5, 0.5, imageSize.width, imageSize.height); // Note that the frames here are all ratios of the watermark image to the export video in size.
IESSticker *sticker = [IESSticker stickerWithImage:image frame:frame rotate:1 opaque:1.0];

//  Add the watermark to the recorder.
config.isRecordWithWaterMark = YES;
config.recorderSticker       = sticker;
```



2. Add an animation watermark.


```Java
//  Five images that form the Douyin logo.
UIImage *image0 = [UIImage imageNamed:@"logo0"];
UIImage *image1 = [UIImage imageNamed:@"logo1"];
UIImage *image2 = [UIImage imageNamed:@"logo2"];
UIImage *image3 = [UIImage imageNamed:@"logo3"];
UIImage *image4 = [UIImage imageNamed:@"logo4"];
// The key frames of the animation watermark, which specify the images to be displayed at the specific points in time.
IESStickerAnimation *animation = [[IESStickerAnimation alloc] init];
animation.frameTs              = @[[NSValue valueWithCMTime:CMTimeMake(000, 1000)],
                                   [NSValue valueWithCMTime:CMTimeMake(100, 1000)],
                                   [NSValue valueWithCMTime:CMTimeMake(200, 1000)],
                                   [NSValue valueWithCMTime:CMTimeMake(300, 1000)],
                                   [NSValue valueWithCMTime:CMTimeMake(400, 1000)]];
animation.values               = @[image0, image1, image2, image3, image4];
animation.repeatType           = kIESAnimationRepeatFromBegin;
animation.type                 = kIESStickerAttributeTypeImage;
animation.isAbsoluteFrameTs    = NO;
//  Initialize the watermark.
CGSize imageSize = CGSizeMake(image.size.width / config.outputSize.width, image.size.height / config.outputSize.height);
CGRect frame                  = CGRectMake(0.5, 0.5, imageSize.width, imageSize.height); // Note that the frames here are all ratios of the watermark image to the export video in size.
IESAnimationSticker *sticker = [IESAnimationSticker stickerWithImage:image frame:frame rotate:1 opaque:1.0];
[sticker addAnimation:animation];

// Add the watermark to the recorder.
config.isRecordWithWaterMark = YES;
config.recorderSticker       = sticker;
```
