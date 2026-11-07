---
title: "Detailed Development Guide - iOS - Magic Template"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-detailed-development-guide-ios-magic-template"
---

<span id="Service process"></span>
### **Service process**

The following flowchart shows the overall template editing process.

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/feaaa4e9e351451589f536d00a59a244~tplv-em5hxbkur4-noop.image) </span>

<span id="License file"></span>
#### **License file**

You must be authorized before you can use Magic Template. Contact ByteDance to obtain the license file for authorization.

1、 Replace the .licbag file in **CutSameIF.bundle** with the license file that you have obtained.

2、Drag **CutSameIF.bundle** to Xcode and click **Finish**.

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/c5f58823a7fd4a779384091ccd0fdbc0~tplv-em5hxbkur4-noop.image) </span>

To obtain the path of the license file, run the following code:

```objectivec
// Obtain the path of the License.bundle file.

  NSString *bundlePath = [[NSBundle mainBundle] pathForResource:@"CutSameIF" ofType:@"bundle" inDirectory:nil];

  // Obtain the path of the .licbag file.

  NSString *licPath = [[bundlePath stringByAppendingString:@"/"] stringByAppendingString:@"xxxx.licbag"];
```


You must initialize the CutSameIF SDK or Magic Template UI SDK before you can use it.

<span id="Set the SDK delegate"></span>
### **Set the** **SDK** **delegate**

<span id="Feature"></span>
#### **Feature**

Sets the SDK delegate so that SDK callbacks can be received.

<span id="API definition"></span>
#### **API definition**

```objectivec
// The delegate that is used to listen for callbacks.

@property (nonatomic, weak) id<CSIFCutSameSDKDelegate> delegate;
```


<span id="Sample code"></span>
#### **Sample code**

```objectivec
// Implement the CSIFCutSameSDKDelegate protocol.

CSIFCutSameSDK.shareInstance.delegate = self;
```


The delegate will then receive callbacks from the SDK.

```objectivec
typedef enum : NSUInteger {

  CSIFCutSameStatusReady, //  The initialization is successful.

  CSIFCutSameErrorInvalidFuncName = 1, //  The method name is invalid.

  CSIFCutSameErrorInvalidPath, //  The license file path is invalid.

  CSIFCutSameErrorInvalidAppID, //  The app ID is invalid.

  CSIFCutSameErrorFileError, //  Failed to open the license file.

  CSIFCutSameErrorTypeNotMatch, //  The license file does not match.

  CSIFCutSameErrorInvalidVersion, //  The version of the license is not supported.

  CSIFCutSameErrorInvalidBlockCount, //  The license block is invalid.

  CSIFCutSameErrorLicenseStatusInvalid, //  The license file status is invalid.

  CSIFCutSameErrorLicenseStatusExpired, //  License file expired.

  CSIFCutSameErrorLicenseNoFunc, //  Failed to find the method name.

  CSIFCutSameErrorLicenseStatusNoMatch, //  The status of the license does not match.

  CSIFCutSameErrorLicenseStatusIdNoMatch, //  The status ID does not match.

  CSIFCutSameErrorUnknowed, //  Unknown error.

} CSIFCutSameStatus;


- (void)cutsameStatusDidChange:(CSIFCutSameStatus)status {

    //  Check the status of the SDK through the callback.

    if (status != CSIFCutSameStatusReady) {

    //  Authorization failed.

    }

}


//  Video exported.

- (void)onExportFinish:(NSURL *)videoURL error:(NSError *)error {

  if (!error) {

    NSLog(@" Video exported to:  %@", videoURL);

  }

}
```


<span id="Configure template fetching"></span>
### **Configure template fetching**

<span id="Feature"></span>
#### **Feature**

Sets parameters such as **host** for template fetching.

<span id="API definition"></span>
#### **API definition**

```objectivec
@interface CSIFTemplateFetcherConfig: NSObject

//  The domain name of the server.

@property (nonatomic, strong) NSString *host;

//  The common parameters in a network request.

@property (nonatomic, strong) NSDictionary *extraCommonParam;

@end
```


<span id="Configure effect fetching"></span>
### **Configure effect fetching**

<span id="Feature"></span>
#### **Feature**

Sets parameters such as **host** for effect fetching.

<span id="API definition"></span>
#### **API definition**

