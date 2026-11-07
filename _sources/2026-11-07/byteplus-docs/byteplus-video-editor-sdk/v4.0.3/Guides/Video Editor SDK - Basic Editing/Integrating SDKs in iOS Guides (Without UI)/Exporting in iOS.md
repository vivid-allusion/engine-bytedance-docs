---
title: "Exporting in iOS"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-exporting-in-ios"
---

This article introduces how to use the export feature of Video Editor SDK. By using the export feature, you can transmit the edited video to a video folder in the sandbox.

<span id="01c5fbf6"></span>
# Prerequisite

Before exporting videos, ensure you have obtained the `HTSVideoData` object using the `NLEInterface_OC` class.

<span id="f70e878e"></span>
# Module description

The following table introduces classes related to the export feature of VE SDK.


|**Class Name** |**Description** |
|---|---|
|HTSVideoData |The video object used in NLE. It is used to store the video data that users are currently processing. |
|IESMMTransProcessData |The export configuration object. You can configure export parameters by using this class. |
|VECompileTaskManagerSession |The manager for video\-compiling tasks. |
|VELVConcat |The video contact object. You can use this class to complete cover configuration for your target video. |


<span id="fd4bc970"></span>
# Procedure


1. To realize different ways of export, configure parameters related to `HTSVideoData` and `IESMMTransProcessData` by using the following code.

   ```Swift
   guard let videoData = nle.veVideoData?.copy() as? HTSVideoData else {
       return
   }
   
   let resolution: Int = 540
   let fps: Int = 30
   
   videoData.transParam.allowFrameReordering = false
   videoData.transParam.bitrate = Int32(_exportBitRate(with: resolution, fps: 30))
   videoData.canvasSize = _exportSize(for: resolution)
   if nle.veVideoData?.lvCompletionAsset == nil {
       nle.veVideoData?.updateTimeLine()
   }
   videoData.isPlaying = false
   videoData.transParam.useVideoDataOutputSize = true
   videoData.transParam.videoSize = videoData.canvasSize
   
   let config = IESMMTransProcessData()
   config.useNewMudule = true  // need true
   config.enableMultiTrack = true  // need true
   config.exportFps = Int32(fps)
   config.enableOptExportFps = true
   config.timeOutPeriod = 4
   config.infoStickerForceAmazing = true
   config.disableEffectGroup = true
   config.enableKeyFrameFeature = true
   config.infostickerTextureRelease = true
   config.disableEffectProcess = false
   config.disableExtracFilter = true
   config.encodeUseFenceRender = true
   config.disableInfoSticker = false
   ```
   

2. To export your target video, call the`transWithVideoData:transConfig:videoProcess:completeBlock:` interface.

   **Sample code**

   ```Swift
   VECompileTaskManagerSession.sharedInstance().trans(with: videoData, transConfig: config, videoProcess: nle.getVideoProcess()) {  [weak self] res in
       guard let url = res?.mergeUrl else {
           return
       }
   ```
   

3. If you want to add a cover for your target video, call the functions related to `VELVConcat`.

   **Sample code**

   ```Swift
    self?._concatCover(with: url, completion: completion)
   ```
   


**Full sample code**

For more information, refer to ExportHelper within the demo project.

For description of parameters used by `IESMMTransProcessData`, refer to the notes in `IESMMTransProcessData.h`.

```Swift
import TTVideoEditor
// step 1: config params
guard let videoData = nle.veVideoData?.copy() as? HTSVideoData else {
    return
}

let resolution: Int = 540
let fps: Int = 30

videoData.transParam.allowFrameReordering = false
videoData.transParam.bitrate = Int32(_exportBitRate(with: resolution, fps: 30))
videoData.canvasSize = _exportSize(for: resolution)
if nle.veVideoData?.lvCompletionAsset == nil {
    nle.veVideoData?.updateTimeLine()
}
videoData.isPlaying = false
videoData.transParam.useVideoDataOutputSize = true
videoData.transParam.videoSize = videoData.canvasSize

let config = IESMMTransProcessData()
config.useNewMudule = true  // need true
config.enableMultiTrack = true  // need true
config.exportFps = Int32(fps)
config.enableOptExportFps = true
config.timeOutPeriod = 4
config.infoStickerForceAmazing = true
config.disableEffectGroup = true
config.enableKeyFrameFeature = true
config.infostickerTextureRelease = true
config.disableEffectProcess = false
config.disableExtracFilter = true
config.encodeUseFenceRender = true
config.disableInfoSticker = false

// step 2: export video
VECompileTaskManagerSession.sharedInstance().trans(with: videoData, transConfig: config, videoProcess: nle.getVideoProcess()) {  [weak self] res in
    guard let url = res?.mergeUrl else {
        return
    }
    
    // step 3: concat cover (Optional)
    self?._concatCover(with: url, completion: completion)
}`
```


&nbsp;
