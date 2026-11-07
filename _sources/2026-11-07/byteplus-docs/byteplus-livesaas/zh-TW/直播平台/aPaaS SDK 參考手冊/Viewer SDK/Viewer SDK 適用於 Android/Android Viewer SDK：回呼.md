---
title: "Android Viewer SDK：回呼"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/android-viewer-sdk-hui-hu-zh-TW"
---

<span id="1b64c86a"></span>
# ITVULiveRoomServerListener

用於監聽`TVULiveRoomServer`實例的回呼類別。你可以在這些回呼中執行相關操作。

```java
public interface ITVULiveRoomServerListener
```


<span id="ea8f5e50"></span>
## 成員函式

<span id="cf15da79"></span>
### onGetRoomDataSuccess

當呼叫`TVULiveRoomServer.start`方法並成功從伺服器取得資料後，會觸發此回呼。

```java
public void onGetRoomDataSuccess(ActivityResult activityResult)
```


**輸入參數**


|**名稱** |**型別** |**說明** |
|---|---|---|
|activityResult |ActivityResult |伺服器返回的直播間資料。 |


<span id="21848038"></span>
### onGetRoomDataFailed

當呼叫`TVULiveRoomServer.start`方法但未能從伺服器取得資料時，會觸發此回呼。

```java
public void onGetRoomDataFailed(int errCode, String errMsg)
```


**輸入參數**


|**名稱** |**型別** |**說明** |
|---|---|---|
|errCode |整數 |錯誤碼。有效值：<br><br><br>* `0`：ERR_BAD_DATA：表示解析伺服器返回資料時發生錯誤。<br><br>* `1`：ERR_LIMITED_ROOM：表示直播間在行動裝置上不可用。 |
|errMsg |字串 |失敗原因。 |


<span id="1a5686b7"></span>
### onFullScreenChange #{#onFullScreenChange}#

當點擊全螢幕或退出全螢幕圖示時，會觸發此回呼。你可以在此回呼中變更播放器方向、顯示或隱藏狀態列等操作。

```java
public void onFullScreenChange()
```


<span id="9d3283d8"></span>
### liveRoomStatusChange

當直播間狀態變更時，會觸發此回呼。

```java
public void liveRoomStatusChange(int value)
```


**輸入參數**


|**名稱** |**型別** |**說明** |
|---|---|---|
|value |整數 |目前直播間狀態。有效值：<br><br><br>* `1`：直播中。<br><br>* `2`：預覽。<br><br>* `3`：回放。<br><br>* `4`：結束。 |


<span id="f623e692"></span>
### playerStatusChange

當播放狀態變更時，會觸發此回呼。

```java
public void playerStatusChange(int playerStatus)
```


**輸入參數**


|**名稱** |**型別** |**說明** |
|---|---|---|
|playerStatus |整數 |目前播放狀態。有效值：<br><br><br>* `0`：已暫停。<br><br>* `1`：播放中。 |


<span id="ce5cdb18"></span>
### onSpeedButtonDidTouch

當點擊播放速度按鈕時，會觸發此回呼。

```java
public void onSpeedButtonDidTouch()
```


<span id="d097dcd1"></span>
### onReplayButtonDidTouch

當點擊重播按鈕時，會觸發此回呼。

```java
public void onReplayButtonDidTouch()
```


<span id="19c591f5"></span>
### onUserForceOffline

當觀眾被強制移出直播間時，SDK會觸發此回呼。

```Java
default void onUserForceOffline(BDLForceOfflineInfo info)
```


**輸入參數**


