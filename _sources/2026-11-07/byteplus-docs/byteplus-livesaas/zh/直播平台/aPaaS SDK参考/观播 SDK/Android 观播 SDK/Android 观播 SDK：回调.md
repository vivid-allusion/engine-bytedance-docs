---
title: "Android 观播 SDK：回调"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-callback-the-viewer-sdk-for-android-zh-CN"
---

<span id="1b64c86a"></span>
# ITVULiveRoomServerListener

用于监听`TVULiveRoomServer`实例的回调类。你可以在这些回调中执行相关操作。

```java
public interface ITVULiveRoomServerListener
```


<span id="ea8f5e50"></span>
## 成员函数

<span id="cf15da79"></span>
### onGetRoomDataSuccess

调用`TVULiveRoomServer.start`方法并成功从服务器获取数据后，会触发此回调。

```java
public void onGetRoomDataSuccess(ActivityResult activityResult)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|activityResult |ActivityResult |从服务器返回的直播间数据。 |


<span id="21848038"></span>
### onGetRoomDataFailed

调用`TVULiveRoomServer.start`方法但未能从服务器获取数据后，会触发此回调。

```java
public void onGetRoomDataFailed(int errCode, String errMsg)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|errCode |Integer |错误码。可选值：<br><br><br>* `0`：ERR_BAD_DATA：表示解析服务器返回的数据时发生错误。<br><br>* `1`：ERR_LIMITED_ROOM：表示直播间在移动端不可用。 |
|errMsg |String |失败原因。 |


<span id="1a5686b7"></span>
### onFullScreenChange #{#onFullScreenChange}#

当点击全屏或退出全屏图标时，会触发此回调。你可以在此回调中更改播放器方向、显示或隐藏状态栏等。

```java
public void onFullScreenChange()
```


<span id="9d3283d8"></span>
### liveRoomStatusChange

当直播间状态发生变化时触发此回调。

```java
public void liveRoomStatusChange(int value)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|value |Integer |当前直播间状态。有效值：<br><br><br>* `1`：直播。<br><br>* `2`：预告。<br><br>* `3`：回放。<br><br>* `4`：结束。 |


<span id="f623e692"></span>
### playerStatusChange

当回放状态发生变化时，会触发此回调。

```java
public void playerStatusChange(int playerStatus)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|playerStatus |Integer |当前播放状态。有效值：<br><br><br>* `0`：暂停。<br><br>* `1`：播放中。 |


<span id="ce5cdb18"></span>
### onSpeedButtonDidTouch

当点击回放速度按钮时，会触发此回调。

```java
public void onSpeedButtonDidTouch()
```


<span id="d097dcd1"></span>
### onReplayButtonDidTouch

当点击回放按钮时，会触发此回调。

```java
public void onReplayButtonDidTouch()
```


<span id="19c591f5"></span>
### onUserForceOffline

当观众被强制移出直播间时，SDK 会触发该回调。

```Java
default void onUserForceOffline(BDLForceOfflineInfo info)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|info |BDLForceOfflineInfo |观众被强制移出直播间的原因。更多信息，请参见[BDLForceOfflineInfo](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#1dbc8f5b)。 |


<span id="76956141"></span>
# **LanguageListener**

用于点击切换语言图标的回调类。

```java
public interface LanguageListener
```


<span id="b9baba94"></span>
## 成员函数

<span id="5567f191"></span>
### onSelectLanguage

当观众点击切换语言图标时，会触发此回调。

```java
void onSelectLanguage(Activity activity,
                          ArrayList<LanguageManager.LANGUAGE> languages,
                          LanguageManager.LANGUAGE curLanguage,
                          SelectLanguageCallBack callBack)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|activity |Activity |直播间的 Activity。 |
