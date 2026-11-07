---
title: "Viewer SDK for iOS: Callbacks"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-SDK-for-ios-callbacks"
---

<span id="BDLNetworkViaWWANViewDelegate"></span>
# BDLNetworkViaWWANViewDelegate

```objectivec
@protocol BDLNetworkViaWWANViewDelegate <NSObject>
```


The delegate methods for the mobile data access prompt view.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[networkViaWWANViewDidTouch:](https://docs.byteplus.com/en/docs/11/31215#BDLNetworkViaWWANViewDelegate-networkviawwanviewdidtouch) |


<span id="instructions"></span>
## Instructions

<span id="BDLNetworkViaWWANViewDelegate-networkviawwanviewdidtouch"></span>
### networkViaWWANViewDidTouch:

```objectivec
- (void)networkViaWWANViewDidTouch:(BDLNetworkViaWWANView *)wwanView;
```


The SDK calls this method when the system PiP mode fails to start.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|wwanView |BDLNetworkViaWWANView\* |The mobile data access prompt view. For more information, see [BDLNetworkViaWWANView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLNetworkViaWWANView). |


<span id="BDLPlayerSliderViewDelegate"></span>
# BDLPlayerSliderViewDelegate

```objectivec
@protocol BDLPlayerSliderViewDelegate <NSObject>
```


The delegate methods for the player progress bar view.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[sliderViewBeganDrag](https://docs.byteplus.com/en/docs/11/31215#BDLPlayerSliderViewDelegate-sliderviewbegandrag) |
|void |[sliderViewEndDrag](https://docs.byteplus.com/en/docs/11/31215#BDLPlayerSliderViewDelegate-sliderviewenddrag) |
|void |[sliderViewDidTap:](https://docs.byteplus.com/en/docs/11/31215#BDLPlayerSliderViewDelegate-sliderviewdidtap) |
|void |[sliderView:progressDidChange:](https://docs.byteplus.com/en/docs/11/31215#BDLPlayerSliderViewDelegate-sliderview-progressdidchange) |


<span id="instructions"></span>
## Instructions

<span id="BDLPlayerSliderViewDelegate-sliderviewbegandrag"></span>
### sliderViewBeganDrag

```objectivec
- (void)sliderViewBeganDrag;
```


The SDK calls this method when viewers start dragging the progress bar.

<span id="BDLPlayerSliderViewDelegate-sliderviewenddrag"></span>
### sliderViewEndDrag

```objectivec
- (void)sliderViewEndDrag;
```


The SDK calls this method when viewers stop dragging the progress bar.

<span id="BDLPlayerSliderViewDelegate-sliderviewdidtap"></span>
### sliderViewDidTap:

```objectivec
- (void)sliderViewDidTap:(BDLPlayerSliderView *)sliderView;
```


The SDK calls this method when viewers tap the progress bar view.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|sliderView |BDLPlayerSliderView\* |The player progress bar view. For more information, see [BDLPlayerSliderView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLPlayerSliderView). |


<span id="BDLPlayerSliderViewDelegate-sliderview-progressdidchange"></span>
### sliderView:progressDidChange:

```objectivec
- (void)sliderView:(BDLPlayerSliderView *)sliderView progressDidChange:(CGFloat)progress;
```


The SDK calls this method when the progress of the progress bar changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|sliderView |BDLPlayerSliderView\* |The player progress bar view. For more information, see [BDLPlayerSliderView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLPlayerSliderView). |
|progress |CGFloat |The current progress. Value range: [0,1]. |


<span id="BDLBasePlayerViewDelegate"></span>
# BDLBasePlayerViewDelegate

```objectivec
@protocol BDLBasePlayerViewDelegate <NSObject>
```


The delegate methods for the custom player view.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[basePlayerView:coverImageViewWillAppear:](https://docs.byteplus.com/en/docs/11/31215#BDLBasePlayerViewDelegate-baseplayerview-coverimageviewwillappear) |
|void |[basePlayerView:coverImageViewDidAppear:](https://docs.byteplus.com/en/docs/11/31215#BDLBasePlayerViewDelegate-baseplayerview-coverimageviewdidappear) |
|void |[basePlayerView:coverImageViewWillDisappear:](https://docs.byteplus.com/en/docs/11/31215#BDLBasePlayerViewDelegate-baseplayerview-coverimageviewwilldisappear) |
|void |[basePlayerView:coverImageViewDidDisappear:](https://docs.byteplus.com/en/docs/11/31215#BDLBasePlayerViewDelegate-baseplayerview-coverimageviewdiddisappear) |
|void |[basePlayerView:coverImageUrlDidChange:](https://docs.byteplus.com/en/docs/11/31215#BDLBasePlayerViewDelegate-baseplayerview-coverimageurldidchange) |
|void |[basePlayerView:coverImageDidChange:error:](https://docs.byteplus.com/en/docs/11/31215#BDLBasePlayerViewDelegate-baseplayerview-coverimagedidchange-error) |
|void |[basePlayerViewPlayerItemDidChange:isLive:willPlay:](https://docs.byteplus.com/en/docs/11/31215#BDLBasePlayerViewDelegate-baseplayerviewplayeritemdidchange-islive-willplay) |
|void |[basePlayerView:videoViewWillAppear:isLive:](https://docs.byteplus.com/en/docs/11/31215#BDLBasePlayerViewDelegate-baseplayerview-videoviewwillappear-islive) |
|void |[basePlayerView:videoViewDidAppear:isLive:](https://docs.byteplus.com/en/docs/11/31215#BDLBasePlayerViewDelegate-baseplayerview-videoviewdidappear-islive) |
|void |[basePlayerView:videoViewWillDisappear:](https://docs.byteplus.com/en/docs/11/31215#BDLBasePlayerViewDelegate-baseplayerview-videoviewwilldisappear) |
|void |[basePlayerView:videoViewDidDisappear:](https://docs.byteplus.com/en/docs/11/31215#BDLBasePlayerViewDelegate-baseplayerview-videoviewdiddisappear) |
|void |[basePlayerView:videoSizeDidChange:](https://docs.byteplus.com/en/docs/11/31215#BDLBasePlayerViewDelegate-baseplayerview-videosizedidchange) |
|void |[basePlayerViewOnFirstVideoFrameRendered:](https://docs.byteplus.com/en/docs/11/31215#BDLBasePlayerViewDelegate-baseplayerviewonfirstvideoframerendered) |
|void |[basePlayerView:supportedVideoResolutionsDidChange:currentVideoResolution:](https://docs.byteplus.com/en/docs/11/31215#BDLBasePlayerViewDelegate-baseplayerview-supportedvideoresolutionsdidchange-currentvideoresolution) |
|void |[basePlayerViewStallStart:](https://docs.byteplus.com/en/docs/11/31215#BDLBasePlayerViewDelegate-baseplayerviewstallstart) |
|void |[basePlayerViewStallEnd:](https://docs.byteplus.com/en/docs/11/31215#BDLBasePlayerViewDelegate-baseplayerviewstallend) |
|void |[basePlayerViewDidSingleTap:](https://docs.byteplus.com/en/docs/11/31215#BDLBasePlayerViewDelegate-baseplayerviewdidsingletap) |
|void |[basePlayerViewDidDoubleTap:](https://docs.byteplus.com/en/docs/11/31215#BDLBasePlayerViewDelegate-baseplayerviewdiddoubletap) |
|void |[basePlayerViewWillStartPictureInPicture:](https://docs.byteplus.com/en/docs/11/31215#BDLBasePlayerViewDelegate-baseplayerviewwillstartpictureinpicture) |
|void |[basePlayerViewDidStartPictureInPicture:](https://docs.byteplus.com/en/docs/11/31215#BDLBasePlayerViewDelegate-baseplayerviewdidstartpictureinpicture) |
|void |[basePlayerView:failedToStartPictureInPictureWithError:](https://docs.byteplus.com/en/docs/11/31215#BDLBasePlayerViewDelegate-baseplayerview-failedtostartpictureinpicturewitherror) |
|void |[basePlayerViewWillStopPictureInPicture:](https://docs.byteplus.com/en/docs/11/31215#BDLBasePlayerViewDelegate-baseplayerviewwillstoppictureinpicture) |
|void |[basePlayerViewDidStopPictureInPicture:](https://docs.byteplus.com/en/docs/11/31215#BDLBasePlayerViewDelegate-baseplayerviewdidstoppictureinpicture) |
|void |[basePlayerView:liveLoadStateDidChange:](https://docs.byteplus.com/en/docs/11/31215#BDLBasePlayerViewDelegate-baseplayerview-liveloadstatedidchange) |
|void |[basePlayerView:livePlaybackStateDidChange:](https://docs.byteplus.com/en/docs/11/31215#BDLBasePlayerViewDelegate-baseplayerview-liveplaybackstatedidchange) |
|void |[basePlayerViewWillFetchVodUrl:](https://docs.byteplus.com/en/docs/11/31215#BDLBasePlayerViewDelegate-baseplayerviewwillfetchvodurl) |
|void |[basePlayerViewDidFetchVodUrl:error:](https://docs.byteplus.com/en/docs/11/31215#BDLBasePlayerViewDelegate-baseplayerviewdidfetchvodurl-error) |
|void |[basePlayerView:vodDidFinishWithError:](https://docs.byteplus.com/en/docs/11/31215#BDLBasePlayerViewDelegate-baseplayerview-voddidfinishwitherror) |
|void |[basePlayerView:vodLoadStateDidChange:](https://docs.byteplus.com/en/docs/11/31215#BDLBasePlayerViewDelegate-baseplayerview-vodloadstatedidchange) |
|void |[basePlayerView:vodPlaybackStateDidChange:](https://docs.byteplus.com/en/docs/11/31215#BDLBasePlayerViewDelegate-baseplayerview-vodplaybackstatedidchange) |
|void |[basePlayerView:vodRetryForError:](https://docs.byteplus.com/en/docs/11/31215#BDLBasePlayerViewDelegate-baseplayerview-vodretryforerror) |
|void |[basePlayerView:onVodAutoContinuePlayback:](https://docs.byteplus.com/en/docs/11/31215#BDLBasePlayerViewDelegate-baseplayerview-onvodautocontinueplayback) |
|void |[basePlayerView:onUserForceOffline:](https://docs.byteplus.com/en/docs/11/31215#BDLBasePlayerViewDelegate-baseplayerview-onuserforceoffline) |


<span id="instructions"></span>
## Instructions

<span id="BDLBasePlayerViewDelegate-baseplayerview-coverimageviewwillappear"></span>
### basePlayerView:coverImageViewWillAppear:

```objectivec
- (void)basePlayerView:(BDLBasePlayerView *)basePlayerView coverImageViewWillAppear:(UIImageView *)coverImageView;
```


The SDK calls this method when the live cover is about to appear.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|basePlayerView |BDLBasePlayerView\* |The custom player view. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLBasePlayerView). |
|coverImageView |UIImageView\* |The live cover view. |


<span id="BDLBasePlayerViewDelegate-baseplayerview-coverimageviewdidappear"></span>
### basePlayerView:coverImageViewDidAppear:

```objectivec
- (void)basePlayerView:(BDLBasePlayerView *)basePlayerView coverImageViewDidAppear:(UIImageView *)coverImageView;
```


The SDK calls this method when the live cover appears.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|basePlayerView |BDLBasePlayerView\* |The custom player view. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLBasePlayerView). |
|coverImageView |UIImageView\* |The live cover view. |


<span id="BDLBasePlayerViewDelegate-baseplayerview-coverimageviewwilldisappear"></span>
### basePlayerView:coverImageViewWillDisappear:

```objectivec
- (void)basePlayerView:(BDLBasePlayerView *)basePlayerView coverImageViewWillDisappear:(UIImageView *)coverImageView;
```


The SDK calls this method when the live cover is about to disappear.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|basePlayerView |BDLBasePlayerView\* |The custom player view. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLBasePlayerView). |
|coverImageView |UIImageView\* |The live cover view. |


<span id="BDLBasePlayerViewDelegate-baseplayerview-coverimageviewdiddisappear"></span>
### basePlayerView:coverImageViewDidDisappear:

```objectivec
- (void)basePlayerView:(BDLBasePlayerView *)basePlayerView coverImageViewDidDisappear:(UIImageView *)coverImageView;
```


The SDK calls this method when the live cover disappears.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|basePlayerView |BDLBasePlayerView\* |The custom player view. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLBasePlayerView). |
|coverImageView |UIImageView\* |The live cover view. |


<span id="BDLBasePlayerViewDelegate-baseplayerview-coverimageurldidchange"></span>
### basePlayerView:coverImageUrlDidChange:

```objectivec
- (void)basePlayerView:(BDLBasePlayerView *)basePlayerView coverImageUrlDidChange:(nullable NSString *)url;
```


The SDK calls this method when the live cover changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|basePlayerView |BDLBasePlayerView\* |The custom player view. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLBasePlayerView). |
|url |nullable NSString\* |The URL of the current live cover image. |


<span id="BDLBasePlayerViewDelegate-baseplayerview-coverimagedidchange-error"></span>
### basePlayerView:coverImageDidChange:error:

```objectivec
- (void)basePlayerView:(BDLBasePlayerView *)basePlayerView coverImageDidChange:(nullable UIImage *)image error:(nullable NSError *)error;
```


The SDK calls this method when the live cover changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|basePlayerView |BDLBasePlayerView\* |The custom player view. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLBasePlayerView). |
|image |nullable UIImage\* |The current live cover image. |
|error |nullable NSError\* |The error information. If this parameter has a value, it means that getting the new live cover image failed, and the previous cover image is used instead. |


<span id="BDLBasePlayerViewDelegate-baseplayerviewplayeritemdidchange-islive-willplay"></span>
### basePlayerViewPlayerItemDidChange:isLive:willPlay:

```objectivec
- (void)basePlayerViewPlayerItemDidChange:(BDLBasePlayerView *)basePlayerView isLive:(BOOL)isLive willPlay:(BOOL)willPlay;
```


The SDK calls this method when the media content changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|basePlayerView |BDLBasePlayerView\* |The custom player view. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLBasePlayerView). |
|isLive |BOOL |Whether it is a live stream.<br><br><br>* `YES`: A live stream.<br><br>* `NO`: Not a live stream. |
|willPlay |BOOL |Whether the content is about to play.<br><br><br>* `YES`: About to play.<br><br>* `NO`: Not about to play. |


<span id="BDLBasePlayerViewDelegate-baseplayerview-videoviewwillappear-islive"></span>
### basePlayerView:videoViewWillAppear:isLive:

```objectivec
- (void)basePlayerView:(BDLBasePlayerView *)basePlayerView videoViewWillAppear:(UIView *)videoView isLive:(BOOL)isLive;
```


The SDK calls this method when the player is about to display.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|basePlayerView |BDLBasePlayerView\* |The custom player view. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLBasePlayerView). |
|videoView |UIView\* |The player view. |
|isLive |BOOL |Whether it is a live stream.<br><br><br>* `YES`: A live stream.<br><br>* `NO`: Not a live stream. |


<span id="BDLBasePlayerViewDelegate-baseplayerview-videoviewdidappear-islive"></span>
### basePlayerView:videoViewDidAppear:isLive:

```objectivec
- (void)basePlayerView:(BDLBasePlayerView *)basePlayerView videoViewDidAppear:(UIView *)videoView isLive:(BOOL)isLive;
```


The SDK calls this method when the player appears.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|basePlayerView |BDLBasePlayerView\* |The custom player view. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLBasePlayerView). |
|videoView |UIView\* |The player view. |
|isLive |BOOL |Whether it is a live stream.<br><br><br>* `YES`: A live stream.<br><br>* `NO`: Not a live stream. |


<span id="BDLBasePlayerViewDelegate-baseplayerview-videoviewwilldisappear"></span>
### basePlayerView:videoViewWillDisappear:

```objectivec
- (void)basePlayerView:(BDLBasePlayerView *)basePlayerView videoViewWillDisappear:(UIView *)videoView;
```


The SDK calls this method when the player is about to disappear.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|basePlayerView |BDLBasePlayerView\* |The custom player view. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLBasePlayerView). |
|videoView |UIView\* |The player view. |


<span id="BDLBasePlayerViewDelegate-baseplayerview-videoviewdiddisappear"></span>
### basePlayerView:videoViewDidDisappear:

```objectivec
- (void)basePlayerView:(BDLBasePlayerView *)basePlayerView videoViewDidDisappear:(UIView *)videoView;
```


The SDK calls this method when the player disappears.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|basePlayerView |BDLBasePlayerView\* |The custom player view. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLBasePlayerView). |
|videoView |UIView\* |The player view. |


<span id="BDLBasePlayerViewDelegate-baseplayerview-videosizedidchange"></span>
### basePlayerView:videoSizeDidChange:

```objectivec
- (void)basePlayerView:(BDLBasePlayerView *)basePlayerView videoSizeDidChange:(CGSize)videoSize;
```


The SDK calls this method when the video size changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|basePlayerView |BDLBasePlayerView\* |The custom player view. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLBasePlayerView). |
|videoSize |CGSize |The current video size. |


<span id="BDLBasePlayerViewDelegate-baseplayerviewonfirstvideoframerendered"></span>
### basePlayerViewOnFirstVideoFrameRendered:

```objectivec
- (void)basePlayerViewOnFirstVideoFrameRendered:(BDLBasePlayerView *)basePlayerView;
```


Call this method after the first frame of the video is rendered.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|basePlayerView |BDLBasePlayerView\* |The custom player view. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLBasePlayerView). |


<span id="BDLBasePlayerViewDelegate-baseplayerview-supportedvideoresolutionsdidchange-currentvideoresolution"></span>
### basePlayerView:supportedVideoResolutionsDidChange:currentVideoResolution:

```objectivec
- (void)basePlayerView:(BDLBasePlayerView *)basePlayerView supportedVideoResolutionsDidChange:(NSArray<NSNumber *> *)supportedVideoResolutions currentVideoResolution:(BDLVideoResolution)currentVideoResolution;
```


The SDK calls this method when the supported video resolutions change.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|basePlayerView |BDLBasePlayerView\* |The custom player view. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLBasePlayerView). |
|supportedVideoResolutions |NSArray<NSNumber\*\>\* |The currently supported video resolutions. |
|currentVideoResolution |BDLVideoResolution |The currently used resolution. For more information, see [BDLVideoResolution](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLVideoResolution). |


<span id="BDLBasePlayerViewDelegate-baseplayerviewstallstart"></span>
### basePlayerViewStallStart:

```objectivec
- (void)basePlayerViewStallStart:(BDLBasePlayerView *)basePlayerView;
```


The SDK calls this method when the video starts stuttering.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|basePlayerView |BDLBasePlayerView\* |The custom player view. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLBasePlayerView). |


<span id="BDLBasePlayerViewDelegate-baseplayerviewstallend"></span>
### basePlayerViewStallEnd:

```objectivec
- (void)basePlayerViewStallEnd:(BDLBasePlayerView *)basePlayerView;
```


The SDK calls this method when the video stuttering ends.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|basePlayerView |BDLBasePlayerView\* |The custom player view. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLBasePlayerView). |


<span id="BDLBasePlayerViewDelegate-baseplayerviewdidsingletap"></span>
### basePlayerViewDidSingleTap:

```objectivec
- (void)basePlayerViewDidSingleTap:(BDLBasePlayerView *)basePlayerView;
```


The SDK calls this method when viewers tap the player.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|basePlayerView |BDLBasePlayerView\* |The custom player view. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLBasePlayerView). |


<span id="BDLBasePlayerViewDelegate-baseplayerviewdiddoubletap"></span>
### basePlayerViewDidDoubleTap:

```objectivec
- (void)basePlayerViewDidDoubleTap:(BDLBasePlayerView *)basePlayerView;
```


The SDK calls this method when viewers double\-tap the player.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|basePlayerView |BDLBasePlayerView\* |The custom player view. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLBasePlayerView). |


<span id="BDLBasePlayerViewDelegate-baseplayerviewwillstartpictureinpicture"></span>
### basePlayerViewWillStartPictureInPicture:

```objectivec
- (void)basePlayerViewWillStartPictureInPicture:(BDLBasePlayerView *)basePlayerView;
```


The SDK calls this method when the system picture\-in\-picture (PiP) mode is about to start.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|basePlayerView |BDLBasePlayerView\* |The custom player view. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLBasePlayerView). |


<span id="BDLBasePlayerViewDelegate-baseplayerviewdidstartpictureinpicture"></span>
### basePlayerViewDidStartPictureInPicture:

```objectivec
- (void)basePlayerViewDidStartPictureInPicture:(BDLBasePlayerView *)basePlayerView;
```


The SDK calls this method when the system PiP mode starts.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|basePlayerView |BDLBasePlayerView\* |The custom player view. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLBasePlayerView). |


<span id="BDLBasePlayerViewDelegate-baseplayerview-failedtostartpictureinpicturewitherror"></span>
### basePlayerView:failedToStartPictureInPictureWithError:

```objectivec
- (void)basePlayerView:(BDLBasePlayerView *)basePlayerView failedToStartPictureInPictureWithError:(NSError *)error;
```


The SDK calls this method when the system PiP mode fails to start.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|basePlayerView |BDLBasePlayerView\* |The custom player view. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLBasePlayerView). |
|error |NSError\* |The error information. |


<span id="BDLBasePlayerViewDelegate-baseplayerviewwillstoppictureinpicture"></span>
### basePlayerViewWillStopPictureInPicture:

```objectivec
- (void)basePlayerViewWillStopPictureInPicture:(BDLBasePlayerView *)basePlayerView;
```


The SDK calls this method when the system PiP mode is about to stop.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|basePlayerView |BDLBasePlayerView\* |The custom player view. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLBasePlayerView). |


<span id="BDLBasePlayerViewDelegate-baseplayerviewdidstoppictureinpicture"></span>
### basePlayerViewDidStopPictureInPicture:

```objectivec
- (void)basePlayerViewDidStopPictureInPicture:(BDLBasePlayerView *)basePlayerView;
```


The SDK calls this method when the system PiP mode stops.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|basePlayerView |BDLBasePlayerView\* |The custom player view. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLBasePlayerView). |


<span id="BDLBasePlayerViewDelegate-baseplayerview-liveloadstatedidchange"></span>
### basePlayerView:liveLoadStateDidChange:

```objectivec
- (void)basePlayerView:(BDLBasePlayerView *)basePlayerView liveLoadStateDidChange:(BDLPlayerLoadState)loadState;
```


The SDK calls this method when the live stream loading status changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|basePlayerView |BDLBasePlayerView\* |The custom player view. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLBasePlayerView). |
|loadState |BDLPlayerLoadState |The current loading status of the player. For more information, see [BDLPlayerLoadState](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerLoadState).<br><br>If the value is `BDLPlayerLoadStateError`, you can get specific error information through [liveError](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLBasePlayerView-liveerror). |


<span id="BDLBasePlayerViewDelegate-baseplayerview-liveplaybackstatedidchange"></span>
### basePlayerView:livePlaybackStateDidChange:

```objectivec
- (void)basePlayerView:(BDLBasePlayerView *)basePlayerView livePlaybackStateDidChange:(BDLPlayerState)playbackState;
```


The SDK calls this method when the live player status changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|basePlayerView |BDLBasePlayerView\* |The custom player view. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLBasePlayerView). |
|playbackState |BDLPlayerState |The current live player status. For more information, see [BDLPlayerState](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerState). |


<span id="BDLBasePlayerViewDelegate-baseplayerviewwillfetchvodurl"></span>
### basePlayerViewWillFetchVodUrl:

```objectivec
- (void)basePlayerViewWillFetchVodUrl:(BDLBasePlayerView *)basePlayerView;
```


The SDK calls this method when the Video\-on\-Demand (VOD) video URL is about to be obtained.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|basePlayerView |BDLBasePlayerView\* |The custom player view. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLBasePlayerView). |


<span id="BDLBasePlayerViewDelegate-baseplayerviewdidfetchvodurl-error"></span>
### basePlayerViewDidFetchVodUrl:error:

```objectivec
- (void)basePlayerViewDidFetchVodUrl:(BDLBasePlayerView *)basePlayerView error:(nullable NSError *)error;
```


The SDK calls this method when the VOD video URL is obtained.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|basePlayerView |BDLBasePlayerView\* |The custom player view. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLBasePlayerView). |
|error |nullable NSError\* |The error information. If this parameter has a value, it means that getting the URL failed. |


<span id="BDLBasePlayerViewDelegate-baseplayerview-voddidfinishwitherror"></span>
### basePlayerView:vodDidFinishWithError:

```objectivec
- (void)basePlayerView:(BDLBasePlayerView *)basePlayerView vodDidFinishWithError:(nullable NSError *)error;
```


The SDK calls this method when the VOD video finishes playing.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|basePlayerView |BDLBasePlayerView\* |The custom player view. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLBasePlayerView). |
|error |nullable NSError\* |The error information. If this parameter has a value, it means that the playing failed. |


<span id="BDLBasePlayerViewDelegate-baseplayerview-vodloadstatedidchange"></span>
### basePlayerView:vodLoadStateDidChange:

```objectivec
- (void)basePlayerView:(BDLBasePlayerView *)basePlayerView vodLoadStateDidChange:(TTVideoEngineLoadState)loadState;
```


The SDK calls this method when the VOD loading status changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|basePlayerView |BDLBasePlayerView\* |The custom player view. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLBasePlayerView). |
|loadState |TTVideoEngineLoadState |The current VOD loading status. |


<span id="BDLBasePlayerViewDelegate-baseplayerview-vodplaybackstatedidchange"></span>
### basePlayerView:vodPlaybackStateDidChange:

```objectivec
- (void)basePlayerView:(BDLBasePlayerView *)basePlayerView vodPlaybackStateDidChange:(TTVideoEnginePlaybackState)playbackState;
```


The SDK calls this method when the VOD playback status changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|basePlayerView |BDLBasePlayerView\* |The custom player view. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLBasePlayerView). |
|playbackState |TTVideoEnginePlaybackState |The current VOD playback status. |


<span id="BDLBasePlayerViewDelegate-baseplayerview-vodretryforerror"></span>
### basePlayerView:vodRetryForError:

```objectivec
- (void)basePlayerView:(BDLBasePlayerView *)basePlayerView vodRetryForError:(NSError *)error;
```


The SDK calls this method when VOD playback failed and a retry is about to occur.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|basePlayerView |BDLBasePlayerView\* |The custom player view. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLBasePlayerView). |
|error |NSError\* |The error information. |


<span id="BDLBasePlayerViewDelegate-baseplayerview-onvodautocontinueplayback"></span>
### basePlayerView:onVodAutoContinuePlayback:

```objectivec
- (void)basePlayerView:(BDLBasePlayerView *)basePlayerView onVodAutoContinuePlayback:(NSTimeInterval)playbackTime;
```


The SDK calls this method when a VOD video automatically resumes playing from the point where it stopped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|basePlayerView |BDLBasePlayerView\* |The custom player view. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLBasePlayerView). |
|playbackTime |NSTimeInterval |The position to which the video seeks after automatically resuming from where it stopped. Unit: seconds. |


<span id="BDLBasePlayerViewDelegate-baseplayerview-onuserforceoffline"></span>
### basePlayerView:onUserForceOffline:

```objectivec
- (void)basePlayerView:(BDLBasePlayerView *)basePlayerView onUserForceOffline:(BDLForceOfflineInfo *)info;
```


The SDK calls this method when viewers are forcibly removed from the live room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|basePlayerView |BDLBasePlayerView\* |The custom player view. For more information, see [BDLBasePlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLBasePlayerView). |
|info |BDLForceOfflineInfo\* |The reason for viewers being forcibly removed from the live room. For more information, see [BDLForceOfflineInfo](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLForceOfflineInfo). |


<span id="BDLLivePullViewControllerDelegate"></span>
# BDLLivePullViewControllerDelegate

```objectivec
@protocol BDLLivePullViewControllerDelegate <NSObject>
```


The delegate methods for the full\-featured live room.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[livePullViewControllerWillLeaveLiveRoom:](https://docs.byteplus.com/en/docs/11/31215#BDLLivePullViewControllerDelegate-livepullviewcontrollerwillleaveliveroom) |
|void |[livePullViewControllerDidLoad:](https://docs.byteplus.com/en/docs/11/31215#BDLLivePullViewControllerDelegate-livepullviewcontrollerdidload) |
|void |[livePullViewControllerWillAppear:](https://docs.byteplus.com/en/docs/11/31215#BDLLivePullViewControllerDelegate-livepullviewcontrollerwillappear) |
|void |[livePullViewControllerDidAppear:](https://docs.byteplus.com/en/docs/11/31215#BDLLivePullViewControllerDelegate-livepullviewcontrollerdidappear) |
|void |[livePullViewControllerWillDisappear:](https://docs.byteplus.com/en/docs/11/31215#BDLLivePullViewControllerDelegate-livepullviewcontrollerwilldisappear) |
|void |[livePullViewControllerDidDisappear:](https://docs.byteplus.com/en/docs/11/31215#BDLLivePullViewControllerDelegate-livepullviewcontrollerdiddisappear) |
|void |[livePullViewControllerWillDestroy:](https://docs.byteplus.com/en/docs/11/31215#BDLLivePullViewControllerDelegate-livepullviewcontrollerwilldestroy) |
|void |[livePullViewControllerEnterFullScreen:](https://docs.byteplus.com/en/docs/11/31215#BDLLivePullViewControllerDelegate-livepullviewcontrollerenterfullscreen) |
|void |[livePullViewControllerLeaveFullScreen:](https://docs.byteplus.com/en/docs/11/31215#BDLLivePullViewControllerDelegate-livepullviewcontrollerleavefullscreen) |
|void |[livePullViewController:showCustomLanguageSelectionView:currentSelectedType:confirm:](https://docs.byteplus.com/en/docs/11/31215#BDLLivePullViewControllerDelegate-livepullviewcontroller-showcustomlanguageselectionview-currentselectedtype-confirm) |
|void |[livePullViewController:showCustomShareView:shareInfo:inviteTokenModel:](https://docs.byteplus.com/en/docs/11/31215#BDLLivePullViewControllerDelegate-livepullviewcontroller-showcustomshareview-shareinfo-invitetokenmodel) |
|void |[livePullViewController:didClickHeaderAd:floatingEnable:](https://docs.byteplus.com/en/docs/11/31215#BDLLivePullViewControllerDelegate-livepullviewcontroller-didclickheaderad-floatingenable) |


<span id="instructions"></span>
## Instructions

<span id="BDLLivePullViewControllerDelegate-livepullviewcontrollerwillleaveliveroom"></span>
### livePullViewControllerWillLeaveLiveRoom:

```objectivec
- (void)livePullViewControllerWillLeaveLiveRoom:(BDLLivePullViewController *)livePullVC;
```


The SDK calls this method when viewers are about to exit the full\-featured live room. You need to release references related to the full\-featured live room in this method.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|livePullVC |BDLLivePullViewController\* |The full\-featured live room. For more information, see [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController). |


<span id="BDLLivePullViewControllerDelegate-livepullviewcontrollerdidload"></span>
### livePullViewControllerDidLoad:

```objectivec
- (void)livePullViewControllerDidLoad:(BDLLivePullViewController *)livePullVC;
```


The SDK calls this method when the view corresponding to the full\-featured live room finishes loading, corresponding to the viewDidLoad lifecycle method.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|livePullVC |BDLLivePullViewController\* |The full\-featured live room. For more information, see [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController). |


<span id="BDLLivePullViewControllerDelegate-livepullviewcontrollerwillappear"></span>
### livePullViewControllerWillAppear:

```objectivec
- (void)livePullViewControllerWillAppear:(BDLLivePullViewController *)livePullVC;
```


The SDK calls this method when the view corresponding to the full\-featured live room is about to appear, corresponding to the viewWillAppear lifecycle method.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|livePullVC |BDLLivePullViewController\* |The full\-featured live room. For more information, see [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController). |


<span id="BDLLivePullViewControllerDelegate-livepullviewcontrollerdidappear"></span>
### livePullViewControllerDidAppear:

```objectivec
- (void)livePullViewControllerDidAppear:(BDLLivePullViewController *)livePullVC;
```


The SDK calls this method when the view corresponding to the full\-featured live room appears, corresponding to the viewDidAppear lifecycle method.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|livePullVC |BDLLivePullViewController\* |The full\-featured live room. For more information, see [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController). |


<span id="BDLLivePullViewControllerDelegate-livepullviewcontrollerwilldisappear"></span>
### livePullViewControllerWillDisappear:

```objectivec
- (void)livePullViewControllerWillDisappear:(BDLLivePullViewController *)livePullVC;
```


The SDK calls this method when the view corresponding to the full\-featured live room is about to disappear, corresponding to the viewWillDisappear lifecycle method.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|livePullVC |BDLLivePullViewController\* |The full\-featured live room. For more information, see [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController). |


<span id="BDLLivePullViewControllerDelegate-livepullviewcontrollerdiddisappear"></span>
### livePullViewControllerDidDisappear:

```objectivec
- (void)livePullViewControllerDidDisappear:(BDLLivePullViewController *)livePullVC;
```


The SDK calls this method when the view corresponding to the full\-featured live room disappears, corresponding to the viewDidDisappear lifecycle method.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|livePullVC |BDLLivePullViewController\* |The full\-featured live room. For more information, see [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController). |


<span id="BDLLivePullViewControllerDelegate-livepullviewcontrollerwilldestroy"></span>
### livePullViewControllerWillDestroy:

```objectivec
- (void)livePullViewControllerWillDestroy:(BDLLivePullViewController *)livePullVC;
```


The SDK calls this method when the view corresponding to the full\-featured live room is about to be destroyed, corresponding to the dealloc lifecycle method.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|livePullVC |BDLLivePullViewController\* |The full\-featured live room. For more information, see [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController). |


<span id="BDLLivePullViewControllerDelegate-livepullviewcontrollerenterfullscreen"></span>
### livePullViewControllerEnterFullScreen:

```objectivec
- (void)livePullViewControllerEnterFullScreen:(BDLLivePullViewController *)livePullVC;
```


The SDK calls this method when the player is about to enter full\-screen mode.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|livePullVC |BDLLivePullViewController\* |The full\-featured live room. For more information, see [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController). |


<span id="BDLLivePullViewControllerDelegate-livepullviewcontrollerleavefullscreen"></span>
### livePullViewControllerLeaveFullScreen:

```objectivec
- (void)livePullViewControllerLeaveFullScreen:(BDLLivePullViewController *)livePullVC;
```


The SDK calls this method when the player is about to exit full\-screen mode.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|livePullVC |BDLLivePullViewController\* |The full\-featured live room. For more information, see [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController). |


<span id="BDLLivePullViewControllerDelegate-livepullviewcontroller-showcustomlanguageselectionview-currentselectedtype-confirm"></span>
### livePullViewController:showCustomLanguageSelectionView:currentSelectedType:confirm:

```objectivec
- (void)livePullViewController:(BDLLivePullViewController *)livePullVC showCustomLanguageSelectionView:(NSArray<NSNumber *> *)languageTypes currentSelectedType:(BDLLanguageType)currentSelectedType confirm:(BDLLanguageConfirmBlock)confirmBlock;
```


The SDK calls this method when the language selection dialog box is displayed.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|livePullVC |BDLLivePullViewController\* |The full\-featured live room. For more information, see [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController). |
|languageTypes |NSArray<NSNumber\*\>\* |All the currently supported language types. |
|currentSelectedType |BDLLanguageType |The currently selected language. For more information, see [BDLLanguageType](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLLanguageType). |
|confirmBlock |BDLLanguageConfirmBlock |The callback triggered when a language is selected. For more information, see [BDLLanguageConfirmBlock](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#bdllanguageconfirmblock). |


<span id="BDLLivePullViewControllerDelegate-livepullviewcontroller-showcustomshareview-shareinfo-invitetokenmodel"></span>
### livePullViewController:showCustomShareView:shareInfo:inviteTokenModel:

```objectivec
- (void)livePullViewController:(BDLLivePullViewController *)livePullVC
           showCustomShareView:(NSString *)shareLink
                     shareInfo:(BDLGetShareInfoResult *)shareInfo
              inviteTokenModel:(nullable BDLGetInviteTokenResult *)inviteTokenModel;
```


The SDK calls this method when viewers tap the share button.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|livePullVC |BDLLivePullViewController\* |The full\-featured live room. For more information, see [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController). |
|shareLink |NSString\* |The shared address. |
|shareInfo |BDLGetShareInfoResult\* |The sharing information. For more information, see [BDLGetShareInfoResult](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLGetShareInfoResult). |
|inviteTokenModel |nullable BDLGetInviteTokenResult\* |The exclusive invitation information of the current viewer. For more information, see [BDLGetInviteTokenResult](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLGetInviteTokenResult). |


<span id="BDLLivePullViewControllerDelegate-livepullviewcontroller-didclickheaderad-floatingenable"></span>
### livePullViewController:didClickHeaderAd:floatingEnable:

```objectivec
- (void)livePullViewController:(BDLLivePullViewController *)livePullVC didClickHeaderAd:(NSString *)url floatingEnable:(BOOL)floatingEnable;
```


The SDK calls this method when viewers tap the header ad.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|livePullVC |BDLLivePullViewController\* |The full\-featured live room. For more information, see [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController). |
|url |NSString\* |The embedded link of the header ad. |
|floatingEnable |BOOL |Whether the ad is displayed on a floating page in the live room.<br><br><br>* `YES`: The ad is displayed on a floating page in the live room. Viewers can watch the video and view the ad at the same time.<br><br>* `NO`: The ad is displayed on a new browser tab. Viewers cannot watch the video and view the ad at the same time. |


<span id="BDLPlayerViewDelegate"></span>
# BDLPlayerViewDelegate

```objectivec
@protocol BDLPlayerViewDelegate <NSObject>
```


The delegate methods for the player view.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[playerView:controlViewIsAppear:](https://docs.byteplus.com/en/docs/11/31215#BDLPlayerViewDelegate-playerview-controlviewisappear) |
|void |[playerView:didFinishPlayingWithIsLive:](https://docs.byteplus.com/en/docs/11/31215#BDLPlayerViewDelegate-playerview-didfinishplayingwithislive) |
|void |[playerView:fullScreenButtonDidTouch:](https://docs.byteplus.com/en/docs/11/31215#BDLPlayerViewDelegate-playerview-fullscreenbuttondidtouch) |
|void |[playerView:videoSizeDidChange:](https://docs.byteplus.com/en/docs/11/31215#BDLPlayerViewDelegate-playerview-videosizedidchange) |
|void |[playerView:coverImageDidChange:error:](https://docs.byteplus.com/en/docs/11/31215#BDLPlayerViewDelegate-playerview-coverimagedidchange-error) |
|void |[playerViewDidSingleTap:](https://docs.byteplus.com/en/docs/11/31215#BDLPlayerViewDelegate-playerviewdidsingletap) |
|void |[playerViewPlayerItemDidChange:isLive:willPlay:](https://docs.byteplus.com/en/docs/11/31215#BDLPlayerViewDelegate-playerviewplayeritemdidchange-islive-willplay) |
|void |[playerView:onUserForceOffline:](https://docs.byteplus.com/en/docs/11/31215#BDLPlayerViewDelegate-playerview-onuserforceoffline) |


<span id="instructions"></span>
## Instructions

<span id="BDLPlayerViewDelegate-playerview-controlviewisappear"></span>
### playerView:controlViewIsAppear:

```objectivec
- (void)playerView:(BDLPlayerView *)playerView controlViewIsAppear:(BOOL)isAppear;
```


The SDK calls this method when the control view appears or disappears.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|playerView |BDLPlayerView\* |The player view. For more information, see [BDLPlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLPlayerView). |
|isAppear |BOOL |Whether to display the control view.<br><br><br>* `YES`: Display.<br><br>* `NO`: Do not display. |


<span id="BDLPlayerViewDelegate-playerview-didfinishplayingwithislive"></span>
### playerView:didFinishPlayingWithIsLive:

```objectivec
- (void)playerView:(BDLPlayerView *)playerView didFinishPlayingWithIsLive:(BOOL)isLive;
```


The SDK calls this method when the video finishes playing.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|playerView |BDLPlayerView\* |The player view. For more information, see [BDLPlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLPlayerView). |
|isLive |BOOL |Whether it is a live stream.<br><br><br>* `YES`: A live stream.<br><br>* `NO`: Not a live stream. |


<span id="BDLPlayerViewDelegate-playerview-fullscreenbuttondidtouch"></span>
### playerView:fullScreenButtonDidTouch:

```objectivec
- (void)playerView:(BDLPlayerView *)playerView fullScreenButtonDidTouch:(BOOL)isSelected;
```


The SDK calls this method when viewers tap the button to enter or exit full\-screen mode.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|playerView |BDLPlayerView\* |The player view. For more information, see [BDLPlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLPlayerView). |
|isSelected |BOOL |Whether viewers tap the button to enter full\-screen mode.<br><br><br>* `YES`: Tap the button to enter full\-screen mode.<br><br>* `NO`: Tap the button to exit full\-screen mode. |


<span id="BDLPlayerViewDelegate-playerview-videosizedidchange"></span>
### playerView:videoSizeDidChange:

```objectivec
- (void)playerView:(BDLPlayerView *)playerView videoSizeDidChange:(CGSize)size;
```


The SDK calls this method when the video size changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|playerView |BDLPlayerView\* |The player view. For more information, see [BDLPlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLPlayerView). |
|size |CGSize |The current video size. |


<span id="BDLPlayerViewDelegate-playerview-coverimagedidchange-error"></span>
### playerView:coverImageDidChange:error:

```objectivec
- (void)playerView:(BDLPlayerView *)playerView coverImageDidChange:(nullable UIImage *)image error:(nullable NSError *)error;
```


The SDK calls this method when the live cover changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|playerView |BDLPlayerView\* |The player view. For more information, see [BDLPlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLPlayerView). |
|image |nullable UIImage\* |The current live cover image. |
|error |nullable NSError\* |The error information. If this parameter has a value, it means that getting the new live cover image failed, and the previous cover image is used instead. |


<span id="BDLPlayerViewDelegate-playerviewdidsingletap"></span>
### playerViewDidSingleTap:

```objectivec
- (void)playerViewDidSingleTap:(BDLPlayerView *)playerView;
```


The SDK calls this method when viewers tap the player.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|playerView |BDLPlayerView\* |The player view. For more information, see [BDLPlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLPlayerView). |


<span id="BDLPlayerViewDelegate-playerviewplayeritemdidchange-islive-willplay"></span>
### playerViewPlayerItemDidChange:isLive:willPlay:

```objectivec
- (void)playerViewPlayerItemDidChange:(BDLPlayerView *)playerView isLive:(BOOL)isLive willPlay:(BOOL)willPlay;
```


The SDK calls this method when the media content changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|playerView |BDLPlayerView\* |The player view. For more information, see [BDLPlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLPlayerView). |
|isLive |BOOL |Whether it is a live stream.<br><br><br>* `YES`: A live stream.<br><br>* `NO`: Not a live stream. |
|willPlay |BOOL |Whether the content is about to play.<br><br><br>* `YES`: About to play.<br><br>* `NO`: Not about to play. |


<span id="BDLPlayerViewDelegate-playerview-onuserforceoffline"></span>
### playerView:onUserForceOffline:

```objectivec
- (void)playerView:(BDLPlayerView *)playerView onUserForceOffline:(BDLForceOfflineInfo *)info;
```


The SDK calls this method when viewers are forcibly removed from the live room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|playerView |BDLPlayerView\* |The player view. For more information, see [BDLPlayerView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLPlayerView). |
|info |BDLForceOfflineInfo\* |The reason for viewers being forcibly removed from the live room. For more information, see [BDLForceOfflineInfo](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLForceOfflineInfo). |


<span id="BDLTopCommentViewDelegate"></span>
# BDLTopCommentViewDelegate

```objectivec
@protocol BDLTopCommentViewDelegate <NSObject>
```


The delegate methods for the pinned comment view.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[topCommentView:didClickNicknameWithComment:](https://docs.byteplus.com/en/docs/11/31215#BDLTopCommentViewDelegate-topcommentview-didclicknicknamewithcomment) |
|void |[topCommentView:didClickComment:](https://docs.byteplus.com/en/docs/11/31215#BDLTopCommentViewDelegate-topcommentview-didclickcomment) |


<span id="instructions"></span>
## Instructions

<span id="BDLTopCommentViewDelegate-topcommentview-didclicknicknamewithcomment"></span>
### topCommentView:didClickNicknameWithComment:

```objectivec
- (void)topCommentView:(BDLTopCommentView *)view didClickNicknameWithComment:(BDLCommentModel *)comment;
```


The SDK calls this method when viewers tap the comment's nickname.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|view |BDLTopCommentView\* |The pinned comment view. For more information, see [BDLTopCommentView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLTopCommentView). |
|comment |BDLCommentModel\* |The comment model. For more information, see [BDLCommentModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLCommentModel). |


<span id="BDLTopCommentViewDelegate-topcommentview-didclickcomment"></span>
### topCommentView:didClickComment:

```objectivec
- (void)topCommentView:(BDLTopCommentView *)view didClickComment:(BDLCommentModel *)comment;
```


The SDK calls this method when viewers tap the text comment or the blank area in the comment.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|view |BDLTopCommentView\* |The pinned comment view. For more information, see [BDLTopCommentView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLTopCommentView). |
|comment |BDLCommentModel\* |The comment model. For more information, see [BDLCommentModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLCommentModel). |


<span id="BDLPlayerResolutionViewDelegate"></span>
# BDLPlayerResolutionViewDelegate

```objectivec
@protocol BDLPlayerResolutionViewDelegate <NSObject>
```


The delegate methods for the resolution selection view.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[resolutionView:resolutionDidChange:](https://docs.byteplus.com/en/docs/11/31215#BDLPlayerResolutionViewDelegate-resolutionview-resolutiondidchange) |


<span id="instructions"></span>
## Instructions

<span id="BDLPlayerResolutionViewDelegate-resolutionview-resolutiondidchange"></span>
### resolutionView:resolutionDidChange:

```objectivec
- (void)resolutionView:(BDLPlayerResolutionView *)resolutionView resolutionDidChange:(BDLVideoResolution)resolution;
```


The SDK calls this method when the resolution changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|resolutionView |BDLPlayerResolutionView\* |The resolution selection view. For more information, see [BDLPlayerResolutionView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLPlayerResolutionView). |
|resolution |BDLVideoResolution |The currently used resolution. For more information, see [BDLVideoResolution](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLVideoResolution). |


<span id="BDLLoginProvider"></span>
# BDLLoginProvider

```objectivec
@protocol BDLLoginProvider <NSObject>
```


The live room delegate for custom login. Suitable for scenarios where the authentication mode is changed from public to custom. For more information, see [Custom authentication login](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the value of <a href="https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLActivity-authmode">authMode</a> is <code>BDLActivityAuthModePublic</code>, which means the authentication mode of the live room is public, and the <code>nickname</code> parameter value of the <a href="https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLUserInfoConfiguration-setnickname-complete">setNickname:complete:</a> method is not <code>nil</code>, then none of the delegate methods will be triggered.</div>


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[loginWithActivity:completion:](https://docs.byteplus.com/en/docs/11/31215#BDLLoginProvider-loginwithactivity-completion) |
|void |[loginComplete:error:](https://docs.byteplus.com/en/docs/11/31215#BDLLoginProvider-logincomplete-error) |
|void |[cancelLoginWithActivity:](https://docs.byteplus.com/en/docs/11/31215#BDLLoginProvider-cancelloginwithactivity) |


<span id="instructions"></span>
## Instructions

<span id="BDLLoginProvider-loginwithactivity-completion"></span>
### loginWithActivity:completion:

```objectivec
- (void)loginWithActivity:(BDLActivity *)activity completion:(void (^)(NSString * _Nullable token))completion;
```


Logs in to the live room in custom mode, allowing viewers to log in to the live room using your own account system.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|activity |BDLActivity\* |The live room information, which is passed in through the [joinLiveRoomWithActivity:success:failure:](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLiveEngine-joinliveroomwithactivity-success-failure) method. |
|completion |void(^)(NSString\* token) |The callback triggered after the custom login to the live room is complete, with no return value. Pass the `token` parameter for login user identity verification. |


<span id="BDLLoginProvider-logincomplete-error"></span>
### loginComplete:error:

```objectivec
- (void)loginComplete:(BDLActivity *)activity error:(NSError *)error;
```


The callback for custom login results.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|activity |BDLActivity\* |The live room information, which is passed in through the [joinLiveRoomWithActivity:success:failure:](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLiveEngine-joinliveroomwithactivity-success-failure) method. |
|error |NSError\* |The error information. If this parameter has a value, it means that the custom login failed. |


<span id="BDLLoginProvider-cancelloginwithactivity"></span>
### cancelLoginWithActivity:

```objectivec
- (void)cancelLoginWithActivity:(BDLActivity *)activity;
```


Cancels the custom login to the live room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|activity |BDLActivity\* |The live room information, which is passed in through the [joinLiveRoomWithActivity:success:failure:](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLiveEngine-joinliveroomwithactivity-success-failure) method. |


<span id="BDLPlayerReplayViewDelegate"></span>
# BDLPlayerReplayViewDelegate

```objectivec
@protocol BDLPlayerReplayViewDelegate <NSObject>
```


The delegate methods for the replay view.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[replayViewDidTouch:](https://docs.byteplus.com/en/docs/11/31215#BDLPlayerReplayViewDelegate-replayviewdidtouch) |
|void |[playerReplayView:replayButtonDidTouch:](https://docs.byteplus.com/en/docs/11/31215#BDLPlayerReplayViewDelegate-playerreplayview-replaybuttondidtouch) |


<span id="instructions"></span>
## Instructions

<span id="BDLPlayerReplayViewDelegate-replayviewdidtouch"></span>
### replayViewDidTouch:

```objectivec
- (void)replayViewDidTouch:(BDLPlayerReplayView *)replayView;
```


The SDK calls this method when viewers tap the replay interface in the live room in portrait mode.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|replayView |BDLPlayerReplayView\* |The replay view. For more information, see [BDLPlayerReplayView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLPlayerReplayView). |


<span id="BDLPlayerReplayViewDelegate-playerreplayview-replaybuttondidtouch"></span>
### playerReplayView:replayButtonDidTouch:

```objectivec
- (void)playerReplayView:(BDLPlayerReplayView *)replayView replayButtonDidTouch:(UIButton *)button;
```


The SDK calls this method when viewers tap the replay button in the live room in landscape mode.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|replayView |BDLPlayerReplayView\* |The replay view. For more information, see [BDLPlayerReplayView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLPlayerReplayView). |
|button |UIButton\* |The replay button. |


<span id="BDLNetworkNotReachableViewDelegate"></span>
# BDLNetworkNotReachableViewDelegate

```objectivec
@protocol BDLNetworkNotReachableViewDelegate <NSObject>
```


The delegate methods for the network disconnection prompt view.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[networkNotReachableView:retryButtonDidTouch:](https://docs.byteplus.com/en/docs/11/31215#BDLNetworkNotReachableViewDelegate-networknotreachableview-retrybuttondidtouch) |


<span id="instructions"></span>
## Instructions

<span id="BDLNetworkNotReachableViewDelegate-networknotreachableview-retrybuttondidtouch"></span>
### networkNotReachableView:retryButtonDidTouch:

```objectivec
- (void)networkNotReachableView:(BDLNetworkNotReachableView *)notReachableview retryButtonDidTouch:(UIButton *)button;
```


The SDK calls this method when viewers tap the retry button.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|notReachableview |BDLNetworkNotReachableView\* |The network disconnection prompt view. For more information, see [BDLNetworkNotReachableView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLNetworkNotReachableView). |
|button |UIButton\* |The retry button. |


<span id="BDLPlayerControlViewDelegate"></span>
# BDLPlayerControlViewDelegate

```objectivec
@protocol BDLPlayerControlViewDelegate <NSObject>
```


The delegate methods for the player control view.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[controlView:playButtonDidTouch:](https://docs.byteplus.com/en/docs/11/31215#BDLPlayerControlViewDelegate-controlview-playbuttondidtouch) |
|void |[controlViewSliderBeganDrag](https://docs.byteplus.com/en/docs/11/31215#BDLPlayerControlViewDelegate-controlviewsliderbegandrag) |
|void |[controlViewSliderEndDrag](https://docs.byteplus.com/en/docs/11/31215#BDLPlayerControlViewDelegate-controlviewsliderenddrag) |
|void |[controlViewSliderViewDidTap](https://docs.byteplus.com/en/docs/11/31215#BDLPlayerControlViewDelegate-controlviewsliderviewdidtap) |
|void |[controlView:progressDidChange:](https://docs.byteplus.com/en/docs/11/31215#BDLPlayerControlViewDelegate-controlview-progressdidchange) |
|void |[controlViewRefreshButtonDidTouch:](https://docs.byteplus.com/en/docs/11/31215#BDLPlayerControlViewDelegate-controlviewrefreshbuttondidtouch) |
|void |[controlViewResolutionButtonDidTouch:](https://docs.byteplus.com/en/docs/11/31215#BDLPlayerControlViewDelegate-controlviewresolutionbuttondidtouch) |
|void |[controlViewSpeedButtonDidTouch:](https://docs.byteplus.com/en/docs/11/31215#BDLPlayerControlViewDelegate-controlviewspeedbuttondidtouch) |
|void |[controlView:fullScreenButtonDidTouch:](https://docs.byteplus.com/en/docs/11/31215#BDLPlayerControlViewDelegate-controlview-fullscreenbuttondidtouch) |
|void |[controlView:resolutionDidChange:](https://docs.byteplus.com/en/docs/11/31215#BDLPlayerControlViewDelegate-controlview-resolutiondidchange) |


<span id="instructions"></span>
## Instructions

<span id="BDLPlayerControlViewDelegate-controlview-playbuttondidtouch"></span>
### controlView:playButtonDidTouch:

```objectivec
- (void)controlView:(BDLPlayerControlView *)controlView playButtonDidTouch:(BOOL)isSelected;
```


The SDK calls this method when viewers tap the play button.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|controlView |BDLPlayerControlView\* |The player control view. For more information, see [BDLPlayerControlView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLPlayerControlView). |
|isSelected |BOOL |Whether the play button is selected.<br><br><br>* `YES`: Selected, meaning the video is playing.<br><br>* `NO`: Not selected, meaning the video is paused. |


<span id="BDLPlayerControlViewDelegate-controlviewsliderbegandrag"></span>
### controlViewSliderBeganDrag

```objectivec
- (void)controlViewSliderBeganDrag;
```


The SDK calls this method when viewers start dragging the progress bar.

<span id="BDLPlayerControlViewDelegate-controlviewsliderenddrag"></span>
### controlViewSliderEndDrag

```objectivec
- (void)controlViewSliderEndDrag;
```


The SDK calls this method when viewers stop dragging the progress bar.

<span id="BDLPlayerControlViewDelegate-controlviewsliderviewdidtap"></span>
### controlViewSliderViewDidTap

```objectivec
- (void)controlViewSliderViewDidTap;
```


The SDK calls this method when viewers tap the progress bar.

<span id="BDLPlayerControlViewDelegate-controlview-progressdidchange"></span>
### controlView:progressDidChange:

```objectivec
- (void)controlView:(BDLPlayerControlView *)controlView progressDidChange:(CGFloat)progress;
```


The SDK calls this method when the playback progress changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|controlView |BDLPlayerControlView\* |The player control view. For more information, see [BDLPlayerControlView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLPlayerControlView). |
|progress |CGFloat |The current playback progress. Value range: [0,1]. |


<span id="BDLPlayerControlViewDelegate-controlviewrefreshbuttondidtouch"></span>
### controlViewRefreshButtonDidTouch:

```objectivec
- (void)controlViewRefreshButtonDidTouch:(BDLPlayerControlView *)controlView;
```


The SDK calls this method when viewers tap the refresh button during the live stream.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|controlView |BDLPlayerControlView\* |The player control view. For more information, see [BDLPlayerControlView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLPlayerControlView). |


<span id="BDLPlayerControlViewDelegate-controlviewresolutionbuttondidtouch"></span>
### controlViewResolutionButtonDidTouch:

```objectivec
- (void)controlViewResolutionButtonDidTouch:(BDLPlayerControlView *)controlView;
```


The SDK calls this method when viewers tap the resolution button.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|controlView |BDLPlayerControlView\* |The player control view. For more information, see [BDLPlayerControlView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLPlayerControlView). |


<span id="BDLPlayerControlViewDelegate-controlviewspeedbuttondidtouch"></span>
### controlViewSpeedButtonDidTouch:

```objectivec
- (void)controlViewSpeedButtonDidTouch:(BDLPlayerControlView *)controlView;
```


The SDK calls this method when viewers tap the playback speed button.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|controlView |BDLPlayerControlView\* |The player control view. For more information, see [BDLPlayerControlView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLPlayerControlView). |


<span id="BDLPlayerControlViewDelegate-controlview-fullscreenbuttondidtouch"></span>
### controlView:fullScreenButtonDidTouch:

```objectivec
- (void)controlView:(BDLPlayerControlView *)controlView fullScreenButtonDidTouch:(BOOL)isSelected;
```


The SDK calls this method when viewers tap the button to enter or exit full\-screen mode.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|controlView |BDLPlayerControlView\* |The player control view. For more information, see [BDLPlayerControlView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLPlayerControlView). |
|isSelected |BOOL |Whether viewers tap the button to enter full\-screen mode.<br><br><br>* `YES`: Tap the button to enter full\-screen mode.<br><br>* `NO`: Tap the button to exit full\-screen mode. |


<span id="BDLPlayerControlViewDelegate-controlview-resolutiondidchange"></span>
### controlView:resolutionDidChange:

```objectivec
- (void)controlView:(BDLPlayerControlView *)controlView resolutionDidChange:(BDLVideoResolution)resolution;
```


The SDK calls this method when the resolution changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|controlView |BDLPlayerControlView\* |The player control view. For more information, see [BDLPlayerControlView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLPlayerControlView). |
|resolution |BDLVideoResolution |The currently used resolution. For more information, see [BDLVideoResolution](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLVideoResolution). |


<span id="BDLLivePullViewControllerActionProvider"></span>
# BDLLivePullViewControllerActionProvider

```objectivec
@protocol BDLLivePullViewControllerActionProvider <NSObject>
```


The provider of full\-featured live room events.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[showLivePullViewController:](https://docs.byteplus.com/en/docs/11/31215#BDLLivePullViewControllerActionProvider-showlivepullviewcontroller) |
|void |[hideLivePullViewController:](https://docs.byteplus.com/en/docs/11/31215#BDLLivePullViewControllerActionProvider-hidelivepullviewcontroller) |
|BOOL |[livePullViewController:onCloseClick:](https://docs.byteplus.com/en/docs/11/31215#BDLLivePullViewControllerActionProvider-livepullviewcontroller-oncloseclick) |


<span id="instructions"></span>
## Instructions

<span id="BDLLivePullViewControllerActionProvider-showlivepullviewcontroller"></span>
### showLivePullViewController:

```objectivec
- (void)showLivePullViewController:(BDLLivePullViewController *)livePullVC;
```


Displays the full\-featured live room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|livePullVC |BDLLivePullViewController\* |The full\-featured live room to display. For more information, see [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController). |


<span id="BDLLivePullViewControllerActionProvider-hidelivepullviewcontroller"></span>
### hideLivePullViewController:

```objectivec
- (void)hideLivePullViewController:(BDLLivePullViewController *)livePullVC;
```


Hides the full\-featured live room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|livePullVC |BDLLivePullViewController\* |The full\-featured live room to hide. For more information, see [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController). |


<span id="BDLLivePullViewControllerActionProvider-livepullviewcontroller-oncloseclick"></span>
### livePullViewController:onCloseClick:

```objectivec
- (BOOL)livePullViewController:(BDLLivePullViewController *)livePullVC onCloseClick:(UIButton *)closeButton;
```


The SDK calls this method when viewers tap the close button of the full\-featured live room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|livePullVC |BDLLivePullViewController\* |The full\-featured live room. For more information, see [BDLLivePullViewController](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController). |
|closeButton |UIButton\* |The close button. |


**Return Value**

Whether to execute [defaultCloseAction](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLivePullViewController(BDLDefaultAction)-defaultcloseaction).


* `YES`: Execute.

* `NO`: Do not execute.

    &nbsp;


<span id="bdlfloatingplayerdelegate"></span>
# BDLFloatingPlayerDelegate

```objectivec
@protocol BDLFloatingPlayerDelegate <NSObject>
```


The delegate methods for the floating player (namely the in\-app PiP).

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[floatingPlayerWillAppear:](https://docs.byteplus.com/en/docs/11/31215#BDLFloatingPlayerDelegate-floatingplayerwillappear) |
|void |[floatingPlayerDidDisappear:](https://docs.byteplus.com/en/docs/11/31215#BDLFloatingPlayerDelegate-floatingplayerdiddisappear) |
|void |[floatingPlayerDidSingleTap:](https://docs.byteplus.com/en/docs/11/31215#BDLFloatingPlayerDelegate-floatingplayerdidsingletap) |
|void |[floatingPlayerDidDoubleTap:](https://docs.byteplus.com/en/docs/11/31215#BDLFloatingPlayerDelegate-floatingplayerdiddoubletap) |
|void |[floatingPlayerWillClose:](https://docs.byteplus.com/en/docs/11/31215#BDLFloatingPlayerDelegate-floatingplayerwillclose) |
|void |[floatingPlayer:onVodAutoContinuePlayback:](https://docs.byteplus.com/en/docs/11/31215#BDLFloatingPlayerDelegate-floatingplayer-onvodautocontinueplayback) |
|BOOL |[floatingPlayerDidClickClose:](https://docs.byteplus.com/en/docs/11/31215#BDLFloatingPlayerDelegate-floatingplayerdidclickclose) |
|void |[floatingPlayer:onUserForceOffline:](https://docs.byteplus.com/en/docs/11/31215#BDLFloatingPlayerDelegate-floatingplayer-onuserforceoffline) |


<span id="instructions"></span>
## Instructions

<span id="BDLFloatingPlayerDelegate-floatingplayerwillappear"></span>
### floatingPlayerWillAppear:

```objectivec
- (void)floatingPlayerWillAppear:(BDLFloatingPlayer *)floatingPlayer;
```


The SDK calls this method when the player is about to appear.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|floatingPlayer |BDLFloatingPlayer\* |The floating player. For more information, see [BDLFloatingPlayer](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLFloatingPlayer). |


<span id="BDLFloatingPlayerDelegate-floatingplayerdiddisappear"></span>
### floatingPlayerDidDisappear:

```objectivec
- (void)floatingPlayerDidDisappear:(BDLFloatingPlayer *)floatingPlayer;
```


The SDK calls this method when the player disappears.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|floatingPlayer |BDLFloatingPlayer\* |The floating player. For more information, see [BDLFloatingPlayer](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLFloatingPlayer). |


<span id="BDLFloatingPlayerDelegate-floatingplayerdidsingletap"></span>
### floatingPlayerDidSingleTap:

```objectivec
- (void)floatingPlayerDidSingleTap:(BDLFloatingPlayer *)floatingPlayer;
```


The SDK calls this method when viewers tap the player.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|floatingPlayer |BDLFloatingPlayer\* |The floating player. For more information, see [BDLFloatingPlayer](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLFloatingPlayer). |


<span id="BDLFloatingPlayerDelegate-floatingplayerdiddoubletap"></span>
### floatingPlayerDidDoubleTap:

```objectivec
- (void)floatingPlayerDidDoubleTap:(BDLFloatingPlayer *)floatingPlayer;
```


The SDK calls this method when viewers double\-tap the player.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|floatingPlayer |BDLFloatingPlayer\* |The floating player. For more information, see [BDLFloatingPlayer](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLFloatingPlayer). |


<span id="BDLFloatingPlayerDelegate-floatingplayerwillclose"></span>
### floatingPlayerWillClose:

```objectivec
- (void)floatingPlayerWillClose:(BDLFloatingPlayer *)floatingPlayer;
```


The SDK calls this method when the player is about to close.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|floatingPlayer |BDLFloatingPlayer\* |The floating player. For more information, see [BDLFloatingPlayer](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLFloatingPlayer). |


<span id="BDLFloatingPlayerDelegate-floatingplayer-onvodautocontinueplayback"></span>
### floatingPlayer:onVodAutoContinuePlayback:

```objectivec
- (void)floatingPlayer:(BDLFloatingPlayer *)floatingPlayer onVodAutoContinuePlayback:(NSTimeInterval)playbackTime;
```


The SDK calls this method when a VOD video automatically resumes playing from the point where it stopped.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|floatingPlayer |BDLFloatingPlayer\* |The floating player. For more information, see [BDLFloatingPlayer](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLFloatingPlayer). |
|playbackTime |NSTimeInterval |The position to which the video seeks after automatically resuming from where it stopped. Unit: seconds. |


<span id="BDLFloatingPlayerDelegate-floatingplayerdidclickclose"></span>
### floatingPlayerDidClickClose:

```objectivec
- (BOOL)floatingPlayerDidClickClose:(BDLFloatingPlayer *)floatingPlayer;
```


The SDK calls this method when viewers tap to close the floating player.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|floatingPlayer |BDLFloatingPlayer\* |The floating player. For more information, see [BDLFloatingPlayer](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLFloatingPlayer). |


**Return Value**

Whether to execute the default tap logic, which is to close the floating player.


* `YES`: Execute.

* `NO`: Do not execute.

    &nbsp;


<span id="floatingplayer-onuserforceoffline"></span>
### floatingPlayer:onUserForceOffline:

```objectivec
- (void)floatingPlayer:(BDLFloatingPlayer *)floatingPlayer onUserForceOffline:(BDLForceOfflineInfo *)info;
```


The SDK calls this method when viewers are forcibly removed from the live room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|floatingPlayer |BDLFloatingPlayer\* |The floating player. For more information, see [BDLFloatingPlayer](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLFloatingPlayer). |
|info |BDLForceOfflineInfo\* |The reason for viewers being forcibly removed from the live room. For more information, see [BDLForceOfflineInfo](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLForceOfflineInfo). |


<span id="BDLCountdownViewDelegate"></span>
# BDLCountdownViewDelegate

```objectivec
@protocol BDLCountdownViewDelegate <NSObject>
```


The delegate methods for the live room countdown view.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[countdownViewDidFinish:](https://docs.byteplus.com/en/docs/11/31215#BDLCountdownViewDelegate-countdownviewdidfinish) |
|void |[countdownViewDidCancel:](https://docs.byteplus.com/en/docs/11/31215#BDLCountdownViewDelegate-countdownviewdidcancel) |


<span id="instructions"></span>
## Instructions

<span id="BDLCountdownViewDelegate-countdownviewdidfinish"></span>
### countdownViewDidFinish:

```objectivec
- (void)countdownViewDidFinish:(BDLCountdownView *)countdownView;
```


The SDK calls this method when the countdown ends.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|countdownView |BDLCountdownView\* |The live room countdown view. For more information, see [BDLCountdownView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLCountdownView). |


<span id="BDLCountdownViewDelegate-countdownviewdidcancel"></span>
### countdownViewDidCancel:

```objectivec
- (void)countdownViewDidCancel:(BDLCountdownView *)countdownView;
```


The SDK calls this method when the countdown is canceled.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|countdownView |BDLCountdownView\* |The live room countdown view. For more information, see [BDLCountdownView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLCountdownView). |


<span id="BDLPlayerSpeedViewDelegate"></span>
# BDLPlayerSpeedViewDelegate

```objectivec
@protocol BDLPlayerSpeedViewDelegate <NSObject>
```


The delegate methods for the playback speed selection view.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[speedView:speedDidChange:](https://docs.byteplus.com/en/docs/11/31215#BDLPlayerSpeedViewDelegate-speedview-speeddidchange) |


<span id="instructions"></span>
## Instructions

<span id="BDLPlayerSpeedViewDelegate-speedview-speeddidchange"></span>
### speedView:speedDidChange:

```objectivec
- (void)speedView:(BDLPlayerSpeedView *)speedView speedDidChange:(BDLPlayerSpeed)speed;
```


The SDK calls this method when the playback speed changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|speedView |BDLPlayerSpeedView\* |The playback speed selection view. For more information, see [BDLPlayerSpeedView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLPlayerSpeedView). |
|speed |BDLPlayerSpeed |The current playback speed. For more information, see [BDLPlayerSpeed](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLPlayerSpeed). |


<span id="BDLActivityListener"></span>
# BDLActivityListener

```objectivec
@protocol BDLActivityListener <NSObject>
```


The listener for the live room.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[activity:networkStatusDidChange:](https://docs.byteplus.com/en/docs/11/31215#BDLActivityListener-activity-networkstatusdidchange) |
|void |[activity:activityStatusDidChange:](https://docs.byteplus.com/en/docs/11/31215#BDLActivityListener-activity-activitystatusdidchange) |


<span id="instructions"></span>
## Instructions

<span id="BDLActivityListener-activity-networkstatusdidchange"></span>
### activity:networkStatusDidChange:

```objectivec
- (void)activity:(BDLActivity *)activity networkStatusDidChange:(BDLNetworkStatus)networkStatus;
```


The callback is triggered when the network status of the live room changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|activity |BDLActivity\* |The live room information, which is passed in through the [joinLiveRoomWithActivity:success:failure:](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLiveEngine-joinliveroomwithactivity-success-failure) method. For more information, see [BDLActivity](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLActivity). |
|networkStatus |BDLNetworkStatus |The current network status. For more information, see [BDLNetworkStatus](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLNetworkStatus). |


<span id="BDLActivityListener-activity-activitystatusdidchange"></span>
### activity:activityStatusDidChange:

```objectivec
- (void)activity:(BDLActivity *)activity activityStatusDidChange:(BDLActivityStatus)activityStatus;
```


The callback is triggered when the live room status changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|activity |BDLActivity\* |The live room information, which is passed in through the [joinLiveRoomWithActivity:success:failure:](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLLiveEngine-joinliveroomwithactivity-success-failure) method. For more information, see [BDLActivity](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLActivity). |
|activityStatus |BDLActivityStatus |The current live room status. For more information, see [BDLActivityStatus](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLActivityStatus). |


<span id="BDLDraggingDelegate"></span>
# BDLDraggingDelegate

```objectivec
@protocol BDLDraggingDelegate <NSObject>
```


The delegate methods for dragging events.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[draggingDidBegan:](https://docs.byteplus.com/en/docs/11/31215#BDLDraggingDelegate-draggingdidbegan) |
|void |[draggingDidChanged:](https://docs.byteplus.com/en/docs/11/31215#BDLDraggingDelegate-draggingdidchanged) |
|void |[draggingDidEnded:](https://docs.byteplus.com/en/docs/11/31215#BDLDraggingDelegate-draggingdidended) |


<span id="instructions"></span>
## Instructions

<span id="BDLDraggingDelegate-draggingdidbegan"></span>
### draggingDidBegan:

```objectivec
- (void)draggingDidBegan:(UIView *)view;
```


The SDK calls this method when dragging begins.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|view |UIView\* |The view that is currently being dragged. |


<span id="BDLDraggingDelegate-draggingdidchanged"></span>
### draggingDidChanged:

```objectivec
- (void)draggingDidChanged:(UIView *)view;
```


The SDK calls this method when the position of the view being dragged changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|view |UIView\* |The view that is currently being dragged. |


<span id="BDLDraggingDelegate-draggingdidended"></span>
### draggingDidEnded:

```objectivec
- (void)draggingDidEnded:(UIView *)view;
```


The SDK calls this method when dragging ends.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|view |UIView\* |The view that is currently being dragged. |


<span id="BDLMultiLanguageViewDelegate"></span>
# BDLMultiLanguageViewDelegate

```objectivec
@protocol BDLMultiLanguageViewDelegate <NSObject>
```


The delegate methods for the language selection dialog box view.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[multiLanguageView:removeFromSuperview:](https://docs.byteplus.com/en/docs/11/31215#BDLMultiLanguageViewDelegate-multilanguageview-removefromsuperview) |


<span id="instructions"></span>
## Instructions

<span id="BDLMultiLanguageViewDelegate-multilanguageview-removefromsuperview"></span>
### multiLanguageView:removeFromSuperview:

```objectivec
- (void)multiLanguageView:(BDLMultiLanguageView *)view removeFromSuperview:(UIView *)superview;
```


The SDK calls this method when the language selection dialog box is hidden.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|view |BDLMultiLanguageView\* |self, which is the current hidden [BDLMultiLanguageView](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLMultiLanguageView) instance. |
|superview |UIView\* |self.superview, which is the superView of the current instance. |


<span id="BDLInteractiveToolContentViewDelegate"></span>
# BDLInteractiveToolContentViewDelegate

```objectivec
@protocol BDLInteractiveToolContentViewDelegate <NSObject>
```


The delegate methods for the interaction tool content view.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|BOOL |[interactiveToolTextView:shouldInteractWithURL:](https://docs.byteplus.com/en/docs/11/31215#BDLInteractiveToolContentViewDelegate-interactivetooltextview-shouldinteractwithurl) |
|void |[didClickContextViewWithModel:contextModel:](https://docs.byteplus.com/en/docs/11/31215#BDLInteractiveToolContentViewDelegate-didclickcontextviewwithmodel-contextmodel) |


<span id="instructions"></span>
## Instructions

<span id="BDLInteractiveToolContentViewDelegate-interactivetooltextview-shouldinteractwithurl"></span>
### interactiveToolTextView:shouldInteractWithURL:

```objectivec
- (BOOL)interactiveToolTextView:(UITextView *)textView shouldInteractWithURL:(NSURL *)URL;
```


Whether the URL in the interaction message text is clickable.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|textView |UITextView\* |The text view where the URL is located. |
|URL |NSURL\* |The URL in the interaction message text. |


**Return Value**


* `YES`: Clickable.

* `NO`: Not clickable.

    &nbsp;


<span id="didclickcontextviewwithmodel-contextmodel"></span>
### didClickContextViewWithModel:contextModel:

```objectivec
- (void)didClickContextViewWithModel:(BDLInteractiveToolModel *)model contextModel:(BDLInteractiveContextModel *)contextModel;
```


The SDK calls this method when viewers tap the interaction tool content view.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|model |BDLInteractiveToolModel\* |The interaction tool model. For more information, see [BDLInteractiveToolModel](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLInteractiveToolModel) |
|contextModel |BDLInteractiveContextModel\* |The model of interaction tool content. For more information, see [BDLInteractiveContextModel](https://docs.byteplus.com/en/docs/11/docs-bdlliveengine#BDLInteractiveContextModel). |
