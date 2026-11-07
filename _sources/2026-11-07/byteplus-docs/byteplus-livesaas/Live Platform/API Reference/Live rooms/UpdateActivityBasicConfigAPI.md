---
title: "UpdateActivityBasicConfigAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-updateactivitybasicconfigapi"
---

Call this API to update the basic configurations of a live room, such as its background image and preview.

Before calling this API operation, you must first call [GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi). Update the values of `GetActivityBasicConfigAPI`'s response parameters as needed and pass them as request parameter values when calling this API operation. If you have custom requirements, to prevent parameter values from being replaced with default values, you must pass the corresponding parameter value even if the parameter is not required.

<span id="requirement"></span>
## Requirement

Rate limit: 120 requests per minute per account

<span id="http-request"></span>
## HTTP request


* URL: `https://livesaas.byteplusapi.com/?Action=UpdateActivityBasicConfigAPI&Version=2020-06-01`

* Method: POST


<span id="request-parameters"></span>
## Request parameters

Not all shared request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters).


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdateActivityBasicConfigAPI` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of this API operation. Current version: `2020-06-01`. |


<span id="body"></span>
### Body


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|ActivityId |Long |Yes |`17218312****` |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |
|Name |String |Yes |`Live Room A` |The name of the live room, which cannot exceed 1950 characters in length. |
|LiveTime |Long |No |`1666258566` |The start time of the live stream in Unix timestamp format. Unit: seconds. The time can be accurate to the minute.<br><br>This is the scheduled start time. The actual start time may vary depending on when the host begins the broadcast.<br><br><br>* The `LiveTime` must be earlier than the `EndTime`, with a maximum difference of 259,200 (72 hours).<br><br>* This parameter value cannot be modified during a live stream. |
|IsBeginLiveEnable |Integer |No |`0` |Specifies whether to enable the feature of live stream start time. Default value: `0`.<br><br>Valid values:<br><br><br>* `0`: Disables the feature.<br><br>* `1`: Enables the feature. You can only start a live stream after the specified start time.<br><br><br>This parameter value cannot be modified during a live stream. |
|IsAutoEndEnable |Integer |No |`0` |Specifies whether to enable the feature of automatically ending the live stream at the specified end time. Default value: `0`.<br><br>Valid values:<br><br><br>* `0`: Disables the feature.<br><br>* `1`: Enables the feature.<br><br><br>This parameter value cannot be modified during a live stream. |
|EndTime |Long |No |`1666358566` |The end time of the live stream in Unix timestamp format. Unit: seconds. The time can be accurate to the minute.<br><br>The `EndTime` must be later than the `LiveTime`, with a maximum difference of 259,200 (72 hours).<br><br><br>* This parameter is required when the value of `IsAutoEndEnable` is `1`.<br><br>* This parameter value cannot be modified during a live stream. |
|IsCoverImageEnable |Integer |No |`0` |Specifies whether to enable the cover image. Default value: `0`.<br><br>Valid values:<br><br><br>* `0`: Disables the cover image.<br><br>* `1`: Enables the cover image. |
|CoverImageUrl |String |No |`https://example.image` |The URL of the cover image in landscape mode.<br><br><br>* Usually, a URL with a protocol header is required as the parameter value. However, if you get the URL of an image uploaded through the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/) (for example, by calling [GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi) to get the URL of a cover image uploaded through the console in a live room), the URL without a protocol header can be used as the parameter value.<br><br>* This parameter is required when the value of `IsCoverImageEnable` is `1`. |
|VerticalCoverImageUrl |String |No |`https://example.image` |The URL of the cover image in portrait mode.<br><br>If not specified, the parameter value is set to the value of `CoverImageUrl`.<br><br><br>* Usually, a URL with a protocol header is required as the parameter value. However, if you get the URL of an image uploaded through the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/) (for example, by calling [GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi) to get the URL of a cover image uploaded through the console in a live room), the URL without a protocol header can be used as the parameter value.<br><br>* This parameter is required when the value of `IsCoverImageEnable` is `1`. |
|IsPcBackImageEnable |Integer |No |`0` |Specifies whether to enable the background image or color for PCs. Default value: `0`.<br><br>Valid values:<br><br><br>* `0`: Disables the background image.<br><br>* `1`: Enables the background image.<br><br>* `2`: Enables the background color. |
|PcBackImageUrl |String |No |`//example.image` |The URL of the background image for PCs. This parameter is required when the value of `IsPcBackImageEnable` is `1`. |
|PcBackImageUrlDefault |String |No |`https://example.image` |The URL of the default background image for PCs, including a protocol header. |
|BackgroundColor |String |No |`#060815` |The background color for PCs, which follows the RGB color model. This parameter is required when the value of `IsPcBackImageEnable` is `2`. You must set the same value as the one returned in the response of [GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi). |
|IsMobileBackImageEnable |Integer |No |`0` |Specifies whether to enable the background image or color for mobile devices. Default value: `0`.<br><br>Valid values:<br><br><br>* `0`: Disables the background image.<br><br>* `1`: Enables the background image.<br><br>* `2`: Enables the background color. |
|MobileBackImageUrl |String |No |`//example.image` |The URL of the background image for mobile devices. This parameter is required when the value of `IsMobileBackImageEnable` is `1`. |
|MobileBackImageUrlDefault |String |No |`https://example.image` |The URL of the default background image for mobile devices, including a protocol header. |
|MobileBackgroundColor |String |No |`#060815` |The background color for mobile devices, which follows the RGB color model. This parameter is required when the value of `IsMobileBackImageEnable` is `2`. You must set the same value as the one returned in the response of [GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi). |
|IsPreviewVideoEnable |Integer |No |`0` |Specifies whether to enable the preview. Default value: `0`<br><br>Valid values:<br><br><br>* `0`: Disables the preview.<br><br>* `1`: Enables the preview. |
|PreviewVideoUrl |String |No |`-` |Deprecated. |
|PreviewVideoVid |String |No |`v03a49g10000ckkavibc77uejmsb****` |The video ID of the preview. This parameter is required when the value of `IsPreviewVideoEnable` is `1`. |
|PreviewVideoVidDefault |String |No |`-` |Deprecated. |
|IsPeopleCountEnable |Integer |No |`0` |Specifies whether to display the number of viewers on the viewing page. Default value: `0`<br><br>Valid values:<br><br><br>* `0`: Does not display the number of viewers.<br><br>* `1`: Displays the number of viewers. |
|IsHeaderImageEnable |Integer |No |`0` |Specifies whether to enable the header image for mobile devices. Default value: `0`<br><br>Valid values:<br><br><br>* `0`: Disables the header image.<br><br>* `1`: Enables the header image. |
|HeaderImageUrl |String |No |`//example.image` |The URL of the header image for mobile devices. This parameter is required when the value of `IsHeaderImageEnable` is `1`. |
|IsWatermarkImageEnable |Integer |No |`0` |Specifies whether to enable the player logo. Default value: `0`<br><br>Valid values:<br><br><br>* `0`: Disables the logo.<br><br>* `1`: Enables the logo. |
|WatermarkImageUrl |String |No |`//example.image` |The URL of the player logo. This parameter is required when the value of `IsWatermarkImageEnable` is `1`. |
|IsThumbUpEnable |Integer |No |`0` |Specifies whether to enable the feature of liking the live room. Default value: `0`<br><br>Valid values:<br><br><br>* `0`: Disables the feature.<br><br>* `1`: Enables the feature. |
|ThumbUpUrl |String |No |`//example.image` |The URL of the like icon. This parameter is required when the value of `IsThumbUpEnable` is `1`. |
|ThumbUpUrlDefault |String |No |`https://example.image` |The URL of the default like icon, including a protocol header. |
|IsShareIconEnable |Integer |No |`0` |Specifies whether to enable the share icon. Default value: `0`<br><br>Valid values:<br><br><br>* `0`: Disables the share icon.<br><br>* `1`: Enables the share icon. |
|ShareIconUrl |String |No |`//example.image` |The URL of the share icon. This parameter is required when the value of `IsShareIconEnable` is `1`. |
|ShareIconUrlDefault |String |No |`https://example.image` |The URL of the default share icon, including a protocol header. |
|IsCommentTranslateEnable |Integer |No |`-` |Deprecated. |
|IsAnnouncementEnable |Integer |No |`0` |Specifies whether to enable the description of the live room. Default value: `0`<br><br>Valid values:<br><br><br>* `0`: Disables the description.<br><br>* `1`: Enables the description. |
|Announcement |String |No |`Live room description` |The description of the live room. This parameter is required when the value of `IsAnnouncementEnable` is `1`. |
|InteractionColor |String |No |`#202124` |The background color of interaction areas on PCs, which follows the RGB color model. You must set the same value as the one returned in the response of [GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi). |
|FontColor |String |No |`#ffffff` |The font color, which follows the RGB color model. You must set the same value as the one returned in the response of [GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi). |
|ColorThemeIndex |String |No |`dark` |The theme. Default value: `dark`<br><br>Valid values:<br><br><br>* `light`: Light mode.<br><br>* `dark`: Dark mode.<br><br>* `cold`: Classic mode.<br><br>* `holiday`: Festive mode. |
|IsPCHeaderImageEnable |Integer |No |`0` |Specifies whether to enable the header image for PCs. Default value: `0`<br><br>Valid values:<br><br><br>* `0`: Disables the header image.<br><br>* `1`: Enables the header image. |
|PCHeaderImageUrl |String |No |`//example.image` |The URL of the header image for PCs. This parameter is required when the value of `IsPCHeaderImageEnable` is `1`. |
|IsCountDownEnable |Integer |No |`0` |Specifies whether to enable the countdown. Default value: `0`<br><br>Valid values:<br><br><br>* `0`: Disables the countdown.<br><br>* `1`: Enables the countdown. |
|IsAutoStartEnable |Integer |No |`0` |Specifies whether to start the live stream automatically. Default value: `0`<br><br>Valid values:<br><br><br>* `0`: Does not start the live stream automatically.<br><br>* `1`: Starts the live stream automatically. |
|AutoStartType |Integer |No |`0` |The mode for automatically starting the live stream. This parameter is required when the value of `IsAutoStartEnable` is `1`. Default value: `0`<br><br>Valid values:<br><br><br>* `0`: Does not automatically start the live stream.<br><br>* `1`: Automatically starts the prerecorded video.<br><br>* `2`: Automatically starts pulling the stream. |
|IsPageLimitEnable |Integer |No |`0` |Specifies whether to enable viewing page restrictions. Default value: `0`<br><br>Valid values:<br><br><br>* `0`: Disables restrictions.<br><br>* `1`: Enables restrictions. |
|PageLimitType |String |No |`pc` |Viewing page restrictions. This parameter is required when the value of `IsPageLimitEnable` is `1`.<br><br>Valid values:<br><br><br>* `pc`: Viewers can only watch videos on PCs.<br><br>* `mobile`: Viewers can only watch videos on mobile devices. |
|IsLanguageEnable |Integer |No |`0` |Specifies whether to enable the language selector on the viewing page. Default value: `0`<br><br>Valid values:<br><br><br>* `0`: Disables the language selector.<br><br>* `1`: Enables the language selector. |
|LanguageType |Array of Integer |No |`[0,1]` |Languages that viewers can select on the viewing page. This parameter is required when the value of `IsLanguageEnable` is `1`. Default value: `0`. You can select up to 13 languages.<br><br>Valid values:<br><br><br>* `0`: Simplified Chinese.<br><br>* `1`: English.<br><br>* `2`: Japanese.<br><br>* `3`: Traditional Chinese.<br><br>* `4`: Korean.<br><br>* `5`: Thai.<br><br>* `6`: Vietnamese.<br><br>* `7`: Arabic.<br><br>* `8`: Turkish.<br><br>* `9`: Spanish.<br><br>* `10`: Indonesian.<br><br>* `11`: Portuguese.<br><br>* `12`: Russian.<br><br>* `13`: Tagalog.<br><br>* `14`: Khmer.<br><br>* `15`: Lao.<br><br>* `16`: Burmese.<br><br>* `17`: Malay.<br><br>* `18`: Hindi.<br><br>* `19`: French.<br><br>* `20`: German.<br><br>* `21`: Italian. |
|SiteTags |Array of [SiteTags](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitybasicconfigapi) |No |`-` |List of category tags in the live room. |
|TextSiteTags |Array of [TextSiteTags](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitybasicconfigapi) |No |`-` |List of text tags in the live room. |
|PreviewVideoId |Long |No |`431674` |The media library ID of the preview. This parameter is required when the value of `IsPreviewVideoEnable` is `1`. |
|AccountId |Long |No |`-` |Deprecated. |
|PreviewVideoReviewStatus |Integer |No |`-` |Deprecated. |
|DefaultSubtitleLanguage |String |No |`-` |Deprecated. |
|SourceSubtitleLanguage |String |No |`-` |Deprecated. |
|OpenLiveAvextractorTask |Integer |No |`-` |Deprecated. |
|IsTimeShift |Integer |No |`0` |This feature is currently not available. Fixed value: `0` |
|PreviewVideoCoverImage |String |No |`https://example.image` |The URL of the preview's cover image. |
|PreviewVideoMediaName |String |No |`Video.mp4` |The name of the preview. |
|IsPreviewPromptEnable |Integer |No |`0` |Specifies whether to enable the preview text. Default value: `0`<br><br>Valid values:<br><br><br>* `0`: Disables the preview text.<br><br>* `1`: Enables the preview text. |
|PreviewPrompt |String |No |`The live stream will start soon.` |The preview text. This parameter is required when the value of `IsPreviewPromptEnable` is `1`. |
|IsReservationEnable |Integer |No |`0` |Specifies whether to enable the booking feature. Default value: `0`<br><br>Valid values:<br><br><br>* `0`: Disables the feature.<br><br>* `1`: Enables the feature. |
|IsReservationSmsEnable |Integer |No |`1` |Specifies whether to enable the SMS reminder for booking. Default value: `1`.<br><br>Valid values:<br><br><br>* `1`: Enables the SMS reminder.<br><br>* `2`: Disables the SMS reminder.<br><br><br>This parameter is only valid when the value of `IsReservationEnable` is `1`. |
|ReservationTime |Integer |No |`300` |Specifies the time, in seconds, before the live stream starts to send an SMS reminder to viewers.<br><br>Unit: seconds.<br><br>This parameter is only valid when the value of `IsReservationSmsEnable` is `1`. |
|ReservationText |String |No |`-` |Deprecated. |
|WatermarkPosition |Integer |No |`0` |The location of the player logo. Default value: `0`<br><br>Valid values:<br><br><br>* `0`: In the upper\-right corner of the player.<br><br>* `1`: In the upper\-left corner of the player.<br><br>* `2`: In the lower\-left corner of the player.<br><br>* `3`: In the lower\-right corner of the player. |
|IsReplayBulletChat |Integer |No |`-` |Deprecated. |
|PresenterChatColor |String |No |`#FFD58B` |The font color for the presenter's chat messages, which follows the RGB color model. You must set the same value as the one returned in the response of [GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi). |
|IsLiveBulletChat |Integer |No |`-` |Deprecated. |
|IsBackgroundBlur |Integer |No |`0` |Specifies whether to enable background blurring. Default value: `0`<br><br>Valid values:<br><br><br>* `0`: Disables the feature.<br><br>* `1`: Enables the feature on mobile devices.<br><br>* `2`: Enables the feature on PCs.<br><br>* `3`: Enables the feature on PCs and mobile devices. |
|FeedbackMessage |String |No |`-` |Deprecated. |
|IsFeedbackEnable |Integer |No |`-` |Deprecated. |
|IsThumbUpNumberEnable |Integer |No |`0` |Specifies whether to display the number of likes for the live room on the viewing page. Default value: `0`<br><br>Valid values:<br><br><br>* `0`: Does not display the number of likes.<br><br>* `1`: Displays the number of likes. |
|SmsLanguage |Integer |No |`0` |The language of SMS messages. Default value: `0`.<br><br>Valid values:<br><br><br>* `0`: Chinese if the phone number starts with +86. English if the phone number starts with other numbers.<br><br>* `1`: Chinese.<br><br>* `2`: English.<br><br>* `3`: Both English and Chinese. |
|MobileChatBackgroundColor |String |No |`#000000` |The background color of comments on mobile devices, which follows the RGB color model. You must set the same value as the one returned in the response of [GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi). |
|ConfigVersion |Integer |No |`1` |The configuration version. Fixed value: `1`. |
|LiveZone |Integer |No |`480` |The time zone. Default value: `480`.<br><br>Valid values:<br><br><br>* `-60`: GMT\-01:00 Ponta del Gada (Portugal).<br><br>* `-120`: GMT\-02:00 Fernando de Noronha (Brazil).<br><br>* `-180`: GMT\-03:00 Brasilia (Brazil).<br><br>* `-240`: GMT\-04:00 Santiago (Chile).<br><br>* `-300`: GMT\-05:00 Washington, D.C. (United States).<br><br>* `-360`: GMT\-06:00 Mexico City (Mexico).<br><br>* `-420`: GMT\-07:00 Denver (United States).<br><br>* `-480`: GMT\-08:00 Vancouver (Canada).<br><br>* `-540`: GMT\-09:00 Alaska (United States).<br><br>* `-570`: GMT\-09:30 Teojae (French Polynesia).<br><br>* `-600`: GMT\-10:00 Hawaii (United States).<br><br>* `-660`: GMT\-11:00 Alofi (Niue).<br><br>* `0`: GMT+00:00 London (United Kingdom).<br><br>* `60`: GMT+01:00 Paris (France).<br><br>* `120`: GMT+02:00 Damascus (Syria).<br><br>* `180`: GMT+03:00 Moscow (Russia).<br><br>* `210`: GMT+03:30 Tehran (Iran).<br><br>* `240`: GMT+04:00 Dubai (United Arab Emirates).<br><br>* `300`: GMT+05:00 New Delhi (India).<br><br>* `330`: GMT+05:30 Mumbai (India).<br><br>* `360`: GMT+06:00 Dhaka (Bangladesh).<br><br>* `390`: GMT+06:30 Yangon (Myanmar).<br><br>* `420`: GMT+07:00 Bangkok (Thailand).<br><br>* `480`: GMT+08:00 Beijing (China).<br><br>* `525`: GMT+08:45 Yukla (Australia).<br><br>* `540`: GMT+09:00 Tokyo (Japan).<br><br>* `570`: GMT+09:30 Darwin (Australia).<br><br>* `600`: GMT+10:00 Canberra (Australia).<br><br>* `630`: GMT+10:30 Lord Howe Island (Australia).<br><br>* `660`: GMT+11:00 Sydney (Australia).<br><br>* `720`: GMT+12:00 Suva (Fiji).<br><br>* `780`: GMT+13:00 Phoenix Islands (Kiribati).<br><br>* `825`: GMT+13:45 Chatham Islands (New Zealand).<br><br>* `840`: GMT+14:00 Christmas Island (Kiribati). |
|RiskWarningSetting |Object of [RiskWarningSetting](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitybasicconfigapi) |No |`-` |Configurations of the reminder pop\-up window displayed when viewers enter the live room. |
|IsColorSync |Integer |No |`0` |Specifies whether to synchronize color configurations to portrait mode. Default value: `0`.<br><br>Valid values:<br><br><br>* `0`: Does not synchronize to portrait mode.<br><br>* `1`: Synchronizes to portrait mode. |
|IsPlayerTopEnable |Integer |No |`0` |Specifies whether to enable the pinned player feature. Default value: `0`<br><br>Valid values:<br><br><br>* `0`: Disables the feature.<br><br>* `1`: Enables the feature. |
|PlayerTopType |Array of Integer |No |`[1,2]` |The terminal where the player is pinned to the top of the page. Default value: `[1,2]`<br><br>This parameter is required when the value of `IsPlayerTopEnable` is `1`.<br><br>Valid values:<br><br><br>* `0`: Deprecated.<br><br>* `1`: The player is pinned to the top of the page on PCs.<br><br>* `2`: The player is pinned to the top of the page on mobile devices in landscape mode. |
|IsReplayAutoOnlineEnable |Integer |No |`0` |Specifies whether to automatically publish the replay on the viewing page after the live stream ends.<br><br>Valid values:<br><br><br>* `0`: Does not automatically release the playback.<br><br>* `1`: Automatically releases the playback. |
|IsSDKPlayEnable |Integer |No |`1` |Specifies whether to enable the player on the viewing page integrated with the Web Viewer SDK to play live videos. Default value: `1`.<br><br>Valid values:<br><br><br>* `0`: Prevents the player from playing live videos. To avoid unnecessary playback, the live stream is disabled at the same time. As a result, viewers cannot watch live videos, whether they are on the viewing page integrated with the Web Viewer SDK or not.<br><br>* `1`: Allows the player to play live videos. |
|SDKPlayStatus |Integer |No |`2` |The status of the live room displayed on the viewing page integrated with the Web Viewer SDK, which may not be the same as the actual status of the live room.<br><br>If not specified, the actual status of the live room is displayed.<br><br>This parameter is only valid when the value of `IsSDKPlayEnable` is `0`.<br><br>Valid values:<br><br><br>* `2`: Preview.<br><br>* `3`: Playback.<br><br>* `4`: Over.<br><br><br>If you set the status to `2` (Preview) or `3` (Playback) but the corresponding content is not available, the page will display the `Over` status. For example, if you set the status to `3` but have not published a replay, the page will show `Over`, not `Playback`. |
|IsVideoChatDisplayed |Integer |No |`0` |Specifies whether to enable the co\-host feature on the live streaming page in a web browser. Default value: `0`.<br><br>Valid values:<br><br><br>* `0`: Disables the feature.<br><br>* `1`: Enables the feature. |
|IsSharedAddressDisplayed |Integer |No |`0` |Specifies whether to display the viewing page address on the live streaming page in a web browser. Default value: `0`.<br><br>Valid values:<br><br><br>* `0`: Does not display the address.<br><br>* `1`: Displays the address. |
|IsReleaseNoticeDisplayed |Integer |No |`0` |Specifies whether to enable the lock preview feature on the live streaming page in a web browser. Default value: `0`.<br><br>Valid values:<br><br><br>* `0`: Disables the feature.<br><br>* `1`: Enables the feature. |
|IsInteractiveEnable |Integer |No |`0` |Specifies whether to allow the host to manage only the specified interaction tools on the live streaming page in a web browser. Default value: `0`.<br><br>Valid values:<br><br><br>* `0`: The host can manage all the following interaction tools.<br><br>* Questionnaire<br><br>* Document<br><br>* Check\-in<br><br>* Quiz<br><br>* Lucky draw<br><br>* Announcement<br><br>* `1`: The host can manage only the specified interaction tools. |
|InteractiveShowSetting |Object of [InteractiveShowSetting](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitybasicconfigapi) |No |`-` |The interaction tools that the host can manage on the live streaming page in a web browser. Configure at least one interaction tool.<br><br>This parameter is required if the value of `IsInteractiveEnable` is `1`. |


