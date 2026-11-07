---
title: "Video export APIs for iOS"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/120-video-export-apis-for-ios"
---

This topic details the video export APIs for iOS.

<span id="80284d26"></span>
# Prerequisities—Initializing EOExportManager

To access export APIs, you need to use the `EOExportManager` class. To do this, initialize an instance of the `EOExportManager` class. This enables you to utilize the export operations mentioned in the following topics.

<span id="c1a9f45b"></span>
## **Request parameters**


|**Parameter** |**Type** |**Description** |**Source** |
|---|---|---|---|
|model |EOExportModel \* |Video information model related to initialization and export. |SDK callback |


<span id="b7eebcbd"></span>
## **Sample code**

```objectivec
[[EOExportManager alloc] initWithExportModel:self.model] 
```


<span id="11f3d6b3"></span>
## **Response parameters**

The `EOExportManager` instance is returned by the APIs that request it.

<span id="28d7eac4"></span>
# Retrieve the cover image

**Request parameters**


|**Parameter** |**Type** |**Description** |
|---|---|---|
|videoSize |CGSize |The width and height of the video. |


**Method definition**

```objectivec
- (void)getVideoCoverImage:(CGSize)videoSize success:(nullable void(^)(UIImage *draftImg, UIImage *videoImg, int64_t videoFrameTime, NSString *coverType))completionBlock 
```


**Sample code**

```objectivec
[self.manager getVideoCoverImage:self.model.originRatioSize success:^(UIImage * _Nonnull draftImg, UIImage * _Nonnull videoImg, int64_t videoFrameTime, NSString * _Nonnull coverType) {
        self.videoFrameTime = videoFrameTime;
        if ([coverType isEqualToString:@"image"]) {
            self.isCoverImage = YES;
        } 
        if (draftImg) {
            self.coverView.image = draftImg;
            self.coverImg = draftImg;
        }
        else {
            self.coverView.image = videoImg;
            self.coverImg = videoImg;
        }
    }];
```


**Response parameters**

`completionBlock` callback


|**Parameter** |**Type** |**Description** |
|---|---|---|
|draftImg |UIImage |The cover image of the draft box. |
|videoImg |UIImage |The cover image selected from video frames. |
|videoFrameTime |int64_t |The time position of the frame in the video from which the cover image is selected. |
|coverType |NSString |The type of the cover. Valid values:<br><br>image: a cover image.<br><br>videoFrame: a cover video frame. |


<span id="f394975c"></span>
# Set the canvasSize

**Method definition**

```objectivec
- (void)setCanvasSize; 
```


**Sample code**

```objectivec
[self.manager setCanvasSize]; 
```


<span id="ba447e19"></span>
# Set the preview

**Request parameters**


|**Parameter** |**Type** |**Description** |
|---|---|---|
|preview |UIView |The parent view of the video to be displayed. |


**Method definition**

```objectivec
- (void)resetPlayeView:(UIView *)preview;
```


**Sample code**

```objectivec
CGFloat ratio = [self.manager getVideoSize].width/[self.manager getVideoSize].height;
    CGFloat previewViewHeight = EO_ScreenHeight() * 445.0/812.0;
    CGFloat newHeight = ratio>1 ? EO_ScreenWidth()/ratio : previewViewHeight;
    CGFloat newWidth = ratio>1 ? EO_ScreenWidth() : newHeight*ratio;
    CGFloat newX = (EO_ScreenWidth()-newWidth)/2;
    CGFloat newY = EO_NavBarHeight()+48+(previewViewHeight-newHeight)/2;
    self.previewView = [[UIView alloc] initWithFrame:CGRectMake(newX, newY, newWidth, newHeight)];
    [self.view addSubview:self.previewView];
    [self.manager resetPlayeView:self.previewView]; 
```


<span id="17bcccc2"></span>
# Pause a video

**Method definition**

```objectivec
- (void)pause; 
```


**Sample code**

```objectivec
[self.manager pause]; 
```


<span id="a417f2fc"></span>
# Set the video to a specified time

**Request parameters**


|**Parameter** |**Type** |**Description** |
|---|---|---|
|videoFrameTime |int64_t |Specifies the time position in the video. |
|isSmooth |Boolean |Specifies whether the video starts exactly at the set time. |


