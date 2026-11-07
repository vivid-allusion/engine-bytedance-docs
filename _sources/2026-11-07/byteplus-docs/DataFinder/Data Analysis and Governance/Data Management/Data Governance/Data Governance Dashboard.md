---
title: "Data Governance Dashboard"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Data_Governance_Dashboard"
---

<span id="_1-概述"></span>
# 1. Overview

The data governance dashboard can automatically detect the event tracking data quality and event tracking usage of the current project, assist data managers to determine whether the event tracking data is healthy, and take further governance actions, including repairing event tracking abnormalities and cleaning up useless event tracking.

<span id="_2-功能说明"></span>
# 2. Function description

<span id="_2-1-入库校验监控"></span>
## 2.1 Warehousing verification monitoring

After receiving the data reported by the SDK, the growth analysis product will verify the data content, and the data that passes the verification will be built into the data table. The wrong data will be intercepted and discarded. The specific processing methods are:


* If an exception in the event name of the piece of data is detected, the piece of data will be discarded and will not be put into storage.

* If the event name passes the test and some of its properties (params) detect an exception, then the exception's properties are discarded, and the event and the rest of the normal properties are still available for storage.


<span id="_2-1-1-事件拦截率"></span>
### 2.1.1 Event block rate

The event block rate indicator is used to monitor the proportion of event data in the current project that is intercepted and cannot be put into storage due to abnormal format or reporting delay. The higher the block rate, the higher the event error, and the greater the data loss.

Event block rate = event error block number/received total number

The number of interceptions is only calculated for metadata that is enabled and enabled without displaying the state. Events with disabled, acceptance pending, and blacklist states are expected to be normally intercepted events and are not within the scope of statistics.

<span id="_2-1-2-数据错误及校验规则"></span>
### 2.1.2 Data Errors and Validation Rules

Data Error Rate = Number of event anomalies detected/Total number received at server level


* Event errors can cause the entire event to be intercepted. Event exceptions include the following:

   
   |**Error code** |**Error description** |**Validation rule** |**Optimization suggestions** |
   |---|---|---|---|
   |1010001 |Event name is invalid |`^[a-zA-Z0-9][a-z0-9A-Z_ .-]{1,255}$` |Event names begin with a letter (uppercase or lowercase) or a number and can contain letters, numbers, _. \-, the length must not exceed 255 characters, please modify the name. |
   |1010002 |Event names conflict with system reserved event name rules |Not a preset event name that starts with $and __. |Conflict with the system reserved event name rules, event names must not start with $or __, please start with a letter, can contain letters, numbers, _. \-, the length must not exceed 255 characters, please modify the name. |
   |1010003 |Event name conflicts with virtual event name |Same name as the created virtual event. |The event name must not have the same name as the virtual event. Please modify the name. |
   |1010004 |number of events exceeded |* If there are more than 1000 events in a single application, the event falls metadata status = \-2, the slotting tag is closed, the event is not built, and the properties are not dropped from the library.<br><br>* Privatization can be configured up to a maximum of 5000. |The number of events has reached the upper limit, and new events cannot be added. Please go to the meta\-event list page and "disable" useless events. |
   |1010005 |event build disabled |This event is disabled in metadata management. |Check the "disabled" state setting for this event in the metadata. |
   |1010006 |The time of the warehousing event exceeds the valid window period |The event occurred outside the last 7 days and the next hour. |Event tracking occurs earlier than the past 7 days, and event reporting is delayed. It is recommended to check the network link situation on the client side, or increase the reporting frequency (need to modify the SDK configuration). |
   |1010007 |Event metadata not accepted or blacklisted |Events not registered/accepted or marked as blacklisted |If you need the event to be warehoused, please change the event status to "enabled" or "hidden". |
   |1010008 |Event metadata does not exist |Event metadata does not exist |After opening the strong verification, the first report will prompt that the metadata does not exist, and it can be warehoused normally after acceptance. |
   

