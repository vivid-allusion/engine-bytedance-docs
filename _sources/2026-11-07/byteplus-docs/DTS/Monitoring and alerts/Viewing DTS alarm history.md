---
title: "Viewing DTS alarm history"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Viewing_DTS_alarm_history"
---

After an alarm is triggered for a Database Transmission Service (DTS) resource task, an alarm history is automatically generated to record information such as the name of the faulty resource, the time the alarm occurred, the duration of the alarm, the alarm level, and the alarm policy name. This facilitates unified and convenient backtracking and view of alarm records. This topic describes how to view historical alarm information of DTS in the Cloud Monitor console.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The alarm history is saved for a maximum of 14 days.

* The resource task is an alarm history from the first time the alarm is triggered to the return to normal. If the alarm is triggered again after recovery, another alarm history will be generated.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [Cloud monitor console](http://console.volcengine.com/cloud-monitor/overview).

2. In the left navigation bar, select **Alarm center** \> **Alarm history**.

3. Above the alarm history list, you can select a target time period and set filters to filter out the target alarm history.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_745ad92c8f10d867315a1191e39a19d0.png) </span>
