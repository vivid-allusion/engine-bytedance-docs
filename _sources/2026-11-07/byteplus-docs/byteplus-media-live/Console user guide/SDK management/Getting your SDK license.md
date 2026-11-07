---
title: "Getting your SDK license"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management"
---

To use the BytePlus MediaLive SDKs in your app, you must first get a valid license. This license activates the SDK's features for your specific app. This topic walks you through the entire process, from creating an SDK application in the console to getting the license required for SDK integration.

> **注意**

> You need to create an SDK application and get a license only when using the following BytePlus MediaLive SDKs:

* > Player SDK for iOS

* > Player SDK for Android

* > Player SDK for React Native

* > Player SDK for Flutter

* > Player SDK for Web (version 2.11.0 or later)

## Prerequisites

* For Android or iOS apps, prepare the following information:

   * **Android**: Your app's package name. You can find this as the `applicationId` value in your project's `build.gradle` file under the `app` directory.

   * **iOS**: Your app's bundle ID. You can find this as the `Bundle Identifier` value in your app target's settings in Xcode.

* For web apps, prepare the following information:

   * **Web** (for browser pages): A wildcard domain such as `*.example.com` that covers all pages where you plan to embed the player.

   * **WebOTT** (Web Over\-The\-Top, for web apps running on Tizen and webOS smart TV systems, supported only by Player SDK for Web 2.12.0 and later)

      * **Tizen**: Your application identifier. You can find this as the `applicationId` value in your project's `config.xml` file.

      * **webOS**: Your application identifier. You can find this as the `id` value in your project's `appinfo.json` file.

## Step 1: Create or bind an SDK application

1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left\-side navigation pane, click **SDK management**.

3. Click **Create SDK application** to create an SDK application, or click **Bind existing application** if you have already created an application in the BytePlus VOD console.

4. Configure the basic information.

   **Android or iOS apps**

For Android or iOS apps, complete the following steps.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a82a7363c8a1444eaef0ea238d643f5c~tplv-goo7wpa0wc-topic.webp)

      * **SDK type**: Select **App** as the SDK type. This type of application is used to integrate client SDKs.

      * **Application name**:

         * If you are creating a new application, enter a unique name. The name must be 1–128 characters long and can contain letters (A\-Z, a\-z), numbers (0\-9), Chinese characters, and certain special characters.

         * If you are binding an existing application, select the app ID. You can find the ID on the application list page of the BytePlus VOD console.

      * **Project**: Select the project for the SDK application. This ensures that only sub\-accounts with access to this project can manage the application.

      * **PackageName** and **Bundle ID**: Enter the package name for your Android app and the bundle ID for your iOS app. This binds the SDK license to your apps to prevent unauthorized use. Provide both if your app supports both platforms, and only one if your app supports a single platform.

         > **注意**

         > Ensure the entered **PackageName** and **Bundle ID** are globally unique.

   **Web apps**

For web apps, complete the following steps.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/87f6bb90aa7f40db931ce4da906f3864~tplv-goo7wpa0wc-topic.webp)

      * **SDK type**: Select **Web** as the SDK type. This type of application is used to integrate the Player SDK for Web.

      * **Application name**:

         * If you are creating a new application, enter a unique name. The name must be 1–128 characters long and can contain letters (A\-Z, a\-z), numbers (0\-9), Chinese characters, and certain special characters.

         * If you are binding an existing application, select the app ID. You can find the ID on the application list page of the BytePlus VOD console.

      * **Project**: Select the project for the SDK application. This ensures that only sub\-accounts with access to this project can manage the application.

      * **Wildcard domain**: Enter the following information based on your scenario.

         * **Web** (for browser pages): To authorize playback, enter a wildcard domain that covers all pages where you plan to embed the player. This allows the player to run on any matching first\-level subdomain.

            **Example**: If you enter `*.example.com`:

            * **Matches**: `a.example.com`, `b.example.com`

            * **Does not match**: `a.b.example.com` (multi\-level subdomain), `example.com` (root domain)

               **Rules**:

            * The value must start with an asterisk (`*`) and cannot exceed 128 characters.

            * The wildcard character (`*`) must be used for a domain that you own, and cannot be used for public suffixes or top\-level domains.

               * Correct: `*.example.com` (because `example.com` is a specific domain that you own).

               * Incorrect: `*.com` or `*.com.cn` (because `.com` is a top\-level domain and `.com.cn` is a public suffix, neither of which is owned by a single entity).

         * **WebOTT** (for web apps running on Tizen and webOS smart TV systems, supported only by Player SDK for Web 2.12.0 and later): Enter your application identifier.

         > **注意**

         > Ensure the entered wildcard domain or application identifier is globally unique.

