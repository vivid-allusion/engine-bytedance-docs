---
title: "Configuring SAML for Zoom"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-configuring-saml-for-room"
---

This article introduces how to configure SAML for your Zoom application in the Admin Portal.

<span id="b5c1c178"></span>
# Uses

This article is divided into two parts:


* [Configuration on Zoom](https://docs.byteplus.com/docs/sealsuite/docs-configuring-saml-for-room#397ca084)

* [Configuration on SealSuite's Admin Portal](https://docs.byteplus.com/docs/sealsuite/docs-configuring-saml-for-room#758b449e)


<span id="397ca084"></span>
# Configuration on Zoom


1. Log in to [Zoom](https://zoom.us) with your Business account.

2. In the left navigation bar, select **ADMIN** \> **Advanced** \> **Single Sign\-on**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2a000cb71e4f43ef9f4072cdb0dd17e1~tplv-goo7wpa0wc-image.image) </span>

3. On the page that appears, specify the following values and click **Save**:

   * **Sign\-in Page URL**: Enter a URL using the following format: `https://example.sealsuite.com/api/idp/sso`

   * **Identity Provider Certificate**: Enter an X.509 certificate retrieved from SealSuite's Admin Portal.

      You can retrieve the X.509 certificate using SealSuite's metadata URL in the following format: `https://example.sealsuite.com/api/idp/metadata`

   * **Service Provider (SP) Entity ID**: Select the URL that starts with `https://`.

   * **Binding**: Select **HTTP\-Redirect**.

   * **Signature Hash Algorithm**: Select **SHA\-256**.

4. Obtain Zoom's Single sign\-on URL by completing the following steps:

   1. Obtain a Service Provider(SP) metadata file at `https://<your_domain>.zoom.us/saml/metadata/sp`

   2. Retrieve Zoom's Single sign\-on URL from the SP metadata file and store it for later use.


<span id="758b449e"></span>
# Configuration on SealSuite's Admin Console


1. Log in to the Admin Console.

2. In the left navigation bar, click **Identity** \> **SSO**.

3. On the **SSO** page, click **Application Marketplace**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/07aa5cca80214f1eb91b0b08735dc6cb~tplv-goo7wpa0wc-image.image) </span>

4. On the **Add New Application** page, use filters to locate the Zoom application template card and click on it.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/39a713fa923d41ccb4ec7fb8b2d40d4f~tplv-goo7wpa0wc-image.image) </span>

5. In the lower right corner of the chosen template card, click **Add**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/864465fca9474aefbbef14ee89a91a10~tplv-goo7wpa0wc-image.image) </span>

6. On the page that appears, complete the following steps to create your own Zoom application.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9147aee00a8c4b238a9b13a7b0df7b24~tplv-goo7wpa0wc-image.image) </span>

   1. In the **General** section, specify **Application Name**, **Application Address**, and **Application Description**.

   2. In the **Application Type** section, you can:

      * View and download SealSuite's metadata file under **IDP Metadata**.

      * Fill in **Zoom unique identifier** and **Single sign\-on address for Zoom** using the following URLs:

         * **Zoom unique identifier**:`https://<your_domain>.zoom.us`

         * **Single sign\-on address for Zoom**: Enter the **Single sign\-on URL** that you saved earlier.

            A single sign\-on URL example is as follows: `https://<your_domain>.zoom.us/saml/SSO`

7. Click **Confirm** to save the configured settings.
