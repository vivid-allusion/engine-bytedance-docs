---
title: "Project Management"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Project_Management__"
---

The SaaS\-cloud native version has the concept of a project, and can perform operations such as application access and user rights management in the project. This article provides you with the main operational guidance for SaaS\-cloud native version of project management.

<span id="11ea09d7"></span>
# Overview

The SaaS\-cloud native version of DataFinder uses the default group of the main account by default, and there is no need to perform group setting related operations in the product console. The concept of adding a **project** can be used to isolate applications, user roles, etc. through the project. Some of the operations of project management are similar to the application management operations of the SaaS version, and will not be repeated here. This article mainly introduces some specific operating instructions for SaaS\-cloud native.

<span id="4fd6e7b2"></span>
# Project details and application list

You can view the basic information of the current project and the list of connected applications on the project details page, and click the corresponding application to view the access information of the corresponding application, such as application ID, APP Key, etc.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d5a03ceacf2946cb9e08f5fbe266183f~tplv-goo7wpa0wc-image.image) </span>

<span id="f5be151f"></span>
# General settings

You can start the project's general settings on the general settings page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cb1ced2db2b9430cb4c9c79046cde9db~tplv-goo7wpa0wc-image.image) </span>


* Query settings

   
   |**Parameter** |**Parameter description** |
   |---|---|
   |Reptile recognition |You can configure the recognition rules of the crawler and the processing method after recognition on the web\-side data. Details can be seen [General Settings: Web Crawler Recognition](https://docs.byteplus.com/docs/DataFinder/General_Settings_Web_Crawler_Recognition). |
   |Query trigger method |Configure the query triggering method when querying the data to be analyzed when using the analysis tool for data analytics, which takes effect for advanced analysis functions other than attribution analysis, path analysis, and business object analysis.<br><br>See configuration details [Query Trigger Method Settings](https://docs.byteplus.com/docs/DataFinder/Query_Trigger_Method_Settings). |
   |Internet Protocol Addresses Only Resolved Not Stored |When configuring analysis, whether it is necessary to keep the original data source of Internet Protocol Address data, after opening, the system only stores the location information after IP resolution, discards Internet Protocol Address data, and hides related attributes. |
   |Multi\-time zone configuration |Multi\-time zone query is only effective for analysis functions, Dashboard, clustering, and basic analysis; the data results of user scrutiny and user labels are consistent with the application time zone. |
   

   In SaaS\-cloud hosting and privatization environments, the query settings for common settings also support resource\-related settings. The parameter configuration instructions are as follows.

   
   |**Parameter** |**Parameter description** |
   |---|---|
   |Query mode |* Accuracy first: sacrificing a certain amount of query efficiency to ensure the accuracy of the data.<br><br>* Speed first: sacrificing a certain amount of data accuracy to ensure query efficiency.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After the opening speed is given priority, the query will make use of the cache as much as possible, but it will affect the consistency of the data, especially in the case of real\-time data and frequent historical data. It is recommended to open the environment where the accuracy of real\-time data is not high and there is no frequent historical data.</div><br><br><br><div data-tips="true" data-tips-type="tip">Data inaccuracies may occur.</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Report of historical data (in the past 7 days)</div><br><br><br>* <div data-tips="true" data-tips-type="tip">real\-time data</div><br> |
   |Resource load balancing |After opening, the utilization of resources will be more balanced. However, when the main and standby delays are high, the accuracy of the data will be affected. It is recommended to open it when the amount of data is large and the requirements for data accuracy are not high. |
   |The limited viewership of query tasks |Turn on the limit viewership of the query task switch, you can customize the limit viewership of conditions, after the configuration is completed, when the subsequent query task meets the limit viewership of the configuration, the query task will limit the number of concurrent queries. |
   

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
