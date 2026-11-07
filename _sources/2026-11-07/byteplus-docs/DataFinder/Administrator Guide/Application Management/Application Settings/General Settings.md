---
title: "General Settings"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/General_Settings"
---

You can set the project's data query, Dashboard chart and other functions in the **general settings** page of application management. After the setting is completed, all analysis tools in the project are queried and analyzed according to the setting results. This article provides you with configuration details for common settings.

<span id="7354c092"></span>
# Usage restrictions

Accounts with only administrative privileges can operate common settings for project management.

<span id="d07129f2"></span>
# General settings

<span id="9c8fbaea"></span>
## Operation entrance

After logging in to the DataFinder console, click on the top navigation bar **Application Management** \> **Application Settings** \> **General Settings** to enter the General Settings page to start the general settings of the project.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/76e3618488014c65880c4633219c44c5~tplv-goo7wpa0wc-image.image) </span>


* Query settings

   
   |**Parameter** |**Parameter description** |
   |---|---|
   |Web crawler recognition |You can configure the recognition rules of the crawler and the processing method after recognition on the web\-side data. Details can be seen [General Settings - Crawler Data Filtering](https://docs.byteplus.com/docs/DataFinder/General_Settings_-_Crawler_Data_Filtering). |
   |Query trigger method |Configure the query triggering method when querying the data to be analyzed when using the analysis tool for data analytics, which takes effect for advanced analysis functions other than attribution analysis, path analysis, and business object analysis.<br><br>See configuration details [Query Trigger Method Settings](https://docs.byteplus.com/docs/DataFinder/Query_Trigger_Method_Settings). |
   |Internet Protocol Addresses Only Resolved Not Stored |When configuring analysis, whether it is necessary to keep the original data source of Internet Protocol Address data, after opening, the system only stores the location information after IP resolution, discards Internet Protocol Address data, and hides related attributes. |
   |Multi\-time zone configuration |Multi\-time zone query is only effective for analysis functions, Dashboard, clustering, and basic analysis; the data results of user scrutiny and user labels are consistent with the application time zone. |
   

* Dashboard and chart settings

   
   |**Parameter** |**Parameter description** |
   |---|---|
   |Color Configuration |Color control is carried out for the same\-ring ratio of the indicator and the ability of data VS; if it is not turned on, it is "green up, red down", and if it is turned on, it is "red up, green down". This function is a global impact function. |
   |Dashboard Chinese and English configuration |After opening, support entering Chinese & English Dashboard names, chart names, folder names. After closing, the history dashboard still retains the Chinese/English switching logic. (At present, this function only supports use in the new version of Dashboard editing state. If you need to configure, please upgrade Dashboard to the latest version) |
   |Dashboard supports embedding external charts |Configure whether other Dashboard can be embedded in the Finder's Dashboard. After turning on the switch, you can add the chart/Dashboard under the volcano domain name to the "current Dashboard". |
   

* Event tracking settings

   
   |**Parameter** |**Parameter description** |
   |---|---|
   |Event tracking check |Configure whether to manually accept event tracking events and event properties. After opening, events and properties need to be manually accepted before warehousing. |
   |Number of common events |Configure the maximum number of meta events, event properties, user properties, and event properties. |
   

* Session playback settings

   
   |**Parameter** |**Parameter description** |
   |---|---|
   |Cloud control configuration |Whether to enable cloud control, after opening, the configuration will be issued through cloud control, otherwise the SDK local configuration will be used. |
   |Basic configuration |Session playback data acquisition switch for a key to open and close the session playback data acquisition. After closing, the collection will be closed at the next SDK cold start, please use caution. |
   |Sample Rate Configuration |The number of collections used to configure the data. For cost reasons, if you want to reduce the amount of data collection for session playback, you can set the sample rate limit to capture all by default. |
   |Desensitization configuration |Configure the desensitization mode of session playback data, support **full desensitization** and **standard mode**.<br><br><br>* Standard mode: The sensitive information automatically discovered by the system and the sensitive information configured on the SDK side will be reported after being desensitized in the form of \*\*\*.<br><br>* Full desensitization mode: All resources such as text and pictures will be reported after being desensitized. |
   |Activate recording mechanism<br><br>(Web only) |* Set the range of collected data, support **full acquisition** and **partial acquisition**.<br><br>* When selecting **partial collection**:<br><br>   * You need to specify the URL of the collection page whitelist or blacklist.<br><br>   * Support the identification rules for configuring single page URLs, and configure page identification rules through "=", "include", and "regular matching".<br><br>   * Supports batch configuration page URLs by clicking the Edit button after the configuration box. |
   |Acquisition range<br><br>(Android only) |* Set the range of collected data, support **full acquisition** and **partial acquisition**.<br><br>* When selecting **partial collection**:<br><br>   * You need to specify the activities for collecting page whitelists or blacklists.<br><br>   * Support the identification rules of the configuration single page, and also support batch configuration by clicking the edit button after the configuration box. |
