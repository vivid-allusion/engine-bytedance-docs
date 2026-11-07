---
title: "Integrating VE SDK using Objective-C"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/docs-integrating-ve-sdk-using-objective-c"
---

This section describes how to quickly integrate BytePlus Video Editor SDK using Objective\-C. This integration method is based on CocoaPods.

<span id="6857307e"></span>
# Prerequisities

Before integrating VE SDK using Swift, you have to complete the following:


* Add the dependencies using Cocoapds . For details, refer to [Managing dependencies using Cocoapods](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-managing-dependencies-using-cocoapoads).

* Retrieve your SDK package from your BytePlus representatives.

   * For more information, refer to the [iOS package deliverables list](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-ios-package-deliverables-list).


<span id="dfa3edda"></span>
# Step 1: Create a new project and copy the code and resources


1. Launch Xcode and create an iOS App project.

   For demonstration purposes, we will use `EffectOne-OC` as the project name.

2. In Xcode, select `Objective-C` as the language.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The package name should match the one used when applying for the Video Editor SDK. Use the resources and authorization files obtained from the official source of the SDK.   </div>
   

3. Obtain files related to the SDK by unzipping the SDK package for Objective\-C.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Reach out to the BytePlus Video Editor SDK team for more information on the SDK package.   </div>
   

4. In the `EffectOne-OC` directory, find and copy the `EOExportUI`folder, the `EOExportUI.podspec` , `EOLocalResources.bundle`, and `Podfile` files into the root directory of your new project, which is `EffectOne-OC` in this example.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/526f8bb5451e4a23a51dbfe01d986945~tplv-goo7wpa0wc-image.image) </span>

5. Open the Podfile file and make modifications as shown in the following figure.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you name your project with a different name, replace <code>EffectOne-OC</code> with the name of your project.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2b57edec0ca4650b3a28c2ce57a5efa~tplv-goo7wpa0wc-image.image) </span>

6. In Terminal, navigate to the directory where the Podfile file of the `EffectOne-OC` project is located.

7. Run the following commands to open the project:

   ```Plain
   pod install --repo-update
   open EffectOne-OC.xcworkspace
   ```
   


<span id="522897f8"></span>
# Step 2: Importing resource packages and core code samples

The SDK can be delivered with special effect props, models, and other files as dependencies. This section specifically focuses on the method of embedding them within the app. For other methods, refer to[ iOS resources import and configuration](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-ios-resource-import-and-configuration).

**To import resource packages and core code samples:** 


1. Import the `EOLocalResources.bundle` file into your project.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You must select the <strong>Create folder references</strong> option during the import and ensure that the bundle is directly under the main bundle at runtime.   </div>
   

2. Add an `EffectOneModule` class, which handles the logic of modules such as authentication, camera, and draft box.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can directly use the <code>EffectOneModule</code> class in the <code>EffectOne-OC</code> demo project.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1877dc789022459cb9daf3342064a7dc~tplv-goo7wpa0wc-image.image) </span>


<span id="57c54c87"></span>
# Step 3: Grant permissions

In the configuration file `Info.plist` of the project, grant permissions to access the camera, microphone, and album:

```JavaScript
//Whether to allow the app to access your media library.
<key>NSAppleMusicUsageDescription</key> 
<string>media</string>//Write your own description.
//Whether to allow the app to use your camera.
<key>NSCameraUsageDescription</key>
<string>Camera</string>// Write your own description.
//Whether to allow the app to use your microphone.
<key>NSMicrophoneUsageDescription</key>
<string>mic</string>//Write your own description.
//Whether to allow the app to save pictures to your mobile phone. 
<key>NSPhotoLibraryAddUsageDescription</key>
<string>photo lib</string>//Write your own description.
//Whether to allow the app to access the photo album. 
<key>NSPhotoLibraryUsageDescription</key>
<string>photo</string>//Write your own description.
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fcbf918782fa4698b368ea212a07f2e4~tplv-goo7wpa0wc-image.image) </span>

<span id="ad78dceb"></span>
# Step 4: Modify files for authentication

This section handles the authentication process, including setting up the configuration for offline mode, specifying the path for the offline license, and handling the result of the authentication process. If authentication succeeds, it further initializes the EOSDK with specific configurations. Modify the `EffectOneModule` file or directly use the `EffectOneModule` file in the demo project for Objective\-C.

**To modify the files for authentication:** 


1. In the file, add the authentication method `makeAuth`.

   ```objectivec
   - (void)makeAuth {
       __weak typeof(self) weakSelf = self;
       EOAuthorizationConfig *config = [[EOAuthorizationConfig alloc] initWithBlock:^(EOAuthorizationConfigInitializer * _Nonnull initializer) {
           initializer.isOnline = NO;
           __strong typeof(self) strongSelf = weakSelf;
           //Set the path where the offline license is located. 
           initializer.licensePathForOffline = [[strongSelf localBundle] pathForResource:strongSelf.authFileName ofType:nil inDirectory:@"License"];
       }];
       
       // Start the authentication.
       [[EOAuthorization sharedInstance] makeAuthWithConfig:config completionHandler:^(BOOL success, NSString * _Nonnull errMsg) {
           __strong typeof(self) strongSelf = weakSelf;
           strongSelf.isAuthSucceeded = success;
           if (!strongSelf.isAuthSucceeded) {
               NSLog(@"%@",errMsg);
           } else {
               [EOSDK initSDK:^{
                   __strong typeof(self) strongSelf = weakSelf;
                   [EOSDK setResourceBaseDir:[EOSDK defaultResourceDir:[strongSelf localBundle].bundlePath]];
                   [EOSDK setResourceDefaultBuiltInConfig:[EOSDK defaultPanelConfigDir:[strongSelf localBundle].bundlePath]];
               }];
           }
       }];
   }
   ```
   

2. Add the method `showRecorderViewController` to call the camera module.

   ```objectivec
   - (void)showRecorderViewController {
       if (!self.isAuthSucceeded) {
           [self showToast:@"authority is failed!,please check it."];
           return;
       }
       //Construct the default configurations of the camera module.
       EORecorderConfig *config = [[EORecorderConfig alloc] initWithBlock:^(EORecorderConfigInitializer * _Nonnull initializer) {
           
       }];
       
       //Display the recorder page. 
       __weak typeof(self) weakSelf = self;
       [EORecorderViewController startRecorderWithConfig:config presenter:self.parentVC delegate:self completion:^(NSError * _Nullable error) {
           __strong typeof(self) strongSelf = weakSelf;
           if (error && strongSelf.parentVC) {
               [strongSelf showErrorAlertWithError:error presenter:strongSelf.parentVC];
           }
       }];
   }
   ```
   

3. Add the method `showDraftViewController` to call the draft box.

   ```objectivec
    - (void)showDraftViewController {
       if (!self.isAuthSucceeded) {
           [self showToast:@"authority is failed!,please check it."];
           return;
       }
       //Display the draft box module.
       [EODraftBoxController presentDraftVCDelegate:self];
   }
   ```
   


<span id="1e4eb6fe"></span>
# Step 5: Add authentication logic


1. Place the authentication logic in the `AppDelegate` or the initial `ViewController` before launching other functionalities.

2. Add the following code to the ViewController file:

   ```objectivec
   
   - (EffectOneModule *)effectOneModule {
       if (!_effectOneModule) {
           _effectOneModule = [[EffectOneModule alloc] initWithParentVC:self];
       }
       return _effectOneModule;
   }
   - (void)viewDidLoad {
       [super viewDidLoad];
       // Do any additional setup after loading the view.
       //Start the authentication.
       [self.effectOneModule makeAuth];
       [self.view addSubview:self.recorderButton];
       [self.view addSubview:self.draftButton];
       CGPoint recoderCenter = CGPointMake(self.view.center.x, self.view.center.y - 50);
       self.recorderButton.frame = CGRectMake(0, 0, 120, 40);
       self.recorderButton.center = recoderCenter;
       
       self.draftButton.frame = CGRectMake(0, 0, 120, 40);
       self.draftButton.center = CGPointMake(recoderCenter.x, recoderCenter.y + 50);
   }
   ```
   

3. Your authentication certificate is typically placed in the `EOLocalResources.bundle\License\` directory with a file name like `XXX.licbag`. Open `EffectOneModule.swift` and replace the string in the following code with `"XXX.licbag"`.

   ```objectivec
   self.authFileName = @"XXX.licbag";
   ```
   


<span id="b313681b"></span>
# Step 6: Launch the editor module


1. Create a Button control.

2. In the click event, run the following code to launch the basic editor module:

   ```objectivec
   - (void)showRecorderViewController {
      [self.effectOneModule showRecorderViewController];
   }
   ```
   


<span id="afa65af7"></span>
# Step 7: Launch the draft box


1. Create a Button control.

2. In the click event, run the following code to launch the draft screen.

   ```objectivec
   - (void)showDraftViewController {
      [self.effectOneModule showDraftViewController];
   }
   ```
   


<span id="0e88ad12"></span>
# <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2ff5fa91cbb545f595ac9bec79533021~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For any integration related questions, refer to our <a href="https://docs.byteplus.com/en/docs/video-editor-sdk/docs-faq">FAQ</a>.</div>
