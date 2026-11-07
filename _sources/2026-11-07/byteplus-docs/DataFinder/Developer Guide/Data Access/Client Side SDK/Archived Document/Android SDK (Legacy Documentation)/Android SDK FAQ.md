---
title: "Android SDK FAQ"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Android_SDK_FAQ"
---

<span id="aa2ed1ca"></span>
### Android SDK data reporting strategy

(1) When the SDK is not initialized, if there are events triggered (including custom ones), it will be cached in the client side memory, up to 300 pieces will be cached

(2) After the SDK is initialized, if there is an event triggered (including preset and custom), whether start is called, the library will be dropped before start, and it will be reported every 60s after start (up to 1600 items each time, if more than 1600 items are generated in one minute, you need to wait for the next 60s to report again).


* Before the 6.15.0 version, there is up to one pack per minute, and one pack has 200 pieces of data. If the failed pack will also try to send it;

* 6.15.0 and beyond policy is a maximum of 8 packs per minute;

   (3) After the SDK is initialized, if you switch users, report it immediately.


<span id="android-sdk是混淆过的还是非混淆的？"></span>
### Is the Android SDK obfuscated or non\-obfuscated?

The SDK provided is obfuscated.

<span id="android-sdk-6-10-0-版本是否还会采集-imsi-字段？"></span>
### Does 6.10.0 Android SDK also capture imsi fields?

After 6.9.6 version, the collection of the imsi field is removed. For parameters such as iimei, mac address, meid, etc., if you need to close, there are two strategies:


* Only turn off the collection behavior:


```sql
config.setImeiEnable(false);
```



* Remove the relevant acquisition code:


```kotlin
teaExtension {   
     //event tracking blacklist configuration, only the following configurations are supported:
     //'MAC_ADDRESS': mac address
     //'IMEI_MEID': imei and meid
     trackBlackList = ['MAC_ADDRESS', 'IMEI_MEID']
 }
```


<span id="安卓-sdk-初始化时设置的渠道信息时填写什么信息？"></span>
### What information is filled in when the channel information is set during the initialization of the Android SDK?

When initializing, the channel parameters are a required information, and the set channel parameters generally refer to the source channel of the app, such as an app store or app treasure, or custom channel information (vivo, huawei, etc.). If the customer cannot obtain these values, a default value can be set, such as "android_channel".

<span id="a-b-实验中-getabconfig-和-getallabtestconfigs-方法的区别？"></span>
### What is the difference between getAbConfig () and getAllAbTestConfigs () methods in A/B experiments?

getAbConfig () obtains the experimental results corresponding to the key passed in the parameter and reports the exposure event;

getAllAbTestConfigs () Gets the shunt results of all client side experiments by the user and does not report exposure events. It is important to note that the user experiment information returned is not a hit experiment (post\-exposure). If you need to obtain the VID information of the exposure group of the experimental user, the Android client side should use the getAbSdkVersion () method to obtain the exposure VID of the user, and the IOS side should use the allVids () method to obtain the exposure VID of the user.

<span id="android-插桩黑名单的配置是做什么用的？"></span>
### What is the configuration of the Android instrumentation blacklist used for?

It is used to filter classes that do not require instrumentation, such as third\-party libraries that do not require instrumentation, for example: Tinker.

<span id="apply-plugin-com-bytedance-std-tracker-此行代码是做什么用的？"></span>
### Apply plugin: 'com.bytedance.std.tracker' What does this line of code do?

Used to introduce the AppLog plug\-in, the plug\-in mainly has the following functions:


* Full event tracking instrumentation

   * Full event tracking is uploaded. If full event tracking is not required, it can be commented out. When accessing the SDK, this plug\-in will be used, and some instrumentation will be done in the dispatchTouchEvent of the Activity during the compilation period;

* Partially configurable sensitive information code collection and removal

* H5 open switch


