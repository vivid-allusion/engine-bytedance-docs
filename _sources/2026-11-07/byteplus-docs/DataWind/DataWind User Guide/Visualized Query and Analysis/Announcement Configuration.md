---
title: "Announcement Configuration"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Announcement_Configuration"
---

The announcement feature supports displaying announcement pop\-ups in both the visual query panel and the dashboard panel. This article introduces the announcement configuration operations for visual queries. For the announcement configuration operations of dashboards, see [Dashboard Viewing Operations](https://docs.byteplus.com/docs/DataWind/Dashboard_Viewing_Operations).

<span id="c2f40712"></span>
# Prerequisites


* The user's account must have dataset editing permissions to **set announcements**.

* The user's account must have view\-only permissions for the dataset to **view announcements**.


<span id="_1-概述"></span>
# Feature overview

Users can improve the efficiency of conveying key information by configuring announcements. The specific content of announcement configuration includes setting announcements, displaying and closing announcements, and viewing announcements.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1ea031802f594a67be1ea2193ac9c912~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Copying, importing, or exporting datasets does not carry over announcements.</div>



<span id="02869a82"></span>
# Set announcements


1. Users can set announcements in the More menu on the right side of the dataset.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/92cd9637b5de44c484a9c36913ee0070~tplv-goo7wpa0wc-image.image) </span>

2. Configure announcements.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e203ed7edbfd425bb73016e01478cb32~tplv-goo7wpa0wc-image.image) </span>

   The parameter configuration instructions are as follows.

   
   |Parameters |Configuration instructions |
   |---|---|
   |Enable announcements |Select whether to enable announcements. After enabling, the announcement will be displayed when entering the visual query interface. |
   |Title |Up to 30 Chinese characters. |
   |Description |Up to 300 Chinese characters.<br><br><br>* Supports undo and redo.<br><br>* Supports applying bold, italic, and underline formatting, as well as inserting hyperlinks and images. |
   |Notification method |Supports two styles: floating window (top left) and pop\-up window (centered). |
   |Style type |Supports two style types: normal and warning.<br><br><br>* Normal style (for data specification updates)<br><br>   * Floating window<br><br>      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/87f6361eb5634d6782cca38f432f8b5b~tplv-goo7wpa0wc-image.image) </span><br><br>   * Pop\-up window<br><br>      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2e9094b5d5fe470aa333e587804c3d45~tplv-goo7wpa0wc-image.image) </span><br><br>* Warning style (for fault alerts)<br><br>   * Floating window<br><br>      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/facec174c5d24446abacb356c3274248~tplv-goo7wpa0wc-image.image) </span><br><br>   * Pop\-up window<br><br>      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b4feb1a419b44bcaa80130e240b7693~tplv-goo7wpa0wc-image.image) </span> |
   |Notification frequency |Supports only once, once every 7 days, or once every 30 days. |
   |Validity period |Disabled by default<br><br><br>* After enabling, a date range can be set. (The default is 00:00 on the current day to 23:59:59 seven days later)<br><br>* After enabling, the announcement will be displayed only when users access within the validity period. |
   


<span id="_2-功能介绍"></span>
# Announcement display and closure


* The announcement display effect has two style types based on the settings: normal and warning.

* After you manually close the announcement pop\-up, it will not be displayed again upon revisiting.

   * For announcements, with a reminder frequency of only once, after closing, it will not be displayed again;

   * for announcements with a reminder frequency of once every 7 days or once every 30 days, after closing, the pop\-up will not be displayed again within that 7\-day or 30\-day period, but will be displayed again in the next 7\-day or 30\-day period.

* If the content of the announcement (title or body) is updated, this rule will be reset.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f632811712454d5292866cd26c276e3f~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-查看公告"></span>
# View announcements

After you close the announcement pop\-up, you can click "View Announcements" in the More menu to view the announcement.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c6b9579d2f0d4a8fb85dc36b010684a4~tplv-goo7wpa0wc-image.image) </span>


* The "View Announcements" entry is displayed only when the announcement is enabled for the visualized dataset and is within the validity period.
