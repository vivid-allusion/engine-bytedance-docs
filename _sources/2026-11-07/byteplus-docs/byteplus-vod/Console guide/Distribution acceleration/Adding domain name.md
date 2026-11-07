---
title: "Adding domain name"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-domain-name-management"
---

To accelerate the content delivery on a particular website, you need to add the domain name to the BytePlus VOD console. This article walks you through the steps of adding a CDN domain name to the BytePlus VOD console.

<span id="8a3b75c9"></span>
## Domain name types

BytePlus VOD supports three types of domain names:


* **Playback domain name**: This type of domain name is used to generate playback URLs for audio and video content. It retrieves the content from the BytePlus VOD origin server.

* **Custom\-origin domain name**: This type of domain name retrieves content from third\-party origin servers, rather than the BytePlus VOD origin servers. This feature is useful in flexible business scenarios where content needs to be fetched from different sources.

* **Image domain name**: This type of domain name is used to generate URLs for cover images and screenshots. It retrieves the content from the BytePlus VOD origin server.


<span id="f9d23f17"></span>
## Prerequisites


* Ensure that you have enabled the BytePlus VOD service.

* Prepare a valid domain name.


<span id="c9511b92"></span>
## Adding a playback domain name


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and select a specific space.

2. Click **Distribution acceleration** \> **Domain names** on the left navigation bar.

3. Select the domain name type by clicking the **Playback domain name** tab.

4. Click **Add domain name**.

5. In the dialog box that appears, configure the following parameters of the domain name:

   1. Fill in the domain name. You must follow the following rules:

      * The domain name must be exact, such as `example.byte-test.com`. By default, wildcard domain names, such as `*.test.com`, are not supported.

      * Capital letters are not supported.

      * Duplicate domain names are not supported. A domain name is considered a duplicate if it is already used in another BytePlus product or feature that uses a CDN.

   2. Select the acceleration region.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">Note      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">To use distribution acceleration in Chinese mainland, you must complete <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-real-name-registration">real\-name authentication</a>.      </div>
      

   3. Click **Confirm**.


<span id="0f2ab068"></span>
## Adding a custom\-origin domain name


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and select a specific space.

2. Click **Distribution acceleration** \> **Domain names** on the left navigation bar.

3. Select the domain name type by clicking the **Custom\-origin domain name** tab.

4. Click **Add domain name**.

5. In the dialog box that appears, configure the following parameters of the domain name:

   1. Fill in the domain name. You must follow the following rules:

      * The domain name must be exact, such as `example.byte-test.com`. By default, wildcard domain names, such as `*.test.com`, are not supported.

      * Capital letters are not supported.

      * Duplicate domain names are not supported. A domain name is considered a duplicate if it is already used in another BytePlus product or feature that uses a CDN.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">To add a wildcard domain name, please <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> to our technical team for application. Currently, wildcard domain names are only supported for <strong>custom\-origin</strong> <strong>configuration</strong>.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">A wildcard domain name cannot be added if it conflicts with an existing subdomain. For example, if a specific subdomain name <code>a.test.com</code> is already configured, you are unable to create the corresponding wildcard domain <code>*.test.com</code>.      </div>
      

   2. Select the acceleration region.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">Note      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">To use distribution acceleration in Chinese mainland, you must complete <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-real-name-registration">real\-name authentication</a>.      </div>
      

   3. Select the origin type and add origin domain.

      
      |Parameter |Description |
      |---|---|
      |Origin type |* Origin IP<br><br>* Origin domain name |
      |Origin domain<br><br>address |You need to add at least one **Origin IP** or **Origin domain name**. The total number of entries cannot exceed 50.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The origin domain must not be identical to the acceleration domain. Such a configuration will trigger a resolution loop, leading to origin\-pulling failures.</div><br> |
      |Origin HOST |Enter the HOST header value (up to 1,024 characters) for the origin\-pulling request.<br><br><br>* You can configure distinct Origin HOST for each origin domain.<br><br>* It defaults to the global Origin HOST but takes priorities if it is specified. |
      

   4. (Optional) Configure **global Origin HOST** to specify the HOST field value carried in the CDN origin\-pulling request. This setting has a lower priority than the **specified Origin HOST** in the origin configuration.

   5. Click **Confirm**.


<span id="0d63a867"></span>
## Adding an image domain name


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and select a specific space.

2. Click **Distribution acceleration** \> **Domain names** on the left navigation bar.

3. Select the domain name type by clicking the **Image domain name** tab.

4. Click **Add domain name**.

5. In the dialog box that appears, configure the following parameters of the domain name:

   1. Fill in the domain name. You must follow the following rules:

      * The domain name must be exact, such as `example.byte-test.com`. By default, wildcard domain names, such as `*.test.com`, are not supported.

      * Capital letters are not supported.

      * Duplicate domain names are not supported. A domain name is considered a duplicate if it is already used in another BytePlus product or feature that uses a CDN.

   2. Select the acceleration region.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">Note      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">To use distribution acceleration in Chinese mainland, you must complete <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-real-name-registration">real\-name authentication</a>.      </div>
      

   3. Click **Confirm**.


After you add a domain name to the BytePlus VOD console, the domain name appears in the domain name list with a status of **Configuring**. Once configuration is complete, the domain name status becomes **Complete**. BytePlus VOD automatically assigns a CNAME target for your domain name, which you can find in the **CNAME** column of the domain name list.