```objectivec
@interface CSIFEffectFetcherConfig: NSObject

//  The domain name of the server.

@property (nonatomic, strong) NSString *host;

//  The path of the algorithm models.

@property (nonatomic, strong) NSString *modelListPath;

//  The path of the effect.

@property (nonatomic, strong) NSString *effectListPath;

@end
```


<span id="Configure video export"></span>
### **Configure video export**

<span id="Feature"></span>
#### **Feature**

Sets parameters for video export.

<span id="API definition"></span>
#### **API definition**

```objectivec
/**

 The resolution for video export.

 */

typedef NS_ENUM(NSInteger, CSIFExportResolution) {

    CSIFExportResolutionP480 = 480,

    CSIFExportResolutionP720 = 720,

    CSIFExportResolutionP1080 = 1080,

    CSIFExportResolutionP2K = 1440,

    CSIFExportResolutionP4K = 2160

};

// The export configuration.

@interface CSIFVideoExportConfig : NSObject

// The resolution for video export, which is 1080p for iPhone 6S and later models and 720p for earlier models.

@property (nonatomic, assign) CSIFExportResolution resolution;

// The metadata to be written to the video.

// The corresponding parameter is com.apple.quicktime.description.

@property (nonatomic, copy) NSString *metadataString;

// unit: bit/s

@property (nonatomic, assign) int bitrate;

@end
```


<span id="SDK initialization"></span>
### **SDK initialization**

<span id="Feature"></span>
#### **Feature**

Initializes the singleton of the **CSIFCutSameSDK** class that manages the lifecycle of the SDK.

The **CSIFTemplateFetcher** object is generated after the initialization.

<span id="API definition"></span>
#### **API definition**

```objectivec
// Configure the SDK.

// @param config            The configuration.

// @param completion  The callback configuration.

- (void)setupWithConfig:(id <CSIFConfigProtocol>)config;
```


<span id="Structure"></span>
### **Structure**

```Plain
@protocol CSIFConfigProtocol

//  The configuration for template fetching.

@property (nonatomic, strong) CSIFTemplateFetcherConfig *templateFetcherConfig;

//  The configuration for effect fetching.

@property (nonatomic, strong) CSIFEffectFetcherConfig *effectFetcherConfig;

//  The path of the license file.

@property (nonatomic, strong) NSString *licensePath;

//  The configuration for video export.

@property (nonatomic, strong) CSIFVideoExportConfig *videoExportConfig;

@end
```


<span id="Sample code"></span>
#### **Sample code**

```objectivec
//  Create a configuration class.

    CSIFConfigImpl *impl = [[CSIFConfigImpl alloc] init];

    //  The path of the license file.

    NSString *bundlePath = [[NSBundle mainBundle] pathForResource:@"License" ofType:@"bundle" inDirectory:nil];

    licPath = [[bundlePath stringByAppendingString:@"/"] stringByAppendingString:@"cutsame_neibu_20210602_20210831_com.cutsame.demo_3.9.2.2.licbag"];

    //  The configuration for template fetching.

    CSIFTemplateFetcherConfig *templateFetcherConfig = [[CSIFTemplateFetcherConfig alloc] init];

    templateFetcherConfig.host = @"http://common.bytedance.net";

    //  The configuration for effect fetching.

    CSIFEffectFetcherConfig *effectFetcherConfig = [[CSIFEffectFetcherConfig alloc] init];

    effectFetcherConfig.host = templateFetcherConfig.host;

    effectFetcherConfig.modelListPath = @"/api/modellistinfo";

    effectFetcherConfig.effectListPath = @"/api/effectlist";



    //  The configuration for video export.

    CSIFVideoExportConfig *videoExportConfig = [[CSIFVideoExportConfig alloc] init];

    videoExportConfig.resolution = CSIFExportResolutionP1080;

    videoExportConfig.metadataString = @"Magic Template video";

    videoExportConfig.bitrate = @"6000000";



    impl.templateFetcherConfig = templateFetcherConfig;

    impl.effectFetcherConfig = effectFetcherConfig;

    impl.videoExportConfig = videoExportConfig;

    impl.licensePath = licPath;

```


<span id="CutSameIF SDK integration"></span>
## **CutSameIF SDK integration**

<span id="Create an object for template fetching"></span>
### **Create an object for template fetching**

<span id="Feature"></span>
#### **Feature**

