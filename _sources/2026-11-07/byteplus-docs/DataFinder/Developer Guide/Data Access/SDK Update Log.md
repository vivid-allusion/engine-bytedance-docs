---
title: "SDK Update Log"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/SDK_Update_Log"
---

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip"><strong>SDK name:</strong> Growth Marketing Suite SDK.</div>


* <div data-tips="true" data-tips-type="tip"><strong>SDK latest version number:</strong> The current SDK version is being released in continuous iterations. You can go to the <a href="https://github.com/volcengine/datarangers-sdk-packages/tree/main">Git open source page </a>to view the latest SDK version and historical version of each end. It is recommended to use the latest version of the SDK.</div>


* <div data-tips="true" data-tips-type="tip"><strong>SDK developer:</strong> Beijing BytePlus Technology Co., Ltd.</div>


* <div data-tips="true" data-tips-type="tip"><strong>Key Features:</strong> The Growth Marketing Suite SDK supports the collection of fundamental data for the analysis of statistical metrics such as new additions, activations, retention, and performance of applications.</div>


* <div data-tips="true" data-tips-type="tip"><strong>Privacy Policy and compliance:</strong> ,<a href="https://docs.byteplus.com/docs/undefined/6a4ce432b59ed0056a0ef323">[Growth Marketing Suite SDK] Developer compliance</a></div>


* <div data-tips="true" data-tips-type="tip"><strong>Data access operation guide:</strong> For detailed access activity details of each end, please refer to the access SDK document of the corresponding end. The main end type links are as follows: <a href="https://docs.byteplus.com/docs/DataFinder/Legacy_Documentation_iOS_SDK_Integration">(Legacy Documentation)iOS SDK Integration</a>, <a href="https://docs.byteplus.com/docs/DataFinder/Android_SDK_Integration_">Android SDK Integration</a>, <a href="https://docs.byteplus.com/docs/DataFinder/HarmonyOS_Next_SDK_Integration_">HarmonyOS Next SDK Integration</a>, <a href="https://docs.byteplus.com/docs/DataFinder/Web_JavaScript_SDK_Integration_">Web/JavaScript SDK Integration</a>, ...</div>



<span id="f7af5196"></span>
# SDK Release Log

<span id="1646d697"></span>
## March 12, 2026

<span id="a52a584b"></span>
### Android: V6.17.7


1. Optimize event tracking verification Page display logic December 4, 2025


<span id="0a4ee65f"></span>
## March 2, 2026

<span id="b4a07798"></span>
### HarmonyOS: V1.3.3\-rc3


1. Align Android/iOS event custom properties limit 50k size, custom properties over 50k will be discarded and carry exception description information


<span id="d1947dc6"></span>
## January 9, 2026

<span id="d2904e59"></span>
### HarmonyOS: V1.3.3\-rc2


1. Optimize SDK packaging logic


<span id="e04ab918"></span>
## December 4, 2025

<span id="96d912c5"></span>
### iOS: V6.17.7\-iOS26


1. Repair iOS26 0x400000000000bad0

2. H5 gets through to update the uuid to do a good job of data verification protection to avoid SDK errors caused by incoming numbers, and only receives null and string.


<span id="313e0457"></span>
## October 11, 2025

<span id="f467ecc3"></span>
### Android: V6.17.6


1. Optimize internal packaging logic

2. Remove iccid acquisition

3. Event custom attributes are limited to 50k size. Custom attributes over 50k will be discarded and carry exception description information

4. Full event tracking custom parameters do not support passing preset properties


<span id="13ccdb4e"></span>
### iOS: V6.17.6


1. Optimize internal packaging logic

2. Event custom attributes are limited to 50k size. Custom attributes over 50k will be discarded and carry exception description information

3. Full event tracking custom parameters do not support passing preset properties


<span id="a04a1a97"></span>
## August 8, 2025

<span id="a030bda3"></span>
### Android: V6.17.5


1. Optimize the page to enter the reporting opportunity

2. Optimize fragment filtering logic

3. Optimize ssid judgment logic


<span id="ca167f7b"></span>
### iOS: V6.17.5


1. Optimize ssid judgment logic


<span id="a2dbaeb3"></span>
## July 4, 2025

<span id="0b50cf1b"></span>
### Android: V6.17.4


1. Android 15 16k so compatible

2. Remove mnc_mcc collection

3. AppId supports safe mode

4. Crash event stack information should not exceed 2000 characters


<span id="244967c7"></span>
### iOS: V6.17.4


1. AppId supports safe mode

2. Added a large\-volume event blocking reporting logic optimization switch, which is turned off by default and can be selected to be turned on.


<span id="bcf9ef1b"></span>
### HarmonyOS: V1.3.3\-rc2


1. Remove mnc_mcc collection

2. AppId supports safe mode


<span id="ebf901cf"></span>
## June 6, 2025

<span id="3bcf01e5"></span>
### Web: V5.2.8


1. After user_uniqueid_id_type is set, persistent storage is performed

2. By default, devtools' own event tracking collection is turned off, which can be configured to be turned on.