* When only a property exception is detected, it will not affect the warehousing of the event, but the abnormal property will be intercepted and not warehoused. Property exceptions include the following:

   
   |**Error code** |**Error description** |**Validation rule** |**Optimization suggestions** |
   |---|---|---|---|
   |1020001 |Invalid event property name |`^[a-zA-Z0-9][a-z0-9A-Z_ .-]{1,64}$` |Property names begin with a letter (uppercase or lowercase) or a number and can contain letters, numbers, _. \-, the length must not exceed 64 characters, please modify the name. |
   |1020002 |Event property names conflict with system reservation rules |Not a preset event name that starts with $and __. There are whitelists ($inactive, $inline, $target_uuid_list, $source_uuid, $is_spider, $source_id, $is_first_time). |The event property name conflicts with the system reservation rules. The name must not start with $and __. Please modify the name. |
   |1020003 |The number of properties per event exceeds the limit |A single event suggests 300 properties, more than 300 but not more than 500, the status is set to 0, which means that the build is disabled, but it can be displayed on the page; more than 500 states are set to \-2, which means hidden and not built. |The number of single event properties has reached the upper limit of 300, and the excess part cannot be warehoused. Please go to the metadata\-event property list page to disable the useless event property. |
   |1020004 |Invalid event property data type |Inconsistent with the property data type recorded in metadata, and strong conversion failed. |The actual reported data format is inconsistent with the property data type recorded in the metadata, and the strong transfer fails; please adjust the report according to the registration type, or modify the registered data type. |
   |1020005 |Invalid event property value |* SaaS\-Cloud Native: Over 2048 characters |If the property value exceeds 2048/1024 characters, the excess part will be truncated and cannot be put into storage. It is recommended to adjust the reported value. |
   |1020006 |Event property not accepted or in blacklist |Event properties Event not registered/not accepted or marked as blacklisted |If you need this property to be warehoused normally, please change the property status to "enabled" or "hidden". |
   |1020007 |Event property metadata does not exist |Event property metadata does not exist |After opening the strong verification, the first report will prompt that the metadata does not exist, and it can be warehoused normally after acceptance. |
   |1020008 |event property disabled |Event properties are disabled. |Check the "disabled" setting for the event property. |
   |1030001 |Event public property name is invalid |`^[a-zA-Z0-9][a-z0-9A-Z_ .-]{1,64}$` |Property names begin with a letter (uppercase or lowercase) or a number and can contain letters, numbers, _. \-, the length must not exceed 64 characters, please modify the name. |
   |1030002 |Event public property names conflict with system reservation rules |Not a preset event name that starts with $and __. There are whitelists ($inactive, $inline, $target_uuid_list, $source_uuid, $is_spider, $source_id, $is_first_time). |The event public property name conflicts with the system reservation rules. Property names must not start with $and __. Please modify the name. |
   |1030003 |The number of common properties of a single application event exceeds the limit |More than 100 event public properties with status set to \-2 do not participate in the build. |The number of event public properties has reached 100, and the excess part cannot be warehoused. Please go to the metadata\-event property list page to disable the useless event public properties. |
   |1030004 |Invalid event public property data type |Inconsistent with the property data type recorded in metadata, and strong conversion failed. |The actual reported data format is inconsistent with the property data type recorded in the metadata, and the strong transfer fails; please adjust the report according to the registration type, or modify the registered data type. |
   |1030005 |Invalid event public property value |* SaaS\-Cloud Native: Over 2048 characters |If the property value exceeds 2048/1024 characters, the excess part will be truncated and cannot be put into storage. It is recommended to adjust the reported value. |
   |1030006 |Event public property not accepted or blacklisted |Event public property not accepted or blacklisted |If you need this property to be warehoused normally, please change the property status to "enabled" or "hidden". |
   |1030007 |Event public property metadata does not exist |Event public property metadata does not exist |After opening the strong verification, the first report will prompt that the metadata does not exist, and it can be warehoused normally after acceptance. |
   |1030008 |Event public property disabled |Event public properties are disabled. |Check the "disabled" setting for the event public property. |
   |1040001 |Invalid user property name |`^[a-zA-Z0-9][a-z0-9A-Z_ .-]{1,64}$` |Property names begin with a letter (uppercase or lowercase) or a number and can contain letters, numbers, _. \-, the length must not exceed 64 characters, please modify the name. |
   |1040002 |The number of user properties exceeds the limit |The number of user properties exceeds the 300 limit. |The number of user properties has reached the upper limit, and new properties cannot be added. Please go to the user properties list page and "disable" useless properties. |
   |1040003 |Invalid user property type |Inconsistent with the property data type recorded in metadata, and strong conversion failed. |The actual reported data format is inconsistent with the property data type recorded in the metadata, and the strong transfer fails; please adjust the report according to the registration type, or modify the registered data type. |
   |1040004 |Invalid user property value |* SaaS\-Cloud Native: Over 2048 characters |If the property value exceeds 2048/1024 characters, the excess part will be truncated and cannot be put into storage. It is recommended to adjust the reported value. |
   |1040005 |User properties not accepted or in the blacklist |User properties not accepted or in the blacklist |If you need this property to be warehoused normally, please change the property status to "enabled" or "hidden". |
   |1040007 |User property metadata does not exist |User property metadata does not exist |After opening the strong verification, the first report will prompt that the metadata does not exist, and it can be warehoused normally after acceptance. |
   |1000001 |User information is illegal |user_unique_id_type incoming error |Checks whether more than user_unique_id_type key has been passed in, or checks whether the corresponding value setting is correct. |
   


