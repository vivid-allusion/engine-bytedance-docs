---
title: "How to prevent OOM issues in automated tasks"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/How_to_prevent_OOM_issues_in_automated_tasks"
---

In automated testing tasks, it is often necessary to actively exit in order to simulate certain scenarios and achieve the testing objectives. 

However, in real\-world scenarios, APMPlus cannot fully adapt to certain automated scenarios. One reason is that there are many different automation frameworks, and another reason is that some customers have developed their own automation frameworks. During automated testing, the SDK is unable to detect exits in certain scenarios and can only attribute these exits to OOM issues, resulting in false positives. Therefore, we have exposed several interfaces for customers to indicate whether the system is in an automation scenario. Once this flag is set, no OOM data will be reported during automated testing.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">APMPlus supports the feature described in this document starting from version 5.1.1.</div>



```objectivec
#import <RangersAPM+OOMCrashConfig.h>

/**
Declare that the program is running in an automated test. If isAutoTest is passed as YES, all Out of Memory (OOM) issues will be masked. The default value is NO.
 
Note:
 
Do not call this function in the production environment, otherwise, OOM data will not be reported.
Call this function before initializing APM, that is, before executing the +[RangersAPM startWithConfig:] function.
 
 Declare that the program is running in automated testing. If isAutoTest is passed as YES, all OOM problems will be blocked. Default is NO.
 Notice: 
    1. Please do not call this function in a production environment, otherwise OOM data will not be reported.
    2. Call this function before initializing APM, that is, before the +[RangersAPM startWithConfig:] function executes.
 */
[RangersAPM OOMCrashMarkAutoTest:YES];
```