|**名稱** |**型別** |**說明** |
|---|---|---|
|info |BDLForceOfflineInfo |觀眾被強制移出直播間的原因。欲了解更多資訊，請參閱[BDLForceOfflineInfo](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#1dbc8f5b)。 |


<span id="76956141"></span>
# **LanguageListener**

用於點擊切換語言圖示的回呼類別。

```java
public interface LanguageListener
```


<span id="b9baba94"></span>
## 成員函式

<span id="5567f191"></span>
### onSelectLanguage

當觀眾點擊切換語言圖示時，會觸發此回呼。

```java
void onSelectLanguage(Activity activity,
                          ArrayList<LanguageManager.LANGUAGE> languages,
                          LanguageManager.LANGUAGE curLanguage,
                          SelectLanguageCallBack callBack)
```


**輸入參數**


|**名稱** |**型別** |**說明** |
|---|---|---|
|activity |Activity |直播間的 Activity。 |
|languages |ArrayList<[LanguageManager.LANGUAGE](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#fb1bfeef)\> |目前支援的語言列表。 |
|curLanguage |[LanguageManager.LANGUAGE](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#fb1bfeef) |目前選擇的語言。 |
|callBack |SelectLanguageCallBack |語言選擇的回呼類別。 |


<span id="d55d6f65"></span>
# SelectLanguageCallBack

用於語言選擇的回呼類別。

```java
interface SelectLanguageCallBack
```


<span id="82521414"></span>
## 成員函式

<span id="9c55fd73"></span>
### onLanguageSelected

當選擇語言時，會觸發此回呼。你可以在應用程式中自訂語言選擇對話框，觀眾選擇語言後，呼叫此回呼通知SDK切換語言。

```java
void onLanguageSelected(LanguageManager.LANGUAGE language)
```


**輸入參數**


|**名稱** |**型別** |**說明** |
|---|---|---|
|language |[LanguageManager.LANGUAGE](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#fb1bfeef) |要切換的語言。 |


<span id="1c2e9aff"></span>
# LiveRoomStatusListener

用於直播間頁面生命週期的回呼類別。

```java
public interface LiveRoomStatusListener
```


<span id="98742e98"></span>
## 成員函式

<span id="4da8af42"></span>
### onLiveRoomActivityCreate

當直播間的Activity建立時，會觸發此回呼。

```java
void onLiveRoomActivityCreate(Activity activity)
```


<span id="cfe9163a"></span>
### onLandLiveRoomBindingAvailable

當橫屏直播間頁面的`ViewBinding`實例初始化時，會觸發此回呼。SDK觸發此回呼後，你可以使用取得的`ViewBinding`實例，按需求修改橫屏直播間頁面的版面配置及圖示。

```java
default void onLandLiveRoomBindingAvailable(TvuLivePlayerLayoutBinding binding, LanguageManager languageManager)
```


**輸入參數**


|**名稱** |**型別** |**說明** |
|---|---|---|
|binding |TvuLivePlayerLayoutBinding |直播間頁面的`ViewBinding`實例。 |
|languageManager |LanguageManager |語言管理器。 |


<span id="cc008fd8"></span>
### onPortraitLiveRoomBindingAvailable

當直屏直播間頁面的`ViewBinding`實例初始化時，會觸發此回呼。SDK觸發此回呼後，你可以使用取得的`ViewBinding`實例，按需求修改直屏直播間頁面的版面配置及圖示。

```Java
default void onPortraitLiveRoomBindingAvailable(TvuPortraitLiveRoomLayoutBinding binding, LanguageManager languageManager) {}
```


**輸入參數**


|**名稱** |**型別** |**說明** |
|---|---|---|
|binding |TvuPortraitLiveRoomLayoutBinding |直播間頁面的`ViewBinding`實例。 |
|languageManager |LanguageManager |語言管理器。 |


<span id="c9fe1d32"></span>
### onLiveRoomActivityPause

當直播間的Activity切換至背景時，SDK會觸發此回呼。

```java
void onLiveRoomActivityPause(Activity activity)
```


<span id="95159e09"></span>
### onLiveRoomActivityResume

當直播間的Activity切換至前景時，SDK會觸發此回呼。

```java
void onLiveRoomActivityResume(Activity activity)
```


<span id="7dceabe6"></span>
### onActivityConfigurationChanged

當直播間的Activity組態變更時，SDK會觸發此回呼。

```java
default void onActivityConfigurationChanged(Activity activity, Configuration configuration)
```


**輸入參數**


|**名稱** |**型別** |**說明** |
|---|---|---|
|activity |Activity |直播間的 Activity。 |
|configuration |Configuration |直播間的 Activity 配置。 |


<span id="b0b8afa7"></span>
### onLiveRoomActivityDestroy

當直播間的Activity銷毀時，SDK會觸發此回呼。

```java
void onLiveRoomActivityDestroy(Activity activity)
```


<span id="6c0002a8"></span>
### onLiveRoomFullDestroyed

當完整功能直播間頁面及浮動視窗皆銷毀時，SDK會觸發此回呼。

```Java
void onLiveRoomFullDestroyed(long activityId)
```


**輸入參數**


|**名稱** |**型別** |**說明** |
|---|---|---|
|activityId |Long |直播間的活動 ID。 |


<span id="3cf5a09e"></span>
### onFloatViewWillAppear

當浮動視窗即將顯示時，SDK會觸發此回呼。

```Java
void onFloatViewWillAppear(long activityId)
```


**輸入參數**


|**名稱** |**型別** |**說明** |
|---|---|---|
|activityId |Long |直播間的活動 ID。 |


<span id="5756eaac"></span>
### onFloatViewWillClose

當浮動視窗即將關閉時，SDK會觸發此回呼。

```Java
void onFloatViewWillClose(long activityId)
```


**輸入參數**


|**名稱** |**型別** |**說明** |
|---|---|---|
|activityId |Long |直播間的活動 ID。 |


<span id="c5c188d8"></span>
### onUserForceOffline

當觀眾被強制移出直播間時，SDK會觸發此回呼。

```Java
default void onUserForceOffline(
    long activityId,
    BDLForceOfflineInfo info
)
```


**輸入參數**


|名稱 |型別 |說明 |
|---|---|---|
|activityId |Long |直播間的活動 ID。 |
|info |BDLForceOfflineInfo |觀眾被強制移出直播間的原因。欲了解更多資訊，請參閱[BDLForceOfflineInfo](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#1dbc8f5b)。 |


<span id="38dde242"></span>
### onRoomServerCreated

當 `TVULiveRoomServer` 實例成功建立時，SDK 會觸發此回調。

```Java
default void onRoomServerCreated(
    Activity activity,
    long activityId,
    TVULiveRoomServer roomServer
)
```


**輸入參數**


|名稱 |型別 |說明 |
|---|---|---|
|activity |Activity |直播間的 Activity。 |
|activityId |Long |直播間的活動 ID。 |
|roomServer |TVULiveRoomServer |`TVULiveRoomServer`實例。欲了解更多資訊，請參閱[TVULiveRoomServer](https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-TW)。 |


<span id="75007939"></span>
# CustomLoginListener

當驗證模式為公開時，用於登入自有帳號系統的回調類。

```java
public interface CustomLoginListener
```


<span id="6cde84c0"></span>
## 成員函式

<span id="d3799085"></span>
### onCustomLoginStart

當觀眾在公開模式下登入自有帳號系統時，會觸發此回調。觀眾以公開模式加入直播間並遇到需要登入的情境，例如發送或點讚評論時，SDK 會呼叫此回調通知您的應用程式觀眾需要登入。您可以使用自有帳號系統實現登入流程。

```java
void onCustomLoginStart(Context context, long activityId, LoginStateCallBack callBack)
```


**輸入參數**


|**名稱** |**型別** |**說明** |
|---|---|---|
|context |Context |直播間頁面的 context。 |
|activityId |long |直播間的活動 ID。 |
|callBack |LoginStateCallBack |觀眾登入結果的回呼類別。 |


<span id="7ae66623"></span>
# LoginStateCallBack

用於觀眾登入結果的回調類。

```java
interface LoginStateCallBack
```


<span id="71e71ad3"></span>
## 成員函式

<span id="cb937422"></span>
### onLoginFinished

觀眾自定義登入嘗試成功、失敗或取消後，會觸發此回調。觀眾登入自有帳號系統後，呼叫此回調通知 SDK 登入結果。

```java
void onLoginFinished(String token)
```


**輸入參數**


|**名稱** |**型別** |**說明** |
|---|---|---|
|token |String |使用者 token。<br><br><br>* 自訂登入成功：以自訂模式將 token 傳遞給 SDK。呼叫[GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-TW)並將`Mode`的值設為`2`以取得 token。<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">請在將 token 傳遞給 SDK 前，調用<code>URLDecoder.decode</code>方法對其進行解碼。   </div><br>   <br><br>* 自訂登入失敗或取消：將 null 傳遞給 SDK。 |


<span id="f36aa242"></span>
# FloatingAwardView.Listener

用於抽獎圖示的回調類。

```java
public interface Listener
```


<span id="88b93823"></span>
## 成員函式

<span id="542104ee"></span>
### onUpdateAwardIcon

當抽獎狀態變化時，會觸發此回調，提示您更新圖示圖片。

```java
void onUpdateAwardIcon(ImageView icon, int awardStatus);
```


**輸入參數**


|**名稱** |**型別** |**說明** |
|---|---|---|
|icon |ImageView |抽獎圖示的 ImageView。 |
|awardStatus |Integer |目前抽獎狀態。有效值：<br><br><br>* `2`：待抽獎。<br><br>* `4`：已抽獎。 |


<span id="e6e91c48"></span>
# SinglePlayerListener

用於自定義播放器的回調類。

```java
public interface SinglePlayerListener
```


<span id="4a494380"></span>
## 成員函式

<span id="4fd51895"></span>
### liveRoomStatusChanged

當直播間狀態變化時，會觸發此回調。

```java
public void liveRoomStatusChanged(int status);
```


**輸入參數**


|**名稱** |**型別** |**說明** |
|---|---|---|
|status |Integer |目前直播間狀態。有效值：<br><br><br>* `1`：直播中。<br><br>* `2`：預覽。<br><br>* `3`：回放。<br><br>* `4`：結束。 |


<span id="34593cf7"></span>
### playableStatusChanged

當資源可播放狀態變化時，會觸發此回調。

```java
public void playableStatusChanged(int playableStatus);
```


**輸入參數**


|**名稱** |**型別** |**說明** |
|---|---|---|
|playableStatus |Integer |資源目前可播放狀態。有效值：<br><br><br>* `0`：無可播放資源，無法呼叫`play`方法。<br><br>* `1`：隨選視訊（VOD）影片（預覽與回放）可播放。可呼叫`play`方法播放影片。<br><br>* `2`：直播流可播放。可呼叫`play`方法播放影片。 |


<span id="92ab6a3c"></span>
### playStatusChanged

當播放狀態變化時，會觸發此回調。

```java
public void playStatusChanged(int playStatus);
```


**輸入參數**


|**名稱** |**型別** |**說明** |
|---|---|---|
|playStatus |Integer |目前播放狀態。有效值：<br><br><br>* `0`：已暫停。<br><br>* `1`：播放中。 |


<span id="2aa8d521"></span>
### sizeChanged

當影片尺寸變化時，會觸發此回調。

```java
public void sizeChanged(int width, int height);
```


**輸入參數**


|**名稱** |**型別** |**說明** |
|---|---|---|
|width |Integer |影片寬度。 |
|height |Integer |影片高度。 |


<span id="fefcc7ad"></span>
### stallingStatusChanged

當卡頓狀態變化時，會觸發此回調。您可以設定是否顯示自定義載入動畫。

```java
public void stallingStatusChanged(boolean isStalling);
```


**輸入參數**


|**名稱** |**型別** |**說明** |
|---|---|---|
|isStalling |Boolean |影片是否卡頓。有效值：<br><br><br>* `true`：卡頓。<br><br>* `false`：未卡頓。 |


<span id="fc35530f"></span>
### vodErrorOccurred

當點播錯誤發生時，會觸發此回調。

```java
public void vodErrorOccurred(Error error);
```


**輸入參數**


|**名稱** |**型別** |**說明** |
|---|---|---|
|error |Error |錯誤詳細資訊。 |


<span id="041bc3f0"></span>
### liveErrorOccurred

當直播錯誤發生時，會觸發此回調。

```Java
public void liveErrorOccurred(VeLivePlayerError error);
```


**輸入參數**


|**名稱** |**型別** |**說明** |
|---|---|---|
|error |VeLivePlayerError |錯誤詳細資訊。 |


<span id="819befab"></span>
### playErrorStatusChanged

當播放錯誤發生時（包含點播與直播錯誤），會觸發此回調。此時影片會暫停播放。您可以設定重試畫面，提示觀眾點擊重試按鈕。

```java
public void playErrorStatusChanged(boolean isPlayError);
```


**輸入參數**


|**名稱** |**型別** |**說明** |
|---|---|---|
|isPlayError |Boolean |是否發生播放錯誤。有效值：<br><br><br>* `true`：發生播放錯誤。<br><br>* `false`：未發生播放錯誤。 |


<span id="0a0d7921"></span>
### vodPrepared

當點播影片準備完成時，會觸發此回調。您可以呼叫 [seekVodTime](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-TW#73d37e7d) 方法。

```java
public void vodPrepared();
```


<span id="ca9ab641"></span>
### vodRenderStarted

當點播影片開始渲染時，會觸發此回調。

```java
public void vodRenderStarted();
```


<span id="4a7ee808"></span>
### vodCurPlayTimeChanged

當點播影片播放進度變化時，會觸發此回調。播放進度每秒更新一次。

```java
public void vodCurPlayTimeChanged(int curTimeInMills);
```


**輸入參數**


|**名稱** |**型別** |**說明** |
|---|---|---|
|curTimeInMills |Integer |目前播放進度。單位：ms。 |


<span id="f472f1bf"></span>
### vodDurationChanged

當點播影片總時長變化時，會觸發此回調。此回調通常於影片切換時觸發。

```java
public void vodDurationChanged(int durationInMills);
```


**輸入參數**


|**名稱** |**型別** |**說明** |
|---|---|---|
|durationInMills |Integer |影片總時長。單位：ms。 |


<span id="18cb3692"></span>
### vodCompletion

當點播影片播放結束時，會觸發此回調。

```java
public void vodCompletion();
```


<span id="1f4cd3a3"></span>
### livePrepared

當直播流準備完成時，會觸發此回調。

```java
public void livePrepared();
```


<span id="bd867a69"></span>
### liveFirstFrameRendered

當直播流開始渲染時，會觸發此回調。

```java
public void liveFirstFrameRendered(boolean isFirstFrame);
```


**輸入參數**


|**名稱** |**型別** |**說明** |
|---|---|---|
|isFirstFrame |Boolean |是否實際渲染的第一幀。由於直播過程中可能重試，此回調可能會被多次觸發。有效值：<br><br><br>* `true`：調用`play`方法後的第一幀。<br><br>* `false`：調用 play 方法後不是第一幀。 |


<span id="840688f4"></span>
### liveCompletion

當直播流結束時，會觸發此回調。

```java
public void liveCompletion();
```


<span id="f67b4cd1"></span>
### coverImageVisibleChanged

當封面可見狀態變化時，會觸發此回調。封面僅在無影片播放時可見。

```java
public void coverImageVisibleChanged(boolean isVisible);
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|isVisible |Boolean |封面是否可見。有效值：<br><br><br>* `true`：可見。<br><br>* `false`：不可見。 |


<span id="341d0efc"></span>
### resolutionInfoChanged

當影片解析度資訊變化時，會觸發此回調。此回調通常於影片切換時觸發。

```java
public void resolutionInfoChanged(String[] resolutions, String defaultResolution);
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|resolutions |String[] |當前支援的解析度列表。 |
|defaultResolution |String |預設選擇的解析度。 |


<span id="a36d4ef5"></span>
### vodAutoSeekPreviousTime

當 VOD 視頻自動從停止點恢復播放時，會觸發此回調。

```java
public void vodAutoSeekPreviousTime(int seekTimeInMills);
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|seekTimeInMills |Integer |自動從停止處恢復後，影片跳轉到的位置。單位：毫秒。 |


<span id="3028f46c"></span>
### onCurVodVidChanged

當當前播放的 VOD 視頻的視頻 ID（Vid）發生變化時，會觸發此回調。這可能發生於觀看頁面的 VOD 視頻切換，或直播間狀態變化時。

```Java
public void onCurVodVidChanged(String vid);
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|vid |String |當前播放的 VOD 影片的 Vid。若未播放 VOD 影片，則返回空字串。 |


<span id="2ef10b21"></span>
### onCurReplayListChanged

當直播間的回放列表發生變化時，會觸發此回調。這可能發生於回放發布或撤回，或直播間狀態變化時。

```Java
public void onCurReplayListChanged(List<Replay> replayList);
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|replayList |List |直播間的回放列表。若直播間無回放，則返回空列表。 |


<span id="f3bdbba8"></span>
### onCurLiveLineIdChanged

當直播源 ID 發生變化時，會觸發此回調。

```Java
public void onCurLiveLineIdChanged(long lineId);
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|lineId |Long |當前直播源的 ID。若直播間非 Live 狀態，則返回 0。 |


<span id="4a792eda"></span>
### onCurLiveLineListChanged

當直播源列表發生變化時，會觸發此回調。

```Java
public void onCurLiveLineListChanged(List<PullStreamUrl> liveLineList);
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|liveLineList |List |直播源列表。若直播間非 Live 狀態，則返回空列表。 |


<span id="fa8bb733"></span>
### onUserForceOffline

當觀眾被強制移出直播間時，SDK 會觸發此回調。

```Java
default void onUserForceOffline(BDLForceOfflineInfo info)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|info |BDLForceOfflineInfo |觀眾被強制移出直播間的原因。更多資訊，請參見[BDLForceOfflineInfo](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#1dbc8f5b)。 |


<span id="a24195f6"></span>
# SeekCompletionListener

重定向完成的回調類。

```java
public interface SeekCompletionListener
```


<span id="0f60d36b"></span>
## 成員函數

<span id="cb0136d3"></span>
### onCompletion

當重定向完成時，會觸發此回調。

```java
void onCompletion(boolean success);
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|success |Boolean |跳轉是否成功。有效值：<br><br><br>* `true`：成功。<br><br>* `false`：失敗。 |


<span id="f163f66b"></span>
# RedirectPageListener

直播間內點擊鏈接的回調類。

```java
public interface RedirectPageListener
```


<span id="a4b50153"></span>
## 成員函數

<span id="381d7dca"></span>
### redirectPage

當鏈接被點擊時，會觸發此回調。當觀眾在直播間點擊 URL、評論區用戶暱稱，或在觀看時長抽獎中點擊領取券獎品按鈕時，SDK 會觸發此回調。

```java
public boolean redirectPage(Activity liveActivity, RedirectInfo redirectInfo)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|liveActivity |Activity |直播間的 Activity。 |
|redirectInfo |[RedirectInfo](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#409d57b8) |跳轉所需的資訊。 |


**返回值**


|**類型** |**說明** |
|---|---|
|Boolean |是否攔截 SDK 的預設跳轉行為。有效值：<br><br><br>* `true`：攔截。SDK 不再執行預設跳轉行為。<br><br>* `false`：不攔截。SDK 繼續執行預設跳轉行為。 |


<span id="7929f65e"></span>
# ITVUMultipleDrawableListener

自定義圖標陣列的回調類。

```java
public interface ITVUMultipleDrawableListener
```


<span id="ec10210c"></span>
## 成員函數

<span id="7a06025a"></span>
### onGetMultipleDrawable

當 SDK 需要時，實現此回調以提供自定義圖標陣列。

```java
Drawable[] onGetMultipleDrawable()
```


**返回值**


|**類型** |**說明** |
|---|---|
|Drawable[] |自訂圖示陣列。 |


<span id="379862a5"></span>
# FloatViewActionListener

浮窗點擊事件的回調類。

```java
public interface FloatViewActionListener
```


<span id="6fbb289b"></span>
## 成員函數

<span id="78dcedeb"></span>
### onClickFloatView

當觀眾點擊浮窗時，SDK 會觸發此回調。

```java
boolean onClickFloatView(long activityId)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|activityId |Long |直播間的活動 ID。 |


**返回值**


|**類型** |**說明** |
|---|---|
|Boolean |是否攔截預設點擊行為。有效值：<br><br><br>* `true`：攔截。SDK 不再執行預設點擊行為。<br><br>* `false`：不攔截。SDK 繼續執行預設點擊行為。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">預設點擊行為為關閉浮動視窗並返回全功能直播間。</div><br> |


<span id="944561e9"></span>
### onClickFloatViewExitBtn

當觀眾點擊浮窗的關閉圖標時，SDK 會觸發此回調。

```java
boolean onClickFloatViewExitBtn(long activityId)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|activityId |Long |直播間的活動 ID。 |


**返回值**


|**類型** |**說明** |
|---|---|
|Boolean |是否攔截預設點擊行為。有效值：<br><br><br>* `true`：攔截。SDK 不再執行預設點擊行為。<br><br>* `false`：不攔截。SDK 繼續執行預設點擊行為。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">預設點擊行為為關閉浮動視窗。</div><br> |


<span id="1d31736d"></span>
# LiveRoomActionListener

直播間操作事件的回調類。

```java
public interface LiveRoomActionListener
```


<span id="c653b8ff"></span>
## 成員函數

<span id="f195449a"></span>
### onClickExitLiveRoom

當觀眾點擊退出按鈕或實體返回鍵退出全功能直播間時，SDK 會觸發此回調。

```java
boolean onClickExitLiveRoom(Activity activity,long activityId)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|activity |Activity |直播間的 Activity。 |
|activityId |Long |直播間的活動 ID。 |


**返回值**


|**類型** |**說明** |
|---|---|
|Boolean |是否攔截預設點擊行為。有效值：<br><br><br>* `true`：攔截。SDK 不再執行預設點擊行為。<br><br>* `false`：不攔截。SDK 繼續執行預設點擊行為。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">預設點擊行為為退出全功能直播間。當正在播放直播或點播影片，且行動裝置已啟用浮動視窗權限時，退出全功能直播間後會顯示浮動視窗。</div><br> |


<span id="2a6e0df9"></span>
# ShareListener

全功能直播間分享圖標點擊事件的回調類。

```Java
public interface ShareListener
```


<span id="10db4675"></span>
## **成員函數**

<span id="9615229e"></span>
### **onShare**

當觀眾在全功能直播間點擊分享圖標時，SDK 會觸發此回調並傳遞直播間的分享地址。

```Java
boolean onShare(Context context,String shareUrl)
```


**輸入參數**


|**名稱** |**類型** |**說明** |
|---|---|---|
|context |Context |直播間頁面的 context。 |
|shareUrl |String |直播間的分享位址。 |


**返回值**


|**類型** |**說明** |
|---|---|
|Boolean |是否攔截預設點擊行為。有效值：<br><br><br>* `true`：攔截。SDK 不再執行預設的點擊行為。<br><br>* `false`：不攔截。SDK 繼續執行預設的點擊行為。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">預設點擊行為為顯示分享對話框。</div><br> |


<span id="9fb2c3e6"></span>
# ServiceApi.ResultCallback

直播間 HTTP 網路請求的回調類。

```Java
public interface ResultCallback<T>
```


<span id="0a47bb3b"></span>
## 成員函數

<span id="930f0300"></span>
### onSuccess

當網路請求成功時，會觸發此回調。

```Java
void onSuccess(T data)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|data |T |網路請求返回的資料。資料類型為泛型。 |


<span id="c76a9a77"></span>
### onFailed

當網路請求失敗時，會觸發此回調。

```Java
void onFailed(int errCode, String errMsg)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|errCode |Integer |網路請求失敗的錯誤碼。 |
|errMsg |String |網路請求失敗的錯誤訊息。 |


<span id="c5d14099"></span>
# CustomLanguageStringListener

自定義系統文字的回調類。

```Java
public interface CustomLanguageStringListener
```


<span id="8dcc1a66"></span>
## 成員函數

<span id="ff935e78"></span>
### onCustomLanguageString

當系統文字顯示時會觸發此回調，用於自定義系統文字。

```Java
String onCustomLanguageString(LanguageManager.LANGUAGE language, String key, String originString)
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|language |[LanguageManager.LANGUAGE](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#fb1bfeef) |目前選擇的語言。 |
|key |String |系統文字的鍵值。 |
|originString |String |預設系統文字。 |


**返回值**


|**類型** |**描述** |
|---|---|
|String |自訂系統文字。 |


<span id="2d2129c0"></span>
# ActivityBookListener

直播預約的回調類。

```Java
public interface ActivityBookListener
```


<span id="80c1bb8a"></span>
## 成員函數

<span id="7eaace3f"></span>
### onBookingButtonClicked

當預約直播按鈕被點擊時，會觸發此回調。

```Java
boolean onBookingButtonClicked(Activity activity, ActivityBookingModel activityBookingModel, ActivityBookStateCallBack callBack);
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|activity |Activity |直播間的 Activity。 |
|activityBookingModel |ActivityBookingModel |直播預約資訊。更多資訊請參見 [ActivityBookingModel](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#e49a0ba0)。 |
|callBack |[ActivityBookStateCallBack](https://docs.byteplus.com/docs/byteplus-livesaas/android-viewer-sdk-hui-hu-zh-TW#d094029e) |成功建立系統日曆事件後，必須在此 callBack 物件上呼叫 setActivityBooked() 方法，通知 SDK 觀眾已預約直播。你可以使用以下範例程式碼，將直播預約按鈕變更為已預約狀態。<br><br>```Java```<br>```callBack.setActivityBooked();```<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">當驗證模式設為公開時，可調用<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-tvuliveroom-zh-TW#5984565f">clearCache</a>方法，清除觀眾當前裝置上 SDK 的所有本地快取，從而將所有直播間中按鈕的預約狀態變更為未預約。</div><br> |


**返回值**


|**類型** |**描述** |
|---|---|
|Boolean |是否攔截 SDK 自動建立系統日曆事件。<br><br><br>* `true`：攔截。你需要自行建立系統日曆事件。你可以呼叫 SDK 的 [addCalendarEvent](https://docs.byteplus.com/docs/byteplus-livesaas/calendarutils-zh-TW#80157294) 方法建立系統日曆事件，或使用其他方式建立。<br><br>* `false`：不攔截。SDK 會自動建立系統日曆事件。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若未調用<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-TW#b29215e9">setActivityBookListener</a>方法，SDK 會自動建立系統行事曆事件。</div><br> |


<span id="6a1fd451"></span>
### onCalendarResult

創建系統日曆事件結果的回調。

```Java
void onCalendarResult(Activity activity, ActivityBookingModel activityBookingModel, boolean isSuccess);
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|activity |Activity |直播間的 Activity。 |
|activityBookingModel |ActivityBookingModel |直播預約資訊。更多資訊請參見 [ActivityBookingModel](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#e49a0ba0)。 |
|isSuccess |Boolean |系統日曆事件建立是否成功。<br><br><br>* `true`：成功。<br><br>* `false`：失敗。 |


<span id="d094029e"></span>
# ActivityBookStateCallBack

自定義系統日曆事件成功創建的回調類。

```Java
public interface ActivityBookStateCallBack
```


<span id="260f8634"></span>
## 成員函數

<span id="4348e175"></span>
### setActivityBooked

當系統日曆事件成功建立時，會觸發此回調。觀眾預約直播後，可以呼叫此回調通知 SDK 該觀眾已預約直播。

```Java
void setActivityBooked()
```


<span id="2c977992"></span>
# CommentCustomizeListener

用於自訂直播間評論的回調類。

```Java
public interface CommentCustomizeListener
```


<span id="f2bfd3a3"></span>
## 成員函式

<span id="8f2d4a40"></span>
### onCustomizeCommentContent

SDK 渲染單條評論內容後會觸發此回調，可用於自訂評論的文字內容或樣式，或替換表情圖像。

```Java
void onCustomizeCommentContent(SingleCommentModel commentModel,
                               CommentConfigModel commentConfigModel,
                               UIConfigModel uiConfigModel,
                               LanguageManager languageManager,
                               SpannableStringBuilder spannableStringBuilder,
                               TextView textView)
```


**輸入參數**


|名稱 |類型 |描述 |
|---|---|---|
|commentModel |SingleCommentModel |單條評論的資料模型。更多資訊請參見 [SingleCommentModel](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#44947300)。 |
|commentConfigModel |CommentConfigModel |直播間評論配置模型。更多資訊請參見 [CommentConfigModel](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#3e9f13cb)。 |
|uiConfigModel |UIConfigModel |直播間 UI 主題色配置模型。更多資訊請參見 [UIConfigModel](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#fed59c08)。 |
|languageManager |LanguageManager |直播間語言管理器。更多資訊請參見 [LanguageManager](https://docs.byteplus.com/docs/byteplus-livesaas/languagemanager-zh-TW)。 |
|spannableStringBuilder |[SpannableStringBuilder](https://developer.android.com/reference/android/text/SpannableStringBuilder) |TextView 目前設定的 spannableString。 |
|textView |TextView |對應單條評論的 TextView。 |


<span id="9bcb18be"></span>
# JoinResultListener

用於觀眾加入全功能直播間結果的回調類。

```Java
public interface JoinResultListener
```


<span id="c964202e"></span>
## 成員函式

<span id="2a1db20d"></span>
### onJoinSuccess

觀眾成功加入全功能直播間時會觸發此回調。

```Java
void onJoinSuccess()
```


<span id="81432595"></span>
### onJoinFailed

觀眾加入全功能直播間失敗時會觸發此回調。

```Java
void onJoinFailed(int errCode,String errMsg)
```


**輸入參數**


|名稱 |類型 |描述 |
|---|---|---|
|errCode |Integer |觀眾加入全功能直播間失敗時的錯誤碼。 |
|errMsg |String |觀眾加入全功能直播間失敗時的錯誤訊息。 |


<span id="192a9ac2"></span>
# PublicNickNameRegisterListener

直播間驗證模式為公開時，暱稱註冊結果的回調類。

```Java
public interface PublicNickNameRegisterListener
```


<span id="fc3b47d6"></span>
## 成員函式

<span id="1dd50cba"></span>
### onRegisterSuccess

暱稱註冊成功時會觸發此回調。

```Java
void onRegisterSuccess()
```


<span id="2cb3c0a1"></span>
### onRegisterFail

暱稱註冊失敗時會觸發此回調。

```Java
void onRegisterFail(int errorCode,String errorMsg)
```


**輸入參數**


|名稱 |類型 |描述 |
|---|---|---|
|errorCode |Integer |暱稱註冊失敗的錯誤碼。 |
|errorMsg |String |暱稱註冊失敗的錯誤訊息。 |


<span id="35d14b67"></span>
# BDLUserFollowListener

用於自訂驗證模式下，觀眾關注主播事件處理的回調監聽器。

```Java
public interface BDLUserFollowListener
```


<span id="8116fb89"></span>
## 成員函式

<span id="5d17bafd"></span>
### onGetUserFollowStatus

當顯示關注主播按鈕時，SDK 會呼叫此方法以獲取觀眾的關注狀態。你可以在此方法內實現獲取關注狀態的具體邏輯，完成後透過 `followStatusUpdateConsumer` 回調返回結果。

```Java
void onGetUserFollowStatus(
    BusinessAccountAndUserInfoModel model,
    Consumer<Boolean> followStatusUpdateConsumer
)
```


**輸入參數**


|名稱 |類型 |描述 |
|---|---|---|
|model |BusinessAccountAndUserInfoModel |關注主播所需的資訊。更多資訊請參見 [BusinessAccountAndUserInfoModel](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#b106da4b)。 |
|followStatusUpdateConsumer |Consumer |取得觀眾關注狀態時觸發的回呼。<br><br>輸入參數：<br><br>`Consumer`：觀眾是否已關注主播。<br><br><br>* `YES`：已關注。<br><br>* `NO`：未關注。 |


<span id="e1ee99bd"></span>
### onUserFollowBtnClicked

觀眾點擊關注或取消關注主播按鈕時，SDK 會呼叫此方法。你可以在此方法內實現關注或取消關注主播的具體邏輯，完成後透過 `followStatusUpdateConsumer` 回調返回結果。

```Java
void onUserFollowBtnClicked(
    View followBtn,
    BusinessAccountAndUserInfoModel model,
    Consumer<Boolean> followStatusUpdateConsumer
)
```


**輸入參數**


|名稱 |類型 |描述 |
|---|---|---|
|followBtn |View |關注或取消關注主播按鈕的視圖。 |
|model |BusinessAccountAndUserInfoModel |關注主播所需的資訊。更多資訊請參見 [BusinessAccountAndUserInfoModel](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#b106da4b)。 |
|followStatusUpdateConsumer |Consumer |觀眾完成關注或取消關注操作時觸發的回呼。<br><br>輸入參數：<br><br>`Consumer`：觀眾最新的關注狀態。<br><br><br>* `YES`：已關注。<br><br>* `NO`：未關注。 |


<span id="e2b06336"></span>
# CommentEditingListener

用於攔截評論輸入框事件的回調類。

```Java
public interface CommentEditingListener
```


<span id="c4805154"></span>
## 成員函式

<span id="6cc8bcc5"></span>
### commentShouldInterceptEditing

觀眾點擊評論輸入框且鍵盤即將彈出時，SDK 會觸發此回調。

```Java
boolean commentShouldInterceptEditing(
    Activity activity,
    CommentUserModel model
)
```


**輸入參數**


|名稱 |類型 |描述 |
|---|---|---|
|activity |Activity |直播間的 Activity。 |
|model |CommentUserModel |判斷是否攔截鍵盤彈窗所需的資訊。如需更多資訊，請參閱[CommentUserModel](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#fdd8e1fe)。 |


**返回值**

是否攔截鍵盤彈出。


* `true`：攔截，鍵盤不會彈出。

* `false`：不攔截，鍵盤會彈出。


<span id="bf6382ae"></span>
# ShopCardDataListener

用於商店卡片資料更新的回調類。

```java
public interface ShopCardDataListener
```


<span id="2dabce86"></span>
## 成員函式

<span id="2b1f118c"></span>
### onFloatingShopCardDataChanged

當浮動商店卡片資料變更時會觸發此回調。

```java
void onFloatingShopCardDataChanged(List<Product> shopCardItemModels);
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|shopCardItemModels |List<[Product](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#0f642632)\> |浮動商品卡片項目的列表。 |


<span id="bf5a0e31"></span>
### onShopCardListDataChanged

當商店卡片列表資料變更時會觸發此回調。

```Java
void onShopCardListDataChanged(Map<String, ProductV2> shopCardDatamap);
```


**輸入參數**


|**名稱** |**類型** |**描述** |
|---|---|---|
|shopCardDatamap |Map<String, ProductV2\> |商品卡片資料對應表，其中鍵為選單 ID，值為對應的商品卡片資料。 |


&nbsp;