5. If you are creating a new application, click **Create an app**. If you are binding an existing application, click **Next**.

6. Configure and bind the license to your SDK application.

   > **说明**

   * > Each license can only be bound to one SDK application.

   * > The validity period for your SDK license begins only when the license is bound to your SDK application.

   * > A license is used to manage the usage rights and duration of the SDK and its value\-added services. For features supported by each license type, see [Client SDK: SDK overview](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-introduction) and [Player SDK for Web: SDK overview](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-web-sdk-overview). For pricing of each license type, see [SDK licenses](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-licenses).

   * > If you need to integrate the Player SDK for Web of a version earlier than 2.11.0, you do not need to bind a license. You can get the app ID directly for SDK integration. However, we recommend that you upgrade the Player SDK for Web to version 2.11.0 or later to get better features and services.

   **Trial license**

The trial license is for **testing purposes only** and is valid for **one month**. For example, a license bound to your application at 10:00 on May 10, 2026, will expire at 10:00 on June 10, 2026.

   Follow these steps to get your trial license:

      1. Select **Trial** as the license type, and then click **Acquire the license**. You will be directed to the **License purchase** page.

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/16b9df9aacb04ab6a2c6a76077845250~tplv-goo7wpa0wc-topic.webp)

      2. On the purchase page, click **Get it now** to proceed with the free license acquisition.

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b997614ab172403f8aca0a33415b9cb6~tplv-goo7wpa0wc-topic.webp)

      3. After completing the checkout process for the free license, return to the configuration page. Select the trial license you just acquired and click **Confirm**.

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f206935371934e1ab2bd4917df8d9935~tplv-goo7wpa0wc-topic.webp)

         > **说明**

         > If the new trial license does not immediately appear in the list, click the refresh icon to update the page.

         > ![](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3afbc908af9f4304bae35f8dc76b10d9~tplv-goo7wpa0wc-topic.webp)

   Before your trial license expires or when you are ready to release your app for production, you must upgrade the license to a basic or premium version. For more information, see [Upgrading a trial license to a basic or premium license](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses#777c7de7).

   **Basic license**

The basic license is intended for the **production environment** and has a **validity period of one year**. For example, a license bound at 10:00 on May 10, 2026, will be valid until 10:00 on May 10, 2027. You can renew a basic license at any time. For more information, see [Renewing a license](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses#b2dde14f).

   To get a basic license, select **Basic** as the license type and choose one of the following methods:

      * Buy directly

         1. Click **Buy now**.

            ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5bedee922aa84a8184d924132120ef07~tplv-goo7wpa0wc-topic.webp)

         2. After completing the purchase, return to the configuration page. Select the basic license from the list and click **Confirm**.

            ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3a4ab8a8ff8b4d708dd4876ccf6006f9~tplv-goo7wpa0wc-topic.webp)

            > **说明**

            > If your newly purchased license does not appear in the list immediately, click the refresh icon to update the page.

            > ![](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3afbc908af9f4304bae35f8dc76b10d9~tplv-goo7wpa0wc-topic.webp)

      * Bind a traffic pack: You can get a free one\-year basic license by binding a live\-stream traffic pack of 100 TB or larger to your application. For more information about the live\-stream traffic pack, see [Resource packs](https://docs.byteplus.com/docs/byteplus-media-live/docs-resource-packs).

         > **说明**

         > This method is **only** available for app\-type applications.

         * **If you already have an eligible traffic pack**: Select the traffic pack from the list and click **Confirm**.

         * **If you do not have an eligible traffic pack**:

            1. Click **Buy Now** to purchase one.

               ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aa45000672b94d6eae8a6509bae35357~tplv-goo7wpa0wc-topic.webp)

            2. After completing the purchase, return to the configuration page. Select the traffic pack from the list and click **Confirm**.

               > **说明**

               > If your newly purchased traffic pack does not appear in the list immediately, click the refresh icon to update the page.

               > ![](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3afbc908af9f4304bae35f8dc76b10d9~tplv-goo7wpa0wc-topic.webp)

   **Premium license**