3. The devtools button can be dragged and dropped.


<span id="215ad703"></span>
## May 7, 2025

<span id="1181fb79"></span>
### Web: V5.2.7


1. Support collection of SDK internal monitoring data


<span id="583ccd4e"></span>
## April 3, 2025

<span id="e9ac37a3"></span>
### Web: V5.2.6


1. Supports retry mechanism after failed Tracer ID binding.

2. Support collecting system type and system version number in Hongmeng system in H5. The collected Hongmeng system name is OpenHarmony, and the version number is x.x.x.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b45d61c55bc444408f05410c934e7aa2~tplv-goo7wpa0wc-image.image) </span>


3. Support collecting UTM information after URL #.

4. Supports a retry mechanism after data reporting fails.


<span id="1a797f2b"></span>
## March 31, 2025

<span id="3ba7e272"></span>
### Android: V6.17.1


1. Preset events support cloud\-controlled blacklist filtering

2. AB exposure event support whether to generate switch repeatedly

3. Devtools support shows if plugins are integrated

4. Plugin removal imei/operator information logic adjustment


<span id="f7f80c47"></span>
### iOS: V6.17.3


1. Preset events support cloud\-controlled blacklist filtering

2. AB exposure event support whether to generate switch repeatedly

3. Devtools supports displaying network capture content


<span id="85ad83a2"></span>
### HarmonyOS MetaService: V1.0.0\-rc1


1. Added Hongmeng Yuan Service SDK


<span id="59b8e827"></span>
### HarmonyOS: V1.3.1\-rc1


1. Preset events support cloud\-controlled blacklist filtering

2. Added long event support

3. Align Android Privacy Mode

4. Add x86_64 so

5. Added SSID request acquisition method

6. os_version Get Logic Adjustment

7. AB exposure event support whether to generate switch repeatedly


<span id="98312497"></span>
## March 14, 2025

<span id="d1141c85"></span>
### Web: V5.2.5


1. Support dynamic recognition of protocol settings for loading three\-party js


<span id="2bdfb402"></span>
## February 28, 2025

<span id="c88a4160"></span>
### Android: V6.17.0


1. Added response to close encryption switch

2. When the web SDK is connected, disable the SDK uuid or uuidType on the web SDK update side when supported.

3. Web SDK supports multiple criteria when getting through

4. sim_region subject to operator switch control

5. External API part tag is deprecated


<span id="7d1e484e"></span>
### iOS: V6.17.2


1. Added response to close encryption switch

2. When the Web SDK is connected, disable the SDK uuid or uuidType on the Web SDK update side when supported.

3. Web SDK supports multiple criteria when getting through

4. Fix the Crash problem caused by the wild pointer occasionally when the user pulls the AB experimental configuration


<span id="e7d34d02"></span>
### Web: V5.2.4


1. Support setting the protocol for loading three\-party js to http or https.

2. Optimized some problems


<span id="1731f501"></span>
## February 12, 2025

<span id="4cdcc23a"></span>
### Web: V5.2.3


1. Increase data reporting compression


<span id="de954739"></span>
## December 3, 2024

<span id="5820105f"></span>
### Flutter: 1.4.1


1. Hongmeng system adaptation

2. Support overseas version dart initialization

3. Event tracking parameters that support array format

4. Optimize iOS event tracking parameter is empty to cause crashes

5. Add start API to support separate calls to init and start


<span id="e663c91d"></span>
## November 30, 2024

<span id="57f6802e"></span>
### HarmonyOS: V1.3.0\-rc1


1. Adjust global log output rules

2. Fix the problem that the exposure type is wrong due to repeated monitoring of exposure

3. Support id_bind

4. Packaging based on release

5. Optimize the SDK product and adjust it to a bytecode product

6. Fix devtools focus issue


<span id="d7da7e86"></span>
## November 26, 2024

<span id="7975ab6c"></span>
### ReactNative: 0.2.13\-rc.0


1. Support react 17 and above

2. Fix ant\-design\-mobile\-rn compatible SegmentedControl component click crash issue


<span id="c55d3a90"></span>
## November 28, 2024

<span id="55ccc4a7"></span>
### Web: V5.2.2


1. Add tracerid binding failed retry

2. Optimize the logic of blacklisting under logSetting

3. Optimized the use of multiple instances


<span id="bec7948f"></span>
## November 13, 2024

<span id="383b6cc8"></span>
### iOS: V6.17.0


1. Compatible with the presence of illegal fields when users set UserID, resulting in SDK Crash scenarios

2. Fix thread deadlock caused by occasional cold start real\-time event tracking detection


<span id="0b50f19c"></span>
## October 23, 2024

<span id="9bb3bbde"></span>
### Web: V5.2.1


1. Added a origin_referrer and origin_referrer_host to the header custom to record the original refer, which defaults to document.referrers.


<span id="7e81cb23"></span>
## September 30, 2024

<span id="ce3e2c34"></span>
### HarmonyOS: 1.2.0\-beta1/SaaS\-only cloud native support


