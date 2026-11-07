---
title: "SDK compliance guide"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/SDK_compliance_guidelines"
---

This topic introduces how to comply when using APMPlus. We address partner concerns and mitigate risks across three areas: collected fields, proper SDK usage, and recommended inspection methods and regulatory summaries.

<span id="0cb7052c"></span>
## Fields collected and permissions requested by APMPlus SDK

First, APMPlus SDK **does not collect personal identity information. It only collects mobile device data to analyze exceptions and performance of apps and devices, helping R&D teams locate and diagnose anomalies**.

For the complete list of collected fields, see [SDK developer compliance specifications](https://docs.byteplus.com/en/docs/apmplus/Compliance_guidelines_for_SDK_developer_usage).

The permissions requested by the APMPlus SDK are as follows:


|**OS** |**Permission** |**When to apply** |**APMPlus usage scenarios** |
|---|---|---|---|
|iOS |Network access mode |Read during initialization |Required when analyzing the device's network status. |
|Android |Read phone status (device IMSI/IMEI number) |Read during initialization |Used to generate a unique device identifier, i.e., Device_ID, for counting the number of devices. |
|Android |Read external storage |Read during initialization |Read saved temporary data |
|Android |Write to external storage |Save during initialization |Save temporary data |


<span id="dbd188d5"></span>
## How to use APMPlus SDK properly


* Ensure your app's privacy policy fully lists all collected fields. For APMPlus's full privacy policy, see [SDK privacy policy](https://docs.byteplus.com/en/docs/apmplus/The_SDK_privacy_policy).

* Only initialize APMPlus SDK after your users agree to the SDK privacy policy.

* The table below describes the data collected by APMPlus SDK and its purposes. For certain fields, we also provide alternative solutions if you prefer not to collect them.

   * iOS client

      
      |**Collected field name** |**Purpose description** |**collection method** |**Alternative solution** |
      |---|---|---|---|
      |Device ID (IDFV) |Used for log stream analysis. Through the device ID, you can view a specific device's exception information stream on APMPlus for troubleshooting. |Obtain IDFV via the system method. The backend uses this field to generate a unique identifier for the device. |See the integration guide for [obtaining device and user count](https://docs.byteplus.com/en/docs/apmplus/Use_advanced_features), and use custom device IDs. |
      |Device model |Used for multi\-dimensional analysis and filtering to view the occurrence of exception issues on different device models. |Obtained via system methods |None |
      |Operating system |Used to distinguish the operating system type (Android/iOS) where the exception occurred. |Fixed field |None |
      |System time zone |Used for exception analysis. It helps analyze exception issues occurring in different time zones. |Obtained via system methods |None |
      |Screen resolution |Used for exception analysis. It helps analyze exception issues that may be caused by screen resolution. |Obtained via system methods |None |
      |Disk usage |Used for exception analysis to determine whether the exception occurred due to insufficient disk space. |Obtained via system methods |None |
      |Memory usage |Used for exception analysis to determine whether an exception occurred due to insufficient memory space. |Obtained via system methods |None |
      |Number of running threads |Used for exception analysis. It helps analyze the operating status of different threads. |Obtained via system methods |None |
      |CPU information |Used for exception analysis. It helps analyze possible compatibility issues with different CPU architectures. |Obtained via system methods |None |
      |Mobile Country Code (MCC) |Used to determine the Internet Service Provider |Obtained via system methods |None |
      |Mobile Network Code (MNC) |Used to determine the Internet Service Provider |Obtained via system methods |None |
      |Application version |Used for multi\-dimensional analysis and filtering to view the occurrence of exception issues across different app versions. |Obtained via system methods |None |
      |Application package name |Used for exception analysis. It helps analyze exception issues across different application packages. |Obtained via system methods |None |
      |Process start time |Used for startup analysis. It helps analyze the time consumption of the app's startup chain. |Obtained via system methods |None |
      |Crash time |Used for log stream analysis. It helps perform exception analysis combined with other app logs. |Obtained via system methods |None |
      |Crash thread name |Used for exception analysis to identify the thread where the exception occurred. |Obtained via system methods |None |
      |Names of visited pages |Used for exception analysis. Reproduce scenarios through the activity page to troubleshoot issues. |Obtained via system methods |Do not include the UItrackers sub\-library when integrating the SDK. |
      |All thread stacks of the current process |Used for exception analysis. It helps analyze the app's operating status when the exception occurred. |Obtained via system methods |None |
      |In\-app language |Used for exception analysis. It helps analyze compatibility issues caused by the system language. |Obtained via system methods |None |
      |App release channel |Used for multi\-dimensional analysis and filtering. It helps analyze exception issues across different channels. |Initialize input information |None |
      |System country/region information |Used for multi\-dimensional analysis and filtering. It helps to analyze the distribution of exception issues across different regions. |Obtained by the server based on the IP address. |None |
      |User ID |Used for log stream analysis. Through the user ID, you can view a specific user's exception information stream on APMPlus for troubleshooting. |Initialize input information |No need to call the method that sets the user ID |
      |Internet Service Provider information |Used for multi\-dimensional analysis and filtering. It helps analyze network issues caused by Internet Service Providers. |Obtained via system methods |None |
      |Network access mode |Used for multi\-dimensional analysis and filtering. It helps analyze issues under different network conditions. |Obtained via system methods |None |
      

   * Android client

      
      |**Collected field name** |**Purpose description** |**collection method** |**Alternative solution** |
      |---|---|---|---|
      |Device ID |Used for log stream analysis. Through the device ID, you can view a specific device's exception information stream on APMPlus for troubleshooting. |Unique identifier generated by the server. |See [Step 2 of the integration guide: Initialize the SDK and enable monitoring](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_Android_SDK_into_the_application), and use a custom device ID. |
      |Device model |Used for multi\-dimensional analysis and filtering to view the occurrence of exception issues on different device models. |Obtained via system methods |None |
      |Operating system |Used to distinguish the operating system type (Android/iOS) where the exception occurred. |Fixed field |None |
      |System time zone |Used for exception analysis. It helps analyze exception issues occurring in different time zones. |Obtained via system methods |None |
      |Screen resolution |Used for exception analysis. It helps analyze exception issues that may be caused by screen resolution. |Obtained via system methods |None |
      |Disk usage |Used for exception analysis to determine whether the exception occurred due to insufficient disk space. |Obtained via system methods |None |
      |Memory usage |Used for exception analysis to determine whether an exception occurred due to insufficient memory space. |Obtained via system methods |None |
      |Number of running threads |Used for exception analysis. It helps analyze the operating status of different threads. |Obtained via system methods |None |
      |CPU information |Used for exception analysis. It helps analyze possible compatibility issues with different CPU architectures. |Obtained via system methods |None |
      |Mobile Country Code (MCC) |Used to determine the Internet Service Provider |Obtained via system methods |None |
      |Mobile Network Code (MNC) |Used to determine the Internet Service Provider |Obtained via system methods |None |
      |Application version |Used for multi\-dimensional analysis and filtering to view the occurrence of exception issues across different app versions. |Obtained via system methods |None |
      |Application package name |Used for exception analysis. It helps analyze exception issues across different application packages. |Obtained via system methods |None |
      |Process start time |Used for startup analysis. It helps analyze the time consumption of the app's startup chain. |Obtained via system methods |None |
      |Crash time |Used for log stream analysis. It helps perform exception analysis combined with other app logs. |Obtained via system methods |None |
      |Crash thread name |Used for exception analysis to identify the thread where the exception occurred. |Obtained via system methods |None |
      |Names of visited pages |Used for exception analysis. Reproduce scenarios through the activity page to troubleshoot issues. |Obtained via system methods |None |
      |All thread stacks of the current process |Used for exception analysis. It helps analyze the app's operating status when the exception occurred. |Obtained via system methods |None |
      |In\-app language |Used for exception analysis. It helps analyze compatibility issues caused by the system language. |Obtained via system methods |None |
      |App release channel |Used for multi\-dimensional analysis and filtering. It helps analyze exception issues across different channels. |Initialize input information |None |
      |System country/region information |Used for multi\-dimensional analysis and filtering. It helps to analyze the distribution of exception issues across different regions. |Obtained by the server based on the IP address. |None |
      |User ID |Used for log stream analysis. Through the user ID, you can view a specific user's exception information stream on APMPlus for troubleshooting. |Initialize input information |No need to call the method that sets the user ID |
      |Internet Service Provider information |Used for multi\-dimensional analysis and filtering. It helps analyze network issues caused by Internet Service Providers. |Obtained via system methods |None |
      |Network access mode |Used for multi\-dimensional analysis and filtering. It helps analyze issues under different network conditions. |Obtained via system methods |None |
      |Android ID |Used by the server to generate a unique device identifier. |Obtained via system methods |None |
      |Device brand |Used for multi\-dimensional analysis and filtering. It helps analyze issues across different device brands. |Obtained via system methods |None |
      |Operating system API version |Used for multi\-dimensional analysis and filtering. It helps analyze issues under different operating system API versions. |Obtained via system methods |None |
      |Battery level |Used for battery monitoring and analysis |Obtained via system methods |None |
      |Network traffic |Used for battery monitoring and analysis |Obtained via system methods |None |
      |Device abi |Used for multi\-dimensional analysis and filtering. It helps analyze exception issues under different device ABIs. |Obtained via system methods |None |
      |ROM |Used for multi\-dimensional analysis and filtering. It helps analyze exception issues across different ROMs. |Obtained via system methods |None |
      |File descriptor list |Used for exception analysis. It helps analyze exception issues caused by file descriptor (fd) usage. |Obtained via system methods |None |
      |Application service log information |Used for exception analysis to provide attribution information. |Obtained via system methods |None |
