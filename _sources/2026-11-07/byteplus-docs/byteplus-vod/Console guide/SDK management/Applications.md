---
title: "Applications"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-sdk-management"
---

To use BytePlus VOD SDKs, you first need a VOD application. This guide shows you how to create an application, configure its basic information, and manage its associated licenses directly within the BytePlus VOD console.

<span id="bfae50a8"></span>
## Prerequisites


* Ensure that you have enabled the BytePlus VOD service.

* Note down the package names of your Android and iOS projects.

   * For an Android project, the package name is the value of `applicationId` in the `build.gradle` file, such as `com.example.myapplicationtest`.

   * For an iOS project, the package name is the value of `bundleId` of the main target in Xcode.


<span id="2d46dc0c"></span>
## Creating an application

To create an application, follow these steps:


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. Click **SDK management** \> **Applications** on the left navigation bar.

3. Click **Create application**.

4. In the dialog box that opens, enter the following information:

   
   |**Parameter** |**Description** |
   |---|---|
   |Project |Projects help you control access to BytePlus resources. You must associate the application with a project. To manage projects, visit the [Project management](https://console.byteplus.com/iam/projcetmanage/) page. |
   |Application name |Enter the name of the application. The application name can contain letters, digits, and underscores (_). The length cannot exceed 64 characters. |
   |Application type |Select the application type. The following options are supported:<br><br><br>* App<br><br>* Web/H5 |
   |Android Package Name |Displayed when **Application type** is **App**. Enter your Android project's package name, which is the `applicationId` value in the `build.gradle` file, for example, `com.example.myapplicationtest`. The length cannot exceed 128 characters. |
   |iOS Bundle ID |Displayed when **Application type** is **App**. Enter your iOS project's bundle ID, which is the value of `bundleId` of the main target in Xcode. The length cannot exceed 128 characters. |
   |Domain name |Displayed when **Application type** is **Web/H5**. Enter your website's wildcard domain name (not the playback domain name). For example: `*.byteplus.com`. |
   |Description |The application description can indicate the purpose of the application. The length of the application description should be less than 140 characters. |
   

5. Click **Confirm**. After you have successfully created an application, you can find the application in the application list. The BytePlus VOD console automatically generates an App ID for the application.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a879557f82a54605990da2aaea4031a4~tplv-goo7wpa0wc-image.image) </span>


<span id="d77794b9"></span>
## **Editing the application's basic information**

To edit the application's basic information, follow these steps:


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. Click **SDK management** \> **Applications** on the left navigation bar.

3. Click **Details** in the **Action** column. This will take you to the **App details** page.

4. In the **Basic information** section, you can make changes to the package name, bundle ID, and description of the application.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Please keep in mind that once the bundle ID and package name are bound to an official license package, they can no longer be modified.   </div>
   

<span id="2b66e1b1"></span>
## **Viewing the licenses bound to the app**

To view the licenses associated with the app, follow these steps:


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. Click **SDK management** \> **Applications** on the left navigation bar.

3. Click **Details** in the **Action** column. This will take you to the **App details** page.

4. In the **Licenses bound to the app** section, you can see any licenses that have been bound to this application. If there are no licenses displayed, click **Go to bind a license to the app**. For how to purchase a license and bind it to your application, see [Licenses](https://docs.byteplus.com/docs/byteplus-vod/docs-license-management).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1f4df9af4c554ec6bea043123c40fbe6~tplv-goo7wpa0wc-image.image) </span>
