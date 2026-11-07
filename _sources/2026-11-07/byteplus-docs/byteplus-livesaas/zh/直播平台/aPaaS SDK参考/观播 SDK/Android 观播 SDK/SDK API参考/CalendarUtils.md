---
title: "CalendarUtils"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/calendarutils-zh-CN"
---

CalendarUtils 类提供了一个静态方法，帮助你将事件添加到终端用户的系统日历中。使用该工具可以以编程方式为即将到来的事件（如直播流）创建日历条目，并为其配置提前通知。

<span id="d142e499"></span>
## 成员函数

<span id="80157294"></span>
### addCalendarEvent

向系统日历添加一个事件。

```Java
public static boolean addCalendarEvent(Context context, String eventTitle, long startTimeInMillis, long endTimeInMillis, int advanceMinutes)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|context |Context |直播间页面的上下文。 |
|eventTitle |String |事件标题，即直播间名称。 |
|startTimeInMillis |Long |直播流开始时间，Unix 时间戳格式。单位：ms。 |
|endTimeInMillis |Long |直播流结束时间，Unix 时间戳格式。单位：ms。 |
|advanceMinutes |Integer |直播流开始前发送通知的分钟数。单位：分钟。 |


**返回值**


|类型 |接口行为 |
|---|---|
|Boolean |如果事件添加成功，则返回 true；否则返回 false。<br><br><br>* `true`：成功。<br><br>* `false`：失败。 |
