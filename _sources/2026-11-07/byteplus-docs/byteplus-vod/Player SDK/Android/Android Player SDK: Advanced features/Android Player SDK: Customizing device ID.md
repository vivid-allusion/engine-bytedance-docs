---
title: "Android Player SDK: Customizing device ID"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-customizing-device-id-android"
---

BytePlus VOD comes with an endpoint tracker, which tracks users' individual play behaviors and identifies issues. The BytePlus VOD Player SDK automatically generates a unique ID for each device. You can monitor the playback history of the device ID on the **Quality insights** page within the BytePlus VOD console. However, if you have a user system of your own and hope to track individual users' play behaviors using the user ID, you can follow the steps in this article to custom the device ID.

<span id="17e78fb2"></span>
## Customizing the device ID

You can customize the device ID during SDK initialization. See the following sample code:

```Java
private void initVodSDK(Context context, String userUniqueId) {
    // 1. Initialize the SDK
    Env.init(new Config.Builder()
        // ...
        .build());
    // 2. Set userUniqueId
    IAppLogInstance applog = AppLogWrapper.getAppLogInstance();
    if (applog != null && !TextUtils.isEmpty(userUniqueId)) {
        applog.setUserUniqueID(userUniqueId); 
    }
}
```


<span id="174ab671"></span>
## Removing the custom device ID

You can remove the custom device ID when the end user logs out. Refer to the code sample below:

```Java
// Called when the end user logs out
private void onUserLogout() {
    IAppLogInstance applog = AppLogWrapper.getAppLogInstance();
    if (applog != null) {
        applog.setUserUniqueID(null);
    }
}
```


<span id="1d685357"></span>
## Updating device ID

You can update the device ID when the end user successfully logs in or switches to another account. Refer to the code sample below.

```java
// Called when the end user logs in or switches to another account
private void onUserLogin(String userUniqueId) {
    IAppLogInstance applog = AppLogWrapper.getAppLogInstance();
    if (applog != null) {
        applog.setUserUniqueID(userUniqueId);
    }
}
```


<span id="840fab67"></span>
## Viewing individual devices' play data

After setting a custom ID, you can monitor the playback history of the device ID on the **Quality insights** page within the BytePlus VOD console. For details, see [Endpoint tracker](https://docs.byteplus.com/docs/byteplus-vod/docs-end-point-tracker).
