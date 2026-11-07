---
title: "Android 观播 SDK：类型详情"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN"
---

<span id="5a425a3d"></span>
## TVURoomAuthMode

直播间的认证模式。

```java
public enum TVULiveRoom.TVURoomAuthMode
```


**枚举值**


|类型 |值 |接口行为 |
|---|---|---|
|PUBLIC |1 |公开模式：观众以嘉宾身份加入直播间，在需要用户信息的场景（如点击评论输入框、点赞评论）时，必须输入昵称完成嘉宾注册。 |
|CUSTOM |2 |自定义模式：观众通过应用中的用户信息加入直播间，可直接进行评论发送、点赞等操作。 |


<span id="142a3b71"></span>
## InitConfig

独立播放器的初始化配置。

```java
public class InitConfig {
    public SinglePlayerListener singlePlayerListener;
    public PlayConfig playConfig = new PlayConfig();
}
```


**成员属性**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|singlePlayerListener |[SinglePlayerListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-callback-the-viewer-sdk-for-android-zh-CN#e6e91c48) |独立播放器的回调类。 |
|playConfig |[PlayConfig](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#3a0c75f8) |回放配置。 |


<span id="3a0c75f8"></span>
## PlayConfig

回放配置。

```java
public class PlayConfig {
    public boolean isLiveAutoPlay = true;
    public boolean isForeShowAutoPlay = true;
    public boolean isPlayBackAutoPlay = true;
    public boolean isForeShowLoop = true;
    public boolean isPlayBackLoop =true;
}
```


**成员属性**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|isLiveAutoPlay |Boolean |直播流是否自动播放。默认值：`true`。有效值：<br><br><br>* `true`：自动播放。<br><br>* `false`：不自动播放。 |
|isForeShowAutoPlay |Boolean |预告是否自动播放。默认值：`true`。有效值：<br><br><br>* `true`：自动播放。<br><br>* `false`：不自动播放。 |
|isPlayBackAutoPlay |Boolean |回放是否自动播放。默认值：`true`。有效值：<br><br><br>* `true`：自动播放。<br><br>* `false`：不自动播放。 |
|isForeShowLoop |Boolean |预告是否循环播放。默认值：`true`。有效值：<br><br><br>* `true`：自动循环播放。<br><br>* `false`：不自动循环播放。 |
|isPlayBackLoop |Boolean |回放是否循环播放。默认值：`true`。有效值：<br><br><br>* `true`：自动循环播放。<br><br>* `false`：不自动循环播放。 |


<span id="409d57b8"></span>
## RedirectInfo

重定向所需的信息。

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


**成员属性**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|entrance |String |点击事件的来源。<br><br><br>* `bannerAdvertisement`：点击页中广告。<br><br>* `floatingShoppingCard`：点击菜单下的商品卡片或商品浮窗。<br><br>* `businessAccount`：点击主播账号的头像或名称。<br><br>* `floatingAdvertisement`：点击浮标广告。<br><br>* `commentLink`：点击评论中的URL。<br><br>* `commentAvatar`：点击评论区的用户头像。<br><br>* `commentContent`：点击评论区的评论内容。<br><br>* `headerAdvertisement`：点击页头广告。<br><br>* `commentNickName`：点击评论区的用户昵称。<br><br>* `taskAwardTicket`：点击基于观看时长抽奖中领取奖券按钮。 |
|contentType |Integer |内容类型。<br><br><br>* `CONTENT_TYPE_URL(1)`：用于点击URL时的跳转。`urlRedirectInfo`字段不能为空。<br><br>* `CONTENT_TYPE_COMMENT(2)`：用于点击评论区用户昵称、用户头像或评论内容时的跳转。`commentModel`字段不能为空。<br><br>* `CONTENT_TYPE_TASK_AWARD_TICKET_URL(3)`：用于点击基于观看时长抽奖中领取奖券按钮时的跳转。`taskAwardTicketInfo`字段不能为空。 |
|urlRedirectInfo |[UrlRedirectInfo](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#9348dd7b) |基于URL跳转的信息。当`contentType`为`1`时填写该字段。 |
|commentModel |[SingleCommentModel](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#44947300) |点击评论区用户昵称、用户头像或评论内容时跳转所需的信息。当`contentType`的值为`2`时该字段不为空。 |
|product |[Product](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#0f642632) |点击菜单下的商品卡片或商品浮窗时跳转所需的商品信息。当`entrance`的值为`floatingShoppingCard`时该字段不为空。 |
|taskAwardTicketInfo |[TaskAwardTicketInfo](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#b5ba89b9) |点击基于观看时长抽奖中领取奖券按钮时跳转所需的信息。当`contentType`的值为`3`时该字段不为空。 |


<span id="9348dd7b"></span>
## UrlRedirectInfo

点击 URL 时重定向所需的信息。

```java
public class UrlRedirectInfo {
    private final String url;
    private final boolean enableFloating;
}
```


**成员属性**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|url |String |在BytePlus Live控制台设置的内嵌链接。 |
|enableFloating |Boolean |内容是否设置为在BytePlus Live控制台的浮窗页面显示。<br><br><br>* `true`：在直播间浮窗页面显示内容。<br><br>* `false`：在新页面显示内容。 |


<span id="44947300"></span>
## SingleCommentModel

单条评论的数据模型。

```java
public class SingleCommentModel extends BaseObservable {
    protected final String mNickname;
    protected String externalUserId = null;
    protected final String mContent;
    protected final boolean mIsPresenter;
    protected final long mMsgId;
}
```


**成员属性**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|mNickname |String |发送评论的用户昵称。 |
|externalUserId |String |发送评论的用户外部用户ID。ID为调用`UserIdStr`时传入的[GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-CN)。 |
|mContent |String |评论内容。 |
|mIsPresenter |Boolean |发送评论的用户是否为主播。有效值：<br><br><br>* `true`：主播。<br><br>* `false`：非主播。 |
|mMsgId |Long |评论ID。 |


<span id="0f642632"></span>
## Product

点击菜单下的商品卡片或商品浮窗时重定向所需的商品信息。

```Java
public class Product {}
```


**成员属性**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|Title |String |商品名称。 |
|Highlight |String |零售价。 |
|Strikethrough |String |刊例价。 |
|Remark |String |商品描述。 |
|IntroduceImage |String |商品图片的URL。 |
|RedirectImage |String |按钮图片的URL。 |


<span id="b5ba89b9"></span>
## TaskAwardTicketInfo

在观看时长抽奖中，点击领奖按钮时重定向所需的奖券信息。

```Java
public class TaskAwardTicketInfo{}
```


**成员属性**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|ticketUrl |String |领奖页面的链接。 |
|taskAwardRule |[TaskAwardRule](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#4e734a5e) |基于观看时长抽奖的奖品信息。 |


<span id="4e734a5e"></span>
## TaskAwardRule

观看时长抽奖的奖品信息。

```Java
public class TaskAwardRule {}
```


**成员属性**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|AwardItemName |String |奖品名称。 |
|AwardItemIcon |String |奖品图片的URL。 |
|TaskAwardItemId |String |奖品ID。 |


<span id="e4a2c940"></span>
## SimpleLayoutParams

视图的自定义位置。

```Java
public class SimpleLayoutParams {
    private int gravity;
    private int marginLeftDp;
    private int marginRightDp;
    private int marginTopDp;
    private int marginBottomDp;
}
```


**成员属性**


|**名称** |**类型** |接口行为 |
|---|---|---|
|gravity |Integer |定义视图在父布局中的位置和对齐方式。具体取值请参见[android.view.Gravity](https://developer.android.com/reference/android/view/Gravity)。 |
|marginLeftDp |Integer |视图距离父布局左侧的边距。单位：dp。 |
|marginRightDp |Integer |视图相对于其父布局的右边距。单位：dp。 |
|marginTopDp |Integer |视图相对于其父布局的上边距。单位：dp。 |
|marginBottomDp |Integer |视图相对于其父布局的下边距。单位：dp。 |


<span id="38b050a5"></span>
## CustomSize

视图的自定义尺寸。

```Java
public class CustomSize {
    private int widthDp;
    private int heightDp;
}
```


**成员属性**


|**名称** |**类型** |接口行为 |
|---|---|---|
|widthDp |Integer |视图的宽度。单位：dp。 |
|heightDp |Integer |视图的高度。单位：dp。 |


<span id="d9f238b6"></span>
## PortraitLiveRoomBottomBarLayout.BottomBar

竖屏模式下直播间底部的图标。

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


**枚举值**


|类型 |值 |接口行为 |
|---|---|---|
|IMAGE_TEXT_ICON |"imageTextIcon" |图形菜单的图标。 |
|INTERACT_TOOL_MENU |"interactToolMenu" |互动工具菜单的图标。 |
|SHOPPING_CARD_MENU |"shoppingCardMenu" |商品卡片菜单的图标。 |
|EMBEDDEDWEB_URLS |"embeddedWebUrls" |内嵌链接菜单的图标。 |
|PORTRAIT_THUMB |"portraitThumb" |直播间点赞图标。 |


<span id="e6c92fb5"></span>
## SendCommentResult

评论发送成功后的结果。

```Java
public class SendCommentResult {
    private String H5MsgId;
    private String Nickname;
}
```


**成员属性**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|H5MsgId |String |评论 ID。 |
|Nickname |String |发送评论用户的昵称。 |


<span id="00d8c2a4"></span>
## Error

表示因网络请求失败，服务器返回的错误。

```Java
public class Error {
    private String Code;
    private String Message;
}
```


**成员属性**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|Code |String |错误码。 |
|Message |String |错误信息。 |


<span id="f1af4dc5"></span>
## ResponseMetadata

直播间网络请求的通用描述。

```Java
public class ResponseMetadata {
    private String RequestId;
    private long SystemTime;
    private Error Error;
}    
```


**成员属性**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|RequestId |String |网络请求的唯一 ID，服务器用于识别该请求。 |
|SystemTime |Long |服务器生成返回调用结果时的系统时间（以 Unix 时间戳秒为单位）。 |
|Error |Error |服务器返回的网络请求失败的错误类。更多信息请参见[Error](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#00d8c2a4)。<br><br><br>* 若`Error`为空：服务器正常返回结果，请求成功。<br><br>* 若`Error`不为空：服务器拒绝请求或发生内部错误，请求失败。 |


<span id="c0244d2f"></span>
## SendCommentResponse

评论提交网络请求后服务器返回的调用结果。

```Java
public class SendCommentResponse extends BaseResponse {
    private SendCommentResult Result;
    private ResponseMetadata ResponseMetadata;
}    
```


**成员属性**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|Result |SendCommentResult |评论发送成功后的结果。更多信息请参见[SendCommentResult](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#e6c92fb5)。 |
|ResponseMetadata |ResponseMetadata |网络请求的通用描述。更多信息请参见[ResponseMetadata](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#f1af4dc5)。 |


<span id="fb1bfeef"></span>
## LanguageManager.LANGUAGE

直播间的语言类型。

```Java
public enum LanguageManager.LANGUAGE 
```


**枚举值**


|类型 |值 |接口行为 |
|---|---|---|
|ZH_HANS |0 |简体中文。 |
|EN |1 |英文。 |
|JA |2 |日文。 |
|ZH_HANT |3 |繁体中文。 |
|KO |4 |韩文。 |
|TH |5 |泰文。 |
|VI |6 |越南语。 |
|AR |7 |阿拉伯语。 |
|TR |8 |土耳其语。 |
|ES |9 |西班牙语。 |
|ID |10 |印尼语 |
|PT |11 |葡萄牙语。 |
|RU |12 |俄语。 |
|TL |13 |塔加洛语。 |
|KM |14 |高棉语。 |
|LO |15 |老挝语。 |
|MY |16 |缅甸语。 |
|MS |17 |马来语。 |
|HI |18 |印地语。 |
|FR |19 |法语。 |
|DE |20 |德语。 |
|IT |21 |意大利语。 |


<span id="e49a0ba0"></span>
## ActivityBookingModel

直播流预约信息。

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


**成员属性**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|activityName |String |直播间名称。 |
|activityId |Long |直播间的活动 ID。 |
|startTimeMillis |Long |直播流的开始时间（Unix 时间戳格式）。单位：ms。 |
|endTimeMillis |Long |直播流的结束时间（Unix 时间戳格式）。单位：ms。 |
|nickName |String |观众昵称。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">仅当观众输入昵称或登录直播间时，该字段才会被赋值。</div><br> |
|externalUserId |String |观众在第三方平台的唯一标识。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">仅当认证模式为自定义且观众登录直播间时，参数才有值。</div><br> |
|userId |Long |用户 ID，即观众在 BytePlus Live 中的唯一标识。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">如果观众未输入昵称或未登录直播间，则该值为<code>0</code>。</div><br> |


<span id="56a27a1b"></span>
## BDThemeIconModel

按钮信息。

```Java
public class BDThemeIconModel {
    private Drawable lightModeIcon;
    private Drawable darkModeIcon;
}
```


**成员属性**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|lightModeIcon |Drawable |浅色模式下使用的图标。 |
|darkModeIcon |Drawable |主题为深色模式时使用的按钮。 |


<span id="3e9f13cb"></span>
## CommentConfigModel

直播间评论配置模型。

```Java
public class CommentConfigModel extends BaseObservable {
    private boolean commentSendEnable;
    private boolean commentTranslateEnable;
}
```


**成员属性**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|commentSendEnable |Boolean |是否允许观众发送评论。<br><br><br>* `true`：允许。<br><br>* `false`：不允许。 |
|commentTranslateEnable |Boolean |是否启用评论翻译。<br><br><br>* `true`：启用。<br><br>* `false`：禁用。 |


<span id="fed59c08"></span>
## UIConfigModel

直播间 UI 主题色配置模型。

```Java
public class UIConfigModel extends BaseObservable {
    private int commentFontColor;
    private int hostCommentColor;
    private boolean isLightTheme;
}
```


**成员属性**


|**名称** |**类型** |**接口行为** |
|---|---|---|
|commentFontColor |Integer |非主播用户发送评论的颜色。 |
|hostCommentColor |Integer |主播发送评论的颜色。 |
|isLightTheme |布尔值 |指示直播间主题是否为浅色。<br><br><br>* `true`：非暗色模式。<br><br>* `false`：暗色模式。 |


<span id="4530ad0e"></span>
## JoinRoomConfig

加入完整直播间所需的配置。

```Java
public class JoinRoomConfig {
    public long activityId;
    public String token;
    public boolean isPortraitLiveRoom;
    public TVULiveRoom.TVURoomAuthMode authMode;
    public JoinResultListener joinResultListener;
  }
```


**成员属性**


|名称 |类型 |接口行为 |
|---|---|---|
|activityId |Long |要加入的直播间的活动 ID。可通过调用[CreateActivityAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2-zh-CN)或[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN)获取该 ID。 |
|token |String |加入直播间所需的授权 token。可通过调用[GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-CN)获取该 token。 |
|isPortraitLiveRoom |布尔值 |直播间是否为竖屏模式。<br><br><br>* `true`：为竖屏模式。<br><br>* `false`：为横屏模式。 |
|authMode |TVURoomAuthMode |该值必须与调用[GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-CN)时传入的 `Mode` 参数值一致。<br><br><br>* `PUBLIC`：当`Mode`的值为`1`时设置为该模式。观众以嘉宾身份加入直播间，在需要用户信息的场景（如点击评论输入框、点赞评论）时，必须输入昵称以完成嘉宾注册。<br><br>* `CUSTOM`：当`Mode`的值为`2`时设置为该模式。观众以应用中的用户信息加入直播间，因此可直接进行发送评论、点赞评论等操作。 |
|joinResultListener |JoinResultListener |直播间加入结果的回调类。该参数可设置为 null。更多信息请参见[JoinResultListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-callback-the-viewer-sdk-for-android-zh-CN#9bcb18be)。 |


<span id="7321845b"></span>
## BDLForceOfflineReason

观众被强制移出直播间的原因。

```Java
public enum BDLForceOfflineReason
```


**枚举值**


|类型 |值 |接口行为 |
|---|---|---|
|BDLiveForceOfflineReasonMultiLogin |0 |用户在开启重复登录防护时，使用多个设备同时登录。 |
|BDLiveForceOfflineReasonUnCheckIn |1 |因未签到超时。 |
|BDLiveForceOfflineReasonIPBanned |2 |IP 地址被封禁。 |
|BDLiveForceOfflineReasonKickOut |3 |被踢出。 |


<span id="b106da4b"></span>
## BusinessAccountAndUserInfoModel

关注主播所需的信息。

```Java
public class BusinessAccountAndUserInfoModel {
    private long activityId;
    private String externalId;
    private String externalName;
    private long hostAccountId;
    private String hostAccountName;
  }
```


**成员属性**


|名称 |类型 |接口行为 |
|---|---|---|
|activityId |Long |直播间的活动 ID。 |
|externalId |String |外部用户 ID，即第三方平台观众的唯一标识。该 ID 即调用[GetSDKTokenAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getsdktokenapi)时传入的 `UserIdStr`。 |
|externalName |String |观众昵称，即调用[GetSDKTokenAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getsdktokenapi)时传入的`Nickname`参数。 |
|hostAccountId |Long |主播账号 ID。 |
|hostAccountName |String |主播账号名称。 |


<span id="fdd8e1fe"></span>
## CommentUserModel

判断是否拦截键盘弹窗所需的信息。

```Java
public class CommentUserModel {
    private long activityId;
    private String nickname;
    private String externalUserId;
    private long userId;
 }
```


**成员属性**


|名称 |类型 |接口行为 |
|---|---|---|
|activityId |Long |直播间的活动 ID。 |
|nickname |String |观众昵称。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">如果观众未输入昵称或未登录直播间，则该值为<code>null</code>。</div><br> |
|externalUserId |String |第三方平台观众的唯一标识。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">仅当认证模式为自定义且观众已登录直播间时，该属性才有值。</div><br> |
|userId |Long |用户 ID，即 BytePlus Live 中观众的唯一标识。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">如果观众未输入昵称或未登录直播间，则该值为<code>0</code>。</div><br> |


<span id="446d9b7a"></span>
## BDLExternalReportConfiguration

数据上报配置。

```Java
public class BDLExternalReportConfiguration {
    private boolean enable;
    private String url;
    private int repeatInterval;
 }
```


**成员属性**


|名称 |类型 |接口行为 |
|---|---|---|
|enable |布尔值 |是否启用数据上报功能。默认值：`false`。有效值：<br><br><br>* `true`：启用。SDK 会在以下时机向`url`上报数据：<br><br>   * 观众成功加入直播间时。<br><br>   * 观众在直播间期间，按`repeatInterval`指定的间隔上报数据。<br><br>   * 观众离开直播间时。<br><br>* `false`：禁用。 |
|url |String |启用该功能时，SDK 发送数据上报 POST 请求的 URL。 |
|repeatInterval |Integer |数据上报的时间间隔。单位：秒。默认值：`30`。 |


<span id="1dbc8f5b"></span>
## BDLForceOfflineInfo

观众被强制移出直播间的信息。

```Java
public class BDLForceOfflineInfo {
    private final BDLForceOfflineReason reason;
    private final String prompt;
 }
```


**成员属性**


|名称 |类型 |接口行为 |
|---|---|---|
|reason |BDLForceOfflineReason |观众被强制移出直播间的原因。更多信息请参见[BDLForceOfflineReason](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#7321845b)。 |
|prompt |String |观众被强制移出直播间时的提示文本。 |