1. Support Hongmeng component exposure capability

2. Support full event tracking capability, beta version

3. Add Oaid, operator information collection switch


<span id="8c73a335"></span>
## September 26, 2024

<span id="e6c9c62e"></span>
### Android: V6.16.11


1. Support custom Oaid

2. Fix profile concurrent calls


<span id="0eaaf5c9"></span>
## September 9, 2024

<span id="794adaef"></span>
### iOS: V6.16.9


1. iOS 18 adaptation

2. Split sub\-library Game, support game mode and game interface separate access


<span id="4e6d050f"></span>
## September 5, 2024

<span id="7218c97f"></span>
### Web: V5.2.0

Update content:


1. Web DevTools has released version 2.0 with updated UI and optimized functionality.

2. Supports bindToken and Tracer dual\-sending logic.

3. Added custom requestToken.

4. Added failed local data store, enabled by enable_storage.


<span id="cd367058"></span>
## August 31, 2024

<span id="600310a5"></span>
### Android: V6.16.10


1. Support 360 Oaid acquisition

2. Support duration event custom event name

3. app_region acquisition logic aligned with iOS

4. Adjust event custom property validation prompt logic


<span id="9d44ed13"></span>
## August 5, 2024

<span id="ce60ebff"></span>
### HarmonyOS: 1.1.0\-beta5/SaaS\-only cloud native support


1. Adjust gzip dependency logic

2. Adjust the oh\-package component name specification


<span id="c018b5e1"></span>
## July 10, 2024

<span id="0b74d3a2"></span>
### Android: V6.16.9


1. Support request to add dynamic headers

2. Adjust the event range of the corresponding version information when the event is added

3. Event tracking validation/circling request shortening request timed out event

4. Fix some known issues


<span id="c11a7cfc"></span>
## June 28, 2024

<span id="b19092aa"></span>
### iOS: V6.16.8


1. Added block function to support custom HTTPHeaderFields

2. stability optimization


<span id="5b957202"></span>
## June 14, 2024

<span id="5ac560ab"></span>
### HarmonyOS: 1.1.0\-beta2/SaaS\-only cloud native support


1. Adapted to the SaaS\-cloud native environment, the SaaS\-cloud native environment has been reported to Hongmeng

2. Adapt to some new features of 5.0 SDK


<span id="62ec278c"></span>
## June 12, 2024

<span id="af9306ab"></span>
### Web: V5.1.12


1. Optimized the stop/reStart APIs by adding logic to re\-expose elements within the visual area when calling reStart.

2. Fixed the tracerdata information report of utm.


<span id="f0bafb3c"></span>
## June 11, 2024

<span id="b740c5eb"></span>
### HarmonyOS Devtools: 1.1.0\-beta2/SaaS\-only cloud native support (debugging tools)


1. Added debug log module

2. Added configuration information module

3. Added built\-in scan function


<span id="3515a633"></span>
## May 17, 2024

<span id="861542cb"></span>
### Web: V5.1.11


1. Fixed the problem of abnormal exposure type of page elements.

2. Report $user_unique_id_type in profile user properties when setting user_unique_id_type is removed.

3. The attributes attribute has been added to the exposure settings, which can be set to not listen when the element attributes change, and the default is true.


<span id="acf35ee8"></span>
## May 8, 2024

<span id="0e6d01a0"></span>
### HarmonyOS: 1.0.0\-beta2/SaaS\-only cloud native support


1. Adapt to 5.0 sdk


<span id="4b5fbdb1"></span>
## April 23, 2024

<span id="74aabe2b"></span>
### iOS: V6.16.6


1. Support Apple privacy configuration domain name


<span id="c1ddbdf9"></span>
## April 18, 2024

<span id="8481416c"></span>
### Web: V5.1.10.feature


1. Fixed an issue where the exposure type of page elements was abnormal after returning from other pages in the open scene.


<span id="bb51daeb"></span>
## April 9, 2024

<span id="e11cf1a3"></span>
### Android: V6.16.6


1. OAID compatible with Honor's new system


<span id="9cbf42d8"></span>
### Web: V5.1.10


1. AB test added full exposure option


<span id="ec5efa4d"></span>
### Web: V5.1.9 feature


1. Fixed an issue that could affect vue pushstate when using the exposure function


<span id="185c04f7"></span>
## March 29, 2024

<span id="7545bd54"></span>
### HarmonyOS: 1.0.0\-beta1/SaaS\-only cloud native support

Supported functions:


* Device registration

* Custom event tracking

* Data reporting

* Request encryption (default encryption/country secret sm2)

   User and user attributes

* server level AB shunt experiment

* Event blacklist

* Multiple instances

* web connection

* Crash acquisition (JS layer)

* Real\-time event tracking verification

* custom header settings

    &nbsp;


<span id="harmonyos-devtools：1-0-0-beta1-2024-3-29"></span>
#### HarmonyOS Devtools：1.0.0\-beta1 / 2024.3.29


* View event information

* View network requests

* Check access status


<span id="77f913de"></span>
## March 5, 2024

