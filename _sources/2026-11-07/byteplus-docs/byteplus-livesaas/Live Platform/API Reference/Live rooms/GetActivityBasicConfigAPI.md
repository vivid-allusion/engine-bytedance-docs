---
title: "GetActivityBasicConfigAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getactivitybasicconfigapi"
---

Call this API to retrieve a comprehensive set of basic configurations for a specified live room.

<span id="requirement"></span>
## Requirement

Rate limit: 120 requests per minute per account

<span id="http-request"></span>
## HTTP request


* URL: `https://livesaas.byteplusapi.com/?Action=GetActivityBasicConfigAPI&Version=2020-06-01`

* Method: GET


<span id="request-parameters"></span>
## Request parameters

Not all shared request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters).

<span id="query"></span>
### Query


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetActivityBasicConfigAPI` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of this API operation. Current version: `2020-06-01`. |
|ActivityId |Long |Yes |`17218312****` |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |


<span id="response-parameters"></span>
## Response parameters


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|ActivityId |Long |`17218312****` |The activity ID of the live room. |
|Name |String |`Live Room A` |The name of the live room. |
|LiveTime |Long |`1666258566` |The start time of the live stream in Unix timestamp format. Unit: seconds.<br><br>This may not be the time the live stream actually starts. |
|IsBeginLiveEnable |Integer |`0` |Indicates whether the feature of live stream start time is enabled.<br><br>Valid values:<br><br><br>* `0`: Disabled.<br><br>* `1`: Enabled. You can only start a live stream after the specified start time. |
|IsCoverImageEnable |Integer |`1` |Indicates whether the cover image is enabled.<br><br>Valid values:<br><br><br>* `0`: Disabled.<br><br>* `1`: Enabled. |
|CoverImageUrl |String |`//example.image` |The URL of the cover image in landscape mode.<br><br>The URL includes a protocol header if configured via an API call, but not if configured via the console. |
|CoverImageUrlDefault |String |`//example.image` |The URL of the default cover image in landscape mode, without a protocol header. |
|VerticalCoverImageUrl |String |`//example.image` |The URL of the cover image in portrait mode.<br><br>If not specified, the parameter value is set to the value of `CoverImageUrl`.<br><br>If the cover image is configured by calling an API operation, the URL includes a protocol header. However, it does not include a protocol header if the cover image is configured via the console. |
|IsPcBackImageEnable |Integer |`1` |Indicates whether the background image or color for PCs is enabled.<br><br>Valid values:<br><br><br>* `0`: The background image is disabled.<br><br>* `1`: The background image is enabled.<br><br>* `2`: The background color is enabled. |
|PcBackImageUrl |String |`//example.image` |The URL of the background image for PCs. This parameter applies only when `IsPcBackImageEnable` is `1`. |
|PcBackImageUrlDefault |String |`https://example.image` |The URL of the default background image for PCs, including a protocol header. |
|IsMobileBackImageEnable |Integer |`1` |Indicates whether the background image or color for mobile devices is enabled.<br><br>Valid values:<br><br><br>* `0`: The background image is disabled.<br><br>* `1`: The background image is enabled.<br><br>* `2`: The background color is enabled. |
|MobileBackImageUrl |String |`//example.image` |The URL of the background image for mobile devices. This parameter takes effect only when the value of `IsMobileBackImageEnable` is `1`. |
|MobileBackImageUrlDefault |String |`https://example.image` |The URL of the default background image for mobile devices, including a protocol header. |
|MobileBackgroundColor |String |`#060815` |The background color for mobile devices, which follows the RGB color model.<br><br>This parameter takes effect only when the value of `IsMobileBackImageEnable` is `2`. |
|IsPreviewVideoEnable |Integer |`0` |Indicates whether the preview is enabled.<br><br>Valid values:<br><br><br>* `0`: Disabled.<br><br>* `1`: Enabled. |
|PreviewVideoUrl |String |`-` |Deprecated. |
|PreviewVideoVid |String |`v03a49g10000ckkavibc77uejmsb****` |The video ID of the preview. This parameter takes effect only when the value of `IsPreviewVideoEnable` is `1`. |
|PreviewVideoVidDefault |String |`-` |Deprecated. |
|IsPeopleCountEnable |Integer |`0` |Indicates whether the number of viewers is displayed on the viewing page.<br><br>Valid values:<br><br><br>* `0`: Not displayed.<br><br>* `1`: Displayed. |
|IsHeaderImageEnable |Integer |`0` |Indicates whether the header image for mobile devices is enabled.<br><br>Valid values:<br><br><br>* `0`: Disabled.<br><br>* `1`: Enabled. |
|HeaderImageUrl |String |`//example.image` |The URL of the header image for mobile devices. This parameter takes effect only when the value of `IsHeaderImageEnable` is `1`. |
|IsWatermarkImageEnable |Integer |`0` |Indicates whether the player logo is enabled.<br><br>Valid values:<br><br><br>* `0`: Disabled.<br><br>* `1`: Enabled. |
|WatermarkImageUrl |String |`//example.image` |The URL of the player logo. This parameter takes effect only when the value of `IsWatermarkImageEnable` is `1`. |
|IsThumbUpEnable |Integer |`0` |Indicates whether viewers can like the live room. Valid values:<br><br><br>* `0`: Disabled.<br><br>* `1`: Enabled. |
|ThumbUpUrl |String |`//example.image` |The URL of the like icon. This parameter takes effect only when the value of `IsThumbUpEnable` is `1`. |
|ThumbUpUrlDefault |String |`https://example.image` |The URL of the default like icon, including a protocol header. |
|IsShareIconEnable |Integer |`0` |Indicates whether the share icon is enabled.<br><br>Valid values:<br><br><br>* `0`: Disabled.<br><br>* `1`: Enabled. |
|ShareIconUrl |String |`//example.image` |The URL of the share icon. This parameter takes effect only when the value of `IsShareIconEnable` is `1`. |
|ShareIconUrlDefault |String |`https://example.image` |The URL of the default share icon, including a protocol header. |
|IsCommentTranslateEnable |Integer |`-` |Deprecated. |
|IsAnnouncementEnable |Integer |`0` |Indicates whether the description of the live room is enabled.<br><br>Valid values:<br><br><br>* `0`: Disabled.<br><br>* `1`: Enabled. |
|Announcement |String |`Live room description` |The description of the live room. This parameter takes effect only when the value of `IsAnnouncementEnable` is `1`. |
|BackgroundColor |String |`#060815` |The background color for PCs, in hexadecimal RGB format.<br><br>This parameter takes effect only when the value of `IsPcBackImageEnable` is `2`. |
|InteractionColor |String |`#202124` |The background color of interaction areas on PCs, which follows the RGB color model. |
|FontColor |String |`#ffffff` |The font color, which follows the RGB color model. |
|ColorThemeIndex |String |`dark` |The theme.<br><br>Valid values:<br><br><br>* `light`: Light mode.<br><br>* `dark`: Dark mode.<br><br>* `cold`: Classic mode.<br><br>* `holiday`: Festive mode. |
|IsPCHeaderImageEnable |Integer |`0` |Indicates whether the header image for PCs is enabled.<br><br>Valid values:<br><br><br>* `0`: Disabled.<br><br>* `1`: Enabled. |
|PCHeaderImageUrl |String |`//example.image` |The URL of the header image for PCs. This parameter takes effect only when the value of `IsPCHeaderImageEnable` is `1`. |
|IsCountDownEnable |Integer |`0` |Indicates whether the countdown is enabled.<br><br>Valid values:<br><br><br>* `0`: Disabled.<br><br>* `1`: Enabled. |
|IsAutoStartEnable |Integer |`0` |Indicates whether the feature of starting the live stream automatically is enabled.<br><br>Valid values:<br><br><br>* `0`: Disabled.<br><br>* `1`: Enabled. |
|IsPageLimitEnable |Integer |`0` |Indicates whether viewing page restrictions are enabled.<br><br>Valid values:<br><br><br>* `0`: Disabled.<br><br>* `1`: Enabled. |
|PageLimitType |String |`pc` |Viewing page restrictions. This parameter takes effect only when the value of `IsPageLimitEnable` is `1`.<br><br>Valid values:<br><br><br>* `pc`: Viewers can only watch videos on PCs.<br><br>* `mobile`: Viewers can only watch videos on mobile devices. |
|IsLanguageEnable |Integer |`0` |Indicates whether the language selector is enabled on the viewing page.<br><br>Valid values:<br><br><br>* `0`: Disabled.<br><br>* `1`: Enabled. |
|LanguageType |Array of Integer |`[0,1]` |Languages that viewers can select on the viewing page. This parameter takes effect only when the value of `IsLanguageEnable` is `1`.<br><br>Valid values:<br><br><br>* `0`: Simplified Chinese.<br><br>* `1`: English.<br><br>* `2`: Japanese.<br><br>* `3`: Traditional Chinese.<br><br>* `4`: Korean.<br><br>* `5`: Thai.<br><br>* `6`: Vietnamese.<br><br>* `7`: Arabic.<br><br>* `8`: Turkish.<br><br>* `9`: Spanish.<br><br>* `10`: Indonesian.<br><br>* `11`: Portuguese.<br><br>* `12`: Russian.<br><br>* `13`: Tagalog.<br><br>* `14`: Khmer.<br><br>* `15`: Lao.<br><br>* `16`: Burmese.<br><br>* `17`: Malay.<br><br>* `18`: Hindi.<br><br>* `19`: French.<br><br>* `20`: German.<br><br>* `21`: Italian. |
|SiteTags |Array of [SiteTags](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi) |`-` |List of category tags in the live room. |
|TextSiteTags |Array of [TextSiteTags](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi) |`-` |List of text tags in the live room. |
|AutoStartType |Integer |`0` |The mode for automatically starting the live stream. This parameter takes effect only when the value of `IsAutoStartEnable` is `1`.<br><br>Valid values:<br><br><br>* `0`: Does not automatically start the live stream.<br><br>* `1`: Automatically starts the prerecorded video.<br><br>* `2`: Automatically starts pulling the stream. |
|PreviewVideoId |Long |`431674` |The media library ID of the preview. This parameter takes effect only when the value of `IsPreviewVideoEnable` is `1`. |
|AccountId |Long |`-` |Deprecated. |
|PreviewVideoReviewStatus |Integer |`-` |Deprecated. |
|DefaultSubtitleLanguage |String |`-` |Deprecated. |
|SourceSubtitleLanguage |String |`-` |Deprecated. |
|OpenLiveAvextractorTask |Integer |`-` |Deprecated. |
|IsTimeShift |Integer |`0` |This feature is currently not available. Fixed value: `0` |
|PreviewVideoCoverImage |String |`https://example.image` |The URL of the preview's cover image. |
|PreviewVideoMediaName |String |`Video.mp4` |The name of the preview. |
|IsPreviewPromptEnable |Integer |`1` |Indicates whether the preview text is enabled.<br><br>Valid values:<br><br><br>* `0`: Disabled.<br><br>* `1`: Enabled. |
|PreviewPrompt |String |`The live stream will start soon.` |The preview text. This parameter takes effect only when the value of `IsPreviewPromptEnable` is `1`. |
|IsReservationEnable |Integer |`1` |Indicates whether the reservation feature is enabled.<br><br>Valid values:<br><br><br>* `0`: Disabled.<br><br>* `1`: Enabled. |
|IsReservationSmsEnable |Integer |`1` |Indicates whether the SMS reminder for booking is enabled. This parameter is only valid when the value of `IsReservationEnable` is `1`.<br><br>Valid values:<br><br><br>* `1`: Enabled.<br><br>* `2`: Disabled. |
|ReservationTime |Integer |`300` |Specifies when to send the SMS reminder, in seconds, before the live stream starts.<br><br>Unit: seconds.<br><br>This parameter is only valid when the value of `IsReservationSmsEnable` is `1`. |
|ReservationText |String |`-` |Deprecated. |
|WatermarkPosition |Integer |`0` |The location of the player logo.<br><br>Valid values:<br><br><br>* `0`: In the upper\-right corner of the player.<br><br>* `1`: In the upper\-left corner of the player.<br><br>* `2`: In the lower\-left corner of the player.<br><br>* `3`: In the lower\-right corner of the player. |
|IsReplayBulletChat |Integer |`-` |Deprecated. |
|PresenterChatColor |String |`#FFD58B` |The font color of the host, which follows the RGB color model. |
|IsLiveBulletChat |Integer |`-` |Deprecated. |
|IsBackgroundBlur |Integer |`0` |Indicates whether background blurring is enabled.<br><br>Valid values:<br><br><br>* `0`: Disabled.<br><br>* `1`: Enabled on mobile devices.<br><br>* `2`: Enabled on PCs.<br><br>* `3`: Enabled on PCs and mobile devices. |
|FeedbackMessage |String |`-` |Deprecated. |
|IsFeedbackEnable |Integer |`-` |Deprecated. |
|IsThumbUpNumberEnable |Integer |`1` |Indicates whether the number of likes for the live room is displayed on the viewing page.<br><br>Valid values:<br><br><br>* `0`: Not displayed.<br><br>* `1`: Displayed. |
|SmsLanguage |Integer |`0` |The language of SMS messages.<br><br>Valid values:<br><br><br>* Defaults to Chinese for phone numbers starting with +86 and English for all other numbers.<br><br>* `1`: Chinese.<br><br>* `2`: English.<br><br>* `3`: Both English and Chinese. |
|MobileChatBackgroundColor |String |`#000000` |The background color of comments on mobile devices, which follows the RGB color model. |
|ConfigVersion |Integer |`1` |The configuration version. Fixed value: `1` |
|LiveZone |Integer |`480` |The time zone.<br><br>Valid values:<br><br><br>* `-60`: GMT\-01:00 Ponta del Gada (Portugal).<br><br>* `-120`: GMT\-02:00 Fernando de Noronha (Brazil).<br><br>* `-180`: GMT\-03:00 Brasilia (Brazil).<br><br>* `-240`: GMT\-04:00 Santiago (Chile).<br><br>* `-300`: GMT\-05:00 Washington, D.C. (United States).<br><br>* `-360`: GMT\-06:00 Mexico City (Mexico).<br><br>* `-420`: GMT\-07:00 Denver (United States).<br><br>* `-480`: GMT\-08:00 Vancouver (Canada).<br><br>* `-540`: GMT\-09:00 Alaska (United States).<br><br>* `-570`: GMT\-09:30 Teojae (French Polynesia).<br><br>* `-600`: GMT\-10:00 Hawaii (United States).<br><br>* `-660`: GMT\-11:00 Alofi (Niue).<br><br>* `0`: GMT+00:00 London (United Kingdom).<br><br>* `60`: GMT+01:00 Paris (France).<br><br>* `120`: GMT+02:00 Damascus (Syria).<br><br>* `180`: GMT+03:00 Moscow (Russia).<br><br>* `210`: GMT+03:30 Tehran (Iran).<br><br>* `240`: GMT+04:00 Dubai (United Arab Emirates).<br><br>* `300`: GMT+05:00 New Delhi (India).<br><br>* `330`: GMT+05:30 Mumbai (India).<br><br>* `360`: GMT+06:00 Dhaka (Bangladesh).<br><br>* `390`: GMT+06:30 Yangon (Myanmar).<br><br>* `420`: GMT+07:00 Bangkok (Thailand).<br><br>* `480`: GMT+08:00 Beijing (China).<br><br>* `525`: GMT+08:45 Yukla (Australia).<br><br>* `540`: GMT+09:00 Tokyo (Japan).<br><br>* `570`: GMT+09:30 Darwin (Australia).<br><br>* `600`: GMT+10:00 Canberra (Australia).<br><br>* `630`: GMT+10:30 Lord Howe Island (Australia).<br><br>* `660`: GMT+11:00 Sydney (Australia).<br><br>* `720`: GMT+12:00 Suva (Fiji).<br><br>* `780`: GMT+13:00 Phoenix Islands (Kiribati).<br><br>* `825`: GMT+13:45 Chatham Islands (New Zealand).<br><br>* `840`: GMT+14:00 Christmas Island (Kiribati). |
|RiskWarningSetting |Object of [RiskWarningSetting](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi) |`-` |Configurations of the reminder pop\-up window displayed when viewers enter the live room. |
|IsColorSync |Integer |`1` |Indicates whether color configurations are synchronized to portrait mode.<br><br>Valid values:<br><br><br>* `0`: Not synchronized.<br><br>* `1`: Synchronized. |
|IsPlayerTopEnable |Integer |`0` |Indicates whether the pinned player feature is enabled.<br><br>Valid values:<br><br><br>* `0`: Disabled.<br><br>* `1`: Enabled. |
|PlayerTopType |Array of Integer |`[1,2]` |The terminal where the player is pinned to the top of the page.<br><br>Valid values:<br><br><br>* `0`: Deprecated.<br><br>* `1`: The player is pinned to the top of the page on PCs.<br><br>* `2`: The player is pinned to the top of the page on mobile devices in landscape mode. |
|IsReplayAutoOnlineEnable |Integer |`0` |Indicates whether the playback is automatically released to the viewing page after the live stream ends.<br><br>Valid values:<br><br><br>* `0`: Not automatically released.<br><br>* `1`: Automatically released. |
|IsSDKPlayEnable |Integer |`1` |Indicates whether the player on the viewing page integrated with the Web Viewer SDK is enabled to play live videos.<br><br>Valid values:<br><br><br>* `0`: Disabled. To avoid unnecessary playback, the live stream is disabled at the same time. As a result, viewers cannot watch live videos, regardless of whether they are on the viewing page integrated with the Web Viewer SDK.<br><br>* `1`: Enabled. |
|SDKPlayStatus |Integer |`2` |The live room status displayed on the Web Viewer SDK viewing page. This may differ from the actual room status.<br><br>This parameter is only valid when the value of `IsSDKPlayEnable` is `0`.<br><br>Valid values:<br><br><br>* `2`: Preview.<br><br>* `3`: Playback.<br><br>* `4`: Over. |
|IsVideoChatDisplayed |Integer |`1` |Indicates whether the co\-host feature is enabled on the live streaming page in a web browser.<br><br>Valid values:<br><br><br>* `0`: Disabled.<br><br>* `1`: Enabled. |
|IsSharedAddressDisplayed |Integer |`1` |Indicates whether the viewing page address is displayed on the live streaming page in a web browser.<br><br>Valid values:<br><br><br>* `0`: Not displayed.<br><br>* `1`: Displayed. |
|IsReleaseNoticeDisplayed |Integer |`1` |Indicates whether the lock preview feature is enabled on the live streaming page in a web browser.<br><br>Valid values:<br><br><br>* `0`: Disabled.<br><br>* `1`: Enabled. |
|IsInteractiveEnable |Integer |`0` |Indicates whether the host can manage only the specified interaction tools on the live streaming page in a web browser.<br><br>Valid values:<br><br><br>* `0`: The host can manage all the following interaction tools.<br><br>* Questionnaire<br><br>* Document<br><br>* Check\-in<br><br>* Quiz<br><br>* Lucky draw<br><br>* Announcement<br><br>* `1`: The host can manage only the specified interaction tools. |
|InteractiveShowSetting |Object of [InteractiveShowSetting](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi) |`-` |The interaction tools that the host can manage on the live streaming page in a web browser.<br><br>This parameter takes effect only when the value of `IsInteractiveEnable` is `1`. |
|EndTime |Long |`1666358566` |The end time of the live stream in Unix timestamp format. Unit: seconds. |
|IsAutoEndEnable |Integer |`1` |Indicates whether the feature of automatically ending the live stream at the specified end time is enabled.<br><br>Valid values:<br><br><br>* `0`: Disabled.<br><br>* `1`: Enabled. |