|languages |ArrayList<[LanguageManager.LANGUAGE](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#fb1bfeef)\> |当前支持的语言列表。 |
|curLanguage |[LanguageManager.LANGUAGE](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#fb1bfeef) |当前选中的语言。 |
|callBack |SelectLanguageCallBack |语言选择的回调类。 |


<span id="d55d6f65"></span>
# SelectLanguageCallBack

语言选择的回调类。

```java
interface SelectLanguageCallBack
```


<span id="82521414"></span>
## 成员函数

<span id="9c55fd73"></span>
### onLanguageSelected

当选择语言时，会触发此回调。你可以在应用中自定义语言选择对话框，观众选择语言后，调用此回调通知 SDK 切换语言。

```java
void onLanguageSelected(LanguageManager.LANGUAGE language)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|language |[LanguageManager.LANGUAGE](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#fb1bfeef) |要切换的语言。 |


<span id="1c2e9aff"></span>
# LiveRoomStatusListener

用于直播间页面生命周期的回调类。

```java
public interface LiveRoomStatusListener
```


<span id="98742e98"></span>
## 成员函数

<span id="4da8af42"></span>
### onLiveRoomActivityCreate

当直播间的 Activity 创建时，会触发此回调。

```java
void onLiveRoomActivityCreate(Activity activity)
```


<span id="cfe9163a"></span>
### onLandLiveRoomBindingAvailable

当横屏模式直播间页面的`ViewBinding`实例初始化时，会触发此回调。SDK 触发此回调后，你可以使用获取到的`ViewBinding`实例按需修改横屏模式直播间页面的布局和图标。

```java
default void onLandLiveRoomBindingAvailable(TvuLivePlayerLayoutBinding binding, LanguageManager languageManager)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|binding |TvuLivePlayerLayoutBinding |直播间页面的`ViewBinding`实例。 |
|languageManager |LanguageManager |语言管理器。 |


<span id="cc008fd8"></span>
### onPortraitLiveRoomBindingAvailable

当竖屏模式直播间页面的`ViewBinding`实例初始化时，会触发此回调。SDK 触发此回调后，你可以使用获取到的`ViewBinding`实例按需修改竖屏模式直播间页面的布局和图标。

```Java
default void onPortraitLiveRoomBindingAvailable(TvuPortraitLiveRoomLayoutBinding binding, LanguageManager languageManager) {}
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|binding |TvuPortraitLiveRoomLayoutBinding |直播间页面的`ViewBinding`实例。 |
|languageManager |LanguageManager |语言管理器。 |


<span id="c9fe1d32"></span>
### onLiveRoomActivityPause

当直播间的 Activity 切换到后台时，SDK 会触发此回调。

```java
void onLiveRoomActivityPause(Activity activity)
```


<span id="95159e09"></span>
### onLiveRoomActivityResume

当直播间的 Activity 切换到前台时，SDK 会触发此回调。

```java
void onLiveRoomActivityResume(Activity activity)
```


<span id="7dceabe6"></span>
### onActivityConfigurationChanged

当直播间的 Activity 配置发生变化时，SDK 会触发此回调。

```java
default void onActivityConfigurationChanged(Activity activity, Configuration configuration)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|activity |Activity |直播间的 Activity。 |
|configuration |Configuration |直播间的 Activity 配置。 |


<span id="b0b8afa7"></span>
### onLiveRoomActivityDestroy

当直播间的 Activity 被销毁时，SDK 会触发此回调。

```java
void onLiveRoomActivityDestroy(Activity activity)
```


<span id="6c0002a8"></span>
### onLiveRoomFullDestroyed

当完整直播间页面和悬浮窗均被销毁时，SDK 会触发此回调。

```Java
void onLiveRoomFullDestroyed(long activityId)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|activityId |Long |直播间的活动 ID。 |


<span id="3cf5a09e"></span>
### onFloatViewWillAppear

当悬浮窗即将出现时，SDK 会触发此回调。

```Java
void onFloatViewWillAppear(long activityId)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|activityId |Long |直播间的活动 ID。 |


<span id="5756eaac"></span>
### onFloatViewWillClose

当悬浮窗即将消失时，SDK 会触发此回调。

```Java
void onFloatViewWillClose(long activityId)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|activityId |Long |直播间的活动 ID。 |


<span id="c5c188d8"></span>
### onUserForceOffline

当观众被强制移出直播间时，SDK 会触发该回调。

```Java
default void onUserForceOffline(
    long activityId,
    BDLForceOfflineInfo info
)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|activityId |Long |直播间的活动 ID。 |
|info |BDLForceOfflineInfo |观众被强制移出直播间的原因。更多信息，请参见[BDLForceOfflineInfo](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#1dbc8f5b)。 |


<span id="38dde242"></span>
### onRoomServerCreated

当`TVULiveRoomServer`实例成功创建时，SDK会触发此回调。

```Java
default void onRoomServerCreated(
    Activity activity,
    long activityId,
    TVULiveRoomServer roomServer
)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|activity |Activity |直播间的 Activity。 |
|activityId |Long |直播间的活动 ID。 |
|roomServer |TVULiveRoomServer |`TVULiveRoomServer`实例。更多信息，请参见[TVULiveRoomServer](https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-CN)。 |


<span id="75007939"></span>
# CustomLoginListener

当认证模式为公开时，用于登录自有账号系统的监听器。

```java
public interface CustomLoginListener
```


<span id="6cde84c0"></span>
## 成员函数

<span id="d3799085"></span>
### onCustomLoginStart

当观众在公开模式下登录自有账号系统时触发此回调。观众在公开模式下加入直播间并遇到需要登录的场景（如发送评论、点赞评论）时，SDK会调用此回调通知你的应用观众需要登录。你可以使用自有账号系统实现登录流程。

```java
void onCustomLoginStart(Context context, long activityId, LoginStateCallBack callBack)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|context |Context |直播间页面的上下文。 |
|activityId |long |直播间的活动 ID。 |
|callBack |LoginStateCallBack |观众登录结果的回调类。 |


<span id="7ae66623"></span>
# LoginStateCallBack

观众登录结果的回调类。

```java
interface LoginStateCallBack
```


<span id="71e71ad3"></span>
## 成员函数

<span id="cb937422"></span>
### onLoginFinished

当观众自定义登录尝试成功、失败或取消后，触发此回调。观众通过自有账号系统登录后，调用此回调通知SDK观众的登录结果。

```java
void onLoginFinished(String token)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|token |String |用户 token。<br><br><br>* 自定义登录成功：在自定义模式下将 token 传递给 SDK。调用[GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-CN)，并将`Mode`的值设置为`2`以获取 token。<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">调用<code>URLDecoder.decode</code>方法对 token 进行解码后再传递给 SDK。   </div><br>   <br><br>* 自定义登录失败或被取消：将 null 值传递给 SDK。 |


<span id="f36aa242"></span>
# FloatingAwardView.Listener

用于抽奖图标的监听器。

```java
public interface Listener
```


<span id="88b93823"></span>
## 成员函数

<span id="542104ee"></span>
### onUpdateAwardIcon

当抽奖状态发生变化时触发此回调，提示你更新图标图片。

```java
void onUpdateAwardIcon(ImageView icon, int awardStatus);
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|icon |ImageView |抽奖图标的 ImageView。 |
|awardStatus |Integer |当前抽奖状态。有效值：<br><br><br>* `2`：待抽奖。<br><br>* `4`：已抽奖。 |


<span id="e6e91c48"></span>
# SinglePlayerListener

用于独立播放器的监听器。

```java
public interface SinglePlayerListener
```


<span id="4a494380"></span>
## 成员函数

<span id="4fd51895"></span>
### liveRoomStatusChanged

当直播间状态发生变化时触发此回调。

```java
public void liveRoomStatusChanged(int status);
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|status |Integer |当前直播间状态。有效值：<br><br><br>* `1`：直播。<br><br>* `2`：预告。<br><br>* `3`：回放。<br><br>* `4`：结束。 |


<span id="34593cf7"></span>
### playableStatusChanged

当资源可播放状态发生变化时触发此回调。

```java
public void playableStatusChanged(int playableStatus);
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|playableStatus |Integer |当前资源可播放状态。有效值：<br><br><br>* `0`：无可播放资源，无法调用`play`方法。<br><br>* `1`：点播视频（预告和回放）可播放。可调用`play`方法播放视频。<br><br>* `2`：直播流可播放。可调用`play`方法播放视频。 |


<span id="92ab6a3c"></span>
### playStatusChanged

当播放状态发生变化时触发此回调。

```java
public void playStatusChanged(int playStatus);
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|playStatus |Integer |当前播放状态。有效值：<br><br><br>* `0`：暂停。<br><br>* `1`：播放中。 |


<span id="2aa8d521"></span>
### sizeChanged

当视频尺寸发生变化时触发此回调。

```java
public void sizeChanged(int width, int height);
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|width |Integer |视频宽度。 |
|height |Integer |视频高度。 |


<span id="fefcc7ad"></span>
### stallingStatusChanged

当卡顿状态发生变化时触发此回调。你可以配置是否显示自定义加载动画。

```java
public void stallingStatusChanged(boolean isStalling);
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|isStalling |Boolean |视频是否卡顿。有效值：<br><br><br>* `true`：卡顿。<br><br>* `false`：不卡顿。 |


<span id="fc35530f"></span>
### vodErrorOccurred

当回放发生错误时触发此回调。

```java
public void vodErrorOccurred(Error error);
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|error |Error |错误详情。 |


<span id="041bc3f0"></span>
### liveErrorOccurred

当直播发生错误时触发此回调。

```Java
public void liveErrorOccurred(VeLivePlayerError error);
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|error |VeLivePlayerError |错误详情。 |


<span id="819befab"></span>
### playErrorStatusChanged

当播放发生错误（包括回放和直播错误）时触发此回调。此时视频会暂停。你可以配置重试界面，提示观众点击重试按钮。

```java
public void playErrorStatusChanged(boolean isPlayError);
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|isPlayError |Boolean |是否发生播放错误。有效值：<br><br><br>* `true`：发生播放错误。<br><br>* `false`：未发生播放错误。 |


<span id="0a0d7921"></span>
### vodPrepared

当回放视频准备就绪时触发此回调。你可以调用[seekVodTime](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-CN#73d37e7d)方法。

```java
public void vodPrepared();
```


<span id="ca9ab641"></span>
### vodRenderStarted

当回放视频渲染开始时触发此回调。

```java
public void vodRenderStarted();
```


<span id="4a7ee808"></span>
### vodCurPlayTimeChanged

当回放视频的播放进度发生变化时触发此回调。播放进度每秒更新一次。

```java
public void vodCurPlayTimeChanged(int curTimeInMills);
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|curTimeInMills |Integer |当前播放进度。单位：ms。 |


<span id="f472f1bf"></span>
### vodDurationChanged

当回放视频总时长发生变化时触发此回调。通常在视频切换时触发此回调。

```java
public void vodDurationChanged(int durationInMills);
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|durationInMills |Integer |视频总时长。单位：ms。 |


<span id="18cb3692"></span>
### vodCompletion

当回放视频播放结束时触发此回调。

```java
public void vodCompletion();
```


<span id="1f4cd3a3"></span>
### livePrepared

当直播流准备就绪时触发此回调。

```java
public void livePrepared();
```


<span id="bd867a69"></span>
### liveFirstFrameRendered

当直播流渲染开始时触发此回调。

```java
public void liveFirstFrameRendered(boolean isFirstFrame);
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|isFirstFrame |Boolean |是否实际渲染的第一帧。由于直播流重试，该回调可能会被触发多次。有效值：<br><br><br>* `true`：调用`play`方法后的第一帧。<br><br>* `false`：调用play方法后不是第一帧。 |


<span id="840688f4"></span>
### liveCompletion

当直播流结束时触发此回调。

```java
public void liveCompletion();
```


<span id="f67b4cd1"></span>
### coverImageVisibleChanged

当封面可见状态发生变化时触发此回调。只有在未播放视频时封面才可见。

```java
public void coverImageVisibleChanged(boolean isVisible);
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|isVisible |Boolean |封面是否可见。有效值：<br><br><br>* `true`：可见。<br><br>* `false`：不可见。 |


<span id="341d0efc"></span>
### resolutionInfoChanged

当视频分辨率信息发生变化时触发此回调。通常在视频切换时触发此回调。

```java
public void resolutionInfoChanged(String[] resolutions, String defaultResolution);
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|resolutions |String[] |当前支持的分辨率列表。 |
|defaultResolution |String |默认选中的分辨率。 |


<span id="a36d4ef5"></span>
### vodAutoSeekPreviousTime

当点播视频自动从停止的位置恢复播放时，会触发该回调。

```java
public void vodAutoSeekPreviousTime(int seekTimeInMills);
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|seekTimeInMills |Integer |视频自动恢复播放后跳转到的位置。单位：ms。 |


<span id="3028f46c"></span>
### onCurVodVidChanged

当当前播放的点播视频的视频 ID（Vid）发生变化时，会触发该回调。此情况可能发生在观看页上的点播视频更换，或直播间状态发生变化时。

```Java
public void onCurVodVidChanged(String vid);
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|vid |String |正在播放的点播视频的 Vid。若未播放点播视频，则返回空字符串。 |


<span id="2ef10b21"></span>
### onCurReplayListChanged

当直播间中的回放列表发生变化时，会触发该回调。此情况可能发生在回放发布或撤回，或直播间状态发生变化时。

```Java
public void onCurReplayListChanged(List<Replay> replayList);
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|replayList |List |直播间的回放列表。若直播间无回放，则返回空列表。 |


<span id="f3bdbba8"></span>
### onCurLiveLineIdChanged

当直播源 ID 发生变化时，会触发该回调。

```Java
public void onCurLiveLineIdChanged(long lineId);
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|lineId |Long |当前直播源的 ID。若直播间不处于直播状态，则返回 0。 |


<span id="4a792eda"></span>
### onCurLiveLineListChanged

当直播源列表发生变化时，会触发该回调。

```Java
public void onCurLiveLineListChanged(List<PullStreamUrl> liveLineList);
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|liveLineList |List |直播源列表。若直播间不处于直播状态，则返回空列表。 |


<span id="fa8bb733"></span>
### onUserForceOffline

当观众被强制移出直播间时，SDK 会触发该回调。

```Java
default void onUserForceOffline(BDLForceOfflineInfo info)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|info |BDLForceOfflineInfo |观众被强制移出直播间的原因。更多信息请参见[BDLForceOfflineInfo](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#1dbc8f5b)。 |


<span id="a24195f6"></span>
# SeekCompletionListener

重定向完成的回调类。

```java
public interface SeekCompletionListener
```


<span id="0f60d36b"></span>
## 成员函数

<span id="cb0136d3"></span>
### onCompletion

当重定向完成时，会触发该回调。

```java
void onCompletion(boolean success);
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|success |Boolean |重定向是否成功。有效值：<br><br><br>* `true`：成功。<br><br>* `false`：失败。 |


<span id="f163f66b"></span>
# RedirectPageListener

直播间内链接点击的回调类。

```java
public interface RedirectPageListener
```


<span id="a4b50153"></span>
## 成员函数

<span id="381d7dca"></span>
### redirectPage

当链接被点击时，会触发该回调。当观众在直播间点击 URL、评论区用户昵称，或在观看时长抽奖中点击领取奖券按钮时，SDK 会触发该回调。

```java
public boolean redirectPage(Activity liveActivity, RedirectInfo redirectInfo)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|liveActivity |Activity |直播间的 Activity。 |
|redirectInfo |[RedirectInfo](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#409d57b8) |重定向所需的信息。 |


**返回值**


|**类型** |**接口行为** |
|---|---|
|Boolean |是否拦截 SDK 默认的重定向行为。有效值：<br><br><br>* `true`：拦截。SDK 不再执行默认重定向行为。<br><br>* `false`：不拦截。SDK 继续执行默认重定向行为。 |


<span id="7929f65e"></span>
# ITVUMultipleDrawableListener

自定义图标数组的回调类。

```java
public interface ITVUMultipleDrawableListener
```


<span id="ec10210c"></span>
## 成员函数

<span id="7a06025a"></span>
### onGetMultipleDrawable

在 SDK 需要时，实现该回调以提供自定义图标数组。

```java
Drawable[] onGetMultipleDrawable()
```


**返回值**


|**类型** |**接口行为** |
|---|---|
|Drawable[] |自定义图标数组。 |


<span id="379862a5"></span>
# FloatViewActionListener

悬浮窗点击事件的回调类。

```java
public interface FloatViewActionListener
```


<span id="6fbb289b"></span>
## 成员函数

<span id="78dcedeb"></span>
### onClickFloatView

当观众点击悬浮窗时，SDK 会触发该回调。

```java
boolean onClickFloatView(long activityId)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|activityId |Long |直播间的活动 ID。 |


**返回值**


|**类型** |**接口行为** |
|---|---|
|Boolean |是否拦截默认点击行为。有效值：<br><br><br>* `true`：拦截。SDK 不再执行默认点击行为。<br><br>* `false`：不拦截。SDK 继续执行默认点击行为。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">默认点击行为为关闭悬浮窗并返回完整直播间。</div><br> |


<span id="944561e9"></span>
### onClickFloatViewExitBtn

当观众点击悬浮窗的关闭图标时，SDK 会触发该回调。

```java
boolean onClickFloatViewExitBtn(long activityId)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|activityId |Long |直播间的活动 ID。 |


**返回值**


|**类型** |**接口行为** |
|---|---|
|Boolean |是否拦截默认点击行为。有效值：<br><br><br>* `true`：拦截。SDK 不再执行默认点击行为。<br><br>* `false`：不拦截。SDK 继续执行默认点击行为。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">默认点击行为为关闭悬浮窗。</div><br> |


<span id="1d31736d"></span>
# LiveRoomActionListener

直播间操作事件的回调类。

```java
public interface LiveRoomActionListener
```


<span id="c653b8ff"></span>
## 成员函数

<span id="f195449a"></span>
### onClickExitLiveRoom

当观众点击退出按钮或实体返回键退出完整直播间时，SDK 会触发该回调。

```java
boolean onClickExitLiveRoom(Activity activity,long activityId)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|activity |Activity |直播间的 Activity。 |
|activityId |Long |直播间的活动 ID。 |


**返回值**


|**类型** |**接口行为** |
|---|---|
|Boolean |是否拦截默认点击行为。有效值：<br><br><br>* `true`：拦截。SDK 不再执行默认点击行为。<br><br>* `false`：不拦截。SDK 继续执行默认点击行为。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">默认点击行为为退出完整直播间。若正在播放直播或点播视频，且移动设备已开启悬浮窗权限，则退出完整直播间时会显示悬浮窗。</div><br> |


<span id="2a6e0df9"></span>
# ShareListener

完整直播间分享图标点击事件的回调类。

```Java
public interface ShareListener
```


<span id="10db4675"></span>
## **成员函数**

<span id="9615229e"></span>
### **onShare**

当观众在完整直播间点击分享图标时，SDK 会触发该回调并传递直播间的分享地址。

```Java
boolean onShare(Context context,String shareUrl)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|context |Context |直播间页面的上下文。 |
|shareUrl |String |直播间的分享地址。 |


**返回值**


|**类型** |**接口行为** |
|---|---|
|Boolean |是否拦截默认点击行为。有效值：<br><br><br>* `true`：拦截。SDK 不再执行默认点击行为。<br><br>* `false`：不拦截。SDK 继续执行默认点击行为。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">默认点击行为为弹出分享对话框。</div><br> |


<span id="9fb2c3e6"></span>
# ServiceApi.ResultCallback

直播间 HTTP 网络请求的回调类。

```Java
public interface ResultCallback<T>
```


<span id="0a47bb3b"></span>
## 成员函数

<span id="930f0300"></span>
### onSuccess

当网络请求成功时，会触发该回调。

```Java
void onSuccess(T data)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|data |T |网络请求返回的数据。数据类型为泛型。 |


<span id="c76a9a77"></span>
### onFailed

当网络请求失败时，会触发该回调。

```Java
void onFailed(int errCode, String errMsg)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|errCode |Integer |网络请求失败的错误码。 |
|errMsg |String |网络请求失败的错误信息。 |


<span id="c5d14099"></span>
# CustomLanguageStringListener

自定义系统文本的回调类。

```Java
public interface CustomLanguageStringListener
```


<span id="8dcc1a66"></span>
## 成员函数

<span id="ff935e78"></span>
### onCustomLanguageString

当系统文本显示时，会触发该回调，用于自定义系统文本。

```Java
String onCustomLanguageString(LanguageManager.LANGUAGE language, String key, String originString)
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|language |[LanguageManager.LANGUAGE](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#fb1bfeef) |当前选中的语言。 |
|key |String |系统文本的 key。 |
|originString |String |系统文本的默认值。 |


**返回值**


|**类型** |**接口行为** |
|---|---|
|String |自定义系统文本。 |


<span id="2d2129c0"></span>
# ActivityBookListener

直播流预约的回调类。

```Java
public interface ActivityBookListener
```


<span id="80c1bb8a"></span>
## 成员函数

<span id="7eaace3f"></span>
### onBookingButtonClicked

当点击预约直播流按钮时，会触发该回调。

```Java
boolean onBookingButtonClicked(Activity activity, ActivityBookingModel activityBookingModel, ActivityBookStateCallBack callBack);
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|activity |Activity |直播间的 Activity。 |
|activityBookingModel |ActivityBookingModel |直播流预约信息。更多信息，请参见 [ActivityBookingModel](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#e49a0ba0)。 |
|callBack |[ActivityBookStateCallBack](https://docs.byteplus.com/docs/byteplus-livesaas/docs-callback-the-viewer-sdk-for-android-zh-CN#d094029e) |成功创建系统日历事件后，必须调用此 callBack 对象的 setActivityBooked() 方法，通知 SDK 观众已预约直播流。可使用以下示例代码将直播流预约按钮更改为已预约状态。<br><br>```Java```<br>```callBack.setActivityBooked();```<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">当认证模式设置为公开时，可调用<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-tvuliveroom-zh-CN#5984565f">clearCache</a>方法清除观众当前设备上 SDK 的所有本地缓存，从而将所有直播间中的按钮状态由已预约变为未预约。</div><br> |


**返回值**


|**类型** |**接口行为** |
|---|---|
|Boolean |是否拦截 SDK 自动创建系统日历事件。<br><br><br>* `true`：拦截。需要自行创建系统日历事件。可以调用 SDK 的 [addCalendarEvent](https://docs.byteplus.com/docs/byteplus-livesaas/calendarutils-zh-CN#80157294) 方法创建系统日历事件，也可以通过其他方式创建。<br><br>* `false`：不拦截。SDK 自动创建系统日历事件。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若未调用<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#b29215e9">setActivityBookListener</a>方法，SDK 会自动创建系统日历事件。</div><br> |


<span id="6a1fd451"></span>
### onCalendarResult

创建系统日历事件结果的回调。

```Java
void onCalendarResult(Activity activity, ActivityBookingModel activityBookingModel, boolean isSuccess);
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|activity |Activity |直播间的 Activity。 |
|activityBookingModel |ActivityBookingModel |直播流预约信息。更多信息，请参见 [ActivityBookingModel](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#e49a0ba0)。 |
|isSuccess |Boolean |系统日历事件创建是否成功。<br><br><br>* `true`：成功。<br><br>* `false`：失败。 |


<span id="d094029e"></span>
# ActivityBookStateCallBack

自定义系统日历事件创建成功的回调类。

```Java
public interface ActivityBookStateCallBack
```


<span id="260f8634"></span>
## 成员函数

<span id="4348e175"></span>
### setActivityBooked

当系统日历事件创建成功时，会触发该回调。当观众预约直播流后，可以调用该回调通知 SDK 观众已预约该直播流。

```Java
void setActivityBooked()
```


<span id="2c977992"></span>
# CommentCustomizeListener

用于自定义直播间评论的回调类。

```Java
public interface CommentCustomizeListener
```


<span id="f2bfd3a3"></span>
## 成员函数

<span id="8f2d4a40"></span>
### onCustomizeCommentContent

SDK 渲染单条评论内容后会触发该回调，用于自定义评论的文本内容或样式，或替换表情图片。

```Java
void onCustomizeCommentContent(SingleCommentModel commentModel,
                               CommentConfigModel commentConfigModel,
                               UIConfigModel uiConfigModel,
                               LanguageManager languageManager,
                               SpannableStringBuilder spannableStringBuilder,
                               TextView textView)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|commentModel |SingleCommentModel |单条评论的数据模型。更多信息，请参见 [SingleCommentModel](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#44947300)。 |
|commentConfigModel |CommentConfigModel |直播间评论配置模型。更多信息，请参见 [CommentConfigModel](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#3e9f13cb)。 |
|uiConfigModel |UIConfigModel |直播间 UI 主题色配置模型。更多信息，请参见 [UIConfigModel](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#fed59c08)。 |
|languageManager |LanguageManager |直播间语言管理器。更多信息，请参见 [LanguageManager](https://docs.byteplus.com/docs/byteplus-livesaas/languagemanager-zh-CN)。 |
|spannableStringBuilder |[SpannableStringBuilder](https://developer.android.com/reference/android/text/SpannableStringBuilder) |TextView 当前设置的 spannableString。 |
|textView |TextView |对应单条评论的 TextView。 |


<span id="9bcb18be"></span>
# JoinResultListener

用于观众加入完整直播间结果的回调类。

```Java
public interface JoinResultListener
```


<span id="c964202e"></span>
## 成员函数

<span id="2a1db20d"></span>
### onJoinSuccess

当观众成功加入完整直播间时会触发该回调。

```Java
void onJoinSuccess()
```


<span id="81432595"></span>
### onJoinFailed

当观众加入完整直播间失败时会触发该回调。

```Java
void onJoinFailed(int errCode,String errMsg)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|errCode |Integer |观众加入完整直播间失败的错误码。 |
|errMsg |String |观众加入完整直播间失败的错误信息。 |


<span id="192a9ac2"></span>
# PublicNickNameRegisterListener

当直播间认证模式为公开时，昵称注册结果的回调类。

```Java
public interface PublicNickNameRegisterListener
```


<span id="fc3b47d6"></span>
## 成员函数

<span id="1dd50cba"></span>
### onRegisterSuccess

昵称注册成功时会触发该回调。

```Java
void onRegisterSuccess()
```


<span id="2cb3c0a1"></span>
### onRegisterFail

昵称注册失败时会触发该回调。

```Java
void onRegisterFail(int errorCode,String errorMsg)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|errorCode |Integer |昵称注册失败的错误码。 |
|errorMsg |String |昵称注册失败的错误信息。 |


<span id="35d14b67"></span>
# BDLUserFollowListener

用于处理自定义认证模式下观众关注主播事件的回调监听器。

```Java
public interface BDLUserFollowListener
```


<span id="8116fb89"></span>
## 成员函数

<span id="5d17bafd"></span>
### onGetUserFollowStatus

当显示关注主播按钮时，SDK 会调用此方法获取观众的关注状态。可以在该方法内实现获取关注状态的具体逻辑，并在完成后通过`followStatusUpdateConsumer`回调返回结果。

```Java
void onGetUserFollowStatus(
    BusinessAccountAndUserInfoModel model,
    Consumer<Boolean> followStatusUpdateConsumer
)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|model |BusinessAccountAndUserInfoModel |关注主播所需的信息。更多信息，请参见 [BusinessAccountAndUserInfoModel](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#b106da4b)。 |
|followStatusUpdateConsumer |Consumer |获取观众关注状态时触发的回调。<br><br>输入参数：<br><br>`Consumer`：观众是否已关注主播。<br><br><br>* `YES`：已遵循。<br><br>* `NO`：未遵循。 |


<span id="e1ee99bd"></span>
### onUserFollowBtnClicked

当观众点击关注或取消关注主播按钮时，SDK 会调用此方法。可以在该方法内实现关注或取消关注主播的具体逻辑，并在完成后通过`followStatusUpdateConsumer`回调返回结果。

```Java
void onUserFollowBtnClicked(
    View followBtn,
    BusinessAccountAndUserInfoModel model,
    Consumer<Boolean> followStatusUpdateConsumer
)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|followBtn |View |关注或取消关注主播按钮的视图。 |
|model |BusinessAccountAndUserInfoModel |关注主播所需的信息。更多信息，请参见 [BusinessAccountAndUserInfoModel](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#b106da4b)。 |
|followStatusUpdateConsumer |Consumer |观众完成关注或取消关注操作时触发的回调。<br><br>输入参数：<br><br>`Consumer`：观众最新的关注状态。<br><br><br>* `YES`：已遵循。<br><br>* `NO`：未遵循。 |


<span id="e2b06336"></span>
# CommentEditingListener

用于拦截评论输入框事件的回调类。

```Java
public interface CommentEditingListener
```


<span id="c4805154"></span>
## 成员函数

<span id="6cc8bcc5"></span>
### commentShouldInterceptEditing

当观众点击评论输入框且键盘即将弹出时，SDK 会触发该回调。

```Java
boolean commentShouldInterceptEditing(
    Activity activity,
    CommentUserModel model
)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|activity |Activity |直播间的 Activity。 |
|model |CommentUserModel |用于判断是否拦截键盘弹窗所需的信息。更多信息，请参见[CommentUserModel](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#fdd8e1fe)。 |


**返回值**

是否拦截键盘弹出。


* `true`：拦截，即键盘不会弹出。

* `false`：不拦截，即键盘会弹出。


<span id="bf6382ae"></span>
# ShopCardDataListener

用于店铺卡片数据更新的回调类。

```java
public interface ShopCardDataListener
```


<span id="2dabce86"></span>
## 成员函数

<span id="2b1f118c"></span>
### onFloatingShopCardDataChanged

当浮动店铺卡片数据发生变化时会触发该回调。

```java
void onFloatingShopCardDataChanged(List<Product> shopCardItemModels);
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|shopCardItemModels |List<[Product](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#0f642632)\> |悬浮窗店铺卡片项列表。 |


<span id="bf5a0e31"></span>
### onShopCardListDataChanged

当店铺卡片列表数据发生变化时会触发该回调。

```Java
void onShopCardListDataChanged(Map<String, ProductV2> shopCardDatamap);
```


**输入参数**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|shopCardDatamap |Map<String, ProductV2\> |店铺卡片数据映射表，其中键为菜单 ID，值为对应的店铺卡片数据。 |


&nbsp;