You can click the blue number to view the detailed reporting log and further investigate the problem.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1188a53385f14c4f995f2c6d770be125~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-1-3-上报延迟"></span>
### Delay in reporting 2.1.3

Growth analysis discards data that has not been reported for more than 7 days without warehousing. For example, if a user behavior occurs on January 1, then it can only be warehoused if the behavior is reported before January 8. After January 8, it cannot be warehoused even if it is reported.

Latency rate = number of warehousing events that occurred beyond the valid window (error type 1010006)/total number received by the server level

If you detect a high rate of delay in reporting a project, it is recommended that you pay attention to the type and version of the SDK and adjust the timing of reporting, such as shortening the reporting interval. It is also recommended that you pay more attention to the networking of user devices.

You can click the blue number to view the detailed reporting log and further investigate the problem.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2720983b82e05138383dbc0410c50610.png) </span>

<span id="_2-2-元数据使用情况"></span>
## 2.2 Usage of metadata

Before launching event tracking governance work, it is first necessary to understand the current construction and usage of event tracking.

<span id="_2-2-1-埋点管理模式"></span>
### 2.2.1 Event tracking management mode

During use, unknown data, incorrectly named events or properties, and incorrect data types often enter the system, only to be discovered when the data is used for analysis. At this point, often the wrong data has affected data analytics, and the cause of the problem is difficult to locate, resulting in a large waste of time. After data acceptance is turned on, data needs to be manually reviewed before entering the system, and released after confirming that the name and property type are correct, so that the data entering the system has correct rules, thereby reducing the abnormalities caused by abnormal data when data is used.

Growth analysis provides you with event tracking warehousing verification mode management mode. You can choose whether to turn it on according to the actual event tracking management requirements, and the default is closed.


* Enable event tracking warehousing verification mode: Events and properties that appear in metadata for the first time need to be manually accepted in data management before warehousing. Data that has not been registered or accepted in advance will not be accepted for warehousing. The effective time after opening is about 10 minutes.

* Turn off event tracking warehousing verification mode: After closing, events and properties will be automatically warehoused, no advance registration or manual acceptance is required, and warehousing will only be blocked when the event/property is marked as "disabled".


You can click "Go to Modify" or open the " **Project Center \> Project Management \> General Settings** " page to configure the switch.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/65be344d400945f6b27c088d2e413041~tplv-goo7wpa0wc-image.image) </span>

