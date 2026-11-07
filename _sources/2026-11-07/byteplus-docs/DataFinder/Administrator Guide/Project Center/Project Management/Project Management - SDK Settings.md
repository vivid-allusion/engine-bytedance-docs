---
title: "Project Management - SDK Settings"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Project_Management_-_SDK_Settings"
---

DataFinder provides you with the ability to set up the SDK. You can adjust the SDK collection items without releasing the version on the client side through the SDK setting function. This article describes the parameters and setup instructions for SDK settings.

<span id="ce34e831"></span>
# Precautions


* When using Project Management \> SDK Settings to send SDK collection items to the client side, Android and iOS need to be upgraded to 6.15.0 and above versions, web needs to be upgraded to 5.1.8 and above versions, and Mini Program needs to be upgraded to 2.10.1 and above versions.

* The function is only open to administrators by default. If you need to adjust the SDK settings, it is recommended to contact your administrator or enable administrative permissions for you.


<span id="_2-功能介绍"></span>
# Function entrance

Project Center \> Project Management \> SDK Settings.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d5ee1889dd4442b086e7c9e5515d0042~tplv-goo7wpa0wc-image.image) </span>

<span id="44581bb8"></span>
# Settings Description

<span id="_2-1-1-全埋点采集"></span>
## Full event tracking


* Open: Indicates that the full event tracking event is allowed to be reported; note that if the SDK turns off the full event tracking collection locally (on the end), the full event tracking event cannot be reported even if the switch on the platform page is turned on. For full event tracking switch configuration details, please refer to the SDK access documentation of each end.

* Close: Indicates that full event tracking events are no longer reported.


<span id="_2-1-2-a-b实验"></span>
## A/B experiment


* On: Indicates that the A/B experiment\-related event tracking and triage functions are in effect; note that if the SDK turns off the experiment function locally (on the end), the experiment cannot be enabled even if the switch on the platform page is turned on. For details of the A/B experimental switch configuration at each end, please refer to the SDK access documentation at each end.

* Off: Indicates that the A/B experiment\-related event tracking and streaming functions are not effective.


<span id="_2-1-3-禁止上报事件名单"></span>
## List of prohibited incidents

This function is used to intercept useless event tracking reports. You can set the events in the "disabled" and "blacklist" states to prohibit reporting, or customize the event range, and the number of custom events is limited to 100.

<span id="_2-1-4-实时上报事件名单"></span>
## Real\-time event list reporting

This function is used to configure event tracking reports with high real\-time requirements. You can customize the event range, and the number of custom events is limited to 100.

Note: When the request volume is too large and the server level resources are tight, the real\-time event reporting may fail. At this time, the request will be downgraded to a normal event batch report.

<span id="_2-1-5-埋点上报时机"></span>
## Event tracking report timing

You can set the event tracking batch reporting timing to adjust the reporting frequency:

Method 1: According to the time interval, the minimum is 10 seconds, and the maximum is 300 seconds.

Method 2: According to the number of local cumulative logs, report to a specific number; minimum 50, maximum 10,000;

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Each end of the DataFinder has a default reporting mechanism and the timing of triggering reporting. After the console is configured here, the configuration result will prevail. See the default reporting mechanism <a href="https://docs.byteplus.com/docs/DataFinder/DataFinder_Data_Access_Overview">DataFinder Data Access Overview</a>.</div>


<span id="_2-1-6-关闭敏感字段采集"></span>
## Turn off sensitive field acquisition

This function is used to turn off the collection of sensitive fields for specific devices. See the page display for the fields that support closing. You can also turn off sensitive field collection on the terminal. For details of sensitive field switch configuration on each terminal, please refer to the SDK access documentation of each terminal.

<span id="5ebe50f3"></span>
## Estimated reporting time

This function is used to specify the approximate time interval for the SDK to send data to the server after the user triggers an event. This time interval can be adjusted based on factors such as network conditions, priorities, and performance to ensure the efficiency and accuracy of data reporting.

For example, for data with low materiality requirements, a longer reporting interval can be set to reduce the impact of client performance and network traffic consumption; for data with high performance requirements, a shorter reporting interval can be set so that the data can be sent to the server for processing as soon as possible.

<span id="46e6aacb"></span>
## Turn on monitoring and acquisition

This configuration item is used to control whether the collection of "monitoring events" is required.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e1f57186d1a4a42b16e70e4ec995370~tplv-goo7wpa0wc-image.image) </span>


* DataFinder adds support for collecting monitoring events ($finder_sdk_monitor). When using this function, you need to update the SDK version to the latest version at the same time.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Monitoring events ($finder_sdk_monitor) can be used to verify that SDK access and data reporting are normal.   </div>
   

* When collecting monitoring events, you can turn on the acquisition switch in the SDK of data access (turned off by default), or you can configure whether to collect monitoring events (not collected by default) through the SDK settings here. The result set here takes precedence over the configuration result on the access SDK side.


After turning on the switch, you can configure the details collected at each end.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c6316c43f5cb43d68d0bd85041dc1020~tplv-goo7wpa0wc-image.image) </span>

You can set the collection method of each end to:


* Turn on monitoring (covering the end side): Turn on monitoring event collection, and configure the application ID that needs to collect monitoring events. After the configuration is completed, monitoring events will be collected regardless of whether the SDK acquisition switch on the data access end side is turned on.

* Turn off the monitoring (cover the end side): Turn off the monitoring event collection. After the configuration is completed, no matter whether the SDK acquisition switch on the data access end side is turned on, the monitoring event will not be collected.

* The default is determined by the end side: after the configuration is completed, the acquisition switch configuration result of the SDK on the data access end side shall prevail to determine whether to collect monitoring events.
