---
title: "SDK General FAQ"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/SDK_General_FAQ"
---

<span id="6ad7dd1e"></span>
# **What is the difference between full event tracking and preset event tracking?** 


* Preset events (active reporting) are used to preset analytical models, such as app_launch, any_event, app_terminate, abtest_exposure;

* Full event tracking event (controlled by the full event tracking switch, turn on the switch to actively upload, do not turn on the switch to upload) For example, bav2b_page full event tracking page access, bav2b_click full event tracking element click;

* Custom event (design event tracking scheme according to business needs and then develop code event tracking).


<span id="如果sdk不初始化，会不会发网络请求？"></span>
# If the SDK is not initialized, will a network request be made?

No network requests are made without initializing the SDK.

<span id="app-launch和app-terminate事件的采集时机"></span>
# Timing of collection of app_launch and app_terminate events

app_launch: When the user launches the APP or enters the foreground, a Launch event will be generated inside the SDK.

app_terminate: iOS is when the user cuts the background (including the lock screen), immediately counts as the end of the session, will generate a Terminate event; while Android is when the user stays in the background for 30s (including the lock screen), and then opens the next time to listen to more than 30s will generate terminate.

<span id="sdk初始化之后，会取哪些敏感信息，比如用户信息这些？"></span>
# After the SDK is initialized, what sensitive information will be retrieved, such as user information?

The SDK has two versions: cn (domestic) and global (overseas), both of which meet the compliance requirements at home and abroad. If you want to know the specific user information, please refer to .

<span id="如果私有化部署之后，sdk还会向字节服务器发送什么信息吗？"></span>
# What other information does the SDK send to the byte server after private deployment?

Private deployment, the SDK does not send information to the byte server.

<span id="客户端sdk的分流缓存策略"></span>
# Shunt caching strategy for client side SDK

Client side: The client side SDK will request the shunt service (http service) when it is initialized, and then request the shunt service every 10 minutes (abtest_fetch_interval), get the shunt result (that is, the experiment hit by the user and the version of the shunt), and cache it locally in the SDK. When a customer calls the API in the SDK to retrieve a streaming result, it essentially reads the result directly from the cache without an HTTP request.

