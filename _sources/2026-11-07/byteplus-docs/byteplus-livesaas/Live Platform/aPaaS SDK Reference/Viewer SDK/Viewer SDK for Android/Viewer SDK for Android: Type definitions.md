---
title: "Viewer SDK for Android: Type definitions"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions"
---

<span id="5a425a3d"></span>
## TVURoomAuthMode

The authentication mode of the live room.

```java
public enum TVULiveRoom.TVURoomAuthMode
```


**Enumerated Value**


|Type |Value |Description |
|---|---|---|
|PUBLIC |1 |Public mode: Viewers join the live room as guests, and must enter their nicknames to complete guest registration in scenarios where user information is required, such as tapping the comment text box and liking comments. |
|CUSTOM |2 |Custom mode: Viewers join the live room using their user information in your app, thus they can directly perform operations such as sending and liking comments. |


<span id="142a3b71"></span>
## InitConfig

The initialization configuration of the custom player.

```java
public class InitConfig {
    public SinglePlayerListener singlePlayerListener;
    public PlayConfig playConfig = new PlayConfig();
}
```


**Member Property**


|**Name** |**Type** |**Description** |
|---|---|---|
|singlePlayerListener |[SinglePlayerListener](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#e6e91c48) |The callback class for the custom player. |
|playConfig |[PlayConfig](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#3a0c75f8) |The playback configuration. |


<span id="3a0c75f8"></span>
## PlayConfig

The playback configuration.

```java
public class PlayConfig {
    public boolean isLiveAutoPlay = true;
    public boolean isForeShowAutoPlay = true;
    public boolean isPlayBackAutoPlay = true;
    public boolean isForeShowLoop = true;
    public boolean isPlayBackLoop =true;
}
```


**Member Property**


|**Name** |**Type** |**Description** |
|---|---|---|
|isLiveAutoPlay |Boolean |Whether the live stream plays automatically. Default value: `true`. Valid values:<br><br><br>* `true`: Play automatically.<br><br>* `false`: Do not play automatically. |
|isForeShowAutoPlay |Boolean |Whether the preview plays automatically. Default value: `true`. Valid values:<br><br><br>* `true`: Play automatically.<br><br>* `false`: Do not play automatically. |
|isPlayBackAutoPlay |Boolean |Whether the playback plays automatically. Default value: `true`. Valid values:<br><br><br>* `true`: Play automatically.<br><br>* `false`: Do not play automatically. |
|isForeShowLoop |Boolean |Whether the preview loops automatically. Default value: `true`. Valid values:<br><br><br>* `true`: Loop automatically.<br><br>* `false`: Do not loop automatically. |
|isPlayBackLoop |Boolean |Whether the playback loops automatically. Default value: `true`. Valid values:<br><br><br>* `true`: Loop automatically.<br><br>* `false`: Do not loop automatically. |


<span id="409d57b8"></span>
## RedirectInfo

The information required for redirection.

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


**Member Property**


|**Name** |**Type** |**Description** |
|---|---|---|
|entrance |String |The entry of tap events.<br><br><br>* `bannerAdvertisement`: Tap in\-page ads.<br><br>* `floatingShoppingCard`: Tap product cards under the menu or floating product cards.<br><br>* `businessAccount`: Tap the avatar or name of host accounts.<br><br>* `floatingAdvertisement`: Tap floating ads.<br><br>* `commentLink`: Tap URLs in comments.<br><br>* `commentAvatar`: Tap user avatar in the comment area.<br><br>* `commentContent`: Tap comment content in the comment area.<br><br>* `headerAdvertisement`: Tap header ads.<br><br>* `commentNickName`: Tap user nicknames in the comment area.<br><br>* `taskAwardTicket`: Tap the button to claim the voucher prize in watch time\-based lucky draws. |
|contentType |Integer |The content type.<br><br><br>* `CONTENT_TYPE_URL(1)`: Used for redirection upon tapping URLs. The `urlRedirectInfo` field cannot be empty.<br><br>* `CONTENT_TYPE_COMMENT(2)`: Used for redirection upon tapping the user nickname, user avatar, or comment content in the comment area. The `commentModel` field cannot be empty.<br><br>* `CONTENT_TYPE_TASK_AWARD_TICKET_URL(3)`: Used for redirection upon tapping the button to claim the voucher prize in watch time\-based lucky draws. The `taskAwardTicketInfo` field cannot be empty. |
|urlRedirectInfo |[UrlRedirectInfo](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#9348dd7b) |The information required for redirection upon tapping the URL. This field is not empty when the value of `contentType` is `1`. |
|commentModel |[SingleCommentModel](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#44947300) |The information required for redirection upon tapping the user nickname, user avatar, or comment content in the comment area. This field is not empty when the value of `contentType` is `2`. |
|product |[Product](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#0f642632) |The product information required for redirection upon tapping product cards under the menu or floating product cards. This field is not empty when the value of `entrance` is `floatingShoppingCard`. |
|taskAwardTicketInfo |[TaskAwardTicketInfo](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#b5ba89b9) |The information required for redirection upon tapping the button to claim the voucher prize in watch time\-based lucky draws. This field is not empty when the value of `contentType` is `3`. |


<span id="9348dd7b"></span>
## UrlRedirectInfo

The information required for redirection upon tapping the URL.

```java
public class UrlRedirectInfo {
    private final String url;
    private final boolean enableFloating;
}
```


**Member Property**


|**Name** |**Type** |**Description** |
|---|---|---|
|url |String |The embedded link set in the BytePlus Live console. |
|enableFloating |Boolean |Whether the content is set to display on a floating page in the BytePlus Live console.<br><br><br>* `true`: Display content on a floating page in the live room.<br><br>* `false`: Display content on a new page. |


<span id="44947300"></span>
## SingleCommentModel

The data model for a single comment.

```java
public class SingleCommentModel extends BaseObservable {
    protected final String mNickname;
    protected String externalUserId = null;
    protected final String mContent;
    protected final boolean mIsPresenter;
    protected final long mMsgId;
}
```


**Member Property**


|**Name** |**Type** |**Description** |
|---|---|---|
|mNickname |String |The nickname of the user who sent the comment. |
|externalUserId |String |The external user ID of the user who sent the comment. The ID is the `UserIdStr` passed when calling [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi). |
|mContent |String |The comment content. |
|mIsPresenter |Boolean |Whether the user who sent the comment is the host. Valid values:<br><br><br>* `true`: The host.<br><br>* `false`: Not the host. |
|mMsgId |Long |The comment ID. |


<span id="0f642632"></span>
## Product

The product information required for redirection upon tapping product cards under the menu or floating product cards.

```Java
public class Product {}
```


**Member Property**


|**Name** |**Type** |**Description** |
|---|---|---|
|Title |String |The product name. |
|Highlight |String |The retail price. |
|Strikethrough |String |The list price. |
|Remark |String |The product description. |
|IntroduceImage |String |The URL of the product image. |
|RedirectImage |String |The URL of the button image. |


<span id="b5ba89b9"></span>
## TaskAwardTicketInfo

The information required for redirection upon tapping the button to claim the voucher prize in watch time\-based lucky draws.

```Java
public class TaskAwardTicketInfo{}
```


**Member Property**


|**Name** |**Type** |**Description** |
|---|---|---|
|ticketUrl |String |The link to the claim prize page. |
|taskAwardRule |[TaskAwardRule](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#4e734a5e) |The prize information for watch time\-based lucky draws. |


<span id="4e734a5e"></span>
## TaskAwardRule

The prize information for watch time\-based lucky draws.

```Java
public class TaskAwardRule {}
```


**Member Property**


|**Name** |**Type** |**Description** |
|---|---|---|
|AwardItemName |String |The prize name. |
|AwardItemIcon |String |The URL of the prize image. |
|TaskAwardItemId |String |The prize ID. |


<span id="e4a2c940"></span>
## SimpleLayoutParams

The custom position of the view.

```Java
public class SimpleLayoutParams {
    private int gravity;
    private int marginLeftDp;
    private int marginRightDp;
    private int marginTopDp;
    private int marginBottomDp;
}
```


**Member Property**


|**Name** |**Type** |Description |
|---|---|---|
|gravity |Integer |Defines the position and alignment of the view in its parent layout. For specific values, see [android.view.Gravity](https://developer.android.com/reference/android/view/Gravity). |
|marginLeftDp |Integer |The left margin of the view from its parent layout. Unit: dp. |
|marginRightDp |Integer |The right margin of the view from its parent layout. Unit: dp. |
|marginTopDp |Integer |The top margin of the view from its parent layout. Unit: dp. |
|marginBottomDp |Integer |The bottom margin of the view from its parent layout. Unit: dp. |


<span id="38b050a5"></span>
## CustomSize

The custom size of the view.

```Java
public class CustomSize {
    private int widthDp;
    private int heightDp;
}
```


**Member Property**


|**Name** |**Type** |Description |
|---|---|---|
|widthDp |Integer |The width of the view. Unit: dp. |
|heightDp |Integer |The height of the view. Unit: dp. |


<span id="d9f238b6"></span>
## PortraitLiveRoomBottomBarLayout.BottomBar

The icons at the bottom of the live room in portrait mode.

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


**Enumerated Value**


|Type |Value |Description |
|---|---|---|
|IMAGE_TEXT_ICON |"imageTextIcon" |The icon of the menu for graphics. |
|INTERACT_TOOL_MENU |"interactToolMenu" |The icon of the menu for interaction tools. |
|SHOPPING_CARD_MENU |"shoppingCardMenu" |The icon of the menu for product cards. |
|EMBEDDEDWEB_URLS |"embeddedWebUrls" |The icon of the menu for embedded link. |
|PORTRAIT_THUMB |"portraitThumb" |The icon for liking the live room. |


<span id="e6c92fb5"></span>
## SendCommentResult

The result after a comment is sent successfully.

```Java
public class SendCommentResult {
    private String H5MsgId;
    private String Nickname;
}
```


**Member Property**


|**Name** |**Type** |**Description** |
|---|---|---|
|H5MsgId |String |The comment ID. |
|Nickname |String |The nickname of the user who sent the comment. |


<span id="00d8c2a4"></span>
## Error

The error class for failed responses from the server to live room network requests.

```Java
public class Error {
    private String Code;
    private String Message;
}
```


**Member Property**


|**Name** |**Type** |**Description** |
|---|---|---|
|Code |String |The error code. |
|Message |String |The error message. |


<span id="f1af4dc5"></span>
## ResponseMetadata

The general description of live room network requests.

```Java
public class ResponseMetadata {
    private String RequestId;
    private long SystemTime;
    private Error Error;
}    
```


**Member Property**


|**Name** |**Type** |**Description** |
|---|---|---|
|RequestId |String |The unique ID of the network request, used by the server to identify the request. |
|SystemTime |Long |The server system time in Unix timestamp when the network request is returned. Unit: seconds. |
|Error |Error |The error class for failed network requests returned by the server. For more information, see [Error](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#00d8c2a4).<br><br><br>* If `Error` is empty: The server returns the result normally, and the request is successful.<br><br>* If `Error` is not empty: The server rejects the request or an internal error occurs, and the request fails. |


<span id="c0244d2f"></span>
## SendCommentResponse

The result returned by the server for the comment submission network request.

```Java
public class SendCommentResponse extends BaseResponse {
    private SendCommentResult Result;
    private ResponseMetadata ResponseMetadata;
}    
```


**Member Property**


|**Name** |**Type** |**Description** |
|---|---|---|
|Result |SendCommentResult |The result after a comment is sent successfully. For more information, see [SendCommentResult](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#e6c92fb5). |
|ResponseMetadata |ResponseMetadata |The general description of network requests. For more information, see [ResponseMetadata](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#f1af4dc5). |


<span id="fb1bfeef"></span>
## LanguageManager.LANGUAGE

The language type of the live room.

```Java
public enum LanguageManager.LANGUAGE 
```


**Enumerated Value**


|Type |Value |Description |
|---|---|---|
|ZH_HANS |0 |Simplified Chinese. |
|EN |1 |English. |
|JA |2 |Japanese. |
|ZH_HANT |3 |Traditional Chinese. |
|KO |4 |Korean. |
|TH |5 |Thai. |
|VI |6 |Vietnamese. |
|AR |7 |Arabic. |
|TR |8 |Turkish. |
|ES |9 |Spanish. |
|ID |10 |Indonesian |
|PT |11 |Portuguese. |
|RU |12 |Russian. |


<span id="e49a0ba0"></span>
## ActivityBookingModel

The live stream booking information.

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


**Member Property**


|**Name** |**Type** |**Description** |
|---|---|---|
|activityName |String |The name of the live room. |
|activityId |Long |The activity ID of the live room. |
|startTimeMillis |Long |The start time of the live stream in Unix timestamp format. Unit: ms. |
|endTimeMillis |Long |The end time of the live stream in Unix timestamp format. Unit: ms. |
|nickName |String |The nickname of the viewer.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The parameter has a value only when the viewer enters the nickname or logs in to the live room.</div><br> |
|externalUserId |String |The unique identifier of the viewer on a third\-party platform.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The parameter has a value only when the authentication mode is custom and the viewer logs in to the live room.</div><br> |
|userId |Long |The user ID, which is the unique identifier in BytePlus Live of the viewer.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The value is <code>0</code> if the viewer does not enter a nickname or does not log in to the live room.</div><br> |


<span id="56a27a1b"></span>
## BDThemeIconModel

The button information.

```Java
public class BDThemeIconModel {
    private Drawable lightModeIcon;
    private Drawable darkModeIcon;
}
```


**Member Property**


|**Name** |**Type** |**Description** |
|---|---|---|
|lightModeIcon |Drawable |The button used if the theme is not dark mode. |
|darkModeIcon |Drawable |The button used if the theme is dark mode. |


<span id="3e9f13cb"></span>
## CommentConfigModel

The model for comment configuration of the live room.

```Java
public class CommentConfigModel extends BaseObservable {
    private boolean commentSendEnable;
    private boolean commentTranslateEnable;
}
```


**Member Property**


|**Name** |**Type** |**Description** |
|---|---|---|
|commentSendEnable |Boolean |Whether to allow viewers to send comments.<br><br><br>* `true`: Allow.<br><br>* `false`: Do not allow. |
|commentTranslateEnable |Boolean |Whether to enable comment translation.<br><br><br>* `true`: Enable.<br><br>* `false`: Disable. |


<span id="fed59c08"></span>
## UIConfigModel

The model for UI theme color configuration of the live room.

```Java
public class UIConfigModel extends BaseObservable {
    private int commentFontColor;
    private int hostCommentColor;
    private boolean isLightTheme;
}
```


**Member Property**


|**Name** |**Type** |**Description** |
|---|---|---|
|commentFontColor |Integer |The color of comments sent by users other than the host. |
|hostCommentColor |Integer |The color of comments sent by the host. |
|isLightTheme |Boolean |Whether the theme of the live room is not dark mode.<br><br><br>* `true`: Not dark mode.<br><br>* `false`: Dark mode. |


<span id="4530ad0e"></span>
## JoinRoomConfig

The configurations required to join the full\-featured live room.

```Java
public class JoinRoomConfig {
    public long activityId;
    public String token;
    public boolean isPortraitLiveRoom;
    public TVULiveRoom.TVURoomAuthMode authMode;
    public JoinResultListener joinResultListener;
  }
```


**Member Property**


|Name |Type |Description |
|---|---|---|
|activityId |Long |The activity ID of the live room to join. You can get the ID by calling [CreateActivityAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2) or [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |
|token |String |The authorization token required to join the live room. You can get the token by calling [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi). |
|isPortraitLiveRoom |Boolean |Whether the live room is in portrait mode.<br><br><br>* `true`: In portrait mode.<br><br>* `false`: In landscape mode. |
|authMode |TVURoomAuthMode |The authentication mode of the live room, including `PUBLIC` and `CUSTOM` modes. Which one to choose depends on the value of the `Mode` parameter passed when you call [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi).<br><br><br>* `PUBLIC`: Set to this mode when the value of `Mode` is `1`. Viewers join the live room as guests, and must enter their nicknames to complete guest registration in scenarios where user information is required, such as tapping the comment text box and liking comments.<br><br>* `CUSTOM`: Set to this mode when the value of `Mode` is `2`. Viewers join the live room using their user information in your app, thus they can directly perform operations such as sending and liking comments. |
|joinResultListener |JoinResultListener |The callback class for the result of joining the live room. The parameter can be set to null. For more information, see [JoinResultListener](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#9bcb18be). |


<span id="7321845b"></span>
## BDLForceOfflineReason

Reasons for viewers being forcibly removed from the live room.

```Java
public enum BDLForceOfflineReason
```


**Enumerated Value**


|Type |Value |Description |
|---|---|---|
|BDLiveForceOfflineReasonMultiLogin |0 |After the repeated login prevention feature is enabled, the same viewer logs in to the same live room on multiple devices simultaneously. |
|BDLiveForceOfflineReasonUnCheckIn |1 |Timeout due to not checking in. |
|BDLiveForceOfflineReasonIPBanned |2 |IP address banned. |
|BDLiveForceOfflineReasonKickOut |3 |Kicked out. |


<span id="b106da4b"></span>
## BusinessAccountAndUserInfoModel

The information required to follow the host.

```Java
public class BusinessAccountAndUserInfoModel {
    private long activityId;
    private String externalId;
    private String externalName;
    private long hostAccountId;
    private String hostAccountName;
  }
```


**Member Property**


|Name |Type |Description |
|---|---|---|
|activityId |Long |The activity ID of the live room. |
|externalId |String |The external user ID, which is the unique identifier for viewers on third\-party platforms. This ID is the `UserIdStr` parameter passed when calling [GetSDKTokenAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getsdktokenapi). |
|externalName |String |The viewer's nickname, which is the `Nickname` parameter passed when calling [GetSDKTokenAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getsdktokenapi). |
|hostAccountId |Long |The host account ID. |
|hostAccountName |String |The host account name. |


<span id="fdd8e1fe"></span>
## CommentUserModel

Information required to determine whether to intercept the keyboard popup.

```Java
public class CommentUserModel {
    private long activityId;
    private String nickname;
    private String externalUserId;
    private long userId;
 }
```


**Member Property**


|Name |Type |Description |
|---|---|---|
|activityId |Long |The activity ID of the live room. |
|nickname |String |The viewer's nickname.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the viewer does not enter a nickname or does not log in to the live room, the value is <code>nil</code>.</div><br> |
|externalUserId |String |The unique identifier of the viewer on third\-party platforms.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This property has a value only when the authentication mode is custom and the viewer has logged in to the live room.</div><br> |
|userId |Long |The user ID, which is the unique identifier of the viewer in BytePlus Live.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the viewer does not enter a nickname or does not log in to the live room, the value is <code>0</code>.</div><br> |


<span id="446d9b7a"></span>
## BDLExternalReportConfiguration

Data reporting configuration.

```Java
public class BDLExternalReportConfiguration {
    private boolean enable;
    private String url;
    private int repeatInterval;
 }
```


**Member Property**


|Name |Type |Description |
|---|---|---|
|enable |Boolean |Whether to enable the data reporting feature. Default value: `false`. Valid values:<br><br><br>* `true`: Enable. The SDK will report data to the `url` at the following timing:<br><br>   * When a viewer joins the live room successfully.<br><br>   * While a viewer is in the live room, data is reported at intervals specified by `repeatInterval`.<br><br>   * When a viewer leaves the live room.<br><br>* `false`: Disable. |
|url |String |After enabling the data reporting feature through `enable`, the SDK will send a `POST` request to this URL at specific timing for data reporting. |
|repeatInterval |Integer |The time interval for reporting data. Unit: seconds. Default value: `30`. |


<span id="1dbc8f5b"></span>
## BDLForceOfflineInfo

The information for viewers being forcibly removed from the live room.

```Java
public class BDLForceOfflineInfo {
    private final BDLForceOfflineReason reason;
    private final String prompt;
 }
```


**Member Property**


|Name |Type |Description |
|---|---|---|
|reason |BDLForceOfflineReason |The reason for viewers being forcibly removed from the live room. For more information, see [BDLForceOfflineReason](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#7321845b). |
|prompt |String |The prompt text for viewers being forcibly removed from the live room. |
