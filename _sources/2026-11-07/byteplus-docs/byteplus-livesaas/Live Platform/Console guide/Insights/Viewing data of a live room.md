---
title: "Viewing data of a live room"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-data-statistics"
---

You can use the **Insights** module to view data details of a live room, such as basic data, marketing data, and viewer behavior data.

<span id="0a53b0b1"></span>
## Procedure


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. On the live room list, click to open a live room.

3. On the left navigation pane, click **Insights** to go to the page and view the data.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/07456f6dd4604892806cf022236d8a8c~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Data on the page does not refresh automatically. You can manually refresh the page to get the real\-time data.   </div>
   

<span id="99fda442"></span>
### Basic data

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d68d2bd0b44b4c5da403d03cc990e8d7~tplv-goo7wpa0wc-image.image) </span>


* Metrics wall: Data is updated every 5 minutes.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d921a65f56ec460e8ccd6ec99ffe64bd~tplv-goo7wpa0wc-image.image) </span>

   You can perform the following operations.

   * Filter data based on the data statistics scope and channel.

      * Data statistics scope: Select **Total viewing**, **Live viewing**, **Preview viewing**, **Playback viewing**, or **Page visit** from the drop\-down list in the upper\-right corner.

         * Total viewing: Data generated when the live room is in the **Live**, **Preview**, or **Playback** status is returned, even if no preview or playback is playing on the viewing page.

         * Live viewing: Data generated when the live room is in the **Live** status is returned.

         * Preview viewing: Data generated when the live room is in the **Preview** status is returned, even if no preview is playing on the viewing page.

         * Playback viewing: Data generated when the live room is in the **Playback** status is returned, even if no playback is playing on the viewing page.

         * Page visit: Data generated when the live room is in the **Live**, **Preview**, **Playback**, or **Over** status is returned, even if no preview or playback is playing on the viewing page.

      * Channel: Select the channel from the **Channel** drop\-down list in the upper\-right corner of the page. Then, data from the selected channel is returned. By default, data from all channels is returned.

   * Export the filtered data to your local storage.

   * View the filtered data.

      
      |Metric |Description |Granularity |Unit |
      |---|---|---|---|
      |PV |The number of views in the live room.<br><br>For example, if one viewer visits the viewing page twice and another viewer visits the viewing page once, the number of views increases by 3.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If a viewer refreshes the viewing page once, the number of views increases by 1.</div><br> |Cumulative |Times |
      |UV |The number of unique viewers in the live room.<br><br>Devices with identical device IDs are considered the same device, and viewers who use the same device are considered a single viewer.<br><br>For example, if one viewer visits the viewing page twice using Device A, another viewer visits the viewing page once using Device B, and one more viewer visits the viewing page three times using Device C, the number of unique viewers increases by 3. |Cumulative |People |
      |Duration |The watch or visit duration of viewers in the live room.<br><br>For example, if the watch duration for one viewer is 30 minutes and that for another viewer is 60 minutes, the duration increases by 90 minutes. |Cumulative |Minutes |
      |Peak concurrent viewers |The peak concurrent viewers in the live room.<br><br>Devices with identical device IDs are considered the same device, and viewers who use the same device are considered a single viewer. |Real\-time |People |
      |Average watch times |The average number of views per viewer in the live room, which is calculated as the number of views (PV) divided by the number of unique viewers (UV).<br><br>For example, if the number of views is 100 and the number of unique viewers is 80, the average number of views per viewer is 1.25 (100/80). |Cumulative |Times/People |
      |Average watch time |The average watch or visit duration per viewer in the live room, which is calculated as the duration divided by the number of unique viewers (UV).<br><br>For example, if the duration is 1000 minutes and the number of unique viewers is 20, the average watch or visit duration is 50 minutes (1000/20). |Cumulative |Minutes/People |
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You can also get the preceding data by calling <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-getpagewatchdataapi">GetPageWatchDataAPI</a>.      </div>
      

