---
title: "Statistical Criteria"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Statistical_Criteria"
---

This function is also known as **Calculation criteria** and **statistical caliber**, which all refer to the same funciton. Usually, when we use advanced analysis for data analytics, the growth analysis (DataFinder) will default to the **user** as the object of statistical analysis, and use the SSID as the user's unique identification ID to calculate the indicator. In addition, growth analysis also provides the ability to switch statistical criteria to meet the scenario of counting user behavior data according to criteria other than the user SSID, and then performing user analysis. This article introduces you to the management operation of statistical criteria.

<span id="_1-概念介绍"></span>
# Background information

In different growth analysis scenarios, different data statistical criteria may be required for data analytics. Here are some example scenarios.


|Industry |Common analysis objects/statistical criteria |Statistical criteria description |
|---|---|---|
|New retail |Equipment |When we want to understand the current usage of new retail industry apps on different devices, we will want to analyze the device as a statistical criteria, rather than statistically analyzing the individual users logged in on the device, but sometimes a device will log in to multiple users, we will want to analyze the device as a statistical criteria to understand the current usage of the device. |
|SaaS |Clue |The sales process will establish a lead conversion funnel, and the main body of the lead funnel is the lead rather than the person who operates the lead. |
|SaaS |Customer |In the SaaS industry, when analyzing customer health, it is necessary to analyze all accounts of the customer company as a statistical metric. |
|Game |Role |In games, a user often creates multiple characters and wants to analyze each character rather than the user. |
|Securities |Capital account |Investors will have funds after opening an account at a brokerage firm. No matter which device they log in to or what login name they use, they can find transactions conducted by the natural person through the funds account. |


DataFinder provides you with management operations for global statistical criteria, including adding statistical criteria and setting default statistical criteria for data analytics. Detailed instructions for operation can be found below.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">DataFinder for your default statistical criteria for the user ssid, when your analysis object for the user, it is recommended to keep the default statistical criteria ssid, DataFinder can ID_Mapping the user's device_id/web_id, user_unique_id, etc. mapping, try to restore a real user through a ssid individual , see details <a href="https://docs.byteplus.com/docs/DataFinder/Supported_User_Unique_Identifiers">Supported User Unique Identifiers</a>.</div>


<span id="305aec30"></span>
# Precautions

When creating new statistical criteria, you need to select an **event property**or **business dimension** as the new statistical criteria:


* **Supported event properties/business dimension requirements** :

   * Only **event properties** of type `string`and `int`can be configured as statistical criteria.

   * When selecting a **business object** as a statistical criteria, only the name of the business object can be selected, and its properties cannot be further selected.

* **Supported analysis metrics** : When the statistical criteria is switched for data analytics, the supported analysis metrics are events associated with criteria event properties/business dimensions.

   
   |Event Properties as Statistical criteria |Business dimension as a statistical criteria |
   |---|---|
   |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/09127b4d1dc14a5bb85c60ac55015e57~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/15b3970860c24fef853304ac6497e159~tplv-goo7wpa0wc-image.image) </span> |
   

* **Statistical criteria UV operator** : After switching the statistical criteria, the value calculated by the UV operator of the subsequent statistical criteria is the value of the criteria property deduplicated, and it is no longer the user UV value of the conventional user criteria.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bd2c44d253cb414991f0478ddec49954~tplv-goo7wpa0wc-image.image) </span>


<span id="_2-快速上手"></span>
# Operation steps

<span id="22bbb970"></span>
## New statistical criteria

After entering the statistical criteria management page, click `New statistical criteria`in the upper right corner to create statistical criteria.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If you encounter a situation where the "New Statistical criteria" cannot be clicked, please confirm whether you have permission first (you need to open the manageable permission of this page).</div>


* <div data-tips="true" data-tips-type="tip">An application can create up to 10 statistical criteria.</div>


* <div data-tips="true" data-tips-type="tip">Statistical criteria that have been created can only be deleted, or the <code>unit</code>name modified, not the event properties.</div>