<span id="interactiveshowsetting"></span>
#### InteractiveShowSetting


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|IsQuestionnaireDisplayed |Integer |No |`0` |Specifies whether to allow the host to manage questionnaires on the live streaming page in a web browser. Default value: `0`.<br><br>Valid values:<br><br><br>* `0`: The host cannot manage questionnaires.<br><br>* `1`: The host can manage questionnaires. |
|IsDocDisplayed |Integer |No |`0` |Specifies whether to allow the host to manage documents on the live streaming page in a web browser. Default value: `0`.<br><br>Valid values:<br><br><br>* `0`: The host cannot manage documents.<br><br>* `1`: The host can manage documents. |
|IsCheckInDisplayed |Integer |No |`0` |Specifies whether to allow the host to manage check\-ins on the live streaming page in a web browser. Default value: `0`.<br><br>Valid values:<br><br><br>* `0`: The host cannot manage check\-ins.<br><br>* `1`: The host can manage check\-ins. |
|IsQuizDisplayed |Integer |No |`0` |Specifies whether to allow the host to manage quizzes on the live streaming page in a web browser. Default value: `0`.<br><br>Valid values:<br><br><br>* `0`: The host cannot manage quizzes.<br><br>* `1`: The host can manage quizzes. |
|IsLuckDrawDisplayed |Integer |No |`0` |Specifies whether to allow the host to manage lucky draws on the live streaming page in a web browser. Default value: `0`.<br><br>Valid values:<br><br><br>* `0`: The host cannot manage lucky draws.<br><br>* `1`: The host can manage lucky draws. |
|IsAnnouncementDisplayed |Integer |No |`0` |Specifies whether to allow the host to manage announcements on the live streaming page in a web browser. Default value: `0`.<br><br>Valid values:<br><br><br>* `0`: The host cannot manage announcements.<br><br>* `1`: The host can manage announcements. |