**Method definition**

```objectivec
- (void)setVideoRatioTime:(int64_t)videoFrameTime isSmooth:(BOOL)isSmooth; 
```


**Sample code**

```objectivec
[self.manager setVideoRatioTime:0 isSmooth:NO]; 
```


<span id="5f5332f1"></span>
# Retrieve the video resolution

**Method definition**

```objectivec
- (CGSize)getVideoSize; 
```


**Sample code**

```objectivec
CGFloat ratio = [self.manager getVideoSize].width/[self.manager getVideoSize].height; 
```


**Response parameters**


|**Type** |**Description** |
|---|---|
|CGSize |The video resolution. |


<span id="58025be1"></span>
# Export a video

**Method definition**

```objectivec
- (void)exportVideoWithProgress:(void (^_Nullable )(CGFloat progress))progressBlock resultBlock:(void (^)(NSError *error,id result))exportBlock; 
```


**Sample code**

```objectivec
[self.manager exportVideoWithProgress:^(CGFloat progress) {
            @strongify(self) 
            NSLog(@"%.2f",progress);
            self.videoSlider.value = progress/100;
            self.progressLabel.text = [NSString stringWithFormat:@"%.f%@",progress,@"%"];
            [self.progressLabel mas_updateConstraints:^(MASConstraintMaker *make) {
                make.left.equalTo(self.videoSlider.mas_left).offset(self.videoSlider.frame.size.width*progress/100-17);
            }];
        } resultBlock:^(NSError * _Nonnull error, id  _Nonnull result) {
            @strongify(self)
            [self restoreState];
            if (error || !result) {
                if ([error.domain isEqualToString:@"cancelProcess"]) {
                    [self.view makeToast:EOExportUILocalization(@"eo_export_import_cancel_export_tip") duration:1.5f position:CSToastPositionCenter];
                }
                else {
                    [self.view makeToast:EOExportUILocalization(@"eo_export_import_error") duration:1.5f position:CSToastPositionCenter];
                }
            }
            else {
                NSURL *filePath = result;
                if (self.delegate && [self.delegate respondsToSelector:@selector(exportVideoPath:videoImage:)]) {
                    [self.delegate exportVideoPath:filePath.path videoImage:self.coverView.image];
                    [self restoreState];
                }
                else {
                    [self.view makeToast:EOExportUILocalization(@"eo_export_import_success") duration:1.5f position:CSToastPositionCenter];
                    UISaveVideoAtPathToSavedPhotosAlbum(filePath.path, self, @selector(video:didFinishSavingWithError:contextInfo:), nil);
                }
            }
        }];
```


**Response parameters**

`progressBlock` callback


|**Parameter** |**Type** |**Description** |
|---|---|---|
|progress |CGFloat |The progress of video export. |


`exportBlock` callback


|**Parameter** |**Type** |**Description** |
|---|---|---|
|error |NSError |The error message for the failed export. |
|result |id |The success message for the export. |


<span id="1913b464"></span>
# Cancel an export

**Method definition**

```objectivec
- (void)cancelExport; 
```


**Sample code**

```objectivec
[self.manager cancelExport]; 
```


<span id="535a6daa"></span>
# Save a cover image

**Request parameters**


|**Parameter** |**Type** |**Description** |**Remarks** |
|---|---|---|---|
|coverImg |UIImage |The cover image. | |
|videoFrameTime |int64_t |The time position of the frame in the video. |If the cover image is selected from an album, the value is 0. |
|type |int |The type of the cover image. |* An image from the album.<br><br>* A video frame. |


**Method definition**

```objectivec
- (void)saveCoverImage:(UIImage *)coverImg time:(int64_t)videoFrameTime canvasType:(int)type;
```


**Sample code**

```objectivec
self.manager saveCoverImage:self.coverView.image time:self.videoFrameTime canvasType:self.isCoverImage ? 1: 2];
```


<span id="fc9860af"></span>
# Retrieve the FPS array

**Method definition**

```objectivec
- (NSArray *)exportFPSTitleArr; 
```


**Sample code**

```objectivec
[self.manager exportFPSTitleArr];
```


<span id="a2368488"></span>
# Retrieve the resolution array

**Method definition**

```objectivec
- (NSArray *)exportPresentTitleArr;
```