Creates an object for template fetching. This object supports two APIs that are used to fetch template categories and templates.

<span id="API definition"></span>
#### **API definition**

```objectivec
//  The object for template fetching.

@property (nonatomic, strong) CSIFTemplateFetcher *fetcher;
```


<span id="Sample code"></span>
#### **Sample code**

```Nginx
CSIFTemplateFetcher *fetcher = CSIFCutSameSDK.shareInstance.fetcher;
```


<span id="Fetch template categories"></span>
### **Fetch template categories**

<span id="Feature"></span>
#### **Feature**

Fetches template categories.

<span id="API definition"></span>
#### **API definition**

```objectivec
//  Fetch all Magic Template categories.

// @param path API

//  @param params   The custom parameters.

//  @param success     The success callback.

//  @param failure       The failure callback.

- (void)queryCategoryListWithPath:(NSString *)path

                      extraParams:(NSDictionary * _Nullable)params

                          success:(void(^)(NSArray<CSIFTemplateCategory *> * _Nullable categoryList))success

                          failure:(void(^)(NSError *error))failure;
```


<span id="Structure"></span>
#### **Structure**

```objectivec
@interface CSIFTemplateCategory : CSIFBaseModel

//  The ID of the category.

@property (nonatomic, assign) NSInteger categoryID;

//  The name of the category.

@property (nonatomic, copy) NSString *name;



@end
```


<span id="Sample code"></span>
#### **Sample code**

```objectivec
[CSIFCutSameSDK.shareInstance.fetcher queryCategoryListWithPath:kTemplateCategoryListUrlPath

                                                   extraParams:nil 

                                                       success:^(NSArray<CSIFTemplateCategory *> * _Nullable categories) {

    //  Template categories are fetched.

} failure:^(NSError * _Nonnull error) {

    //  An error occurred.

}];
```


<span id="Fetch templates"></span>
### **Fetch templates**

<span id="Feature"></span>
#### **Feature**

Fetches templates in the specified category.

<span id="API definition"></span>
#### **API definition**

```objectivec
//  Fetch Magic Template templates based on the category ID.

// @param path api

//  @param params         The custom parameters.

//  @param categoryID   The ID of the category.

//  @param cursor           The cursor used to fetch templates in pagination mode, which is 0 for the first request of this API.

//  @param count            The number of templates to be fetched.

//  @param success           The success callback.

//  @param failure             The failure callback.

- (void)queryTemplateListWithPath:(NSString *)path

                      extraParams:(NSDictionary * _Nullable)params

                       categoryID:(NSInteger)categoryID

                           cursor:(NSUInteger)cursor

                            count:(NSUInteger)count

                          success:(void(^)(CSIFTemplateList * _Nullable templateList))success

                          failure:(void(^)(NSError *error))failure;
```


<span id="Structure"></span>
#### **Structure**

```objectivec
@interface CSIFTemplateList : CSIFBaseModel

//  The cursor for the next fetching.

@property (nonatomic, assign) NSInteger nextCursor;

//  Indicates whether more templates are to be fetched.

@property (nonatomic, assign) BOOL hasMore;

//  The list of templates.

@property (nonatomic, copy) NSArray<CSIFTemplateModel *> *templateList;

@end



@interface CSIFTemplateModel : CSIFBaseModel

//  The ID of the template.

@property (nonatomic, assign) NSInteger templateID;

//  The short title of the template.

@property (nonatomic, copy) NSString *shortTitle;

//  The full title of the template.

@property (nonatomic, copy) NSString *title;

// Required. The author. This parameter is not specified for professionally generated content (PGC).

@property (nonatomic, strong) CSIFTemplateAuthor *author;

// The custom counter.

@property (nonatomic, copy) NSDictionary *counterData;

//  The thumbnail information.

@property (nonatomic, strong) CSIFTemplateCoverModel *cover;

//  The information about the original video.

@property (nonatomic, strong) CSIFTemplateVideoInfo *originVideoInfo;

//  The information about the transcoded video.

@property (nonatomic, strong) CSIFTemplateVideoInfo *videoInfo;

//  The limit for uploading the template.

@property (nonatomic, strong) CSIFTemplateLimit *limit;

//  The time when the template was created.

@property (nonatomic, assign) NSInteger createTime;

//  The length of the video.

@property (nonatomic, assign) NSInteger duration;

//  The extra information for uploading the template from the client.

@property (nonatomic, copy) NSString *extra;

//  The extra information about the template model.

@property (nonatomic, copy) CSIFCutSameTemplateModel *extraModel;

//  The number of template segments.

@property (nonatomic, assign) NSInteger fragmentCount;

//  The number of template users.

@property (nonatomic, assign) NSUInteger usageAmount;

//  The number of template likes.

@property (nonatomic, assign) NSUInteger likeAmount;

//  The MD5 string of the template.

@property (nonatomic, copy) NSString *md5;

//  The status of the template. Valid values: 1 and 2. A value of 1 indicates that the template is online. A value of 2 indicates that the template is offline.

@property (nonatomic, assign) CSIFTemplateItemStatus status;

//  The tags of the template.

@property (nonatomic, copy) NSString *templateTags;

//  The URL of the template.

@property (nonatomic, copy) NSString *templateUrl;

//  The hint for the template.

@property (nonatomic, copy) NSString *hintLabel;

@end
```


