---
title: "Dynamic Variable"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Dynamic-Variable"
---

<span id="c89048e7"></span>
# 1. Overview

When pushing, we often need to introduce user\-specific content, such as user names, cities, and other user properties. At this time, we can use the "dynamic variable" function.

<span id="4d7acce1"></span>
# 2. What properties are supported by dynamic variables?


* The calculation logic is the user property for analyzing the final value, which you can set in the features page. If the existing user properties are not satisfied, you can set them in "Data Management" \- "User Properties" and add them in event tracking; if the user properties you need are not reported with the event, we also provide Open API import method, access method: [User tag OpenAPI](https://www.volcengine.com/docs/6285/1108215).

* At the same time, we also preset a number of public event properties, as follows:



|Property Name |Value |
|---|---|
|loc_province_id |State of Idaho |
|os_version |12.1.4 |
|app_region |China |
|device_model |iphone 6 |
|app_version |0.2.5 |
|os_name |ios |
|loc_city_id |5583739 |
|language |en |
|app_channel |facebook |
|region |China |
|loc_country_id |America |
|platform | |
|network_carrier |verizon |
|brand |apple |


<span id="f5236ed6"></span>
# 3. Use configuration

In push experiments, push messages, and process canvas, you can use dynamic variables.


1. After clicking "Insert Properties", a property selection box will appear in the text box below, where all final value user properties and default supported public event properties can be selected.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b7c3caee88b144bb8ae353519e02e133~tplv-goo7wpa0wc-image.image) </span>

2. When you select a property, you are prompted to set a default value to ensure that messages sent to users are not affected if the property is deleted or the value is empty.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/12c4f295b2354a428da64e908b8365fd~tplv-goo7wpa0wc-image.image) </span>
