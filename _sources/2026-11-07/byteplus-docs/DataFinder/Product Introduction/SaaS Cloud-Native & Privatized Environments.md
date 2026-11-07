---
title: "SaaS Cloud-Native & Privatized Environments"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/SaaS_Cloud-Native_Privatized_Environments"
---

The current DataFinder provides you with two categories of SaaS and private deployment methods. The SaaS environment is SaaS\-cloud\-native environment. The product functions and operation processes of the two types of SaaS environments are basically the same, and there are slight differences in the operation and some details of the administrator. This article introduces how to identify two types of SaaS environments.

<span id="97c01009"></span>
# How can I confirm whether my SaaS environment is a SaaS\-cloud native environment?

If you are using DataFinder's SaaS environment and you are unsure whether your environment is SaaS\-cloud\-native, you can log in to the DataFinder product console and check the following to determine whether you are using a SaaS\-cloud\-native environment.


* View the product's console link URL.

   
   |**SaaS\-cloud native environment** |
   |---|
   |SaaS\-Cloud Native provides you with multiple service regions. After logging in to the product console, you can view the region where your current service is located in the upper right corner of the page.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ed30759d9db34be1ba3e9d52f4af466d~tplv-goo7wpa0wc-image.image) </span><br><br>Therefore, if there is geographically relevant information in the upper right corner of the interface, your current environment is a SaaS\-cloud native environment. |
   |Product Console Link URL Format: https://console.volcengine.com/datafinder/ **project** /\*\*\*\*/ project/detail<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14ba221a108544ccab0499b4a8455a8b~tplv-goo7wpa0wc-image.image) </span><br><br>Include the **project** keyword in the URL.<br><br>The new **Project Center** function module in the SaaS\-cloud native environment places more emphasis on managing and using DataFinder as a unit of projects, so the keywords of **project** are included in the product console URL. |
   

* SaaS\-cloud\-native supported geographies

   
   |**SaaS\-cloud native environment** |
   |---|
   |Overseas regions:<br><br><br>* Southeast Asia (Johor): ap\-south\-east\-1 |
   

   Users of SaaS\-cloud native environments who wish to see which region is currently using the DataFinder service can refer to [Supported Regions](https://docs.byteplus.com/docs/DataFinder/Supported_Regions).


<span id="e1c69e92"></span>
# Precautions

DataFinder in different environments and regions is roughly the same in terms of product functions and usage logic. The main differences are:


* Data reporting address: The data reporting addresses in different environments and regions are inconsistent. You need to report the data to the address in the corresponding region. If the reporting address does not match the region, the data cannot be queried and analyzed normally. Please refer to the data reporting address for various domains [Data Reporting Address](https://docs.byteplus.com/docs/DataFinder/Data_Reporting_Address).

* Application/project/group management operations: There are differences in the administrator operation entrance of different environments. For example, the operation entrance of SaaS\-cloud\-native environments is mainly in the project management entrance.


Other differences can be found when viewing the corresponding feature documentation, focusing on the description of the supported environment for the feature.

<span id="8980fa28"></span>
# Notes on SaaS environments in the help documentation

In order to facilitate you to follow up on the SaaS environment you are currently using to view the corresponding help documents, the guidance documents under different environmental scenarios are marked in the help documents in the following ways:


* In SaaS\-cloud\-native, most products are used in the same way, and this type of documentation does not specifically distinguish between SaaS and SaaS cloud\-native in the help documentation. If similar content refers to both SaaS and privatization, the SaaS section indicates that it applies to SaaS\-cloud\-native.