**Sample code**

```objectivec
[CSIFCutSameSDK.shareInstance.fetcher queryTemplateListWithPath:kTemplateListUrlPath

                                                 extraParams:nil

                                                  categoryID:self.categoryModel.categoryID

                                                      cursor:self.cursor.unsignedIntValue

                                                       count:10

                                                     success:^(CSIFTemplateList * _Nullable templateList)

{

// Templates are fetched.

} failure:^(NSError * _Nonnull error) {

//  An error occurred.

}];
```


<span id="Media asset management"></span>
## **Media asset management**

<span id="Create a media asset management object"></span>
### **Create a media asset management object**

<span id="Feature"></span>
#### **Feature**

Creates a media asset management object, which is a **source** object. One video production process in Magic Template uses one **source** object.

<span id="API definition"></span>
#### **API definition**

```objectivec
//  Create a source object.
- (CSIFCutSameSource *)createSource;
```


<span id="Sample code"></span>
#### **Sample code**

```objectivec
CSIFCutSameSource *source = [CSIFCutSameSDK.shareInstance createSource];
```


<span id="Process media assets for video production"></span>
### **Process media assets for video production**

<span id="Feature"></span>
#### **Feature**

Processes media assets for video production after the **source** object is created and the media assets that meet the template requirements are provided.

<span id="API definition"></span>
#### **API definition**

```objectivec
//  Process media assets.

//  Generate media asset models based on the specified source media assets and template.

//  @param progress        The processing progress. The value ranges from 0 to 1.

//  @param completion   The completion callback.

- (void)prepareSourceWithProgress:(void(^)(CGFloat))progress

            completion:(void(^)(NSArray<CSIFCutSameMaterialAssetModel *> *materialAssetModels, NSError *error))completion;
```


<span id="Sample code"></span>
#### **Sample code**

```objectivec
//  Obtain the source object.

CSIFCutSameSource *source = CSIFCutSameSDK.shareInstance.source;

//  Set the template.

[source setSelectedTemplate:self.cutSameTemplateModel];

//  Set source media assets.

source.selectedAssets = self.viewModel.currentSelectAssetModels;

//  Process media assets.

[source prepareSourceWithProgress:^(CGFloat progress) {

// progress: [0, 1]

} completion:^(NSArray<CSIFCutSameMaterialAssetModel *> * _Nonnull materialAssetModels, NSError *error) {

//  materialAssetModels: Processed assets.

//  error: Indicates whether an error occurred.

}
```


<span id="Replace a media asset"></span>
### **Replace a media asset**

<span id="Feature"></span>
#### **Feature**

Replaces a media asset in the preview phase.

<span id="API definition"></span>
#### **API definition**

```objectivec
//  Replace a media asset.

//  @param originAsset   The original media asset.

//  @param newAsset      The new media asset.

//  @param progress        The replacement progress.

//  @param completion   The completion callback.

- (void)replaceAsset:(CSIFAssetModel *)originAsset

      withAsset:(CSIFAssetModel *)newAsset

      progress:(void (^)(CGFloat))progress

     completion:(void (^)(CSIFCutSameMaterialAssetModel *model, NSError *error))completion;
```


<span id="Sample code"></span>
#### **Sample code**

