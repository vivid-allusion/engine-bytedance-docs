---
title: "Editor module configuration and features"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/docs-ios-editor-module-configuration-and-features_1_1_0"
---

<span id="b5f6ce4d"></span>
# Settings

The settings classes include:


* EOEditorConfig

* EOEditorSceneConfig


<span id="f4a86df8"></span>
## EOEditorConfig

Using the builder pattern, all properties exposed externally in the `config` are set to `readonly`. Initialization is done through the corresponding initializer.

`EOEditorConfig` serves as a configuration container for the initialization parameters of the editing page. All sub\-configurations are located within this class.


|**Class** |**Field and Method** |**Type** |**Description** |
|---|---|---|---|
|EOEditorConfig |videoEditorConfig |EOVideoEditorViewControllerConfig |The ViewController configuration class of the editor screen, which can be used to configure UI elements, such as the sidebar. |
||* <br><br><br>(instancetype)initWithBlock:(void (^)(EOEditorConfigInitializer \*))block; |N/A |The initialization function. Using the builder pattern, all attributes exposed in `config` are readonly. Initialization is done uniformly using the corresponding initializer. |
|||||
|||||
|||||


<span id="0a04cc5f"></span>
### **Class definition**

```objectivec
@interface EOEditorConfig : NSObject

@property (nonatomic, strong, readonly) EOVideoEditorViewControllerConfig *videoEditorConfig;

- (instancetype)initWithBlock:(void (^)(EOEditorConfigInitializer *))block NS_DESIGNATED_INITIALIZER;

@end
```


<span id="da7ddcda"></span>
### EOVideoEditorViewControllerConfig

Setting up the editing page ViewController, the setting class for the primary editing page:


|**Class** |**Field and Method** |**Type** |**Description** |
|---|---|---|---|
|EOVideoEditorViewControllerConfig |sideBarConfig |EOEditorSideBarConfig |The configuration class for the sidebar. |
||musicBarHidden |Boolean |Whether the music bar can be hidden. The default value is `No`. |
||* <br><br><br>(instancetype)initWith:(EOVideoEditorViewControllerConfigInitializer \*)initializer; |N/A |The initialization function. |


<span id="596938c0"></span>
#### Class definition

```objectivec
@interface EOVideoEditorViewControllerConfig : NSObject

@property (nonatomic, strong, readonly) EOEditorSideBarConfig *sideBarConfig;

@property (nonatomic, assign) BOOL musicBarHidden;

- (instancetype)initWith:(EOVideoEditorViewControllerConfigInitializer *)initializer;

@end
```


<span id="951c81fa"></span>
## EOEditorSceneConfig

`EOEditorSceneConfig` is a class designed for configuring the behavior and appearance upon entering the editor screen. This class encapsulates initialization parameters, providing a structured approach to setting up the editor screen's environment.


|**Class** |**Field and Method** |**Type** |**Description** |
|---|---|---|---|
|EOEditorSceneConfig |draftModel |EOSDKDraftModel |The draft model, which is used for re\-entering the editor screen from the draft box. |
||resources |NSArray |Used for entering the editor screen from the camera screen or after selecting a footage item from the album. |
||backgroundMusic |id |Specifies the background music for shooting. |
||coverImage |UIImage |Specifies the first frame on the camera screen, which is used for redirection optimization. |
||previewContentMode |EOEditorPreviewContentMode |The video display mode. |


<span id="1d10a735"></span>
## Class definition

To enter the editor screen from different contexts, specific parameters need to be configured accordingly:


* **From the Draft Box**:

   * Set a value for the `draftModel` parameter to provide the necessary data from the draft box to the editor screen.

* **From the Camera Screen**:

   * Set values for the `resources`, `backgroundMusic`, and `coverImage` parameters based on the media data obtained from the camera screen. This includes providing resources such as video clips or images, background music, and a cover image for the editor screen.


```objectivec
@interface EOEditorSceneConfig : NSObject

///   Restore from draft
@property (nonatomic, strong) EOSDKDraftModel *draftModel;

/// Resources from Recorder or Album
@property (nonatomic, copy) NSArray<id> *resources;

/// Selected BGM Resource from Recorder
@property (nonatomic, strong, nullable) id backgroundMusic;

/// First resource thumbnail from Recorder
@property (nonatomic, strong, nullable) UIImage *coverImage;

/// Default is `EOEditorPreviewContentModeAspectFit`
@property (nonatomic, assign) EOEditorPreviewContentMode previewContentMode;

@end
```


<span id="4d59ad61"></span>
# Sidebar

The table below outlines the attributes and methods of the sidebar's configuration class:


