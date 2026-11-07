---
title: "Creating on-call schedules"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Creating_on-call_schedules"
---

An on\-call schedule is used to arrange the on\-call personnel responsible for receiving notification messages during a specific period. Properly designed schedules ensure notifications and alerts are responded to promptly and handled properly. This topic describes how to create an on\-call schedule.

<span id="HTXr1A2j"></span>
## Limits


* Currently, you can create up to 1,000 on\-call schedules.

* Each on\-call schedule can contain up to 10 on\-call layers and 10 substitutes.

* Each on\-call layer can contain up to 10 on\-call shifts, and each shift can contain up to 10 on\-call contacts and 10 on\-call groups.


<span id="ssd7uJSl"></span>
## Procedure


1. Log in to the [Observability Platform console](https://console.byteplus.com/observe/dashboard/dashboard).

2. In the left navigation pane, select "**Alert Center \-\> Notification configuration**" to go to the "Notification configuration" page.

3. Select the **Duty plan** tab, click **Create a watch schedule**, and configure the on\-call schedule parameters as needed.

   
   |Parameter |Description |
   |---|---|
   |Name of duty plan |Specify a name for the on\-call schedule as a unique identifier. Duplicate names are not allowed. |
   |Duty rotation configuration |Configure on\-call rotation layers as needed, including on\-call layers and substitutes. To reorder on\-call layers or substitutes, drag <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0fe5c1dacdbb5862fbe539835fa92584.png) </span>in the upper\-right corner of the target on\-call layer or substitute.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Within the same time period, substitutes take precedence over on\-call layers. When both a substitute and an on\-call layer are configured, notifications and alert messages are sent directly to the contacts in the substitute.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Within the same time period, if multiple substitutes or on\-call layers are configured, notifications and alert messages are sent to contacts in a higher\-priority substitute or on\-call layer based on the on\-call rotation order.</div><br><br><br>* **Duty layer**: The core configuration layer of an on\-call rotation. It defines key information such as the time range, effective range, rotation interval, and on\-call shifts of the current on\-call schedule.<br><br>* **Substitute**: The backup for on\-call layers, with similar configurations to the on\-call layer. This feature is typically used for temporary shift swaps. For example, if a contact in the regular on\-call layer is absent due to leave or other reasons and cannot check alerts or troubleshoot issues promptly, we recommend temporarily assigning another contact as a substitute. This keeps the original on\-call schedule intact while ensuring that notifications and alerts are responded to promptly and handled properly. |
   |On\-call time range |The time range of the on\-call schedule. You can customize the on\-call start time and end time as needed.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If you do not specify an on\-call end time, the schedule repeats indefinitely.</div><br> |
   |Effective period range |The effective time range is a subset of the on\-call time range. This parameter defines when on\-call work is actually required within the time range of the on\-call schedule.<br><br><br>* **Always**: The effective time range is identical to the on\-call time range.<br><br>* **Every day**: Select one or more time periods within the on\-call time range each day for on\-call work. You can specify one or more time periods. |
   |Rotation interval |The interval of on\-call shift rotation, which can be configured as needed. For example, suppose there are two on\-call shifts, and you set the rotation interval to one day. The first shift is on call for one day, and then the second shift takes over. This cycle continues until the on\-call ends. |
   |Shift |The contacts who are actually on call. You can add multiple on\-call shifts as needed. You can select multiple contacts or contact groups. To reorder on\-call shifts, drag <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5b3d1f1b51324fff04ba192b31cf5714.png) </span> to the left of the target shift. |
   

4. You can preview the schedule in real time in the calendar on the right. After you confirm that the settings are correct, click **Confirm** to complete creating the on\-call schedule.


<span id="hLxGSIX6"></span>
## What to do next

When you create a notification policy, you can select an on\-call schedule as the notification recipient target. For notification policy details, see [Creating notification policies](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_notification_policies).