The metadata state flow diagram is as follows:

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI1MTVweCIgaGVpZ2h0PSI0OTVweCIgdmlld0JveD0iLTAuNSAtMC41IDUxNSA0OTUiPjxkZWZzLz48Zz48cGF0aCBkPSJNIDIxMiA2MiBMIDIxMiAxNTUuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyMTIgMTYwLjg4IEwgMjA4LjUgMTUzLjg4IEwgMjEyIDE1NS42MyBMIDIxNS41IDE1My44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gMjcyIDMyIEwgMzg1LjYzIDMyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMzkwLjg4IDMyIEwgMzgzLjg4IDM1LjUgTCAzODUuNjMgMzIgTCAzODMuODggMjguNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjE1MiIgeT0iMiIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZTU5OSIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzJweDsgbWFyZ2luLWxlZnQ6IDE1M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE0cHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5QZW5kaW5nIEFwcHJvdmFsPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDM5MiAzMiBMIDI3OC4zNyAzMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDI3My4xMiAzMiBMIDI4MC4xMiAyOC41IEwgMjc4LjM3IDMyIEwgMjgwLjEyIDM1LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIzOTIiIHk9IjIiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmU1OTkiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMycHg7IG1hcmdpbi1sZWZ0OiAzOTNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxNHB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+QmxhY2tsaXN0PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDM5MiAxOTIgTCAyNzguMzcgMTkyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMjczLjEyIDE5MiBMIDI4MC4xMiAxODguNSBMIDI3OC4zNyAxOTIgTCAyODAuMTIgMTk1LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIzOTIiIHk9IjE2MiIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZTU5OSIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTkycHg7IG1hcmdpbi1sZWZ0OiAzOTNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxNHB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+SGlkZTwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAyMTIgMjIyIEwgMjEyIDMxNS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDIxMiAzMjAuODggTCAyMDguNSAzMTMuODggTCAyMTIgMzE1LjYzIEwgMjE1LjUgMzEzLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSAyNzIgMTkyIEwgMzg1LjYzIDE5MiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDM5MC44OCAxOTIgTCAzODMuODggMTk1LjUgTCAzODUuNjMgMTkyIEwgMzgzLjg4IDE4OC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMTUyIiB5PSIxNjIiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDE5MnB4OyBtYXJnaW4tbGVmdDogMTUzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTRweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlN0YXJ0PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDIxMiAzMjIgTCAyMTIgMjI4LjM3IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMjEyIDIyMy4xMiBMIDIxNS41IDIzMC4xMiBMIDIxMiAyMjguMzcgTCAyMDguNSAyMzAuMTIgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIxNTIiIHk9IjMyMiIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzUycHg7IG1hcmdpbi1sZWZ0OiAxNTNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxNHB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+RGlzYWJsZTwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMTUyIiB5PSI0MjIiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDQ1MnB4OyBtYXJnaW4tbGVmdDogMTUzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTRweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPmV4Y2VlZCB0aGUgbGltaXQ8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMjIgMzIgTCAxNDUuNjMgMzIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAxNTAuODggMzIgTCAxNDMuODggMzUuNSBMIDE0NS42MyAzMiBMIDE0My44OCAyOC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGVsbGlwc2UgY3g9IjEyIiBjeT0iMzIiIHJ4PSIxMCIgcnk9IjEwIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDIyIDE5MiBMIDE0NS42MyAxOTIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAxNTAuODggMTkyIEwgMTQzLjg4IDE5NS41IEwgMTQ1LjYzIDE5MiBMIDE0My44OCAxODguNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxlbGxpcHNlIGN4PSIxMiIgY3k9IjE5MiIgcng9IjEwIiByeT0iMTAiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gMjIgNDUyIEwgMTQ1LjYzIDQ1MiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDE1MC44OCA0NTIgTCAxNDMuODggNDU1LjUgTCAxNDUuNjMgNDUyIEwgMTQzLjg4IDQ0OC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGVsbGlwc2UgY3g9IjEyIiBjeT0iNDUyIiByeD0iMTAiIHJ5PSIxMCIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMzIiIHk9IjEyIiB3aWR0aD0iMTAwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiA5OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDIycHg7IG1hcmdpbi1sZWZ0OiAzM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE0cHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5EYXRhIHJlcG9ydGluZzwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMzIiIHk9IjE3MiIgd2lkdGg9IjEwMCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogOThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxODJweDsgbWFyZ2luLWxlZnQ6IDMzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTRweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkRhdGEgcmVwb3J0aW5nPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIzMiIgeT0iNDMyIiB3aWR0aD0iMTAwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiA5OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDQ0MnB4OyBtYXJnaW4tbGVmdDogMzNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxNHB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+RGF0YSByZXBvcnRpbmc8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjMyIiB5PSI0MiIgd2lkdGg9IjEwMCIgaGVpZ2h0PSIzMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogOThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA1N3B4OyBtYXJnaW4tbGVmdDogMzNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxNHB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgZm9udC13ZWlnaHQ6IGJvbGQ7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkVuYWJsZSBzdHJvbmcgdmVyaWZpY2F0aW9uPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIzMiIgeT0iMjAyIiB3aWR0aD0iMTAwIiBoZWlnaHQ9IjMwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiA5OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDIxN3B4OyBtYXJnaW4tbGVmdDogMzNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxNHB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgZm9udC13ZWlnaHQ6IGJvbGQ7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkRpc2FibGUgc3Ryb25nIHZlcmlmaWNhdGlvbjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMzIiIHk9IjQ2MiIgd2lkdGg9IjEwMCIgaGVpZ2h0PSIzMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogOThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA0NzdweDsgbWFyZ2luLWxlZnQ6IDMzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTRweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGZvbnQtd2VpZ2h0OiBib2xkOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5EaXNhYmxlIHN0cm9uZyB2ZXJpZmljYXRpb248L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjIxMiIgeT0iOTIiIHdpZHRoPSIxMDAiIGhlaWdodD0iMzAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDk4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTA3cHg7IG1hcmdpbi1sZWZ0OiAyMTNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxNHB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+QWNjZXB0YW5jZSBhcHByb3ZlZDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMjgyIiB5PSIyIiB3aWR0aD0iMTAwIiBoZWlnaHQ9IjMwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiA5OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDE3cHg7IG1hcmdpbi1sZWZ0OiAyODNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxNHB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+QWRkIHRvIGJsYWNrbGlzdDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMjgyIiB5PSIzMiIgd2lkdGg9IjEwMCIgaGVpZ2h0PSIzMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogOThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA0N3B4OyBtYXJnaW4tbGVmdDogMjgzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTRweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlJlbW92ZSBmcm9tIGJsYWNrbGlzdDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PC9nPjwvc3ZnPg==" />


