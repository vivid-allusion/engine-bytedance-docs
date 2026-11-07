---
title: "Managing iOS highlight clippings"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/150-managing-ios-highlight-clippings"
---

Highlight clipping is a technique used to manage the exposure of the brightest parts of an image or video, ensuring that they do not exceed the display's capability, which would result in a loss of detail and a washed\-out appearance. The highlight clipping process:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/971e8a1cefdb486ba3873e44705672af~tplv-goo7wpa0wc-image.image) </span>

<span id="da7a1c66"></span>
# Prerequisities


* Ensure you have obtained a valid license.

* You have produced or purchased template materials and have obtained the material package.

* Ensure that you have initialized the SDK. For more information, refer to [Step 1: Initializing the authorization configuration](https://docs.byteplus.com/docs/video-editor-sdk/150-initializing-and-preparing-the-ios-magic-template-sdk#96672fb0).


<span id="a13e2065"></span>
# Step 1: Confirming if certificates include highlight clipping authorization

To confirm if the certificate includes authorization related to highlight production, use the following method:

```objectivec
BOOL isAuth = [[EOAuthorization sharedInstance] isCheckAuthForHighLight]; 
```


<span id="ee67da24"></span>
# Step 2: Media scanning and scoring

Media Scanning and Scoring refers to a process within media processing or content management systems where the system analyzes and evaluates media files, such as images or videos.

<span id="782b5c01"></span>
## Scanning configuration

The system scans the media files, which may involve reading metadata, analyzing content, or both. This can be done to detect specific features, objects, scenes, or to gather information that helps in organizing or categorizing the media.

Create and configure an `ILAConfig` object with the highlight clipping authentication buffer and the path to the dependent model. The setup involves specifying the license buffer and the model directory:

```objectivec
/// Pass in the highlight authentication buffer and the path of the dependent model
ILAConfig *ilaConfig = [[ILAConfig alloc] initWithLicenceBuffer:[[EOAuthorization sharedInstance] cvLicenseBuffer] modelDir:[[NSBundle mainBundle] pathForResource:[NSString stringWithFormat:@"EOLocalResources.bundle/EffectResource/ILAModels.bundle"] ofType:nil]];

[ILAManager setConfig:ilaConfig];
[[ILAManager sharedInstance] initialization];

ILATaskConfig *taskConfig = [[ILATaskConfig alloc] initWithScene:ILAScanSceneAlbum];
```


<span id="8e894c7b"></span>
## Start scanning

The purpose of this code is to initiate a scanning process on a list of media assets (`assetList`) using a configuration (`taskConfig`) that defines how the scanning should be performed. The scanning process involves analyzing the media assets to extract relevant information, which can then be used for further processing, such as template matching.

Start scanning using `ILAManager` with the asset list and task configuration. Handle progress and completion with the provided callbacks:

```objectivec

    NSString *taskID = [[ILAManager sharedInstance] scanWithAssetList:assetList
                                                           taskConfig:taskConfig
                                                             progress:^(int32_t cur, int32_t total, int32_t code, ILAAsset * _Nonnull asset, ILAScanResult * _Nonnull result, BOOL hasScan, bool asset_cv_finish) {

    } finish:^(int32_t code, NSArray * _Nonnull result, NSDictionary * _Nonnull mapping) {
        
        /// After scanning, refer to 5.3 to finish template matching
        
    }];
```


<span id="3c85e76d"></span>
# Step 3: Matching recommended templates using results

This code is typically used in applications that require automated content analysis and processing, such as video editing tools or content recommendation systems. After scanning and analyzing media assets, the system matches the content with predefined templates to suggest or automatically apply edits that enhance the media based on its characteristics.

```objectivec
/// After the scan is complete, you can obtain the scan results based on the material ID
NSArray <ILAScanResult *> *scanResults = [[ILAManager sharedInstance] queryResultsWithLocalId:ilaAsset.assetId];

/// Use the scan results and template list, pass them to the SDK to get the matched template information, topN is the maximum number of matched templates
NSArray *matchedInfos = [EOHighLightWrapper matchTemplate:momentTemplates.copy scanResultList:hlResults topN:[EOHighLightManager sharedManager].topN];
```


<span id="4f85d7b3"></span>
# Step 4: Creating videos

For more information on creating videos, refer to [Managing Magic Template objects in iOS](https://docs.byteplus.com/docs/video-editor-sdk/150-managing-magic-template-objects-in-ios).

<span id="9d891c0c"></span>
# Highlight clipping data classes

These are the data classes used in iOS highlight clippings.

<span id="00e3ed33"></span>
## EOHLTemplateMatchedInfo

This class represents the result of the template matching process, containing information about the matched template and the list of media items that were used in the matching process along with their highlights results.


|**Parameter** |**Type** |**Description** |
|---|---|---|
|`momentTemplate` |EOMomentTemplate\* |The matched template information |
|`mediaList` |NSArray\* |List of items containing input media and their highlights results |


<span id="2ff9ad2a"></span>
## EOHLTemplateMatchedItem

This class contains details about each media item that was matched with a template, including the recognized media and the results of the extraction process, such as classification and aesthetic scoring.


|**Parameter** |**Type** |**Description** |
|---|---|---|
|`media` |EORecognizeMedia\* |The recognized media |
|`extractorResult` |EOHighLightResult\* |The classification and aesthetic scoring of the recognized media |


<span id="9c1758b9"></span>
## EORecognizeMedia

This class defines the structure for media items that are to be recognized and processed, including details such as the media's ID, file path, type, dimensions, duration, and creation date.


|**Parameter** |**Type** |**Description** |
|---|---|---|
|`mediaID` |NSString\* |Unique identifier for the media item |
|`path` |NSString\* |Local file path to the media item |
|`type` |int |Type of media: 1 for Image, 2 for Video |
|`width` |int |Width of the media item in pixels |
|`height` |int |Height of the media item in pixels |
|`durationMs` |long |Duration of the media item in milliseconds (set to 0 for images) |
|`createTimeMs` |long |Creation date of the media item in milliseconds since the epoch |