* Tables and graphs

   You can perform the following operations.

   * Filter data based on the channel and time range.

      * Channel: Select the channel from the **Channel** drop\-down list in the upper\-right corner of the page. Then, data from the selected channel is returned. By default, data from all channels is returned.

      * Time range: You can select **Event day**, **Next 7 days**, **Next 30 days**, or a specified time range to display data in the corresponding time range on each tab. By default, **Event day** is selected.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">Event day refers to the entire day where the live stream time configured in the live room belongs.         </div>
         

   * Export the filtered data to your local storage.

   * View the filtered data.

      
      |Screenshot |Metric |Description |Granularity |Unit |
      |---|---|---|---|---|
      |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0df2e5955f7b4072abc930ef3e42a317~tplv-goo7wpa0wc-image.image) </span> |Online viewers |A trend chart for the number of online viewers in the live room.<br><br>Devices with identical device IDs are considered the same device, and viewers who use the same device are considered a single viewer.<br><br>You can perform the following operations.<br><br><br>* Filter data based on the channel and time range.<br><br>* Select the time granularity in the chart.<br><br>* Hover over the chart to view the number of online viewers at a specific time.<br><br>* Export the filtered data to your local storage. |Real\-time |People |
      |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6b7e2a90c698430a862fb48f2b8264d7~tplv-goo7wpa0wc-image.image) </span> |Online popularity |A trend chart for the popularity in the live room.<br><br>Popularity is calculated using growth and reduction coefficients based on the number of unique viewers.<br><br>You can perform the following operations.<br><br><br>* Filter data based on the channel and time range.<br><br>* Select the time granularity in the chart.<br><br>* Move your pointer over the chart to view the popularity and the corresponding time point.<br><br>* Export the filtered data to your local storage. |Real\-time |Popularity |
      |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1d2d6a70c7f04a47b682acc4372e744a~tplv-goo7wpa0wc-image.image) </span> |Watch times |A trend chart for the number of watch times (PV) in the live room.<br><br>You can perform the following operations.<br><br><br>* Filter data based on the channel and time range.<br><br>* Select the time granularity in the chart.<br><br>* Move your pointer over the chart to view the watch times and the corresponding time point.<br><br>* Export the filtered data to your local storage. |Real\-time |Times |
      |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/67eb702d3ed742c587c14c81f964f728~tplv-goo7wpa0wc-image.image) </span> |Watch time |A trend chart showing the total watch time for various stream types: ultra\-low latency, normal latency, live videos (combined), previews, and playbacks.<br><br>You can perform the following operations.<br><br><br>* Filter data based on the channel and time range.<br><br>* Select the time granularity in the chart.<br><br>* Click **Total**, **Live**, **Ultra\-low latency live**, **Normal latency live**, **Preview**, **Playback**, or **Over** under the chart to hide or display the corresponding data in the chart.<br><br>* Move your pointer over the chart to view the watch time and the corresponding time point.<br><br>* Export the filtered data to your local storage.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><strong>Over</strong> refers to the status where a live stream has ended but playback is not released to the viewing page yet. The corresponding watch time represents the time viewers spend on the viewing page when the live room is in this status.</div><br> |Real\-time |Minutes |
      |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/67511a570a8a47548040e2142a2f63cf~tplv-goo7wpa0wc-image.image) </span> |Regional distribution |A table that lists the peak concurrent viewers, the number of views (PV), and the page visit duration for different countries or regions, which are ranked by the number of views.<br><br>You can perform the following operations.<br><br><br>* Filter data based on the channel and time range.<br><br>* Adjust the scrollbar in the lower\-left corner. Then, only the countries or regions with peak concurrent viewers within the range set by the scrollbar are highlighted in the map.<br><br>* Move your pointer over the highlighted area in the map to view the country or region and the corresponding peak concurrent viewers.<br><br>* Export the filtered data to your local storage. |* Peak concurrent viewers: Real\-time<br><br>* Number of views and page visit duration: Cumulative |* Peak concurrent viewers: People<br><br>* Number of views: Times<br><br>* Page visit duration: Minutes |
      |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/83d25b91c6a64ffa8d0dcafa997ed249~tplv-goo7wpa0wc-image.image) </span> |Activity data |Analysis graphs for viewers' watch time and timing for entering the live room, as well as a trend chart for the number of comments.<br><br>You can perform the following operations.<br><br><br>* Filter data based on the channel and time range.<br><br>* Move your pointer over the chart to view the number of comments and the corresponding time point.<br><br>* Click **Total activity**, **Real activity**, or **Bot activity** under the chart to hide or display the corresponding data in the chart.<br><br>   * Total activity: The sum of real comments and bot comments.<br><br>   * Real activity: The number of comments sent by the host, viewers, and guests, including deleted comments and comments under review.<br><br>   * Bot activity: The number of comments sent by bots, including deleted comments and comments under review.<br><br>* Export the filtered data to your local storage. |Real\-time |Analysis graphs: %<br><br>Trend chart: Not applicable |
      


<span id="95561e27"></span>
### Marketing data

On the **Marketing data** page, you can perform the following operations.


* Filter data based on the channel.

   Select the channel from the **Channel** drop\-down list in the upper\-right corner of the page. Then, data from the selected channel is returned. By default, data from all channels is returned.

* Export the data overview and click details.

