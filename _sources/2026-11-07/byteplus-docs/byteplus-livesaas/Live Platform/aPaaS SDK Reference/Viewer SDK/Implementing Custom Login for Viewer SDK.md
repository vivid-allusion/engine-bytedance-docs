---
title: "Implementing Custom Login for Viewer SDK"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/implementing-custom-login"
---

Custom Login is an authentication mechanism that allows your viewers to use account information from your own user system (e.g., your e\-commerce platform, app, or internal system) to seamlessly access the BytePlus Live viewing page.

This feature enables deep integration of BytePlus Live services with your business scenarios, achieving **unified identity authentication** and a smooth user experience. It also allows you to correlate account information from your own system within live streaming data analytics for **cross\-platform analysis**.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3f56a1df68f346be8abd6c6d2718d291~tplv-goo7wpa0wc-image.image" width="729px" /></div>


<span id="a07a662d"></span>
## Difference from OAuth 2.0

Both Custom Login and OAuth 2.0 can achieve "third\-party user login," where viewers first log into your account system before watching a live stream. Choose the appropriate method based on your business scenario and technical requirements.


* **Choose OAuth 2.0 if:** 

   * Your system already has a **mature, standard OAuth 2.0 user authorization service**.

   * You prefer to follow industry\-standard protocols for system integration, which simplifies long\-term maintenance.

   * An extra page redirect and authorization step is acceptable for your user experience.

* **Choose Custom Login if:** 

   * You want to implement a Single Sign\-On (SSO) experience, allowing users to enter the live room seamlessly.

   * Your system **does not have a ready\-made OAuth 2.0 service**, but you still need to implement third\-party user login.

   * You require greater **control and flexibility** over the integration process, such as customizing token expiration and refresh logic.


<span id="60bfc569"></span>
## User flow showcase

We provide two common login interaction flows for you to experience.


