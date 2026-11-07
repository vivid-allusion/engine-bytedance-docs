---
title: "Viewing data in the data center"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-checking-your-streaming-statistics"
---

You can view the live room data and user portrait under your BytePlus Live account in the data center.

<span id="f50cb1d1"></span>
## Live room data


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. Click **Data center** \> **Live room data**.

3. On the **Live room data** page, you can view data in the metric wall and the live room list.

   * Metric wall: Data is updated every day.

      You can perform the following operations.

      * Filter data based on the time range.

      * Export the filtered data to your local storage.

      * View the filtered data.

         
         |Metric |Description |Granularity |Unit |
         |---|---|---|---|
         |Total live rooms |The total number of live rooms created in the selected time range under your BytePlus account. |Cumulative |Rooms |
         |Total views |The total number of views for all live rooms in the selected time range under your BytePlus account.<br><br>For example, if one viewer visits the viewing page twice and another viewer visits the viewing page once, the number of views increases by 3.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If a viewer refreshes the viewing page once, the number of views increases by 1.</div><br> |Cumulative |Times |
         |Total unique viewers |The total number of unique viewers for all live rooms in the selected time range under your BytePlus account.<br><br>Devices with identical device IDs are considered the same device, and viewers who use the same device are regarded as one person in a live room.<br><br>For example, if one viewer visits the viewing page twice using Device A, another viewer visits the viewing page once using Device B, and one more viewer visits the viewing page three times using Device C, the number of unique viewers increases by 3. |Cumulative |People |
         |Average live rooms |The average number of live rooms visited per viewer in the selected time range under your BytePlus account, which is calculated as the sum of unique viewers for all live rooms divided by the total unique viewers.<br><br>The sum of unique viewers for all live rooms deduplicates viewers using the same device in a live room, while the total number of unique viewers deduplicates viewers using the same device across live rooms.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Devices with identical device IDs are considered the same device.</div><br> |Cumulative |Rooms |
         |Average watch time |The average watch time per viewer in the selected time range under your BytePlus account, which is calculated as the total watch time for all live rooms divided by the total number of unique viewers for all live rooms. |Cumulative |Minutes |
         |Average watch times |The average watch times per viewer in the selected time range under your BytePlus account, which is calculated as the total number of views for all live rooms divided by the total number of unique viewers for all live rooms. |Cumulative |Times |
         |Total watch time |The total watch time for all live rooms in the selected time range under your BytePlus account.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can only get the data in the exported <code>.xlsx</code> file.</div><br> |Cumulative |Minutes |
         

   * Live room list

      You can perform the following operations.

      * Filter data based on the live room name and data statistics scope.

         * Live room name: Fuzzy search is supported.

         * Data statistics scope: Select an option on the right of the **Average watch time (mins)**  or **Average visit duration (mins)**  column.

            * Total viewing: Data generated when the live room is in the **Live**, **Preview**, or **Playback** status is returned, even if no preview or playback is playing on the viewing page.

            * Live viewing: Data generated when the live room is in the **Live** status is returned.

            * Preview viewing: Data generated when the live room is in the **Preview** status is returned, even if no preview is playing on the viewing page.

            * Playback viewing: Data generated when the live room is in the **Playback** status is returned, even if no playback is playing on the viewing page.

            * Page visit: Data generated when the live room is in the **Live**, **Preview**, **Playback**, or **Over** status is returned, even if no preview or playback is playing on the viewing page.

      * Export the filtered data to your local storage.

      * Click **Check details** in the **Data details** column to go to the **Insights** \> **Basic data** page of a live room. For more information, see [Viewing data of a live room](https://docs.byteplus.com/docs/byteplus-livesaas/docs-data-statistics).

      * View the filtered data.

         
         |Metric |Description |Granularity |Unit |
         |---|---|---|---|
         |Activity ID |The activity ID of the live room.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can only get the data in the exported <code>.xlsx</code> file.</div><br> |Fixed value |Not applicable |
         |Live room name |The name of the live room. |Not applicable |Not applicable |
         |Live stream time |The live stream time configured on the **Producer** \> **Basic information** page of the live room. |Not applicable |Not applicable |
         |Total live duration (mins) |The total live duration for the live room, including the ultra\-low latency live streaming and normal latency live streaming. |Cumulative |Minutes |
         |Total views/Total visits |The total number of views or visits in the live room.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If a viewer or visitor refreshes the viewing page once, the number of views or visits increases by 1.</div><br> |Cumulative |Times |
         |Unique viewers/Unique visitors |The total number of unique viewers or visitors in the live room.<br><br>Devices with identical device IDs are considered the same device, and viewers or visitors who use the same device are regarded as one person.<br><br>For example, if one visitor visits the viewing page twice using Device A, another visitor visits the viewing page once using Device B, and one more visitor visits the viewing page three times using Device C, the number of unique visitors increases by 3. |Cumulative |People |
         |Peak concurrent viewers/Peak concurrent visitors |The peak concurrent viewers or visitors in the live room.<br><br>Devices with identical device IDs are considered the same device, and viewers or visitors who use the same device are regarded as one person. |Real\-time |People |
         |Number of comments |The total number of comments sent by the host, viewers, guests, and bots in the live room, including deleted comments and comments under review. |Cumulative |Not applicable |
         |Average watch time (mins)/Average visit duration (mins) |The average watch time or visit duration per viewer in the live room, which is calculated as the total watch time or visit duration divided by the number of unique viewers or visitors. |Cumulative |Minutes |
         |Total watch time (mins)/Total visit duration (mins) |The total watch time or visit duration of viewers or visitors in the live room.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can only get the data in the exported <code>.xlsx</code> file.</div><br> |Cumulative |Minutes |
         


<span id="97aba2c9"></span>
## User portrait


1. Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).

