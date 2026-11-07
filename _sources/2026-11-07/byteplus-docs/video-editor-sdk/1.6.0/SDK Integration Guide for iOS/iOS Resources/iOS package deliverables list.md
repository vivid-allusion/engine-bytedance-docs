---
title: "iOS package deliverables list"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/160-ios-package-deliverables-list"
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

The EffectOneKit.xcframework is designed for self\-deployment or local import. For more information, refer to [iOS resources import and configuration](https://docs.byteplus.com/docs/video-editor-sdk/35805).

It includes the following features:


* For self\-deployment or local import.

* Supports the real machine (arm64), emulator (x86) architecture, and emulator (arm64) architecture.

* Contains the symbol table dSYMs of the ARM64 machine, which is used to parse the crash stack.

* Contains `Privacyinfo.xcprivacy` to meet Apple compliance requirements.


<span id="a0f1e7d0"></span>
## EOLocalResources.bundle

The EOLocalResource.bundle encompasses essential resources for BytePlus Video Editor SDK, supporting both display and editing aspects crucial for UI components. It consists of:


1. **BuiltInResource Directory:**  Housing display resources, this directory includes icons and text essential for UI components to ensure a visually cohesive experience.

2. **EffectResource Directory:**  Dedicated to editing resources, this directory stores elements vital for UI components involved in the editing process. For more information, refer to [iOS resources import and configuration](https://docs.byteplus.com/docs/video-editor-sdk/35805).

3. **License Directory:**  This directory hosts the offline license file, a key component for ensuring proper licensing and functionality.


This bundle consolidates all necessary dependencies, enhancing the SDK's capability to deliver a seamless video editing experience. Developers can refer to the documentation for insights into resource import and configuration.

<span id="cdb67431"></span>
## EffectOneKit.podspec

For managing dependencies using local Cocoapods access methods. For more information, refer to [Managing dependencies using Cocoapods](https://docs.byteplus.com/docs/video-editor-sdk/160-managing-dependencies-using-cocoapods).

<span id="ab8c1ada"></span>
## EffectOneKit_spm

For managing dependencies using local SPM access methods, refer to [Managing dependencies using SPM](https://docs.byteplus.com/docs/video-editor-sdk/160-managing-dependencies-using-spm).

<span id="0edf3040"></span>
## EffectOne—iOS

The EffectOne—iOS sample code, written in Swift, consists of the following key components:


* **EffectOneModule.swift:** 

   * This file demonstrates the utilization of each functional API provided by the BytePlus Video Editor SDK for applying EffectOne effects.

   * It showcases how to initialize the SDK and make calls to the EffectOne API to apply effects to a given video URL.

* **EOCustomRequestBuilderImpl.swift:** 

   * This file demonstrates the definition of the resource acquisition interface from the server.

* **EOExportUI:** 

   * This file contains the implementation code for the video export feature.

   * It initializes the BytePlus Video Editor SDK, configures export options using BytePlusVideoExportOptions, and calls the video export API.

   * The export process includes handling the input and output URLs, providing feedback on success or failure.

* **CutSame:** 

   * This file demonstrates the UI implementation code of Magic Template and highlight clippings.


These Swift code snippets serve as a practical reference for integrating EffectOne features and implementing video export functionality using the BytePlus Video Editor SDK within an iOS application. Developers can customize and extend this code to meet specific project requirements.

**Sample code of EOCustomRequestBuilderImpl.swift:** 

```Swift
import UIKit
import EffectOneKit


class EOCustomRequestBuilderImpl: NSObject, EOResourceRequestBuilderProtocol {
    //  Get config
    func buildConfigURLRequest(byPanelKey panelKey: String?, resourceInfo resource: [AnyHashable : Any]?) -> URLRequest? {
        let url = "https://cvsdk.tos-cn-beijing.volces.com/resource/eo/1.3.0/EffectResource/Panel_configs/\(panelKey ?? "").json"
        var request = URLRequest(url: URL(string: url)!)
        request.httpMethod = "GET"
        return request
    }
    
    //  Get icon
    func iconUrlString(_ iconName: String?, panelKey: String?) -> String? {
        return panelKey == EOPanelKeyCutSame ? "https://cvsdk.tos-cn-beijing.volces.com/resource/eo/1.3.0/EffectResource/Resource_icons/\(iconName ?? "")" : ""
    }
    
    //  Get video
    func videoUrlString(_ videoName: String?, panelKey: String?) -> String? {
        return "https://cvsdk.tos-cn-beijing.volces.com/resource/eo/1.3.0/EffectResource/Resource_videos/\(videoName ?? "")"
    }
    
    //  Get template
    func buildResourceDownloadRequest(byRelativePath relativePath: String?, isModel: Bool, panelKey: String?, resourceInfo resource: [AnyHashable : Any]?) -> URLRequest? {
        let url = "https://cvsdk.tos-cn-beijing.volces.com/resource/eo/1.3.0/RemoteResource\(relativePath ?? "")"
        return URLRequest(url: URL(string: url)!)
    }
}
```


**Sample code of EffectOneModule.swift**:

```Swift
import Foundation
import UIKit
import Toast
// Need to introduce EffectOneKit
import EffectOneKit
// Export component needs to be introduced
import EOExportUI
// You need to introduce and cut the same components.
import CutSameUIIF

class EffectOneModule : NSObject
{
    let authFileName : String = "com.volcengine.effectone.inhouse.licbag"
    // Store authentication state
    var isAuthSucceeded: Bool = false
    // Store the used VC for the pop-up interface
    var parentVC: UIViewController
    
    //The application that temporarily stores the shooting component is used to hide the album selection page when exiting the editing component
    private weak var recorderVC: UIViewController?
    
    init(parentVC: UIViewController) {
        self.parentVC = parentVC
    }
    // Enable authentication
    public func makeAuth(){
        let config = EOAuthorizationConfig { [self] initializer in
            // The authentication method is offline authentication.
            initializer.isOnline = false
            // Set the path where the offline certificate is located
            initializer.licensePathForOffline = self.localBundle().path(forResource: self.authFileName, ofType: nil, inDirectory: "License")!
        }
        // Start authentication
        EOAuthorization.sharedInstance().makeAuth(with: config) {isSuccess, errMsg in
            self.isAuthSucceeded = isSuccess
            if !self.isAuthSucceeded {
                // Authentication failed to print error code
                print(errMsg)
            }
            else
            {
                //  Authentication successful, initialize EOSDK and resource allocation
                EOSDK.initSDK { [weak self] in
                   //  Set the resource root path
                   EOSDK.setResourceBaseDir(EOSDK.getEODocumentRootDir() + "/download")
                   //  Set the configuration file root path
                   EOSDK.setResourceDefaultBuiltInConfig(EOSDK.defaultPanelConfigDir(self!.localBundle().bundlePath))
                   // Set built-in resource path
                   EOSDK.setBuiltInResourceDir(EOSDK.defaultResourceDir(self!.localBundle().bundlePath))
                   //  Register to cut the same item to get the resource agreement
                   EOInjectContainer.shared().resourceRequestBuilderImpl = EOCustomRequestBuilderImpl()
                   //  Set fetch from server level
                   EOSDK.useRemoteConfig(true, useRemoteResource: true)
                }
            }
        }
    }
    // Access to the source of the basic editing component
    enum EditorParams {
        case normal(EORecordInfo)
        case draft(EOSDKDraftModel)
    }
    
    //  Get resource root directory
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
    
    func showAlert(withTitle title: String,
                   message: String,
                   cancelTitle: String?,
                   confirmTitle: String?,
                   cancelHandler: (() -> Void)?,
                   confirmHandler: (() -> Void)?) {
        let alert = UIAlertController(title: title, message: message, preferredStyle: .alert)

        if let cancelTitle = cancelTitle {
            let cancelAction = UIAlertAction(title: cancelTitle, style: .cancel) { _ in
                cancelHandler?()
            }
            alert.addAction(cancelAction)
        }

        if let confirmTitle = confirmTitle {
            let confirmAction = UIAlertAction(title: confirmTitle, style: .default) { _ in
                confirmHandler?()
            }
            alert.addAction(confirmAction)
        }

        self.parentVC.present(alert, animated: true, completion: nil)
    }
}

extension EffectOneModule {
    public func showRecorderViewController() {
        if !self.isAuthSucceeded {
            self.showToast("authority is failed!,please check it.")
            return
        }
                
        let config = EORecorderConfig { initializer in
            // Configure the recorder if needed
            
            initializer.configRecorderViewController { recorderVCInitializer in
                // Configure recoderViewController if needed
            }
        }
        
        EORecorderViewController.startRecorder(with: config, presenter: self.parentVC, delegate: self) { [weak self] error in
            if let err = error as? NSError, let presenter = self?.parentVC {
                self?.showErrorAlert(err, presenter: presenter)
            }
        }
    }
    
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
    
    public func gotoDuetViewController(withVideoURL videoURL:URL) {
        if !self.isAuthSucceeded {
            self.showToast("authority is failed!,please check it.")
            return
        }
        
                
        let config = EORecorderConfig { initializer in
            // Configure recorder if needed
            initializer.configRecorderViewController { recorderVCInitializer in
                // Configure recoderViewController if needed
                recorderVCInitializer.musicBarHidden = true
                let sideConfig = EORecorderSideBarConfig()
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
    
    // Enter CutSame page
    func showCutSameController() {
        CutSameRouter.toCutSameCategoryVC()
    }    
}

extension EffectOneModule: EORecorderViewControllerDelegate {
    func recorderViewControllerDidTapAlbum(_ recorderViewController: EORecorderViewController) {
        // Show album page
        self.recorderVC = recorderViewController

         // Use the album component in EOSDK to realize the picture selection function
        guard let resourcePicker = EOInjectContainer.shared().resourcePickerSharedImpl else {
            return
        }
        
        recorderViewController.pausePreview()
        
        resourcePicker.pickResourcesFromRecorder { [weak self] resources, error, cancel in
            guard !resources.isEmpty else {
                return;
            }
            
            let info = EORecordInfo()
            info.mediaAssets = resources
            info.source = .album
            // Show the edit page after completing the selection
            if let presenter = self?.topMostViewController() {
                self?.showEditorViewController(.normal(info), presenter: presenter)
            }
        }
    }
  
    // After finishing shooting, jump to the editing page
    func recorderViewController(_ recorderViewController: EORecorderViewController, didFinishRecordingMediaWith info: EORecordInfo) {
         // The application that temporarily stores the shooting component is used to hide the album selection page when exiting the editing component
        self.recorderVC = recorderViewController
        
        recorderViewController.pausePreview()
         // Enter basic editing
        self.showEditorViewController(.normal(info), presenter: recorderViewController)
    }
}

extension EffectOneModule {
    // The shooting is completed or enter the basic editing from the album. 
    func showEditorViewController(_ params: EditorParams, presenter: UIViewController) {
        if !self.isAuthSucceeded {
            self.showToast("authority is failed!,please check it.")
            return
        }
                
        let config = EOEditorConfig { initializer in
            // Configure editor if needed
            
            initializer.configVideoEditorViewController { editorVCInitializer in
                // Configure videoEditorViewController if needed
                
            }
        }
 
        let sceneConfig = EOEditorSceneConfig()
        switch params {
        case .normal(let info):
            sceneConfig.resources = info.mediaAssets
            sceneConfig.backgroundMusic = info.backgroundMusic
            sceneConfig.coverImage = info.coverImage
            sceneConfig.previewContentMode = info.source == .camera ? .aspectFill : .aspectFit
            sceneConfig.fromType = info.source == .camera ? "camera" : "album"
            if info.isDuet == true  {
                sceneConfig.editorPreviewForType = .duetEditor
                sceneConfig.duetMusic = info.duetUrl
            }
        case .draft(let model):
            sceneConfig.draftModel = model
        }
        
        EOVideoEditorViewController.startEditor(with: config, sceneConfig: sceneConfig, presenter: presenter, delegate: self) { [weak self, weak presenter] error in
            if let err = error as? NSError, let vc = presenter {
                self?.showErrorAlert(err, presenter: vc)
            }
        };
    }
    
    public func showDraftViewController() {
        if !self.isAuthSucceeded {
            self.showToast("authority is failed!,please check it.")
            return
        }
        
        EODraftBoxController.presentDraftVCDelegate(self)
    }
}

extension EffectOneModule: EOVideoEditorViewControllerDelegate {
    func videoEditorViewControllerDidCancel(_ videoEditorViewController: EOVideoEditorViewController) {
        if let recorder = recorderVC {
            // Hide album selection page
            recorder.dismiss(animated: true, completion: nil)
        } else {
            //  Hide the edit page when entering the edit page from the draft and then exiting the edit
            videoEditorViewController.dismiss(animated: true, completion: nil)
        }
    }
    
    // Click the Next button to launch the export page
    func videoEditorViewControllerTapNext(_ exportModel: EOExportModel, presentVC viewController: UIViewController) {
        EOExportViewController.startExport(with: exportModel, presentVC: viewController)
    }
}

extension EffectOneModule: EODraftBoxControllerDelegate {
    //Enter the basic editing component from the draft screen
    func draftBoxController(_ draftBoxController: EODraftBoxController, didSelectDraft draftModel: EOSDKDraftModel) {
        self.showEditorViewController(.draft(draftModel), presenter: draftBoxController)
    }
}
    //Call highlight clippings
    public func showHighLightViewController() {
        if !self.isAuthSucceeded {
            self.showToast("authority is failed!,please check it.")
            return
        }
        _showHighLightViewController()
    }
}
// MARK: highLightFirm
extension EffectOneModule {
    public func _showHighLightViewController() {
        if !self.isAuthSucceeded {
            self.showToast("authority is failed!,please check it.")
            return
        }
        EOAlbumHelper.eoCheckAlbumAuthorized {//  Album permissions are turned on
            // Start highlight clippings
            EOHighLightManager.toHighLight()
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
}

extension EffectOneModule: EOVideoEditorViewControllerDelegate {
    func videoEditorViewControllerDidCancel(_ videoEditorViewController: EOVideoEditorViewController) {
        if let recorder = recorderVC {
            // Hide album selection page
            recorder.dismiss(animated: true, completion: nil)
        } else {
            // Hide the edit page when entering the edit page from the draft and then exiting the edit
            videoEditorViewController.dismiss(animated: true, completion: nil)
        }
    }
    
    //  Click the Next button to launch the export page
    func videoEditorViewControllerTapNext(_ exportModel: EOExportModel, presentVC viewController: UIViewController) {
        EOExportViewController.startExport(with: exportModel, presentVC: viewController)
    }
}

extension EffectOneModule: EODraftBoxControllerDelegate {
    // Moving from draft to basic editing components
    func draftBoxController(_ draftBoxController: EODraftBoxController, didSelectDraft draftModel: EOSDKDraftModel) {
        self.showEditorViewController(.draft(draftModel), presenter: draftBoxController)
    }
}
```


<span id="f897d706"></span>
## Using the sample code

For more information on using the sample code, refer to [Running the sample code](https://docs.byteplus.com/docs/video-editor-sdk/160-getting-started-with-ios#kae0LyfI8X).
