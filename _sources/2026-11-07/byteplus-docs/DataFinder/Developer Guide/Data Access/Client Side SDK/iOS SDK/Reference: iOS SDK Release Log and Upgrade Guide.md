---
title: "Reference: iOS SDK Release Log and Upgrade Guide"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Reference_iOS_SDK_Release_Log_and_Upgrade_Guide"
---

<span id="85f7573b"></span>
# SDK Release Log

<span id="2317b69d"></span>
## June 25, 2026

<span id="2080f1d8"></span>
### iOS: V6.17.11


1. Fix and magic policy SDK click event failure problem under RXCocoa (switch: config.autoTrackDelegateProxyForwardingEnabled)


<span id="e459a0df"></span>
## April 24, 2026

<span id="89ef5ae9"></span>
### iOS: V6.17.10


1. OpenUdid hardcoding keyword removal

2. Profile setting filter optimization


<span id="ac3848b1"></span>
## December 4, 2025

<span id="170b1431"></span>
### iOS: V6.17.7\-iOS26


1. Repair iOS26 0x400000000000bad0

2. H5 gets through to update the uuid to do a good job of data verification protection to avoid SDK errors caused by incoming numbers, and only receives null and string.


<span id="8438a19f"></span>
## October 11, 2025

<span id="a945a093"></span>
### iOS: V6.17.6


1. Optimize internal packaging logic

2. Event custom attributes are limited to 50k size. Custom attributes over 50k will be discarded and carry exception description information

3. Full event tracking custom parameters do not support passing preset properties


<span id="08f3ae90"></span>
## August 8, 2025

<span id="43f62512"></span>
### iOS: V6.17.5


1. Optimize ssid judgment logic


<span id="5bc344a7"></span>
## July 4, 2025

<span id="7a0177d8"></span>
### iOS: V6.17.4


1. AppId supports safe mode

2. Added a large\-volume event blocking reporting logic optimization switch, which is turned off by default and can be selected to be turned on.


<span id="e489fb4d"></span>
## March 31, 2025

<span id="bf384ae1"></span>
### iOS: V6.17.3


1. iOS Devtools supports network capture

2. Preset event support cloud control blacklist

3. AB exposure frequency control

4. Tracer duplex plugin adds failure retry logic


<span id="d87349c3"></span>
## February 28, 2025

<span id="8527f340"></span>
### iOS: V6.17.2


1. Added response to close encryption switch

2. When the Web SDK is connected, disable the SDK uuid or uuidType on the Web SDK update side when supported.

3. Web SDK supports multi\-caliber when connected

4. Fix the Crash problem caused by the wild pointer occasionally when the user pulls the AB experimental configuration


<span id="4648a131"></span>
## November 13, 2024

<span id="adb7fa6f"></span>
### iOS: V6.17.0


1. Compatible with the presence of illegal fields when users set UserID, resulting in SDK Crash scenarios

2. Fix thread deadlock caused by occasional cold start real\-time event tracking detection


<span id="d30be980"></span>
## September 9, 2024

<span id="753f7536"></span>
### iOS: V6.16.9


1. iOS 18 adaptation

2. Split sub\-library Game, support game mode and game interface separate access


<span id="74c702ff"></span>
## June 28, 2024

<span id="401f8ae4"></span>
### iOS: V6.16.8


1. Added block function to support custom HTTPHeaderFields

2. stability optimization

3. Remove custom header persistence


<span id="87768740"></span>
## April 23, 2024

<span id="ee9e9a7f"></span>
### iOS: V6.16.6


1. Support Apple privacy configuration domain name


<span id="e5c3c5ef"></span>
## More historical versions

See the release history for more historical versions [SDK更新日志](https://docs.byteplus.com/docs/undefined/663450cccb273002f1bb4b3b).