<span id="ed4db53e"></span>
### Android: V6.16.4


1. Circle selection/real\-time event tracking verification Support multiple set\-cookies parsing


<span id="dbf0f60e"></span>
### iOS: V6.16.4


1. Full event tracking


<span id="86bdb19b"></span>
## January 17, 2024

<span id="6cb70128"></span>
### Web: V5.1.9


1. After optimizing the webid request exception, cache the data of the abnormal webid

2. Slide event tracking supports dynamically added elements

3. Added custom properties for full event tracking


<span id="c99c0490"></span>
## January 2, 2024

<span id="e06cd0d4"></span>
### Android: V6.16.3


1. Support Android Gradle Plugin 8 version plugin

2. HTTPS request support to set up SSLSocketFactory

3. Preset Event Launch and Terminate Support Off

4. clipboard access code supports plug\-in removal


<span id="019a7ea0"></span>
### iOS: V6.16.3


1. No longer collect carrier and mcc_mnc attributes

2. Preset Event Launch and Terminate Support Off

3. uuid information is changed to encrypted storage


<span id="419f9345"></span>
## November 29, 2023

<span id="abfba352"></span>
### Web: V5.1.8


1. Optimized the referring information of single page application PV

2. Optimized the information reported by the hash route

3. Support configuring mask layer transparency for multi\-link or visual experiments

4. Added the configuration delivery of logsettings


<span id="_2023年11月29日"></span>
## November 29, 2023

<span id="android-ios-v6-16-2"></span>
### Android / iOS: V6.16.2


1. WebVIew circle selection optimization div == 0 scene circle selection

2. Fixed some known issues

    &nbsp;


<span id="november-16-2023"></span>
## November 16, 2023

<span id="web-v5-1-7"></span>
### Web: V5.1.7


1. Optimized the reporting of exposure event tracking

2. Added reporting of sliding event tracking

3. Fix the problem that the setting properties do not take effect after the embedded H5 and the client side are connected

4. The event tracking debugging tool removes the restriction of url parameters, just open enable_debug

    &nbsp;


<span id="september-28-2023"></span>
## September 28, 2023

<span id="android-ios-v6-16-0"></span>
### Android / iOS: V6.16.0


1. Expansion of exposure event capabilities, support interception, adding attributes, exposure according to display time, etc

    &nbsp;


<span id="september-11-2023"></span>
## September 11, 2023

<span id="android-v6-15-5"></span>
### Android: V6.15.5


1. The local data cache is adjusted to 30 days (the server level only receives historical data within 7 days by default. If you need to report the local cached data within the range of 7 days, please contact the operation and maintenance to adjust the server level settings synchronously)

2. Version and model information when the event is added

3. Add WebView loop

4. Optimized some functions

    &nbsp;


<span id="ios-v6-15-5"></span>
### iOS: V6.15.5


1. Version and model information when the event is added

2. Add WebView loop

3. Optimized some functions

    &nbsp;


<span id="july-26-2023"></span>
## July 26, 2023

<span id="ios-v6-15-4"></span>
### iOS: V6.15.4


1. Optimized some functions

    &nbsp;


<span id="july-18-2023"></span>
## July 18, 2023

<span id="android-v6-15-4"></span>
### Android: V6.15.4


1. ALink DDL Added Failed Callback

2. Optimized some functions

    &nbsp;


<span id="june-13-2023"></span>
## June 13, 2023

<span id="小程序-v2-9-1"></span>
### Mini Program: V2.9.1


1. Using the asynchronous storage interface

2. AB split interface supports timeout setting


<span id="_2023年05月29日"></span>
## May 29, 2023

<span id="android-v6-15-2"></span>
### Android: V6.15.2


1. Compliance transformation

2. Exposure event detection strategy support toggle

3. Adapt to Tinker plugin

4. Supports some header field filtering

5. Optimized some functions


<span id="ios-v6-15-2"></span>
### iOS: V6.15.2


1. Exposure event detection strategy support toggle

2. Supports some header field filtering

3. Optimized some functions


<span id="_2023年4月10日"></span>
## April 10, 2023

<span id="小程序-v2-9-0"></span>
### Mini Program: V2.9.0


1. Support for Lark widgets

2. Support anonymous_id

3. Support national secret encryption

4. Support for capturing Mini Program default tabbar click events


<span id="_2023年03月31日"></span>
## March 31, 2023

<span id="android-v6-15-0"></span>
### Android: V6.15.0


1. Privatized cloud control configuration is issued

2. Privatization supports custom encryption and provides national secret encryption plugins

3. Batch report plan adjustment

4. Support AB response encryption

5. Optimized some functions


<span id="ios-v6-15-0"></span>
### iOS: V6.15.0


1. Privatized cloud control configuration is issued

2. Added sublibrary Encryptor/SM2, privatization request encryption supports national secret SM2 algorithm

3. Batch report plan adjustment

4. Support AB response encryption

5. Optimized some functions


<span id="_2023年03月15日"></span>
## March 15, 2023

<span id="web-v5-1-6"></span>
### Web: V5.1.6


