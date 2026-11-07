---
title: "Feature comparison between SaaS and aPaaS"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-feature-comparison-between-saas-and-apaas"
---

To meet your requirements for live streaming and viewing within your own product environment, BytePlus Live has integrated and packaged underlying capabilities, providing an aPaaS solution that can be independently integrated into your product. The SaaS solution and the aPaaS solution have certain differences in features on the viewing page. For more information, see the following table.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Features supported by iframe embedding are the same as those supported by the SaaS solution. For more information, see <a href="https://docs.byteplus.com/byteplus-livesaas/docs/embedding-a-viewing-page-with-iframe?version=v1.0">iframe</a>.</div>


* <div data-tips="true" data-tips-type="tip"><strong>Not applicable</strong> in the following table indicates that the feature does not have a use case in the current solution.</div>


* <div data-tips="true" data-tips-type="tip">In the following table, if a feature is supported only for custom mode, it indicates that the feature is applicable under the following scenarios:</div>


   * <div data-tips="true" data-tips-type="tip">The authentication mode of a live room is set to custom mode (applicable to Viewer SDK for Android/iOS/Flutter).</div>


   * <div data-tips="true" data-tips-type="tip">The authentication mode of a live room is set to public mode under the following conditions (applicable to Viewer SDK for Android/iOS):</div>


      * <div data-tips="true" data-tips-type="tip">For Viewer SDK for iOS: The <code>nickName</code> value of <code>BDLActivity</code> is empty, and the <code>setLoginProvider:</code> method has been called.</div>


      * <div data-tips="true" data-tips-type="tip">For Viewer SDK for Android: The <code>setCustomLoginListener</code> method has been called.</div>