<span id="interactiveshowsetting"></span>
#### InteractiveShowSetting


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|IsQuestionnaireDisplayed |Integer |`0` |Indicates whether the host can manage questionnaires on the live streaming page in a web browser.<br><br>Valid values:<br><br><br>* `0`: The host cannot manage questionnaires.<br><br>* `1`: The host can manage questionnaires. |
|IsDocDisplayed |Integer |`0` |Indicates whether the host can manage documents on the live streaming page in a web browser.<br><br>Valid values:<br><br><br>* `0`: The host cannot manage documents.<br><br>* `1`: The host can manage documents. |
|IsCheckInDisplayed |Integer |`0` |Indicates whether the host can manage check\-ins on the live streaming page in a web browser.<br><br>Valid values:<br><br><br>* `0`: The host cannot manage check\-ins.<br><br>* `1`: The host can manage check\-ins. |
|IsQuizDisplayed |Integer |`0` |Indicates whether the host can manage quizzes on the live streaming page in a web browser.<br><br>Valid values:<br><br><br>* `0`: The host cannot manage quizzes.<br><br>* `1`: The host can manage quizzes. |
|IsLuckDrawDisplayed |Integer |`0` |Indicates whether the host can manage lucky draws on the live streaming page in a web browser.<br><br>Valid values:<br><br><br>* `0`: The host cannot manage lucky draws.<br><br>* `1`: The host can manage lucky draws. |
|IsAnnouncementDisplayed |Integer |`0` |Indicates whether the host can manage announcements on the live streaming page in a web browser.<br><br>Valid values:<br><br><br>* `0`: The host cannot manage announcements.<br><br>* `1`: The host can manage announcements. |