* Acceptance pending: After turning on "Data warehousing verification", unknown meta events and properties in the system will enter the acceptance pending list. Only after manual acceptance will the relevant data be allowed to enter the system. The name and property data types determined during acceptance are used as validation rules for the corresponding metadata. When "data warehousing verification" is not enabled, unknown meta events and properties in the system will be directly added to metadata.

* Blacklist: Meta events or properties in the blacklist never enter the system, but when removed from the blacklist, they appear in the acceptance pending list as new unknown events.


Metadata availability comparison table for different states:


| |**Status** |**Data Management Display** |**Whether to occupy metadata quota** |**Whether to build storage** |**Is it available in the product?**  |
|---|---|---|---|---|---|
|Over limit |\-2 |No |No |No |No |
|Disable |0 |Yes |No |No |No |
|Enable |1 |Yes |Yes |Yes |Yes |
|Hide |2 |Yes |Yes |Yes |No |
|Acceptance pending |3 |No |No |No |No |
|Blacklist |4 |No |No |No |No |


<span id="_2-2-2-元数据使用情况"></span>
### 2.2.2 MSetadata usage

You can **Data Management \> Data Governance \> Data Governance Dashboard \> Metadata Usage** module to view the current project metadata creation quantity and usage statistics, including: the number of queries in the last 30 days, the number of queries in the last 30 days, the number of associated charts (only events are supported, not properties), and the number of warehouses yesterday (only events are supported, not properties).

In order to facilitate the use of project members and reduce unnecessary redundant information and data, it is recommended that data administrators promptly disable invalid events/properties in the project, such as events/properties that are not queried or have not been reported for a long time.

