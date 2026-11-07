---
title: "Camera module configuration and features"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/docs-ios-camera-module-configuration-and-features_1_1_0"
---

This topic provides a concise overview of how to use and configure a camera module and its parameters.

<span id="c433cb80"></span>
# Settings: EORecorderConfig

Using the builder pattern, all properties exposed externally in the `config` are read\-only. Initialization is done through the corresponding initializer.

`EORecorderConfig` serves as the configuration container and contains the initialization parameters for the shooting page. All sub\-configurations are placed under this class.


|**Class** |**Field and Method** |**Type** |**Description** |
|---|---|---|---|
|EORecorderConfig |modelPath |NSString |The path of the model files used by the camera module. Default value: EOBaseKit.modelResourceDir. |
||cameraPosition |AVCaptureDevicePosition |The default camera for the camera module. Default value: AVCaptureDevicePositionFront, which indicates the front\-facing camera. |
||videoResolution |EORecorderVideoResolution |The video resolution for the camera module. Valid values: 540p, 720p, 1280p, and 4K.<br><br>The resolution depends on the hardware and can be at most 720p for the front\-facing camera of some outdated devices.<br><br>For iPhone 7 and later, the default value is EORecorderVideoResolution1080p. For earlier devices, the default value is EORecorderVideoResolution720p. |
||recorderViewControllerConfig |EORecorderViewControllerConfig |The ViewController configuration class of the camera screen, which can be used to configure UI elements, such as the sidebar. |
||(instancetype)initWithBlock:(void (^)(EORecorderConfigInitializer \*))block | |The initialization function. Using the builder pattern, all attributes exposed in `config` are readonly. Initialization is done uniformly through the corresponding initializer. For more information, see the following examples. |


<span id="fb99d92b"></span>
## Class definition

```Java
@interface EORecorderConfig : NSObject

//  The file path of model used by the recorder. By default, this parameter is set to 'EOBaseKit.modelResourceDir'.
@property (nonatomic, copy, readonly) NSString *modelPath;

// The default camera of the recorder. By default, the parameter is set to AVCaptureDevicePositionFront, indicating the front camera is used.
@property (nonatomic, assign, readonly) AVCaptureDevicePosition cameraPosition;

// The resolution of the recorder. Available options include 540p, 720p, 1280p, and 4k.
// The choice of resolution depend on the devices you use. Some old versions of devices only support using the resolution of 720p at most.
// The default value for iPhone 7 or later is 'EORecorderVideoResolution1080p'.
 // The default value for older versions of devices is 'EORecorderVideoResolution720p'.
@property (nonatomic, assign, readonly) EORecorderVideoResolution videoResolution;

// ViewController is a configuration class of the recording page.
@property (nonatomic, strong, readonly) EORecorderViewControllerConfig *recorderViewControllerConfig;

// Initialize the below function.
- (instancetype)initWithBlock:(void (^)(EORecorderConfigInitializer *))block;

@end
```


<span id="56efd1a3"></span>
## Set the path of EORecorderConfig in iOS

This code snippet shows how to quickly set up the model file path using `EORecorderConfig`'s simple initializer. By using the path from `EOBaseKit.modelResourceDir()`, it makes setting up iOS projects easier and clearer.

```Java
let config = EORecorderConfig { initializer in
    //  Configure the path of the model file. 
    initializer.modelPath = EOBaseKit.modelResourceDir()
}
```


<span id="1265f1b0"></span>
## EORecorderViewControllerConfig

Set the ViewController of the camera screen, which is the class for the first screen of the camera module.


|**Class** |**Field and Method** |**Type** |**Description** |
|---|---|---|---|
|EORecorderViewControllerConfig |sideBarConfig |EORecorderSideBarConfig |The configuration class for the sidebar. |
||musicBarHidden |Boolean |Whether the music bar should be hidden. The default is `No`. |
||stickerButtonHidden |Boolean |Whether the sticker button should be hidden. The default is `No`. |
||albumButtonHidden |Boolean |Whether the album button should be hidden. The default is `No`. |
||\-(instancetype)initWithInitializer:(EORecorderViewControllerConfigInitializer \*)initializer | |The initialization function. |


<span id="84d98e86"></span>
### Class definition

```JSON
@interface EORecorderViewControllerConfig : NSObject

 //  The configuration class of the sidebar.
@property (nonatomic, strong, readonly) EORecorderSideBarConfig *sideBarConfig;

/// Top middle music bar visible
/// default `NO`
@property (nonatomic, assign) BOOL musicBarHidden;

/// Bottom left sticker button visible
/// default `NO`
@property (nonatomic, assign) BOOL stickerButtonHidden;

/// Bottom right sticker button visible
/// default `NO`
@property (nonatomic, assign) BOOL albumButtonHidden;

 // Initialize the below function.
- (instancetype)initWithInitializer:(EORecorderViewControllerConfigInitializer *)initializer;

@end
```


<span id="e0414fda"></span>
# Sidebar: EORecorderSideBarConfig

The following table describes the configuration class of the sidebar.