|**Class** |**Field and Method** |**Type** |**Description** |
|---|---|---|---|
|EOEditorSideBarConfig |itemKeys |NSMutableArray |An array of sidebar element keys. By default, the following seven elements are provided and the order can be changed. No custom elements are supported.<br><br>Default value:<br><br>```JSON```<br>```@[ EOEditorBarItemKeyClip, // Edit.```<br>```EOEditorBarItemKeyText, // Text.```<br>```EOEditorBarItemKeySticker, // Text stickers.```<br>```EOEditorBarItemKeyFilter, // Filters.```<br>```EOEditorBarItemKeyEffect, // Special effects.```<br>```EOEditorBarItemKeyFaceSticker, // Facial effects.```<br>```EOEditorBarItemKeyVoice // Sound effects.```<br>```]```<br> |
||unfoldCount |NSUInteger |Counts the number of non\-collapsible elements starting from the top. |
||foldEnabled |Boolean |Whether the sidebar can be hidden. The default value is `Yes`. |


<span id="a981d013"></span>
## Class definition

```objectivec
@interface EOEditorSideBarConfig : NSObject

// Array of keys that presenting right side bar items.
// Could change the order. Custom new items not supported yet.
// default order: [ 
//     EOEditorBarItemKeyClip,
//      EOEditorBarItemKeyText,
//     EOEditorBarItemKeySticker,
//     EOEditorBarItemKeyFilter,
//     EOEditorBarItemKeyEffect,
//     EOEditorBarItemKeyFaceSticker,
//     EOEditorBarItemKeyVoice
/// ]
@property (nonatomic, strong) NSMutableArray<EOEditorBarItemKey> *itemKeys;

// The number of side bar items that would not be folded,
// count from the first object of `itemKeys`
// default is `5`
@property (nonatomic, assign) NSUInteger unfoldCount;

// Controls the fold mode for sidebar
// default is `YES`
@property (nonatomic, assign) BOOL foldEnabled;

@end
```


<span id="22d9eb8d"></span>
## **Sample code**

```Swift
let config = EOEditorConfig { initializer in
    initializer.configVideoEditorViewController { editorVCInitializer in
        //  Adjust the sequence of the functional buttons in the sidebar.
        editorVCInitializer.sideBarConfig.itemKeys.exchangeObject(at: 0, withObjectAt: 1)
    }
}

let sceneConfig = EOEditorSceneConfig()
sceneConfig.resources = info.mediaAssets
sceneConfig.backgroundMusic = info.backgroundMusic
sceneConfig.coverImage = info.coverImage

// If you want to directly enter editing using local resources, you can also construct a model that conforms to the EOMediaAssetProtocol protocol as follows and set it to sceneConfig.resources.
// let asset = EOMediaAssetDefaultImpl()
// asset.url = URL(fileURLWithPath: Bundle.main.path(forResource: "localVideo", ofType: "mp4") ?? "")
// sceneConfig.resources = [asset]

EOVideoEditorViewController.startEditor(with: config, sceneConfig: sceneConfig, presenter: presenter, delegate: self) { [weak self, weak presenter] error in
    if let err = error as? NSError, let vc = presenter {
        self?.showErrorAlert(err, presenter: vc)
    }
};
```


<span id="78ed5dd7"></span>
# Image editing feature

The image editing feature has been added, and it's enabled by default. The global configuration class is:


|**Class** |**Field and Method** |**Type** |**Description** |
|---|---|---|---|
|EOBusinessConfig |ImageEditingEnabled |Boolean |Whether the image editing feature can be switched off. The default value is `Yes`. |
|||||


<span id="12c95df1"></span>
## Class definition

```objectivec
@interface EOBusinessConfig : NSObject

/// Single image could be editing as image mode or shot video mode,
/// set `YES` to let editor process and export the input image as image, otherwise as video.
/// default `YES`
@property (nonatomic, assign) BOOL imageEditingEnabled;

@end
```


<span id="72bb1a1c"></span>
## Sample code

```Swift
// disable image editing
EOSDK.businessConfig().imageEditingEnabled = false
```


<span id="cb0a6df5"></span>
# Navigation push function

Navigation push refers to the action of pushing a new view controller onto a navigation stack in iOS development. In iOS apps that use navigation controllers, a navigation push transitions the user to a new screen by pushing the destination view controller onto the navigation stack. This typically creates a navigation bar at the top of the screen, allowing the user to navigate back to the previous screen using a back button.

```Swift
if let editorViewController = EOVideoEditorViewController(config: config, sceneConfig: sceneConfig) {
    editorViewController.delegate = self
    presenter.navigationController?.pushViewController(editorViewController, animated: true)
} else {
    self.showToast("show editor failed")
}
```
