---
title: "iOS package deliverables list"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/docs-ios-package-deliverables-list"
---

BytePlus Video Editor SDK consists of the following packages:


* EffectOneKit.xcframework

* EOLocalResources.bundle

* EffectOneKit.podspec

* EffectOneKit_spm

* Video Editor SDK for iOS


To retrieve the SDK packages, reach out to the BytePlus Video Editor SDK team.

<span id="486ce067"></span>
## EffectOneKit.xcframework

The EffectOneKit.xcframework is designed for self\-deployment or local import. For more information, refer to [iOS resources import and configuration](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-ios-resource-import-and-configuration).

It includes the following features:


* Supports the real machine (ARM64) and emulator (x86) architecture.

* Contains the symbol table dSYMs of the ARM64 machine, which is used to parse the crash stack.

* Contains `Privacyinfo.xcprivacy` to meet Apple compliance requirements.


<span id="a0f1e7d0"></span>
## EOLocalResources.bundle

The EOLocalResource.bundle encompasses essential resources for BytePlus Video Editor SDK, supporting both display and editing aspects crucial for UI components. It consists of:


1. **BuiltInResource Directory:**  Housing display resources, this directory includes icons and text essential for UI components to ensure a visually cohesive experience.

2. **EffectResource Directory:**  Dedicated to editing resources, this directory stores elements vital for UI components involved in the editing process. Detailed information on resource import and configuration is available for reference.

3. **License Directory:**  This directory hosts the offline license file, a key component for ensuring proper licensing and functionality.


This bundle consolidates all necessary dependencies, enhancing the SDK's capability to deliver a seamless video editing experience. Developers can refer to the documentation for insights into resource import and configuration.

<span id="cdb67431"></span>
## EffectOneKit.podspec

For managing dependencies using local Cocoapods access methods. For more information, refer to [Managing dependencies using Cocoapods](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-managing-dependencies-using-cocoapoads).

<span id="ab8c1ada"></span>
## EffectOneKit_spm

For managing dependencies using local SPM access methods, refer to [Managing dependencies using SPM](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-managing-dependencies-using-spm).

<span id="0edf3040"></span>
## EffectOne—iOS

The EffectOne—iOS sample code, written in Swift, consists of two key components:


* **EffectOneModule.swift:** 

   * This file demonstrates the utilization of each functional API provided by the BytePlus Video Editor SDK for applying EffectOne effects.

   * It showcases how to initialize the SDK and make calls to the EffectOne API to apply effects to a given video URL.

* **EOExportUI:** 

   * This file contains the implementation code for the video export feature.

   * It initializes the BytePlus Video Editor SDK, configures export options using BytePlusVideoExportOptions, and calls the video export API.

   * The export process includes handling the input and output URLs, providing feedback on success or failure.


These Swift code snippets serve as a practical reference for integrating EffectOne features and implementing video export functionality using the BytePlus Video Editor SDK within an iOS application. Developers can customize and extend this code to meet specific project requirements.

**Sample code of EffectOneModule.swift**:

```Java
import Foundation
import UIKit
import Toast
//Importing EffectOneKit is required.
import EffectOneKit
//Importing the export component is required.
import EOExportUI

class EffectOneModule : NSObject
{
    let authFileName : String = "com.volcengine.effectone.inhouse.licbag"
    //Save the authentication status.
    var isAuthSucceeded: Bool = false
    //Save the used VC for the pop-up pane. 
    var parentVC: UIViewController
    
    //Temporarily save the VC related to the camera component. When users exit the editing module, it can be used to dismiss the photo selection page.
    private weak var recorderVC: UIViewController?
    
    init(parentVC: UIViewController) {
        self.parentVC = parentVC
    }
    //Launch the authentication.
    public func makeAuth(){
        let config = EOAuthorizationConfig { [self] initializer in
            //Set the authentication method to offline authentication.
            initializer.isOnline = false
            //Set the path where the offline license is saved.
            initializer.licensePathForOffline = self.localBundle().path(forResource: self.authFileName, ofType: nil, inDirectory: "License")!
        }
        //Start the authentication.
        EOAuthorization.sharedInstance().makeAuth(with: config) {isSuccess, errMsg in
            self.isAuthSucceeded = isSuccess
            if !self.isAuthSucceeded {
                //When authentication is not successful, print the error message.
                print(errMsg)
            }
            else
            {
                //When authentication is successful，initialize EOSDK and add resource settings.
                EOSDK.initSDK { [weak self] in
                    // Configure the root path of resources.
                    EOSDK.setResourceBaseDir(EOSDK.defaultResourceDir(self!.localBundle().bundlePath))
                    // Configure the root path of configuration files.
                    EOSDK.setResourceDefaultBuiltInConfig(EOSDK.defaultPanelConfigDir(self!.localBundle().bundlePath))
                }
            }
        }
    }
    //Start the basic editing component.
    public func showRecorderViewController() {
        if !self.isAuthSucceeded {
            self.showToast("authority is failed!,please check it.")
            return
        }
        //Construct default configruations for the camera module.
        let config = EORecorderConfig { initializer in}
        
        //Show the camera page.
        EORecorderViewController.startRecorder(with: config, presenter: self.parentVC, delegate: self) { [weak self] error in
            if let err = error as? NSError, let presenter = self?.parentVC {
                self?.showErrorAlert(err, presenter: presenter)
            }
        }
    }
    //After videoshooting or selecting albums, you can enter the  basic editing module. 
    public func showEditorViewController(info: EORecordInfo, presenter: UIViewController) {
        if !self.isAuthSucceeded {
            self.showToast("authority is failed!,please check it.")
            return
        }
        //Construct default configruations for the editor module.
        let config = EOEditorConfig { initializer in}
        //Configure input parameters for the editor module.
        let sceneConfig = EOEditorSceneConfig()
        sceneConfig.resources = info.mediaAssets
        sceneConfig.backgroundMusic = info.backgroundMusic
        sceneConfig.coverImage = info.coverImage
        sceneConfig.previewContentMode = info.source == .camera ? .aspectFill : .aspectFit
        //Show the editor page.
        EOVideoEditorViewController.startEditor(with: config, sceneConfig: sceneConfig, presenter: presenter, delegate: self) { [weak self, weak presenter] error in
            if let err = error as? NSError, let vc = presenter {
                self?.showErrorAlert(err, presenter: vc)
            }
        };
    }
    //Launch the function in the draft module.
    public func showDraftViewController() {
        if !self.isAuthSucceeded {
            self.showToast("authority is failed!,please check it.")
            return
        }
        //Show the draft module.
        EODraftBoxController.presentDraftVCDelegate(self)
    }
    
    //Obtain the root directory of resources.
    private func localBundle() -> Bundle {
        Bundle(path: Bundle.main.path(forResource: "EOLocalResources", ofType: "bundle") ?? "") ?? Bundle.main
    }
    
    private func showErrorAlert(_ err: NSError, presenter: UIViewController) {
        let msg = "\(NSLocalizedString("eo_home_error_alert_title", comment: ""))\(err.domain):\(err.code)"
        let alert = UIAlertController(title: nil, message: msg, preferredStyle: .alert)
        alert.addAction(UIAlertAction(title: NSLocalizedString("eo_home_error_alert_ok", comment: ""), style: .cancel))
        presenter.present(alert, animated: true)
    }
    
    public func showToast(_ text: String) {
        guard let window = UIApplication.shared.keyWindow else {
            return
        }
        window.makeToast(text, duration: 1.5, position:CSToastPositionCenter)
    }
    
    private func topMostViewController() -> UIViewController? {
        var topViewController: UIViewController?
        let window = UIApplication.shared.keyWindow
        let rootViewController = window?.rootViewController
        if let tabBar = rootViewController as? UITabBarController {
            topViewController = tabBar.selectedViewController
        } else {
            topViewController = rootViewController;
        }
        if let nav = topViewController as? UINavigationController {
            topViewController = nav.topViewController
        }
        while topViewController?.presentedViewController != nil {
            topViewController = topViewController?.presentedViewController
            if let nav = topViewController as? UINavigationController {
                topViewController = nav.topViewController
            }
        }
        return topViewController
    }
}

extension EffectOneModule: EORecorderViewControllerDelegate {
    //Show the album page.
    func recorderViewControllerDidTapAlbum(_ recorderViewController: EORecorderViewController) {
        //Temporarily save the VC related to the camera component. When users exit the editing module, it can be used to dismiss the photo selection page.
        self.recorderVC = recorderViewController

        //Use the album module within the EOSDK to realize the photo selection function.
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
            //After photo selection is complete, show the editing page.
            if let presenter = self?.topMostViewController() {
                self?.showEditorViewController(info: info, presenter: presenter)
            }
        }
    }
    //After videoshooting is complete, jump to the editing page.
    func recorderViewController(_ recorderViewController: EORecorderViewController, didFinishRecordingMediaWith info: EORecordInfo) {
        //Temporarily save the VC related to the camera component. When users exit the editing module, it can be used to dismiss the photo selection page.
        self.recorderVC = recorderViewController
        //Show the basic editing module.
        self.showEditorViewController(info: info, presenter: recorderViewController)
    }
}

extension EffectOneModule: EOVideoEditorViewControllerDelegate {
    func videoEditorViewControllerDidCancel(_ videoEditorViewController: EOVideoEditorViewController) {
        if let recorder = recorderVC {
            //Dismiss the photo selection page.
            recorder.dismiss(animated: true, completion: nil)
        } else {
            //After you complete using the draft module, launch the editing page and exit the same page, the particular page wil be dismissed.
            videoEditorViewController.dismiss(animated: true, completion: nil)
        }
    }
    
    //Click on the Next Step button to launch the export page.
    func videoEditorViewControllerTapNext(_ exportModel: EOExportModel, presentVC viewController: UIViewController) {
        EOExportViewController.startExport(with: exportModel, presentVC: viewController)
    }
}
```


<span id="f897d706"></span>
## Using the sample code

For more information on using the sample code, refer to [Getting started with iOS](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-getting-started-with-ve-ios).