<span id="android，关闭-oaid-android-id-采集时，该设备卸载重装-device-id-是否变化、重装时操作系统升级是否会变化？"></span>
### Android, when oaid & android id collection is turned off, does the device change device_id uninstalled and reinstalled, and does the operating system upgrade change when reinstalled?

If the Android ID is turned off, there will be generation logic inside the SDK, which will only take effect during installation and will be regenerated after uninstallation.

For details, please refer to the document "Turn off Android ID collection".

<span id="离线集成-sdk-想要避免-mac-信息的采集，在-app-的-build-gradle-中添加-teaextension-配置发现会报错"></span>
### If the offline integration SDK wants to avoid the collection of mac information, add the teaExtension configuration in the app's build.gradle and find that an error will be reported.

```kotlin
//Just choose one of the two

 //only turn off the acquisition behavior
 config.setMacEnable(false);

 //Remove the relevant acquisition code
 //outermost configuration in build.gradle at the app level
 teaExtension { 
     //event tracking blacklist configuration, only the following configurations are supported:
     //'MAC_ADDRESS': mac address
     //'IMEI_MEID': imei and meid
     trackBlackList = ['MAC_ADDRESS', 'IMEI_MEID'] 
 }
```


<span id="请问-a-b-实验-sdk-有针对-google-play-审核政策的版本吗？"></span>
### Does the A/B experimental SDK have a version of the review policy for Google Play?

At present, there is no SDK version specifically for Google Play. Overseas APPs need to integrate the global version, which meets the overseas privacy compliance policy.

<span id="sdk-初始化前会缓存数据，会获取用户信息吗？"></span>
### The SDK will cache data before initialization, will it get user information?

No, the custom event triggered by Android before initialization only caches the event information, and adds the obtained device information user information after initialization. It will not be obtained before init and will be obtained after init.

<span id="sdk-关闭所有设备采集，会影响数据采集吗？"></span>
### SDK closes all device collection, will it affect data collection?

It will affect the consistency of the did after unloading and reloading.

For details, please refer to the document "Turn off Android ID collection".

<span id="android-sdk-和其他第三方-sdk（如-bonreesdk）一起集成时插件-plugin-报冲突？"></span>
### Does the plugin conflict when the Android SDK is integrated with other third\-party SDKs such as bonreesdk?

```kotlin
//build.gradle at the app module level
//Default to the last declaration in the plugin list, if there is a conflict,
//You can adjust it to the first one after official plugins such as application/kotlin.
apply plugin: 'com.bytedance.std.tracker'
```


<span id="android-sdk-有可以检测-ssid-变化的-api-吗？"></span>
### Does the Android SDK have an API that can detect ssid changes?

You can listen to onRemoteIdGet through the callback method addDataObserver. The first parameter is boolean changed, but any parameter change will be true. At this time, you can compare @NonNull String oldSsid and @NonNull String newSsid to see if they are the same. If they are different, they will consider the change.

<span id="集成-android-sdk-的-app-最新版本是周二发的，为什么周一就有这么多人行为流里有新版本的事件？"></span>
### The latest version of the APP integrated with the Android SDK was released on Tuesday. Why are there so many events about the new version in the behavior stream on Monday?

It should be that the production reporting address was used during the test, so there is data.

<span id="android-sdk-获取的-oaid-是什么？"></span>
### What is the oaid obtained by the Android SDK?

OAID is the Open Anonymous Device Identifier (Open Anonymous Device Identifier, OAID), which is a device identifier of the Android platform in the alliance standard "Mobile Intelligent End Point Supplementary Device Identification System Specification" jointly researched and formulated by the Mobile Security Alliance, China Information and Communications Research Institute and end point manufacturers.

<span id="android-sd-k上报的数据，可以区分区分设备分类为手机-or-平板吗？"></span>
### Can the data reported by the Android SDK distinguish between devices classified as mobile phones or tablets?

The SDK does not make a direct distinction, but can only be distinguished by parameters, using the resolution field.