```objectivec
//  Process the media asset to be replaced.

[source replaceAsset:self.viewModel.inputData.singleAssetModel withAsset:self.viewModel.currentSelectAssetModels.firstObject progress:^(CGFloat progress) {

//  progress: the replacement progress. Valid values: 0 to 1.

} completion:^(CSIFCutSameMaterialAssetModel *martrialAsset, NSError *error) {

//  martrialAsset: Processed assets.

//  error: Indicates whether an error occurred.

}
```


<span id="Playback object management"></span>
## **Playback object management**

<span id="Create a preview object"></span>
### **Create a preview object**

<span id="Feature"></span>
#### **Feature**

Creates a preview object.

<span id="API definition"></span>
#### **API definition**

```objectivec
//  Create a preview object.

//  @param containerView  The container view of the player.

- (CSIFCutSamePlayer *)createPlayerWithContainerView:(nonnull UIView *)containerView;
```


<span id="Sample code"></span>
#### **Sample code**

```objectivec
- (CSIFCutSamePlayer *)cutSamePlayer {

    if (!_cutSamePlayer) {

        //  Create a preview object.

        //  @param containerView: the container view of the player.

        _cutSamePlayer = [CSIFCutSameSDK.shareInstance createPlayerWithContainerView:self.playerContainerView];

        //  Set a delegate to listen for playback events.

        _cutSamePlayer.delegate = self;

    }

    return _cutSamePlayer;

}
```


<span id="Listen for playback events"></span>
### **Listen for playback events**

<span id="Feature"></span>
#### **Feature**

Listens for playback events through a delegate.

<span id="API definition"></span>
#### **API definition**

```objectivec
//  The delegate listens for callbacks upon the occurrence of the following playback events:

@protocol CSIFCutSamePlayerDelegate <NSObject>

@optional

//  Playback progress change.

//  @param player       The player object.

//  @param progress   The replacement progress.

- (void)player:(CSIFCutSamePlayer *)player progressDidChanged:(double)progress;

//  Playback pausing.

//  @param player       The player object.

- (void)playerDidPause:(CSIFCutSamePlayer *)player;

//  Playback resumption.

//  @param player        The player object.

- (void)playerDidPlay:(CSIFCutSamePlayer *)player;

@end
```


<span id="Sample code"></span>
#### **Sample code**

```objectivec
//  Set a playback delegate.

self.cutSamePlayer.delegate = self;



//  Receive callbacks.

#pragma mark - CSIFCutSamePlayerDelegate

- (void)player:(CSIFCutSamePlayer *)player progressDidChanged:(double)progress

{

 //  Process the callback upon playback progress change.

}

- (void)playerDidPause:(CSIFCutSamePlayer *)player

{

//  Process the callback upon playback pausing.

}

- (void)playerDidPlay:(CSIFCutSamePlayer *)player

{

//  Process the callback upon playback resumption.

}
```


<span id="Update the player layout"></span>
### **Update the player layout**

<span id="Feature"></span>
#### **Feature**

Updates the layout of a player after the layout of its parent view is changed.

<span id="API definition"></span>
#### **API definition**

```objectivec
//  Update the layout of the player.

// Obtain the current frame of the player.

- (CGRect)frame;

//  Update the frame of the player.

//  @param rect    The frame of the parent view.

//  @return             The frame of the player.

- (CGRect)updatePlayerWithRect:(CGRect)rect;
```


<span id="Sample code"></span>
#### **Sample code**

```objectivec
// Update the layout of the player.

[self.cutSamePlayer updatePlayerWithRect:self.playerContainerView.bounds];
```


<span id="Obtain playback information"></span>
### **Obtain playback information**

<span id="Feature"></span>
#### **Feature**

Obtains playback information.

<span id="API definition"></span>
#### **API definition**

```objectivec
//  The time when playback was paused.

@property (nonatomic, assign) CMTime pauseTime;

//  Indicates whether playback is ongoing.

@property (nonatomic, assign) BOOL isPlaying;

//  The current time.

@property (nonatomic, assign, readonly) CMTime currentTime;

//  The length of the video.

@property (nonatomic, assign, readonly) CMTime duration;
```


<span id="Extract a video frame"></span>
### **Extract a video frame**

<span id="Feature"></span>
#### **Feature**

Extracts the video frame at the specified time point in the timeline.

<span id="API definition"></span>
#### **API definition**