You can also click on the event name/property name to view the details, and the operation diagram:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b506f694f6b4c24beff56780493a01b~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-导出全量埋点方案"></span>
## 2.3 Export full event tracking scheme

You can click the "Export event tracking scheme" button in the upper right corner of the page to get the complete event tracking scheme document (excel format) of the current project, including custom events/properties, preset events/properties, and user properties.

Operation diagram:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d9ae8a0007a43fab41fb1f8be1b8e9f~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-常见问题"></span>
# 3. Frequently Asked Questions

<span id="_3-1-哪些人需要关注数据治理看板？"></span>
## 3.1 Who needs to pay attention to the data governance dashboard?

We recommend that the "data administrator" or "event tracking leader" regularly check the data governance dashboard, which can help you detect abnormalities in the event tracking data in a timely manner and correct the data as soon as possible to avoid losses.

<span id="_3-2-哪些项目需要开启埋点入库校验？"></span>
## 3.2 Which items need to enable event tracking and warehousing verification?

Enabling warehousing verification can ensure that all event tracking is manually reviewed, which can provide maximum convenience and data accuracy when querying event tracking. Therefore, if your project has the role of "event tracking leader", it is recommended that you turn on the warehousing verification switch.

If your team is currently unable to assign the role of "event tracking leader", in order to avoid data interception loss caused by long\-term unacceptance/registration of event tracking information, it is recommended that you turn off the warehousing verification switch.

<span id="_3-3-开启埋点入库强校验一段时间又关闭了，期间未验收的数据会自动验收么？"></span>
## **3.3 Turn on event tracking and put into storage. The strong verification has been closed for a period of time. Will the unaccepted data be automatically accepted during the period?** 

No. Meta events or properties that enter the acceptance pending list remain in the acceptance pending list until they are manually accepted by the user, and the relevant data does not enter the system.

<span id="_3-4-元事件数量超限了怎么办？"></span>
## **What should I do if the number of events of 3.4 yuan exceeds the limit?** 

At present, you can contact customer service or customers to successfully delete some metadata that is no longer in use to reduce the number of metadata. At the same time, it is recommended to adjust the naming method of meta events in the event tracking scheme. Usually, the frequently changing part of the metadata name can be reported as the property of the event.

<span id="_3-5-开启了数据校验，为什么部分数据查不到了？"></span>
## **3.5 Data verification is turned on, why can't some data be found?** 

After enabling event tracking warehousing verification, only the data reported after acceptance will be warehoused, and the unaccepted data will not be warehoused.

<span id="b6254c0f"></span>
## 3.6 Data verification is turned on, and properties are entered in the metadata. Why can't property data be reported to the warehouse normally?

If you have enabled event tracking warehousing verification, you have also entered properties in advance in the metadata, but after the property data is reported, you do not see the reported data normally on the corresponding property data page. It may be because the reported properties are inconsistent with the types of properties entered in the metadata.


* The event\-related properties of DataFinder are divided into event public properties and event properties. After enabling the event tracking warehousing check, make sure that the property type of the property when reporting is the same as the property type defined at the time of metadata entry, otherwise the reported property data will be intercepted.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When event tracking is not enabled, if the property types are inconsistent, the property data can be reported normally, but this reporting method is not recommended. It is strongly recommended that you report data with the same property types as those defined in metadata.   </div>
   

* You can view the type of property you entered in metadata and the type of property you set when reporting data in the following ways.

   * Check the type of property entered in metadata:

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/104a285b80654dc4a3a9937ba6096279~tplv-goo7wpa0wc-image.image) </span>

      You can check the property type field of the corresponding property on the event properties page to confirm whether the property is "event public property" or "event property".

   * The type of property set when reporting data:

      You can view the data access SDK code to see the reporting location of the corresponding property. Usually:

      * When a property is reported in header.custom, the property type is "Event public property".

      * When a property is reported together with a specific event in the corresponding event, the property type is "Event Property".

         Each end of the event public properties, event properties reported location description can view the corresponding end of the SDK integration document, for example, iOS end, you can view [iOS SDK Integration](https://docs.byteplus.com/docs/DataFinder/iOS_SDK_Integration).
