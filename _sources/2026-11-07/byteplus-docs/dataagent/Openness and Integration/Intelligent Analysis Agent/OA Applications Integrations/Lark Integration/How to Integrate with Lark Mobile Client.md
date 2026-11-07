---
title: "How to Integrate with Lark Mobile Client"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/How_to_Integrate_with_Lark_Mobile_Client"
---

This article describes how to integrate DataWind with the Lark mobile client.

<span id="e5b2a5a3"></span>
# Feature overview

In Lark integration applications, an essential part is integrating or deploying the DataWind mobile application on the Lark mobile client, so that users can access and open DataWind directly from the Lark Workbench.

This requires completing [Basic Configuration for Lark Integration](https://docs.byteplus.com/docs/dataagent/Basic_Configuration_for_Lark_integration) and [How to Bind Lark Accounts and Batch Create Users](https://docs.byteplus.com/docs/dataagent/How_to_Bind_Lark_Accounts_and_Batch_Create_Users), followed by the operational steps described below in this article.

<span id="868fb8ac"></span>
# Operation introduction

<span id="8890a973"></span>
## Mobile client deployment


* Please contact the BytePlus product deployment engineer and provide **the APP ID information for this application** and **the application's homepage address**. The BytePlus team will assist in uploading the mini program code package and completing the mobile client deployment.

* If the user applying for the application is not the one uploading the code package, permissions can first be transferred via Lark. After deployment is complete, the application permissions can be returned.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bfbd75710d214693a6066c2c6cf25cc0~tplv-goo7wpa0wc-image.image) </span>


* Since the SaaS version of DataWind does not currently support Lark mini program single sign\-on, you can set the mobile client address of the web application as the SaaS DataWind homepage link in the Lark application backend, which allows you to add a mobile client entry in the Lark Workbench.

   * Homepage: https://[domain name]/bi/datawind\-h5/tabs?[region name]

   * Example: If [domain name] is console.volcengine.com and [region name] is Shanghai, then the homepage URL is: [https://console.volcengine.com/bi/datawind-h5/tabs?region=cn-shanghai](https://console.volcengine.com/bi/datawind-h5/tabs?region=cn-shanghai). Note


The region information for accessing the SaaS version is as follows. For more details, see [Region access and BytePlus intranet connection](https://www.volcengine.com/docs/4726/1418732):

North China 2 \- Beijing: region=cn\-beijing

East China 2 \- Shanghai: region=cn\-shanghai

Asia Pacific Southeast \- Johor: region=ap\-southeast\-1

<span id="f5e21601"></span>
## Pinning the application to the top on the mobile client

**You can recommend the application in the Lark Workbench to pin it to the top on the mobile client.** 


* In Lark, click Workbench \-\> click the settings icon in the upper right corner \-\> click Recommended Application Management \-\> click Go to Settings \-\> you will be redirected to the Application Management page.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/311f28615bfa4905a86e7c2a9cc1f79d~tplv-goo7wpa0wc-image.image) </span>


* Click Workbench on the left panel, then Workbench Settings, then Admin Recommendations. Click Add Recommendation Rule and fill out the form. After adding, the application can be pinned to the top.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5b47be6c042d488f896d8ca472f0bc10~tplv-goo7wpa0wc-image.image) </span>


* After saving, you will see that the application is now pinned to the top.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1009631d52584cd4a164cb90758c46f3~tplv-goo7wpa0wc-image.image) </span>

Caution

If both the bot application and the mobile application are enabled at the same time, it is possible that clicking on the mobile device will directly open the bot dialog box. In this case, simply click the bot and then choose to open the application.