* View the filtered data.

   
   |Metric ||Description |Granularity |Unit |Update frequency |
   |---|---|---|---|---|---|
   |Account clicks |PV |The number of times viewers click the host account in the live room. |Cumulative |Times |5 minutes |
   ||UV |The number of unique viewers who click the host account in the live room.<br><br>Devices with identical device IDs are considered the same device, and viewers who use the same device are regarded as one person. |Cumulative |People ||
   |Ad and card clicks |PV |The number of times viewers click the header ad, in\-page ads, floating ad, and product cards in the live room. |Cumulative |Times ||
   ||UV |The number of unique viewers who click the header ad, in\-page ads, floating ad, and product cards in the live room.<br><br>Devices with identical device IDs are considered the same device, and viewers who use the same device are regarded as one person. |Cumulative |People ||
   |Data overview |Marketing type |The marketing type.<br><br>Valid values:<br><br><br>* Header ad<br><br>* In\-page ads<br><br>* Floating ad<br><br>* Product cards |Not applicable |Not applicable |5 minutes |
   ||Title |The title of the ad or product card. ||||
   ||Marketing content |The content of advertisement or product card. ||||
   ||Embedded link |The link of advertisement or product card. ||||
   ||PV |The number of times viewers click the header ad, in\-page ad, floating ad, or product card in the live room. |Cumulative |Times ||
   ||UV |The number of unique viewers who click the header ad, in\-page ad, floating ad, or product card in the live room.<br><br>Devices with identical device IDs are considered the same device, and viewers who use the same device are regarded as one person. |Cumulative |People ||
   |Click details |Nickname |The nickname of the viewer. |Not applicable |Not applicable |Real\-time |
   ||User ID |The unique identifier in BytePlus Live of the viewer.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If a viewer does not log in to the live room by entering the nickname or by other methods, the user ID of the viewer is 0.</div><br> ||||
   ||Associated user ID |The unique identifier of the viewer on third\-party platforms. You can use this associated user ID to identify the viewer's identity within your organization, enabling user insights and data analysis as needed.<br><br>The associated user ID of the viewer varies based on how the viewer logs in to the live room.<br><br><br>* Custom account: The value passed through the `UserId` parameter during custom login. For more information, see [Custom authentication login](https://docs.byteplus.com/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions).<br><br>* Phone number: The `passport_id` generated when the viewer registers BytePlus Live using a phone number.<br><br>* OAuth 2.0: The field corresponding to the user ID in your own account system.<br><br>* Allowlist: The allowlist verification information entered by the viewer.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This field has a value only when the viewer logs in to the live room using the methods mentioned above.</div><br> ||||
   ||Phone number |The phone number of the viewer. ||||
   ||Marketing type |The marketing type.<br><br>Valid values:<br><br><br>* Header ad<br><br>* In\-page ads<br><br>* Floating ad<br><br>* Product cards<br><br>* Product list<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The marketing type <strong>Product list</strong> indicates the menu for product cards.</div><br> ||||
   ||Title |The title of advertisement, product card, or the menu for product cards. ||||
   ||Marketing content |The content of advertisement, product card, or the menu for product cards. ||||
   ||Embedded link |The link of advertisement, product card, or the menu for product cards. ||||
   ||Click time |The time when the viewer clicked the advertisement, product card, or the menu for product cards.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can only get the data in the exported <code>.xlsx</code> file.</div><br> ||||
   


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">By calling <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-getadvertisementdataapi">GetAdvertisementDataAPI</a>, you can also get the preceding data except for the click details.</div>


<span id="2b292a98"></span>
### Viewer behavior data

On the **Viewer behavior data** page, you can view data within the last 90 days. Specifically, you can perform the following operations.


* Filter data based on the channel, nickname, and time when a viewer entered and exited the live room.

   Select the channel from the **Channel** drop\-down list in the upper\-right corner of the page. Then, data from the selected channel is returned. By default, data from all channels is returned.

* Select the **Merge the same device** or **Merge the same viewer** checkbox to merge multiple records of the same device or viewer, based on the device ID or user ID respectively.

   For more accurate records, select **Merge the same viewer** if login is required. If login is not required, select **Merge the same device**.

* Export the filtered data to your local storage.

