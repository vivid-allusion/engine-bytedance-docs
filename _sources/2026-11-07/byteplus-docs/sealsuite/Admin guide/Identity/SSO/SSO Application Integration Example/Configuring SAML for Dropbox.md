---
title: "Configuring SAML for Dropbox"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-dropbox"
---

This article introduces how to configure SAML for your Dropbox application in the Admin Portal.

<span id="d63277c4"></span>
# Uses

This article is divided into two parts:


* [Configuration on Dropbox Admin Console](https://docs.byteplus.com/docs/sealsuite/docs-dropbox#e2cf4974)

* [Configuration on SealSuite's Admin Portal](https://docs.byteplus.com/docs/sealsuite/docs-dropbox#6b9944f0)


<span id="e2cf4974"></span>
# Configuration on Dropbox Admin Console


1. Log in to [Dropbox](https://www.dropbox.com/login).

2. In the left navigation bar, click **Admin console**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b486877141c1499db95631a771aab16c~tplv-goo7wpa0wc-image.image) </span>

3. In the left navigation bar of the page that appears, click **Settings**.

4. On the **Settings** page, click **Single sign\-on**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/955e3b88d3a648df83483810e90e794b~tplv-goo7wpa0wc-image.image) </span>

5. On the **Single sign\-on** page, enable the **Single sign\-on** option and specify the following values:

   * **Identity provider sign\-in URL**: Enter a URL using the following format: `https://example.sealsuite.net/api/idp/sso`

   * **X.509** **certificate**: Enter the X.509 certificate retrieved from SealSuite's Admin Portal.

      You can retrieve the X.509 Certificate using SealSuite's metadata URL in the following format: `https://example.sealsuite.net/api/idp/metadata`

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4bc1c771f4444b52aa0f568833ae88e6~tplv-goo7wpa0wc-image.image) </span>

6. In **SSO sign\-in URL**, click **Copy link** and save the link for later use.

   The link will be used as the Dropbox entity ID on SealSuite's Admin Portal.


<span id="6b9944f0"></span>
# Configuration on SealSuite's Admin Console


1. Log in to the Admin Console.

2. In the left navigation bar, click **Identity** \> **SSO**.

3. On the **SSO** page, click **Application Marketplace**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/07aa5cca80214f1eb91b0b08735dc6cb~tplv-goo7wpa0wc-image.image) </span>

4. On the **Add New Application** page, use filters to locate the Dropbox application template card and click on it.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c111065b6ed3491bb1a47244db55ffaf~tplv-goo7wpa0wc-image.image) </span>

5. In the lower right corner of the chosen template card, click **Add**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/27a9c80dc3114f8eb51dbc71ca3ce5e7~tplv-goo7wpa0wc-image.image) </span>

6. On the page that appears, complete the following steps to create your own Dropbox application.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/31e08817a42f468b809464ab0ddb9c33~tplv-goo7wpa0wc-image.image) </span>

   1. In the **General** section, specify **Application Name**, **Application Address**, and **Application Description**.

   2. In the **Application Type** section, you can:

      * View and download SealSuite's metadata file under **IDP Metadata**.

      * Fill in **Dropbox unique identifier** using the Dropbox entity ID that you saved earlier.

7. Click **Confirm** to save the configured settings.
