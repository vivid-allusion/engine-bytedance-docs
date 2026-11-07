---
title: "CalendarUtils"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/calendarutils-zh-TW"
---

CalendarUtils 類別提供一個靜態方法，協助你將事件新增至終端使用者的系統行事曆。使用此工具可程式化地為即將到來的事件（例如直播）建立行事曆條目，並設定提前通知。

<span id="d142e499"></span>
## 成員函式

<span id="80157294"></span>
### addCalendarEvent

將事件新增至系統行事曆。

```Java
public static boolean addCalendarEvent(Context context, String eventTitle, long startTimeInMillis, long endTimeInMillis, int advanceMinutes)
```


**輸入參數**


|名稱 |型別 |說明 |
|---|---|---|
|context |Context |直播間頁面的 context。 |
|eventTitle |String |事件標題，即直播間名稱。 |
|startTimeInMillis |Long |直播開始時間，採 Unix 時間戳格式。單位：毫秒。 |
|endTimeInMillis |Long |直播結束時間，採 Unix 時間戳格式。單位：毫秒。 |
|advanceMinutes |Integer |直播開始前發送通知的分鐘數。單位：分鐘。 |


**回傳值**


|型別 |說明 |
|---|---|
|Boolean |若事件新增成功則回傳 true，否則回傳 false。<br><br><br>* `true`：成功。<br><br>* `false`：失敗。 |