* View the filtered data.

   
   |Metric |Description |
   |---|---|
   |User ID |The unique identifier in BytePlus Live of the viewer.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If a viewer does not log in to the live room by entering the nickname or by other methods, the user ID of the viewer is 0.</div><br> |
   |Associated user ID |The unique identifier of the viewer on third\-party platforms. You can use this associated user ID to identify the viewer's identity within your organization, enabling user insights and data analysis as needed.<br><br>The associated user ID of the viewer varies based on how the viewer logs in to the live room.<br><br><br>* Custom account: The value passed through the `UserId` parameter during custom login. For more information, see [Custom authentication login](https://docs.byteplus.com/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions).<br><br>* Phone number: The `passport_id` generated when the viewer registers BytePlus Live using a phone number.<br><br>* OAuth 2.0: The field corresponding to the user ID in your own account system.<br><br>* Allowlist: The allowlist verification information entered by the viewer.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This field has a value only when the viewer logs in to the live room using the methods mentioned above.</div><br> |
   |Nickname |The nickname of the viewer. |
   |Duration (mins) |The watch or visit duration of viewers in the live room. Unit: minutes.<br><br>Data varies based on the option selected on the right of this column.<br><br><br>* Total viewing: The duration of watching ultra\-low latency live streaming, normal latency live streaming, previews, and playbacks.<br><br>* Normal latency live: The duration of watching normal latency live streaming.<br><br>* Ultra\-low latency live: The duration of watching ultra\-low latency live streaming.<br><br>* Preview viewing: The duration of watching previews.<br><br>* Playback viewing: The duration of watching playbacks.<br><br>* Page visit: The duration spent on the viewing page. |
   |Comments |The number of comments sent by the viewer, including deleted comments and comments under review. |
   |Phone number |The phone number of the viewer used to log in to the live room. |
   |Invitation code |The invitation code used by the viewer for logging in to the live room. |
   |Inviter |The nickname of the inviter who shared an exclusive link, QR code, or poster to the viewer.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This field has a value only when the viewer enters the live room by using the exclusive link, QR code, or poster shared by the inviter and logs in to the live room.</div><br> |
   |Region |The region of the viewer. |
   |IP |The IP address of the viewer. |
   |Terminal type |The device type used by the viewer. |
   |Entry timing |The time the viewer entered the live room. |
   |Entry time \- Exit time |The time when the viewer entered and exited the live room. |
   |Mute |Indicates whether the viewer is muted. |
   |Kick out |Indicates whether the viewer is kicked out of the live room. |
   |Block IP |Indicates whether the viewer's IP address is blocked. |
   |Trial watch |The actual duration of the viewer's trial watch. Unit: minutes. |
   |Extended parameter |An additional parameter synchronized to BytePlus Live, which can be used to associate with the viewer. For example, you can synchronize the viewer's department from your own account system to BytePlus Live.<br><br>You can only get the data in the exported `.xlsx` file. |
   |Channel |The channel through which the viewer first entered the live room.<br><br>You can only get the data in the exported `.xlsx` file. |
   


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">By calling <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-listuserbehaviordataapi">ListUserBehaviorDataAPI</a>, you can also get the preceding data except for the number of comments and the channel.</div>


<span id="72e50a88"></span>
### Live booking data

On the **Live booking data** page, you can perform the following operations.


* Filter data based on the phone number for booking and channel.

   * Phone number for booking: Fuzzy search is supported.

   * Channel: Select the channel from the **Channel** drop\-down list in the upper\-right corner of the page. Then, data from the selected channel is returned. By default, data from all channels is returned.

* Export the filtered data to your local storage.

* View the filtered data.

   
   |Metric |Description |
   |---|---|
   |User ID |The unique identifier in BytePlus Live of the viewer. |
   |Associated user ID |The unique identifier of the viewer on third\-party platforms. You can use this associated user ID to identify the viewer's identity within your organization, enabling user insights and data analysis as needed.<br><br>The associated user ID of the viewer varies based on how the viewer logs in to the live room.<br><br><br>* Custom account: The value passed through the `UserId` parameter during custom login. For more information, see [Custom authentication login](https://docs.byteplus.com/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions).<br><br>* Phone number: The `passport_id` generated when the viewer registers BytePlus Live using a phone number.<br><br>* OAuth 2.0: The field corresponding to the user ID in your own account system.<br><br>* Allowlist: The allowlist verification information entered by the viewer.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This field has a value only when the viewer logs in to the live room using the methods mentioned above.</div><br> |
   |Phone number for booking |The phone number used for booking. Before the live stream starts, an SMS notification will be sent to the phone number if the **SMS reminder** switch is turned on on the **Producer** \> **Basic information** page. |
   |Nickname |The nickname of the viewer. |
   |IP address |The IP address of the viewer. |
   |Region |The region of the viewer. |
   |Booking submission time |The time when the viewer booked the live stream. |
   |Terminal type |The device type used by the viewer. |
   |Extended parameter |An additional parameter synchronized to BytePlus Live, which can be used to associate with the viewer. For example, you can synchronize the viewer's department from your own account system to BytePlus Live.<br><br>You can only get the data in the exported `.xlsx` file. |
   |Channel |The channel where the viewer comes from.<br><br>You can only get the data in the exported `.xlsx` file. |
   


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Even if the same phone number is used for booking, user IDs can differ. This occurs when a viewer logs in to the live room using different methods (e.g., by nickname versus by phone number), which results in different user IDs.</div>


