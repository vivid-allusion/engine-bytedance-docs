---
title: "Reference: Android SDK Release Log and Upgrade Guide"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Reference_Android_SDK_Release_Log_and_Upgrade_Guide"
---

<span id="d11d4a9b"></span>
## June 29, 2026

<span id="c689a038"></span>
### Android: V6.17.11


1. Android 4.2 version compatibility optimization


<span id="e1f8b2b8"></span>
## April 24, 2026

<span id="d36ef42e"></span>
### Android: V6.17.10


1. Profile setting filter optimization


<span id="20d22640"></span>
## March 12, 2026

<span id="4c79fa30"></span>
### Android: V6.17.7


1. Optimize event tracking validation Page display logic


<span id="fd2ae69e"></span>
## October 11, 2025

<span id="87671c4e"></span>
### Android: V6.17.6


1. Optimize internal packaging logic

2. Remove iccid acquisition

3. Event custom attributes are limited to 50k size. Custom attributes over 50k will be discarded and carry exception description information

4. Full event tracking custom parameters do not support passing preset properties


<span id="8428ef06"></span>
## August 8, 2025

<span id="3e7598ad"></span>
### Android: V6.17.5


1. Optimize the page to enter the reporting opportunity

2. Optimize fragment filtering logic

3. Optimize ssid judgment logic


<span id="0c971c7d"></span>
## July 4, 2025

<span id="067b54cb"></span>
### Android: V6.17.4


1. Android 15 16k so compatible

2. Remove mnc_mcc collection

3. AppId supports safe mode

4. Crash event stack information should not exceed 2000 characters


<span id="fddc5c75"></span>
## March 31, 2025

<span id="6dfe5068"></span>
### Android: V6.17.1


1. Preset events support cloud\-controlled blacklist filtering

2. AB exposure event support whether to generate switch repeatedly

3. Devtools support shows if plugins are integrated

4. Plugin removal imei/operator information logic adjustment


<span id="a848fe82"></span>
## February 28, 2025

<span id="42b4b4db"></span>
### Android: V6.17.0


1. Added response to close encryption switch

2. Support disabling SDK uuid or uuidType on the web SDK update side when the web SDK is connected.

3. Web SDK supports multi\-caliber when connected

4. sim_region subject to operator switch control

5. External API part tag is deprecated


<span id="c902f5a1"></span>
### September 26, 2024

<span id="4cd836ef"></span>
### Android: V6.16.11


1. Support custom Oaid

2. Fix profile concurrent calls


<span id="bb0ce0d7"></span>
## August 31, 2024

<span id="556de3b4"></span>
### Android: V6.16.10


1. Support 360 Oaid acquisition

2. Support duration event custom event name

3. app_region acquisition logic aligned with iOS

4. Adjust event custom property validation prompt logic


<span id="e509eeaf"></span>
## July 10, 2024

<span id="a5064fc9"></span>
### Android: V6.16.9


1. Support request to add dynamic headers

2. Adjust the event range of the corresponding version information when the event is added

3. Event tracking validation/circling request shortening request timed out event

4. Fix some known issues


<span id="117cd336"></span>
## April 9, 2024

<span id="0bc3146a"></span>
### Android: V6.16.6


1. OAID compatible with Honor's new system


<span id="5b07bfa7"></span>
## March 5, 2024

<span id="8fdbd414"></span>
### Android: V6.16.4


1. Circle selection/real\-time event tracking verification Support multiple set\-cookies parsing


<span id="b2dad06b"></span>
## January 2, 2024

<span id="c2749b24"></span>
### Android: V6.16.3


1. Support Android Gradle Plugin version 8

2. HTTPS request support setting up SSLSocketFactory

3. Clipboard access code support plugin removal


<span id="72626863"></span>
## September 11, 2023

<span id="9adba291"></span>
### Android: V6.15.5


1. The local data cache is adjusted to 30 days (the server level only receives historical data within 7 days by default. If you need to report the local cached data within the range of 7 days, please contact the operation and maintenance to adjust the server level settings synchronously)

2. Version model information when event addition is generated

3. Add WebView loop

4. Optimized some functions


<span id="2246da2f"></span>
## July 18, 2023

<span id="2fb1682f"></span>
### Android: V6.15.4


1. ALink DDL Added Failed Callback

2. Optimized some functions


<span id="91a75366"></span>
## May 29, 2023

<span id="183be96d"></span>
### Android: V6.15.2


1. Compliance transformation

2. Exposure event detection strategy support toggle

3. Adapt to Tinker plugin

4. Supports some header field filtering

5. Optimized some functions


<span id="e7e4c6fb"></span>
## March 31, 2023

<span id="ac68bfcf"></span>
### Android: V6.15.0


1. Privatized cloud control configuration is issued

2. Privatization supports custom encryption and provides national secret encryption plugins

3. Batch report plan adjustment

4. Support AB response encryption

5. Optimized some functions


<span id="ccad3489"></span>
## February 14, 2023

<span id="ed86db8e"></span>
### Android: V6.14.3


1. Huawei mobile operating system recognizes harmony os

2. Full event tracking switch Plugin

3. Add IccId switch

4. Removing support dependencies

5. Adjust the monitoring switch rules for domestic SAAS users and complete the first\-phase monitoring link


<span id="e7d5cc98"></span>
## December 21, 2022

<span id="ccc23d2c"></span>
### Android: V6.14.2


1. Support RN loop selection

2. Support user multi\-caliber binding OneID

3. Extended event tracking API to support event\-level A/B Testing exposure settings

4. Embedded H5 ABTest shunt connection

5. Report policy adjustment: report once by default in the background (and manually call flush to share 10s frequency control)

6. Support commercial IPID requirements

7. Fix known issues


<span id="cf2977c2"></span>
## October 14, 2022

<span id="4ee719f9"></span>
### Android: V6.13.3


1. Added application crash event collection

2. Added disable event configuration

3. Added capture Google AID configuration switch

4. Added Get Multi\-Instance Interface

5. Added pull AB test configuration interface to set timeouts and callbacks

6. Real\-time event tracking verification Added page access event verification

7. Support setting user uuid before SDK initialization

8. Fragment full event tracking

9. Fix known issues


<span id="69d96942"></span>
## September 5, 2022

<span id="9bfe3f3d"></span>
### Android: V6.12.0


1. Add multiple instances to configure debugging log switches and custom printing separately

2. Added support for debugging tools

3. Fix known issues


<span id="ef3310ee"></span>
## July 14, 2022

<span id="ba98037c"></span>
### Android: V6.11.0


1. Added support for configuring full event tracking event types

2. Added validation log hints for event names and properties

3. Fix known issues


<span id="2f58411e"></span>
## historical version

Can be seen [SDK Update Log](https://docs.byteplus.com/docs/DataFinder/SDK_Update_Log).