The premium license is intended for the **production environment** and has a **validity period of one year**. For example, a license bound at 10:00 on May 10, 2026, will be valid until 10:00 on May 10, 2027. You can renew a premium license at any time. For more information, see [Renewing a license](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses#b2dde14f).

   Follow these steps to get the premium license:

      1. Select **Premium** as the license type.

      2. Click **Buy now**.

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a98e6675afe345348571f5ef165106c8~tplv-goo7wpa0wc-topic.webp)

      3. After completing the purchase, return to the configuration page. Select the premium license and click **Confirm**.

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/31b655fa42144106a5f1b0836dca473b~tplv-goo7wpa0wc-topic.webp)

         > **说明**

         > If your newly purchased license does not appear in the list immediately, click the refresh icon to update the page.

         > ![](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3afbc908af9f4304bae35f8dc76b10d9~tplv-goo7wpa0wc-topic.webp)

7. Your application now appears in the application list on the **SDK management** page. Locate your application in the list, and find the **App ID** and **Application name**. You will need both to integrate and initialize the SDK.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7ac12129476144c8b5a06412796f84e3~tplv-goo7wpa0wc-topic.webp)

## Step 2: Get the license

The BytePlus MediaLive SDK must be used with an SDK license. The license you get is valid only for the bound SDK application.

On the [SDK management](https://console.byteplus.com/live/main/sdk) page, find the target application.

* For Android or iOS apps, click the download icon to download the license file. Then, use the license file to integrate the SDK.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/44a07076e89243e38d48f42a5ad23276~tplv-goo7wpa0wc-topic.webp)

* For web apps, click the download icon to download the license file, or click **detail** to get the license URL used to integrate the Player SDK for Web.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/954db88e8e494a199525032b09044587~tplv-goo7wpa0wc-topic.webp)

> **说明**

> Make sure the application status is **Activated**.

* > If the status is **Expired**, you must renew the license first. For more information, see [Renewing a license](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses#b2dde14f).

* > If the status is **Not activated**, click the ellipsis icon (...) in the **Action** column and select **Activate** to configure and bind the license. For more information on how to configure and bind the license, see [Step 1: Create or bind an SDK application](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management#91608dc8).

## Related operations

On the **SDK management** page, you can do the following in the **Action** column.

* **Edit**: Click **Edit** to change the application name, **PackageName**, **Bundle ID**, wildcard domain, or WebOTT application identifier.

   * If the license has already been activated, the system regenerates the license based on the updated app information after the change. You need to replace the SDK license file or license URL. The original license remains valid for a period of time, and the new license keeps the same expiration time as the original one.

   * If the license has expired, the system generates a new license based on the updated app information when you renew the license. You need to replace the SDK license file or license URL after the renewal is complete.

* **Delete**: Click the ellipsis (...) icon and select **Delete** to permanently delete the application.

   > **注意**

   > If you accidentally delete an application, you can recover it and continue using the original App ID through **Bind existing application**. When binding the application, you need to reconfigure the **PackageName**, **Bundle ID**, wildcard domain, or WebOTT application identifier. The system does not retain the configuration information from before deletion. If the SDK application was just deleted, it may not appear immediately in the **Bind existing application** dialog box. In this case, try again later.

* **Renew**: When your license is about to expire or has expired, click **Renew** to renew the license. For more information, see [Renewing a license](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses#b2dde14f).

* **Upgrade**: Click **Upgrade** to upgrade the trial license to a basic or premium license. For more information, see [Upgrading a trial license to a basic or premium license](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses#777c7de7).

* **Activate**: If a license has not been bound to the application, click the ellipsis (...) icon and select **Activate** to configure and bind the license. For more information on how to configure and bind the license, see [Step 1: Create or bind an SDK application](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management#91608dc8).

## What to do next

Use the license file, license URL, app ID, and application name that you get from the console to integrate and initialize the SDK. For more information, see:

* iOS: [Integrating the Player SDK for iOS](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-ios) and [Initializing the Player SDK for iOS](https://docs.byteplus.com/docs/byteplus-media-live/docs-initializing-for-ios)

* Android: [Integrating the Player SDK for Android](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-android) and [Initializing the Player SDK for Android](https://docs.byteplus.com/docs/byteplus-media-live/docs-initializing-for-android)

* Flutter: [Integrating the Player SDK for Flutter](https://docs.byteplus.com/docs/byteplus-media-live/integrating-the-player-sdk-for-flutter) and [Initializing the Player SDK for Flutter](https://docs.byteplus.com/docs/byteplus-media-live/initializing-the-player-sdk-for-flutter)

* React Native: [Integrating the Player SDK for React Native](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-rn) and [Initializing the Player SDK for React Native](https://docs.byteplus.com/docs/byteplus-media-live/docs-initializing-for-rn)

* Player SDK for Web: [Integrating the Player SDK for Web](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web_1)
