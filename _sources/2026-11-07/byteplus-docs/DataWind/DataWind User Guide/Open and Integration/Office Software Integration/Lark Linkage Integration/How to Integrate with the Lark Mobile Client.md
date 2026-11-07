---
title: "How to Integrate with the Lark Mobile Client"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/How_to_Integrate_with_the_Lark_Mobile_Client"
---

This article describes how to integrate DataWind with the Lark mobile client.

<span id="4aec1aad"></span>
# Feature overview

A key part of integrating with Lark is deploying the DataWind mobile application on the Lark mobile client, allowing users to access and open DataWind directly from the Lark Workbench.

This requires you to complete [Basic Configuration for Lark Integration](https://docs.byteplus.com/docs/DataWind/Basic_Configuration_for_Lark_Integration) and [How to Bind Lark Accounts and Batch Create sers](https://docs.byteplus.com/docs/DataWind/How_to_Bind_Lark_Accounts_and_Batch_Create_sers), then follow the steps below in this article.

<span id="3b92e5b7"></span>
# Instructions

<span id="73b9331f"></span>
## Mobile client deployment


* Please contact the BytePlus product deployment engineer and provide **the APP ID information of the application** and **the application's homepage address**. The BytePlus team will assist in uploading the mini program code package and completing the mobile client deployment.

* If the user applying for the application is not the one uploading the code package, you can first transfer permissions through Lark, and after deployment is complete, return the application permissions.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8dff2e8110e64726be26e2b41e4347cc~tplv-goo7wpa0wc-image.image) </span>

* Since the SaaS version of DataWind does not currently support Lark mini program single sign\-on, you can set the mobile client address of the web application as the SaaS DataWind homepage link in the Lark application backend, so that a mobile client entry can be added in the Lark Workbench.

   * Homepage: https://[domain]/bi/datawind\-h5/tabs?[region]

   * For example, if [domain] is console.volcengine.com and [region] is Shanghai, then the homepage URL is: [https://console.volcengine.com/bi/datawind-h5/tabs?region=cn-shanghai](https://console.volcengine.com/bi/datawind-h5/tabs?region=cn-shanghai).

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The region information for accessing the SaaS version is as follows. For more information, see <a href="https://docs.byteplus.com/docs/undefined/6a05e62618a680056d54216b">Access regions and Volcano Engine intranet connection</a>:      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">North China 2 \- Beijing: region=cn\-beijing      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">East China 2 \- Shanghai: region=cn\-shanghai      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Asia Pacific Southeast \- Johor: region=ap\-southeast\-1      </div>
      

<span id="f96933fa"></span>
## Pin the mobile client

**You can recommend the application in the Lark Workbench and pin the mobile client as follows:** 


* In Lark, click Workbench \-\> click the settings icon in the upper right corner \-\> click Manage Recommended Applications \-\> click Go to Settings \-\> go to the application management page.

* Click Workbench on the left \- Workbench Settings \- Admin Recommendations, click Add Recommendation Rule and fill out the form. After adding, the application can be pinned.

* After saving, you will see that the application has been pinned.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When both the bot application and the mobile application are enabled, it is possible that clicking on the mobile side will directly open the bot dialog. At this time, simply click the bot and then select "Open application".   </div>
