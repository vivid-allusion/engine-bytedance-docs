---
title: "Managing Magic Template objects in iOS"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/160-managing-magic-template-objects-in-ios"
---

Managing the template objects involves handling their creation, modification, and usage within the application, ensuring they are utilized effectively for generating or editing content.

<span id="53164663"></span>
# Create template source management objects

Create objects of CSIFCutSameSource to manage the resources.

<span id="11d57c58"></span>
#### API definition

```objectivec
+ (CSIFCutSameSource * _Nonnull)createSourceFromTemplatePath:(NSString * _Nonnull)path 
```


<span id="ecebfcb7"></span>
#### Sample code

```objectivec
// Import the template path 
CSIFCutSameSource *source = [CSIFCutSameSDK createSourceFromTemplatePath:@"xxx"];  
```


<span id="38d502b1"></span>
# Parsing template information

Parse the template to get the slot information of the template.

<span id="0edfd6da"></span>
#### API definition

```objectivec
- (void)prepareTemplateWithProgress:(nullable void(^)(CGFloat))progress
                          completion:(nullable void(^)(NLEModel_OC * _Nullable, CSIFCutSameTemplateModel * _Nullable, NSError * _Nullable, NSString * _Nullable))completion; 
```


<span id="6836e6d0"></span>
#### Sample code

```objectivec
[self.cutsameSource prepareTemplateWithProgress:^(CGFloat progress) {
       
} completion:^(NLEModel_OC * _Nullable nleModel, CSIFCutSameTemplateModel * _Nullable templateModel, NSError * _Nullable error, NSString * _Nullable errorMsg) {

}]; 
```


<span id="35d0b476"></span>
# Material composition processing

Perform compression, reverse playback, and other treatments on the selected material after selection.

<span id="927293c8"></span>
#### API definition

```objectivec
- (void)prepareSourceWithProgress:(void(^ _Nullable)(CGFloat))progress
                       completion:(void(^ _Nullable)(NSArray *_Nullable materialAssetModels, NSError *_Nullable error))completion; 
```


<span id="63b051cb"></span>
#### Sample code

```objectivec
[self.cutsameSource prepareSourceWithProgress:^(CGFloat progress) {
     
} completion:^(NSArray * _Nullable materialAssetModels, NSError * _Nullable error) {

}]; 
```


<span id="bb1d09d5"></span>
# Create CSIFCutSamePlayer object

Create a `CSIFCutSamePlayer` object, which provides capabilities such as video preview, slot editing, text editing, and video export.

<span id="0ec3a8ae"></span>
#### API definition

```objectivec
+ (CSIFCutSamePlayer * _Nonnull)createPlayerWithContainerView:(UIView * _Nonnull)containerView 
                                                       source:(CSIFCutSameSource * _Nonnull)source; 
```


<span id="b7f8f4d6"></span>
#### Sample code

```objectivec
[CSIFCutSameSDK createPlayerWithContainerView:self.playerContainer source:self.cutsameSource]; 
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Creating a <code>CSIFCutSamePlayer</code> depends on the creation of a <code>CSIFCutSameSource object</code>.</div>


* <div data-tips="true" data-tips-type="tip">After using the object of <code>CSIFCutSamePlayer</code>, use the method of <code>destoryPlayer</code> to destroy it.</div>



<span id="b9b191f1"></span>
# Replay

Use the object of `CSIFCutSamePlayer` to control the replay and play of the template.

<span id="af2eb436"></span>
#### API definition

Refer to the definition of `CSIFCutSamePlayer` class to see more object methods.

```objectivec
@interface CSIFCutSamePlayer : NSObject

/// Release the player 
- (void)destoryPlayer;
/// Reset the player
- (void)resetPlayer;

// Play control
/// Play
- (void)play;
/// Pause
- (void)pause;

/// Jump to a time to play
/// @param time Time stamp
/// @param completion Callback after the jump
- (void)seekToTime:(CMTime)time completion:(nullable dispatch_block_t)completion;

/// Jump to a time to play
/// @param time Time stamp
/// @param seekMode seek mode 0:smooth 1:Accurate
/// @param completion Callback after the jump
- (void)seekToTime:(CMTime)time seekMode:(int)seekMode completion:(nullable dispatch_block_t)completion;

@end
```


<span id="68140767"></span>
#### Sample code

```objectivec
[self.cutsamePlayer play]; 
```