1. Support national secret algorithm encryption and reporting

2. Optimized some functions


<span id="_2023年02月28日"></span>
## February 28, 2023

<span id="web-v5-1-5"></span>
### Web: V5.1.5


1. Support for anonymous ID settings

2. Optimize the stay duration under IOS and report when leaving


<span id="小程序-v2-8-3"></span>
### Mini Program: V2.8.3


1. Support to turn on the real\-time detection function under the hot start of the Mini Program


<span id="_2023年02月16日"></span>
## February 16, 2023

<span id="ios-v6-14-4"></span>
### iOS: V6.14.4


1. Added sublibrary GlobalRemoteID to support feature collection


<span id="_2023年02月14日"></span>
## February 14, 2023

<span id="android-v6-14-3"></span>
### Android: V6.14.3


1. Huawei mobile operating system recognizes harmony os

2. Full event tracking switch Plugin

3. Add IccId switch

4. Removing support dependencies

5. Adjust the monitoring switch rules for domestic SAAS users and complete the first\-phase monitoring link


<span id="ios-v6-14-2"></span>
### iOS: V6.14.2


1. Basic library to OneKit dependencies


<span id="_2023年2月9日"></span>
## February 9, 2023

<span id="小程序-v2-8-2"></span>
### Mini Program: V2.8.2


1. Fix tracer's utm short URL receiving request issue


<span id="_2023年2月7日"></span>
## February 7, 2023

<span id="小程序-v2-8-1"></span>
### Mini Program: V2.8.1


1. Add information such as the title of the previous page to the page browsing event (predefine_pageview)

2. Ability to add params for preset events


<span id="_2023年1月3日"></span>
## January 3, 2023

<span id="小程序-v2-8-0"></span>
### Mini Program: V2.8.0


1. Support Kuaishou Mini Program


<span id="_2022年12月21日"></span>
## December 21, 2022

<span id="android-v6-14-2"></span>
### Android: V6.14.2


1. Support RN circle selection;

2. Support user multi\-criteria binding OneID;

3. Extended event tracking API to support event\-level A/B Testing exposure settings;

4. Embedded H5 ABTest shunt connection;

5. Report policy adjustment: report once by default in the background (and manually call flush to share 10s frequency control);

6. Support commercial IPID requirements.

7. Fix known issues.


<span id="ios-v6-14-1"></span>
### iOS: V6.14.1


1. Support user multi\-criteria binding OneID;

2. Support for new user models.

3. Tester H5 function is connected;

4. Extended event tracking API to support event\-level A/BTesting exposure settings.

5. Fix known issues.


<span id="reactnative-v0-2-4"></span>
### ReactNative: V0.2.4


1. Support RN circle selection;

2. element_path increase the pagename to which the element belongs, and increase the index of each level element relative to the parent node;

3. Greatly shortens the path length of ReactNavigation page elements.

4. Against js compression, the commonly used click component names are no longer garbled after js compression;

5. Fix known issues.


<span id="_2022年12月15日"></span>
## December 15, 2022

<span id="小程序-v2-7-1"></span>
### Mini Program: V2.7.1


1. Add retry function for webid request, default 10 times, provide request_webid_number parameters to override settings;

2. Added supplementary reporting within 3 seconds when the Mini Program retreats to the background;

3. Provide parameter control to turn on or off related functions: support skipping environmental monitoring of launch, network, etc., support turning off event name attribute detection, support turning off Mini Program real\-time detection function


<span id="_2022年12月9日"></span>
## December 9, 2022

<span id="小程序-v2-7-0"></span>
### Mini Program: V2.7.0


1. Support JD.com Mini Program


<span id="_2022年11月29日"></span>
## November 29, 2022

<span id="小程序-v2-6-0"></span>
### Mini Program: V2.6.0


1. Support encryption: Encrypt the reported event content and implement the encrypt plug\-in

2. Align some client side APIs (first phase): setUserUniqueID, setHeaderInfo, removeHeaderInfo


<span id="_2022年11月18日"></span>
## November 18, 2022

<span id="web-v5-1-4"></span>
### web: V5.1.4


1. Added event tracking debugging tool;

2. The client side supports AB API calls

3. Added disable_ab_rest parameter to disable AB reset when switching uuids


<span id="_2022年11月17日"></span>
## November 17, 2022

<span id="小程序-v2-5-4"></span>
### Mini Program: V2.5.4


1. Add information such as the Mini Program version of the collection business


<span id="_2022年10月21日"></span>
## October 21, 2022

<span id="小程序-v2-5-3"></span>
### Mini Program: V2.5.3


1. Added supplementary reporting of cache events (stored in storage) when hot starting and switching networks


<span id="_2022年10月18日"></span>
## October 18, 2022

<span id="web-v5-1-3"></span>
### web: V5.1.3


1. Added hash routing monitoring;

2. Support AB multi\-link experiment fallback;

3. Support AB cross\-domain name storage data;

4. The client side connection parameter was changed from Native to enable_native;


<span id="_2022年10月14日"></span>
## October 14, 2022