2. Click **Data center** \> **User portrait**.

3. On the **User portrait** page, you can perform the following operations.

   * Filter data based on the nickname and phone number of a viewer, as well as the category tag values of a live room.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You can select at most 20 tag values at a time.      </div>
      

   * Export the filtered data to your local storage.

   * View the filtered data.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If a viewer does not log in to a live room or only enters the nickname in a live room, the user portrait of this viewer will not be displayed.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The following metrics can generate data in real time, while the remaining metrics will generate data 5 minutes after a viewer leaves the live room:      </div>
      

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Bookings      </div>
      

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Votes      </div>
      

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Questionnaires      </div>
      

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Lucky draw participations      </div>
      

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Wins      </div>
      

      
      |Metric |Description |Granularity |Unit |
      |---|---|---|---|
      |Nickname |The nickname of the viewer. |Not applicable |Not applicable |
      |User ID |The unique identifier in BytePlus Live of the viewer. |Not applicable |Not applicable |
      |Associated user ID |The unique identifier of the viewer on third\-party platforms. You can use this associated user ID to identify the viewer's identity within your organization, enabling user insights and data analysis as needed.<br><br>The associated user ID of the viewer varies based on how the viewer logs in to the live room.<br><br><br>* Custom account: The value passed through the `UserId` parameter during custom login. For more information, see [Custom authentication login](https://docs.byteplus.com/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions).<br><br>* Phone number: The `passport_id` generated when the viewer registers BytePlus Live using a phone number.<br><br>* OAuth 2.0: The field corresponding to the user ID in your own account system.<br><br>* Allowlist: The allowlist verification information entered by the viewer.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This field has a value only when the viewer logs in to the live room using the methods mentioned above.</div><br> |Not applicable |Not applicable |
      |Phone number |The phone number of the viewer used to log in to the live room. |Real\-time |Not applicable |
      |Login account |This metric is related to the method used by the viewer for logging in to the live room. For example, if the viewer logs in to the live room using their phone number, this metric value is **Phone number**. If the viewer logs in to the live room via your own account system, this metric value is the name of the account login app. |Real\-time |Not applicable |
      |Ultra\-low latency watch time (mins) |The duration of watching ultra\-low latency live streaming. |Cumulative |Minutes |
      |Total watch time (mins) |Data varies based on the option selected on the right of this column.<br><br><br>* Total viewing: The duration of watching ultra\-low latency live streaming, normal latency live streaming, previews, and playbacks.<br><br>* Live viewing: The duration of watching ultra\-low latency live streaming and normal latency live streaming.<br><br>* Preview viewing: The duration of watching previews.<br><br>* Playback viewing: The duration of watching playbacks.<br><br>* Page visit: The duration spent on the viewing page. |Cumulative |Minutes |
      |Total live rooms |The total number of live rooms visited by the viewer. |Cumulative |Times |
      |Number of comments |The number of comments sent by the viewer, including deleted comments and comments under review. |Cumulative |Not applicable |
      |Region |The region of the viewer. |Real\-time |Not applicable |
      |IP address |The IP address of the viewer. |Real\-time |Not applicable |
      |Bookings |The number of times that the viewer booked live streams. |Cumulative |Times |
      |Votes |The number of times that the viewer submitted votes. |Cumulative |Times |
      |Questionnaires |The number of times that the viewer submitted questionnaires. |Cumulative |Times |
      |Lucky draw participations |The number of times that the viewer participated in real\-time lucky draws. |Cumulative |Times |
      |Wins |The number of times that the viewer won prizes in real\-time lucky draws. |Cumulative |Times |
      

   * Click **Details** in the **Portrait** column to view the basic data, watch footprints, and interactive data of a viewer. If you filter data based on the category tag values of a live room, you can also view the data before and after the filtering.

      
      |Metric |Description |Granularity |Unit |
      |---|---|---|---|
      |Basic data |The basic information of the viewer, including the user ID, login account, phone number, terminal device, region, and IP address. |Not applicable |Not applicable |
      |Watch footprints |The viewing history of the viewer, including the number of live rooms where the viewer watched videos, the total visit duration, the number of minutes spent watching live videos and playbacks in specific live rooms, and the time when the viewer entered specific live rooms. |Cumulative |Total live rooms: rooms<br><br>Total visit duration, watch live, and watch playback: minutes |
      |Interactive data |The number of times that the viewer booked live streams, submitted votes, submitted questionnaires, participated in real\-time lucky draws, won prizes in real\-time lucky draws, and the number of comments sent by the viewer, including deleted comments and comments under review. |Cumulative |Bookings, votes, questionnaires, lucky draw participations, and wins: Times<br><br>Number of comments: Not applicable |
