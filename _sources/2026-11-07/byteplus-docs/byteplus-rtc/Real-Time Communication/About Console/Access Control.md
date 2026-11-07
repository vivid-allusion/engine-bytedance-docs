---
title: "Access Control"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1134900"
---

To enhance security and implement fine\-grained control over your RTC resources, you can use Identity and Access Management (IAM) users. This document provides a comprehensive list of IAM policies required for accessing different features on the RTC console, enabling you to grant the least privilege necessary for specific tasks.

> Refer to [Creating an IAM user](https://docs.byteplus.com/en/byteplus-platform/docs/creating-a-user) for information on how to create IAM users.


<span id="requirement-for-iam-users"></span>
## Requirement for IAM users

To access all pages on the RTC console, go to [IAM](https://console.byteplus.com/iam/policymanage) and choose a policy below and apply it to the sub\-account. You can also apply the respective policy for each page.

Always grant your IAM user the minimum permissions required for the specific task (the principle of least privilege).

 &nbsp;


|Feature |Description |Policy | |
|---|---|---|---|
|Full access to all pages on the RTC console |Read and write |RTCFullAccess | |
|Full access to all pages on the RTC console |Read only |RTCReadOnlyAccess | |
|**Application Management** and **Business ID** |Read and write |RTCAppBusinessIdentityFullAccess | |
|**Application Management** and **Business ID** |Read only |RTCAppBusinessIdentityReadOnly | |
|**Monitor Center** \> **Diagnostic Tools** |A useful tool that helps you quickly analyze and diagnose experience problems during RTC calls, such as video with no sound or a video stall. |RTCMonitorDiagnosisAccess | |
|**Monitor Center** \> **Real\-time Metrics** |Real\-time statistics on quality data, usage data, and operation data. |RTCMonitorRealTimeAccess | |
|**Monitor Center** \> **Alerts** |To be notified promptly of call abnormalities, configure alert rules that define when and how you are informed. |RTCAlarmReadOnlyAccess<br><br>RTCAlarmFullAccess | |
|**Monitor Center** \> **Quality Overview** |You can view quality data for a specific time period by application or business ID, such as the success rate of joining rooms, freeze rate, success rate of sending the first frame, and success rate of decoding the first frame. |RTCMonitorQualityAccess | |
|**Monitor Center** \> **Operational Data** |Operation Data provides helpful statistics for operators including numbers of users and rooms, duration of each call, the number of calls. You can view data for a specific time period by application or business ID. |RTCMonitorQualityAccess | |
|**Monitor Center** \> **Cloud Media Processing** |Provides quality data on Cloud Media Processing, which includes Cloud Recording, Push to CDN, Snapshot, and Segment. |RTCPostProcessQualityAccess | |
|**Monitor Center** \> **RTS Quality Data** |Read and write |RTCMonitorQualityAccess |RTS quality data. |
|**Usage Statistics** |Read and write |RTCUsageStatisticsAccess | |
|**Settings** |Read only |RTCConfigurationReadOnlyAccess | |
|**Settings** |Read and write |RTCConfigurationFullAccess | |
|**Settings** \> **Cloud Recording** |VOD resource access |VodFullAccess | |


<span id="before-using-additional-service-with-an-iam-user"></span>
## Before using additional services with an IAM user

For features that require BytePlus services besides RTC, such as [Cloud recording](https://docs.byteplus.com/en/docs/12/docs-115526), ensure the BytePlus account that owns the IAM users meets the following requirements.


* The `ServiceRoleForRTC` role has been added to your BytePlus account through [Cross-service authorization](https://console.byteplus.com/iam/service/attach_role?ServiceName=rtc).

* Your BytePlus account has enabled or purchased the [BytePlus Video on Demand (VOD)](https://www.byteplus.com/en/product/vod) service.

* Refer to the [table above](https://docs.byteplus.com/docs/byteplus-rtc/docs-1134900#permission) and grant IAM users necessary permissions.
