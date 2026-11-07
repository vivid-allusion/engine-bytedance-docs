---
title: "Viewer SDK for Android: Callbacks"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks"
---

<span id="1b64c86a"></span>
# ITVULiveRoomServerListener

The callback class for listening to the `TVULiveRoomServer` instance. You can perform relevant operations in these callbacks.

```java
public interface ITVULiveRoomServerListener
```


<span id="ea8f5e50"></span>
## Member Functions

<span id="cf15da79"></span>
### onGetRoomDataSuccess

The callback is triggered when the `TVULiveRoomServer.start` method completes execution and successfully gets data from the server.

```java
public void onGetRoomDataSuccess(ActivityResult activityResult)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|activityResult |ActivityResult |The live room data returned from the server. |


<span id="21848038"></span>
### onGetRoomDataFailed

The callback is triggered when the `TVULiveRoomServer.start` method completes execution but fails to get data from the server.

```java
public void onGetRoomDataFailed(int errCode, String errMsg)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|errCode |Integer |The error code. Valid values:<br><br><br>* `0`: ERR_BAD_DATA, which indicates that an error occurred when parsing data returned from the server.<br><br>* `1`: ERR_LIMITED_ROOM, which indicates that the live room is not available on mobile devices. |
|errMsg |String |The reason for failure. |


<span id="1a5686b7"></span>
### onFullScreenChange #{#onFullScreenChange}#

The callback is triggered when the full\-screen or exit\-full\-screen icon is tapped. You can change the player's orientation, show or hide the status bar, and more in this callback.

```java
public void onFullScreenChange()
```


<span id="9d3283d8"></span>
### liveRoomStatusChange

The callback is triggered when the live room status changes.

```java
public void liveRoomStatusChange(int value)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|value |Integer |The current live room status. Valid values:<br><br><br>* `1`: Live.<br><br>* `2`: Preview.<br><br>* `3`: Playback.<br><br>* `4`: Over. |


<span id="f623e692"></span>
### playerStatusChange

The callback is triggered when the play status changes.

```java
public void playerStatusChange(int playerStatus)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|playerStatus |Integer |The current play status. Valid values:<br><br><br>* `0`: Paused.<br><br>* `1`: Playing. |


<span id="ce5cdb18"></span>
### onSpeedButtonDidTouch

The callback is triggered when the playback speed button is tapped.

```java
public void onSpeedButtonDidTouch()
```


<span id="d097dcd1"></span>
### onReplayButtonDidTouch

The callback is triggered when the replay button is tapped.

```java
public void onReplayButtonDidTouch()
```


<span id="19c591f5"></span>
### onUserForceOffline

The SDK triggers this callback when viewers are forcibly removed from the live room.

```Java
default void onUserForceOffline(BDLForceOfflineInfo info)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|info |BDLForceOfflineInfo |The reason for viewers being forcibly removed from the live room. For more information, see [BDLForceOfflineInfo](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#1dbc8f5b). |


<span id="76956141"></span>
# **LanguageListener**

The callback class for tapping the icon to switch languages.

```java
public interface LanguageListener
```


<span id="b9baba94"></span>
## Member Functions

<span id="5567f191"></span>
### onSelectLanguage

The callback is triggered when the switch language icon is tapped. When viewers tap the switch language icon, the SDK calls this callback to notify your app of the tap event.

```java
void onSelectLanguage(Activity activity,
                          ArrayList<LanguageManager.LANGUAGE> languages,
                          LanguageManager.LANGUAGE curLanguage,
                          SelectLanguageCallBack callBack)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|activity |Activity |The Activity of the live room. |
