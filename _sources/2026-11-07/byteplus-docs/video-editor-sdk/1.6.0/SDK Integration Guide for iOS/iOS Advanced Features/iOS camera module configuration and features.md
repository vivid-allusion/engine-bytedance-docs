---
title: "iOS camera module configuration and features"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/160-ios-camera-module-configuration-and-features"
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
||(instancetype)initWithBlock:(void (^)(EORecorderConfigInitializer \*))block |N/A |The initialization function. Using the builder pattern, all attributes exposed in `config` are readonly. Initialization is done uniformly through the corresponding initializer. For more information, see the following examples. |


<span id="fb99d92b"></span>
## Class definition

```objectivec
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

```objectivec
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

```objectivec
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
|EORecorderSideBarConfig |itemKeys |NSMutableArray |An array of sidebar element keys. By default, the following six elements are provided and the order can be changed. No custom elements are supported.<br><br>Default value:<br><br>```objectivec```<br>```@[ EORecordBarItemRotateCameraKey, // Flip the camera.```<br>```EORecordBarItemFlashKey, // Flash.```<br>```EORecordBarItemTimerKey, // Countdown timer.```<br>```EORecordBarItemFiltersKey, // Filters.```<br>```EORecordBarItemBeautyKey, // Beauty effects.```<br>```EORecordBarItemSpeedKey, // Speed.```<br>```]```<br> |
||unfoldCount |NSUInteger |Counts the number of non\-collapsible elements starting from the top. |
||foldEnabled |Boolean |Whether the sidebar can be hidden. The default value is `Yes`. |


<span id="ac0ad8e7"></span>
## Class definition

```objectivec
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

```objectivec
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


|**Class** |**Field and method** |**Type** |**Description** |**Remarks** |
|---|---|---|---|---|
|EORecorderViewControllerDelegate |* (void)recorderViewController:(EORecorderViewController \*)recorderViewController didFinishRecordingMediaWithInfo:(EORecordInfo \*)info |N/A |Callback for shooting completion, where the callback data is consolidated in an instance of `EORecordInfo`. |Here, you can access the recorded video (non\-edited). |
||* (void)recorderViewControllerDidCancel:(EORecorderViewController \*)recorderViewController |N/A |The callback for closing camera page. If you implement this method, the SDK will not automatically dismiss the page. It needs the caller to handle it. |N/A |
||\-(void)recorderViewControllerDidTapAlbum:(EORecorderViewController \*)recorderViewController |N/A |Callback for the album button in the camera screen. |N/A |
|EORecordInfo |mediaAssets |NSArray\> \* |Media data |N/A |
||backgroundMusic |id |The selected background music in the camera screen. |N/A |
||source |EORecordInfoSource |Data source: Camera / Photo library |N/A |
||coverImage |UIImage \* |The first frame image of the first data in `mediaAssets`. |N/A |


<span id="901d3578"></span>
## Class definition

```Swift
@protocol EORecorderViewControllerDelegate 
 
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


<span id="7aaa6f56"></span>
# Video duet function

The video duet feature allows users to select a local video and then activate the camera function. It controls the layout of video duets and camera frames in a preview view using a resource package. The selected local video starts playing when shooting begins and stops when shooting ends. Duet images and camera images are recorded together in the resulting video.

**Prerequisities**

You must complete the following before you can configure the video duet function:


* Requires the following resources:

   * Local videos, which can be downloaded from a server or selected from the album.

   * The resource package named `duet.bundle` must be downloaded to the local device beforehand. It is typically included in purchased delivery resources.

* Camera and microphone permissions are necessary.


<span id="fd4ea100"></span>
## Step 1: Selecting a video from the album

`EOResourcePickerImpl` conforms to `EOResourcePickerProtocol` and can be accessed through a utility class.

```objectivec
//1  
EOInjectContainer.shared().resourcePickerSharedImpl
//2
- (void)pickVideoForDuetWithCompletion:(nonnull EOResourcePickerCompletion)completion;
```


<span id="8fd67aa5"></span>
## Step 2: Creating a video duet controller

You can create a video duet controller by completing the following steps.

<span id="f688f316"></span>
### EODuetViewController

`EODuetViewController` is a custom or framework\-provided view controller designed specifically for managing and displaying duet recording functionality within an application.

**Parameters**


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|config |EORecorderConfig \* |configInstance |Configuration object for the duet recording setup. |
|presenter |UIViewController \* |presenterViewController |The view controller that presents the duet recording interface. |
|duetVideoURL |NSURL \* |[NSURL URLWithString:@"..."] |The URL of the local video selected for duet recording. |
|delegate |id_Nullable |delegateInstance |Optional delegate for receiving callbacks during the recording process. |
|completion |void (^)(NSError \* _Nullable error) |^(NSError \*error) {} |Completion block called after the duet recording setup completes, with an optional error parameter. |


**Sample code**

```objectivec
+ (void)startDuetWithConfig:(EORecorderConfig *)config
                  presenter:(UIViewController *)presenter
               duetVideoURL:(NSURL *)videoURL 
                   delegate:(id _Nullable)delegate
                 completion:(void (^)(NSError * _Nullable error))completion;
```


<span id="fc87cc1e"></span>
### EORecorderConfig

This configuration structure (`EORecorderConfig`) encapsulates settings related to music bar visibility and additional options for controlling microphone usage and selecting duet layouts within the recording interface.

**Parameters**


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|musicBarHidden |Boolean |true |Boolean property set to `true`, indicating whether the music bar is hidden. |
|sideConfig |Dictionary | |Dictionary containing additional configuration keys: `barItemMicKey` and `barItemDuetLayoutKey`. |
|sideConfig \- barItemMicKey |String |mic_switch |Key used to add a microphone switch for toggling microphone functionality during recording. |
|sideConfig \- barItemDuetLayoutKey |String |duet_layout_entry |Key used to add an entry point for selecting duet layouts, allowing users to choose different layouts for duet recordings. |


**Sample code**

```Swift
let config = EORecorderConfig { initializer in 
            // config recorder if needed
            
            initializer.configRecorderViewController { recorderVCInitializer in
                // config recoderViewController if needed
                
                recorderVCInitializer.musicBarHidden = true 
                if let stickerButtonHidden: Bool = DebugConfig.value(forKey: "recorderStickerButtonHidden") {
                    recorderVCInitializer.stickerButtonHidden = stickerButtonHidden
                }
                if let albumButtonHidden: Bool = DebugConfig.value(forKey: "recorderAlbumButtonHidden") {
                    recorderVCInitializer.albumButtonHidden = albumButtonHidden
                }
                var sideConfig = EORecorderSideBarConfig()
                sideConfig.itemKeys = [EORecordSideBarItemKey.barItemRotateCameraKey,
                                       EORecordSideBarItemKey.barItemFlashKey,
                                       EORecordSideBarItemKey.barItemMicKey,
                                       EORecordSideBarItemKey.barItemDuetLayoutKey,
                                       EORecordSideBarItemKey.barItemTimerKey,
                                       EORecordSideBarItemKey.barItemFiltersKey,
                                       EORecordSideBarItemKey.barItemBeautyKey,
                                       EORecordSideBarItemKey.barItemSpeedKey,]
                recorderVCInitializer.sideBarConfig = sideConfig
            }
        }
```


<span id="29c71516"></span>
## Full sample code: Selecting from the album

```objectivec
public func showDuetViewController() {
        if !self.isAuthSucceeded {
            self.showToast("authority is failed!,please check it.")
            return
        } 
        
        EOAlbumHelper.eoCheckAlbumAuthorized { [weak self] in
            guard let resourcePicker = EOInjectContainer.shared().resourcePickerSharedImpl else {
                return
            }
            
            resourcePicker.pickVideoForDuet(completion: { [weak self] resources, error, cancel in
                if let resorce = resources.first {
                    self?.gotoDuetViewController(withVideoURL: resorce.url!)
                }
                
            }) 
            
        } restrictedOrDenied: { [weak self] in
            self?.showAlert(withTitle: NSLocalizedString("eo_home_camera_album_unauth_alert_title", comment: ""),
                                  message: NSLocalizedString("eo_home_camera_album_unauth_alert_message", comment: ""),
                                  cancelTitle: NSLocalizedString("eo_home_camera_unauth_alert_cancel", comment: ""),
                                  confirmTitle: NSLocalizedString("eo_home_camera_unauth_alert_confirm", comment: ""),
                                  cancelHandler: nil,
                                  confirmHandler: {
                if #available(iOS 10.0, *) {
                    UIApplication.shared.open(URL(string: UIApplication.openSettingsURLString)!, options: [:]) { success in
                        // Completion handler
                    }
                } else {
                    UIApplication.shared.openURL(URL(string: UIApplication.openSettingsURLString)!)
                }
            })
        }

        
    }