<span id="46448583"></span>
### Questionnaire data

On the **Questionnaire data** page, you can view the following data.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can only view data within the last 90 days.</div>



|Metric |Description |Remarks |
|---|---|---|
|Questionnaire title |The title of the questionnaire. |You can also get the data by calling [ListQuestionnaireDataAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listquestionnairedataapi). |
|Send time |The time when the questionnaire was sent to the viewing page. ||
|Submitted questionnaires |The number of questionnaires submitted by viewers. ||
|User ID |The unique identifier in BytePlus Live of the viewer.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If a viewer does not log in to the live room by entering the nickname or by other methods, the user ID of the viewer is 0.</div><br> |You can also get the data by calling [ListQuestionnaireAnswerDataAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listquestionnaireanswerdataapi) or clicking **Export** in the **Actions** column. |
|Associated user ID |The unique identifier of the viewer on third\-party platforms. You can use this associated user ID to identify the viewer's identity within your organization, enabling user insights and data analysis as needed.<br><br>The associated user ID of the viewer varies based on how the viewer logs in to the live room.<br><br><br>* Custom account: The value passed through the `UserId` parameter during custom login. For more information, see [Custom authentication login](https://docs.byteplus.com/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions).<br><br>* Phone number: The `passport_id` generated when the viewer registers BytePlus Live using a phone number.<br><br>* OAuth 2.0: The field corresponding to the user ID in your own account system.<br><br>* Allowlist: The allowlist verification information entered by the viewer.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This field has a value only when the viewer logs in to the live room using the methods mentioned above.</div><br> ||
|Nickname |The nickname of the viewer. ||
|Phone number |The phone number of the viewer.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This metric has a value only when the <strong>Question type</strong> is set to <strong>Personal information</strong> \> <strong>Phone number</strong>.</div><br> ||
|Email |The email of the viewer.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This metric has a value only when the <strong>Question type</strong> is set to <strong>Personal information</strong> \> <strong>Email</strong>.</div><br> ||
|Region |The region of the viewer. ||
|Question and answer |The question description and the answer to the question. ||
|Submission time |The time when the questionnaire was submitted. ||
|Extended parameter |An additional parameter synchronized to BytePlus Live, which can be used to associate with the viewer. For example, you can synchronize the viewer's department from your own account system to BytePlus Live. |You can only get the data by clicking **Export** in the **Actions** column. |


<span id="07c72899"></span>
### Voting data

On the **Voting data** page, you can view the following data.


|Metric |Description |Remarks |
|---|---|---|
|Vote title |The title of the vote. |None. |
|Voting type |The type of the vote, which indicates whether a viewer can select one or more options. ||
|Deadline |The submission deadline for the vote. ||
|Participants |The number of viewers who submitted the vote. ||
|Options |The options selected by the viewer. |You can also get the data by clicking **Export** in the **Actions** column. |
|Nickname |The nickname of the viewer. ||
|User ID |The unique identifier in BytePlus Live of the viewer. ||
|Associated user ID |The unique identifier of the viewer on third\-party platforms. You can use this associated user ID to identify the viewer's identity within your organization, enabling user insights and data analysis as needed.<br><br>The associated user ID of the viewer varies based on how the viewer logs in to the live room.<br><br><br>* Custom account: The value passed through the `UserId` parameter during custom login. For more information, see [Custom authentication login](https://docs.byteplus.com/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions).<br><br>* Phone number: The `passport_id` generated when the viewer registers BytePlus Live using a phone number.<br><br>* OAuth 2.0: The field corresponding to the user ID in your own account system.<br><br>* Allowlist: The allowlist verification information entered by the viewer.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This field has a value only when the viewer logs in to the live room using the methods mentioned above.</div><br> ||
|Phone number |The phone number of the viewer. ||
|Email |The email of the viewer. ||
|Submission time |The time when the vote was submitted. ||
|IP address |The IP address of the viewer. ||
|Extended parameter |An additional parameter synchronized to BytePlus Live, which can be used to associate with the viewer. For example, you can synchronize the viewer's department from your own account system to BytePlus Live. |You can only get the data by clicking **Export** in the **Actions** column. |


<span id="907f00b8"></span>
### Lucky draw data


