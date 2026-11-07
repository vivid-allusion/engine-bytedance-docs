---
title: "为观众 SDK 实现自定义登录"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-custom-login-zh-CN"
---

自定义登录是一种身份验证机制，允许您的观众使用您自有用户系统（例如您的电商平台、应用或内部系统）的账户信息，无缝访问 BytePlus Live 观看页。

该功能可实现 BytePlus Live 服务与您的业务场景深度集成，实现**统一身份认证**和流畅的用户体验。此外，您还可以在直播数据分析中关联自有系统的账户信息，实现**跨平台分析**。

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3f56a1df68f346be8abd6c6d2718d291~tplv-goo7wpa0wc-image.image" width="729px" /></div>


<span id="a07a662d"></span>
## 与 OAuth 2.0 的区别

自定义登录和 OAuth 2.0 均可实现“第三方用户登录”，即观众在观看直播流前先登录您的账户系统。请根据您的业务场景和技术需求选择合适的方式。


* **如需选择 OAuth 2.0：** 

   * 您的系统已具备**成熟、标准的 OAuth 2.0 用户授权服务**。

   * 您倾向于采用业界标准协议进行系统集成，以简化长期维护。

   * 您的用户体验可以接受额外的页面跳转和授权步骤。

* **如需选择自定义登录：** 

   * 您希望实现单点登录（SSO）体验，让用户无缝进入直播间。

   * 您的系统**尚未具备现成的 OAuth 2.0 服务**，但仍需实现第三方用户登录。

   * 您需要对集成过程拥有更高的**控制权和灵活性**，例如自定义令牌的过期与刷新逻辑。


<span id="60bfc569"></span>
## 用户流程展示

我们为您提供两种常见的登录交互流程供体验。