```


<span id="0e644a17"></span>
## Full sample code: Entering the duet video function

```Swift
public func gotoDuetViewController(withVideoURL videoURL:URL) {
        if !self.isAuthSucceeded {
            self.showToast("authority is failed!,please check it.")
            return
        } 
          
        updateImageEditingEnabledIfNeeded()
                
        let config = EORecorderConfig { initializer in
            // config recorder if needed
            
            initializer.configRecorderViewController { recorderVCInitializer in
                // config recoderViewController if needed
                
                recorderVCInitializer.musicBarHidden = true
                if let stickerButtonHidden: Bool = DebugConfig.value(forKey: "recorderStickerButtonHidden") {
                    recorderVCInitializer.stickerButtonHidden = stickerButtonHidden
                }
                if let albumButtonHidden: Bool = DebugConfig.value(forKey: "recorderAlbumButtonHidden") {
                    recorderVCInitializer.albumButtonHidden = albumButtonHidden
                }
                var sideConfig = EORecorderSideBarConfig()
                sideConfig.itemKeys = [EORecordSideBarItemKey.barItemRotateCameraKey,
                                       EORecordSideBarItemKey.barItemFlashKey,
                                       EORecordSideBarItemKey.barItemMicKey,
                                       EORecordSideBarItemKey.barItemDuetLayoutKey,
                                       EORecordSideBarItemKey.barItemTimerKey,
                                       EORecordSideBarItemKey.barItemFiltersKey,
                                       EORecordSideBarItemKey.barItemBeautyKey,
                                       EORecordSideBarItemKey.barItemSpeedKey,]
                recorderVCInitializer.sideBarConfig = sideConfig
            }
        }
        
        EODuetViewController.startDuet(with: config, presenter: self.parentVC,duetVideoURL:videoURL, delegate: self, completion: { [weak self] error in
            if let err = error as? NSError, let presenter = self?.parentVC {
                self?.showErrorAlert(err, presenter: presenter)
            }
        })
    }
```