* On the **Real\-time lucky draws** tab of the **Lucky draw data** page, you can perform the following operations.

   * View the following data.

      
      |Metric |Description |
      |---|---|
      |Prize name |The name of the prize. |
      |Prize type |The type of the prize. |
      |Draw time |The time when winners were selected. |
      |Participants |The number of viewers who participated in the lucky draw. |
      |Winners |The number of viewers who won the prize. |
      |Winning percentage |The percentage of winners to participants. |
      |Winner list |The list of winners. |
      |Participant list |The list of participants. |
      

   * View or export the winner list.

      
      |Metric |Description |
      |---|---|
      |User ID |The unique identifier in BytePlus Live of the viewer. |
      |Associated user ID |The unique identifier of the viewer on third\-party platforms. You can use this associated user ID to identify the viewer's identity within your organization, enabling user insights and data analysis as needed.<br><br>The associated user ID of the viewer varies based on how the viewer logs in to the live room.<br><br><br>* Custom account: The value passed through the `UserId` parameter during custom login. For more information, see [Custom authentication login](https://docs.byteplus.com/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions).<br><br>* Phone number: The `passport_id` generated when the viewer registers BytePlus Live using a phone number.<br><br>* OAuth 2.0: The field corresponding to the user ID in your own account system.<br><br>* Allowlist: The allowlist verification information entered by the viewer.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This field has a value only when the viewer logs in to the live room using the methods mentioned above.</div><br> |
      |Nickname |The nickname of the viewer. |
      |Email |The email of the viewer. |
      |Phone number |The phone number of the viewer. |
      |Priority for winning |Indicates whether the viewer has a priority for winning the prize. |
      |Recipient name |The recipient name entered after the viewer wins the prize. |
      |Recipient phone number |The recipient phone number entered after the viewer wins the prize. |
      |Shipping address |The shipping address entered after the viewer wins the prize. |
      |Prize information |The name of the prize. |
      

   * View or export the participant list.

      
      |Metric |Description |
      |---|---|
      |User ID |The unique identifier in BytePlus Live of the viewer. |
      |Associated user ID |The unique identifier of the viewer on third\-party platforms. You can use this associated user ID to identify the viewer's identity within your organization, enabling user insights and data analysis as needed.<br><br>The associated user ID of the viewer varies based on how the viewer logs in to the live room.<br><br><br>* Custom account: The value passed through the `UserId` parameter during custom login. For more information, see [Custom authentication login](https://docs.byteplus.com/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions).<br><br>* Phone number: The `passport_id` generated when the viewer registers BytePlus Live using a phone number.<br><br>* OAuth 2.0: The field corresponding to the user ID in your own account system.<br><br>* Allowlist: The allowlist verification information entered by the viewer.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This field has a value only when the viewer logs in to the live room using the methods mentioned above.</div><br> |
      |Nickname |The nickname of the viewer. |
      |Email |The email of the viewer. |
      |Phone number |The phone number of the viewer. |
      |Winner |Indicates whether the viewer wins the prize. |
      |Priority for winning |Indicates whether the viewer has a priority for winning the prize. |
      |Prize information |The name of the prize. |
      

   * Export all the winning information in the live room.

      
      |Metric |Description |
      |---|---|
      |Draw time |The time when winners were selected. |
      |User ID |The unique identifier in BytePlus Live of the viewer. |
      |Nickname |The nickname of the viewer. |
      |Login phone number |The phone number of the viewer used to log in to the live room. |
      |Associated user ID |The unique identifier of the viewer on third\-party platforms. You can use this associated user ID to identify the viewer's identity within your organization, enabling user insights and data analysis as needed.<br><br>The associated user ID of the viewer varies based on how the viewer logs in to the live room.<br><br><br>* Custom account: The value passed through the `UserId` parameter during custom login. For more information, see [Custom authentication login](https://docs.byteplus.com/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions).<br><br>* Phone number: The `passport_id` generated when the viewer registers BytePlus Live using a phone number.<br><br>* OAuth 2.0: The field corresponding to the user ID in your own account system.<br><br>* Allowlist: The allowlist verification information entered by the viewer.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This field has a value only when the viewer logs in to the live room using the methods mentioned above.</div><br> |
      |Recipient name |The recipient name entered after the viewer wins the prize. |
      |Recipient phone number |The recipient phone number entered after the viewer wins the prize. |
      |Shipping address |The shipping address entered after the viewer wins the prize. |
      |Email |The email of the viewer. |
      |Priority for winning |Indicates whether the viewer has a priority for winning the prize. |
      |Prize name |The name of the prize. |
      

