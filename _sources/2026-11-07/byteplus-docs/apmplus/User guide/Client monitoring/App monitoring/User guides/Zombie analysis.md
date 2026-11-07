---
title: "Zombie analysis"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Zombie_analysis"
---

Zombie is a zombie object, which is an object that has already been released but is reused, resulting in wild pointer problems.

Wild pointer issues in common scenarios can be quickly exposed and resolved during development with the help of Xcode tools. However, some problems are missed in production because they are triggered by more complex scenarios and are difficult to reproduce offline. For crashes caused by these wild pointers, it is difficult to effectively troubleshoot the problem based solely on the stack trace at the time of the crash. To address this pain point, Application Performance Management Plus provides developers with an online Zombie detection feature.

<span id="a29928ac"></span>
## Precautions


* The Zombie module can expose wild pointer issues in online environments and capture the classes and stack trace that lead to wild pointers.

* Wild pointers do not necessarily cause crashes. However, after this module is integrated, it will actively throw an exception when a wild pointer is accessed, which may increase your application's crash rate. It is recommended to enable this module for a limited number of users during a gradual rollout.

    &nbsp;


<span id=".5q2l6aqk5LiA77ya5Yik5pat5bqU55So5piv5ZCm5a2Y5Zyo6YeO5oyH6ZKI"></span>
## Step 1: Determine whether the application contains any wild pointers

Use **crash details** in the filter options to quickly locate issues.

The crash call stack consists of Objective\-C Runtime methods, for example, objc_msgSend, objc_retain, objc_release, and many others.

In certain cases, memory that has already been released may be reallocated by the Operating System, causing the objects in memory to not be the objects you expect and triggering a doesNotRecognizeSelector exception.

<span id="03728fd0"></span>
## Step 2: Integrate the SDK

The dangling pointer issue cannot be resolved with the existing information. You can introduce the Zombie module into the SDK and configure the sampling rate for zombie objects. Use the online Zombie analysis feature to obtain more on\-site information and resolve the wild pointer issue.


* Integrate the Zombie module. For details, refer to [Integrate the iOS SDK into your application](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_iOS_SDK_app).

* Configure zombie object sampling rate For details, refer to [the SDK setting](https://docs.byteplus.com/en/docs/apmplus/SDK_reporting_configuration).

   Description of zombie\-related metrics:

   
   |Metric |DescriptionS |
   |---|---|
   |Zombie object sampling rate |Configuring this option allows you to turn on the feature only for a subset of online users. The default sampling rate is 0. |
   |Allowlist for collecting zombie objects |After configuring this option, exceptions will be thrown and context information captured only if a wild pointer issue occurs in the classes specified in the configuration. If this option is not configured, any class that encounters a wild pointer issue will trigger the zombie collection policy. |
   |The allowlist for zombie object analysis |When analyzing dangling pointer issues, you may need to know how objects are released. After configuring this option, when objects of classes specified in the configuration are released, their deallocation stack traces will be saved. If a wild pointer issue occurs later, the deallocation stack trace will be reported together with the crash, and you can view this information in the crash details page under **crash information \> Dealloc stack trace**.<br><br>Capturing stack traces has an impact on performance. It is recommended that you do not configure this option initially. If a wild pointer issue is found in the production environment and the root cause cannot be identified, you can enable this configuration option to obtain more information. |
   |The maximum number of dealloc stack traces |Controls the maximum number of object release stack traces that the SDK can store. Increasing this number allows more stack traces to be cached, helping to avoid situations where, when a wild pointer occurs, the cache does not contain the release stack trace for the object. Decreasing the number reduces the impact on memory usage. |
   


<span id=".5pWw5o2u5raI6LS5"></span>
## Step 3: Consume data

You can consume the data reported by online zombie analysis in crash analytic.


1. Based on the stack trace characteristics from Zombie analysis, locate the crash stack trace reported by Zombie analysis.

   1. zombie analyzes the reported crash stack trace, and there is a call stack line for **zombieMsgHandle** in the stack trace.

   2. View crash information to identify which class's object encountered a wild pointer.

2. The stack trace cannot locate the issue. You can configure the allowlist for zombie object analysis and add the classes that trigger wild pointer issues to the allowlist.

3. Based on the reported Dealloc stack trace, view the time when the object was released.

4. Locate the business code.