|languages |ArrayList<[LanguageManager.LANGUAGE](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#fb1bfeef)\> |The list of languages currently supported. |
|curLanguage |[LanguageManager.LANGUAGE](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#fb1bfeef) |The currently selected language. |
|callBack |SelectLanguageCallBack |The callback class for language selection. |


<span id="d55d6f65"></span>
# SelectLanguageCallBack

The callback class for language selection.

```java
interface SelectLanguageCallBack
```


<span id="82521414"></span>
## Member Functions

<span id="9c55fd73"></span>
### onLanguageSelected

The callback is triggered when a language is selected. You can customize a language selection dialog box in your app, and after viewers select a language, call this callback to notify the SDK to switch languages.

```java
void onLanguageSelected(LanguageManager.LANGUAGE language)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|language |[LanguageManager.LANGUAGE](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#fb1bfeef) |The language to switch to. |


<span id="1c2e9aff"></span>
# LiveRoomStatusListener

The callback class for the lifecycle of the live room page.

```java
public interface LiveRoomStatusListener
```


<span id="98742e98"></span>
## Member Functions

<span id="4da8af42"></span>
### onLiveRoomActivityCreate

The callback is triggered when the Activity of the live room is created.

```java
void onLiveRoomActivityCreate(Activity activity)
```


<span id="cfe9163a"></span>
### onLandLiveRoomBindingAvailable

The callback is triggered when the `ViewBinding` instance initialization is completed for the live room page in landscape mode. After the SDK triggers this callback, you can use the obtained `ViewBinding` instance to modify the layout and icons of the live room page in landscape mode as needed.

```java
default void onLandLiveRoomBindingAvailable(TvuLivePlayerLayoutBinding binding, LanguageManager languageManager)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|binding |TvuLivePlayerLayoutBinding |The `ViewBinding`instance of the live room page. |
|languageManager |LanguageManager |The language manager. |


<span id="cc008fd8"></span>
### onPortraitLiveRoomBindingAvailable

The SDK triggers this callback when the `ViewBinding` instance initialization is completed for the live room page in portrait mode. After the SDK triggers this callback, you can use the obtained `ViewBinding` instance to modify the layout and icons of the live room page in portrait mode as needed.

```Java
default void onPortraitLiveRoomBindingAvailable(TvuPortraitLiveRoomLayoutBinding binding, LanguageManager languageManager) {}
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|binding |TvuPortraitLiveRoomLayoutBinding |The `ViewBinding`instance of the live room page. |
|languageManager |LanguageManager |The language manager. |


<span id="c9fe1d32"></span>
### onLiveRoomActivityPause

The SDK triggers this callback when the Activity of the live room is switched to the background.

```java
void onLiveRoomActivityPause(Activity activity)
```


<span id="95159e09"></span>
### onLiveRoomActivityResume

The SDK triggers this callback when the Activity of the live room is switched to the foreground.

```java
void onLiveRoomActivityResume(Activity activity)
```


<span id="7dceabe6"></span>
### onActivityConfigurationChanged

The SDK triggers this callback when the Activity configuration of the live room changes.

```java
default void onActivityConfigurationChanged(Activity activity, Configuration configuration)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|activity |Activity |The Activity of the live room. |
|configuration |Configuration |The Activity configuration of the live room. |


<span id="b0b8afa7"></span>
### onLiveRoomActivityDestroy

The SDK triggers this callback when the Activity of the live room is destroyed.

```java
void onLiveRoomActivityDestroy(Activity activity)
```


<span id="6c0002a8"></span>
### onLiveRoomFullDestroyed

The SDK triggers this callback when both the full\-featured live room page and the floating window are destroyed.

```Java
void onLiveRoomFullDestroyed(long activityId)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|activityId |Long |The activity ID of the live room. |


<span id="3cf5a09e"></span>
### onFloatViewWillAppear

The SDK triggers this callback when the floating window is about to appear.

```Java
void onFloatViewWillAppear(long activityId)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|activityId |Long |The activity ID of the live room. |


<span id="5756eaac"></span>
### onFloatViewWillClose

The SDK triggers this callback when the floating window is about to disappear.

```Java
void onFloatViewWillClose(long activityId)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|activityId |Long |The activity ID of the live room. |


<span id="c5c188d8"></span>
### onUserForceOffline

The SDK triggers this callback when viewers are forcibly removed from the live room.

```Java
default void onUserForceOffline(
    long activityId,
    BDLForceOfflineInfo info
)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|activityId |Long |The activity ID of the live room. |
|info |BDLForceOfflineInfo |The reason for viewers being forcibly removed from the live room. For more information, see [BDLForceOfflineInfo](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#1dbc8f5b). |


<span id="38dde242"></span>
### onRoomServerCreated

The SDK triggers this callback when the `TVULiveRoomServer` instance is successfully created.

```Java
default void onRoomServerCreated(
    Activity activity,
    long activityId,
    TVULiveRoomServer roomServer
)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|activity |Activity |The Activity of the live room. |
|activityId |Long |The activity ID of the live room. |
|roomServer |TVULiveRoomServer |The `TVULiveRoomServer` instance. For more information, see [TVULiveRoomServer](https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver). |


<span id="75007939"></span>
# CustomLoginListener

The callback class for logging in to your own account system when the authentication mode is public.

```java
public interface CustomLoginListener
```


<span id="6cde84c0"></span>
## Member Functions

<span id="d3799085"></span>
### onCustomLoginStart

The callback is triggered when viewers log in to your own account system in public mode. When viewers join the live room in public mode and encounter scenarios requiring login, such as sending and liking comments, the SDK calls this callback to notify your app that viewers need to log in. You can implement the login process using your own account system.

```java
void onCustomLoginStart(Context context, long activityId, LoginStateCallBack callBack)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|context |Context |The context of the live room page. |
|activityId |long |The activity ID of the live room. |
|callBack |LoginStateCallBack |The callback class for viewer login results. |


<span id="7ae66623"></span>
# LoginStateCallBack

The callback class for viewer login results.

```java
interface LoginStateCallBack
```


<span id="71e71ad3"></span>
## Member Functions

<span id="cb937422"></span>
### onLoginFinished

The callback is triggered when the custom login of viewers is successful, fails, or is cancelled. Call this callback to notify the SDK of the viewers' login results after they log in to your custom account system.

```java
void onLoginFinished(String token)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|token |String |The user token.<br><br><br>* The custom login is successful: Pass the token in custom mode to the SDK. Call [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi) and set the value of `Mode` to `2` to get the token.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Call the <code>URLDecoder.decode</code> method to decode the token before passing it to the SDK.   </div><br>   <br><br>* The custom login fails or is cancelled: Pass the null value to the SDK. |


<span id="f36aa242"></span>
# FloatingAwardView.Listener

The callback class for the lucky draw icon.

```java
public interface Listener
```


<span id="88b93823"></span>
## Member Functions

<span id="542104ee"></span>
### onUpdateAwardIcon

The callback is triggered when the lucky draw status changes. The SDK triggers this callback to notify you to update the image when the lucky draw status changes.

```java
void onUpdateAwardIcon(ImageView icon, int awardStatus);
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|icon |ImageView |The ImageView of the lucky draw icon. |
|awardStatus |Integer |The current lucky draw status. Valid values:<br><br><br>* `2`: To be drawn.<br><br>* `4`: Already drawn. |


<span id="e6e91c48"></span>
# SinglePlayerListener

The callback class for the custom player.

```java
public interface SinglePlayerListener
```


<span id="4a494380"></span>
## Member Functions

<span id="4fd51895"></span>
### liveRoomStatusChanged

The callback is triggered when the live room status changes.

```java
public void liveRoomStatusChanged(int status);
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|status |Integer |The current live room status. Valid values:<br><br><br>* `1`: Live.<br><br>* `2`: Preview.<br><br>* `3`: Playback.<br><br>* `4`: Over. |


<span id="34593cf7"></span>
### playableStatusChanged

The callback is triggered when the playable status of resources changes.

```java
public void playableStatusChanged(int playableStatus);
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|playableStatus |Integer |The current playable status of resources. Valid values:<br><br><br>* `0`: No resources are playable, so you cannot call the `play` method.<br><br>* `1`: Video On Demand (VOD) videos (previews and playbacks) are playable. You can call the `play` method to play the videos.<br><br>* `2`: A live stream is playable. You can call the `play` method to play the video. |


<span id="92ab6a3c"></span>
### playStatusChanged

The callback is triggered when the play status changes.

```java
public void playStatusChanged(int playStatus);
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|playStatus |Integer |The current play status. Valid values:<br><br><br>* `0`: Paused.<br><br>* `1`: Playing. |


<span id="2aa8d521"></span>
### sizeChanged

The callback is triggered when the video size changes.

```java
public void sizeChanged(int width, int height);
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|width |Integer |The width of the video. |
|height |Integer |The height of the video. |


<span id="fefcc7ad"></span>
### stallingStatusChanged

The callback is triggered when the stuttering status changes. You can configure whether to display the custom loading animation.

```java
public void stallingStatusChanged(boolean isStalling);
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|isStalling |Boolean |Whether the video is stuttering. Valid values:<br><br><br>* `true`: Stuttering.<br><br>* `false`: Not stuttering. |


<span id="fc35530f"></span>
### vodErrorOccurred

The callback is triggered when a VOD error occurs.

```java
public void vodErrorOccurred(Error error);
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|error |Error |Error details. |


<span id="041bc3f0"></span>
### liveErrorOccurred

The callback is triggered when a live error occurs.

```Java
public void liveErrorOccurred(VeLivePlayerError error);
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|error |VeLivePlayerError |Error details. |


<span id="819befab"></span>
### playErrorStatusChanged

The callback is triggered when a play error occurs, including VOD and live error. During this time, the video is paused. You can configure a retry screen to guide viewers to tap retry.

```java
public void playErrorStatusChanged(boolean isPlayError);
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|isPlayError |Boolean |Whether a play error occurs. Valid values:<br><br><br>* `true`: A play error occurs.<br><br>* `false`: No play error occurs. |


<span id="0a0d7921"></span>
### vodPrepared

The callback is triggered when the VOD video is ready. You can call the [seekVodTime](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview#73d37e7d) method.

```java
public void vodPrepared();
```


<span id="ca9ab641"></span>
### vodRenderStarted

The callback is triggered when the VOD video rendering starts.

```java
public void vodRenderStarted();
```


<span id="4a7ee808"></span>
### vodCurPlayTimeChanged

The callback is triggered when the playback progress of the VOD video changes. The playback progress is updated every second.

```java
public void vodCurPlayTimeChanged(int curTimeInMills);
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|curTimeInMills |Integer |The current playback progress. Unit: ms. |


<span id="f472f1bf"></span>
### vodDurationChanged

The callback is triggered when the total duration of the VOD video changes. This callback is usually triggered when the video switches.

```java
public void vodDurationChanged(int durationInMills);
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|durationInMills |Integer |The total duration of the video. Unit: ms. |


<span id="18cb3692"></span>
### vodCompletion

The callback is triggered when the VOD video finishes playing.

```java
public void vodCompletion();
```


<span id="1f4cd3a3"></span>
### livePrepared

The callback is triggered when the live stream is ready.

```java
public void livePrepared();
```


<span id="bd867a69"></span>
### liveFirstFrameRendered

The callback is triggered when the live stream rendering starts.

```java
public void liveFirstFrameRendered(boolean isFirstFrame);
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|isFirstFrame |Boolean |Whether this is the first frame actually being rendered. This callback may be triggered multiple times due to retries during the live stream. Valid values:<br><br><br>* `true`: This is the first frame after calling the `play` method.<br><br>* `false`: This is not the first frame after calling the play method. |


<span id="840688f4"></span>
### liveCompletion

The callback is triggered when the live stream ends.

```java
public void liveCompletion();
```


<span id="f67b4cd1"></span>
### coverImageVisibleChanged

The callback is triggered when the visibility status of the cover changes. The cover is not visible when the video is playing, and is visible when no video is playing.

```java
public void coverImageVisibleChanged(boolean isVisible);
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|isVisible |Boolean |Whether the cover is visible. Valid values:<br><br><br>* `true`: Visible.<br><br>* `false`: Not visible. |


<span id="341d0efc"></span>
### resolutionInfoChanged

The callback is triggered when video resolution information changes. This callback is usually triggered when the video switches.

```java
public void resolutionInfoChanged(String[] resolutions, String defaultResolution);
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|resolutions |String[] |The list of currently supported resolutions. |
|defaultResolution |String |The resolution selected by default. |


<span id="a36d4ef5"></span>
### vodAutoSeekPreviousTime

The callback is triggered when a VOD video automatically resumes playing from the point where it stopped.

```java
public void vodAutoSeekPreviousTime(int seekTimeInMills);
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|seekTimeInMills |Integer |The position to which the video seeks after automatically resuming from where it stopped. Unit: ms. |


<span id="3028f46c"></span>
### onCurVodVidChanged

The callback for the video ID (Vid) change of the playing VOD video, which is triggered when the VOD video playing on the viewing page changes or when the live room status changes.

```Java
public void onCurVodVidChanged(String vid);
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|vid |String |The Vid of the playing VOD video. If no VOD video is playing, an empty string is returned. |


<span id="2ef10b21"></span>
### onCurReplayListChanged

The callback for the playback list change in the live room, which is triggered when playbacks are released or withdrawn or when the live room status changes.

```Java
public void onCurReplayListChanged(List<Replay> replayList);
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|replayList |List |The playback list of the live room. If the live room has no playbacks, an empty array is returned. |


<span id="f3bdbba8"></span>
### onCurLiveLineIdChanged

The callback is triggered when the live source ID changes.

```Java
public void onCurLiveLineIdChanged(long lineId);
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|lineId |Long |The ID of the current live source. If the live room is not in the Live status, 0 is returned. |


<span id="4a792eda"></span>
### onCurLiveLineListChanged

The callback is triggered when the live source list changes.

```Java
public void onCurLiveLineListChanged(List<PullStreamUrl> liveLineList);
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|liveLineList |List |The list of live sources. If the live room is not in the Live status, an empty array is returned. |


<span id="fa8bb733"></span>
### onUserForceOffline

The SDK triggers this callback when viewers are forcibly removed from the live room.

```Java
default void onUserForceOffline(BDLForceOfflineInfo info)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|info |BDLForceOfflineInfo |The reason for viewers being forcibly removed from the live room. For more information, see [BDLForceOfflineInfo](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#1dbc8f5b). |


<span id="a24195f6"></span>
# SeekCompletionListener

The callback class for redirection completion.

```java
public interface SeekCompletionListener
```


<span id="0f60d36b"></span>
## Member Functions

<span id="cb0136d3"></span>
### onCompletion

The callback is triggered when the redirection completes.

```java
void onCompletion(boolean success);
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|success |Boolean |Whether the redirection is successful. Valid values:<br><br><br>* `true`: Successful.<br><br>* `false`: Failed. |


<span id="f163f66b"></span>
# RedirectPageListener

The callback class for tapping links in the live room.

```java
public interface RedirectPageListener
```


<span id="a4b50153"></span>
## Member Functions

<span id="381d7dca"></span>
### redirectPage

The callback is triggered when a link is tapped. The SDK triggers this callback when viewers tap a URL in the live room, user nickname in the comments area, or the button to claim the voucher prize in watch time\-based lucky draws.

```java
public boolean redirectPage(Activity liveActivity, RedirectInfo redirectInfo)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|liveActivity |Activity |The Activity of the live room. |
|redirectInfo |[RedirectInfo](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#409d57b8) |The information required for redirection. |


**Return value**


|**Type** |**Description** |
|---|---|
|Boolean |Whether to intercept the SDK's default redirection behavior. Valid values:<br><br><br>* `true`: Intercept. The SDK no longer executes the default redirection behavior.<br><br>* `false`: Do not intercept. The SDK continues to execute the default redirection behavior. |


<span id="7929f65e"></span>
# ITVUMultipleDrawableListener

The callback class for custom icon array.

```java
public interface ITVUMultipleDrawableListener
```


<span id="ec10210c"></span>
## Member Functions

<span id="7a06025a"></span>
### onGetMultipleDrawable

The callback for custom icon array. The SDK calls this callback when it requires an array of icons. You need to implement this callback yourself and return an array of custom icons.

```java
Drawable[] onGetMultipleDrawable()
```


**Return value**


|**Type** |**Description** |
|---|---|
|Drawable[] |The array of your custom icons. |


<span id="379862a5"></span>
# FloatViewActionListener

The callback class for floating window tap events.

```java
public interface FloatViewActionListener
```


<span id="6fbb289b"></span>
## Member Functions

<span id="78dcedeb"></span>
### onClickFloatView

The SDK triggers this callback when viewers tap the floating window.

```java
boolean onClickFloatView(long activityId)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|activityId |Long |The activity ID of the live room. |


**Return value**


|**Type** |**Description** |
|---|---|
|Boolean |Whether to intercept the default tap behavior. Valid values:<br><br><br>* `true`: Intercept. The SDK no longer executes the default tap behavior.<br><br>* `false`: Do not intercept. The SDK continues to execute the default tap behavior.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The default tap behavior is to close the floating window and return to the full\-featured live room.</div><br> |


<span id="944561e9"></span>
### onClickFloatViewExitBtn

The SDK triggers this callback when viewers tap the close icon of the floating window.

```java
boolean onClickFloatViewExitBtn(long activityId)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|activityId |Long |The activity ID of the live room. |


**Return value**


|**Type** |**Description** |
|---|---|
|Boolean |Whether to intercept the default tap behavior. Valid values:<br><br><br>* `true`: Intercept. The SDK no longer executes the default tap behavior.<br><br>* `false`: Do not intercept. The SDK continues to execute the default tap behavior.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The default tap behavior is to close the floating window.</div><br> |


<span id="1d31736d"></span>
# LiveRoomActionListener

The callback class for live room operation events.

```java
public interface LiveRoomActionListener
```


<span id="c653b8ff"></span>
## Member Functions

<span id="f195449a"></span>
### onClickExitLiveRoom

The SDK triggers this callback when viewers tap the exit button or the physical back button to exit the full\-featured live room.

```java
boolean onClickExitLiveRoom(Activity activity,long activityId)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|activity |Activity |The Activity of the live room. |
|activityId |Long |The activity ID of the live room. |


**Return value**


|**Type** |**Description** |
|---|---|
|Boolean |Whether to intercept the default tap behavior. Valid values:<br><br><br>* `true`: Intercept. The SDK no longer executes the default tap behavior.<br><br>* `false`: Do not intercept. The SDK continues to execute the default tap behavior.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The default tap behavior is to exit the full\-featured live room. If a live or VOD video is playing and the floating window permission is enabled on mobile devices, the floating window is displayed upon exiting the full\-featured live room.</div><br> |


<span id="2a6e0df9"></span>
# ShareListener

The callback class for share icon tap events in the full\-featured live room.

```Java
public interface ShareListener
```


<span id="10db4675"></span>
## **Member Functions**

<span id="9615229e"></span>
### **onShare**

The SDK triggers this callback and passes the shared address of the live room when viewers tap the share icon in the full\-featured live room.

```Java
boolean onShare(Context context,String shareUrl)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|context |Context |The context of the live room page. |
|shareUrl |String |The shared address of the live room. |


**Return value**


|**Type** |**Description** |
|---|---|
|Boolean |Whether to intercept the default tap behavior. Valid values:<br><br><br>* `true`: Intercept. The SDK no longer executes the default tap behavior.<br><br>* `false`: Do not intercept. The SDK continues to execute the default tap behavior.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The default tap behavior is to \*\*\*\* display the share dialog box.</div><br> |


<span id="9fb2c3e6"></span>
# ServiceApi.ResultCallback

The callback class for live room HTTP network requests.

```Java
public interface ResultCallback<T>
```


<span id="0a47bb3b"></span>
## Member Functions

<span id="930f0300"></span>
### onSuccess

The callback is triggered when the network request is successful.

```Java
void onSuccess(T data)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|data |T |The data returned by the network request. The data type is generic. |


<span id="c76a9a77"></span>
### onFailed

The callback is triggered when the network request fails.

```Java
void onFailed(int errCode, String errMsg)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|errCode |Integer |The error code of the failed network request. |
|errMsg |String |The error message of the failed network request. |


<span id="c5d14099"></span>
# CustomLanguageStringListener

The callback class for custom system text.

```Java
public interface CustomLanguageStringListener
```


<span id="8dcc1a66"></span>
## Member Functions

<span id="ff935e78"></span>
### onCustomLanguageString

The callback is triggered when the system text is displayed, and is used to customize the system text.

```Java
String onCustomLanguageString(LanguageManager.LANGUAGE language, String key, String originString)
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|language |[LanguageManager.LANGUAGE](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#fb1bfeef) |The currently selected language. |
|key |String |The key of the system text. |
|originString |String |The default system text. |


**Return value**


|**Type** |**Description** |
|---|---|
|String |The custom system text. |


<span id="2d2129c0"></span>
# ActivityBookListener

The callback class for booking the live stream.

```Java
public interface ActivityBookListener
```


<span id="80c1bb8a"></span>
## Member Functions

<span id="7eaace3f"></span>
### onBookingButtonClicked

The callback is triggered when the button to book the live stream is tapped.

```Java
boolean onBookingButtonClicked(Activity activity, ActivityBookingModel activityBookingModel, ActivityBookStateCallBack callBack);
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|activity |Activity |The Activity of the live room. |
|activityBookingModel |ActivityBookingModel |The live stream booking information. For more information, see [ActivityBookingModel](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#e49a0ba0). |
|callBack |[ActivityBookStateCallBack](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#d094029e) |After successfully creating a system calendar event on your own, you need to call this callback to notify the SDK that the viewer has booked the live stream. You can use the following sample code to change the button for booking the live stream to the booked status.<br><br>```Java```<br>```callBack.setActivityBooked();```<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the authentication mode is set to public, you can call the <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-tvuliveroom#5984565f">clearCache</a> method to clear all local cache of the SDK on the viewer's current device, thereby changing the button from the booked status to unbooked status in all live rooms of the viewer.</div><br> |


**Return value**


|**Type** |**Description** |
|---|---|
|Boolean |Whether to intercept the SDK's automatic creation of system calendar events.<br><br><br>* `true`: Intercept. You need to create the system calendar event on your own. You can call the SDK's [addCalendarEvent](https://docs.byteplus.com/docs/byteplus-livesaas/calendarutils#80157294) method to create the system calendar event, or you can use other methods to create it.<br><br>* `false`: Do not intercept. The SDK automatically creates the system calendar event.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#b29215e9">setActivityBookListener</a> method is not called, the SDK automatically creates the system calendar event.</div><br> |


<span id="6a1fd451"></span>
### onCalendarResult

The callback for the result of creating a system calendar event.

```Java
void onCalendarResult(Activity activity, ActivityBookingModel activityBookingModel, boolean isSuccess);
```


**Input Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|activity |Activity |The Activity of the live room. |
|activityBookingModel |ActivityBookingModel |The live stream booking information. For more information, see [ActivityBookingModel](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#e49a0ba0). |
|isSuccess |Boolean |Whether the system calendar event creation is successful.<br><br><br>* `true`: Successful.<br><br>* `false`: Failed. |


<span id="d094029e"></span>
# ActivityBookStateCallBack

The callback class for successful creation of custom system calendar events.

```Java
public interface ActivityBookStateCallBack
```


<span id="260f8634"></span>
## Member Functions

<span id="4348e175"></span>
### setActivityBooked

The callback is triggered when a system calendar event is created successfully. After a viewer books the live stream, you can call this callback to notify the SDK that the viewer has booked the live stream.

```Java
void setActivityBooked()
```


<span id="2c977992"></span>
# CommentCustomizeListener

The callback class for customizing comments in the live room.

```Java
public interface CommentCustomizeListener
```


<span id="f2bfd3a3"></span>
## Member Functions

<span id="8f2d4a40"></span>
### onCustomizeCommentContent

The callback is triggered after the SDK renders the content of a single comment, and is used to customize the text content or style of the comment, or to replace the emoji image.

```Java
void onCustomizeCommentContent(SingleCommentModel commentModel,
                               CommentConfigModel commentConfigModel,
                               UIConfigModel uiConfigModel,
                               LanguageManager languageManager,
                               SpannableStringBuilder spannableStringBuilder,
                               TextView textView)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|commentModel |SingleCommentModel |The data model for a single comment. For more information, see [SingleCommentModel](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#44947300). |
|commentConfigModel |CommentConfigModel |The model for comment configuration of the live room. For more information, see [CommentConfigModel](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#3e9f13cb). |
|uiConfigModel |UIConfigModel |The model for UI theme color configuration of the live room. For more information, see [UIConfigModel](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#fed59c08). |
|languageManager |LanguageManager |The language manager of the live room. For more information, see [LanguageManager](https://docs.byteplus.com/docs/byteplus-livesaas/languagemanager). |
|spannableStringBuilder |[SpannableStringBuilder](https://developer.android.com/reference/android/text/SpannableStringBuilder) |The spannableString currently set by the TextView. |
|textView |TextView |The TextView corresponding to a single comment. |


<span id="9bcb18be"></span>
# JoinResultListener

The callback class for the result of viewers joining the full\-featured live room.

```Java
public interface JoinResultListener
```


<span id="c964202e"></span>
## Member Functions

<span id="2a1db20d"></span>
### onJoinSuccess

The callback is triggered when viewers join the full\-featured live room successfully.

```Java
void onJoinSuccess()
```


<span id="81432595"></span>
### onJoinFailed

The callback is triggered when viewers fail to join the full\-featured live room.

```Java
void onJoinFailed(int errCode,String errMsg)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|errCode |Integer |The error code for viewers failing to join the full\-featured live room. |
|errMsg |String |The error message for viewers failing to join the full\-featured live room. |


<span id="192a9ac2"></span>
# PublicNickNameRegisterListener

The callback class for nickname registration results when the authentication mode of the live room is public.

```Java
public interface PublicNickNameRegisterListener
```


<span id="fc3b47d6"></span>
## Member Functions

<span id="1dd50cba"></span>
### onRegisterSuccess

The callback is triggered when the nickname registration is successful.

```Java
void onRegisterSuccess()
```


<span id="2cb3c0a1"></span>
### onRegisterFail

The callback is triggered when the nickname registration fails.

```Java
void onRegisterFail(int errorCode,String errorMsg)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|errorCode |Integer |The error code of the nickname registration failure. |
|errorMsg |String |The error message of the nickname registration failure. |


<span id="35d14b67"></span>
# BDLUserFollowListener

The callback class for the event of a viewer following the host in custom authentication mode.

```Java
public interface BDLUserFollowListener
```


<span id="8116fb89"></span>
## Member Functions

<span id="5d17bafd"></span>
### onGetUserFollowStatus

The SDK calls this method to get the viewer's follow status when the button to follow the host is displayed. You can implement the specific logic for getting the follow status within this method and return the result through the `followStatusUpdateConsumer` callback upon completion.

```Java
void onGetUserFollowStatus(
    BusinessAccountAndUserInfoModel model,
    Consumer<Boolean> followStatusUpdateConsumer
)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|model |BusinessAccountAndUserInfoModel |The information required to follow the host. For more information, see [BusinessAccountAndUserInfoModel](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#b106da4b). |
|followStatusUpdateConsumer |Consumer |The callback triggered when the viewer's follow status is obtained.<br><br>Input parameters:<br><br>`Consumer`: Whether the viewer has followed the host.<br><br><br>* `YES`: Followed.<br><br>* `NO`: Not followed. |


<span id="e1ee99bd"></span>
### onUserFollowBtnClicked

The SDK calls this method when the viewer taps the button to follow or unfollow the host. You can implement the specific logic for following or unfollowing the host within this method and return the result through the `followStatusUpdateConsumer` callback upon completion.

```Java
void onUserFollowBtnClicked(
    View followBtn,
    BusinessAccountAndUserInfoModel model,
    Consumer<Boolean> followStatusUpdateConsumer
)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|followBtn |View |The view of the button to follow or unfollow the host. |
|model |BusinessAccountAndUserInfoModel |The information required to follow the host. For more information, see [BusinessAccountAndUserInfoModel](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#b106da4b). |
|followStatusUpdateConsumer |Consumer |The callback triggered when the viewer's follow or unfollow action is completed.<br><br>Input parameters:<br><br>`Consumer`: The viewer's latest follow status.<br><br><br>* `YES`: Followed.<br><br>* `NO`: Not followed. |


<span id="e2b06336"></span>
# CommentEditingListener

The callback class for intercepting events in the comment text box.

```Java
public interface CommentEditingListener
```


<span id="c4805154"></span>
## Member Functions

<span id="6cc8bcc5"></span>
### commentShouldInterceptEditing

When the viewer taps the comment text box and the keyboard is about to pop up, the SDK triggers this callback.

```Java
boolean commentShouldInterceptEditing(
    Activity activity,
    CommentUserModel model
)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|activity |Activity |The Activity of the live room. |
|model |CommentUserModel |Information required to determine whether to intercept the keyboard popup. For more information, see [CommentUserModel](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#fdd8e1fe). |


**Return value**

Whether to intercept the keyboard popup.


* `true`: Intercept, which means the keyboard will not pop up.

* `false`: Do not intercept, which means the keyboard will pop up.