<span id="sitetags"></span>
#### SiteTags


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Value |String |Yes |`1` |The category tag value. |
|Index |Integer |Yes |`0` |The index of the category tag, which identifies the display order on the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).<br><br>Value range: [0,19]. |


<span id="textsitetags"></span>
#### TextSiteTags


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Value |String |Yes |`3` |The text tag value. |
|Index |Integer |Yes |`0` |The index of the text tag, which identifies the display order on the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).<br><br>Value range: [0,4]. |


<span id="riskwarningsetting"></span>
#### RiskWarningSetting


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|IsRiskWarningEnable |Integer |No |`0` |Specifies whether to enable the reminder pop\-up window. Default value: `0`.<br><br>Valid values:<br><br><br>* `0`: Disables the feature.<br><br>* `1`: Enables the feature. |
|RiskWarningButtonText |String |No |`Understood` |The button name for the reminder pop\-up window. |
|RiskWarningContent |String |No |`Welcome to the live room! Please abide by the laws and regulations of the organizer's and your countries and do not send comments that are pornographic, illegal, vulgar, or defamatory in nature. Be a model viewer to others. We politely request that you do not disrupt the good order of the live room by engaging in trolling or other malicious behavior. Use your common sense if and when presented with a private product offer between you and the host.` |The content of the reminder. |
|RiskWarningTitle |String |No |`Reminder` |The title of the reminder pop\-up window. |