```objectivec
//  Extract the video frame at the specified time point in the timeline.

//  @param time              The time point in the timeline at which the video frame is to be extracted.

//  @param completion  The callback upon extraction completion.

- (void)getVideoFrameWithTime:(CMTime)time completion:(void(^)(UIImage * _Nullable, NSError * _Nullable))completion;
```


<span id="Sample code"></span>
#### **Sample code**

```objectivec
//  Extract the video frame at the 0.1s in the timeline.

[self.cutSamePlayer getVideoFrameWithTime:CMTimeMake(1, 10) completion:^(UIImage * image, NSError * error) {

    self.previewImage = image;

}];
```


<span id="Control playback"></span>
### **Control playback**

<span id="Feature"></span>
#### **Feature**

Controls playback, such as pausing a video, playing a video, or dragging the slider on the progress bar to the specified time point.

<span id="API definition"></span>
#### **API definition**

```objectivec
//  Control playback.

//  Play a video.

- (void)play;

//  Pause a video.

- (void)pause;



//  Drag the slider on the progress bar to the specified time point.

//  @param time                The time point.

//  @param completion    The callback upon slider dragging.

- (void)seekToTime:(CMTime)time completion:(nullable dispatch_block_t)completion;
```


<span id="Sample code"></span>
#### **Sample code**

```objectivec
//  Pauses playback.

self.cutSamePlayer pause];



//  Drag the slider on the progress bar to the specified time point and play the video from that time point.

[self.cutSamePlayer seekToTime:seekTime completion:^{

    @strongify(self)

    [self.cutSamePlayer play];

 }];
```


<span id="Edit asset clips"></span>
### **Edit asset clips**

You can update the length of a video clip, update the content of a text clip, or replace a video clip.

<span id="Obtain asset clip metadata"></span>
### **Obtain asset clip metadata**

<span id="Feature"></span>
#### **Feature**

The metadata of a video clip includes the video thumbnail and length.

The metadata of a text clip refers to the thumbnail of the video frame at the start time of the text.

<span id="API definition"></span>
#### **API definition**

```objectivec
/**

 * Thumbnail size: 100×100 pixels

 * @"kCSIFCutSameMetaInfoCoverImageKey": UIImage    The thumbnail of the video clip.

 * Video length information.

 * @"kCSIFCutSameMetaInfoDurationKey": NSNumber    The length of the video clip.

 * */

//  Obtain information about a video clip.

//  @param fragment: the video clip.

- (NSDictionary<NSString *, id> *)metaInfoForVideoFragment:(CSIFTemplateVideoEditFragment *)fragment;



/**

 * Thumbnail size: 100×100 pixels

 * kCSIFCutSameMetaInfoCoverImageKey: UIImage           The thumbnail of the video frame at the start time of the specified text.

 * */

//  Obtain information about a text clip.

//  @param fragment                                                               The text clip.

- (NSDictionary<NSString *, id> *)metaInfoForTextFragment:(CSIFTemplateTextFragment *)fragment;
```


<span id="Sample code"></span>
#### **Sample code**

```objectivec
NSMutableArray *fragmentImages = [[NSMutableArray alloc] init];

NSMutableArray *fragmentTimes = [[NSMutableArray alloc] init];



[self.cutSamePlayer.displayFragments enumerateObjectsUsingBlock:^(CSIFTemplateVideoEditFragment * _Nonnull obj, NSUInteger idx, BOOL * _Nonnull stop) {

   NSDictionary *metaInfo = [self.cutSamePlayer metaInfoForVideoFragment:obj];

   //  Obtain the thumbnail of the video clip.

   if ([metaInfo objectForKey:kCSIFCutSameMetaInfoCoverImageKey]) {

      [fragmentImages addObject:[metaInfo objectForKey:kCSIFCutSameMetaInfoCoverImageKey]];

   }

   //  Obtain the length of the video clip.

   if ([metaInfo objectForKey:kCSIFCutSameMetaInfoDurationKey]) {

      [fragmentTimes addObject:[metaInfo objectForKey:kCSIFCutSameMetaInfoDurationKey]];

   }

}];



//  Obtain the thumbnail of the video frame at the start time of the specified text.

NSDictionary *metaInfo = [self.cutSamePlayer metaInfoForTextFragment:textFragment];

UIImage *cover = [metaInfo objectForKey:kCSIFCutSameMetaInfoCoverImageKey];
```


<span id="Obtain text clips"></span>
### **Obtain text clips**

