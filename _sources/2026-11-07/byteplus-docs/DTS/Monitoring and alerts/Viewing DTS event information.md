---
title: "Viewing DTS event information"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Viewing_DTS_event_information"
---

The event center provides fault monitoring for cloud products. When an event occurs in Database Transmission Service DTS, information such as the event time, event source, event name, and event details is saved to the Event center. By viewing Database Transmission Service DTS events, you can identify and resolve issues in a timely manner. This topic describes how to view Database Transmission Service DTS events in the Cloud Monitor console.

<span id=".5p-l55yLLWR0cy3nmoTkuovku7Y="></span>
## Viewing Database Transmission Service DTS events


1. Log on to the [Cloud Monitor console](https://console.byteplus.com/cloud-monitor/overview).

2. In the left\-side navigation pane, choose **Event center** \> **Cloud Product Event**.

3. On the **Cloud Product Event** page, view the Event information of Database Transmission Service DTS within the specified time range.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2aed02e2b2c17fe035c28739d4a2aec3.png) </span>

   You can filter events by specifying a time range and event type. Description:

   * As shown in area ① in the preceding figure, you can quickly select or custom select a time range to filter events that occurred within that time range.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">The system will query event information within the last hour by default. You can query data from the last 30 days at most.      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">The specified time range is accurate to the minute, with the seconds value defaulting to 00.      </div>
      

   * As shown in area ② in the preceding figure, select **Database Transmission Service** and event type to filter Event information.

   * As shown in area ③ in the preceding figure, you can View the list of events that meet the filter condition. The **Event** string consists of three parts. The format is `Event Source:Event Type:Event Content`.

4. In the **Action** column of a specific event, click **Details** to view the detailed information of the event in JSON format.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bf5292a32d4998854a0a8d2c54e14389.png) </span>