**Sample code**

```objectivec
[self.manager exportPresentTitleArr];
```


<span id="57a7bb4e"></span>
# Set the FPS

**Request parameters**


|**Parameter** |**Type** |**Description** |
|---|---|---|
|index |NSInteger |The FPS array subscript. |


**Method definition**

```objectivec
- (void)setExportFPSSelectIndex:(NSInteger)index;
```


**Sample code**

```objectivec
[self.manager setExportFPSSelectIndex:fpsIndex];
```


<span id="ccc9d1d3"></span>
# Set the resolution

**Request parameters**


|**Parameter** |**Type** |**Description** |
|---|---|---|
|index |NSInteger |The resolution array subscript. |


**Method definition**

```objectivec
- (void)setExportPresentSelectIndex:(NSInteger)index;
```


**Sample code**

```objectivec
[self.manager setExportPresentSelectIndex:resolutionIndex];
```


<span id="48d9bb47"></span>
# Extract a video frame

**Request parameters**


|**Parameter** |**Type** |**Description** |
|---|---|---|
|atTime |NSTimeInterval |The time position of the extracted video frame. |
|size |CGSize |The video resolution. |
|isLastImage |BOOL |Marks the last image in the case of multiple calls. |


**Method definition**

```objectivec
- (void)getProcessedPreviewImageAtTime:(NSTimeInterval)atTime
                         preferredSize:(CGSize)size
                           isLastImage:(BOOL)isLastImage
                           compeletion:(void (^)(UIImage *image, NSTimeInterval atTime))compeletion;
```


**Sample code**

```objectivec
CGFloat ratioTime = self.videoFrameTime * 1.0 / USEC_PER_SEC;
        @weakify(self);
        [self.manager getProcessedPreviewImageAtTime:ratioTime preferredSize:[self.manager getVideoSize] isLastImage:NO compeletion:^(UIImage * _Nonnull image, NSTimeInterval atTime) {
            @strongify(self);
            !self.onDismiss ?: self.onDismiss(image, self.videoFrameTime,NO);
            [self dismissViewControllerAnimated:YES completion:nil];
        }];
```


**Response parameters**

`completion` callback


|**Parameter** |**Type** |**Description** |
|---|---|---|
|image |UIImage |The video frame successfully extracted. |
|atTime |NSTimeInterval |The time position of the extracted video frame. |


<span id="d7cc519a"></span>
# Extract multiple video frames

**Request parameters**


|**Parameter** |**Type** |**Description** |
|---|---|---|
|atTimes |NSArray |The time array of extracted video frames. |
|size |CGSize |The video resolution. |
|withEffect |BOOL |Specifies whether the extracted video frames have special effects. |


**Method definition**

```objectivec
- (void)getPreviewImages:(NSArray *)atTimes
           preferredSize:(CGSize)size
              withEffect:(BOOL)withEffect
              frameBlock:(void (^)(UIImage *image, NSTimeInterval atTime))frameBlock;
```


**Sample code**

```objectivec
CGSize size = self.previewView.frame.size;
    NSTimeInterval durationStep = [self.manager totalVideoDuration] / 12;
    NSMutableArray *timeArray = [NSMutableArray arrayWithCapacity:0];
    for (NSInteger index = 0; index < 12; index++) {
        [timeArray addObject:[NSNumber numberWithFloat:durationStep * index]];
    }
    @weakify(self);
    [self.manager getPreviewImages:[timeArray copy] preferredSize:size withEffect:YES frameBlock:^(UIImage * _Nonnull image, NSTimeInterval atTime) {
        @strongify(self);
        if (image) {
            [self.frames addObject:image];
            if (self.frames.count == 12) {
                [self.pickerView updateVideoFrames:self.frames durationRatios:self.durationRatios];
            }
        }
    }];
```


**Response parameters**

`frameBlock` callback


|**Parameter** |**Type** |**Description** |
|---|---|---|
|image |UIImage |The video frames successfully extracted. |
|atTime |NSTimeInterval |The time positions of the extracted video frames. |


<span id="223866d1"></span>
# Extracting a frame from a video (current frame)

**Method definition**

```objectivec
//Extracting a frame from a video (current frame)
54- (UIImage *)capturePreviewUIImage; 
```