<span id="ios-v6-13-1"></span>
### iOS: V6.13.1


1. Added pulling DataTester experiment method, supports setting timeout time and response callback function;

2. Event tracking real\-time verification prompt optimization;

3. Allows users to customize part of the HTTPHeader for SDK requests.

4. Support setting user uuid before SDK initialization;

5. Fix known issues.


<span id="android-v6-13-3"></span>
### Android: V6.13.3


1. Added application crash event collection.

2. Added disabled event configuration;

3. Added capture Google AID configuration switch;

4. Added Get multi\-instance interface;

5. Added pull AB test configuration interface to set timeouts and callbacks;

6. Real\-time event tracking verification Added page access event verification;

7. Support setting user uuid before SDK initialization;

8. Fragment event tracking;

9. Fix known issues.


<span id="_2022年10月11日"></span>
## October 11, 2022

<span id="小程序-v2-5-2"></span>
### Mini Program: V2.5.2


1. Perfect cache logic: Optimized for cache logic when the network exists (the network may be blocked or there may be timeouts)


<span id="_2022年9月23日"></span>
## September 23, 2022

<span id="小程序-v2-5-1"></span>
### Mini Program: V2.5.1


1. Fixed an issue where the "share" event returned an empty path without initialization.

2. app_terminate increase terminate_type parameters to distinguish the reporting time;

3. Fixed some logical problems of Mini Program real\-time event tracking detection for host judgment;


<span id="_2022年9月5日"></span>
## September 5, 2022

<span id="ios-v6-12-5"></span>
### iOS: V6.12.5


1. Added support for activation service custom parameters;

2. Remove the strong dependency on CoreLocation.

3. Added support for debugging tools.

4. Fix known issues.


<span id="android-v6-12-0"></span>
### Android: V6.12.0


1. Added multiple instances to configure debugging log switch and custom printing separately;

2. Added support for debugging tools.

3. Fix known issues.


<span id="_2022年9月1日"></span>
## September 1, 2022

<span id="小程序-v2-5-0"></span>
### Mini Program: V2.5.0


1. Fix the decoding of urls in createViewUrl


<span id="_2022年07月20日"></span>
## July 20, 2022

<span id="web-v5-1-2"></span>
### web: V5.1.2


* Added event tracking verification function of H5 page;


<span id="_2022年07月14日"></span>
## July 14, 2022

<span id="ios-v6-11-0"></span>
### iOS: V6.11.0


1. Added support for configuring full event tracking event types;

2. Added event name and attribute validation log hints;

3. Added anti\-cheating module to report manually;

4. Fix known issues.


<span id="android-v6-11-0"></span>
### Android: V6.11.0


1. Added support for configuring full event tracking event types;

2. Added event name and attribute validation log hints;

3. Fix known issues.


<span id="_2022年06月2日"></span>
## June 2, 2022

<span id="web-v5-1-1"></span>
### web: V5.1.1


* Added exposure event capture;

* Added tracking event collection.

* Added event & attribute legitimacy verification;

* Added user_unique_id_type attributes;

* Added full event tracking event single event switch.


<span id="_2022年05月23日"></span>
## May 23, 2022

<span id="ios-v6-10-0"></span>
### iOS: V6.10.0


* Added capture screen direction and GPS coordinates;

* Add duration events and leave page event duration;

* Added exposure event capture;

* Support setting user ID type.

* Support for clearing cache events.


<span id="android-v6-10-0"></span>
### Android: V6.10.0


* Added capture screen direction and GPS coordinates;

* Add duration events and leave page event duration;

* Added exposure event capture;

* Support for setting user ID types.


<span id="_2022年03月29日"></span>
## March 29, 2022

<span id="ios-v6-8-1"></span>
### iOS: V6.8.1


* Added event collection callback, support custom modification parameters;

* Added internationalization support for real\-time event tracking verification capabilities;

* Fix known issues.


<span id="android-v6-9-6"></span>
### Android: V6.9.6


* Adapt to Hongmeng system;

* Adapt to x5webview, support custom webview;

* Added the ability to ignore, manually capture pages, and click events.

* Added event collection callback, support custom modification parameters;

* Added Fragment full event tracking event switch;

* Added internationalization support for real\-time event tracking verification capabilities;

* Added the configuration of setting the current process as the main process;

* Adapted to support ASM9;

* Added OAID and Androidid acquisition switches;

* Stripping away unnecessary dependencies.

* Fix known issues.


<span id="_2022年02月11日"></span>
## February 11, 2022

<span id="ios：v6-7-0"></span>
### iOS：v6.7.0


* The SDK supports multiple instances.

* Alink interface attribute_data and alink_data increase encryption;

* Full event tracking supports custom attributes;

* Fix known issues.


<span id="android：v6-8-0"></span>
### Android：v6.8.0


* The SDK supports multiple instances.

* Alink interface attribute_data and alink_data increase encryption;

* The alink short URL reports the $invoke event when it repeatedly evokes the app;

* Support Activity and View to set custom event tracking properties;

