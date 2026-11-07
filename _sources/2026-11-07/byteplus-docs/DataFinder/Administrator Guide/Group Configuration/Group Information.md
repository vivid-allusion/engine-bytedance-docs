---
title: "Group Information"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Group_Information"
---

<span id="基本信息"></span>
## Basic information

In group management, administrators and group administrators can see the basic information of the group, as shown in the following figure:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/241b9960a65c498181c4df559fb9de94~tplv-goo7wpa0wc-image.image) </span>


* The group number is the unique identifier of the group.

* The group administrator has the right to modify the group name, and neither the administrator nor the members can modify the group name.

* The number of applications connected to BytePlus Growth Analysis under the group will be displayed in the group application office. Click the number of applications to jump to the application list for application viewing;

* The number of group users will be displayed at the group user, and clicking on the number of users will jump to user management to view the user list;

* The group administrator will display the names of all administrators under the group.


<span id="集团数据用量"></span>
## Group data usage

After the group is authorized to use or experience the product, the group administrator will see the event consumption of the authorized product in the group center. In the pie chart, you can see the proportion of event consumption to authorized events for the group as a whole. The line chart on the right side of the pie chart allows you to see the trend in event consumption for each month during the current authorization period (accounting period).

After clicking on the data points of the line chart and further clicking "View Current Period Details", the detailed data below the line chart will be focused on the selected month, and you can view the event consumption of each application for each day.

The chart below shows the daily event volume in an app after focusing on a single month. In this state, if you want to return to the monthly viewing state, you can click the [View Overall] button in the upper right corner of the application details table to proceed.

<span id="指标解释"></span>
### Indicator explanation


| |Effective event volume |Daily average DAU |MAU |
|---|---|---|---|
|Calculation method |sum of statistically effective events |The SSID caliber is used to count the number of users who trigger valid events every day and calculate the average value in the calendar month every day (there are very few applications with user_unique_id caliber) |According to the SSID caliber, count the number of users who triggered valid events in the past full month (there are very few applications with a caliber of user_unique_id) |
|Calculation timing |The statistics of the previous day will be completed at 10:00 the next day. |The statistics of the previous day will be completed at 10:00 the next day. |Complete the statistics of the previous month at 10:00 on the 1st of each month |


The event divides the event into different dates based on the time it was received by the server, which is not exactly equivalent to when the event actually occurred on the client side. In addition, the range of effective events will vary from product to product, as follows:


| |Mobile end (automatic reporting) |Mini Program (automatic reporting) |Web page (automatic reporting) |custom report |
|---|---|---|---|---|
|Growth analysis |app_launch,<br><br>app_terminate,<br><br>play_session,<br><br>bav2b_page,<br><br>bav2b_click, bav2b_beat,<br><br>bav2b_page_statistics,<br><br>rangers_push_click,<br><br>rangers_push_show | | | |
|on_share, on_error |predefine_pageview |Undisabled custom events | | |
|Game growth analysis |app_launch, play_session |*  |*  |Undisabled custom events |
|A/B Testing \* |The same goes for growth analysis/game growth analysis |The same goes for growth analysis/game growth analysis |The same goes for growth analysis/game growth analysis |The same goes for growth analysis/game growth analysis |



* A/B testing, also supports calculating consumption by the amount of incoming events. For more information, please contact the Customer Success Manager for details.

   The scope of the above valid events may be adjusted with function iteration, but it will not affect the statistics.
