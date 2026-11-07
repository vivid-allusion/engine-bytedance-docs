---
title: "Initializing and preparing the iOS Magic Template SDK"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/140-initializing-and-preparing-the-ios-magic-template-sdk"
---

This topic describes steps to initialize and prepare the iOS Magic Template SDK project.

<span id="96672fb0"></span>
# Step 1: Initializing the a**uthorization** configuration

Set up the authorization configuration related to SDK .

**To initialize the authorization configuration:** 


1. Place the authorization file under the host project directory.

   ```objectivec
   EOAuthorizationConfig *config = [[EOAuthorizationConfig alloc] initWithBlock:^(EOAuthorizationConfigInitializer * _Nonnull initializer) {
       initializer.isOnline = NO;
       // Configure the path to the authorization file
       initializer.licensePathForOffline = [[NSBundle mainBundle] pathForResource:@"com.volcengine.effectone.licbag" ofType:nil];
   }]; 
   ```
   

2. Initialize the authorization.

   ```objectivec
   [[EOAuthorization sharedInstance] makeAuthWithConfig:config completionHandler:^(BOOL success, NSString * _Nonnull errMsg) {
       [CSIFCutSameSDK setupWithCompletion:^(CSIFCutSameStatus status) {
       if (status == CSIFCutSameStatusReady) { 
           // Magic Template authorization successful
       }
   }];
   ```
   


<span id="e80a7dc1"></span>
# Step 2: Initializing SDK

After successful authorization initialization, proceed to initialize the configuration related to the Magic Template SDK.

<span id="c910abbf"></span>
#### Sample code

```objectivec
// Global initialization of EffectOne
[EOSDK initSDK:^{
 
}];
```


<span id="0ec00e95"></span>
# Step 3: Retrieving template list (optional)

If you are using the **Material SDK** to retrieve the template list, you can obtain the templates through the following interface. If you are retrieving the template materials on your own, skip this step.

<span id="c7575198"></span>
#### Sample code

```objectivec
[EOInjectContainer.shared.resourceLoaderSharedImpl loadConfigByPanelKey:EOPanelKeyCutSame localOnly:NO completion:^(NSString * _Nonnull panelKey, NSArray<id> * _Nullable tabs, NSError * _Nullable error) {
 
}];
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information on managing Magic Template materials, refer to <a href="https://docs.byteplus.com/docs/video-editor-sdk/140-ios-resources-import-and-configuration">iOS resources import and configuration</a>.</div>
