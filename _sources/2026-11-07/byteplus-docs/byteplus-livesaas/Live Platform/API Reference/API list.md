---
title: "API list"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-API-list"
---

To integrate BytePlus Live features into your application, you can use this comprehensive API reference. This document lists all available APIs, categorized by function such as Live Rooms, Live Streaming, and Insights, to help you quickly locate the specific endpoint you need.

<span id="live-rooms"></span>
## Live rooms


|**API** |**Description** |
|---|---|
|[CreateActivityAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2) |Creates a live room for live activities. |
|[DeleteActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-deleteactivityapi) |Deletes a specific live room. |
|[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) |Gets the basic information of all the existing live rooms under your BytePlus account. |
|[UpdateActivityStatusAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitystatusapi) |Updates the status of a live room. You can restore the live room to the **Preview** status, lock the preview, and unlock the preview. |
|[UpdatePullToPushAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updatepulltopushapi) |Starts or stops pulling a stream for a live room from a specified URL. |
|[GetActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityapi) |Gets the basic information of a live room, such as its status and viewing page address. |
|[GetStreamsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getstreamsapi) |Gets the information required for pushing a stream to a live room, or pulling a stream from a third\-party platform. |
|[GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi) |Gets the basic configurations of a live room, such as the background image and preview. |
|[UpdateActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitybasicconfigapi) |Updates the basic configurations of a live room, such as the background image and preview. |
|[UpdateLoopVideoAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateloopvideoapi) |Edits the looped video of a live room. |
|[UpdateLoopVideoStatusAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateloopvideostatusapi) |Enables or disables looped playback. |
|[ForbidLiveStreamAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-forbidlivestreamapi) |Forbids streams of specific live sources in a live room. After a stream is forbidden, viewers can no longer watch this stream, and no playback will be generated for it. |
|[ResumeLiveStreamAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-resumelivestreamapi) |Resumes forbidden streams of specific live sources in a live room. |
|[GetLiveStreamForbidStatusAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getlivestreamforbidstatusapi) |Checks whether the stream of a specific live source in a live room is forbidden. |
|[GetAccountTemplateAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getaccounttemplateapi) |Gets the list of live room templates under your BytePlus account. |
|[ListUploadedFilesAPI](https://docs.byteplus.com/docs/byteplus-livesaas/listuploadedfilesapi) |Gets the list of files uploaded on the live streaming page in a web browser or shared via the interaction tools menu in a specific live room. To get the download URL of a file, you can use the file ID from the response to call [GetUploadedFilesDownloadUrlAPI](https://docs.byteplus.com/docs/byteplus-livesaas/getuploadedfilesdownloadurlapi). |
|[GetUploadedFilesDownloadUrlAPI](https://docs.byteplus.com/docs/byteplus-livesaas/getuploadedfilesdownloadurlapi) |Gets the download URLs of files uploaded on the live streaming page in a web browser or shared via the interaction tools menu in a specific live room. |
|[ListActivityFeedInfosAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/listactivityfeedinfosapi) |Gets the basic information of all the existing live rooms under your BytePlus account and IAM users, including the cover image, virtual popularity, host account, and creation time. |


<span id="live-streaming"></span>
## Live streaming


|**API** |**Description** |
|---|---|
|[GetTemporaryLoginTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-gettemporarylogintokenapi) |Gets the secret key of a live room, which is used to start a live stream. |
|[GetWebPushLiveClientAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getwebpushliveclientapi) |Gets the URL for the live streaming page of a live room, allowing the host to start a live stream from a web browser without logging in. |
|[GetWebPushLiveClientWithExpiryAPI](https://docs.byteplus.com/docs/byteplus-livesaas/getwebpushliveclientwithexpiryapi) |Gets the URL for the live streaming page of a live room, allowing the host to start a live stream from a web browser without logging in. The returned URL expires after a specified time period. |


<span id="playbacks"></span>
## Playbacks


|**API** |**Description** |
|---|---|
|[UploadReplayAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-uploadreplayapi) |Binds a video to a live room to serve as its playback. You must first upload the video to the media library before performing the operation. |
|[ListMediasAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listmediasapi) |Gets the information of videos on the playback list of the current live room. |
|[UpdateMediaOnlineStatusAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updatemediaonlinestatusapi) |Releases, withdraws, or removes a playback. You must first upload a video as the playback before performing the operation. |
|[DeleteMediaAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-deletemediaapi) |Deletes a video from the playback list of a live room. |
|[DeleteMediasAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-deletemediasapi) |Deletes at most 100 videos at a time from the playback list of a live room. |


<span id="sensitive-words"></span>
## Sensitive words


|**API** |**Description** |
|---|---|
|[AddActivityAntidirtAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-addactivityantidirtapi) |Adds sensitive words to a live room. |
|[GetActivityAntidirtAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityantidirtapi) |Gets the list of sensitive words configured for a live room. You can choose to get all sensitive words or sensitive words containing specific keywords. |
|[DelActivityAntidirtAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-delactivityantidirtapi) |Deletes sensitive words from a live room. |


<span id="insights"></span>
## Insights


|**API** |**Description** |
|---|---|
|[GetPageWatchDataAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getpagewatchdataapi) |Gets the basic data of a live room, including page views, unique page views, total view duration, and more. Data is updated every five minutes. |
|[GetAdvertisementDataAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getadvertisementdataapi) |Gets the marketing data of a live room. |
|[ListUserBehaviorDataAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listuserbehaviordataapi) |Gets the viewer behavior data of a live room. |
|[ListQuestionnaireAnswerDataAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listquestionnaireanswerdataapi) |Gets the answers to a questionnaire of a live room (A maximum of 10,000 results can be queried). |
|[ListQuestionnaireDataAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listquestionnairedataapi) |Gets the questionnaire data of a live room. |
|[ListAnActivityStartAndEndTimeAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listanactivitystartandendtimeapi) |Gets the start and end time of each live stream in a live room. |
|[GetAccountDataByTimeIntervalAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getaccountdatabyTimeintervalapi) |Gets the data for all live rooms under your BytePlus account, including cumulative views and unique viewers. |
|[ListActivityDetailAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivitydetailapi) |Gets the data for specific live rooms under your BytePlus account, including total live duration and average watch time. |
|[GetActivityQualityDataAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityqualitydataapi) |Gets the data on the live streaming quality of a live room in a specific time range. |
|[GetAccountQualityDataAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getaccountqualitydataapi) |Gets the data on the live streaming quality of all the live rooms under your BytePlus account in a specific time range. |
|[GetActivityReservationAPIV2](https://docs.byteplus.com/en/docs/byteplus-livesaas/getactivityreservationapiv2) |Gets the booking information of a specific live room. |


<span id="comments"></span>
## Comments


|**API** |**Description** |
|---|---|
|[PresenterChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-presenterchatapi) |Sends a comment as the host in a live room. |
|[PollingChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-pollingchatapi) |Gets comments in a live room. |
|[GetHotChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-gethotchatapi) |Gets top comments of a live room. BytePlus Live identifies a comment as a top comment if it receives a high number of likes. |
|[GetTopChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-gettopchatapi) |Gets the comment pinned to the top of the chat area. |
|[DeleteChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-deletechatapi) |Deletes certain comments from a live room. |
|[LikeChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-likechatapi) |Likes a comment. |
|[TopChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-topchatapi) |Pins a comment to the top of the chat area. |
|[EmptyChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-emptychatapi) |Clears all the comments of a live room. |
|[UpdateChatReviewStatusAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updatechatreviewstatusapi) |Enables or disables the chat review feature. |
|[ConfirmReviewChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-confirmreviewchatapi) |Approves a comment. |
|[SilenceUserAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-silenceuserapi) |Prohibits certain viewers of a live room from sending comments. |
|[GetSilenceUserListAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsilenceuserlistapi) |Gets the list of viewers prohibited from sending comments. |


<span id="menus"></span>
## Menus


|**API** |**Description** |
|---|---|
|[GetActivityMenuAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitymenuapi) |Gets the list of menus in a live room. |
|[UpdateActivityMenuAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitymenuapi) |Updates the menu of a live room. |
|[GetActivityProductAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityproductapi) |Gets the configurations of product cards in a live room. |
|[UpdateActivityProductAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivityproductapi) |Updates the configurations of product cards in a live room. |
|[ExplainProduct](https://docs.byteplus.com/en/docs/byteplus-livesaas/explainproduct) |Pins a product to the top of the menu and displays it in a floating window on the viewing page, or restores the product to its original position in the menu and removes it from the floating window display on the viewing page. |
|[CreateActivityProductLibrary](https://docs.byteplus.com/en/docs/byteplus-livesaas/createactivityproductlibrary) |Adds one or more product libraries to a specific live room. Then, you can get products from the product library of Shopify or your own system in the live room. |
|[UpdateActivityProductLibrary](https://docs.byteplus.com/en/docs/byteplus-livesaas/updateactivityproductlibrary) |Updates the information of product libraries in a specific live room, including the name, type, and configurations of product libraries. |
|[DeleteActivityProductLibrary](https://docs.byteplus.com/en/docs/byteplus-livesaas/deleteactivityproductlibrary) |Deletes one or more product libraries in a specific live room. |
|[GetActivityProductCommonConfig](https://docs.byteplus.com/en/docs/byteplus-livesaas/getactivityproductcommonconfig) |Gets the configurations of products in a specified live room, including the ID, name, type, and configurations of product libraries. |
|[ListActivityProductCommons](https://docs.byteplus.com/en/docs/byteplus-livesaas/listactivityproductcommons) |Gets the product library information of one or more live rooms at a time. |
|[UpdatePresenterNameAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updatepresenternameapi) |Updates the host nickname used when sending a comment. |
|[UpdateBulletScreensSwitchAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updatebulletscreensswitchapi) |Configures whether to display the bullet comment switch on the viewing page. |
|[ListQuestionChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/listquestionchatapi) |Gets questions from the Q&A menu, sorted by the number of likes or sent time, with the most popular or recent questions returned first. To get replies to questions, you can use the question ID from the response to call [ListAnswerChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/listanswerchatapi). |
|[ListAnswerChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/listanswerchatapi) |Gets replies to specific questions from the Q&A menu, sorted by the number of likes or sent time, with the most popular or recent replies to a question returned first. |


<span id="viewing-restrictions"></span>
## Viewing restrictions


|**API** |**Description** |
|---|---|
|[UpdateCustomizationViewPermissionAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updatecustomizationviewpermissionapi) |Updates the login link for viewing and commenting restrictions. |


<span id="promotion"></span>
## Promotion


|**API** |**Description** |
|---|---|
|[ListLivePromotionsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listlivepromotionsapi) |Gets the list of third\-party platforms for live stream promotion added in a live room. |
|[AddLivePromotionsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-addlivepromotionsapi) |Adds multiple third\-party platforms at a time to simulcast a live stream from a live room to these platforms. After the live room starts a live stream, BytePlus Live pushes the live stream to platforms enabled for live stream promotion. |
|[UpdateLivePromotionsStatusAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updatelivepromotionsstatusapi) |Updates the distribution status of a third\-party platform in a live room to specify whether the platform is enabled for live stream promotion. |
|[DeleteLivePromotionsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-deletelivepromotionsapi) |Deletes a third\-party platform for live stream promotion in a live room. |
|[UpdateHostAccount](https://docs.byteplus.com/en/docs/byteplus-livesaas/updatehostaccount) |Adds a host account or updates the information of an existing host account under your account. |
|[DeleteHostAccount](https://docs.byteplus.com/en/docs/byteplus-livesaas/deletehostaccount) |Deletes a specific host account under your account. |
|[ListHostAccounts](https://docs.byteplus.com/en/docs/byteplus-livesaas/listhostaccounts) |Gets information such as the ID, name, and avatar URL of host accounts under your account. |
|[UpdateActivityHostAccount](https://docs.byteplus.com/en/docs/byteplus-livesaas/updateactivityhostaccount) |Updates the host account associated with a specific live room and configures whether to enable the account settings feature in the live room. |
|[GetBusinessAccountInfoAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getbusinessaccountinfoapi) |Gets information such as the ID, name, and avatar URL of the host account associated with a specific live room. |


<span id="interaction-tools"></span>
## Interaction tools


|**API** |**Description** |
|---|---|
|[GetVoteListAPI](https://docs.byteplus.com/docs/byteplus-livesaas/GetVoteListAPI) |Call `GetVoteListAPI` to obtain the vote configuration information for a specified live room. |
|[GetVoteStatisticsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/GetVoteStatisticsAPI) |Call `GetVoteStatisticsAPI` to get the voting data of a live room. |
|[UpdatePresenterAwardConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/UpdateAwardConfig) |Call `UpdatePresenterAwardConfigAPI` to add, update, or delete a real\-time lucky draw for a live room. |
|[ListAwardConfigsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/ListAwardConfigs) |Call `ListAwardConfigsAPI` to obtain the configuration details of lucky draws. |
|[SendAward](https://docs.byteplus.com/docs/byteplus-livesaas/SendAward) |Call `SendAward` to start a real\-time lucky draw in a live room. |
|[WithdrawAward](https://docs.byteplus.com/docs/byteplus-livesaas/WithdrawAward) |Call `WithdrawAward` to withdraw a real\-time lucky draw from a live room. Note that a withdrawn lucky draw cannot be sent again or updated. |
|[UpdateActivityQuizConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/UpdateActivityQuizConfig) |Call `UpdateActivityQuizConfigAPI` to update the configuration information for unsent quizzes in a specified live room. |
|[ListActivityQuizConfigsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/ListActivityQuizConfigs) |Call `ListActivityQuizConfigsAPI` to obtain the quiz configuration information for a specified live room. |
|[ListQuizStatisticsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/ListQuizStatisticsAPI) |Call `ListQuizStatisticsAPI` to retrieve a paginated list of quizzes and their engagement statistics. The data includes the number of participants, the count of correct answers, and other relevant details for a specified live room. |
|[GetQuizDataAPI](https://docs.byteplus.com/docs/byteplus-livesaas/GetQuizDataAPI) |Call `GetQuizDataAPI` to obtain detailed information about a specified quiz in a live streaming room. This includes the number of participants, the number of correct answers, and the content of each option. |
|[GetCheckInListAPI](https://docs.byteplus.com/docs/byteplus-livesaas/GetCheckInListAPI) |Call `GetCheckInListAPI` to obtain all check\-in or specified check\-in information for the designated live room, including check\-in ID, number of participants, check\-in duration, and more. |
|[GetCheckInRecordStatisticsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/GetCheckInRecordStatisticsAPI) |Call `GetCheckInRecordStatisticsAPI` to obtain the check\-in records for a specific live room. |
|[UpdateFloatingAdvertisementAPI](https://docs.byteplus.com/docs/byteplus-livesaas/UpdateFloatingAdvertisement) |Call `UpdateFloatingAdvertisementAPI` to update the status, link, and other configuration details of a floating advertisement in a specified live room. |
|[GetTaskAwardItemListAPI](https://docs.byteplus.com/docs/byteplus-livesaas/GetTaskAwardItemListAPI) |Call `GetTaskAwardItemListAPI` to get the list of prizes for the watch time\-based lucky draw that has been sent in the live room. |
|[ListAwardRecordStatisticsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/ListAwardRecordStatisticsAPI) |Call `ListAwardRecordStatisticsAPI` to obtain the list of participating or winning viewers for a specific lucky draw in a live streaming room. |


<span id="account-configurations"></span>
## Account configurations


|**API** |**Description** |
|---|---|
|[ListSiteTagAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listsitetagapiv2) |Gets the list of tags for live rooms under your BytePlus account. |
|[UpdateSiteTagAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updatesitetagapiv2) |Updates the information of tags for live rooms under your BytePlus account. |


<span id="client-sdk"></span>
## Client SDK


|**API** |**Description** |
|---|---|
|[GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi) |Gets the authorization token that is required to allow viewers to enter a live room through web pages or apps integrated with the Viewer SDK. |
