---
title: "為 Viewer SDK 實現自訂登入"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/wei-viewer-sdk-shi-xian-zi-ding-deng-ru-zh-TW"
---

自訂登入是一種驗證機制，允許您的觀眾使用您自有用戶系統的帳戶資訊（例如您的電商平台、應用程式或內部系統），無縫存取 BytePlus Live 的觀看頁面。

此功能可讓 BytePlus Live 服務與您的業務場景深度整合，實現**統一身份驗證**並提供流暢的用戶體驗。同時，您也能在直播數據分析中關聯自有系統的帳戶資訊，以進行**跨平台分析**。

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3f56a1df68f346be8abd6c6d2718d291~tplv-goo7wpa0wc-image.image" width="729px" /></div>


<span id="a07a662d"></span>
## 與 OAuth 2.0 的差異

自訂登入與 OAuth 2.0 均可實現「第三方用戶登入」，即觀眾在觀看直播前先登入您的帳戶系統。請根據您的業務場景與技術需求選擇合適的方法。


* **若選擇 OAuth 2.0：** 

   * 您的系統已具備**成熟且標準的 OAuth 2.0 用戶授權服務**。

   * 您偏好遵循業界標準協議進行系統整合，便於長期維護。

   * 用戶體驗可接受額外的頁面跳轉與授權步驟。

* **若選擇自訂登入：** 

   * 您希望實現單一登入（SSO）體驗，讓用戶無縫進入直播間。

   * 您的系統**尚未具備現成的 OAuth 2.0 服務**，但仍需實現第三方用戶登入。

   * 您需要對整合流程有更高的**控制權與彈性**，例如自訂權杖的有效期與刷新邏輯。


<span id="60bfc569"></span>
## 用戶流程展示

我們提供兩種常見的登入互動流程供您體驗。


