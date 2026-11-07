---
title: "App Crash Analysis"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/App-Crash-Analysis"
---

<span id="一-概览"></span>
# 1. Overview

**What is crash analysis?** 


* Crash analysis service provides mobile apps with the ability of "collecting\-analyzing\-monitoring\-alarming" of real\-time online stability related data, iOS supports the detection and analysis of OOM crashes, stuck and other issues, Android supports the monitoring and analysis of Java crashes, Java startup crashes, Native crashes, ANR and other issues.

* The crash analysis service associated with "A/B Testing" supports Android/iOS application types to help customers establish 5\-minute online fault perception capabilities. In the future, it will be further used in conjunction with performance analysis/remote logging services to build a closed loop of abnormal "perception\-location\-recovery" operation and maintenance capabilities to improve the app experience.


**The current "programming experiment, push experiment" of "A/B testing" supports access to crash analysis capabilities, because only the APP (mobile end) can get app_crash events.** 

<span id="二-创建指标"></span>
# 2. Create metrics

<span id="_1-系统预置指标"></span>
## 1. System preset metrics

By default, the following metrics are used as the metrics preset by the system, as follows:


|Serial number |**Metric name** |Metric description |**Metric type** |Set metrics |Is it a must\-see metric? |
|---|---|---|---|---|---|
|1 |Number of crashes |Number of crashes in all launched devices (PV) |Single metric |app_crash: total number of times |No |
|2 |Crash rate |Number of crashes in all launched devices/total number of launches |Combined metrics |A: app_crash: Total number of group entries<br><br>B: app_launch: Total number of group entries<br><br>A/B |No |
|3 |The number of users affected by crash |The number of users who experienced crashes on all launch devices(UV) |Single metric |app_crash: Total headcount |No |
|4 |Crashes affect user percentage |The number of users who experienced crashes on all launch devices/Total number of users who launched |Combined metrics |A: app_crash: total number of people<br><br>B: app_launch: total number of people<br><br>A/B |No |


Monitor alarming:


* The metric preset by the system has turned on the monitoring alarm by default, and you can turn off and modify the alarm rules;

* Alarm rules: compared with control group \> 50%; not check the "Trigger Alert for a significant change".


<span id="_2-如何使用崩溃指标"></span>
## 2. How to use crash metrics

Crash metrics need to be used, Application Performance Monitor Full Link Edition needs to be connected, and the relevant contract configuration needs to be completed by the Customer Manager before it can be used.

For access details, see [Application Performance Monitor Full Link Edition, Access Documentation](https://www.volcengine.com/docs/6431/68850).

<span id="三-实验报告"></span>
# 3. Experimental report

If your application is plugged into the Application Performance Monitor full\-link product and you add a crash metric when creating an experiment, you can see the data for that metric on the Experiment Reports page. As shown below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/51f4668ccb4842d186067c8b8c4ae784~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/739a2b13fdfe46d0a6a2c21fcc90a093~tplv-goo7wpa0wc-image.image) </span>
