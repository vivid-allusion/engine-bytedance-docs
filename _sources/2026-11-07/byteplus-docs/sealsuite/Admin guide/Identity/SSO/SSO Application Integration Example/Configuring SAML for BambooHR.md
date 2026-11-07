---
title: "Configuring SAML for BambooHR"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-configuring-saml-for-bamboohr"
---

This article introduces how to configure SAML for your BambooHR application in the Admin Portal.

<span id="596824ff"></span>
# Uses

This article is divided into two parts:


* [Configuration on BambooHR Admin Portal](https://docs.byteplus.com/docs/sealsuite/docs-configuring-saml-for-bamboohr#808d842f)

* [Configuration on SealSuite's Admin Portal](https://docs.byteplus.com/docs/sealsuite/docs-configuring-saml-for-bamboohr#e8ca9569)


<span id="808d842f"></span>
# Configuration on BambooHR Admin Portal


1. Log in to the BambooHR Admin Portal as an administrator.

2. In the navigation bar, click the Settings icon \> **Apps**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/31a235f7a5fc40e8860c0e8da1d82156~tplv-goo7wpa0wc-image.image) </span>

3. In the **Not Installed** section of the **Apps Settings** page, locate the **SAML Single Sign\-On** application and click **Install** on the right side.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ed281bdd1004119befeda73b8e598d5~tplv-goo7wpa0wc-image.image) </span>

4. On the page that appears, specify the following values and click **Install**:

   * **SSO Login URL**: Enter a URL using the following format: `https://example.sealsuite.net/api/idp/sso`

   * **x.509 Certificate**: Enter the X.509 certificate retrieved from SealSuite's Admin Portal.

      You can retrieve the X.509 certificate using SealSuite's metadata URL in the following format: `https://example.sealsuite.net/api/idp/metadata`

   * **Allow optional email & password login**: Toggle the option to login through email and password if required.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/91bb4b8ecea04b7abb624d76970dd5f3~tplv-goo7wpa0wc-image.image) </span>


<span id="e8ca9569"></span>
# Configuration on SealSuite's Admin Console


1. Log in to the Admin Console.

2. In the left navigation bar, click **Identity** \> **SSO**.

3. On the **SSO** page, click **Application Marketplace**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/07aa5cca80214f1eb91b0b08735dc6cb~tplv-goo7wpa0wc-image.image) </span>

4. On the **Add New Application** page, use filters to locate the BambooHR application template card and click on it.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e2e03b075e22465b8dfdfd6481df9e2e~tplv-goo7wpa0wc-image.image) </span>

5. In the lower right corner of the chosen template card, click **Add**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a27ce80fcfaa4e74a5591da5940502d6~tplv-goo7wpa0wc-image.image) </span>

6. On the page that appears, complete the following steps to create your own BambooHR application.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d8f04b5acff41c792a082559d580dd4~tplv-goo7wpa0wc-image.image) </span>

   1. In the **General** section, specify **Application Name**, **Application Address**, and **Application Description**.

   2. In the **Application Type** section, you can:

      * View and download SealSuite's metadata file under **IDP Metadata**.

      * Fill in **Single sign\-on address for BambooHR** using the following URL: `https://{your_bamboohr_domain}.bamboohr.com/saml/consume.php`

7. Click **Confirm** to save the configured settings.
