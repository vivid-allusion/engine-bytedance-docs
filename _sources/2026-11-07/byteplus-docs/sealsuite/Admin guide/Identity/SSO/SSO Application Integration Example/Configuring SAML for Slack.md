---
title: "Configuring SAML for Slack"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-configuring-saml-for-slack"
---

This article introduces how to configure SAML for your Slack application in the Admin Portal.

<span id="f993cbea"></span>
# Uses

This article is divided into two parts:


* [Configuration on your Slack workspace](https://docs.byteplus.com/docs/sealsuite/docs-configuring-saml-for-slack#c1c5510c)

* [Configuration on SealSuite's Admin Portal](https://docs.byteplus.com/docs/sealsuite/docs-configuring-saml-for-slack#840305cb)


<span id="c1c5510c"></span>
# Configuration on your Slack workspace


1. Log in to your organization's Slack workspace as a workspace owner.

2. In the left navigation bar, click on your organization's name \> **Settings & administration** \> **Workspace settings**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/91ecb12efb2d4e23b2e028e48bfe6860~tplv-goo7wpa0wc-image.image) </span>

3. On the **Settings & Permissions** page, click the **Authentication** tab.

4. In \*\*\*\* the **Configure an authentication method** section, locate **SAML authentication** and click **Upgrade** to go to the page where you can upgrade your plan.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cafa3206fbe14f258cc3674e7d8816e3~tplv-goo7wpa0wc-image.image) </span>

5. On the page that appears, choose the **Business+**  plan to use SAML authentication.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e41ea0b134f247e0a833cf4257a0e382~tplv-goo7wpa0wc-image.image) </span>

6. After a Business+ account is created, navigate to the **Settings & Permissions** page and click the **Authentication** tab.

7. On the right side of **SAML authentication**, click **Configure**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/15eaf6daf8ab48c4a184b22b6e659c71~tplv-goo7wpa0wc-image.image) </span>

8. On the pane that appears, specify the following values:

   1. **SAML 2.0 Endpoint (HTTP)** : Enter a URL using the following format: `https://example.sealsuite.com/api/idp/sso`

   2. **Identity Provider Issuer**: Enter a URL using the following format: `https://example.sealsuite.com/api/idp/metadata`

   3. **Public Certificate**: Enter the X.509 certificate retrieved from SealSuite's Admin Portal.

      You can retrieve the X.509 Certificate using SealSuite's metadata URL in the following format: `https://example.sealsuite.com/api/idp/metadata`

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f41c3820b8ca4999b8c2027e51f57b5b~tplv-goo7wpa0wc-image.image) </span>

9. In the **Advanced** **Options** section, complete the steps below:

   1. Select \*\*Sign`AuthnRequest` \*\*and save the X.509 certificate for later use.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2985bcdb8f234a9e83ee42dcc79b2312~tplv-goo7wpa0wc-image.image) </span>

   2. In **Service Provider Issuer**, enter the following URL:`https://{WORKSPACE_NAME}/slack.com`

   3. Check **Responses Signed** and **Assertions Signed**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/481fd20cf3e542c6a651b36eced96193~tplv-goo7wpa0wc-image.image) </span>

10. In the **Settings** section, select your desired options for SAML authentication and click **Save Configuration**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb62fa2c04c54a1ca6b70a47adfa88ce~tplv-goo7wpa0wc-image.image) </span>

11. Make sure you land on the confirmation page as shown below.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/060c7b29ec234916b9df1c2ec64218fd~tplv-goo7wpa0wc-image.image) </span>


<span id="840305cb"></span>
# Configuration on SealSuite's Admin Console


1. Log in to the Admin Console.

2. In the left navigation bar, click **Identity** \> **SSO**.

3. On the **SSO** page, click **Application Marketplace**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/07aa5cca80214f1eb91b0b08735dc6cb~tplv-goo7wpa0wc-image.image) </span>

4. On the **Add New Application** page, use filters to locate the Slack application template card and click on it.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/73271b19b32944878cbc7bef652f1abb~tplv-goo7wpa0wc-image.image) </span>

5. In the lower right corner of the chosen template card, click **Add**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1fd7e52d3660459198851ba203afea8d~tplv-goo7wpa0wc-image.image) </span>

6. On the page that appears, complete the following steps to create your own Slack application.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6106f62d85704e5ca7a9770343d9f555~tplv-goo7wpa0wc-image.image) </span>

   1. In the **General** section, specify **Application Name**, **Application Address**, and **Application Description**.

   2. In the **Application Type** section, you can:

      * View and download SealSuite's metadata file under **IDP Metadata**.

      * Upload Slack's metadata file under **Slack Metadata file**.

         Slack's metadata file can be created using the X.509 certificate that \*\*\*\* you saved earlier.

7. Click **Confirm** to save the configured settings.

8. (Optional) Configure SAML request data by adding user attributes as shown below.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/875cdfc9bd414f0e8249c46989ae9657~tplv-goo7wpa0wc-image.image) </span>