<span id="Feature"></span>
#### **Feature**

Obtains text clips. Asset clips include video clips and text clips.

<span id="API definition"></span>
#### **API definition**

```objectivec
//  The array of video clips.

//  The array of text clips whose content can be updated.

@property (nonatomic, copy, readonly) NSArray<CSIFTemplateTextFragment *> *canReplaceTextFragments;
```


<span id="Structure"></span>
#### **Structure**

```objectivec
//  The text clip.

@interface CSIFTemplateTextFragment : NSObject

//  The ID of the text clip.

@property (nonatomic, copy, readonly) NSString *payloadID;

//  The time range of the text clip.

@property (nonatomic, assign, readonly) CMTimeRange timeRange;

//  The content of the text clip.

@property (nonatomic, copy) NSString *content;

//  The thumbnail of the video frame at the start time of the text clip.

@property (nonatomic, strong) UIImage *albumImage;



@end
```


<span id="Update a text clip"></span>
### **Update a text clip**

<span id="Feature"></span>
#### **Feature**

Updates the text content of a text clip.

<span id="API definition"></span>
#### **API definition**

```objectivec
//  Update the text content.

//  @param fragment  The text clip.

//  @param text            The content of the text.

- (BOOL)updateTextFragment:(CSIFTemplateTextFragment *)fragment withText:(NSString *)text;
```


<span id="Sample code"></span>
#### **Sample code**

```objectivec
//  @param fragment  The text clip.

//  @param text            The content of the text.

[self.cutSamePlayer updateTextFragment:textFragment withText:textFragment.content];
```


<span id="Obtain video clips"></span>
### **Obtain video clips**

<span id="Feature"></span>
#### **Feature**

Obtains video clips. Asset clips include video clips and text clips.

<span id="API definition"></span>
#### **API definition**

```objectivec
//  The array of video clips.

@property (nonatomic, copy, readonly) NSArray<CSIFTemplateVideoEditFragment *> *displayFragments;
```


<span id="Structure"></span>
#### **Structure**

```objectivec
//  The video clip.

@interface CSIFTemplateVideoEditFragment : NSObject

//  The ID of the video clip.

@property (nonatomic, copy) NSString *payloadID;

//  The time range of the video clip in the timeline of the new video.

@property (nonatomic, assign) CMTimeRange targetTimeRange;

//  The time range of the video clip in the timeline of the original video.

@property (nonatomic, assign) CMTimeRange sourceTimeRaneg;

//  Indicates whether the video clip can be replaced.

@property (nonatomic, assign) BOOL canReplace;

//  Indicates whether the video clip is in overlay mode.

@property (nonatomic, assign) BOOL isSubVideo;

//  The thumbnail of the video frame at the start time of the text clip.

@property (nonatomic, strong) UIImage *albumImage;

//  The video cropping information.

@property (nonatomic, strong) CSIFVideoCropInfo *crop;

//  Indicates whether to play the video clip backward.

@property (nonatomic, assign) BOOL isReversed;

//  Indicates whether the asset is a video.

@property (nonatomic, assign) BOOL isVideo;

//  Path of a video or a picture.

@property (nonatomic, copy) NSString *assetPath;

@end
```


<span id="Update a video clip"></span>
### **Update a video clip**

<span id="Feature"></span>
#### **Feature**

Updates a video clip. You can update only the time range of the video clip.

<span id="API definition"></span>
#### **API definition**

```objectivec
// Update the time range of the video clip.

/**

 * Obtain the length of the video asset segment. Key value.

 * @"kCSIFCutSameTimeRangeValueKey" : NSValue<CMTimeRange>

 * */

//  Update the time range of the video clip.

//  @param info              The information such as the time range.

//  @param payloadID   The ID of the video clip.

- (BOOL)modifyFragmentWithInfo:(NSDictionary<NSString *, id> *)info payloadID:(NSString *)payloadID;
```


<span id="Sample code"></span>
#### **Sample code**

```objectivec
//  The time range.

CMTimeRange newRange = [self.editView currentTimeRange];

if (CMTimeCompare(newRange.start, self.fragment.sourceTimeRaneg.start) != 0) {

      NSValue *timeRangeValue = [NSValue valueWithCMTimeRange:newRange];

      //  Update the time range.

      [[self player] modifyFragmentWithInfo:@{kCSIFCutSameTimeRangeValueKey: timeRangeValue} payloadID:self.fragment.payloadID];

}
```


