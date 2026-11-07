---
title: "SDK Changelog"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/SDK-Changelog"
---

Update logs for 2023 and beyond can be found on the [SDK Release Log ](https://www.volcengine.com/docs/6285/69616)page.

<span id="_2022年12月21日"></span>
## December 21, 2022

<span id="android-v6-14-2"></span>
### Android: V6.14.2


1. Support RN circle selection;

2. Support user multi\-caliber binding OneID;

3. Extended event tracking API to support event\-level A/B Testing exposure settings;

4. Embedded H5 ABTest shunt connection;

5. Report policy adjustment: report once by default in the background (and manually call flush to share 10s frequency control);

6. Support commercial IPID requirements.

7. Fix known issues.


<span id="ios-v6-14-1"></span>
### iOS: V6.14.1


1. Support user multi\-caliber binding OneID;

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


<span id="_2022年11月18日"></span>
## November 18, 2022

<span id="web-v5-1-4"></span>
### Web: V5.1.4


1. Added event tracking debugging tool;

2. The client side supports AB API calls

3. Added disable_ab_rest parameter to disable AB reset when switching uuids


<span id="_2022年10月18日"></span>
## October 18, 2022

<span id="web-v5-1-3"></span>
### Web: V5.1.3


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
