---
title: "Use Multiple Apps"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Use_Multiple_Apps"
---

If you have multiple applications and need to analyze user behavior data in multiple applications, you can enable the multi\-application function using DataFinder. This article explains how to use the multi\-application function.

<span id="f0e70f11"></span>
# Precautions


|Attention segmentation |Detailed description |
|---|---|
|Environmental constraints |SaaS\-cloud\-native and private environments are supported. |
|Function switch |This feature is for advanced use and is currently available on demand for customers with relatively complex business needs.<br><br><br>* Customers who newly purchased Finder: After cloud native and privatization 4.4 version, it can be turned on on demand freely, and the multi\-application function is turned on by default; the multi\-subject and multi\-ID type functions are turned off by default.<br><br>* Customers who have purchased Finder: Support is only enabled for environments using one_id services, and manual execution is required for historical data migration. |
|Binding relationship |* A DataFinder project supports binding multiple applications.<br><br>* An application only supports the option to bind one principal.<br><br>* A principal can be bound by multiple applications.<br><br>   When a subject is bound by multiple applications, subsequent data analytics supports the analysis of the current subject's behavior data in multiple applications, and can also filter through the application ID to analyze only the subject's behavior data in some of the applications.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Since an app only supports binding one principal, if you need to use the multi\-principal feature to perform data analytics on multiple agents, you need to create multiple apps in your project, each binding one principal.</div><br> |
|Other related products |When using the multi\-agent function, you also need to activate the CDP product at the same time. |


<span id="36eb83d3"></span>
# Operation process

<span id="6a805ed7"></span>
## Step1: Add multiple applications

After opening multiple applications, when you log in and enter the Project Center \- Project details page of DataFinder, click **Edit** to enter the project editing state, you can see that multiple applications can be bound to a project at the same time, and click "Create Application" to add multiple applications.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b1c5d27efb8240c3b861449487749eec~tplv-goo7wpa0wc-image.image) </span>

After the addition is complete, you can view the application information here, such as the application ID (appid), etc., for details, see [Project Management](https://docs.byteplus.com/docs/DataFinder/Project_Management__).

<span id="b6d1ed5e"></span>
## Step2: Data reporting

<span id="d5eeb9f4"></span>
### Report application information: appid

After opening the multi\-application function, you need to mark clearly which application data is reported when reporting data. Similar to non\-multi\-application scenarios, you only need to set the reported application ID ( **appid** ) when initializing data access, and use appid to identify the reported application.

For detailed data access reporting code details, please refer to the initialization section of each end's data access documentation.

<span id="099531a5"></span>
## Step3: View application information for reported data

Events/attributes and other metadata are managed at the project level, making it easy to manage the same business and use the same event tracking scheme at different ends. You can view the application information for reporting data in App Management, for example, on the General Events page to see which applications reported these events.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d6c8f12b1a2242298fcd53e1ea030b5e~tplv-goo7wpa0wc-image.image) </span>

<span id="5079060a"></span>
## Step4: Data analysis

After enabling the configuration multi\-application function, when you perform data analytics in the future, you can analyze all application data associated with a subject, and also support filtering by application ID in segmentation filtering to analyze only some application data.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d07829cfa6a64da985e2c477baf1885a~tplv-goo7wpa0wc-image.image) </span>

<span id="3951d358"></span>
## Step5: Data dashboard

Dashboard is aggregated in project granularity, and each chart in a Dashboard can be created based on the analysis results of different subjects or different applications, making it easy to create a data dashboard with a global perspective.

The chart in Dashboard also supports the **chart filter** , and the configuration filters only the data of some applications through the application ID, which is convenient for switching the data performance of the same business at different ends.


* Global filter configuration for the entire Dashboard board

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/41b87fc74cc84a55aeca903c6ba5f5cd~tplv-goo7wpa0wc-image.image) </span>

* Filter configuration for a chart in Dashboard

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df8b3a5c95594258b8eadbb9099ae87b~tplv-goo7wpa0wc-image.image) </span>