|**流程** |**說明** |**使用案例** |**示範** |
|---|---|---|---|
|**先登入** |觀眾必須先登入才能進入直播間觀看及互動。 |適用於需要嚴格身份驗證、存取控制或用戶行為追蹤的場景，例如企業培訓、付費課程或專屬會員活動。此方式安全性較高，但可能會提高觀眾的進入門檻。 |1. 點擊 [這裡](https://live.byteplus.com/demo/sdk/index.playground.html?mode=pc-custom)開啟示範。<br><br>2. 輸入暱稱並點擊**登入**。<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9641e97317334dcd8890507134d6a016~tplv-goo7wpa0wc-image.image) </span><br><br>您即可觀看直播並發送訊息。 |
|**先觀看** |觀眾可作為遊客進入直播間觀看。僅當觀眾嘗試進行評論、點讚等互動操作時才會觸發登入流程。 |適用於公開活動及以引流轉化為目標的行銷直播。此方式降低了初始進入門檻，有助於吸引更多參與者。 |1. 點擊 [這裡](https://live.byteplus.com/demo/sdk/index.playground.html?mode=pc-custom)開啟示範。<br><br>2. 點擊**遊客登入**即可直接進入。您可以看到直播畫面及訊息。<br><br>3. 嘗試在聊天框輸入訊息以觸發登入提示。<br><br>4. 輸入暱稱並點擊**登入**。<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b56406e8ebb842ff86b284a5942d70f9~tplv-goo7wpa0wc-image.image) </span><br><br>您即可發送訊息。 |


<span id="fa2173d1"></span>
## 實作指南

本節提供上述兩種流程的實作指南。請根據您的觀看頁面整合場景選擇合適的方法。無論採用哪種方法，您都必須呼叫[GetSDKTokenAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getsdktokenapi)，為每位觀眾動態取得臨時權杖。

<span id="e47acb29"></span>
### 場景一：原生 Android App 整合

<span id="807fa016"></span>
#### **流程一：先登入**

**原則**：觀眾必須先登入才能進入直播間。驗證模式為「自訂」。呼叫[GetSDKTokenAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getsdktokenapi)時，需將`mode`參數設為`2`。

**流程**：


1. **用戶登入**：用戶登入您的應用程式後，嘗試進入直播間。

2. **App 請求權杖**：您的 App 向業務伺服器請求驗證權杖。

3. **伺服器取得權杖**：您的伺服器呼叫 BytePlus Live 後端 API `GetSDKTokenAPI`，傳入用戶資訊並設置`mode=2`，以請求自訂模式權杖。

4. **伺服器回傳權杖**：驗證成功後，BytePlus Live 伺服器回傳一次性臨時權杖。

5. **App 接收權杖**：您的伺服器將權杖轉發給 App。

6. **App 進入直播間**：App 使用權杖呼叫 SDK 的[joinLiveRoom](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-tvuliveroom?lang=en#joinliveroom)方法進入直播間。


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c8fc6b0914f44aff8916abd5098c4bf4~tplv-goo7wpa0wc-image.image) </span>

**程式碼範例**：

取得`mode=2`權杖後，呼叫`joinLiveRoom`方法。

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
#### **流程二：先觀看**

**原則**：觀眾先以訪客身份進入，僅於執行特定互動時才提示登入。此流程涉及**切換驗證模式**：先以`mode=1`（公開）權杖進入，登入成功後再切換為`mode=2`（自訂）。

**流程**：

**階段一：訪客進入直播間**


1. **用戶進入直播間**：用戶在您的 App 點擊進入直播間。

2. **應用程式請求訪客權杖**：您的應用程式會向您的伺服器請求公開模式（`mode=1`）權杖。

3. **伺服器取得權杖**：您的伺服器會以 `mode=1` 呼叫 `GetSDKTokenAPI`。

4. **伺服器轉發權杖**：權杖會從 BytePlus Live 返回並傳送至您的應用程式。

5. **應用程式設置登入監聽器**：應用程式會呼叫 SDK 的 [setCustomLoginListener](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings?lang=en#setcustomloginlistener) 方法，註冊監聽器以處理未來的登入請求。

6. **應用程式進入直播間**：應用程式會以 `mode=1` 權杖呼叫 [joinLiveRoom](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-tvuliveroom?lang=en#joinliveroom)，允許使用者以訪客身份進入。


**階段二：觸發登入**


1. **使用者互動**：當使用者執行需要身份驗證的操作（評論、按讚、投票等）時，SDK 會觸發登入流程。

2. **`onCustomLoginStart`** ** 回呼**：SDK 會在您預設的 `CustomLoginListener` 上呼叫 [onCustomLoginStart](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#d3799085) 回呼，通知應用程式需要登入。

3. **應用程式處理登入**：您的應用程式會顯示自訂登入介面。

4. **使用者完成登入**：使用者會透過您的登入介面進行身份驗證。

5. **應用程式請求權杖**：成功登入後，應用程式會向您的伺服器請求自訂模式（`mode=2`）權杖。

6. **伺服器取得權杖**：您的伺服器會以 `mode=2` 呼叫 `GetSDKTokenAPI`。

7. **伺服器轉發權杖**：權杖會從 BytePlus Live 返回並傳送至您的應用程式。

8. **`onLoginFinished`** ** 回呼**：應用程式會將新取得的 `mode=2` 權杖傳入 [onLoginFinished](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#cb937422) 回呼。若使用者取消，則傳入 `null`。

9. **SDK 完成登入**：SDK 會使用新權杖取得使用者資訊並刷新登入狀態，使使用者能夠互動。


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f2dbc6af4b404947bd69473c5949f890~tplv-goo7wpa0wc-image.image) </span>

**程式碼範例**：

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
### 情境二：原生 iOS 應用程式整合

<span id="df4ee69f"></span>
#### **流程一：先登入**

**原則**：觀眾必須先登入才能進入直播間。驗證模式為「自訂」。呼叫 [GetSDKTokenAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getsdktokenapi) 時，需將 `mode` 參數設為 `2`。

**流程**：


1. **使用者登入**：使用者登入您的應用程式後嘗試進入直播間。

2. **應用程式請求權杖**：您的應用程式會向業務伺服器請求驗證權杖。

3. **伺服器取得權杖**：您的伺服器會呼叫 BytePlus Live 伺服器端 API `GetSDKTokenAPI`，傳入使用者資訊並設置 `mode=2`，以請求自訂模式權杖。

4. **伺服器返回權杖**：驗證成功後，BytePlus Live 伺服器會返回一次性、臨時權杖。

5. **應用程式接收權杖**：您的伺服器會將權杖轉發至您的應用程式。

6. **應用程式進入直播間**：應用程式會以權杖呼叫 SDK 的 [joinLiveRoomWithActivity:success:failure:](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#BDLLiveEngine-joinliveroomwithactivity-success-failure) 方法進入直播間。


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7969abecc4574f2384d406ca9a65740c~tplv-goo7wpa0wc-image.image) </span>

**程式碼範例**：

取得 `mode=2` 權杖後，呼叫 `joinLiveRoomWithActivity:success:failure:` 方法。

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
#### **流程二：先觀看**

**原則**：觀眾先以訪客身份進入，僅在執行特定互動時才提示登入。此流程涉及 **切換驗證模式**：先以 `mode=1`（公開）權杖進入，成功登入後再切換至 `mode=2`（自訂）。

**流程與程式碼範例**

**階段一：訪客進入直播間**


1. **使用者進入直播間**：使用者在您的應用程式中點擊進入直播間。

2. **應用程式請求訪客權杖**：您的應用程式會向您的伺服器請求公開模式（`mode=1`）權杖。

3. **伺服器取得權杖**：您的伺服器會以 `mode=1` 呼叫 `GetSDKTokenAPI`。

4. **伺服器轉發權杖**：權杖會從 BytePlus Live 返回並傳送至您的應用程式。

5. **App 設定 loginProvider** 委託給 BDLLiveEngine，該委託是自訂模式下登入直播間的代理。範例程式碼如下。

   ```objectivec
   ...
   [[BDLLiveEngine sharedInstance] setLoginProvider:self];
   ...
   ```
   

6. **App 進入直播間**：App 使用 [joinLiveRoomWithActivity:success:failure:](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#BDLLiveEngine-joinliveroomwithactivity-success-failure) 方法並帶入令牌以進入直播間。


**階段二：觸發登入**


1. **用戶互動**：當用戶執行需要身份驗證的操作（評論、按讚、投票等），SDK 會觸發登入流程。

2. **調用登入方法**：SDK 調用 [loginWithActivity:completion:](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-SDK-for-ios-callbacks#BDLLoginProvider-loginwithactivity-completion) 方法啟動登入流程。

3. **App 處理登入**：您的 App 顯示自訂登入 UI。

4. **用戶完成登入**：用戶透過您的登入介面進行身份驗證。

5. **App 請求令牌**：登入成功後，App 向您的伺服器請求自訂模式（`mode=2`）令牌。

6. **伺服器取得令牌**：您的伺服器調用 `GetSDKTokenAPI` 並帶入 `mode=2`。

7. **伺服器傳遞令牌**：令牌由 BytePlus Live 返回並傳送至您的 App。

8. **透過回呼傳遞令牌**：App 透過調用 `completion` 回呼於 [loginWithActivity:completion:](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-SDK-for-ios-callbacks#BDLLoginProvider-loginwithactivity-completion) 方法中，將自訂模式令牌傳給 SDK。

   ```objectivec
   - (void)loginWithActivity:(BDLActivity *)activity completion:(void (^)(NSString * _Nullable token))completion {
       // Replace the getToken: method with the method you use to get the authorization token.
       [self getToken:^(NSString *token) {
           completion(token);
       }];
   }
   ```
   

9. SDK 使用令牌向 BytePlus Live 請求觀眾資訊。

10. BytePlus Live 驗證令牌有效後，將觀眾資訊返回給 SDK。若令牌驗證失敗或令牌為空，BytePlus Live 會返回錯誤訊息給 SDK。

11. SDK 調用 `loginComplete:error:` 方法通知 App 自訂登入流程是否成功。範例程式碼如下。


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



12. （可選）若觀眾登入流程期間直播間頁面被關閉，SDK 會觸發 `cancelLoginWithActivity:` 回呼，您可依需求取消自訂登入流程。範例程式碼如下。


```objectivec
- (void)cancelLoginWithActivity:(BDLActivity *)activity {
// After the cancelLoginWithActivity: callback is triggered, cancel the custom login process as needed.
    NSLog(@"If the live room page is closed during the login process, you can cancel the login process as needed in the app");
}
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f2dbc6af4b404947bd69473c5949f890~tplv-goo7wpa0wc-image.image) </span>

<span id="d794a557"></span>
### 情境三：Web SDK 整合

Web SDK 支援 PC 與行動平台的自訂驗證。

<span id="40bdb66e"></span>
#### **流程一：先登入**

**原則**：觀眾必須先登入才能進入直播間。驗證模式為「自訂」。呼叫 [GetSDKTokenAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getsdktokenapi) 時，需將 `mode` 參數設為 `2`。

**流程**：


1. 用戶登入您的網站。

2. 您的伺服器調用 `GetSDKTokenAPI`（帶入 `mode=2`）以取得驗證令牌。

3. 初始化 `ByteLiveWebSDK` 時，設定 `mode` 為 `2` 並傳入取得的 `token`。


**程式碼範例**：

```javascript
var webSDK = new window.ByteLiveWebSDK({
    activityId: 172291833994****,
    token: 'ak3T%2FdaGJDL5zSFD7%2F1GPGP****',
    service: 'liveDemo',
    mode: 2, 
    ...
```


<span id="dee99e46"></span>
#### **流程二：先觀看**

**原則**：觀眾先以訪客身份進入，僅於執行特定互動時才提示登入。此流程涉及 **切換驗證模式**：先以 `mode=1`（公開）令牌進入，登入成功後再切換為 `mode=2`（自訂）。

**流程**：


1. **訪客初始化**：以 `mode: 1`、`disabledLogin: true`（禁用 SDK 內建登入）及 `mode=1` 令牌初始化 SDK。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">您可以透過以下任一方式取得 mode=1 的授權 token：   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">登入 <a href="https://console.byteplus.com/livesaas/liveManagement/">BytePlus Live 控制台</a>，於直播間的 <strong>Web SDK 嵌入</strong>分頁的 <strong>Producer</strong> \> <strong>頁面嵌入</strong>頁面取得 token。   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">呼叫 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi">GetSDKTokenAPI</a> 以取得 token。   </div>
   

2. **監聽事件**：使用 `webSDK.on('permission.need', handleLogin)` 監聽 [permission.need](https://docs.byteplus.com/en/docs/byteplus-livesaas/events#permission-need) 事件。

3. **事件觸發**：當觀眾嘗試需要登入的互動（評論、按讚等），SDK 會發出 `permission.need` 事件。

4. **執行登入**：於您的 `handleLogin` 函數中觸發自訂登入流程（例如顯示登入彈窗）。

5. **取得新令牌**：用戶登入成功後，從您的伺服器取得新的 `mode=2` 令牌。

6. **更新令牌**：調用 [updateMode2Token](https://docs.byteplus.com/en/docs/byteplus-livesaas/api#updatemode2token) 於 SDK 內更新令牌。SDK 會自動處理後續登入狀態刷新。


**程式碼範例**：

```javascript
var webSDK = new window.ByteLiveWebSDK({
    activityId: 172291833994****,
    token: 'ps****',
    service: 'liveDemo',
    mode: 1,
    options: {
      saveUserInfo: true, // Optional.當 mode 的值設為 1 時，用於快取使用者資訊。
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
### 其他場景：H5、iframe 或 SaaS 查看頁面

若您透過 H5、iframe 嵌入查看頁面，或直接使用 SaaS 查看頁面連結，請參考 [自定義驗證登入](https://docs.byteplus.com/zh-CN/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions) 文件以實現自定義登入。
