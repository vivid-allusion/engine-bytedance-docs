---
title: "Configuring SAML for 15Five"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-15five-x-sealsuite-saml"
---

This article introduces how to configure SAML for your 15Five application in the Admin Portal.

<span id="63c874a3"></span>
# Uses

This article is divided into two parts:


* [Configuration on 15Five Admin Portal](https://docs.byteplus.com/docs/sealsuite/docs-15five-x-sealsuite-saml#842c304a)

* [Configuration on SealSuite's Admin Portal](https://docs.byteplus.com/docs/sealsuite/docs-15five-x-sealsuite-saml#22699266)


<span id="842c304a"></span>
# Configuration on 15Five Admin Portal


1. Log in to the 15Five Admin Portal.

2. In the upper right corner of the homepage, click on **Settings** \> **Company settings**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2caed90d1b744ec3acb75479baf25820~tplv-goo7wpa0wc-image.image) </span>

3. On the page that appears, click on **SSO** \> **Getting Started**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7c92cf180ddd478d83b6ee3ddf50d392~tplv-goo7wpa0wc-image.image) </span>

4. In the **Getting Started** tab, specify the subdomain that you want to use on 15Five and click **Save**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you have changed your subdomain, you need to re\-login to the 15Five Admin Portal.   </div>
   

5. Use the provided metadata URL to obtain a Service Provider(SP) metadata file.

   Save the metadata file in XML format for later use.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d546b1303b84785947e00b619c1dea7~tplv-goo7wpa0wc-image.image) </span>

6. On the **Single Sign\-On** page, click the **Metadata & Contact** tab.

7. In the **Metadata & Contact** tab, complete the following steps:

   1. Specify a **Contact Email** that serves as the point of contact for SSO inquiries.

   2. Enable the **Automatically update metadata** option and enter your identity provider's metadata URL using the following format: `https://example.sealsuite.net/api/idp/metadata`.

   3. Copy metadata from the specified metadata URL and paste it under **XML metadata**.

   4. Click **Save**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cca9b458f4864ec8a0e5e43dea6adfaa~tplv-goo7wpa0wc-image.image) </span>

8. On the **Single Sign\-On** page, click the **Details** tab.

9. On the page that appears, complete the following steps and click **Save**:

   1. Set **IdP Single Sign\-On Service Binding** to **HTTP POST**.

   2. In the **User Attributes** section, you need to:

      1. Set **Name ID Contents** to **Email**.

      2. Set **Email attribute name** to **email**.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eab39ea9e15e4d78943e73cc012eb52e~tplv-goo7wpa0wc-image.image) </span>


<span id="22699266"></span>
# Configuration on SealSuite's Admin Console


1. Log in to the Admin Console.

2. In the left navigation bar, click **Identity** \> **SSO**.

3. On the **SSO** page, click **Application Marketplace**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/07aa5cca80214f1eb91b0b08735dc6cb~tplv-goo7wpa0wc-image.image) </span>

4. On the **Add New Application** page, use filters to locate the 15Five application template card and click on it.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/433fef5188a94672be72a35fc44f44d6~tplv-goo7wpa0wc-image.image) </span>

5. In the lower right corner of the chosen template card, click **Add**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ff3e1cc254c34d75a16e7dd2f73fd428~tplv-goo7wpa0wc-image.image) </span>

6. On the page that appears, complete the following steps to create your own 15Five application.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8371fb4c72824e83aee9ecc0d5a2cc2c~tplv-goo7wpa0wc-image.image) </span>

   1. In the **General** section, specify **Application Name**, **Application Address**, and **Application Description**.

   2. In the **Application Type** section, you can:

      * View or download SealSuite's metadata file under **IDP Metadata**.

      * Upload the SP metadata file that you saved earlier under **15five Metadata File**.

7. Click **Confirm** to save the configured settings.