|**Flow** |**Description** |**Use Case** |**Demo** |
|---|---|---|---|
|**Login\-First** |Viewers must log in before they can enter the live room to watch and interact. |Ideal for scenarios requiring strict identity verification, access control, or user behavior tracking, such as corporate training, paid courses, or exclusive member events. This method offers higher security but may increase the barrier to entry for viewers. |1. Click [here](https://live.byteplus.com/demo/sdk/index.playground.html?mode=pc-custom) to open the demo.<br><br>2. Enter a nickname and click **Log in**.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9641e97317334dcd8890507134d6a016~tplv-goo7wpa0wc-image.image) </span><br><br>You can then watch the live stream and send messages. |
|**Watch\-First** |Viewers can enter the live room as tourists to watch. The login process is triggered only when they attempt to perform interactive actions like commenting or liking. |Suitable for public events and marketing broadcasts aimed at lead generation and conversion. This method lowers the initial barrier to entry, encouraging wider participation. |1. Click [here](https://live.byteplus.com/demo/sdk/index.playground.html?mode=pc-custom) to open the demo.<br><br>2. Click **Tourists Login** to enter directly. You can see the live stream and messages.<br><br>3. Try typing a message in the chat box to trigger the login prompt.<br><br>4. Enter a nickname and click **Login**.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b56406e8ebb842ff86b284a5942d70f9~tplv-goo7wpa0wc-image.image) </span><br><br>You can then send messages. |


<span id="fa2173d1"></span>
## Implementation guide

This section provides the implementation guide for the two flows above. Choose the appropriate method based on your viewing page integration scenario. For all methods, you must call the [GetSDKTokenAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getsdktokenapi) to dynamically get a temporary token for each viewer.

<span id="e47acb29"></span>
### Scenario 1: Native Android App integration

<span id="807fa016"></span>
#### **Flow 1: Login\-First**

**Principle**: Viewers must log in before entering the live room. The authentication mode is "Custom". You need to set the `mode` parameter to `2` when calling the [GetSDKTokenAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getsdktokenapi).

**Process**:


1. **User Logs In**: The user logs into your app and then attempts to enter a live room.

2. **App Requests Token**: Your app requests an authentication token from your business server.

3. **Server Gets Token**: Your server calls the BytePlus Live server\-side API `GetSDKTokenAPI`, passing the user's information and setting `mode=2` to request a custom\-mode token.

4. **Server Returns Token**: After successful validation, the BytePlus Live server returns a one\-time, temporary token.

5. **App Receives Token**: Your server relays the token to your app.

6. **App Enters Live Room**: The app calls the SDK's [joinLiveRoom](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-tvuliveroom?lang=en#joinliveroom) method with the token to enter the live room.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c8fc6b0914f44aff8916abd5098c4bf4~tplv-goo7wpa0wc-image.image) </span>

**Code Sample**:

After obtaining the `mode=2` token, call the `joinLiveRoom` method.

```java
// 1. Configure live room parameters
long activityId = 1721010849258****L; // The activity ID of the live room
String token = "ak3T%2FdaGJDL5zSFD7%2F1GPGP****wx0zaTfQ1M4Dahp8%3D"; // The mode=2 auth token from your server
TVULiveRoom.TVURoomAuthMode roomAuthMode = TVULiveRoom.TVURoomAuthMode.CUSTOM; // Auth mode: Custom
boolean isPortrait = true; // Whether it is a portrait live room

// 2. Call joinLiveRoom to enter the live room
TVULiveRoom.joinLiveRoom(context, new JoinRoomConfig(activityId, token, roomAuthMode, isPortrait));
```


<span id="b0a716bb"></span>
#### **Flow 2: Watch\-First**

**Principle**: Viewers first enter as guests and are prompted to log in only when they perform specific interactions. This involves **switching auth modes**: first entering with a `mode=1` (Public) token, then switching to `mode=2` (Custom) after a successful login.

**Process**:

**Phase 1: Guest Enters Live Room**


1. **User Enters Live Room**: The user taps to enter a live room in your app.

2. **App Requests Guest Token**: Your app requests a public\-mode (`mode=1`) token from your server.

3. **Server Gets Token**: Your server calls `GetSDKTokenAPI` with `mode=1`.

4. **Server Relays Token**: The token is returned from BytePlus Live and sent to your app.

5. **App Sets Login Listener**: The app calls the SDK's [setCustomLoginListener](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings?lang=en#setcustomloginlistener) method to register a listener for handling future login requests.

6. **App Enters Live Room**: The app calls [joinLiveRoom](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-tvuliveroom?lang=en#joinliveroom) with the `mode=1` token, allowing the user to enter as a guest.


**Phase 2: Login Triggered**


1. **User Interacts**: When the user performs an action requiring identity (commenting, liking, voting, etc.), the SDK triggers the login flow.

2. **`onCustomLoginStart`** ** Callback**: The SDK invokes the [onCustomLoginStart](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#d3799085) callback on your pre\-set `CustomLoginListener`, notifying the app that a login is required.

3. **App Handles Login**: Your app displays your custom login UI.

4. **User Completes Login**: The user authenticates through your login interface.

5. **App Requests Token**: After a successful login, the app requests a custom\-mode (`mode=2`) token from your server.

6. **Server Gets Token**: Your server calls `GetSDKTokenAPI` with `mode=2`.

7. **Server Relays Token**: The token is returned from BytePlus Live and sent to your app.

8. **`onLoginFinished`** ** Callback**: The app passes the newly acquired `mode=2` token into the [onLoginFinished](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#cb937422) callback. If the user cancels, it passes `null`.

9. **SDK Finalizes Login**: The SDK uses the new token to fetch user info and refresh the login state, enabling the user to interact.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f2dbc6af4b404947bd69473c5949f890~tplv-goo7wpa0wc-image.image) </span>

**Code Sample**:

```java
// 1. Set the custom login listener
CustomSettings settings = CustomSettings.Holder.mSettings;
settings.setCustomLoginListener((context, activityId, callBack) -> {
    // 2. After the onCustomLoginStart callback is triggered, execute the app's custom login logic.
    // This example shows a dialog, but you can replace it with a navigation to your own login screen.
    new AlertDialog.Builder(context)
            .setTitle("Please Log In")
            .setView(editText) // Assuming editText is a view for user input
            .setCancelable(false)
            .setPositiveButton(android.R.string.yes, (dialog, which) -> {
                // 3. After a successful login, get the mode=2 token from your server.
                // This example assumes the user inputs the token directly.
                String token = editText.getText().toString().trim();
                
                // 4. Trigger the onLoginFinished callback, passing the decoded token to the SDK.
                // Note: The token from the server might be URL-encoded and require decoding.
                callBack.onLoginFinished(URLDecoder.decode(token));
            })
                // 5. If the user cancels, trigger the callback with null.
            .setNegativeButton(android.R.string.no, ((dialog, which) -> callBack.onLoginFinished(null)))
            .setIcon(android.R.drawable.ic_dialog_alert)
            .show();
});
```


<span id="04937a04"></span>
### Scenario 2: Native iOS App integration

<span id="df4ee69f"></span>
#### **Flow 1: Login\-First**

**Principle**: Viewers must log in before entering the live room. The authentication mode is "Custom". You need to set the `mode` parameter to `2` when calling the [GetSDKTokenAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getsdktokenapi).

**Process**:


1. **User Logs In**: The user logs into your app and then attempts to enter a live room.

2. **App Requests Token**: Your app requests an authentication token from your business server.

3. **Server Gets Token**: Your server calls the BytePlus Live server\-side API `GetSDKTokenAPI`, passing the user's information and setting `mode=2` to request a custom\-mode token.

4. **Server Returns Token**: After successful validation, the BytePlus Live server returns a one\-time, temporary token.

5. **App Receives Token**: Your server relays the token to your app.

6. **App Enters Live Room**: The app calls the SDK's [joinLiveRoomWithActivity:success:failure:](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#BDLLiveEngine-joinliveroomwithactivity-success-failure) method with the token to enter the live room.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7969abecc4574f2384d406ca9a65740c~tplv-goo7wpa0wc-image.image) </span>

**Code Sample**:

After obtaining the `mode=2` token, call the `joinLiveRoomWithActivity:success:failure:` method.

```objc
- (void)joinLiveRoom {
    // 1. Configure live room parameters
    BDLActivity *activity = [[BDLActivity alloc] init];
    activity.activityId = @(167808997736****); // The activity ID of the live room
    activity.token = @"ak3T%2FdaGJDL5zSFD7%2F1GPGP****"; // The mode=2 auth token from your server
    activity.isPortrait = YES; // Whether it is a portrait live room
    activity.authMode = BDLActivityAuthModeCustom; // Auth mode: Custom

    // 2. Call the method to enter the live room
    [[BDLLiveEngine sharedInstance] joinLiveRoomWithActivity:activity success:^{
        // Join the live room successfully.
    } failure:^(NSError * _Nonnull error) {
        // Failed to join the live room.
    }];
}
```


<span id="e630c266"></span>
#### **Flow 2: Watch\-First**

**Principle**: Viewers first enter as guests and are prompted to log in only when they perform specific interactions. This involves **switching auth modes**: first entering with a `mode=1` (Public) token, then switching to `mode=2` (Custom) after a successful login.

**Process and code sample**

**Phase 1: Guest Enters Live Room**


1. **User Enters Live Room**: The user taps to enter a live room in your app.

2. **App Requests Guest Token**: Your app requests a public\-mode (`mode=1`) token from your server.

3. **Server Gets Token**: Your server calls `GetSDKTokenAPI` with `mode=1`.

4. **Server Relays Token**: The token is returned from BytePlus Live and sent to your app.

5. **App** **Sets the loginProvider** delegate for BDLLiveEngine, which is the proxy for logging in to the live room in custom mode. The sample code is as follows.

   ```objectivec
   ...
   [[BDLLiveEngine sharedInstance] setLoginProvider:self];
   ...
   ```
   

6. **App Enters Live Room**: The app calls [joinLiveRoomWithActivity:success:failure:](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#BDLLiveEngine-joinliveroomwithactivity-success-failure) method with the token to enter the live room.


**Phase 2: Login Triggered**


1. **User Interacts**: When the user performs an action requiring identity (commenting, liking, voting, etc.), the SDK triggers the login flow.

2. **Invoke Login Method**: The SDK calls the [loginWithActivity:completion:](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-SDK-for-ios-callbacks#BDLLoginProvider-loginwithactivity-completion) method to initiate the login process.

3. **App Handles Login**: Your app displays your custom login UI.

4. **User Completes Login**: The user authenticates through your login interface.

5. **App Requests Token**: After a successful login, the app requests a custom\-mode (`mode=2`) token from your server.

6. **Server Gets Token**: Your server calls `GetSDKTokenAPI` with `mode=2`.

7. **Server Relays Token**: The token is returned from BytePlus Live and sent to your app.

8. **Pass Token via Callback**: The app passes the custom mode token to the SDK by calling the `completion` callback in the [loginWithActivity:completion:](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-SDK-for-ios-callbacks#BDLLoginProvider-loginwithactivity-completion) method.

   ```objectivec
   - (void)loginWithActivity:(BDLActivity *)activity completion:(void (^)(NSString * _Nullable token))completion {
       // Replace the getToken: method with the method you use to get the authorization token.
       [self getToken:^(NSString *token) {
           completion(token);
       }];
   }
   ```
   

9. The SDK requests viewer information from BytePlus Live by using the token.

10. After verifying that the token is valid, BytePlus Live returns the viewer information to the SDK. If the token verification fails or the token is empty, BytePlus Live returns an error message to the SDK.

11. The SDK calls the `loginComplete:error:` method to notify the app whether the custom login process is successful. The sample code is as follows.


```objectivec
- (void)loginComplete:(BDLActivity *)activity error:(NSError *)error {
    if (!error) {
        NSLog(@"Custom login is successful");
    }
    else {
        NSLog(@"Custom login failed %@", error.localizedDescription);
    }
}
```



12. (Optional) If the live room page is closed during the viewer login process, the SDK triggers the `cancelLoginWithActivity:` callback, and you can cancel the custom login process as needed. The sample code is as follows.


```objectivec
- (void)cancelLoginWithActivity:(BDLActivity *)activity {
// After the cancelLoginWithActivity: callback is triggered, cancel the custom login process as needed.
    NSLog(@"If the live room page is closed during the login process, you can cancel the login process as needed in the app");
}
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f2dbc6af4b404947bd69473c5949f890~tplv-goo7wpa0wc-image.image) </span>

<span id="d794a557"></span>
### Scenario 3: Web SDK Integration

The Web SDK supports custom authentication on both PC and mobile platforms.

<span id="40bdb66e"></span>
#### **Flow 1: Login\-First**

**Principle**: Viewers must log in before entering the live room. The authentication mode is "Custom". You need to set the `mode` parameter to `2` when calling the [GetSDKTokenAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getsdktokenapi).

**Process**:


1. The user logs into your website.

2. Your server calls `GetSDKTokenAPI` (with `mode=2`) to get an auth token.

3. When initializing `ByteLiveWebSDK`, set `mode` to `2` and pass the obtained `token`.


**Code Sample**:

```javascript
var webSDK = new window.ByteLiveWebSDK({
    activityId: 172291833994****,
    token: 'ak3T%2FdaGJDL5zSFD7%2F1GPGP****',
    service: 'liveDemo',
    mode: 2, 
    ...
```


<span id="dee99e46"></span>
#### **Flow 2: Watch\-First**

**Principle**: Viewers first enter as guests and are prompted to log in only when they perform specific interactions. This involves **switching auth modes**: first entering with a `mode=1` (Public) token, then switching to `mode=2` (Custom) after a successful login.

**Process**:


1. **Guest Initialization**: Initialize the SDK with `mode: 1`, `disabledLogin: true` (to disable the SDK's built\-in login), and a `mode=1` token.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can obtain the authorization token for mode=1 in any of the following ways:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Log in to the <a href="https://console.byteplus.com/livesaas/liveManagement/">BytePlus Live console</a> and get the token from the <strong>Web SDK embedding</strong> tab on the <strong>Producer</strong> \> <strong>Page embedding</strong> page in a live room.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Call <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi">GetSDKTokenAPI</a> to get the token.   </div>
   

2. **Listen for Event**: Use `webSDK.on('permission.need', handleLogin)` to listen to the [permission.need](https://docs.byteplus.com/en/docs/byteplus-livesaas/events#permission-need) event.

3. **Event Triggered**: When a viewer attempts an interaction that requires login (commenting, liking, etc.), the SDK emits the `permission.need` event.

4. **Execute Login**: In your `handleLogin` function, trigger your custom login process (e.g., show a login modal).

5. **Get New Token**: After the user successfully logs in, fetch a new `mode=2` token from your server.

6. **Update Token**: Call [updateMode2Token](https://docs.byteplus.com/en/docs/byteplus-livesaas/api#updatemode2token) to update the token within the SDK. The SDK will automatically handle the subsequent login state refresh.


**Code Sample**:

```javascript
var webSDK = new window.ByteLiveWebSDK({
    activityId: 172291833994****,
    token: 'ps****',
    service: 'liveDemo',
    mode: 1,
    options: {
      saveUserInfo: true, // Optional. Used to cache user information when the value of mode is set to 1.
      disabledLogin: true, // Disable BytePlus Live's built-in login system.
    }
  })
  
    const login = () => {
    // Implement the login logic yourself.
    return {
      Nickname: 'Viewer A',
      UserIdStr: '57584'
    }
  }

  const getSDKToken = () => {
    //  Implement the logic yourself to get the token when the value of mode is set to 2.
    return {
      Token: 'hdsh****'
    }
  }
  // Execute the handleLogin function after detecting the permission.need event.
  const handleLogin = async () => {
      // Trigger the custom login process and viewers must log in to your account system.
      const userInfo = await login();
      // Use the login user information to call GetSDKTokenAPI to get the token when the value of mode is set to 2.
      const res = getSDKToken(userInfo);
      // Call the SDK's updateMode2Token method to replace the mode=1 token with the mode=2 token.
      webSDK.updateMode2Token(res.Token);
  }
  // Listen to the permission.need event.
  webSDK.on('permission.need', handleLogin);
```


<span id="2f0cd1e6"></span>
### Other Scenarios: H5, iframe, or SaaS Viewing Page

If you are embedding the viewing page via H5, iframe, or using the direct SaaS viewing page link, please refer to the [Custom authentication login](https://docs.byteplus.com/zh-CN/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions) documentation to implement custom login.
