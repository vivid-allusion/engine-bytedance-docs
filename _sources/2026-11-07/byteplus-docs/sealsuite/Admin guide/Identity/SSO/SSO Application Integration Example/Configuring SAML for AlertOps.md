---
title: "Configuring SAML for AlertOps"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-the-alertops"
---

This article introduces how to configure SAML for your AlertOps application in the Admin Portal.

<span id="0bfcc228"></span>
# Uses

This article is divided into two parts:


* [Configuration on AlertOps](https://docs.byteplus.com/docs/sealsuite/docs-the-alertops#e844994a)

* [Configuration on SealSuite's Admin Portal](https://docs.byteplus.com/docs/sealsuite/docs-the-alertops#5d2d6b46)


<span id="e844994a"></span>
# Configuration on AlertOps


1. Log in to your AlertOps account.

2. In the upper right corner of the screen, navigate to your User Account settings and click **Account Settings**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c2db7aa004bf4302b2259780e55fed23~tplv-goo7wpa0wc-image.image) </span>

3. On the **Account Settings** page, click **Update SSO** and check the **Use single sign\-on (SSO)**  box.

4. In the **SSO** section, complete the following steps:

   1. In **Issuer URL**, enter `https://example.sealsuite.net/api/idp/metadata`

   2. In **SAML endpoint URL**, enter `https://example.sealsuite.net/api/idp/sso`

   3. (Optional) In **SLO endpoint URL**, enter `https://example.sealsuite.net/api/idp/slo`

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Replace <code>example.sealsuite.net</code> with your own domain.      </div>
      

   4. In **SAML Signature Algorithm**, select **SHA256**.

   5. In **X.509 Certificate**, enter your identity provider's X.509 certificate.

      To obtain an X.509 certificate, use the Issuer URL that you have specified.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8bab3a036d064591a37dd9d26e2f4fb2~tplv-goo7wpa0wc-image.image) </span>

5. On the upper right corner of the **SSO** section, click the green tick icon to save the details.


<span id="5d2d6b46"></span>
# Configuration on SealSuite's Admin Console


1. Log in to the Admin Console.

2. In the left navigation bar, click **Identity** \> **SSO**.

3. On the **SSO** page, click **Application Marketplace**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/07aa5cca80214f1eb91b0b08735dc6cb~tplv-goo7wpa0wc-image.image) </span>

4. On the **Add New Application** page, use filters to locate the AlertOps application template card and click on it.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/386830c729064b52b6ebdd36cf40e9a9~tplv-goo7wpa0wc-image.image) </span>

5. In the lower right corner of the chosen template card, click **Add**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/12f776e745b64ff8ac36450833836f20~tplv-goo7wpa0wc-image.image) </span>

6. On the page that appears, complete the following steps to create your own AlertOps application.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f2d3d584b93340e1a21a4235ef0e3546~tplv-goo7wpa0wc-image.image) </span>

   1. In the **General** section, specify **Application Name**, **Application Address**, and **Application Description**.

   2. In the **Application Type** section, you can:

      * View or download SealSuite's metadata file under **IDP Metadata**.

      * Fill in the **AlertOps Entity ID** and **AlertOps SSO URL** using the corresponding formats:

         * **AlertOps Entity ID**: `https://app.alertops.com/{YOUR_DOMAIN}`

         * **AlertOps SSO URL**: `https://api.alertops.com/api/v2/saml/{YOUR_DOMAIN}`

7. Click **Confirm** to save the configured settings.
