---
title: "Can the Android SDK work without support?"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Can_the_Android_SDK_work_without_support"
---

Yes.

When integrating Application Performance Monitoring Full Link Edition, add the following code to the dependencies section of the app module's `build.gradle` file to avoid depending on support.

```Java
implementation('com.volcengine:apm_insight:1.5.9.cn') {
    exclude group:'com.android.support'
}
```
