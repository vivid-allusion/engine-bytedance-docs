---
title: "Preset Dashboard - Indicator Criteria"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Preset_Dashboard_-_Indicator_Criteria"
---

Preset Dashboard function:

When you successfully create an application and enter the Dashboard for the first time, the platform will prompt you to select the platform corresponding to the application (mobile end, web end, Mini Program end, etc.). After the selection is completed, the platform will automatically preset the corresponding dashboard.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a3bdaee72bc4480b9101b9eab27fd08~tplv-goo7wpa0wc-image.image) </span>

Assuming that you select the Dashboard & indicator on the mobile terminal, and you need the indicators on other terminals in the future, you can configure it as a Dashboard through the "Scene Template" \- "General" re\-positioning template.

The indicator criteria of the preset Dashboard at each end is explained.

<span id="_1-关于统计人数的口径id"></span>
# 1. About the criteria ID of the statistics

When calculating the number of people (or users), the default is to sum the SSIDs of the relevant events, that is, the number of people is SSID by default.

<span id="_2-预置看板中用到的指标说明"></span>
# 2. Description of indicators used in the preset Dashboard


|Dashboard name |App terminal |Indicator name |Calculation method |
|---|---|---|---|
|new user analysis |Inter\-App communications |new users |Total number of deduplicates reported for the first time in the time frame and any_active_event occurred |
|||active users |Total number of deduplicates any_active_event occurred in the time frame |
|||user retention rate |In the time frame, the first event & return visit event are any_active_event users |
||mobile end |new users |Total number of deduplicates reported for the first time in the time frame app_launch and app_platform = app |
|||active users |Total number of deduplicates app_launch and app_platform = app in time frame |
|||user retention rate |In the time frame, the first event & return visit event are both app_launch and app_platform = percentage of users of the app |
|||new users from all sources |In the time frame, there is a behavior report for the first time in the time frame, app_launch has occurred and app_platform = the channel distribution of the total number of deduplicates of the app |
|||new user activation channel distribution |In the time frame, there is a behavior report for the first time in the time frame, app_launch has occurred and app_platform = the activation channel distribution of the total number of deduplicates of the app |
|||Daily visits per capita |Average daily number of app_launch in time frame and app_platform = app |
|||weekly active days distribution |The distribution of days app_launch and app_platform = app in the past 7 days |
||web page |new users |Total number of deduplicates reported for the first time in the time frame predefine_pageview and app_platform = web |
|||active users |Total number of deduplicates that predefine_pageview and app_platform = web in time frame |
|||user retention rate |In the time frame, the first event & return visit event are both predefine_pageview and app_platform = web user percentage |
||Mini Program |new users |Total number of deduplicates reported for the first time in the time frame app_launch app_platform = mp |
|||active users |Total number of deduplicates that have any_active_event and app_platform = mp in time frame |
|||user retention rate |In the time frame, the proportion of the total number of deduplicates whose first event & return visit event are any_active_event and app_platform = mp |
|active user analysis |inter\-App communications |active users |Total number of deduplicates reported in the time frame and any_active_event occurred |
|||active user trend |Total number of deduplicates that any_active_event occurred daily in the time frame |
|||percentage of new users |Percentage of total deduplicates any_active_event the first event in the time frame |
|||old and new user structure |First Incident & Return Incident are any_active_event total population distribution |
||mobile end |active users |Total number of deduplicates reported in the time frame app_launch and app_platform = app |
|||active user trend |Total number of deduplicates app_launch per day in time frame and app_platform = app |
|||percentage of new users |Percentage of users with app_launch first event and app_platform = app in time frame |
|||old and new user structure |Time frame, first & return events are app_launch and app_platform = deduplicate user distribution of the app |
||web page |active users |Total number of deduplicates reported in the time frame predefine_pageview and app_platform = web |
|||active user trend |Total number of deduplicates per day that predefine_pageview and app_platform = web in time frame |
|||percentage of new users |Percentage of users whose first event is predefine_pageview and app_platform = web |
|||old and new user structure |Time range, first & return events are predefine_pageview and app_platform = deduplicate user distribution of web |
||Mini Program |active users |Total number of deduplicates reported app_launch and app_platform = mp in the time frame |
|||active user trend |Total number of deduplicates that have occurred app_launch per day with app_platform = mp in the time frame |
|||percentage of new users |Percentage of deduplicate users with app_launch first event and app_platform = mp in time frame |
|||old and new user structure |The user distribution of the first & return events is app_launch and app_platform = mp in the time range |
|user retention analysis |inter\-App communications |next day retention |Number of deduplicate users any_active_event in time frame, day before & yesterday/number of deduplicate users any_active_event day before |
|||retention trend |The number of deduplicate users any_active_event on t\-n days & t\-1 days in the time range/the number of deduplicate users any_active_event on t\-n days |
|||next week retention |Number of deduplicate users any_active_event last week & last week/deduplicate users any_active_event last week in time frame |
|||retention trend |Number of deduplicate users any_active_event n weeks ago & last week/number of deduplicate users any_active_event n weeks ago |
||mobile end |next day retention |In the time frame, the day before & yesterday app_launch and app_platform = the number of deduplicate users of the app/the day before app_launch and app_platform = the number of deduplicate users of the app |
|||retention trend |In the time frame, app_launch occurred on t\-n days & t\-1 days and app_platform = deduplicate users of app/app_launch occurred on t\-n days and app_platform = deduplicate users of app, in units |
|||next week retention |Time frame, last week & last week app_launch and app_platform = deduplicate users of app/last week app_launch and app_platform = deduplicate users of app |
|||retention trend |Occurred n weeks ago & last week app_launch and app_platform = deduplicate users of app/n weeks ago app_launch and app_platform = deduplicate users of app in |
||web page |next day retention |Time frame, day before & yesterday predefine_pageview and app_platform = deduplicate users of web/day before predefine_pageview and app_platform = deduplicate users of web |
|||retention trend |In the time frame, t\-n days & t\-1 days have occurred predefine_pageview and app_platform = deduplicate users of the web/t\-n days have occurred predefine_pageview and app_platform = deduplicate users of the web |
|||next week retention |Time frame, last week & last week predefine_pageview and app_platform = deduplicate users of web/last week apredefine_pageview and app_platform = deduplicate users of web |
|||retention trend |Occurred n weeks ago & last week predefine_pageview and app_platform = deduplicate users of web/n weeks ago predefine_pageview and app_platform = deduplicate users of web |
||Mini Program |next day retention |The number of deduplicate users that occurred app_launch the day before & yesterday and app_platform = mp in the time range/The number of deduplicate users that occurred app_launch the day before and app_platform = mp |
|||retention trend |Number of deduplicate users app_launch on t\-n days & t\-1 days and app_platform = mp/number of deduplicate users app_launch on t\-n days and app_platform = mp |
|||next week retention |Number of deduplicate users that occurred in the previous week & last week app_launch and app_platform = mp/Number of deduplicate users that occurred in the last week app_launch and app_platform = mp |
|||retention trend |Number of deduplicate users app_launch n weeks ago & last week with app_platform = mp/number of deduplicate users app_launch n weeks ago with app_platform = mp |
|user lifecycle |inter\-App communications |active user |Total number of deduplicates any_active_event during the calculation period |
|||new user |Total number of deduplicates any_active_event for the first time during the calculation period. That is, if the time interval is 7 days and the start date is January 1, then the user who has triggered the any_active_event event for the first time from January 1 to January 7 is considered a new user; |
|||retained user |Number of users who any_active_event in the previous period |
|||returned user |Number of users who did not occur in the previous period but any_active_event in the current period |
|||lapsed user |Number of users any_active_event in the previous period but not in the current period |
||mobile end |active user |Total number of deduplicates app_launch and app_platform = app in the period |
|||new user |Total number of deduplicates that app_launch for the first time in this calculation cycle and app_platform = app. That is, if the time interval is 7 days and the start date is January 1, then the user who has triggered the app_launch event for the first time from January 1 to January 7 is considered a new user; |
|||retained user |Number of users app_launch and app_platform = app |
|||returned user |Number of users who did not occur in the previous period but app_launch in the current period and app_platform = app |
|||lapsed user |Number of users app_launch and app_platform = app |
||web page |active user |Total number of deduplicates predefine_pageview with app_platform = web in this period |
|||new user |The total number of deduplicates that predefine_pageview for the first time in this calculation cycle and app_platform = web. That is, if the time interval is 7 days and the start date is January 1, then the user who has triggered the any_active_event event for the first time from January 1 to January 7 is considered a new user; |
|||retained user |Number of users predefine_pageview and app_platform = web |
|||returned user |Number of users who did not occur in the previous period but predefine_pageview in the current period and app_platform = web |
|||lapsed user |Number of users predefine_pageview and app_platform = web |
||Mini Program |active user |Total number of deduplicates app_launch in the period with app_platform = mp |
|||new user |The total number of deduplicates that app_launch for the first time in the calculation period and app_platform = mp. That is, if the time interval is 7 days and the start date is January 1, then the user who has triggered the app_launch event for the first time from January 1 to January 7 is considered a new user; |
|||retained user |Number of users app_launch in the previous and current period and app_platform = mp |
|||returned user |Number of users that did not occur in the previous period but app_launch in the current period and app_platform = mp |
|||lapsed user |Number of users app_launch in the previous period but not in the current period and app_platform = mp |
|Customer engagement |Inter\-App communications |main Event Analysis (Number & Number of People) |Time range, number of any_active_event & number of event name distributions |
|||daily visits per capita |Average number of triggers that occurred any_active_event users over time |
|||city distribution (number of times & number of people) |City distribution of any_active_event users over time |
||mobile end |number of sessions |Total number of active users in the app in the time frame (app launch) |
|||conversations per capita |Number of total calls/sessions in the app by active users in the time frame (app launch) |
|||average screen time |Time frame, active users in the app/number of users (app launch) |
|||average usage time |Time frame, active users in\-app usage/usage (app launch) |
|||daily visits per capita |Time frame, app_launch and app_platform = average number of triggers for app users |
|||city distribution (number of times & number of people) |City distribution of app_launch users over time |
||web page |number of views |Total number of predefine_pageview in the time frame |
|||IP number |The number of deduplicate IPs predefine_pageview in the app and app_platform = web |
|||number of sessions |The number of sessions that have predefine_pageview in the time frame and app_platform = web |
|||average session duration |Time range, total duration of all sessions/number of sessions, in seconds |
|||daily visits per capita |Time frame, predefine_pageview occurred and app_platform = average number of web users |
|||source website \- session count distribution |In the time frame, predefine_pageview occurred under each source website and app_platform = number of webs |
|||page exit rate |Time frame, exit rate of each website page (last website in session) |
|||city distribution (number of sessions & number of sessions) |In time frame, predefine_pageview occurred and app_platform = city distribution of web users |
||Mini Program |number of visits |Total number of app_launch in the application over time |
|||visits per capita |Total number/number of app_launch in the app over time |
|||average screen time |Time frame, session usage/number of sessions app_terminte in the app |
|||scene value visits |Distribution of the number of times to enter the Mini Program through the Mini Program scene value in the time range |
|||QR code scan times |Number of times the Mini Program QR code was scanned in the time frame |
|||city distribution (number of times & number of people) |City distribution of app_launch users over time |
|user channel distribution |mobile end |new user |Time frame, new user app_launch and app_platform = app's (first) source channel (app_channel) |
|||Day Retention Ratio at Day 1 |Time frame for the first time in each source channel (app_channel) app_launch and app_platform = Day Retention Ratio at Day 1 of the app |
|||active user |Time frame app_launch and app_platform = (first time) source channel of active users of the app (app_channel) |
|||Day Retention Ratio at Day 1 |Day Retention Ratio at Day 1 for active users in each source channel (app_channel) |
|||daily active users |Average number of app_launch by source (app_channel) in the last 30 days app_platform = deduplicate app |
|||daily new users |Average number of app_launch by source (app_channel) in the last 30 days app_platform = deduplicate app |
|||daily usage per capita |Number of daily app_launch and app_platform = app per person per source channel (app_channel) over the past 30 days |
|||Daily usage time per capita (s) |In the past 30 days, app_launch per person per day in each source channel (app_channel) and app_platform = app duration |
|user device distribution |mobile end |Operating System \- Number/Number of Active Users |Over time, app_launch occurred and app_platform = OS distribution of app users |
|||Mobile phone brands \- number of active users/frequency distribution |In the time frame, app_launch occurred and app_platform = distribution of mobile phone systems of app users |
|||Device Model \- Number of Active Users/Number Distribution |Over time, app_launch occurred and app_platform = device type distribution of app users |
|||System Version \- Number/Number of Active Users |In time frame, app_launch occurred and app_platform = distribution of system types for app users |
|||Resolution \- number of active users/frequency distribution |Over time, app_launch occurred and app_platform = resolution distribution of app users |
|||Network Type \- Number of Active Users/Number Distribution |Over time, app_launch occurred and app_platform = Network type distribution of app users |
|||Operators \- Number/Number of Active Users |Over time, app_launch occurred and app_platform = operator distribution of app users |
||web page |End point type \- number of active users/number distribution |Over time, predefine_pageview occurred and app_platform = end point type distribution for web users |
|||Operating System \- Number/Number of Active Users |Operating system distribution of predefine_pageview and app_platform = web users over time |
|||Browser \- Number of active users/distribution |In time frame, predefine_pageview occurred and app_platform = browser distribution of web users |
|||Resolution \- number of active users/frequency distribution |Over time, predefine_pageview occurred and app_platform = resolution distribution of web users |
|||Locale \- Number/Number of Active Users |Over time, predefine_pageview occurred and app_platform = locale distribution of web users |
|web page access analysis |web page |traffic |Total number of predefine_pageview in the time frame |
|||page visitors |Total number of deduplicates predefine_pageview and app_platform = web in time frame (based on cookies) |
|||Number of IP addresses |Time frame predefine_pageview and app_platform = number of IPs for web |
|||Page bounce rate |Exit pages as exit pages as a percentage of predefine_pageview and app_platform = total number of web exits |
|||Average visit duration (s) |The average length of all sessions that meet the filter criteria within the time range |
|||Average depth of visit |All filtered sessions in the time range occurred predefine_pageview and app_platform = average number of web |
|referrer analysis |web page |active user |Total number of deduplicates predefine_pageview and app_platform = web in time frame (based on cookies) |
|||Average session duration (s) |Total duration of all sessions/number of sessions in the time range |
|||average session depth |Sum of session depth (predefine_pageview) for all sessions in time frame/number of sessions |
|||session count |Number of sessions that occurred predefine_pageview and app_platform = web |
|||bounce rate |Number of sessions that left the site after only one page ((predefine_pageview)) % of total sessions |
|page view analysis |Mini Program |Mini Program Page Views |Number of users visiting any page (predefine_pageview) in the Mini Program in the selected time frame |
|||page views |Number of visits to any page within the Mini Program (predefine_pageview) in the selected time frame |
|||exit rate |Number of exits from the Mini Program exit page (app_terminate)/total number of visits to any page (predefine_pageview) within the Mini Program in the selected time frame |
|||share count |The actual number of shares generated within the Mini Program within the selected time frame |
|||entry page count |Number of Mini Program visits (app_launch) in the selected time frame |
|||exit page count |Number of Mini Program exits (app_terminate) in the selected time frame |
|||length of stay per capita |Total number of hours/visits to the Mini Program's page (predefine_pageview) in the selected time frame |
|||average length of stay |Total length/number of visits to the Mini Program's page (predefine_pageview) in the selected time frame |
|scenario value analysis |Mini Program |Scene value visits |Number of visits to scene values in the Mini Program within the selected time frame |
|||Scenario Value Visitors |Number of visitors to the scene value in the Mini Program in the selected time frame |
|||scene value page views |Scene value distribution of visiting pages (predefine_pageview) in the Mini Program for the selected time frame to understand the referrer of each page |
|||Scene value average screen time |Access the Mini Program's average screen time by scene value for the selected time range |
|||scene value average usage time |The average usage time of accessing the Mini Program by scenario value within the selected time frame |
|share analytics |Mini Program |share count |The number of genuine shares generated within the Mini Program within the selected time frame |
|||share count |The number of genuine shares generated within the Mini Program within the selected time frame |
|||return traffic |Number of times to enter the Mini Program through the share link within the selected time frame |
|||Share the re\-engagement rate |The number of times you entered the Mini Program through the share link/share within the selected time frame |
|||share new user |The number of new users who entered the Mini Program through the share link in the selected time frame |
|||Number of page views per share |The number of visits to each page through the share link within the selected time frame |
|QR code analysis |Mini Program |number of scans |Number of Mini Program QR code scans in the selected time frame |
|||number of people scanning the code |Number of people scanning the Mini Program QR code in the selected time frame |
|||Scan the code to add new people |The number of new scanners of the Mini Program QR code within the selected time frame |
|||QR code number |The number of QR codes that were overscanned in the selected time frame |