|**流程** |**接口行为** |**应用场景** |**演示** |
|---|---|---|---|
|**先登录后观看** |观众必须先登录，才能进入直播间观看和互动。 |适用于需要严格身份验证、访问控制或用户行为追踪的场景，如企业培训、付费课程或专属会员活动。此方式安全性更高，但可能会提高观众的进入门槛。 |1. 点击[此处](https://live.byteplus.com/demo/sdk/index.playground.html?mode=pc-custom)打开演示。<br><br>2. 输入昵称并点击**登录**。<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9641e97317334dcd8890507134d6a016~tplv-goo7wpa0wc-image.image) </span><br><br>随后即可观看直播流并发送消息。 |
|**先观看后登录** |观众可作为游客进入直播间观看。仅在尝试评论、点赞等互动操作时才会触发登录流程。 |适用于面向潜在客户引流和转化的公开活动及营销直播。此方式降低了初始进入门槛，鼓励更多用户参与。 |1. 点击[此处](https://live.byteplus.com/demo/sdk/index.playground.html?mode=pc-custom)打开演示。<br><br>2. 点击**游客登录**即可直接进入。可查看直播流和消息。<br><br>3. 尝试在聊天框输入消息以触发登录提示。<br><br>4. 输入昵称并点击**登录**。<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b56406e8ebb842ff86b284a5942d70f9~tplv-goo7wpa0wc-image.image) </span><br><br>随后即可发送消息。 |


<span id="fa2173d1"></span>
## 实现指南

本节为上述两种流程提供实现指南。请根据您的观看页集成场景选择合适的方式。无论采用哪种方式，您都需调用[GetSDKTokenAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getsdktokenapi)，为每位观众动态获取临时令牌。

<span id="e47acb29"></span>
### 场景一：原生 Android 应用集成

<span id="807fa016"></span>
#### **流程 1：先登录**

**原理**：观众需先登录后才能进入直播间。认证模式为“自定义”。调用[GetSDKTokenAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getsdktokenapi)时，需将`mode`参数设置为`2`。

**流程**：


1. **用户登录**：用户登录你的应用后尝试进入直播间。

2. **应用请求 Token**：你的应用向业务服务器请求认证 Token。

3. **服务器获取 Token**：你的服务器调用 BytePlus Live 服务端 API `GetSDKTokenAPI`，传入用户信息并设置 `mode=2`，请求自定义模式 Token。

4. **服务器返回 Token**： BytePlus Live 服务器验证成功后，返回一次性临时 Token。

5. **应用接收 Token**：你的服务器转发 Token 到你的应用。

6. **应用进入直播间**：应用使用该令牌调用 SDK 的[joinLiveRoom](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-tvuliveroom?lang=en#joinliveroom)方法，进入直播间。


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c8fc6b0914f44aff8916abd5098c4bf4~tplv-goo7wpa0wc-image.image) </span>

**代码示例**：

获取`mode=2`令牌后，调用`joinLiveRoom`方法。

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
#### **流程 2：先观看**

**原理**：观众以嘉宾身份先进入，仅在进行特定交互时才提示登录。该流程涉及**切换认证模式**：先用 `mode=1`（公开）token 进入，登录成功后切换为 `mode=2`（自定义）。

**流程**：

**阶段 1：嘉宾进入直播间**


1. **用户进入直播间**：用户在你的应用中点击进入直播间。

2. **应用请求嘉宾 Token**：你的应用向你的服务器请求一个公开模式（`mode=1`）的 Token。

3. **服务器获取 Token**：你的服务器调用 `GetSDKTokenAPI`，并传入 `mode=1`。

4. **服务器返回 Token**：Token 从 BytePlus Live 返回并发送给你的应用。

5. **应用设置登录监听器**：应用调用 SDK 的 [setCustomLoginListener](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings?lang=en#setcustomloginlistener) 方法，注册监听器以处理后续登录请求。

6. **应用进入直播间**：应用使用 [joinLiveRoom](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-tvuliveroom?lang=en#joinliveroom) 方法，并传入 `mode=1` Token，允许用户以嘉宾身份进入。


**阶段 2：触发登录**


1. **用户交互**：当用户执行需要身份的操作（评论、点赞、投票等）时，SDK 会触发登录流程。

2. **`onCustomLoginStart`** ** 回调**：SDK 会在你预设的 `CustomLoginListener` 上调用 [onCustomLoginStart](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#d3799085) 回调，通知应用需要登录。

3. **应用处理登录**：你的应用展示自定义登录界面。

4. **用户完成登录**：用户通过你的登录界面完成身份验证。

5. **应用请求 Token**：登录成功后，应用向你的服务器请求自定义模式（`mode=2`）的 token。

6. **服务器获取 Token**：你的服务器调用 `GetSDKTokenAPI` 并传入 `mode=2`。

7. **服务器返回 Token**：Token 从 BytePlus Live 返回并发送给你的应用。

8. **`onLoginFinished`** ** 回调**：应用将新获取的 `mode=2` Token 传入 [onLoginFinished](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#cb937422) 回调。如果用户取消，则传入 `null`。

9. **SDK 完成登录**：SDK 使用新 Token 获取用户信息并刷新登录状态，使用户可以互动。


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f2dbc6af4b404947bd69473c5949f890~tplv-goo7wpa0wc-image.image) </span>

**代码示例**：

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
### 场景 2：原生 iOS 应用集成

<span id="df4ee69f"></span>
#### **流程 1：先登录**

**原则**：观众必须先登录才能进入直播间。认证模式为“自定义”。调用 [GetSDKTokenAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getsdktokenapi) 时，需要将 `mode` 参数设置为 `2`。

**流程**：


1. **用户登录**：用户登录你的应用后尝试进入直播间。

2. **应用请求 Token**：你的应用向业务服务器请求认证 Token。

3. **服务器获取 Token**：你的服务器调用 BytePlus Live 服务端 API `GetSDKTokenAPI`，传入用户信息并设置 `mode=2`，请求自定义模式 Token。

4. **服务器返回 Token**： BytePlus Live 服务器验证成功后，返回一次性临时 Token。

5. **应用接收 Token**：你的服务器转发 Token 到你的应用。

6. **应用进入直播间**：应用调用 SDK 的 [joinLiveRoomWithActivity:success:failure:](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#BDLLiveEngine-joinliveroomwithactivity-success-failure) 方法，并传入 Token 进入直播间。


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7969abecc4574f2384d406ca9a65740c~tplv-goo7wpa0wc-image.image) </span>

**代码示例**：

获取 `mode=2` Token 后，调用 `joinLiveRoomWithActivity:success:failure:` 方法。

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
#### **流程 2：先观看**

**原理**：观众以嘉宾身份先进入，仅在进行特定交互时才提示登录。该流程涉及**切换认证模式**：先用 `mode=1`（公开）token 进入，登录成功后切换为 `mode=2`（自定义）。

**流程及代码示例**

**阶段 1：嘉宾进入直播间**


1. **用户进入直播间**：用户在你的应用中点击进入直播间。

2. **应用请求嘉宾 Token**：你的应用向你的服务器请求一个公开模式（`mode=1`）的 Token。

3. **服务器获取 Token**：你的服务器调用 `GetSDKTokenAPI`，并传入 `mode=1`。

4. **服务器返回 Token**：Token 从 BytePlus Live 返回并发送给你的应用。

5. **应用设置 loginProvider** 委托给 BDLLiveEngine，该委托作为自定义模式下登录直播间的代理。示例代码如下。

   ```objectivec
   ...
   [[BDLLiveEngine sharedInstance] setLoginProvider:self];
   ...
   ```
   

6. **应用进入直播间**：应用通过携带 token 调用 [joinLiveRoomWithActivity:success:failure:](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#BDLLiveEngine-joinliveroomwithactivity-success-failure) 方法进入直播间。


**阶段 2：触发登录**


1. **用户交互**：当用户执行需要身份的操作（评论、点赞、投票等）时，SDK 会触发登录流程。

2. **调用登录方法**：SDK 调用 [loginWithActivity:completion:](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-SDK-for-ios-callbacks#BDLLoginProvider-loginwithactivity-completion) 方法发起登录流程。

3. **应用处理登录**：你的应用展示自定义登录界面。

4. **用户完成登录**：用户通过你的登录界面完成身份验证。

5. **应用请求 Token**：登录成功后，应用向你的服务器请求自定义模式（`mode=2`）的 token。

6. **服务器获取 Token**：你的服务器调用 `GetSDKTokenAPI` 并传入 `mode=2`。

7. **服务器返回 Token**：Token 从 BytePlus Live 返回并发送给你的应用。

8. **通过回调传递 Token**：应用在 [loginWithActivity:completion:](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-SDK-for-ios-callbacks#BDLLoginProvider-loginwithactivity-completion) 方法中调用 `completion` 回调，将自定义模式的 token 传递给 SDK。

   ```objectivec
   - (void)loginWithActivity:(BDLActivity *)activity completion:(void (^)(NSString * _Nullable token))completion {
       // Replace the getToken: method with the method you use to get the authorization token.
       [self getToken:^(NSString *token) {
           completion(token);
       }];
   }
   ```
   

9. SDK 使用该 token 向 BytePlus Live 请求观众信息。

10. BytePlus Live 验证 token 有效后，将观众信息返回给 SDK。如果 token 校验失败或 token 为空， BytePlus Live 会向 SDK 返回错误信息。

11. SDK 调用 `loginComplete:error:` 方法，通知应用自定义登录流程是否成功。示例代码如下。


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



12. （可选）如果在观众登录流程中关闭了直播间页面，SDK 会触发 `cancelLoginWithActivity:` 回调，你可以根据需要取消自定义登录流程。示例代码如下。


```objectivec
- (void)cancelLoginWithActivity:(BDLActivity *)activity {
// After the cancelLoginWithActivity: callback is triggered, cancel the custom login process as needed.
    NSLog(@"If the live room page is closed during the login process, you can cancel the login process as needed in the app");
}
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f2dbc6af4b404947bd69473c5949f890~tplv-goo7wpa0wc-image.image) </span>

<span id="d794a557"></span>
### 场景 3：Web SDK 集成

Web SDK 支持在 PC 和移动端自定义认证。

<span id="40bdb66e"></span>
#### **流程 1：先登录**

**原理**：观众需先登录后才能进入直播间。认证模式为“自定义”。调用 [GetSDKTokenAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getsdktokenapi) 时，需要将 `mode` 参数设置为 `2`。

**流程**：


1. 用户登录你的网站。

2. 你的服务器调用 `GetSDKTokenAPI`（携带 `mode=2`）获取认证 token。

3. 初始化 `ByteLiveWebSDK` 时，设置 `mode` 为 `2`，并传入获取到的 `token`。


**代码示例**：

```javascript
var webSDK = new window.ByteLiveWebSDK({
    activityId: 172291833994****,
    token: 'ak3T%2FdaGJDL5zSFD7%2F1GPGP****',
    service: 'liveDemo',
    mode: 2, 
    ...
```


<span id="dee99e46"></span>
#### **流程 2：先观看**

**原理**：观众以嘉宾身份先进入，仅在进行特定交互时才提示登录。该流程涉及**切换认证模式**：先用 `mode=1`（公开）token 进入，登录成功后切换为 `mode=2`（自定义）。

**流程**：


1. **嘉宾初始化**：使用 `mode: 1`、`disabledLogin: true`（禁用 SDK 内置登录）和 `mode=1` token 初始化 SDK。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">你可以通过以下任意方式获取 mode=1 的授权 token：   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">登录<a href="https://console.byteplus.com/livesaas/liveManagement/"> BytePlus BytePlus Live 控制台</a>，在直播间的<strong>Web SDK 嵌入</strong>标签页的<strong>Producer</strong> \> <strong>页面嵌入</strong>页面获取 token。   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">调用 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi">GetSDKTokenAPI</a> 获取 token。   </div>
   

2. **监听事件**：通过 `webSDK.on('permission.need', handleLogin)` 监听 [permission.need](https://docs.byteplus.com/en/docs/byteplus-livesaas/events#permission-need) 事件。

3. **事件触发**：当观众尝试需要登录的交互（评论、点赞等）时，SDK 会触发 `permission.need` 事件。

4. **执行登录**：在 `handleLogin` 函数中，触发自定义登录流程（如弹出登录弹窗）。

5. **获取新 Token**：用户登录成功后，从你的服务器获取新的 `mode=2` token。

6. **更新 Token**：调用 [updateMode2Token](https://docs.byteplus.com/en/docs/byteplus-livesaas/api#updatemode2token) 方法，更新 SDK 内的 token。SDK 会自动处理后续的登录状态刷新。


**代码示例**：

```javascript
var webSDK = new window.ByteLiveWebSDK({
    activityId: 172291833994****,
    token: 'ps****',
    service: 'liveDemo',
    mode: 1,
    options: {
      saveUserInfo: true, // Optional.用于在 mode 设置为 1 时缓存用户信息。
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
### 其他场景：H5、iframe 或 SaaS 观看页

如果通过 H5、iframe 嵌入观看页，或使用 SaaS 观看页的直接链接，请参考 [自定义认证登录](https://docs.byteplus.com/zh-CN/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions)文档实现自定义登录。