|Feature ||Description |SaaS solution (PC + mobile) |Viewer SDK for Android/iOS/Flutter |Web Viewer SDK |
|---|---|---|---|---|---|
|Marketing promotion |Share a live room to social platforms |Viewers can share a live room's QR code or link to social platforms such as Facebook and WhatsApp. |Supported |Supported<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Viewers can only share a live room's link.</div><br> |Supported |
||Customize the viewing page's favicon |Customize the favicon displayed in locations such as the browser's address bar, bookmark, and tab for the viewing page. |Supported on PCs only |Not applicable |Not supported |
||Customize shared address |Customize the link, QR code, including the code displayed on the invitation poster, used to share a live room. |Supported |Supported |Supported |
||Cover, background, and theme |Configure the landscape and portrait covers, background image or color, and theme of a live room. |Supported<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only PCs and mobile devices in landscape mode support background image or color.</div><br> |Supported<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Does not support the portrait cover.</div><br> |Supported<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Not applicable for background image or color.</div><br> |
||Header image |Configure the header image of a live room. |Supported on PCs and mobile devices in landscape mode |Supported in landscape mode only |Only supported on mobile devices in landscape mode with full\-page integration |
||Background blurring |Blur the background of a live room. |Supported on PCs and mobile devices in landscape mode |Supported<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For Android, supported in portrait mode only.</div><br> |Supported on PCs and mobile devices in landscape mode |
||Pinned player |Hide the header and pin the player to the top of the viewing page. |Supported on PCs and mobile devices in landscape mode |Not supported |Supported on PCs and mobile devices in landscape mode |
||Live room in landscape and portrait modes |Landscape mode is suitable for scenarios such as training, conferences, and activities, while portrait mode is suitable for scenarios such as marketing and e\-commerce. |Supported |Supported |Supported |
||Preview |Upload and play a preview for the warm\-up of your live stream, which promotes content and attracts more users. |Supported |Supported |Supported |
||Countdown |Viewers can view the countdown to a live stream when entering a live room before the live stream starts. |Supported |Supported |Supported |
||Display popularity |Display the number of online viewers in a live room. |Supported |Supported |Supported |
||Book a live stream |Viewers can book a live stream. For SaaS solution and Web Viewer SDK, viewers can receive SMS notifications before the live stream starts. For Viewer SDK for Android and Viewer SDK for iOS, viewers can add an event to the system calendar of their phones. |Supported |Supported |Supported |
||Landing page |Display a page about your live stream before viewers enter the viewing page on mobile devices. |Supported on mobile devices only |Not supported |Not supported |
||Host account |By associating with a host account, viewers can follow the host on the viewing page or navigate to the host account's homepage on other platforms such as Facebook. |Supported |Supported<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Following the host is supported only for iOS and Android, and requires custom authentication mode.</div><br> |Supported |
||Switch between different venues |For live streams with multiple venues, such as online career fairs or large conferences, you can share a single live room link that allows viewers to enter and switch between different venues. |Supported |Supported |Supported |
||Invitation poster |Viewers can share an invitation poster of a live room to invite others to enter the live room. |Supported |Supported |Supported |
||Player logo |Display your custom logo on the viewing page's player. |Supported |Not supported |Supported on mobile devices in landscape mode with full\-page integration, on mobile devices in portrait mode, and on PCs |
||Menu for graphics |Customize the content displayed under a menu for graphics in a live room, including images, texts, and links. |Supported |Supported |Supported |
||In\-page ads |Customize the advertisement carousel in the middle of the page, which is used to raise brand awareness. Viewers are redirected to the floating layer or another page after they tap or click in\-page ads. |Supported |Supported |Supported |
||Header ad |Customize the redirect URL at the top of the page. Viewers are redirected to the floating layer or another page after they tap or click the header ad. |Supported on PCs and mobile devices in landscape mode |Supported in landscape mode only |Only supported on mobile devices in landscape mode with full\-page integration |
||Floating ad |Upload the picture and customize the redirect URL of the floating ad. Viewers are redirected to the floating layer or another page after they tap or click the floating ad. |Supported |Supported |Supported |
||Product display (menu for product cards) |Add the menu for product cards to customize the information and redirect URLs of products, and adjust the display order of products. Viewers are redirected to the floating layer or another page after they tap or click a card. They can also view product information in a floating card on the right of the player. |Supported |Supported<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Does not support reading the display menu configuration on the BytePlus Live console.</div><br> |Supported |
||Put products on sale |Put products on sale in real time. |Supported |Supported |Supported |
||Menu for aggregated live stream |Create a list of recommended live rooms. |Supported on PCs and mobile devices in landscape mode |Not supported |Not supported |
||Picture\-in\-Picture (PiP) |Viewers can watch live videos, playbacks, and previews in PiP mode. |Supported on PCs only |Supported |Supports PiP mode for PCs and small window mode for mobile devices. |
||System notifications |Display lucky draw notifications, dynamic emoji effects, gift messages, and entrance messages on the viewing page. Viewers can block such system notifications. |Supported |Supported<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Only supports lucky draw notifications and entrance messages.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Supports lucky draw notifications only for custom mode.</div><br> |Supported |
||Customize SMS |Customize reminder SMS to create a personalized live room and enhance user\-friendliness. |Supported |Not applicable |Supported |
|Interactions |Comments |Send comments, including bullet comments |Supported<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only PCs and mobile devices in landscape mode support bullet comments.</div><br> |Supports comments, but not bullet comments |Supported<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only PCs and mobile devices in landscape mode support bullet comments.</div><br> |
||Host's comments |Highlight the host's comments. |Supported |Supported |Supported |
||Pinned comment |Pin a comment to the top of the chat area. |Supported |Supported |Supported |
||Likes |Display the number of likes, customize the icon for liking a live room, and allow viewers to like a live room or comment. |Supported |Supported |Supported<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only supports reading the likes icon configuration on the BytePlus Live console.</div><br> |
||Live room description |Display a brief introduction to the live room. |Supported on PCs and mobile devices in landscape mode |Supported |Supported on PCs and mobile devices in landscape mode |
||Theater mode |Web theater mode, which allows viewers to enjoy the video, comments, and interactions. |Supported on PCs only |Not applicable |Not applicable |
||Real\-time lucky draws |Manual or automatic draws. Members in the VIP list have priority in winning. |Supported |Supported only for custom mode |Supported |
||Lucky draws for cumulative viewing time |Viewers who accumulate a certain amount of time for watching a live stream in a live room are eligible for draws. |Supported |Not supported |Supported |
||Gift rewards |Viewers can use free gifts or redeem points for gifts to reward hosts.<br><br>To allow viewers to redeem points for gifts, you must integrate your points system with BytePlus Live. |Supported |Supported only for custom mode |Supported |
||Menu for Q&A |Viewers can ask and answer questions. |Supported on PCs and mobile devices in landscape mode<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only PCs support reading the display mode configuration on the BytePlus Live console.</div><br> |Not supported |Supported on PCs and mobile devices in landscape mode<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The display mode configured on the BytePlus Live console does not take effect. You can only configure the display position of the menu through DOM settings.</div><br> |
||Check\-ins |Initiate check\-ins in a live room. |Supported |Supported |Supported |
||Questionnaires |Send questionnaires in a live room. |Supported |Supported |Supports sending questionnaires manually and sending questionnaires when the live stream ends. |
||Voting |Send votes in a live room. |Supported |Supported |Supported |
||Preview and download documents |Viewers can preview and download Word, PPT, or PDF files in a live room. |Supported |Not supported |Supported |
||Menu for interactions |Share images and text messages in the chat to provide updates or interact with viewers, in addition to other interactions like real\-time lucky draws. |Supported<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only PCs support reading the display mode configuration on the BytePlus Live console.</div><br> |Supported<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Does not support reading the display menu and display mode configurations on the BytePlus Live console.</div><br> |Supported<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The display mode configured on the BytePlus Live console does not take effect. You can only configure the display position of the menu through DOM settings.</div><br> |
||Dynamic emojis |Viewers can send dynamic emojis and trigger effects in the chat area, which increases the number of comments and enhances the interactive atmosphere in a live room. |Supported |Viewers can only view dynamic emojis in the chat area |Supported |
||Select video quality |Viewers can select video quality as needed. |Supported |Supported |Supported |
||Full\-screen mode |Viewers can watch live videos, previews, and playbacks in full\-screen mode. |Supported |Supported |Supported |
||Refresh a live stream |During a live stream, viewers can refresh the page to reconnect to the live room. |Supported |Supported |Supported |
||View historical comments |Viewers can load historical comments by scrolling down. |Supported |Supported |Supported |
||Popular comments |Display comments with the most likes. |Supported on PCs and mobile devices in landscape mode |Supported in landscape mode only |Supported on PCs and mobile devices in landscape mode |
|Viewing restrictions |Public access |Viewers can directly enter a live room without logging in. |Supported |Supported |Supported |
||Password\-protected viewing |Viewers must enter the correct password before entering a live room. |Supported |Not supported |Not supported |
||Phone number login |Provide the SMS verification service to ensure the authenticity of viewer information. |Supported |Not supported |Supported |
||Phone number allowlist |Add phone numbers of viewers to the allowlist before the live stream starts, granting those viewers direct access to a live room. You can choose to send SMS reminders to such viewers 5 minutes before the live stream starts. |Supported |Not supported |Not supported |
||Invitation code\-protected viewing |Viewers must enter the correct invitation code before entering a live room, with each code inviting one viewer. |Supported |Not supported |Not supported |
||Custom authorization |Authorize your own account system to allow viewers to enter a live room by using their user credentials of your system. |Supported |Supported |Supported |
||OAuth 2.0 |Your own account system supports single sign\-on by using the OAuth 2.0 standard authorization protocol. |Supported |Not supported |Not supported |
||Backup viewing page address |Generate a backup link to address viewer access issues. Viewers can use this link to enter a live room without any viewing restrictions. |Supported |Not applicable |Not applicable |
|Security control |Customize sensitive words |Customize sensitive words in a live room so that comments containing such words are only visible to viewers who send them and viewers' nicknames cannot contain such words. |Supported |Supported |Supported |
||Review viewers' comments before displaying them |Review viewers' comments before displaying them on the viewing page. |Supported |Supported |Supported |
||Export, clear, and delete comments |Export, clear, and delete comments. |Supported |Supported |Supported |
||Mute viewers |Mute viewers who send inappropriate comments. |Supported |Supported |Supported |
||Lock preview |Lock the status of a live room to **Preview** so that viewers can only watch the preview or view the cover on the viewing page even if you start a live stream or release a playback. This is applicable to scenarios where live stream quality needs advance testing. |Supported |Supported |Supported |
||Welcome message |Display a welcome message in the chat area to inform viewers about chat rules, fulfilling the organizer's responsibility for notifications. |Supported |Supported |Supported |
||Reminder |Display a reminder pop\-up window when viewers enter the live room to inform them about trading risks and chat rules, fulfilling the organizer's responsibility for notifications. |Supported |Supported |Supported |
||Change nicknames |Viewers can change their nicknames in a live room. |Supported |Not supported |Supported |
||Fullscreen watermark |Use viewers' nicknames, phone numbers, and other information as a full\-screen watermark. |Supported |Supported |Supported |
||Mute all viewers |Prohibit all viewers from sending comments. |Supported |Supported |Supported |
||Kick out |Kick viewers out of the live room and prevent them from rejoining the live room. |Supported |Supported |Supported |
||Ban IP address |Kick viewers out of the live room and prevent anyone from accessing the live room through the banned IP address. |Supported |Supported |Supported |
|Ultra\-low latency live streaming |Ultra\-low latency live streaming |BytePlus Live supports ultra\-low latency live streaming for tens of millions of concurrent viewers. Compared to normal latency live streaming with a latency of 5 to 10 seconds, ultra\-low latency live streaming can reduce latency to 1 to 2 seconds, offering you a smooth and high\-quality live viewing experience. |Supported |Not supported |Supported |
|Data analysis |Real\-time data dashboard |View the real\-time data dashboard on the BytePlus Live console. |Supported |Supported |Supported |
||Viewing data |View basic data such as watch duration, page views (PV), unique viewers (UV), and geographic distribution of viewers on the BytePlus Live console. You can also view and export detailed data statistics. |Supported |Supported |Supported |
||Comment data |View and export comment data of a live room on the BytePlus Live console. |Supported |Supported |Supported |
||Check\-in data |View and export check\-in data on the BytePlus Live console. |Supported |Not supported |Supported |
||Questionnaire data |View and export questionnaire data on the BytePlus Live console. |Supported |Supported |Supported |
||Voting data |View and export voting data on the BytePlus Live console. |Supported |Supported |Supported |
||Lucky draw data |View and export lucky draw data on the BytePlus Live console. |Supported |Supported |Supported |
||Gift data |View and export gift data on the BytePlus Live console. |Supported |Not supported |Supported |
||Marketing data |View PV and UV for the host account and ads of a live room on the BytePlus Live console. |Supported |Supported |Supported |
||Live booking data |View and export live booking data on the BytePlus Live console. |Supported |Not supported |Supported |
||Viewer behaviour data |View and export viewer behavior data on the BytePlus Live console. |Supported |Supported |Supported |
||Account\-level data |View user portraits of viewers on the BytePlus Live console. |Supported |Supported |Supported |
|Playbacks |Automatically publish playbacks to the viewing page |The playback generated after a live stream ends is automatically released to the viewing page. |Supported |Supported |Supported |
||Playback speed |Viewers can select to play previews or playbacks at the speed of 0.5x, 0.75x, 1.0x, 1.25x, 1.5x, or 2x. |Supported |Supported |Supported |
||Bullet comments for playbacks |Viewers can send and view bullet comments scrolling across the player when watching playbacks. You can select to display the bullet comments sent during the live stream for viewers who watch playbacks. |Supported on PCs and mobile devices in landscape mode |Not supported |Not supported |
||Mark highlights |Mark highlights in a playback so that viewers can easily find exciting moments in the playback. |Supported on PCs only |Not supported |Supported on PCs only |
|Internalization |Multilingual live room |Viewers can switch between different languages in a live room. |Supported |Supported |Supported<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">On PCs, viewers cannot switch between languages directly on the viewing page, but can change the language of the viewing page by changing the browser language.</div><br> |
||Comment translation |Comments can be automatically translated into multiple languages. |Supported |Supported |Supported on mobile devices only |
