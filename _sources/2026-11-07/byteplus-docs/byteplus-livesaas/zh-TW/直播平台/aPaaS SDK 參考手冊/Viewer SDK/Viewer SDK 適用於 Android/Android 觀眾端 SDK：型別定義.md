---
title: "Android 觀眾端 SDK：型別定義"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW"
---

<span id="5a425a3d"></span>
## TVURoomAuthMode

直播間的驗證模式。

```java
public enum TVULiveRoom.TVURoomAuthMode
```


**列舉值**


|型別 |值 |描述 |
|---|---|---|
|PUBLIC |1 |公開模式：觀眾以訪客身份加入直播間，並在需要用戶資訊的場景（如點擊評論文字框、點讚評論等）必須輸入暱稱以完成訪客註冊。 |
|CUSTOM |2 |自定義模式：觀眾以你 App 的用戶資訊加入直播間，因此可直接進行評論發送、點讚等操作。 |


<span id="142a3b71"></span>
## InitConfig

自定義播放器的初始化配置。

```java
public class InitConfig {
    public SinglePlayerListener singlePlayerListener;
    public PlayConfig playConfig = new PlayConfig();
}
```


**成員屬性**


|**名稱** |**型別** |**描述** |
|---|---|---|
|singlePlayerListener |[SinglePlayerListener](https://docs.byteplus.com/docs/byteplus-livesaas/android-viewer-sdk-hui-hu-zh-TW#e6e91c48) |自定義播放器的回調類。 |
|playConfig |[PlayConfig](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#3a0c75f8) |播放配置。 |


<span id="3a0c75f8"></span>
## PlayConfig

播放配置。

```java
public class PlayConfig {
    public boolean isLiveAutoPlay = true;
    public boolean isForeShowAutoPlay = true;
    public boolean isPlayBackAutoPlay = true;
    public boolean isForeShowLoop = true;
    public boolean isPlayBackLoop =true;
}
```


**成員屬性**


|**名稱** |**型別** |**描述** |
|---|---|---|
|isLiveAutoPlay |Boolean |直播是否自動播放。預設值：`true`。有效值：<br><br><br>* `true`：自動播放。<br><br>* `false`：不自動播放。 |
|isForeShowAutoPlay |Boolean |預覽是否自動播放。預設值：`true`。有效值：<br><br><br>* `true`：自動播放。<br><br>* `false`：不自動播放。 |
|isPlayBackAutoPlay |Boolean |回放是否自動播放。預設值：`true`。有效值：<br><br><br>* `true`：自動播放。<br><br>* `false`：不自動播放。 |
|isForeShowLoop |Boolean |預覽是否自動循環播放。預設值：`true`。有效值：<br><br><br>* `true`：自動循環播放。<br><br>* `false`：不自動循環播放。 |
|isPlayBackLoop |Boolean |回放是否自動循環播放。預設值：`true`。有效值：<br><br><br>* `true`：自動循環播放。<br><br>* `false`：不要自動循環。 |


<span id="409d57b8"></span>
## RedirectInfo

重定向所需的資訊。

```java
public class RedirectInfo {
    public static final int CONTENT_TYPE_URL = 1;
    public static final int CONTENT_TYPE_COMMENT = 2;
    public static final int CONTENT_TYPE_TASK_AWARD_TICKET_URL = 3;

    private final String entrance;
    private final int contentType;
    private UrlRedirectInfo urlRedirectInfo;
    private SingleCommentModel commentModel;
    private Product product;
    private TaskAwardTicketInfo taskAwardTicketInfo;
}
```


**成員屬性**


|**名稱** |**類型** |**說明** |
|---|---|---|
|entrance |String |點擊事件的來源。<br><br><br>* `bannerAdvertisement`：點擊頁內廣告。<br><br>* `floatingShoppingCard`：點擊菜單下的商品卡片或浮動商品卡片。<br><br>* `businessAccount`：點擊主持人帳號的頭像或名稱。<br><br>* `floatingAdvertisement`：點擊浮動廣告。<br><br>* `commentLink`：點擊評論中的網址。<br><br>* `commentAvatar`：點擊評論區的用戶頭像。<br><br>* `commentContent`：點擊評論區的評論內容。<br><br>* `headerAdvertisement`：點擊標頭廣告。<br><br>* `commentNickName`：點擊評論區的用戶暱稱。<br><br>* `taskAwardTicket`：點擊觀看時長抽獎中領取券獎品的按鈕。 |
|contentType |Integer |內容類型。<br><br><br>* `CONTENT_TYPE_URL(1)`：點擊網址時用於跳轉。`urlRedirectInfo` 欄位不可為空。<br><br>* `CONTENT_TYPE_COMMENT(2)`：點擊評論區的用戶暱稱、用戶頭像或評論內容時用於跳轉。`commentModel` 欄位不可為空。<br><br>* `CONTENT_TYPE_TASK_AWARD_TICKET_URL(3)`：點擊觀看時長抽獎中領取券獎品的按鈕時用於跳轉。`taskAwardTicketInfo` 欄位不可為空。 |
|urlRedirectInfo |[UrlRedirectInfo](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#9348dd7b) |基於網址跳轉的資訊。當 `contentType` 為 `1` 時，此欄位會被填充。 |
|commentModel |[SingleCommentModel](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#44947300) |點擊評論區的用戶暱稱、用戶頭像或評論內容時所需的跳轉資訊。當 `contentType` 的值為 `2` 時，此欄位不可為空。 |
|product |[Product](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#0f642632) |點擊菜單下的商品卡片或浮動商品卡片時所需的商品資訊。當 `entrance` 的值為 `floatingShoppingCard` 時，此欄位不可為空。 |
|taskAwardTicketInfo |[TaskAwardTicketInfo](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#b5ba89b9) |點擊觀看時長抽獎中領取券獎品的按鈕時所需的跳轉資訊。當 `contentType` 的值為 `3` 時，此欄位不可為空。 |


<span id="9348dd7b"></span>
## UrlRedirectInfo

點擊 URL 進行重定向所需的資訊。

```java
public class UrlRedirectInfo {
    private final String url;
    private final boolean enableFloating;
}
```


**成員屬性**


|**名稱** |**類型** |**說明** |
|---|---|---|
|url |String |在 BytePlus Live 控制台設置的嵌入連結。 |
|enableFloating |Boolean |內容是否設置為在 BytePlus Live 控制台的浮動頁面顯示。<br><br><br>* `true`：在直播間的浮動頁面顯示內容。<br><br>* `false`：在新頁面顯示內容。 |


<span id="44947300"></span>
## SingleCommentModel

單條評論的資料模型。

```java
public class SingleCommentModel extends BaseObservable {
    protected final String mNickname;
    protected String externalUserId = null;
    protected final String mContent;
    protected final boolean mIsPresenter;
    protected final long mMsgId;
}
```


**成員屬性**


|**名稱** |**類型** |**說明** |
|---|---|---|
|mNickname |String |發送評論的用戶暱稱。 |
|externalUserId |String |發送評論的用戶的外部用戶 ID。該 ID 是在呼叫 [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-TW) 時傳入的 `UserIdStr`。 |
|mContent |String |評論內容。 |
|mIsPresenter |Boolean |發送評論的用戶是否為主持人。有效值：<br><br><br>* `true`：主持人。<br><br>* `false`：非主持人。 |
|mMsgId |Long |評論 ID。 |


<span id="0f642632"></span>
## Product

點擊菜單下的商品卡片或浮動商品卡片進行重定向所需的商品資訊。

```Java
public class Product {}
```


**成員屬性**


|**名稱** |**類型** |**說明** |
|---|---|---|
|Title |String |商品名稱。 |
|Highlight |String |零售價格。 |
|Strikethrough |String |標價。 |
|Remark |String |商品描述。 |
|IntroduceImage |String |商品圖片的網址。 |
|RedirectImage |String |按鈕圖片的網址。 |


<span id="b5ba89b9"></span>
## TaskAwardTicketInfo

在觀看時長抽獎中，點擊領取券獎品按鈕進行重定向所需的資訊。

```Java
public class TaskAwardTicketInfo{}
```


**成員屬性**


|**名稱** |**類型** |**說明** |
|---|---|---|
|ticketUrl |String |領取獎品頁面的連結。 |
|taskAwardRule |[TaskAwardRule](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#4e734a5e) |觀看時長抽獎的獎品資訊。 |


<span id="4e734a5e"></span>
## TaskAwardRule

觀看時長抽獎的獎品資訊。

```Java
public class TaskAwardRule {}
```


**成員屬性**


|**名稱** |**類型** |**說明** |
|---|---|---|
|AwardItemName |String |獎品名稱。 |
|AwardItemIcon |String |獎品圖片的網址。 |
|TaskAwardItemId |String |獎品 ID。 |


<span id="e4a2c940"></span>
## SimpleLayoutParams

視圖的自定義位置。

```Java
public class SimpleLayoutParams {
    private int gravity;
    private int marginLeftDp;
    private int marginRightDp;
    private int marginTopDp;
    private int marginBottomDp;
}
```


**成員屬性**


|**名稱** |**類型** |說明 |
|---|---|---|
|gravity |Integer |定義視圖在父佈局中的位置與對齊方式。具體值請參見 [android.view.Gravity](https://developer.android.com/reference/android/view/Gravity)。 |
|marginLeftDp |Integer |視圖距父佈局左側的邊距。單位：dp。 |
|marginRightDp |Integer |視圖相對於其父佈局的右邊距。單位：dp。 |
|marginTopDp |Integer |視圖相對於其父佈局的上邊距。單位：dp。 |
|marginBottomDp |Integer |視圖相對於其父佈局的下邊距。單位：dp。 |


<span id="38b050a5"></span>
## CustomSize

視圖的自定義尺寸。

```Java
public class CustomSize {
    private int widthDp;
    private int heightDp;
}
```


**成員屬性**


|**名稱** |**類型** |描述 |
|---|---|---|
|widthDp |Integer |視圖的寬度。單位：dp。 |
|heightDp |Integer |視圖的高度。單位：dp。 |


<span id="d9f238b6"></span>
## PortraitLiveRoomBottomBarLayout.BottomBar

直式直播間底部的圖示。

```Java
public enum BottomBar {
    IMAGE_TEXT_ICON("imageTextIcon"),
    INTERACT_TOOL_MENU("interactToolMenu"),
    SHOPPING_CARD_MENU("shoppingCardMenu"),
    EMBEDDEDWEB_URLS("embeddedWebUrls"),
    PORTRAIT_THUMB("portraitThumb");
    BottomBar(String value){
        this.value = value;
    }
    public String value;
}
```


**列舉值**


|類型 |值 |描述 |
|---|---|---|
|IMAGE_TEXT_ICON |"imageTextIcon" |圖形菜單的圖示。 |
|INTERACT_TOOL_MENU |"interactToolMenu" |互動工具菜單的圖示。 |
|SHOPPING_CARD_MENU |"shoppingCardMenu" |商品卡片菜單的圖示。 |
|EMBEDDEDWEB_URLS |"embeddedWebUrls" |嵌入連結菜單的圖示。 |
|PORTRAIT_THUMB |"portraitThumb" |直播間點讚的圖示。 |


<span id="e6c92fb5"></span>
## SendCommentResult

評論發送成功後的結果。

```Java
public class SendCommentResult {
    private String H5MsgId;
    private String Nickname;
}
```


**成員屬性**


|**名稱** |**類型** |**描述** |
|---|---|---|
|H5MsgId |String |評論 ID。 |
|Nickname |String |發送評論用戶的暱稱。 |


<span id="00d8c2a4"></span>
## Error

代表伺服器針對失敗的網路請求返回的錯誤。

```Java
public class Error {
    private String Code;
    private String Message;
}
```


**成員屬性**


|**名稱** |**類型** |**描述** |
|---|---|---|
|Code |String |錯誤碼。 |
|Message |String |錯誤訊息。 |


<span id="f1af4dc5"></span>
## ResponseMetadata

直播間網路請求的通用描述。

```Java
public class ResponseMetadata {
    private String RequestId;
    private long SystemTime;
    private Error Error;
}    
```


**成員屬性**


|**名稱** |**類型** |**描述** |
|---|---|---|
|RequestId |String |網路請求的唯一 ID，伺服器用於識別請求。 |
|SystemTime |Long |伺服器回應產生時的系統時間（以 Unix 時間戳記秒為單位）。 |
|Error |Error |伺服器返回的網路請求失敗錯誤類。更多資訊請參見[Error](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#00d8c2a4)。<br><br><br>* 若`Error`為空：伺服器正常返回結果，請求成功。<br><br>* 若`Error`不為空：伺服器拒絕請求或發生內部錯誤，請求失敗。 |


<span id="c0244d2f"></span>
## SendCommentResponse

伺服器針對評論提交網路請求返回的結果。

```Java
public class SendCommentResponse extends BaseResponse {
    private SendCommentResult Result;
    private ResponseMetadata ResponseMetadata;
}    
```


**成員屬性**


|**名稱** |**類型** |**描述** |
|---|---|---|
|Result |SendCommentResult |評論成功發送後的結果。更多資訊請參見[SendCommentResult](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#e6c92fb5)。 |
|ResponseMetadata |ResponseMetadata |網路請求的通用描述。更多資訊請參見[ResponseMetadata](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#f1af4dc5)。 |


<span id="fb1bfeef"></span>
## LanguageManager.LANGUAGE

直播間的語言類型。

```Java
public enum LanguageManager.LANGUAGE 
```


**列舉值**


|類型 |值 |描述 |
|---|---|---|
|ZH_HANS |0 |簡體中文。 |
|EN |1 |英文。 |
|JA |2 |日文。 |
|ZH_HANT |3 |繁體中文。 |
|KO |4 |韓文。 |
|TH |5 |泰文。 |
|VI |6 |越南文。 |
|AR |7 |阿拉伯文。 |
|TR |8 |土耳其文。 |
|ES |9 |西班牙文。 |
|ID |10 |印尼文 |
|PT |11 |葡萄牙文。 |
|RU |12 |俄文。 |
|TL |13 |塔加洛語。 |
|KM |14 |高棉文。 |
|LO |15 |寮文。 |
|MY |16 |緬甸文。 |
|MS |17 |馬來文。 |
|HI |18 |印地語。 |
|FR |19 |法文。 |
|DE |20 |德文。 |
|IT |21 |義大利文。 |


<span id="e49a0ba0"></span>
## ActivityBookingModel

直播預約資訊。

```Java
public class ActivityBookingModel {
    String activityName;
    long activityId;
    long startTimeMillis; 
    long endTimeMillis;
    String nickName;
    String externalUserId;
    long userId;
}
```


**成員屬性**


|**名稱** |**類型** |**描述** |
|---|---|---|
|activityName |String |直播間名稱。 |
|activityId |Long |直播間的活動 ID。 |
|startTimeMillis |Long |直播開始時間（Unix 時間戳記格式）。單位：ms。 |
|endTimeMillis |Long |直播結束時間（Unix 時間戳記格式）。單位：ms。 |
|nickName |String |externalUserId<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">僅當觀眾輸入暱稱或登入直播間時，此欄位才會有值。</div><br> |
|String |觀眾在第三方平台上的唯一識別碼。 |Long<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">僅當驗證模式為自定義且觀眾登入直播間時，該參數才有值。</div><br> |
|觀眾在 BytePlus Live 的唯一識別碼。 |名稱 |描述<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若觀眾未輸入暱稱或未登入直播間，該值為<code>0</code>。</div><br> |


<span id="56a27a1b"></span>
## BDThemeIconModel

按鈕資訊。

```Java
public class BDThemeIconModel {
    private Drawable lightModeIcon;
    private Drawable darkModeIcon;
}
```


**成員屬性**


|**lightModeIcon** |**Drawable** |**亮色模式下使用的圖示。**  |
|---|---|---|
|darkModeIcon |Drawable |暗色模式下使用的圖示。 |
|名稱 |類型 |描述 |


<span id="3e9f13cb"></span>
## CommentConfigModel

直播間評論配置模型。

```Java
public class CommentConfigModel extends BaseObservable {
    private boolean commentSendEnable;
    private boolean commentTranslateEnable;
}
```


**成員屬性**


|**commentSendEnable** |**Boolean** |**是否允許觀眾發送評論。**  |
|---|---|---|
|true：允許。 |false：不允許。 |commentTranslateEnable<br><br><br>* Boolean<br><br>* 是否啟用評論翻譯。 |
|true：啟用。 |false：停用。 |名稱<br><br><br>* 類型<br><br>* 描述 |


<span id="fed59c08"></span>
## UIConfigModel

直播間 UI 主題色配置模型。

```Java
public class UIConfigModel extends BaseObservable {
    private int commentFontColor;
    private int hostCommentColor;
    private boolean isLightTheme;
}
```


**成員屬性**


|**commentFontColor** |**Integer** |**非主播用戶發送評論的顏色。**  |
|---|---|---|
|hostCommentColor |Integer |主播發送評論的顏色。 |
|isLightTheme |整數 |主持人所發送評論的顏色。 |
|是否為亮色主題 |布林值 |指示直播間主題是否為淺色。<br><br><br>* `true`：非深色模式。<br><br>* `false`：深色模式。 |


<span id="4530ad0e"></span>
## JoinRoomConfig

加入全功能直播間所需的配置。

```Java
public class JoinRoomConfig {
    public long activityId;
    public String token;
    public boolean isPortraitLiveRoom;
    public TVULiveRoom.TVURoomAuthMode authMode;
    public JoinResultListener joinResultListener;
  }
```


**成員屬性**


|名稱 |類型 |描述 |
|---|---|---|
|activityId |Long |要加入的直播間活動 ID。可透過呼叫 [CreateActivityAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2-zh-TW) 或 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-TW) 取得此 ID。 |
|token |String |加入直播間所需的授權令牌。可透過呼叫 [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-TW) 取得此令牌。 |
|isPortraitLiveRoom |布林值 |直播間是否為直式模式。<br><br><br>* `true`：直式模式。<br><br>* `false`：橫式模式。 |
|authMode |TVURoomAuthMode |此值必須與呼叫 [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-TW) 時傳入的 `Mode` 參數值一致。<br><br><br>* `PUBLIC`：當 `Mode` 的值為 `1` 時，設為此模式。觀眾以訪客身份加入直播間，並在需要用戶資訊的場景（如點擊評論文字框、點讚評論）時，必須輸入暱稱以完成訪客註冊。<br><br>* `CUSTOM`：當 `Mode` 的值為 `2` 時，設為此模式。觀眾以您 App 的用戶資訊加入直播間，因此可直接進行發送評論、點讚等操作。 |
|joinResultListener |JoinResultListener |加入直播間結果的回調類別。此參數可設為 null。如需更多資訊，請參閱 [JoinResultListener](https://docs.byteplus.com/docs/byteplus-livesaas/android-viewer-sdk-hui-hu-zh-TW#9bcb18be)。 |


<span id="7321845b"></span>
## BDLForceOfflineReason

觀眾被強制移出直播間的原因。

```Java
public enum BDLForceOfflineReason
```


**列舉值**


|類型 |值 |描述 |
|---|---|---|
|BDLiveForceOfflineReasonMultiLogin |0 |用戶在啟用重複登入防止功能時，於多個裝置同時登入。 |
|BDLiveForceOfflineReasonUnCheckIn |1 |因未簽到而超時。 |
|BDLiveForceOfflineReasonIPBanned |2 |IP 位址被封禁。 |
|BDLiveForceOfflineReasonKickOut |3 |被踢出。 |


<span id="b106da4b"></span>
## BusinessAccountAndUserInfoModel

關注主播所需的資訊。

```Java
public class BusinessAccountAndUserInfoModel {
    private long activityId;
    private String externalId;
    private String externalName;
    private long hostAccountId;
    private String hostAccountName;
  }
```


**成員屬性**


|名稱 |類型 |描述 |
|---|---|---|
|activityId |Long |直播間活動 ID。 |
|externalId |String |外部用戶 ID，即第三方平台觀眾的唯一識別碼。此 ID 為呼叫 [GetSDKTokenAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getsdktokenapi) 時傳入的 `UserIdStr`。 |
|externalName |String |觀眾暱稱，即呼叫 [GetSDKTokenAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getsdktokenapi) 時傳入的 `Nickname` 參數。 |
|hostAccountId |Long |主辦方帳號 ID。 |
|hostAccountName |String |主辦方帳號名稱。 |


<span id="fdd8e1fe"></span>
## CommentUserModel

判斷是否攔截鍵盤彈窗所需的資訊。

```Java
public class CommentUserModel {
    private long activityId;
    private String nickname;
    private String externalUserId;
    private long userId;
 }
```


**成員屬性**


|名稱 |類型 |描述 |
|---|---|---|
|activityId |Long |直播間活動 ID。 |
|nickname |String |觀眾暱稱。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">如果觀眾尚未輸入暱稱或登入直播間，該值為 <code>null</code>。</div><br> |
|externalUserId |String |觀眾在第三方平台的唯一識別碼。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">僅當驗證模式為自定義且觀眾已登入直播間時，該屬性才有值。</div><br> |
|userId |Long |用戶 ID，即觀眾在 BytePlus Live 的唯一識別碼。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若觀眾未輸入暱稱或未登入直播間，該值為<code>0</code>。</div><br> |


<span id="446d9b7a"></span>
## BDLExternalReportConfiguration

資料上報配置。

```Java
public class BDLExternalReportConfiguration {
    private boolean enable;
    private String url;
    private int repeatInterval;
 }
```


**成員屬性**


|名稱 |類型 |描述 |
|---|---|---|
|enable |布林值 |是否啟用數據上報功能。預設值：`false`。有效值：<br><br><br>* `true`：啟用。SDK 會在以下時機將數據上報至 `url`：<br><br>   * 觀眾成功加入直播間時。<br><br>   * 觀眾在直播間期間，依 `repeatInterval` 設定的間隔上報數據。<br><br>   * 觀眾離開直播間時。<br><br>* `false`：停用。 |
|url |String |啟用此功能時，SDK 發送數據上報 POST 請求的 URL。 |
|repeatInterval |Integer |數據上報的時間間隔。單位：秒。預設值：`30`。 |


<span id="1dbc8f5b"></span>
## BDLForceOfflineInfo

觀眾被強制移出直播間的資訊。

```Java
public class BDLForceOfflineInfo {
    private final BDLForceOfflineReason reason;
    private final String prompt;
 }
```


**成員屬性**


|名稱 |類型 |描述 |
|---|---|---|
|reason |BDLForceOfflineReason |觀眾被強制移出直播間的原因。如需更多資訊，請參閱 [BDLForceOfflineReason](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#7321845b)。 |
|prompt |String |觀眾被強制移出直播間時的提示文字。 |
