---
title: "Album configuration and features"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/140-album-configuration-and-features"
---

The album is an independent component in BytePlus Video Editor SDK. It allows you to perform operations such as selecting one or more items, previewing images and videos, and cropping photos. It can be used in services that require the album feature.

<span id="132d47f9"></span>
# Album main class description

<span id="41952da3"></span>
## DAKResourcePicker

`DAKResourcePicker` calls the album.

```Swift
///   Call the album.
/// - Parameters:  
///   - config: Album settings.
///   - completion: A callback for the completion of calling the album.
- (void)pickResourceWithConfig:(DAKResourcePickerConfig *)config
                    completion:(DAKResourcePickerCompletion)completion;
```


<span id="fd170d2e"></span>
## DAKResourcePickerConfig

The configuration class for the album, which can be configured as needed.

The following table describes some attributes:


|**Attribute** |**DataType** |**Default Value** |**Description** |
|---|---|---|---|
|hintText |NSString |You can select both photos and videos. |The text displayed at the bottom of the list of photos in the album. The text key is `eo_album_tips`. |
|minDuration |NSUInteger |100 |The minimum length of a video, in ms. |
|maxDuration |NSUInteger |60 × \*\* 60 \*\* × 1,000. |The maximum length of a video, in ms. |
|maxSelectCount |NSUInteger |35 |The maximum number of resources that can be selected from the album. |
|minSelectCount |NSUInteger |1 |The minimum number of resources that can be selected from the album. |
|imageEnable |Boolean |Yes |Specifies whether images can be selected. |
|videoEnable |Boolean |Yes |Specifies whether videos can be selected. |
|allEnable |Boolean |Yes |Specifies whether both images and videos can be selected. |
|showGif |Boolean |Yes |Specifies whether GIFs can be displayed. |
|singleSelect |Boolean |No |Specifies whether only one resource can be selected. |
|canRepeat |Boolean |Yes |Specifies whether repeated resources can be selected from the album. |


<span id="916f7c03"></span>
### Class definition

```objectivec
///   The displayed copy at the bottom of the album list. 
@property (nonatomic, copy) NSString *hintText;
  
/// The minimized video duration in milliseconds. The default value is 100 ms.
@property (nonatomic, assign) NSUInteger minDuration;

/// The maximized video duration in milliseconds. The default value is 60 * 60 * 1000 ms.
@property (nonatomic, assign) NSUInteger maxDuration;

/// The upper limit on the number of albums that you can choose. The default number is 35.
@property (nonatomic, assign) NSUInteger maxSelectCount;

///  The lower limit on the number of albums that you can choose. The default number is 1.
@property (nonatomic, assign) NSUInteger minSelectCount;

/// Whether to allow photo selections. By default, this parameter is set to YES.
@property (nonatomic, assign) BOOL imageEnable;

/// Whether to allow video selections. By default, this parameter is set to YES.
@property (nonatomic, assign) BOOL videoEnable;

/// Whether to allow photo and album selections. By default, this parameter is set to YES.
@property (nonatomic, assign) BOOL allEnable;

/// Whether to display GIF pictures. By default, this parameter is set to YES.
@property (nonatomic, assign) BOOL showGif;

/// Whether single selection is enabled. By default, this parameter is set to NO.
@property (nonatomic, assign) BOOL singleSelect;

/// Whether to allow repeatedly selecting albums. By default, this parameter is set to YES.
@property (nonatomic, assign) BOOL canRepeat;
```


<span id="73973f7b"></span>
## DAKResourcePickerModelProtocol

After selecting resources from the album, the application invokes a protocol that represents the type of array element chosen. This facilitates seamless handling and processing of the selected resources, enhancing the user experience in managing multimedia content.

Functions of this class are shown in the following table:


|**Function** |**Description** |**Remarks** |
|---|---|---|
|\-(DVEAlbumAssetMediaType)type; |The type of resource to be obtained from the album. |The value `DVEAlbumAssetMediaType` indicates the enumeration type, `DVEAlbumAssetMediaTypeVideo` indicates the video type, and<br><br>`DVEAlbumAssetMediaTypeImage` indicates the image type. |
|\-(NSData \*)imageData; |The binary data of the resource in the album. |N/A |
|\-(NSURL \*)videoURL; |The path of the resource in the album. |N/A |


<span id="f989e42c"></span>
## DAKResourcePickerModel

After completing the selection from the album, the application invokes an array of elements in accordance with the DAKResourcePickerModelProtocol protocol. This ensures adherence to predefined standards and facilitates seamless handling of selected resources within the application.

Attributes of this class are shown in the following table:


|**Attribute** |**Description** |**Remarks** |
|---|---|---|
|type |The type of resource to be obtained from the album. |The value `DVEAlbumAssetMediaType` indicates the enumeration type, `DVEAlbumAssetMediaTypeVideo` indicates the video type, and<br><br>`DVEAlbumAssetMediaTypeImage` indicates the image type. |
|imageData |The binary data of the resource in the album. |N/A |
|videoURL |The path of the resource in the album. |N/A |


<span id="491891ca"></span>
## **Sample code for an album call**

```Swift
// Declare the prioritized DAKResourcePicker object.
    private lazy var resourcePicker = {
        return DAKResourcePicker()
    }()  
    // Call the album.
    let config = DAKResourcePickerConfig()
    //Single selection is not supported.
    config.singleSelect = false
    // Choose videos or photos. 
    config.pickType = .imageVideo
    resourcePicker.pickResource(with: config) { [weak self] resources in
         //Handle the response sent back by the callback function according to your business logic. 
    }
```


The video export interface is usually customized by you. As this code is open\-sourced in the sample for you to refer to and reuse, you can refer to the [iOS package deliverables list](https://docs.byteplus.com/docs/video-editor-sdk/140-ios-package-deliverables-list) for more information. Alternatively, you can directly call the corresponding video export interfaces by referring to [Video export APIs for iOS](https://docs.byteplus.com/docs/video-editor-sdk/140-video-export-apis-for-ios).
