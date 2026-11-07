---
title: "iOS Player SDK: Customizing device ID"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-customizing-device-id-ios"
---

BytePlus VOD comes with an endpoint tracker, which tracks users' individual play behaviors and identifies issues. The BytePlus VOD Player SDK automatically generates a unique ID for each device. You can monitor the playback history of the device ID on the **Quality insights** page within the BytePlus VOD console. However, if you have a user system of your own and hope to track individual users' play behaviors using the user ID, you can follow the steps in this article to custom the device ID.

<span id="17e78fb2"></span>
## Customizing the device ID

You can customize the device ID during SDK initialization. See the following sample code:

```objectivec
// Initialize the SDK
- (void)initTTSDK {
    // Set the app ID
    NSString *appId = @"xxx";
    [TTSDKManager startWithConfiguration:configuration];
    
    // Set the user ID
    [TTSDKManager setCurrentUserUniqueID:<#userid#>]；
}
```


<span id="174ab671"></span>
## Removing the device ID

You can remove the custom device ID when the end user logs out. Refer to the code sample below:

```objectivec
// Called when the end user logs out
- (void)onUserLogout {
    [TTSDKManager clearUserUniqueID];
}
```


<span id="1d685357"></span>
## Updating the device ID

You can update the device ID when the end user successfully logs in or switches to another account. Refer to the code sample below.

```objectivec
// Called when the end user logs in or switches to another account
- (void)onUserLogin {
    [TTSDKManager setCurrentUserUniqueID:<#userid#>];
}
```


<span id="840fab67"></span>
## Viewing individual devices' play data

After setting a custom ID, you can monitor the playback history of the device ID on the **Quality insights** page within the BytePlus VOD console. For details, see [Endpoint tracker](https://docs.byteplus.com/docs/byteplus-vod/docs-end-point-tracker).
