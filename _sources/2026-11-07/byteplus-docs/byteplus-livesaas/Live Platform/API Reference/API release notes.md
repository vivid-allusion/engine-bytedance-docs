---
title: "API release notes"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-api-release-notes"
---

The BytePlus Live API release notes provide a comprehensive and chronological log of all API and callback updates. You can use this document to track new features, breaking changes, and enhancements, ensuring your application remains compatible and up\-to\-date.

<span id="7b8c2a41"></span>
## July 2026


|API/Callback |Description |Release Date |
|---|---|---|
|[GetActivityProductAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityproductapi) |Added the `UAInfo` and `DirectUrls` parameters to support the multi\-environment direct URL feature for product cards. |2026\-07\-23 |
|[UpdateActivityProductAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivityproductapi) |Added the `UAInfo` and `DirectUrls` parameters to support the multi\-environment direct URL feature for product cards. |2026\-07\-23 |
|BytePlus Live API Endpoint |Updated the recommended BytePlus Live API endpoint to `https://livesaas.byteplusapi.com`. The original endpoint, `https://open.byteplusapi.com`, remains available. |2026\-07\-10 |


<span id="april-2026"></span>
## April 2026


|API/Callback |Description |Release Date |
|---|---|---|
|[GetVoteListAPI](https://docs.byteplus.com/docs/byteplus-livesaas/GetVoteListAPI) |Call `GetVoteListAPI` to obtain the vote configuration information for a specified live room. |2026\-04\-01 |
|[GetVoteStatisticsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/GetVoteStatisticsAPI) |Call `GetVoteStatisticsAPI` to get the voting data of a live room. |2026\-04\-01 |
|[UpdatePresenterAwardConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/UpdateAwardConfig) |Call `UpdatePresenterAwardConfigAPI` to add, update, or delete a real\-time lucky draw for a live room. |2026\-04\-01 |
|[ListAwardConfigsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/ListAwardConfigs) |Call `ListAwardConfigsAPI` to obtain the configuration details of lucky draws. |2026\-04\-01 |
|[SendAward](https://docs.byteplus.com/docs/byteplus-livesaas/SendAward) |Call `SendAward` to start a real\-time lucky draw in a live room. |2026\-04\-01 |
|[WithdrawAward](https://docs.byteplus.com/docs/byteplus-livesaas/WithdrawAward) |Call `WithdrawAward` to withdraw a real\-time lucky draw from a live room. Note that a withdrawn lucky draw cannot be sent again or updated. |2026\-04\-01 |
|[UpdateActivityQuizConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/UpdateActivityQuizConfig) |Call `UpdateActivityQuizConfigAPI` to update the configuration information for unsent quizzes in a specified live room. |2026\-04\-01 |
|[ListActivityQuizConfigsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/ListActivityQuizConfigs) |Call `ListActivityQuizConfigsAPI` to obtain the quiz configuration information for a specified live room. |2026\-04\-01 |
|[ListQuizStatisticsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/ListQuizStatisticsAPI) |Call `ListQuizStatisticsAPI` to retrieve a paginated list of quizzes and their engagement statistics. The data includes the number of participants, the count of correct answers, and other relevant details for a specified live room. |2026\-04\-01 |
|[GetQuizDataAPI](https://docs.byteplus.com/docs/byteplus-livesaas/GetQuizDataAPI) |Call `GetQuizDataAPI` to obtain detailed information about a specified quiz in a live streaming room. This includes the number of participants, the number of correct answers, and the content of each option. |2026\-04\-01 |
|[GetCheckInListAPI](https://docs.byteplus.com/docs/byteplus-livesaas/GetCheckInListAPI) |Call `GetCheckInListAPI` to obtain all check\-in or specified check\-in information for the designated live room, including check\-in ID, number of participants, check\-in duration, and more. |2026\-04\-01 |
|[GetCheckInRecordStatisticsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/GetCheckInRecordStatisticsAPI) |Call `GetCheckInRecordStatisticsAPI` to obtain the check\-in records for a specific live room. |2026\-04\-01 |
|[UpdateFloatingAdvertisementAPI](https://docs.byteplus.com/docs/byteplus-livesaas/UpdateFloatingAdvertisement) |Call `UpdateFloatingAdvertisementAPI` to update the status, link, and other configuration details of a floating advertisement in a specified live room. |2026\-04\-01 |
|[GetTaskAwardItemListAPI](https://docs.byteplus.com/docs/byteplus-livesaas/GetTaskAwardItemListAPI) |Call `GetTaskAwardItemListAPI` to get the list of prizes for the watch time\-based lucky draw that has been sent in the live room. |2026\-04\-01 |
|[ListAwardRecordStatisticsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/ListAwardRecordStatisticsAPI) |Call `ListAwardRecordStatisticsAPI` to obtain the list of participating or winning viewers for a specific lucky draw in a live streaming room. |2026\-04\-01 |
|[ActivityAwardInfoCallBack](https://docs.byteplus.com/docs/byteplus-livesaas/ActivityAwardInfoCallBack) |When a real\-time lucky draw is held, BytePlus Live sends a POST request to your custom URL and passes data such as the live room ID, prize information, and winner information in the body. |2026\-04\-01 |
|[ActivityTaskAwardInfoCallBack](https://docs.byteplus.com/docs/byteplus-livesaas/ActivityTaskAwardInfoCallBack) |When a user participates in a watch time\-based lucky draw and a prize is won, BytePlus Live sends a POST request to your custom URL and passes the live room ID, prize information, and winner information in the body. |2026\-04\-01 |
|[CheckinStatusModifyCallback](https://docs.byteplus.com/docs/byteplus-livesaas/CheckinStatusModifyCallback) |When check\-in events occur, such as check\-in creation, deletion, sending, or the deadline being reached, BytePlus Live sends a POST request to your custom URL and passes the live room ID and updated check\-in status in the body. |2026\-04\-01 |


<span id="january-2026"></span>
## January 2026


|API/Callback |Description |Release Date |
|---|---|---|
|[ActivityAutoReplayCallBack](https://docs.byteplus.com/docs/byteplus-livesaas/activityautoreplaycallback) |Added the parameters `LiveStartTime` and `LiveEndTime` to show the start time and the end time of a live stream corresponding to the playback video. |2026\-01\-27 |
|[ForbidLiveStreamAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-forbidlivestreamapi) |This API has been deprecated. Please contact technical support if you need assistance. |2026\-01\-14 |


<span id="november-2025"></span>
## November 2025


|API/Callback |Description |Release Date |
|---|---|---|
|[UpdateActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitybasicconfigapi) |Added the following values for the `LanguageType`:<br><br><br>* `13`: Tagalog.<br><br>* `14`: Khmer.<br><br>* `15`: Lao.<br><br>* `16`: Burmese.<br><br>* `17`: Malay.<br><br>* `18`: Hindi.<br><br>* `19`: French.<br><br>* `20`: German.<br><br>* `21`: Italian. |2025\-11\-12 |
|[GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi) | | |
|[UpdateAwardItem](https://docs.byteplus.com/en/docs/byteplus-livesaas/updateawarditem) |Supports managing prizes for your account, including adding, updating, deleting, and retrieving prize information. |2025\-11\-12 |
|[GetAwardItemList](https://docs.byteplus.com/en/docs/byteplus-livesaas/getawarditemlist) | |2025\-11\-12 |
|[DeleteAwardItem](https://docs.byteplus.com/en/docs/byteplus-livesaas/deleteawarditem) | |2025\-11\-12 |


<span id="august-2025"></span>
## August 2025


|API/Callback |Description |Release Date |
|---|---|---|
|[UpdateActivityProductAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivityproductapi) |The character limit for `Title` and `Remark` in product cards is increased to 3315. |2025\-08\-12 |


<span id="july-2025"></span>
## July 2025


|API/Callback |Description |Release Date |
|---|---|---|
|[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) |* Added the request parameter `FollowerUserName` to get live rooms created by a specific account.<br><br>* Added the response parameters `VerticalCoverImage` and `SubAccountName` to get the URL of the live room's cover image in portrait mode and the account used to create the live room. |2025\-07\-17 |
|[GetLoginLivesaasSts](https://docs.byteplus.com/en/docs/byteplus-livesaas/getloginlivesaassts) |Supports getting the STS signature for a specific account in BytePlus Live. This signature allows you to use an iframe to embed functional modules from the BytePlus Live console into your page. |2025\-07\-15 |
|[ListActivityMediaAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/listactivitymediaapi) |Support for getting information of videos in the video library or temporary storage under the media library, including the video ID and name. |2025\-07\-15 |
|[TempToMediaActivityMediaAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/temptomediaactivitymediaapi) |Support for transferring videos from temporary storage to a specific category in the video library for permanent storage. |2025\-07\-15 |
|[GetVideoLibraryFolderTree](https://docs.byteplus.com/en/docs/byteplus-livesaas/getvideolibraryfoldertree) |Support for getting information about the default category or a specific category and their subcategories under your account. |2025\-07\-15 |


<span id="february-2025"></span>
## February 2025


|API/Callback |Description |Release Date |
|---|---|---|
|[ListActivityFeedInfosAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/listactivityfeedinfosapi) |Added the request parameters `SortBy`, `SortOrder`, and `SiteTagNews` to sort live rooms based on specific rules and order, and filter live rooms based on category tag values. |2025\-02\-25 |
|[ExplainProduct](https://docs.byteplus.com/en/docs/byteplus-livesaas/explainproduct) |Supports pinning a product to the top of the menu and displaying it in a floating window. You can also unpin the product to restore it to its original position and remove it from the floating window. |2025\-02\-20 |
|[ActivityExplainProductCallBack](https://docs.byteplus.com/docs/byteplus-livesaas/activityexplainproductcallBack) |Added the callback `ActivityExplainProductCallBack`, which is triggered when a product in your live room is in any of the following situations:<br><br><br>* Pinned to the top of the menu and displayed in a floating window on the viewing page.<br><br>* Restored to its original position under the menu and no longer displayed in a floating window on the viewing page. |2025\-02\-20 |


<span id="january-2025"></span>
## January 2025


|API/Callback |Description |Release Date |
|---|---|---|
|[ListHostAccounts](https://docs.byteplus.com/en/docs/byteplus-livesaas/listhostaccounts) |Added the request parameter `ExternalPlatformId` to filter host accounts based on the external platform ID. |2025\-01\-16 |


<span id="december-2024"></span>
## December 2024


|API/Callback |Description |Release Date |
|---|---|---|
|[ListActivityFeedInfosAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/listactivityfeedinfosapi) |Added the response parameter `SiteTags` to get the list of category tags in each live room. |2024\-12\-05 |


<span id="november-2024"></span>
## November 2024


|API/Callback |Description |Release Date |
|---|---|---|
|[ListActivityProductCommons](https://docs.byteplus.com/en/docs/byteplus-livesaas/listactivityproductcommons) |Support for getting the product library information of one or more live rooms at a time. |2024\-11\-21 |
|[UpdateHostAccount](https://docs.byteplus.com/en/docs/byteplus-livesaas/updatehostaccount) |Support for adding a host account, updating the information of an existing host account, deleting a host account, and getting information of host accounts under your account. |2024\-11\-07 |
|[DeleteHostAccount](https://docs.byteplus.com/en/docs/byteplus-livesaas/deletehostaccount) | |2024\-11\-07 |
|[ListHostAccounts](https://docs.byteplus.com/en/docs/byteplus-livesaas/listhostaccounts) | |2024\-11\-07 |
|[UpdateActivityHostAccount](https://docs.byteplus.com/en/docs/byteplus-livesaas/updateactivityhostaccount) |Support for updating the host account associated with a live room and configuring whether to enable the account settings feature in the live room. |2024\-11\-07 |
|[GetBusinessAccountInfoAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getbusinessaccountinfoapi) |Added the response parameter `IsFollowEnable` to indicate whether viewers are allowed to follow the host on the viewing page. |2024\-11\-07 |
|[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) |Added the request parameters `SortBy` and `SortOrder` to set the rules and order for sorting the returned live rooms. |2024\-11\-07 |


<span id="october-2024"></span>
## October 2024


|API/Callback |Description |Release Date |
|---|---|---|
|[CreateActivityAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2) |Added the request parameter IsBeginLiveEnable to specify whether to enable the live stream start time feature. |2024\-10\-10 |
|[GetActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityapi) |Added the response parameter IsBeginLiveEnable to indicate whether the live stream start time feature is enabled. |2024\-10\-10 |
|[UpdateActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitybasicconfigapi) |* Added the request parameter IsBeginLiveEnable to specify whether to enable the live stream start time feature.<br><br>* Added the request parameter `IsInteractiveEnable` to specify whether to allow the host to manage only the specified interaction tools on the live streaming page in a web browser.<br><br>* Added the request parameter `InteractiveShowSetting` to specify the interaction tools that the host can manage on the live streaming page in a web browser. |2024\-10\-10 |
|[GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi) |* Added the response parameter `IsBeginLiveEnable` to indicate whether the feature of live stream start time is enabled. Once enabled, you can only start a live stream after the specified start time.<br><br>* Added the response parameter `IsInteractiveEnable` to indicate whether the host can manage only the specified interaction tools on the live streaming page in a web browser.<br><br>* Added the response parameter `InteractiveShowSetting` to indicate the interaction tools that the host can manage on the live streaming page in a web browser. |2024\-10\-10 |
|[ForbidLiveStreamAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-forbidlivestreamapi) |Added the error code `200027`. |2024\-10\-10 |
|[ResumeLiveStreamAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-resumelivestreamapi) |Added the error code `200027`. |2024\-10\-10 |


<span id="september-2024"></span>
## September 2024


|API/Callback |Description |Release Date |
|---|---|---|
|[ListActivityFeedInfosAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/listactivityfeedinfosapi) |Support for getting the basic information of all existing live rooms under your BytePlus account, including those created by IAM users, including the cover image, virtual popularity, host account, and creation time. |2024\-09\-26 |


<span id="august-2024"></span>
## August 2024


|API/Callback |Description |Release Date |
|---|---|---|
|[CreateActivityProductLibrary](https://docs.byteplus.com/en/docs/byteplus-livesaas/createactivityproductlibrary) |Support for adding one or more product libraries to a specific live room. Then, you can get products from the product library of Shopify or your own system in the live room. |2024\-08\-15 |
|[UpdateActivityProductLibrary](https://docs.byteplus.com/en/docs/byteplus-livesaas/updateactivityproductlibrary) |Support for updating the information of product libraries in a specific live room, including the name, type, and configurations of product libraries. |2024\-08\-15 |
|[DeleteActivityProductLibrary](https://docs.byteplus.com/en/docs/byteplus-livesaas/deleteactivityproductlibrary) |Support for deleting one or more product libraries in a specific live room. |2024\-08\-15 |
|[GetActivityProductCommonConfig](https://docs.byteplus.com/en/docs/byteplus-livesaas/getactivityproductcommonconfig) |Support for getting the configurations of products in a specified live room, including the ID, name, type, and configurations of product libraries. |2024\-08\-15 |
|[GetActivityProductAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityproductapi) |Added the response parameter `ExternalProductId`. |2024\-08\-15 |
|[UpdateActivityProductAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivityproductapi) |Added the request parameter `ExternalProductId`. |2024\-08\-15 |


<span id="july-2024"></span>
## July 2024


|API/Callback |Description |Release Date |
|---|---|---|
|[ActivityClickReservationCallBack](https://docs.byteplus.com/docs/byteplus-livesaas/activityclickreservationcallBack) |Added the callback `ActivityClickReservationCallBack`. |2024\-07\-23 |
|[GetActivityReservationAPIV2](https://docs.byteplus.com/en/docs/byteplus-livesaas/getactivityreservationapiv2) |Added the API `GetActivityReservationAPIV2`. |2024\-07\-23 |


<span id="june-2024"></span>
## June 2024


|API/Callback |Description |Release Date |
|---|---|---|
|[CreateActivityAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2) |Added the request parameters `EndTime` and `IsAutoEndEnable`. |2024\-06\-25 |
|[UpdateActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitybasicconfigapi) |Added the request parameters `EndTime` and `IsAutoEndEnable`. |2024\-06\-25 |
|[GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi) |Added the response parameters `EndTime` and `IsAutoEndEnable`. |2024\-06\-25 |
|[GetActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityapi) |Added the response parameters `EndTime` and `IsAutoEndEnable`. |2024\-06\-25 |
|[ForbidLiveStreamAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-forbidlivestreamapi) |Changed both the maximum value and default value of the `ForbidTime` parameter from 7 × 24 × 60 × 60 to 31 × 24 × 60 × 60. |2024\-06\-12 |
|[ListUploadedFilesAPI](https://docs.byteplus.com/docs/byteplus-livesaas/listuploadedfilesapi) |Support for getting the list of files uploaded on the live streaming page in a web browser or sent under the menu for interaction tools in a specific live room. |2024\-06\-06 |
|[GetUploadedFilesDownloadUrlAPI](https://docs.byteplus.com/docs/byteplus-livesaas/getuploadedfilesdownloadurlapi) |Support for getting the download URLs of files uploaded on the live streaming page in a web browser or sent under the menu for interaction tools in a specific live room. |2024\-06\-06 |
|[ListQuestionChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/listquestionchatapi) |Support for getting questions under the menu for Q&A. |2024\-06\-06 |
|[ListAnswerChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/listanswerchatapi) |Support for getting replies to specific questions under the menu for Q&A. |2024\-06\-06 |
|[ActivityQuestionChatCallBack](https://docs.byteplus.com/docs/byteplus-livesaas/activityquestionchatcallback) |When a user sends a question under the menu for Q&A, BytePlus Live sends a POST request to your custom URL and passes the question data in the body. |2024\-06\-06 |


<span id="may-2024"></span>
## May 2024


|API/Callback |Description |Release Date |
|---|---|---|
|[GetWebPushLiveClientWithExpiryAPI](https://docs.byteplus.com/docs/byteplus-livesaas/getwebpushliveclientwithexpiryapi) |Support for getting the URL for the live streaming page of a live room, allowing the host to start a live stream from a web browser without the need for logging in. The returned URL expires after a specified period. |2024\-05\-31 |
|[GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi) |Added the response parameters `IsVideoChatDisplayed`, `IsSharedAddressDisplayed`, and `IsReleaseNoticeDisplayed`. |2024\-05\-31 |
|[UpdateActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitybasicconfigapi) |Added the request parameters `IsVideoChatDisplayed`, `IsSharedAddressDisplayed`, and `IsReleaseNoticeDisplayed`. |2024\-05\-31 |
|[DelActivityAntidirtAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-delactivityantidirtapi) |Added the request parameter `DeleteAll`. |2024\-05\-10 |
|[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) |Added the request parameters `HostAccountId`, `HostAccountName`, and `LiveMode`, as well as response parameters `HostAccountId`, `HostAccountName`, and `LiveMode`. |2024\-05\-10 |
|[ListUserBehaviorDataAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listuserbehaviordataapi) |Added the request parameter `ScrollId`, as well as response parameters `ScrollId` and `SilenceStatus`. |2024\-05\-10 |
|[PollingChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-pollingchatapi) |Added the response parameter `IsTipOff`. |2024\-05\-10 |
|[GetActivityProductAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityproductapi) |Added the response parameters `ProductsPosition` and `DefaultRedirectImage`. |2024\-05\-10 |
|[GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi) |Added the request parameters `InviteToken`, `AvatarUrl`, and `CustomComment`. |2024\-05\-10 |
|[UpdateActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitybasicconfigapi) |Added the request parameter `IsReservationSmsEnable`. |2024\-05\-10 |
|[GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi) |Added the response parameter `IsReservationSmsEnable`. |2024\-05\-10 |
|[GetActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityapi) |Added the response parameters `VerticalCoverImage` and `LiveMode`. |2024\-05\-10 |
|[CreateActivityAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2) |Added the request parameter `LiveMode`. |2024\-05\-10 |


<span id="february-2024"></span>
## February 2024


|**API/Callback** |**Description** |**Release Date** |
|---|---|---|
|[GetActivityProductAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityproductapi) |Added the response parameter `TagName`. |2024\-02\-29 |
|[UpdateActivityProductAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivityproductapi) |Added the request parameter `TagName`. |2024\-02\-29 |
|[GetAccountTemplateAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getaccounttemplateapi) |Supports getting the list of live room templates under your BytePlus account. |2024\-02\-29 |


<span id="january-2024"></span>
## January 2024


|**API/Callback** |**Description** |**Release Date** |
|---|---|---|
|[GetActivityQualityDataAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityqualitydataapi) |Supports retrieving live streaming quality data for a live room within a specific time range. |2024\-01\-23 |
|[GetAccountQualityDataAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getaccountqualitydataapi) |Support for getting the data on the live streaming quality of all the live rooms under your BytePlus account in a specific time range. |2024\-01\-23 |


<span id="november-2023"></span>
## November 2023


|**API/Callback** |**Description** |**Release Date** |
|---|---|---|
|[UpdateBusinessAccountInfoAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updatebusinessaccountinfoapi) |Support for updating the brand account information in a live room. |2023\-12\-21 |
|[GetBusinessAccountInfoAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getbusinessaccountinfoapi) |Support for getting the brand account information in a live room. |2023\-12\-21 |
|[GetAccountDataByTimeIntervalAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getaccountdatabyTimeintervalapi) |Support for getting the data for all live rooms under your BytePlus account, including cumulative views and unique viewers. |2023\-11\-30 |
|[ListActivityDetailAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivitydetailapi) |Support for getting the data for specific live rooms under your BytePlus account, including cumulative live duration and average watch duration per viewer. |2023\-11\-30 |
|[UpdateActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitybasicconfigapi) |Added the request parameter `VerticalCoverImageUrl`. |2023\-11\-30 |
|[GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi) |Added the response parameter `VerticalCoverImageUrl`. |2023\-11\-30 |