* Add plugin blacklist configuration event tracking collection;

* Optimized the adaptability of vivo and CoolPad mobile phones to obtain oaid;

* Fix known issues.


<span id="_2021年12月13日"></span>
## December 13, 2021

<span id="ios：v6-6-0"></span>
### iOS：v6.6.0


* Added autoTrackEnabled switch;

* Optimize background and passive startup.

* Added interface for manually pulling AB test configuration;

* Optimize the Alink function.


<span id="android：v6-7-0"></span>
### Android：v6.7.0


* Add start and launch preset event properties;

* Optimize imei and meid acquisition, adapt privacy compliance;

* Added interface for manually pulling AB test configuration;

* Fix known issues.


<span id="_2021年11月15日"></span>
## November 15, 2021

<span id="ios：v6-5-0"></span>
### iOS：v6.5.0


* Added full event tracking event property;

* ALink removes is_retargeting callback limit;

* Added the new trackEventEnabled switch to turn off all event reporting.


<span id="android：v6-6-2"></span>
### Android：v6.6.2


* Added full event tracking event property;

* Added initialization configuration field: report event switch;

* Cancel the reporting conditions for remarketing.

* Fix known issues.


<span id="_2021年10月20日"></span>
## October 20, 2021

<span id="ios：v6-4-0"></span>
### iOS：v6.4.0


* Added app_launch and invoke events to support $deeplink_url preset properties;

* Support adding uuid upload in event params;

* Fix known issues.


<span id="_2021年10月15日"></span>
## October 15, 2021

<span id="android：v6-5-0"></span>
### Android：v6.5.0


* Added support for multiple instances.

* Added app_launch and invoke events to support $deeplink_url preset properties;

* The plugin adapts to ASM7;

* Fix known issues.


<span id="_2021年9月08日"></span>
## September 08, 2021

<span id="ios：v6-3-0"></span>
### iOS：v6.3.0


* Added custom encryption method (available for private deployment);

* Fix BDAutoTrackDefaults class file lock crash;

* Add whether isNewUser is a new user.


<span id="android：v6-4-1"></span>
### Android：v6.4.1


* Fixed the error of the correspondence between uuid and ssid in launch;

* Support oaid version 1.0.26.


<span id="_2021年8月04日"></span>
## August 04, 2021

<span id="ios：v6-2-3"></span>
### iOS：v6.2.3


* Support Apple Search Ads.

* Support Alink related data collection.


<span id="_2021年8月03日"></span>
## August 03, 2021

<span id="android：v6-3-0"></span>
### Android：v6.3.0


* When adding and switching users, set the data sending method;

* Increase the debug mode to close the log;

* Support Alink related data collection.


<span id="_2021年7月21日"></span>
## July 21, 2021

<span id="小程序：v1-7-0"></span>
### Mini Program: v1.7.0


* Add custom WebID.

* Increase the default to get utms related data from the interface;


<span id="_2021年6月18日"></span>
## June 18, 2021

<span id="android：v6-2-0"></span>
### Android：v6.2.0


* Add the interface to obtain the applog version number;

* Fix event tracking detection interruption problem;

* Switch the user support to clear the A/B configuration cache information switch, the default is true;


<span id="_2021年6月15日"></span>
## June 15, 2021

<span id="ios：v6-2-0"></span>
### iOS：v6.2.0


* Support four\-digit version number reporting interface;

* Support embedded H5 to turn off full event tracking event collection;

* Switch the user support to clear the A/B configuration cache information switch, the default is true;


<span id="_2021年5月15日"></span>
## May 15, 2021

<span id="android：v6-1-2"></span>
### Android：v6.1.2


* Separate the scheme into separate modules without setting the scehem parameter.

* When initializing, add switch to control whether to collect embedded H5 data;

* Update the access field before sending the event;

* Clear the vid cache when switching users.


<span id="_2021年4月15日"></span>
## April 15, 2021

<span id="android：v6-0-2"></span>
### Android：v6.0.2


* Support profile user attribute reporting;

* Support embedded H5 reporting event tracking from Native;

* Fix client side time reporting issue.


<span id="ios：v6-0-0"></span>
### iOS：v6.0.0


* Support profile user attribute reporting;

* Support embedded H5 reporting event tracking from Native;

* Optimize AB data update strategy when switching users.


<span id="_2021年02月08日"></span>
## February 08, 2021

<span id="android：v5-5-6"></span>
### Android：v5.5.6


* Support the first trigger event marker $is_fisrt_time report;

* Add game side event tracking template interface;

* Fix playesession computation time issue.


<span id="ios：v5-6-5"></span>
### iOS：v5.6.5


* Support the first trigger event marker $is_fisrt_time report;

* Add game side event tracking template interface;

* Optimize the acquisition of AB configuration timing, and obtain it immediately after the SDK is initialized.


<span id="_2021年01月06日"></span>
## January 6, 2021

<span id="ios：v5-6-4"></span>
### iOS：v5.6.4


* Support bitcode;

* Support platform side attributes;