<span id="Replace a media asset"></span>
### **Replace a media asset**

<span id="Feature"></span>
#### **Feature**

Replaces a video clip. Before you call this API, you must call the replacement method of the **CSIFCutSameSource** object to preprocess the new clip so that it can be used to replace the original clip.

<span id="API definition"></span>
#### **API definition**

```objectivec
//  Replace a video clip.

//  @param asset             The asset model.

//  @param payloadID    The ID of the video clip.

- (BOOL)replaceFragmentWithAsset:(CSIFCutSameMaterialAssetModel *)asset withPayloadID:(NSString *)payloadID;
```


<span id="Sample code"></span>
#### **Sample code**

```objectivec
CSIFCutSameSource *source = CSIFCutSameSDK.shareInstance.source;

//  Replace a video clip.

[source replaceAsset:self.viewModel.inputData.singleAssetModel withAsset:self.viewModel.currentSelectAssetModels.firstObject progress:^(CGFloat progress) {

//  progress: the replacement progress. Valid values: 0 to 1.

} completion:^(CSIFCutSameMaterialAssetModel *martrialAsset, NSError *error) {

//  martrialAsset: Processed assets.

//  error: Indicates whether an error occurred.

  if (newMaterialAssetModel) {

  //  The preprocessing is successful. Replace the video clip.

     [self.cutSamePlayer replaceFragmentWithAsset:newMaterialAssetModel withPayloadID:self.displayFragments[self.curEditIndex].payloadID];

  }

}
```


<span id="Export a video"></span>
### **Export a video**

<span id="Feature"></span>
#### **Feature**

Exports a video.

<span id="API definition"></span>
#### **API definition**

```objectivec
//  Export the video.

//  @param config              The configuration for video export.

//   @param progress         The processing progress. Valid values: 0 to 100.

//  @param completion    The callback upon export completion.

- (void)exportVideoWithConfig:(CSIFVideoExportConfig *)config progress:(void (^)(CGFloat))progress completion:(void (^)(NSURL *videoURL, NSError *error))completion;
```


<span id="Sample code"></span>
#### **Sample code**

```objectivec
// 1080p, 6000kb/s

CSIFVideoExportConfig *config = [[CSIFVideoExportConfig alloc] init];

config.resolution = CSIFExportResolutionP1080;

config.bitrate = 6000000;

[self.cutSamePlayer exportVideoWithConfig:config

                                 progress:^(CGFloat progress) {

//  progress: the export progress. Valid values: 0 to 100.

} completion:^(NSURL *videoURL, NSError * _Nonnull error) {

//  The callback upon export completion.

}
```


<span id="Magic Template UI SDK integration"></span>
## **Magic Template UI SDK integration**

<span id="Present the UI"></span>
### **Present the UI**

<span id="Feature"></span>
#### **Feature**

Presents the UI.

<span id="API definition"></span>
#### **API definition**

```objectivec
//  Present the UI.

//  @param parentController     The parent view controller.

- (void)presentOnViewController:(UIViewController *)parentController;
```


<span id="Sample code"></span>
#### **Sample code**

```objectivec
- (void)showUISDK {

    //  Check the SDK authorization status.

    if (![self checkAuthAlert]) return;

    //  Create a template list UI.

    CSIFMVTemplatesTabViewController *mvtemplateVC = [[CSIFMVTemplatesTabViewController alloc] init];

    //  Present the UI.

    [mvtemplateVC presentOnViewController:self];

}
```


After the UI is presented, the Magic Template UI SDK implements the operations supported by Magic Template.

<span id="Export a video"></span>
### **Export a video**

<span id="Feature"></span>
#### **Feature**

Exported videos are automatically stored in the system album. The delegate of the SDK will receive a callback upon the export.

<span id="API definition"></span>
#### **API definition**

```objectivec
//  @param videoURL    The URL of the video.

//  @param error            The error information.

- (void)onExportFinish:(NSURL *)videoURL error:(NSError *)error;
```


<span id="Sample code"></span>
#### **Sample code**

```objectivec
//  Video exported.

- (void)onExportFinish:(NSURL *)videoURL error:(NSError *)error {

  if (!error) {

    NSLog(@" Video exported to:  %@", videoURL);

  }

}
```
