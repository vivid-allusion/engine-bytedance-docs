---
title: "Web/JavaScript SDK Release Log and Upgrade Guide"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Web_JavaScript_SDK_Release_Log_and_Upgrade_Guide"
---

<span id="1270f3e2"></span>
# Upgrade operation points

When upgrading the Web SDK, you need to modify the version number of the introduced SDK to the new version number.

<span id="ac7c30c7"></span>
# Publish log

<span id="82235596"></span>
## December 16, 2025

<span id="4c6f049e"></span>
### Web: V5.2.11


1. Added Allow setting invalid values when setting public parameters


```HTML
window.collectEvent('init', {
  enable_invalid_config: true
})
```



2. Full event tracking supports page capture

3. The npm package supports event tracking real\-time verification and devtools


<span id="39c18ee9"></span>
## September 30, 2025

<span id="f55ca0ff"></span>
### Web: V5.2.10


1. Support flutter and H5 connection

2. Support Android, ios, Hongmeng to get did and more experimental results when getting through, please refer to the opening article for details

3. Support setting full event tracking to collect parent element attributes, refer to the full event tracking article for details

4. Optimized some problems


<span id="9aab16b7"></span>
## July 14, 2025

<span id="403db3d6"></span>
### Web: V5.2.9


1. Heat map can also be displayed after turning off full event tracking

2. APPID supports encrypted transmission


<span id="d9e37963"></span>
## June 6, 2025

<span id="735ab5ff"></span>
### Web: V5.2.8


1. After user_uniqueid_id_type is set, persistent storage is performed

2. By default, devtools' own event tracking collection is turned off, which can be configured to be turned on.

3. The devtools button can be dragged and dropped.


<span id="865b6c96"></span>
## May 7, 2025

<span id="adddb2c7"></span>
### Web: V5.2.7


1. Support collection of SDK internal monitoring data


<span id="6549650e"></span>
## April 3, 2025

<span id="95394d72"></span>
### V5.2.6


1. Supports retry mechanism after failed Tracer ID binding.

2. Support collecting system type and system version number in Hongmeng system in H5. The collected Hongmeng system name is OpenHarmony, and the version number is x.x.x.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b45d61c55bc444408f05410c934e7aa2~tplv-goo7wpa0wc-image.image) </span>


3. Support collecting UTM information after URL #.

4. Supports a retry mechanism after data reporting fails.


<span id="b5b4e874"></span>
## March 14, 2025

<span id="feef7cf1"></span>
### Web: V5.2.5


1. Support dynamic recognition of protocol settings for loading three\-party js


<span id="6772ed01"></span>
## February 28, 2025

<span id="138330c8"></span>
### Web: V5.2.4


1. Support setting the protocol for loading three\-party js to http or https.

2. Optimized some problems


<span id="d8a20f31"></span>
## February 12, 2025

<span id="e803feeb"></span>
### Web: V5.2.3


1. Increase data reporting compression


<span id="8edcbb6e"></span>
## November 28, 2024

<span id="7dca17d2"></span>
### Web: V5.2.2


1. Add tracerid binding failed retry

2. Optimize the logic of blacklisting under logSetting

3. Optimized the use of multiple instances


<span id="4cddcfe3"></span>
## October 23, 2024

<span id="0f3f96ad"></span>
### Web: V5.2.1


1. Added a origin_referrer and origin_referrer_host to the header custom to record the original refer, which defaults to document.referrers.


<span id="cf34dc97"></span>
## September 5, 2024

<span id="c93b35d5"></span>
### Web: V5.2.0

Update content:


1. Web DevTools has released version 2.0 with updated UI and optimized functionality.

2. Supports bindToken and Tracer dual\-sending logic.

3. Added custom requestToken.

4. Added failed local data store, enabled by enable_storage.


<span id="dae821b4"></span>
## June 12, 2024

<span id="f421fef2"></span>
### Web: V5.1.12


1. Optimized the stop/reStart APIs by adding logic to re\-expose elements within the visual area when calling reStart.

2. Fixed the tracerdata information report of utm.


<span id="53ec02ea"></span>
## May 17, 2024

<span id="e9614b7c"></span>
### Web: V5.1.11


1. Fixed the problem of abnormal exposure type of page elements.

2. Report $user_unique_id_type in profile user properties when setting user_unique_id_type is removed.

3. The attributes attribute has been added to the exposure settings, which can be set to not listen when the element attributes change, and the default is true.


<span id="fcfe7765"></span>
## April 18, 2024

<span id="ca264e42"></span>
### Web: V5.1.10.feature


1. Fixed an issue where the exposure type of page elements was abnormal after returning from other pages in the open scene.


<span id="a4378fd9"></span>
### Web: V5.1.10


1. AB test added full exposure option


<span id="8a4c548a"></span>
### Web: V5.1.9 feature


1. Fixed an issue that could affect vue pushstate when using the exposure function


<span id="e53f8cc3"></span>
## January 17, 2024

<span id="52f50c03"></span>
### Web: V5.1.9


1. After optimizing the webid request exception, cache the data of the abnormal webid

2. Slide event tracking supports dynamically added elements

3. Added custom properties for full event tracking


<span id="6d4b8f31"></span>
## November 29, 2023

<span id="0a71a20c"></span>
### Web: V5.1.8


1. Optimized the referring information of single page application PV

2. Optimized the information reported by the hash route

3. Support configuring mask layer transparency for multi\-link or visual experiments

4. Added the configuration delivery of logsettings

    &nbsp;


<span id="november-16-2023"></span>
## November 16, 2023

<span id="9836bddd"></span>
### Web: V5.1.7


1. Optimized the reporting of exposure event tracking

2. Added reporting of sliding event tracking

3. Fix the problem that the setting properties do not take effect after the embedded H5 and the client side are connected

4. The event tracking debugging tool removes the restriction of url parameters, just open enable_debug


<span id="493a608c"></span>
### Web: V5.1.6


1. Support national secret algorithm encryption and reporting

2. Optimized some functions


<span id="2d7190d7"></span>
## February 28, 2023

<span id="86970e28"></span>
### Web: V5.1.5


1. Support for anonymous ID settings

2. Optimize the stay duration under IOS and report when leaving


<span id="9923d52f"></span>
### November 18, 2022

<span id="aa64c45f"></span>
### web: V5.1.4


1. Added event tracking debugging tool;

2. The client side supports AB API calls

3. Added disable_ab_rest parameter to disable AB reset when switching uuids


<span id="ee3fa828"></span>
## October 18, 2022

<span id="b98285dc"></span>
### web: V5.1.3


1. Added hash routing monitoring;

2. Support AB multi\-link experiment fallback;

3. Support AB cross\-domain name storage data;

4. The client side connection parameter was changed from Native to enable_native;


<span id="bd16a1af"></span>
## July 20, 2022

<span id="6992c86f"></span>
### web: V5.1.2


* Added event tracking verification function of H5 page;


<span id="7cd68e00"></span>
## June 2, 2022

<span id="20baa444"></span>
### web: V5.1.1


* Added exposure event capture;

* Added tracking event collection.

* Added event & attribute legitimacy verification;

* Added user_unique_id_type attributes;

* Added full event tracking event single event switch.