**Sample code**

```objectivec
[self.manager capturePreviewUIImage]; 
```


**Response parameters**


|**Parameter** |**Description** |
|---|---|
|UIImage |Current frame image. |


<span id="c0ad40d7"></span>
# Retrieve the total duration of a video

**Method definition**

```objectivec
- (NSTimeInterval)totalVideoDuration;
```


**Sample code**

```objectivec
NSTimeInterval durationStep = [self.manager totalVideoDuration] / 12;
```


**Response parameters**


|**Type** |**Description** |
|---|---|
|NSTimeInterval |The video duration. |


<span id="936c119f"></span>
# Select a photo from the photo library

**Method definition**

```objectivec
- (void)getPickSingleImageResourceWithCompletion:(nullable void(^)(NSURL * _Nullable pickImage, NSError * _Nullable error, BOOL cancel))completionBlock;
```


**Sample code**

```objectivec
[self.manager getPickSingleImageResourceWithCompletion:^(UIImage * _Nullable pickImage, NSError * _Nullable error, BOOL cancel) {
                    @strongify(self);
                    if (pickImage) {
                        [self coverAlbumImageCrop:self.view coverViewImage:pickImage];
                    }
                }];
```


**Response parameters**

`completionBlock` callback


|**Parameter** |**Type** |**Description** |
|---|---|---|
|pickImage |NSURL |The path of the photo selected from the photo library. |
|error |NSError |The error message for the photo selection failure. |
|cancel |BOOL |Specifies whether to cancel the operation. |


<span id="c91b75e5"></span>
# Retrieve the duration of the main track

**Method definition**

```objectivec
- (CGFloat)mainTrackMaxEnd;
```


**Sample code**

```objectivec
[self.manager mainTrackMaxEnd]
```


**Response parameters**


|**Type** |**Description** |
|---|---|
|CGFloat |The duration of the main track of a video. |


<span id="564e5131"></span>
# Specify whether to add a cover during export

**Request parameters**


|**Parameter** |**Type** |**Description** |
|---|---|---|
|isCover |Boolean |Specifies whether to add a cover. |


**Method definition**

```objectivec
- (void)shouldAddCover:(BOOL)isCover;
```


**Sample code**

```objectivec
[self.manager shouldAddCover:NO];
```


<span id="53c3adb2"></span>
# Specify whether to add a watermark during export

**Request parameters**


|**Parameter** |**Type** |**Description** |
|---|---|---|
|shouldAddWaterMark |Boolean |Specifies whether to add a watermark. |


**Method definition**

```objectivec
- (void)shouldAddWaterMark:(BOOL)shouldAddWaterMark;
```


**Sample code**

```objectivec
[self.manager shouldAddWaterMark:YES];
```


<span id="5dcac3c8"></span>
# Set the watermark image

**Request parameters**


|**Parameter** |**Type** |**Description** |
|---|---|---|
|waterMarkImage |UIImage |The image to be used as the watermark. |


**Method definition**

```objectivec
- (void)addWaterMarkImage:(UIImage *)waterMarkImage;
```


**Sample code**

```objectivec
[self.manager addWaterMarkImage:EOExportUIImage(@"eo_export_waterMark")];
```


<span id="7e116190"></span>
# Set the watermark size

**Request parameters**


|**Parameter** |**Type** |**Description** |
|---|---|---|
|waterMarkSize |CGSize |**Watermark size calculation method**: current video resolution / 375 \* size width and height |


**Method definition**

```objectivec
- (void)setWaterMarkSize:(CGSize)waterMarkSize;
```


**Sample code**

```objectivec
CGFloat WaterMarkWidth = 29;
        CGFloat WaterMarkHeight = 31;
        switch (self.presentIndex) {
            case 0:
                WaterMarkHeight = WaterMarkHeight * (540/375);
                WaterMarkWidth = WaterMarkWidth * (540/375);
                break;
            case 1:
                WaterMarkHeight = WaterMarkHeight * (720/375);
                WaterMarkWidth = WaterMarkWidth * (720/375);
                break;
            case 2:
                WaterMarkHeight = WaterMarkHeight * 1080/375;
                WaterMarkWidth = WaterMarkWidth * (1080/375);
                break;
            case 3:
                WaterMarkHeight = WaterMarkHeight * (2160/375);
                WaterMarkWidth = WaterMarkWidth * (2160/375);
                break;
            default:
                break;
        }
[self.manager setWaterMarkSize:CGSizeMake(WaterMarkWidth, WaterMarkHeight)];
```