<span id="response-parameters"></span>
## Response parameters


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|ActivityId |Long |`17218312****` |The activity ID of the live room. |
|ActivityIdStr |String |`-` |Deprecated. |
|Status |Integer |`-` |Deprecated. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```JSON
POST https://livesaas.byteplusapi.com/?Action=UpdateActivityBasicConfigAPI&Version=2020-06-01
{
    "ActivityId": 17218312****,
    "IsSDKPlayEnable": 1,
    "SDKPlayStatus": 2,
    "Name": "Live Room A",
    "LiveTime": 1666258566,
    "IsBeginLiveEnable": 0,
    "IsCoverImageEnable": 0,
    "CoverImageUrl": "https://example.image",
    "VerticalCoverImageUrl": "https://example.image",
    "IsPcBackImageEnable": 0,
    "PcBackImageUrl": "//example.image",
    "PcBackImageUrlDefault": "https://example.image",
    "IsMobileBackImageEnable": 0,
    "MobileBackImageUrl": "//example.image",
    "MobileBackImageUrlDefault": "https://example.image",
    "IsPreviewVideoEnable": 0,
    "PreviewVideoUrl": "",
    "PreviewVideoVid": "",
    "PreviewVideoVidDefault": "",
    "IsPeopleCountEnable": 0,
    "IsHeaderImageEnable": 0,
    "HeaderImageUrl": "",
    "IsWatermarkImageEnable": 0,
    "WatermarkImageUrl": "",
    "IsThumbUpEnable": 0,
    "ThumbUpUrl": "",
    "ThumbUpUrlDefault": "",
    "IsShareIconEnable": 0,
    "ShareIconUrl": "",
    "ShareIconUrlDefault": "https://example.image",
    "IsCommentTranslateEnable": 0,
    "Announcement": "",
    "IsAnnouncementEnable": 0,
    "BackgroundColor": "#060815",
    "InteractionColor": "#202124",
    "FontColor": "#ffffff",
    "ColorThemeIndex": "dark",
    "IsPCHeaderImageEnable": 0,
    "PCHeaderImageUrl": "",
    "IsCountdownEnable": 0,
    "IsAutoStartEnable": 0,
    "IsPageLimitEnable": 0,
    "PageLimitType": "",
    "IsLanguageEnable": 0,
    "LanguageType": [],
    "SiteTags": [],
    "TextSiteTags": [],
    "AutoStartType": 0,
    "IsPlayerTopEnable": 0,
    "PlayerTopType": [],
    "IsReplayAutoOnlineEnable": 0,
    "PreviewVideoId": 0,
    "AccountId": 0,
    "PreviewVideoReviewStatus": 0,
    "DefaultSubtitleLanguage": "",
    "SourceSubtitleLanguage": "",
    "OpenLiveAvextractorTask": 0,
    "IsTimeShift": 0,
    "PreviewVideoCoverImage": "",
    "PreviewVideoMediaName": "",
    "IsPreviewPromptEnable": 0,
    "PreviewPrompt": "The live stream will start soon.",
    "IsReservationEnable": 0,
    "IsReservationSmsEnable": 1,
    "ReservationTime": 300,
    "ReservationText": "",
    "WatermarkPosition": 0,
    "IsReplayBulletChat": 0,
    "PresenterChatColor": "#FFD58B",
    "IsLiveBulletChat": 0,
    "IsBackgroundBlur": 0,
    "FeedbackMessage": "",
    "IsFeedbackEnable": 0,
    "IsThumbUpNumberEnable": 1,
    "SmsLanguage": 0,
    "MobileChatBackgroundColor": "#000000",
    "MobileBackgroundColor": "#060815",
    "ConfigVersion": 1,
    "LiveZone": 480,
    "IsColorSync": 0,
    "IsVideoChatDisplayed": 0,
    "IsSharedAddressDisplayed": 0,
    "IsReleaseNoticeDisplayed": 0,
    "IsInteractiveEnable": 1,
    "InteractiveShowSetting": {
        "IsQuestionnaireDisplayed": 1,
        "IsDocDisplayed": 1,
        "IsCheckInDisplayed": 1,
        "IsQuizDisplayed": 0,
        "IsLuckDrawDisplayed": 0,
        "IsAnnouncementDisplayed": 0
        },
    "EndTime": 1666358566,
    "IsAutoEndEnable": 0
    "RiskWarningSetting": {
        "IsRiskWarningEnable": 0,
        "RiskWarningTitle": "",
        "RiskWarningContent": "",
        "RiskWarningButtonText": ""
    },
}
```


