---
title: "Data about RTC Calls"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70136"
---

To analyze your RTC call data by specific business scenarios, you can use the `BusinessId` to tag and aggregate data. This guide shows you how to view general quality, operational, and real\-time data in the console, and provides step\-by\-step instructions for setting up `BusinessId` to enable scenario\-based data aggregation.


* On the `Monitor Center > Quality Overview` page, you can view quality\-related indicators, such as stall rate and network transmission latency compliance.

* On the `Monitor Center > Operation Data` page, you can view user activity indicators, such as the total number of users and the total number of rooms.

* On the `Monitor Center > Real-time monitoring` page, you can view indicators related to device, location, and SDK version.


The monitoring interface includes the following pages:


* Quality Overview:


<span>![图片](https://p16-arcosite-sg.ibyteimg.com/tos-alisg-i-k9wyc2ijk0-sg/4757951763af4a6291bc908e6e612333~tplv-k9wyc2ijk0-image.image) </span>


* Operation Data:


<span>![图片](https://p16-arcosite-sg.ibyteimg.com/tos-alisg-i-k9wyc2ijk0-sg/141e6452b0dc47eb82a04493f82093b7~tplv-k9wyc2ijk0-image.image) </span>


* Real\-time monitoring:


<span>![图片](https://p16-arcosite-sg.ibyteimg.com/tos-alisg-i-k9wyc2ijk0-sg/c62ada12e6e4461a90a7111f64a0abe3~tplv-k9wyc2ijk0-image.image) </span>

<span id="aggregate-call-data-by-business-scenario"></span>
## Aggregate call data by business scenario

When viewing these call data, you can aggregate data by dimensions such as `AppId`, `BusinessId`, and time period. For example, when you use RTC to build an application for video conferencing for internal use and you need to view usage data for various departments, you can use `BusinessId` to tag calls by department. This allows you to view each department's usage data in the console.

<span id="procedure"></span>
### Procedure

Refer to the following steps to aggregate and view relevant data:


1. Go to the `Console > BusinessId` page, and add the BusinessId you need under AppId. As shown in the figure below, the application with `AppId = defaultAppName` has a `BusinessId` named `chatroom`.


<span>![图片](https://p16-arcosite-sg.ibyteimg.com/tos-alisg-i-k9wyc2ijk0-sg/b4f8e50053ee4247830e330f93b910b6~tplv-k9wyc2ijk0-image.image) </span>

You can add a new `BusinessId` such as `livePK` shown below:

<span>![图片](https://p16-arcosite-sg.ibyteimg.com/tos-alisg-i-k9wyc2ijk0-sg/0eabf103dc8c41fc88bc7898ff6f1038~tplv-k9wyc2ijk0-image.image) </span>

2. When the service is enabled, set the corresponding `AppId` and `BusinessId` to tag the service data with these identifiers.

When enabling audio & video calls, you can use the following interfaces to set the `BusinessId`:


* Android: [setBusinessId](https://docs.byteplus.com/en/docs/12/docs-70080#setbusinessid)

* iOS: [setBusinessId](https://docs.byteplus.com/en/docs/12/docs-70086#setbusinessid)

* macOS: [setBusinessId](https://docs.byteplus.com/en/docs/12/docs-70092#setbusinessid)

* Windows: [SetBusinessId](https://docs.byteplus.com/en/docs/12/docs-70095#setbusinessid)

* Website: [setBusinessId](https://docs.byteplus.com/en/docs/12/docs-104478#setbusinessid)

3. Once your users place audio & video calls using the app, you can aggregate and view the relevant data according to `BusinessId` on the console.
