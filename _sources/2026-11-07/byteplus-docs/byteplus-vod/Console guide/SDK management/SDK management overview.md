---
title: "SDK management overview"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-sdk-management-overview"
---

The **SDK Management** page is a central hub in the BytePlus VOD console for managing applications that integrate the BytePlus VOD SDKs. This page allows you to perform key tasks such as creating an application, purchasing a license package, and binding the license to your application to enable SDK functionalities.

<span id="9bc33bd2"></span>
## Key concepts


* **Application**: A BytePlus VOD application manages the BytePlus VOD SDKs you use, including binding your traffic pack to your Android and iOS projects, generating SDK licenses, and providing SDK download addresses. After you create an application in the BytePlus VOD console, a unique App ID will be assigned to the application.

* **License**: BytePlus VOD manages the validity period and permissions of the VOD SDKs and value\-added services through licenses. Licenses are available in Standard and Premium editions, each offering different functionalities. Every license possesses a unique license ID and must be bound to an application. Additionally, licenses come in two types: Trial and Official. Trial licenses are exclusively used for debugging and do not support renewal or modification. It is recommended to apply for an official license before your project goes online.

* **License package**: Licenses within the same package share the same permissions and validity period. By default, a license package contains only one license and can only be bound to one application. If you develop multiple applications at the same time and want to bind multiple applications to a license package, please contact your [sales representative](https://www.byteplus.com/en/contact).


<span id="cccbb8ca"></span>
## Process


|Process |**Description** |Documentation |
|---|---|---|
|Create an application |Create an application in the BytePlus VOD console and configure basic information such as the application name, Package Name, Bundle ID, and description. |[Creating an application](https://docs.byteplus.com/docs/byteplus-vod/docs-sdk-management#2d46dc0c) |
|Apply for a free trial license |Apply for a trial license of a specific edition based on your business needs. The trial license is valid for 30 days. |[Applying for a free trial license](https://docs.byteplus.com/docs/byteplus-vod/docs-license-management#aeaf94c3) |
|Bind the license to the application |Bind the application you created to the trial license you applied for, and download the license file to your local device. |[Binding the license to an application](https://docs.byteplus.com/docs/byteplus-vod/docs-license-management#945ed2ba) |
|Integrate the SDK into your project |Integrate the Player SDK into your project and set the license file path by referring to the documentation. |* [Android Player SDK: Quickstart](https://docs.byteplus.com/docs/byteplus-vod/docs-getting-started-with-the-android-player-sdk)<br><br>* [iOS Player SDK: Quickstart](https://docs.byteplus.com/docs/byteplus-vod/docs-getting-started-with-the-ios-player-sdk)<br><br>* [Web Player SDK: Quickstart](https://docs.byteplus.com/docs/byteplus-vod/docs-getting-started-with-the-web-player-sdk) |
|Upgrade to an official license |After testing the SDK features, upgrade to an official license. |[Upgrading to an official license](https://docs.byteplus.com/docs/byteplus-vod/docs-license-management#c1adce16) |