<span id="d9944346"></span>
# Image cropping page

**Request parameters**


|**Parameter** |**Type** |**Description** |
|---|---|---|
|vc |UIViewController |The current controller. |
|imagePath |NSString |The image path. |


**Method definition**

```objectivec
- (void)pushCropVC:(UIViewController *)vc imagePath:(NSString *)imagePath Completion:(nullable void(^)(NSString *imagePath))completionBlock;
```


**Sample code**

```objectivec
[weakSelf.manager getPickSingleImageResourceWithCompletion:^(NSURL * _Nullable pickImage, NSError * _Nullable error, BOOL cancel) {
    if (pickImage) { 
        [weakSelf.manager pushCropVC:weakSelf imagePath:[pickImage path] Completion:^(NSString * _Nonnull imagePath) {
            if (imagePath.length) {
                weakSelf.coverView.image = [UIImage imageWithContentsOfFile:imagePath];
                weakSelf.pickerView.isSelectPickAlbumImage = YES;
                [weakSelf switchPreviewOrPickAlbumImage:YES];
            }
        }];
    }
}];
```


**Response parameters**


|**Type** |**Description** |
|---|---|
|completionBlock |The path of the cropped image. |


<span id="990f5995"></span>
# Set the canvas color (black by default)

**Request parameters**


|**Parameter** |**Type** |**Description** |
|---|---|---|
|color |UIColor |The canvas color. |


**Method definition**

```objectivec
- (void)setCanvasColor:(UIColor *)color; 
```


**Sample code**

```objectivec
[self.manager setCanvasColor:[EOExportUIHelper eo_colorWithHex:@"000000"]]; 
```


<span id="e5959dab"></span>
# Configuring metadata

**Request parameters**


|**Parameter** |**Type** |**Description** |
|---|---|---|
|metadata |NSDictionary |* "com.apple.quicktime.copyright"//AVMetadataCommonKeyCopyrights<br><br>* "com.apple.quicktime.information"//AVMetadataQuickTimeMetadataKeyInformation<br><br>* "com.apple.quicktime.software" // AVMetadataCommonKeySoftware<br><br>* Others |


**Method definition**

```objectivec
- (void)setMetadata:(NSDictionary <NSString*,NSString*> *)metadata; 
```


**Sample code**

```objectivec
NSDictionary * metadataDict = [[NSDictionary alloc] initWithObjectsAndKeys:@"EffectOne",@"com.apple.quicktime.copyright", nil];
        [self.manager setMetadata:metadataDict]; 
```


<span id="676a0278"></span>
# Exporting images

**Request parameters**


|**Parameter** |**Type** |**Description** |
|---|---|---|
|completion |void (^)(UIImage \* _Nullable image, NSError \* _Nullable error) |Export completion callback. |


**Method definition**

```objectivec
/// export image 
- (void)exportImageWithCompletion:(void (^)(UIImage * _Nullable image, NSError * _Nullable error))completion;
```


**Sample code**

```objectivec
    [self.manager shouldAddWaterMark:YES]; 
    [self.manager addWaterMarkImage:EOExportUIImage(@"eo_export_waterMark")];
    [self.manager setWaterMarkSize:self.warterMarkSize];
    [self.manager shouldAddCover:NO];
    __weak typeof(self) weakSelf = self;

    [self.manager exportImageWithCompletion:^(UIImage * _Nullable image, NSError * _Nullable error) {
        __strong typeof(self) strongSelf = weakSelf;
        if (error || !image) {
            [strongSelf.view makeToast:EOExportUILocalization(@"eo_export_save_error") duration:1.5f position:CSToastPositionCenter];
            return;
        }
        
        if (strongSelf.delegate && [strongSelf.delegate respondsToSelector:@selector(exportViewController:didExportImage:)]) {
            [strongSelf.delegate exportViewController:strongSelf didExportImage:image];
            [strongSelf restoreState];
        } else {
            [strongSelf saveImageToPhotoLibrary:image];
        }
    }];
```
