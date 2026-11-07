---
title: "Introduction"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70065"
---

You can create and manage Apps on the [RTC Console](https://console.byteplus.com/rtc/workplaceRTC). The RTC Console is the portal for you to purchase and manage RTC products and services. And it also provides statistics on quality and operation data for RTC calls.

> To safeguard your account and data during the collaboration, we recommend you create [Identity and Access Management (IAM)](https://console.byteplus.com/iam) users and access RTC service and data with each of them. An IAM user is also referred to as a sub\-account user. Grant your IAM user the [necessary permissions](https://docs.byteplus.com/en/docs/12/docs-1134900).


<span id="app-management"></span>
## App Management


|Feature |Description |
|---|---|
|[App Management](https://console.byteplus.com/rtc/listRTC) |Create and manage applications. App management includes temporary\-Token generation and Token verification. Refer to [Before Using RTC Service](https://docs.byteplus.com/en/docs/12/docs-69865) for more details. |
|[Business ID](https://console.byteplus.com/rtc/bidRTC) |Create and manage business IDs. Categorize the applications by labeling an application with a business ID. You can then configure all applications with the same business ID using a single set of configurations. View statistics on the call quality and usage data by business ID.<br><br>Tagging a business ID on the RTC Console is equivalent to calling setBusinessId in the SDK. Refer to [Setting Configurations for Scenarios](https://docs.byteplus.com/en/docs/12/docs-70135) for more details. |


<span id="monitor-center"></span>
## Monitor Center

The Monitoring Center provides dashboards for call quality and operational data.

To allow a sub\-account to access the following tools and data metrics on the console or via the OpenAPI, apply the required policy to that sub\-account.


|Feature |Description |
|---|---|
|[Diagnostic Tool](https://console.byteplus.com/rtc/callQualityRTC/diagnosis) |A tool that helps you quickly analyze and diagnose call experience issues, such as video with no audio or video stalls. |
|[Real-time Metrics](https://console.byteplus.com/rtc/callQualityRTC/monitor) |Real\-time statistics on quality data, usage data, and operation data. |
|[Alerts](https://console.byteplus.com/rtc/callQualityRTC/alarm) |To receive prompt notifications about call anomalies, configure alert rules that define the trigger conditions and notification methods. |
|[Quality Overview](https://console.byteplus.com/rtc/callQualityRTC/qos) |You can view the quality data for a specific time period by application or business ID, such as success rates of joining rooms, freeze rate, success rates of sending the first frame, and the success rate of decoding the first frame. |
|[Operational Data](https://console.byteplus.com/rtc/callQualityRTC/operation) |Operation Data provides helpful statistics for operators including the number of users and rooms, the duration of each call, and the total number of calls. You can view the data for a specific time period by application or business ID. |
|[Cloud Media Processing](https://console.byteplus.com/rtc/callQualityRTC/postprocessing) |View quality data for Cloud Media Processing services, including Cloud Recording, Push to CDN, Snapshot, and Segment. |


<span id="usage-statistics"></span>
## Usage Statistics

Go to [Usage Statistics](https://console.byteplus.com/rtc/statisticsRTC) and view the usage data on calls and the other services. You can view the data for a specific time period by application or business ID.

<span id="additional-services"></span>
## Additional Services

Go to [Settings](https://console.byteplus.com/rtc/cloudRTC) to enable and manage services including [Cloud Recording](https://docs.byteplus.com/en/docs/12/docs-115526), [Push to CDN](https://docs.byteplus.com/en/docs/12/docs-69850), [Snapshot](https://docs.byteplus.com/en/docs/12/docs-snapshot), [Segment](https://docs.byteplus.com/en/docs/12/docs-155129), [Audio Selection](https://docs.byteplus.com/en/docs/12/docs-113547), and [Online Media Streaming](https://docs.byteplus.com/en/docs/12/docs-105188).

Note that you will be charged for using the additional services. Refer to [Pricing](https://docs.byteplus.com/en/docs/12/docs-69871) for the detailed billing rules.

<span id="procedure-for-enabling-additional-services-for-an-account"></span>
### Procedure for enabling additional services for an account

For services that utilize other BytePlus services, such as Cloud Recording, follow the instructions below.


1. Attach the ServiceRoleForRTC role to your BytePlus account to enable cross\-service authorization.

2. Ensure that you have enabled or purchased the [BytePlus Video on Demand (VOD)](https://www.byteplus.com/en/product/vod) service.

3. Go to [Settings](https://console.byteplus.com/rtc/cloudRTC) and toggle the button to start the service. Follow the on\-screen prompts to complete the required configuration.


<span id="callbacks"></span>
## Callbacks

To add and manage callback rules, go to [Settings](https://console.byteplus.com/rtc/cloudRTC)  **\> Callbacks**. Refer to [Enable Message Notification](https://docs.byteplus.com/en/docs/12/docs-75110) for more details on subscribing to notifications from the RTC server.