* On the Watch time\-based lucky draws tab of the **Lucky draw data** page, you can perform the following operations.

   * View the following data.

      
      |Metric |Description |
      |---|---|
      |Prize name |The name of the prize. |
      |Prize type |The type of the prize. |
      |Prize link |The link used to claim the prize.<br><br>This metric has a value only when the prize type is **Voucher**. |
      |Participants |The number of viewers who participated in the lucky draw. |
      |Winners |The number of viewers who won the prize. |
      |Actual winning percentage |The percentage of winners to participants. |
      |Winner list |The list of winners. |
      |Participant list |The list of participants. |
      

   * View or export the winner list.

      
      |Metric |Description |
      |---|---|
      |User ID |The unique identifier in BytePlus Live of the viewer. |
      |Nickname |The nickname of the viewer. |
      |Email |The email of the viewer. |
      |Login phone number |The phone number of the viewer used to log in to the live room. |
      |Recipient name |The recipient name entered after the viewer wins the prize. |
      |Recipient phone number |The recipient phone number entered after the viewer wins the prize. |
      |Address |The shipping address entered after the viewer wins the prize. |
      |Prize information |The name of the prize. |
      |Associated user ID |The unique identifier of the viewer on third\-party platforms. You can use this associated user ID to identify the viewer's identity within your organization, enabling user insights and data analysis as needed.<br><br>The associated user ID of the viewer varies based on how the viewer logs in to the live room.<br><br><br>* Custom account: The value passed through the `UserId` parameter during custom login. For more information, see [Custom authentication login](https://docs.byteplus.com/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions).<br><br>* Phone number: The `passport_id` generated when the viewer registers BytePlus Live using a phone number.<br><br>* OAuth 2.0: The field corresponding to the user ID in your own account system.<br><br>* Allowlist: The allowlist verification information entered by the viewer.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can only get the data in the exported <code>.xlsx</code> file.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">This field has a value only when the viewer logs in to the live room using the methods mentioned above.</div><br> |
      

   * View or export the participant list.

      
      |Metric |Description |
      |---|---|
      |User ID |The unique identifier in BytePlus Live of the viewer. |
      |Nickname |The nickname of the viewer. |
      |Email |The email of the viewer. |
      |Login phone number |The phone number of the viewer used to log in to the live room. |
      |Winner |Indicates whether the viewer wins the prize. |
      |Prize information |The name of the prize. |
      |Associated user ID |The unique identifier of the viewer on third\-party platforms. You can use this associated user ID to identify the viewer's identity within your organization, enabling user insights and data analysis as needed.<br><br>The associated user ID of the viewer varies based on how the viewer logs in to the live room.<br><br><br>* Custom account: The value passed through the `UserId` parameter during custom login. For more information, see [Custom authentication login](https://docs.byteplus.com/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions).<br><br>* Phone number: The `passport_id` generated when the viewer registers BytePlus Live using a phone number.<br><br>* OAuth 2.0: The field corresponding to the user ID in your own account system.<br><br>* Allowlist: The allowlist verification information entered by the viewer.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can only get the data in the exported <code>.xlsx</code> file.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">This field has a value only when the viewer logs in to the live room using the methods mentioned above.</div><br> |
      

   * Export all the winning information in the live room.

      
      |Metric |Description |
      |---|---|
      |Draw time |The time when winners were selected. |
      |User ID |The unique identifier in BytePlus Live of the viewer. |
      |Nickname |The nickname of the viewer. |
      |Login phone number |The phone number of the viewer used to log in to the live room. |
      |Associated user ID |The unique identifier of the viewer on third\-party platforms. You can use this associated user ID to identify the viewer's identity within your organization, enabling user insights and data analysis as needed.<br><br>The associated user ID of the viewer varies based on how the viewer logs in to the live room.<br><br><br>* Custom account: The value passed through the `UserId` parameter during custom login. For more information, see [Custom authentication login](https://docs.byteplus.com/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions).<br><br>* Phone number: The `passport_id` generated when the viewer registers BytePlus Live using a phone number.<br><br>* OAuth 2.0: The field corresponding to the user ID in your own account system.<br><br>* Allowlist: The allowlist verification information entered by the viewer.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This field has a value only when the viewer logs in to the live room using the methods mentioned above.</div><br> |
      |Recipient name |The recipient name entered after the viewer wins the prize. |
      |Recipient phone number |The recipient phone number entered after the viewer wins the prize. |
      |Address |The shipping address entered after the viewer wins the prize. |
      |Email |The email of the viewer. |
      |Prize name |The name of the prize. |
      


<span id="5407f578"></span>
### Check\-in data

On the **Check\-in data** page, you can view the following data.


