---
title: "CalendarUtils"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/calendarutils"
---

The calendar utility class.

<span id="d142e499"></span>
## Member Functions

<span id="80157294"></span>
### addCalendarEvent

Creates a system calendar event.

```Java
public static boolean addCalendarEvent(Context context, String eventTitle, long startTimeInMillis, long endTimeInMillis, int advanceMinutes)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|context |Context |The context of the live room page. |
|eventTitle |String |The title of the event, that is, the name of the live room. |
|startTimeInMillis |Long |The start time of the live stream in Unix timestamp format. Unit: ms. |
|endTimeInMillis |Long |The end time of the live stream in Unix timestamp format. Unit: ms. |
|advanceMinutes |Integer |How long a notification is sent in advance of the start time of the live stream. Unit: minutes. |


**Return Value**


|Type |Description |
|---|---|
|Boolean |Whether the system calendar event creation is successful.<br><br><br>* `true`: Successful.<br><br>* `false`: Failed. |
