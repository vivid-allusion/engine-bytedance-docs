---
title: "Client SDK integration"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Integrate_the_client_SDK"
---

The RUM feature of the APM console provides the following sub\-services: App Monitoring, WebPro Monitoring, PC Monitoring, Mini Monitoring, Mini Pro Monitoring, and OS Monitoring. This topic lists the SDK integration document for different monitoring services. Refer to the ones based on your business requirements.

<span id="ab9c392a"></span>
## App Monitoring

APMPlus provides comprehensive monitoring capabilities for mobile apps, including both native monitoring and hybrid monitoring.

Both iOS and Android platforms support the collection of multiple exception and crash types, as well as on\-site data restoration and analysis. In addition, they offer comprehensive performance analysis, enabling precise root cause tracing to help developers efficiently resolve exceptions.


|**Platform/Language** |**Main feature** |**Integrated SDK** |
|---|---|---|
|Android |Analysis of various metrics for the app, such as crashes, performance, and webview page. |[Integrating applications with the Android SDK](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_Android_SDK_into_the_application) |
|Harmony |Analysis of crashes for the app. |[Integrating applications with the Harmony SDK](https://docs.byteplus.com/en/docs/apmplus/Integrate_Harmony_SDK_into_applications) |
|iOS |Analysis of various metrics for the app, such as crashes, errors, and lags. |[Integrating applications with the iOS SDK](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_iOS_SDK_app) |


<span id="f298313e"></span>
## WebPro Monitoring

WebPro monitoring is a frontend monitoring product provided by APMPlus. It is applicable to browser pages and H5 pages within mobile apps. It monitors site performance, promptly detects exceptions, and helps track and analyze issues.

You can use the following two methods to integrate the WebPro Monitoring SDK: NPM package integration and CDN integration. CDN integration is recommended. For details, see [Web SDK integration](https://docs.byteplus.com/en/docs/apmplus/Integrate_WebPro_SDK).

The main differences between the two integration methods are as follows:


* Upgrade: For the SDK version upgrade, NPM integration requires manual version updates and redeployment, but CDN integration does not require manual updates and always fetches the latest SDK version.

* Monitoring timing: NPM packages are eventually bundled into business code. CDN integration directly inserts a script into the HTML. The script starts collecting exceptions in advance. Therefore, CDN integration can monitor exceptions earlier compared to NPM integration.


<span id="e28038c9"></span>
## Mini Pro Monitoring

Mini Pro Monitoring, provided by APMPlus, provides JS error analysis and page load performance analysis for TikTok Mini Program, WeChat Mini Program, Alipay Mini Program, Baidu Mini Program, and Feishu Mini Program. It helps you track and analyze issues.

Mini Pro Monitoring can be categorized into **native mini program integration** and **third\-party framework integration**. Refer to the corresponding document based on your business requirements.


* [Native mini program integration](https://docs.byteplus.com/en/docs/apmplus/Integrate_Mini_Program_Pro_SDK#.5Y6f55Sf5bCP56iL5bqP5o6l5YWl)

* [Third-party framework integration](https://docs.byteplus.com/en/docs/apmplus/Integrate_Mini_Program_Pro_SDK#.5LiJ5pa55qGG5p625o6l5YWl)


<span id="0da83ed3"></span>
## Mini Monitoring

It is applicable to products and services on the  platform. It supports native mini programs including WeChat Mini Program, TikTok Mini Program, Alipay Mini Program, and Baidu Mini Program, but do not support frameworks such as Taro and uni\-app.

For SDK integration documents, see [Mini Program SDK integration](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_mini_program_SDK).
