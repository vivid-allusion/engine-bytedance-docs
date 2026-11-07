---
title: "Exporting Magic Template videos in iOS"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/130-exporting-magic-template-videos-in-ios"
---

Exporting Magic Template videos involves saving the created content in the desired format or platform, ensuring compatibility and quality for distribution or further editing.

<span id="de898c80"></span>
# Export the video to the local storage

Export the replay video to the local storage.

<span id="49783f3a"></span>
#### API definition

```objectivec
- (void)exportVideoWithConfig:(CSIFVideoExportConfig * _Nonnull)config progress:(void (^ _Nullable)(CGFloat))progress completion:(void (^ _Nullable)(NSURL * _Nullable videoURL, NSError * _Nullable error))completion
```


<span id="724aa12c"></span>
#### Sample code

```objectivec
[self.cutsamePlayer exportVideoWithConfig:config progress:^(CGFloat progress) {

} completion:^(NSURL * _Nullable videoURL, NSError * _Nullable error) {

}];
```


<span id="41533068"></span>
# Video frame extraction

Get a screenshot of a specific time stamp.

<span id="15cd504d"></span>
#### API definition

```objectivec
- (void)getVideoFrameWithTime:(CMTime)time completion:(void(^ _Nonnull)(UIImage * _Nullable, NSError * _Nullable))completion;
```


<span id="780ba312"></span>
#### Sample code

```objectivec
[self.cutSamePlayer getVideoFrameWithTime:CMTimeMake(1, 10) completion:^(UIImage *image, NSError *error) {

}];
```


<span id="13cb5f03"></span>
# Clearing draft resources

```objectivec
// Clears intermediate files generated during the editing process. 
// Can be used after using the Magic Template feature
[CSIFCutSameSDK clearDrafts];
```
