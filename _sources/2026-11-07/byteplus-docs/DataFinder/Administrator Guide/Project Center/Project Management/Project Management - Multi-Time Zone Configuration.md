---
title: "Project Management - Multi-Time Zone Configuration"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Project_Management_-_Multi-Time_Zone_Configuration"
---

This function is an advanced function, which is not turned on by default, and does not support closing after opening. If necessary, please contact the customer to successfully activate the function.

<span id="一、概述"></span>
## 1. Overview

For the business of going overseas and collecting multinational users, there are often demands for multi\-time zone inquiries. That is, at the time of analysis, the **calculation results** of the reported data are displayed according to the specified time zone. For example, a global operation headquartered in China wants to view the reported data of users in the Middle East and East Asia simultaneously according to China time. Just configure the display time zone to China time zone.

<span id="二、多时区使用配置"></span>
## 2. Multi\-time zone usage configuration

<span id="_2-1-配置时区"></span>
### 2.1 Configure the optional time zone of the application

The default is that the project/application has been configured with a time zone (UTC + 8 in the domestic environment), that is, all data results are displayed according to UTC + 8. You can configure optional time zones within the app in **Project Center** \> **General Settings**.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4f875573fc5f4ea9a7161850fa95242f~tplv-goo7wpa0wc-image.image) </span>


* After clicking the **Edit** button in the upper right corner, in the multi\-time zone configuration area, you can add "target time zone", and click **Confirm** after completing the configuration.

* Multi\-time zone query is only effective for analysis functions, Dashboard, clustering, and basic analysis; the data results of user scrutiny and user labels are consistent with the application time zone.


<span id="_2-2数据计算准则"></span>
### 2.2 Data calculation guidelines


|Object |Data reporting time (default domestic utc + 8 & overseas utc + 0) |Query content |Target time zone |Display effect |
|---|---|---|---|---|
|Event |2023\-01\-01 08:00:00 |App launch \- UV 100 |UTC +10 |Time zone offset 2 hours, 2023\-01\-01 06:00, App launch \- UV 100 |
|Event properties |2023\-01\-01 08:00:00 |App launch (ios channel) \- UV 80 |UTC +10 |Time zone offset 2 hours, 2023\-01\-01 06:00, App launch (iOS channel) \- UV 80 |
|User attributes |2023\-01\-01 08:00:00 |App launch (registration time 2022\-12\-01~ 03) \- UV |UTC +10 |If the calculation contains the "datetime user attribute (last value) ", the "datetime user attribute" cannot be converted.<br><br>2023\-01\-01 06:00 App launch\-UV, superimposed user registration time 2022\-12\-01~ 03 (UTC + 08) |


<span id="_2-3-使用范围"></span>
### 2.3 Scope of use


1. Application scope: advanced analysis, fundamental analysis, Dashboard, clustering

2. After selecting a time zone, the following range items are displayed along with the time zone.

   
   |Scope of application |Schematic diagram |
   |---|---|
   |General purpose: analysis period (calendar)<br><br><br>* All conversion calculations are based on the selected time zone conditions. If you modify the target time zone, it will be automatically adjusted. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ee406d1ef73943e4a6f51c8240f78ad9~tplv-goo7wpa0wc-image.image) </span> |
   |General purpose: data results, download data<br><br><br>* The display time is displayed according to the time zone conditions after conversion calculation |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9fc4b584b1a04e7688114df330cfbaa1~tplv-goo7wpa0wc-image.image) </span> |
   |General: Time\-class data<br><br><br>* The display time is displayed according to the time zone conditions after conversion calculation | |
   |Dashboard: Each Dashboard board supports configuring time zones<br><br><br>* Filter time: The display time is displayed according to the time zone conditions after the conversion calculation<br><br>* Chart: Time zones can be applied to all charts under Dashboard, drill down to Advanced Analysis to display the chart's "original" time zone |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/55d812e942a04b01a1e5f0c3662fb60e~tplv-goo7wpa0wc-image.image) </span> |
   |Dashboard \- Subscription and Monitoring: Push Time Support Configuration Time Zone<br><br><br>* The default is consistent with the Dashboard time zone. The subscription push time is pushed according to the set time zone. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ed34de30e7a84123b028778e695d0e90~tplv-goo7wpa0wc-image.image) </span> |
   |User segmentation:<br><br><br>* The calculation conditions support different time zones, and the calculation results are based on the configured time zone<br><br>* (Growth Analysis) Update/Calculation time displayed at UTC + 08 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/90abe1597839408abda44c3085c50815~tplv-goo7wpa0wc-image.image) </span> |
