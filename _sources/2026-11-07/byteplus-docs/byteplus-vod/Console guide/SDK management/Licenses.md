---
title: "Licenses"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-license-management"
---

BytePlus VOD uses licenses to manage the validity period and permissions of the Player SDK and its value\-added services. Each license must be bound to an application and is available in Standard and Advanced editions. This guide provides step\-by\-step instructions on how to apply for, bind, upgrade, and renew a license in the BytePlus VOD console to activate the full capabilities of the Player SDK.

<span id="b799178e"></span>
## **Prerequisites**

Ensure you have created an application in the BytePlus VOD console. For details, see [Applications](https://docs.byteplus.com/docs/byteplus-vod/docs-sdk-management).

<span id="8841cd0e"></span>
## **Notes**


* A single license can be used for both the Android and iOS versions of your app.


<span id="aeaf94c3"></span>
## **Applying for a free trial license**

During the project testing phase, you can apply for a free trial license in the BytePlus VOD console. The trial license is valid for 30 days. When the trial expires, you must upgrade to an official license. The application steps are as follows:


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. Click **SDK management** \> **Licenses** on the left navigation bar.

3. Click **Buy Now**.

4. Select the application type, license edition, type, and duration according to your business needs.

5. Select a project. Projects help you control access to BytePlus resources. You must associate the license with a project. To manage projects, visit the [Project management](https://console.byteplus.com/iam/projcetmanage/) page.

6. Select the suitable application type, license edition, type, and duration according to your business needs, and then click **Purchase**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For the features supported by each edition of the Player SDK, see <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-player-sdk-overview">Player SDK overview</a>.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/893e0da6ef1c401599b6fbff7c3ce9e6~tplv-goo7wpa0wc-image.image) </span>

7. Review the order information and proceed with the payment process. Once the payment is successful, click **Go to console** to navigate to the **Licenses** page, where you can find detailed information about your license, including the license package ID, effective time, and expiration time.


<span id="945ed2ba"></span>
## **Binding the license to an application**

After successfully applying for a license, you need to bind it to an application. The steps are as follows:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>



* <div data-tips="true" data-tips-type="tip">Each license package contains only one license and can only be bound to one application. If your company develops multiple apps and you want to bind multiple applications to one license package, contact your <a href="https://www.byteplus.com/en/contact">sales representative</a>.</div>


* <div data-tips="true" data-tips-type="tip">After binding a license to your app, you cannot change the package name or Bundle ID. Doing so will prevent your app from using the VOD SDK. If you need to modify the package name or Bundle ID due to a mistake or special business circumstances, please submit a <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001112">support ticket</a>, and we will process it as soon as possible.</div>



To bind the license to an application, follow these steps:


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. Click **SDK management** \> **Licenses** on the left navigation bar.

3. Click **Details** in the **Action** column. This will take you to the **License package details** page.

4. In the **Bind an existing application** section, click **Add app** at the bottom of the page and choose available applications in the drawer that pops out.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6d8bfe13ef164035951e5177c689e7e6~tplv-goo7wpa0wc-image.image) </span>

5. After binding, click the **Download** button to download the license file to your local device. You will need to set the path to the license file when integrating the SDK.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/30811f5969cb422982369076ff74d37e~tplv-goo7wpa0wc-image.image) </span>


<span id="c1adce16"></span>
## **Upgrading to an official license**

The trial license is valid for 30 days. You need to upgrade to an official license before the trial license expires. The steps are as follows:


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. Click **SDK management** \> **Licenses** on the left navigation bar.

3. Click **Renew** in the **Action** column.

4. Select the duration of the license as 1 or 2 years.

5. Click **Purchase** and proceed with the payment process as instructed.


<span id="cec31a8d"></span>
## **Renewing your license**

Renewal means extending the validity period of the license. You can choose to extend it for one or two years. We recommend that you renew your license at least one month before it expires. Follow the steps below to extend your license:


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. Click **SDK management** \> **Licenses** on the left navigation bar.

3. Click **Renew** in the **Action** column.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e77a97d2aa32482aa37add641391f85f~tplv-goo7wpa0wc-image.image) </span>

4. Proceed with the payment process as instructed.


<span id="bea00e6a"></span>
## **FAQs**

<span id="ce226fc8"></span>
### Do I need to update the app after renewing the license?


* **For Android/iOS applications**: You do not need to release a new version of the app after renewing the license. If there is a change in your license, such as upgrading from a trial license to an official one or extending your official license, the Player SDK will automatically detect these changes in the license file and update the validity period of the license. However, to avoid potential issues with automatic updates caused by network problems, it is recommended to manually download the new license file after making any changes. Simply replace the old license file in your current app version with the new one, and then release a new version of your app.

* **For Web/H5 applications**: If you have set the online address of the license file through the `license.mainUrl` parameter when integrating the Web Player SDK, the SDK will automatically update to the latest license version after the license is upgraded or renewed, without requiring manual updates.


<span id="6ecdf422"></span>
### **Do I need to update the Player SDK after replacing the license file?** 

No, there is no need to update the Player SDK after replacing the license file.

<span id="42804df6"></span>
### **What happens if the license isn't renewed after it expires?** 

We recommend renewing your license at least one month in advance. Failing to renew the license may impact your playback experience:


* **For the Android/iOS Player SDK**

   * If you are using the Premium Edition, it will be downgraded to the Standard Edition after the license expires, resulting in the loss of Premium Edition features.

   * If you are using the Standard Edition, the expiration will lead to a downgrade to the system player, which may cause issues such as degraded performance metrics. If the downgrade occurs while using DRM playback capability, it may result in playback failure.

* **For the Web Player SDK**: After the license expires, the Web Player SDK will still support basic playback control capabilities but will add a watermark showing the BytePlus logo.


<span id="117ca619"></span>
### Can I update the package name or Bundle ID bound to a license?

After binding a license to your app, you cannot change the package name or Bundle ID. Doing so will prevent your app from using the VOD SDK. If you need to modify the package name or Bundle ID due to a mistake or special business circumstances, please submit a [support ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001112), and we will process it as soon as possible.
