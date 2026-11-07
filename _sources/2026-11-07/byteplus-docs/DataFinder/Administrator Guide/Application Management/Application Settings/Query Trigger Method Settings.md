---
title: "Query Trigger Method Settings"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Query_Trigger_Method_Settings"
---

<span id="_1-概述"></span>
# 1. Overview

In the face of different business scenarios and different data volumes, the flexible setting of data query methods (automatic query & manual query) can help us reduce operations, avoid interference, and reduce system pressure.

For example, when the amount of data is not large and the indicators are not complex, we hope that the data indicators can automatically initiate queries in real time, produce results quickly, and do not need to perform manual operations every time, reducing the number of operation steps; when facing complex data indicators, we usually hope that after the data indicators we want to query are completely set, we can start to initiate queries to avoid operational interference; at the same time, when the amount of data queried is too large, automatically initiating queries will keep the system in a query state, and the pressure is too high. Manual queries may be more appropriate.

<span id="_2-入口及设置"></span>
# 2. Entrance and Settings


* Entrance location: Click the top navigation bar to enter the application settings, and you can view and set the query trigger method.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/678f1ad2cd9c40999ededc6364495532~tplv-goo7wpa0wc-image.image) </span>

* "Automatically initiate a query" is turned off by default. When it is turned off, in the analysis function, the "query" button can be seen, and you need to manually click to initiate a query each time. Take event analysis as an example, as shown below:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8e0c828cc14a4230b06e3187182e6995~tplv-goo7wpa0wc-image.image) </span>

* When clicking to open "Automatically initiate a query", in the analysis function, the "query" button disappears and is invisible, and each indicator change will initiate an automatic query in real time. Take event analysis as an example, as shown below:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/16f79ab23a184b5788d912667874888e~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/225c7ad79b20458db2e15c8f828c6b91~tplv-goo7wpa0wc-image.image) </span>


<span id="_3-设置后生效功能"></span>
# 3. Effective function after setting

Query Trigger Settings This configuration is currently only effective for advanced analysis functions other than attribution analysis, path analysis, and business object analysis, and all basic analysis functions are not effective.


|**Function** |**Whether it takes effect** |
|---|---|
|Event Analysis |✅ |
|Custom Retention |✅ |
|Funnel Analysis |✅ |
|Distribution Analysis |✅ |
|User Composition |✅ |
|User Path |❌ |
|Attribution Analysis |❌ |
|User Lifecycle |✅ |
|Heat Map Analysis |✅ |
|LTV Analysis |✅ |
|Item Analysis |❌ |
|Custom SQL Query |✅ |
|Fundamental Analysis Full Features |❌ |