Server level: The server level SDK will request the meta service (mysql\-based http service) during initialization, and then request the meta service every once in a while (the interval can be set through the SDK's API, the default is 60 seconds update) to obtain the meta information of the experiment (non\-shunt results) and cache it. When a customer calls the API in the SDK to get the shunt result, essentially the SDK uses the experimental meta information to shunt locally, and no http request occurs.

<span id="如何获取客户端sdk离线包？"></span>
# How to get client side SDK offline package?

You can refer to the SDK link in the manual integration section of the official help documentation.

<span id="实验曝光事件-abtest-exposure-可以关闭吗？"></span>
# Can the experimental exposure event be closed abtest_exposure?

Event collection can be closed, but after closing the AB system will not have the corresponding data, so the experiment and Feature in the running state, and want to see the experimental report data, it is not recommended to close abtest_exposure event collection.

<span id="客户端分流结果刷新时间间隔是多久？可以自定义时间间隔拉取分流结果吗？"></span>
# What is the refresh interval for client side offload results? Can I customize the time interval to pull shunt results?

The shunt results are rerequested every 10 minutes (600s), but the latest shunt results can be pulled through the pullAbTestConfigs method provided by the client side.

<span id="上报事件后多久可以在系统看到数据？"></span>
# How soon can I see data in the system after reporting an incident?

After reporting an event, the corresponding data can be seen in the system in 5 to 10 minutes under normal circumstances, because the data needs to go through relevant steps such as collection, processing, construction, and warehousing.

<span id="客户端sdk数据上报策略"></span>
# Client side SDK data reporting strategy

The client side SDK is reported in batches, and the specific strategies are as follows:


* Report every 60s.

* Switch users and report immediately.

* Profile request, report immediately.

* Calling flush triggers an immediate call.


<span id="客户端sdk分流时机"></span>
# Client side SDK offload timing


1. Initialization will perform shunt, generally cold start will be initialized.

2. The shunt service is rerequested every 10 minutes.

3. The shunt successfully gets the experimental result. If it is not available locally, it will exist locally. If it is already available locally, overwrite the previously stored one. Get the experimental parameters (call getabconfig). If you hit the experiment, you will get the corresponding version value. If not, it is the default value.


<span id="客户端sdk如何实时获取分流结果？"></span>
# How does the client side SDK get streaming results in real time?

The client side SDK provides a real\-time API for obtaining shunt results: pullAbTestConfigs (), which can also be executed in a child thread.

<span id="finder和a-b的sdk是不是同一套？"></span>
# Are Finder and A/B SDKs the same?

Client side SDK: Finder and A/B share a set of SDKs, Finder uses the reporting capabilities of the SDK, and A/B uses the offloading and reporting capabilities of the SDK.

Server level SDK: Finder and A/B are two sets of SDKs. The Finder server level SDK has custom event reporting capabilities, and the A/B server level SDK has streaming capabilities and preset exposure event reporting capabilities.

<span id="对于购买finder后期增购a-b产品的客户，a-b的sdk是否需要重新集成or需要进行配置的"></span>
# For customers who purchase A/B products in the later stage of the Finder, whether the A/B SDK needs to be reintegrated or configured

Client side SDK: Finder and A/B are the same client side SDK. Just turn on the A/B switch, and you need to put the code related to obtaining experimental parameters in the code. Any changes to the code of the APP need to be reissued.

Server level SDK: Finder and A/B are different server level SDKs that require separate reference to the help documentation for integration.

<span id="a-b系统一个项目对应的app-id是固定的吗？多端是否使用同一个app-id"></span>
# Is the app_id corresponding to a project in the A/B system fixed? Do you use the same app_id

The appid is the unique identifier of the application. Whether multiple endpoints choose the same appid depends on whether data connection is required, because data between different applications is isolated. If it is the same application and you want to analyze the data in one application, report it under one application. If you want to isolate the data, create different experiments and specify the corresponding appid for event reporting.

<span id="客户端sdk是否支持配置不上报数据？"></span>
# Does the client side SDK support configuration not reporting data?

Not supported yet.

<span id="可以支持watch-os埋点吗？"></span>
# Can watch os event tracking be supported?

Not supported.

<span id="客户端sdk是否支持横屏-竖屏采集，如何实现的？"></span>
# Does the client side SDK support horizontal/vertical screen capture?

Android and iOS supported, Mini Program and Web/JavaScript temporarily unsupported. When initializing, set to turn on screen orientation collection. After turning it on, parameters will be added to all params reporting events:


* key: $screen_orientation

* value: "portrait" | "landscape"


**iOS**

```json
config.screenOrientationEnabled = YES;
```


**Android**

```json
config.setSecreenOrientationEnabled(true);
```


<span id="移动端sdk什么情况下会发起设备注册请求？"></span>
# When will the mobile end SDK initiate a device registration request?


1. Switching uuid initiates device registration

2. Refresh regularly, refresh interval is 6 hours

3. When nothing was done locally


<span id="app内嵌h5怎么实现数据打通？"></span>
# How to achieve data connection with H5 embedded in the APP?

For details, please refer to the section "Get through the embedded H5 page" in the documentation of the official website.

<span id="app内嵌h5如何做分流，打通与不打通有什么方案？"></span>
# How to do shunting with H5 embedded in the APP, and what are the plans for getting through and not getting through?

If you want to see the user's link behavior completely, you need to do the APP embedded H5 to get through, but after getting through, there is no way to do A/B experiments on the APP embedded H5 side. If you want to do A/B experiments, you need to do experiments on the APP side. Therefore, every experiment requires the client side to send version support;

If the APP and H5 are relatively independent and do not pay attention to the complete link behavior of the user, then there is no need to do data connection. H5 integrates the H5 SDK, and the APP integrates the APP SDK. The system also views the data of the APP and H5 separately. H5 experiments can be integrated directly according to the document.

If the APP and H5 do not do data connection, but want to connect, at present, only real\-name user association can be achieved. Both the APP and H5 need to be set with uuids, and the two uuids are consistent, so anonymous users cannot be associated. H5 does experiments directly according to the document integration, but for experiments done by H5, there is no way to use the event tracking behavior of the APP as an experimental indicator.

<span id="app能否支持打通阿里mpass-h5？"></span>
# Can the APP support getting through Ali mpass h5?

At present, the SDK only supports native WebView and Tencent X5, and does not support other frameworks for the time being.

<span id="移动端sdk的ssid存到哪里？是sdcard或者keychain里吗？"></span>
# Where is the ssid of the mobile end SDK saved? Is it in SDCard or Keychain?

No, the Android ssid will be saved to sharedpreference, iOS ssid will be saved to userdefaults, and the ssid will be gone after uninstalling.

<span id="flutter-sdk哪个版本支持全埋点功能？"></span>
# Which version of the Flutter SDK supports full event tracking?

1.4.0 version starts to support full event tracking function, please refer to the documentation for introduction: [Flutter SDK Full Event Tracking](https://docs.byteplus.com/docs/DataFinder/Flutter_SDK_Full_Event_Tracking).

<span id="react-native-sdk如何接入全埋点功能？"></span>
# How can React Native SDK access the full event tracking function?

Please refer to this function for details: [React Native full event tracking](https://docs.byteplus.com/docs/DataFinder/React_Native_Full_Event_Tracking).

<span id="react-native-版本的全埋点sdk，点击日志抓不到page-path？"></span>
# React Native version of the full event tracking SDK, click log can not catch page_path?

The APP page_path is the page where the clicked element is located, which is configured in autoTrack.config. If this is not configured, there is no value. Reference documents: [React Native full event tracking](https://docs.byteplus.com/docs/DataFinder/React_Native_Full_Event_Tracking).

<span id="5c01d8a1"></span>
# Is libcurl used in the Windows SDK?

The Windows SDK does not use libcurl.

<span id="5375cae8"></span>
# What is the SSL part of the Windows SDK? How to handle the issue of certificate renewal.

The SSL in the Windows SDK is not OpenSSL nor Windows Schannel. Because the Windows SDK itself is developed in Rust language and is compiled and packaged into a version of the Windows platform, there is no openssl or schannel in it. It is a set of HTTP mechanisms in Rust itself. At the same time, it supports external incoming HTTPClient, and when it is external, it is generated by external control requests.

<span id="d094a9b8"></span>
# What encoding format does Windows SDK char \* use?

The Windows SDK recommends using the UTF\-8 encoding format.