|**Class** |**Field and Method** |**Type** |**Description** |
|---|---|---|---|
|EORecorderSideBarConfig |itemKeys |NSMutableArray |An array of sidebar element keys. By default, the following six elements are provided and the order can be changed. No custom elements are supported.<br><br>Default value:<br><br>```JSON```<br>```@[ EORecordBarItemRotateCameraKey, // Flip the camera.```<br>```EORecordBarItemFlashKey, // Flash.```<br>```EORecordBarItemTimerKey, // Countdown timer.```<br>```EORecordBarItemFiltersKey, // Filters.```<br>```EORecordBarItemBeautyKey, // Beauty effects.```<br>```EORecordBarItemSpeedKey, // Speed.```<br>```]```<br> |
||unfoldCount |NSUInteger |Counts the number of non\-collapsible elements starting from the top. |
||foldEnabled |Boolean |Whether the sidebar can be hidden. The default value is `Yes`. |


<span id="ac0ad8e7"></span>
## Class definition

```Java
@interface EORecorderSideBarConfig : NSObject

// An array of the key of side bar elements. The following six elements are provided by default, and the display sequence of these elements can be modified. Currently, adding custom elements is not supported. 
// Default elements @[
//     EORecordBarItemRotateCameraKey, // Flip the camera
//     EORecordBarItemFlashKey, // The flashlight
//     EORecordBarItemTimerKey, // Timer
//     EORecordBarItemFiltersKey, // Filter
//     EORecordBarItemBeautyKey, // Beauty effect
//     EORecordBarItemSpeedKey, // Speed changer
// ]
@property (nonatomic, strong) NSMutableArray *itemKeys;

//   Count the number of unfolding elements from the top.
@property (nonatomic, assign) NSUInteger unfoldCount;

/// Controls whether the sidebar can be hidden.
/// default is `YES`
@property (nonatomic, assign) BOOL foldEnabled;

@end
```


<span id="fdc9053d"></span>
## Sample code

```Java
let config = EORecorderConfig { initializer in    
    initializer.configRecorderViewController { recorderVCInitializer in
        //  Adjust the sequence of funtional buttons in the sidebar.
        recorderVCInitializer.sideBarConfig.itemKeys.exchangeObject(at: 0, withObjectAt: 1)
    }
}
```


<span id="ef87a4c3"></span>
# Callback function

These are the details for the callback function:


|Class |Field and method |Type |Description |Remarks |
|---|---|---|---|---|
|EORecorderViewControllerDelegate |* (void)recorderViewController:(EORecorderViewController \*)recorderViewController didFinishRecordingMediaWithInfo:(EORecordInfo \*)info | |Callback for shooting completion, where the callback data is consolidated in an instance of `EORecordInfo`. |Here, you can access the recorded video (non\-edited). |
||* (void)recorderViewControllerDidCancel:(EORecorderViewController \*)recorderViewController | |The callback for closing camera page. If you implement this method, the SDK will not automatically dismiss the page. It needs the caller to handle it. | |
||\-(void)recorderViewControllerDidTapAlbum:(EORecorderViewController \*)recorderViewController | |Callback for the album button in the camera screen. | |
|EORecordInfo |mediaAssets |NSArray\> \* |Media data | |
||backgroundMusic |id |The selected background music in the camera screen. | |
||source |EORecordInfoSource |Data source: Camera / Photo library | |
||coverImage |UIImage \* |The first frame image of the first data in `mediaAssets`. | |


<span id="901d3578"></span>
## Class definition

```objectivec
@protocol EORecorderViewControllerDelegate <NSObject>

@optional
- (void)recorderViewController:(EORecorderViewController *)recorderViewController didFinishRecordingMediaWithInfo:(EORecordInfo *)info;
- (void)recorderViewControllerDidCancel:(EORecorderViewController *)recorderViewController;
- (void)recorderViewControllerDidTapAlbum:(EORecorderViewController *)recorderViewController;

@end
```


<span id="6e2f32b2"></span>
## Sample code

```Swift
extension EffectOneModule: EORecorderViewControllerDelegate {
    func recorderViewControllerDidTapAlbum(_ recorderViewController: EORecorderViewController) {
        self.recorderVC = recorderViewController

        guard let resourcePicker = EOInjectContainer.shared().resourcePickerSharedImpl else {
            return
        }
        
        resourcePicker.pickResourcesFromRecorder { [weak self] resources, error, cancel in
            guard !resources.isEmpty else {
                return;
            }
            
            let info = EORecordInfo()
            info.mediaAssets = resources
            info.source = .album
            
            if let presenter = self?.topMostViewController() {
                self?.showEditorViewController(info: info, presenter: presenter)
            }
        }
    }
    
    func recorderViewController(_ recorderViewController: EORecorderViewController, didFinishRecordingMediaWith info: EORecordInfo) {
        self.recorderVC = recorderViewController
        
        self.showEditorViewController(info: info, presenter: recorderViewController)
    }
}
```


<span id="226189e4"></span>
# Navigation push function

Navigation push refers to the action of pushing a new view controller onto a navigation stack in iOS development. In iOS apps that use navigation controllers, a navigation push transitions the user to a new screen by pushing the destination view controller onto the navigation stack. This typically creates a navigation bar at the top of the screen, allowing the user to navigate back to the previous screen using a back button.

```Swift
EORecorderViewController.requestMediaAuth { [weak self] granted in
    guard granted else {
        self?.showToast("Request media auth failed")
        return
    }
    guard let strongSelf = self else {
        return
    }
    
    do {
        let recorderViewController = try EORecorderViewController(config: config)
        recorderViewController.delegate = strongSelf
        strongSelf.parentVC.navigationController?.pushViewController(recorderViewController, animated: true)
    } catch {
        self?.showToast("show recorder failed: \(error)")
    }
}
```
