---
title: "Cannot see the reported crash events"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Cannot_see_the_reported_crash_events"
---

1. Please first confirm that the initialization configuration is correct, especially the AppID field, which must be set to the ID of the application you have created on APMInsight.

2. Confirm whether your trigger method is correct. The correct trigger method is as follows:

   * Add a crash simulation event in your code

   * Use Xcode to compile and install your app on a simulator or a physical device

   * Open the app in an emulator or on a physical device, and trigger a simulated crash event.

   * Simply reopening the app will trigger crash event reporting.

      There are a few points to note:

   * You cannot use Xcode Run to start the app to trigger a crash event. When the app crashes, Xcode will terminate execution, so the SDK cannot record the crash event.

   * Crash events must be triggered after the SDK has been initialized. If the crash is triggered automatically, it is recommended to introduce a delay before triggering the event. This helps prevent a situation where, after restarting the app, a new crash occurs before the previous crash event has been reported.

3. After confirming that the above process is correct, you can perform local packet capture and filter for [tbm.snssdk.com](http://tbm.snssdk.com/)/monitor/collect/c/crash. If you capture traffic to this endpoint, it indicates that the crash has been reported.
