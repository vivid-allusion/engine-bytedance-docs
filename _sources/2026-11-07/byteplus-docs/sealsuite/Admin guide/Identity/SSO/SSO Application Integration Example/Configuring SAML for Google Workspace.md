---
title: "Configuring SAML for Google Workspace"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-configuring-saml-for-google-workspace"
---

This article introduces how to configure SAML for your Google application in the Admin Portal.

<span id="0abc053e"></span>
# Uses

This article is divided into two parts:


* [Configuration on Google Admin Console](https://docs.byteplus.com/docs/sealsuite/docs-configuring-saml-for-google-workspace#3b3e5bb2)

* [Configuration on SealSuite's Admin Portal](https://docs.byteplus.com/docs/sealsuite/docs-configuring-saml-for-google-workspace#819d0e5d)


<span id="3b3e5bb2"></span>
# Configuration on Google Admin Console


1. Log in to [Google Admin console](https://admin.google.com/) with an administrator account.

2. In the left navigation bar, click **Security** \> **Overview**.

3. On the page that appears, click the **Set up Single Sign\-On (SSO) with a third\-party IdP** option.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4fae4c3d1be6415391e42877be0939fd~tplv-goo7wpa0wc-image.image) </span>

4. On the pane that appears, specify the following values and configure necessary settings for SAML SSO.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For demonstration, we set up SSO for the entire organisation by editing the <strong>Third\-party SSO profile for your organisation</strong> section. To set up SSO for organisation units or groups, edit the <strong>Third\-party SSO profiles</strong> section.   </div>
   

   * **Sign\-in page URL**: Enter a URL using the following format:`https://example.sealsuite.net/api/idp/sso`

      This endpoint is used by Google to send a SAML request to SealSuite. For more information on relevant endpoints used by Google, refer to [Single Sign-on](https://cloud.google.com/architecture/identity/single-sign-on).

   * **Sign\-out page URL**: Enter a URL using the following format:`https://example.sealsuite.net/`

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d79af4ec52ea439ca85555a7bea52725~tplv-goo7wpa0wc-image.image) </span>


<span id="819d0e5d"></span>
# Configuration on SealSuite's Admin Console


1. Log in to the Admin Console.

2. In the left navigation bar, click **Identity** \> **SSO**.

3. On the **SSO** page, click **Application Marketplace**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/07aa5cca80214f1eb91b0b08735dc6cb~tplv-goo7wpa0wc-image.image) </span>

4. On the **Add New Application** page, use filters to locate the Google Workspace application template card and click on it.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0bf787edcd8046aa81ea62c91d612bf6~tplv-goo7wpa0wc-image.image) </span>

5. In the lower right corner of the chosen template card, click **Add**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e666b561b2694978a7ef87af0c49c256~tplv-goo7wpa0wc-image.image) </span>

6. On the page that appears, complete the following steps to create your own Google application.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3b619325b1f74d6dad1e369bdba04bcc~tplv-goo7wpa0wc-image.image) </span>

   1. In the **General** section, specify the following values:

      * **Application Name**: Enter a name to identify the application.

      * **Application Address**: Enter an address using the following URL: `https://www.google.com/a/{YOUR_DOMAIN}/ServiceLogin?continue=https://console.cloud.google.com/`

      * **Application Description**: Provide a description of the application if necessary.

   2. In the **Application Type** section, you can:

      * View and download SealSuite's metadata file under **IDP Metadata**.

      * Fill in **Single sign\-on address for Google** using the following URL: `https://www.google.com/a/{YOUR_DOMAIN}/acs`

7. Click **Confirm** to save the configured settings.