|Metric |Description |Remarks |
|---|---|---|
|Check\-in title |The title of the check\-in. |None. |
|Send time |The time when the check\-in was sent to the viewing page. ||
|Check\-in duration |The duration of the check\-in. ||
|Status |The status of the check\-in. ||
|Participants |The number of viewers who participated in the check\-in. ||
|User ID |The unique identifier in BytePlus Live of the viewer. |* You can also get the data by clicking **Export** in the **Actions** column.<br><br>* You cannot view or export the data when the check\-in is in progress. |
|Associated user ID |The unique identifier of the viewer on third\-party platforms. You can use this associated user ID to identify the viewer's identity within your organization, enabling user insights and data analysis as needed.<br><br>The associated user ID of the viewer varies based on how the viewer logs in to the live room.<br><br><br>* Custom account: The value passed through the `UserId` parameter during custom login. For more information, see [Custom authentication login](https://docs.byteplus.com/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions).<br><br>* Phone number: The `passport_id` generated when the viewer registers BytePlus Live using a phone number.<br><br>* OAuth 2.0: The field corresponding to the user ID in your own account system.<br><br>* Allowlist: The allowlist verification information entered by the viewer.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This field has a value only when the viewer logs in to the live room using the methods mentioned above.</div><br> ||
|Nickname |The nickname of the viewer. ||
|Email |The email of the viewer. ||
|Phone number |The phone number of the viewer. ||
|Check\-in time |The time when the viewer checked in. ||
|Check\-in information |The check\-in information entered by the viewer. ||


<span id="62a20bf7"></span>
### Quiz data

On the **Quiz data** page, you can perform the following operations.


* Click **View details** to view the details.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4bd7826a868847c2be2537d334d666dd~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You cannot view the details if a quiz is withdrawn from the viewing page.   </div>
   

* View the following data.

   
   |Metric |Description |
   |---|---|
   |Quiz title |The title of the quiz. |
   |Quiz type |The type of the quiz, which indicates whether a viewer can select one or more options. |
   |Send time |The time when the quiz was sent to the viewing page. |
   |Answering time |The time limit for answering the quiz. |
   |Participants |The number of viewers who participated in the quiz. |
   |Correct responders |The number of viewers who answered correctly. |
   

* View or export the participant list.

   
   |Metric |Description |
   |---|---|
   |User ID |The unique identifier in BytePlus Live of the viewer. |
   |Associated user ID |The unique identifier of the viewer on third\-party platforms. You can use this associated user ID to identify the viewer's identity within your organization, enabling user insights and data analysis as needed.<br><br>The associated user ID of the viewer varies based on how the viewer logs in to the live room.<br><br><br>* Custom account: The value passed through the `UserId` parameter during custom login. For more information, see [Custom authentication login](https://docs.byteplus.com/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions).<br><br>* Phone number: The `passport_id` generated when the viewer registers BytePlus Live using a phone number.<br><br>* OAuth 2.0: The field corresponding to the user ID in your own account system.<br><br>* Allowlist: The allowlist verification information entered by the viewer.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This field has a value only when the viewer logs in to the live room using the methods mentioned above.</div><br> |
   |Email |The email of the viewer. |
   |Nickname |The nickname of the viewer. |
   |Submission time |The time when the viewer submitted the quiz. |
   |Submitted answer |The quiz answer submitted by the viewer. |
   |Result |Indicates whether the viewer answered correctly. |
   


<span id="a910a50d"></span>
### Gift details

On both the **Free gifts** and **Points gifts** tabs of the **Gift details** page, you can perform the following operations.


* Filter data based on the time when viewers sent gifts.

* Export the filtered data to your local storage.

* View the filtered data.

   
   |Metric |Description |
   |---|---|
   |User ID |The unique identifier in BytePlus Live of the viewer. |
   |Associated user ID |The unique identifier of the viewer on third\-party platforms. You can use this associated user ID to identify the viewer's identity within your organization, enabling user insights and data analysis as needed.<br><br>The associated user ID of the viewer varies based on how the viewer logs in to the live room.<br><br><br>* Custom account: The value passed through the `UserId` parameter during custom login. For more information, see [Custom authentication login](https://docs.byteplus.com/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions).<br><br>* Phone number: The `passport_id` generated when the viewer registers BytePlus Live using a phone number.<br><br>* OAuth 2.0: The field corresponding to the user ID in your own account system.<br><br>* Allowlist: The allowlist verification information entered by the viewer.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This field has a value only when the viewer logs in to the live room using the methods mentioned above.</div><br> |
   |Nickname |The nickname of the viewer. |
   |Gift name |The name of the gift. |
   |Gift picture |The picture of the gift. |
   |Unit price |The unit price of the gift. |
   |Gifts sent |The number of gifts sent. |
   |Send time |The time when the viewer sent gifts. |
