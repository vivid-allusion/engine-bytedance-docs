---
title: "Configuring SAML for Notion"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-configuring-saml-for-notion"
---

This article introduces how to configure SAML for your Notion application in the Admin Portal.

<span id="8eb27d3e"></span>
# Uses

This article is divided into two parts:


* [Configuration on your Notion workspace](https://docs.byteplus.com/docs/sealsuite/docs-configuring-saml-for-notion#e347315a)

* [Configuration on SealSuite's Admin Portal](https://docs.byteplus.com/docs/sealsuite/docs-configuring-saml-for-notion#0d8161e7)


<span id="e347315a"></span>
# Configuration on your Notion workspace


1. Log in to your organization's Notion workspace as a workspace owner.

2. In the left navigation bar, click **Settings & Members**.

3. In the left navigation bar of the pop\-up window, click **Identity & provisioning**.

4. On the page that appears, verify your email domain under the **Domain management** section.

   For demonstration, we use `test-sso.sealsuite.net` as a sample domain name.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6ca9f07422b747fbba5667743a37046d~tplv-goo7wpa0wc-image.image) </span>

5. Under the **SAML Single sign\-on (SSO)**  section, toggle the **Enable SAML SSO** option.

6. On the pop\-up window, complete the following steps and click **Enable SAML**:

   1. Copy and save the **Assertion Consumer Service URL** for later use.

   2. Select **Identity Provider URL** and enter a URL based on the SealSuite server you use.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f520709c714d4e3aa713b4a7730fcb08~tplv-goo7wpa0wc-image.image) </span>

   3. Select **Identity Provider Metadata XML** and enter the metadata retrieved from SealSuite's Admin Portal.

      You can retrieve the metadata using SealSuite's metadata URL in the following format: `https://example.sealsuite.com/api/idp/metadata`

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0752dc1a537d42ac9bc7955d5d70f2b0~tplv-goo7wpa0wc-image.image) </span>

7. (Optional) Adjust your login method and enable the **Automatic account creation** option.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/859123cc5c3f432a92e6bb83da0a286a~tplv-goo7wpa0wc-image.image) </span>


<span id="0d8161e7"></span>
# Configuration on SealSuite's Admin Console


1. Log in to the Admin Console.

2. In the left navigation bar, click **Identity** \> **SSO**.

3. On the **SSO** page, click **Application Marketplace**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/07aa5cca80214f1eb91b0b08735dc6cb~tplv-goo7wpa0wc-image.image) </span>

4. On the **Add New Application** page, use filters to locate the Notion application template card and click on it.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d8acd231ec294e0bb0e7a5fc13a00bab~tplv-goo7wpa0wc-image.image) </span>

5. In the lower right corner of the chosen template card, click **Add**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c8173fa18ea94879aa4938d8a5e352e9~tplv-goo7wpa0wc-image.image) </span>

6. On the page that appears, complete the following steps to create your own Notion application.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5660c0d3bfc6491dae76146021207aaf~tplv-goo7wpa0wc-image.image) </span>

   1. In the **General** section, specify **Application Name**, **Application Address**, and **Application Description**.

   2. In the **Application Type** section, you can:

      * View and download SealSuite's metadata file under **IDP Metadata**.

      * Fill in **Single sign\-on address for Notion** using the **Assertion Consumer Service URL** you saved earlier.

7. Click **Confirm** to save the configured settings.