<span id="sitetags"></span>
#### SiteTags


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|Name |String |`Tag A` |The name of the category tag. |
|Value |String |`1` |The category tag value. |
|Index |Integer |`0` |The index of the category tag, which identifies the display order on the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).<br><br>Value range: [0,19]. |
|DbIndex |Integer |`-` |Deprecated. |
|Show |Integer |`-` |Deprecated. |
|Id |Integer |`-` |Deprecated. |


<span id="textsitetags"></span>
#### TextSiteTags


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|Name |String |`Tag B` |The name of the text tag. |
|Value |String |`3` |The text tag value. |
|Index |Integer |`0` |The index of the text tag, which identifies the display order on the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).<br><br>Value range: [0,4]. |
|DbIndex |Integer |`-` |Deprecated. |
|Show |Integer |`-` |Deprecated. |
|Id |Integer |`-` |Deprecated. |


<span id="riskwarningsetting"></span>
#### RiskWarningSetting


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|IsRiskWarningEnable |Integer |`0` |Indicates whether the reminder pop\-up window is enabled.<br><br>Valid values:<br><br><br>* `0`: Disabled.<br><br>* `1`: Enabled. |
|RiskWarningButtonText |String |`Understood` |The button name for the reminder pop\-up window. |
|RiskWarningContent |String |`Welcome to the live room! Please abide by the laws and regulations of the organizer's and your countries and do not send comments that are pornographic, illegal, vulgar, or defamatory in nature. Be a model viewer to others. We politely request that you do not disrupt the good order of the live room by engaging in trolling or other malicious behavior. Use your common sense if and when presented with a private product offer between you and the host.` |The content of the reminder. |
|RiskWarningTitle |String |`Reminder` |The title of the reminder pop\-up window. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetActivityBasicConfigAPI&Version=2020-06-01&ActivityId=17218312****
```


<span id="sample-response"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "GetActivityBasicConfigAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1666121102
    },
     "Result": {
        "ActivityId": 17218312****,
        "Name": "Live Room A",
        "LiveTime": 1666258566,
        "IsBeginLiveEnable": 0, 
        "IsCoverImageEnable": 1,
        "CoverImageUrl": "//example.image",
        "CoverImageUrlDefault": "//example.image",
        "VerticalCoverImageUrl": "//example.image",
        "IsPcBackImageEnable": 1,
        "PcBackImageUrl": "//example.image",
        "PcBackImageUrlDefault": "https://example.image",
        "IsMobileBackImageEnable": 1,
        "MobileBackImageUrl": "//example.image",
        "MobileBackImageUrlDefault": "https://example.imagee",
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
        "IsPreviewPromptEnable": 1,
        "PreviewPrompt": "The live stream will start soon.",
        "IsReservationEnable": 1,
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
        "IsColorSync": 1,
        "RiskWarningSetting": {
            "IsRiskWarningEnable": 0,
            "RiskWarningTitle": "",
            "RiskWarningContent": "",
            "RiskWarningButtonText": ""
        },
        "IsSDKPlayEnable": 1,
        "SDKPlayStatus": 2,
        "IsVideoChatDisplayed": 1,
        "IsSharedAddressDisplayed": 1,
        "EndTime": 1666358566,
        "IsAutoEndEnable": 1,
        "IsReleaseNoticeDisplayed": 1,
        "IsInteractiveEnable": 1,
        "InteractiveShowSetting": {
            "IsQuestionnaireDisplayed": 1,
            "IsDocDisplayed": 1,
            "IsCheckInDisplayed": 1,
            "IsQuizDisplayed": 0,
            "IsLuckDrawDisplayed": 0,
            "IsAnnouncementDisplayed": 0
        }
    }
}
```


<span id="error-codes"></span>
## Error codes

For a list of shared error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).
