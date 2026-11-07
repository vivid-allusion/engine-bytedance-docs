---
title: "Utilizing Magic Template objects in iOS"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/150-utilizing-magic-template-objects-in-ios"
---

Utilizing Magic Template's template objects involves effectively integrating and leveraging them within your application to streamline content creation and customization processes.

<span id="2597950e"></span>
# Get template media material

Get the template's media materials, that is, the information of the template's variable slots.

<span id="f7a19beb"></span>
#### API definition

```objectivec
@interface CSIFCutSameTemplateModel : CSIFBaseModel
@property (nonatomic, copy, nullable) NSArray *fragments;
@end
```


<span id="f799a8be"></span>
#### Sample code

```objectivec
[self.cutsameSource prepareTemplateWithProgress:^(CGFloat progress) {

} completion:^(NLEModel_OC * _Nullable nleModel, CSIFCutSameTemplateModel * _Nullable templateModel, NSError * _Nullable error, NSString * _Nullable errorMsg) {
    //Can be retrieved through callback
    self.fragments = templateModel.fragments;
}]; 
```


<span id="6d5c1166"></span>
# Update media material

Support the feature of replacing media materials, that is, replacing slot materials.

<span id="3023da54"></span>
#### API definition

```objectivec
// CSIFCutSameSource
- (void)replaceAsset:(CSIFAssetModel *)originAsset
           withAsset:(CSIFAssetModel *)newAsset
            progress:(void (^)(CGFloat))progress
          completion:(void (^)(CSIFCutSameMaterialAssetModel *model, NSError *error))completion;
        
// CSIFCutSamePlayer
- (BOOL)replaceFragmentWithAsset:(CSIFCutSameMaterialAssetModel *)asset 
                   withPayloadID:(NSString *)payloadId;
```


<span id="eca622cf"></span>
#### Sample code

```objectivec
[self.cutsameSource replaceAsset:originAsset withAsset:newAsset progress:^(CGFloat progress) {
 
} completion:^(CSIFCutSameMaterialAssetModel *martrialAsset, NSError *error) {
    [self.cutSamePlayer replaceFragmentWithAsset:martrialAsset withPayloadID:fragment.payloadID];
}];
```


<span id="996806dc"></span>
# Get text material in player

Get template text material.

<span id="24fa4677"></span>
#### API definition

```objectivec
@interface CSIFCutSamePlayer (EditText)
@property (nonatomic, copy, readonly) NSArray *_Nullable canReplaceTextFragments;
@end 
```


<span id="efae79b8"></span>
#### Sample code

```objectivec
NSArray *textFragments = player.canReplaceTextFragments; 
```


<span id="aa05bf6c"></span>
# Update template text material

Support the feature of editing template text.

<span id="386c56a4"></span>
#### API definition

```objectivec
- (BOOL)updateTextFragment:(nonnull CSIFTemplateTextFragment *)fragment withText:(nonnull NSString *)text; 
```


<span id="d7b17c3d"></span>
#### Sample code

```objectivec
[cutSamePlayer updateTextFragment:textFragment withText:@"new text"]; 
```


<span id="758248d3"></span>
# Play control

Support play control, such as starting, pausing, and seeking a specific time.

<span id="b358fc7c"></span>
#### API definition

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


<span id="e3119ebe"></span>
#### Sample code

```objectivec
[self.cutsamePlayer play]; 
```


<span id="603fb8a2"></span>
# Set the volume of a specific segment

<span id="31a10352"></span>
#### API definition

```objectivec
- (BOOL)modifyFragmentWithInfo:(NSDictionary *)info payloadID:(NSString *)payloadId 
```


<span id="90827a66"></span>
#### Sample code

```objectivec
[cutSamePlayer modifyFragmentWithInfo:@{CSIFCutSamePlayerInfoKeyVolume: @(volume)} payloadID:fragment.payloadID]; 
```


<span id="32399906"></span>
# Get the volume of a specific segment

<span id="5eb9b451"></span>
#### API definition

```objectivec
- (NSDictionary *)metaInfoForVideoFragment:(CSIFTemplateVideoEditFragment *)fragment 
```


<span id="ace43636"></span>
#### Sample code

```objectivec
NSNumber *volumeValue = [self.cutSamePlayer metaInfoForVideoFragment:self.displayFragments[self.curEditIndex]][CSIFCutSamePlayerInfoKeyVolume]; 
```
