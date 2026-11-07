---
title: "Preset User Properties"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Preset-User-Properties"
---

The system provides you with a large number of preset user properties, and also provides you with preset events that customize bound user properties, so that you can customize user properties through this event.

<span id="134aacf0"></span>
# Preset user properties


|**Property name** |**Property value type** |**Data source** |**Property description** |
|---|---|---|---|
|web_id |String |Server side generation | |
|device_id |String |user incoming | |
|user_is_new |Number |Server side generation |The main difference between new and old users (user_is_new) and whether the first day of access ($is_first_day) is that the former is affected by the selected time period, while the latter is not affected, so the latter has better consistency in the calculation results obtained in different chart types. It is recommended to use whether the first day of access ($is_first_day) to judge new and old users.<br><br>First day visit ($is_first_day): The target event and the first event occurred on the same day.<br><br>user_is_new: The target event and the first event occur in the same cycle. For example, in a bar chart, the period is the time frame selected by the user. |
|first_event_time |String |Server side generation |activation time |
|last_active_date |String |Server side generation |Last active date |


<span id="08c938b8"></span>
# User property binding


|**Event name** |**Event display name** |**Property** |
|---|---|---|
|__profile_set |user properties |Properties are custom user properties |
|__profile_set_once |user properties |Properties are custom user properties |
|__profile_unset |Cancel user properties |Properties are custom user properties |
|__profile_increment |incremental user properties |Properties are custom user properties |
|__profile_append |Add user properties |Properties are custom user properties |