<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/350786ffabe1400489c37c44c243802f~tplv-goo7wpa0wc-image.image) </span>


|Parameter |Configuration instructions |
|---|---|
|Event properties |* Currently, only event properties and business objects with data types of `string`and `int`can be configured as statistical criteria, so not all event properties can be seen in the drop\-down menu where event properties are selected.<br><br>* When selecting a business object as a statistical criteria, only the name of the business object can be selected, and its properties cannot be further selected. |
|Unit |`Units`are used to assist in the description of indicators during analysis, with a maximum length of 4 characters. |
|Scope of application |Select the application range of the created criteria.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">At present, only SaaS\-cloud\-native environments support applying multi\-criteria to "user grouping".</div><br><br><br>* <div data-tips="true" data-tips-type="warning">After using multi\-criteria for grouping, currently only event analysis, retention analysis, and conversion analysis support saving query results as user grouping.</div><br><br><br>   <div data-tips="true" data-tips-type="warning"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cf9984f152594eb8a2a046a3a660f672~tplv-goo7wpa0wc-image.image" />   </div><br>    |


<span id="ea8354f0"></span>
## Set default statistical criteria

After entering the statistical criteria management page, click `Set Default Values`in the upper right corner to set the default statistical criteria for subsequent data analytics.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8e43753753af4e0d8a1e776fb1bbdff7~tplv-goo7wpa0wc-image.image) </span>

After the setting is completed, in the statistical criteria list, the "default" logo will appear after the corresponding statistical criteria.

<span id="_3-功能使用"></span>
# Use statistical criteria

Here is an example to show you how to use the statistical criteria. For example, a new channel (app_channel) statistical criteria has been created in the statistical criteria, and the application scope of this criteria is "analysis tool" and "user grouping".

<span id="38867668"></span>
## Cluster circle selection based on multi\-criteria

When creating a grouping, you can toggle the statistical criteria when setting the grouping circle selection.

<span id="136f4f84"></span>
## Multi\-aperture based data analytics

When using the analysis tool for growth analysis, you can view the current default statistical criteria at the top of the configuration area of the analysis tool, or you can manually modify the statistical criteria in the drop\-down menu.


1. In the case of event analysis, you can toggle the statistical criteria to the newly created channel criteria at the top.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Due to the different events associated with different statistical criteria, switching the statistical criteria will clear the selected events.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac0dc7a527ba416aa1ef874f67fa6af6~tplv-goo7wpa0wc-image.image) </span>

   * After switching the criteria, when you configure the indicator, select the indicator in the drop\-down box to associate the event for the **channel** property.

   * In the indicator operator, all the data related to **UV** are the values of the **channel** property criteria deduplicate.

   * When configuring subdivision filtering or grouping, filtering or grouping can be performed based on the subgroups of the above channel property criteria.

2. In the query chart of an analysis tool, operations such as exporting data or storing it as a cluster are usually supported. If you switch the statistical criteria, operations such as viewing samples may not be supported.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Currently, only event analysis, retention analysis, and conversion analysis in SaaS\-cloud native environments support storing query results as clusters.   </div>
   

<span id="_4-支持范围"></span>
# Scope of support


|Advanced Analytical Model |Multi\-aperture analysis |
|---|---|
|Event analysis |✔️In a SaaS\-cloud native environment, query results can be stored as a cluster |
|Retention analysis |✔️In a SaaS\-cloud native environment, query results can be stored as a cluster |
|Conversion analysis |✔️In a SaaS\-cloud native environment, query results can be stored as a cluster |
|Distribution analysis |✔️ |
|Component analysis |✔️ |
|User path |✔️ |
|Attribution analysis |Does not involve |
|User lifecycle |❌ It is not supported for the time being, so stay tuned. |
|Heat map analysis |❌ It is not supported for the time being, so stay tuned. |
|LTV analysis |❌ It is not supported for the time being, so stay tuned. |
|Business Object Analysis |❌ It is not supported for the time being, so stay tuned. |