<span id="sample-response"></span>
### Sample response

```JSON
{
  "ResponseMetadata": {
    "RequestId": "201806041104200100100232280022D30",
    "Action": "UpdateActivityBasicConfigAPI",
    "Version": "2020-06-01",
    "Service": "livesaas",
    "Region": "ap-singapore-1",
    "SystemTime": 1656358566
  },
  "Result": {
    "ActivityId": 17218312****,
    "ActivityIdStr": "",
    "Status": 0
  }
}
```


<span id="error-codes"></span>
## Error codes

The following table lists error codes specific to this API operation. For a list of shared error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |100000 |The EndTime cannot be earlier than now. |Modify the value of the `EndTime` parameter and try again. |
|200 |100000 |The EndTime cannot be earlier than the LiveTime. |Modify the value of parameter `EndTime` or `LiveTime` and try again. |
|200 |100000 |The EndTime cannot be later than 72 hours from the LiveTime. |The maximum difference between the value of parameter `EndTime` and that of parameter `LiveTime` is 259,200 (72 hours). Modify the parameter value and try again. |
|200 |100000 |The EndTime or IsAutoEndEnable cannot be modified during a live stream. |End the live stream first and then modify the value of parameter `EndTime` or `IsAutoEndEnable`. |
|200 |100000 |The LiveTime or IsBeginLiveEnable cannot be modified during a live stream. |End the live stream first and then modify the value of parameter `LiveTime` or `IsBeginLiveEnable`. |
|200 |100000 |Invalid %s |The parameter is invalid. Modify the value based on the specifications and try again. |