* Provides an interface for separate initialization of class methods and separate launch of the SDK.

   +[BDAutoTrack sharedTrackWithConfig:]

   +[BDAutoTrack startTrack]


<span id="_2020年12月30日"></span>
## December 30, 2020

<span id="android：v5-5-5"></span>
### Android：v5.5.5


* Add platform attributes, as the end;

* AB configuration client side caching mechanism changes;

* Special cases of webview refresh issues.


<span id="_2020年12月04日"></span>
## December 04, 2020

<span id="微信小程序：v1-3-11"></span>
### WeChat Mini Program: v1.3.11


* Added enable_filter_crawler parameters to filter crawler scenes after opening (scene: 1129, currently only WeChat Mini Program has this scene).


<span id="_2020年11月25日"></span>
## November 25, 2020

<span id="android：v5-5-1"></span>
### Android：v5.5.1


* Added car ring selection data collection;

* Adapt to 1.0.23 SDK.


<span id="ios：v5-6-3"></span>
### iOS：v5.6.3


* Optimize the GlobalDID algorithm.


<span id="_2020年11月20日"></span>
## November 20, 2020

<span id="微信小程序：v1-3-6"></span>
### WeChat Mini Program: v1.3.6


* Optimize mp_platform field type to string.


<span id="_2020年10月20日"></span>
## October 20, 2020

<span id="android：v5-4-1"></span>
### Android：v5.4.1


* Added profile interface (private environment support);

* Added Vue support \- Cordova. Vue Packaging App;

* Fix event tracking detection related issues.


<span id="_2020年10月19日"></span>
## October 19, 2020

<span id="微信小程序：v1-3-6"></span>
### WeChat Mini Program: v1.3.6


* Added utm parameter processing;

* Optimized profile data type detection (privatization V3.X version).


<span id="_2020年09月22日"></span>
## September 22, 2020

<span id="微信小程序：v1-3-0"></span>
### WeChat Mini Program: v1.3.0


* Added automatic reporting predefine_pageview_hide (page exit) event.


<span id="_2020年09月11日"></span>
## September 11, 2020

<span id="微信小程序：v1-2-0"></span>
### WeChat Mini Program: v1.2.0


* Added profile function, providing profileSet, profileUnset and other methods (privatized V3.X version).


<span id="_2020年08月29日"></span>
## August 29, 2020

<span id="android：v5-3-0"></span>
### Android：v5.3.0


* Added full event tracking switch;

* Fixed the inability to customize the message header;

* Listen to the cloud integration compatibility.


<span id="_2020年08月20日"></span>
## August 20, 2020

<span id="ios：v5-4-1"></span>
### iOS：v5.4.1


* Added query encryption;

* Fixed the problem that server level backpack parsing failed in a privatized environment.


<span id="_2020年07月29日"></span>
## July 29, 2020

<span id="ios：v5-4-0"></span>
### iOS：v5.4.0


* Optimize IDFA acquisition strategy to provide separate acquisition.


<span id="_2020年07月28日"></span>
## July 28, 2020

<span id="android：v5-2-6"></span>
### Android：v5.2.6


* Fixed the crash caused by switching uuid timing.


<span id="_2020年07月13日"></span>
## July 13, 2020

<span id="android：v5-2-4"></span>
### Android：v5.2.4


* Repair oaid;

* Fixed startup crash issue.


<span id="_2020年06月19日"></span>
## June 19, 2020

<span id="ios：v5-3-1"></span>
### iOS：v5.3.1


* Added custom public attribute Custom header interface;

* Added immediate report data flush interface.


<span id="_2020年06月17日"></span>
## June 17, 2020

<span id="android：v5-2-1"></span>
### Android：v5.2.1


* Optimize uuid switching, origin_session_id strategy;

* Fixed the bug.


<span id="_2020年06月15日"></span>
## June 15, 2020

<span id="ios：v5-3-0"></span>
### iOS：v5.3.0


* Optimize uuid switching cache strategy;

* Fixed the bug.


<span id="_2020年06月09日"></span>
## June 9, 2020

<span id="android：v5-2-0"></span>
### Android：v5.2.0


* Added real\-time event tracking detection and reporting interface;

* Optimize uuid after switching users, add session policy.


<span id="ios：v5-2-0"></span>
### iOS：v5.2.0


* Added real\-time event tracking detection and reporting interface;

* Fixed the bug.


<span id="_2020年04月28日"></span>
## April 28, 2020

<span id="android：v5-1-2"></span>
### Android：v5.1.2


* Optimize the pop\-up window simulation function;

* Fix the bug.


<span id="ios：v5-1-0"></span>
### iOS：v5.1.0


* Optimize setAbEnable interface;

* Fixed the bug.


<span id="_2020年04月12日"></span>
## April 12, 2020

<span id="android：v5-0-0"></span>
### Android：v5.0.0


* Optimize circling data collection capabilities;

* Support for privatization A/B requests.


<span id="ios：v5-0-0"></span>
### iOS：v5.0.0


* Optimized ABTestConfigValueForKey interface defaultValue problem.
