---
title: "Configuring SAML for AssetSonar"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-assetsonar-x-sealsuite-saml"
---

This article introduces how to configure SAML for AssetSonar applications in the Admin Portal.

<span id="5825e415"></span>
# Uses

This article is divided into two parts:


* [Configuration on AssetSonar's Admin Portal](https://docs.byteplus.com/docs/sealsuite/docs-assetsonar-x-sealsuite-saml#6d03420c)

* [Configuration on SealSuite's Admin Portal](https://docs.byteplus.com/docs/sealsuite/docs-assetsonar-x-sealsuite-saml#17e9ea50)


<span id="6d03420c"></span>
# Configuration on AssetSonar's Admin Portal


1. Log in to your AssetSonar Admin Portal.

2. On the upper right corner of the **Dashboard** page, click the gear icon.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3ffb4d347e2540238db97f088b299520~tplv-goo7wpa0wc-image.image) </span>

3. On the page that appears, click the **ADD ONS** tab.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9da3a4d1857f4d3e946e9a854934cfaf~tplv-goo7wpa0wc-image.image) </span>

4. In the left navigation area below the search bar, locate **SAML Integration** and click it.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/90a41dbac7ad44bd8e5c498f58fa1d1f~tplv-goo7wpa0wc-image.image) </span>

5. In the **SAML Integration** section, enable **SAML Integration** and configure the provided configuration items on the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6fce824c63ba44e88589865f51975a46~tplv-goo7wpa0wc-image.image) </span>

   1. **Identity Provider URL**: Set it to a link using the following format: `https://example.sealsuite.net/api/idp/sso`

   2. **Identity Provider Certificate**: Fill in an X.509 certificate and restore its format by completing the steps below.

      1. To obtain an X.509 certificate formatted in a certain way, copy the X.509 certificate from the metadata URL of your SealSuite application such as `https://example.sealsuite.net/api/idp/metadata` and format it [here](https://www.samltool.com/format_x509cert.php).

      2. After the format conversion is completed, copy the value in the **X.509 cert with header** section and paste it under the **Identity Provider Certificate** option.

6. Save the **AssetSonar consumer service url** for later use.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f2a63409f8d84ebbb7f9b81ddd58d62a~tplv-goo7wpa0wc-image.image) </span>

7. In the upper right corner of the **ADD ONS** page, click **UPDATE** to save your changes.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fffc1fcfc6084093807b5a6c360e34b9~tplv-goo7wpa0wc-image.image) </span>


<span id="17e9ea50"></span>
# Configuration on SealSuite's Admin Console


1. Log in to the Admin Console.

2. In the left navigation bar, click **Identity** \> **SSO**.

3. On the **SSO** page, click **Application Marketplace**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/07aa5cca80214f1eb91b0b08735dc6cb~tplv-goo7wpa0wc-image.image) </span>

4. On the **Add New Application** page, use filters to locate the AssetSonar application template card and click on it.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ad644ac1c98b4d04884308b62969f1ce~tplv-goo7wpa0wc-image.image) </span>

5. In the lower right corner of the chosen template card, click **Add**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6d3450da4fd341679d01c1d268fbff9e~tplv-goo7wpa0wc-image.image) </span>

6. On the page that appears, complete the following steps to create an AssetSonar application.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/44ae3188ebf44c41bf47049652f9b1b6~tplv-goo7wpa0wc-image.image) </span>

   1. In the **General** section, specify **Application Name**, **Application Address**, and **Application Description**.

   2. In the **Application Type** section, you can:

      * View or download SealSuite's metadata file under the **IDP Metadata** option.

      * Fill in **AssetSonar SSO URL** using the **AssetSonar consumer service URL** that you saved earlier.

7. Click **Confirm** to save the configured settings.
