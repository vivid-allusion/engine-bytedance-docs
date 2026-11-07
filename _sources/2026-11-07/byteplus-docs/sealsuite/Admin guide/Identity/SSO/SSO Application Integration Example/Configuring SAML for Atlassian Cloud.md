---
title: "Configuring SAML for Atlassian Cloud"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-configuring-saml-for-atlassian"
---

This article introduces how to configure SAML for your Atlassian Cloud application in the Admin Portal.

<span id="137be3fd"></span>
# Uses

This article is divided into two parts:


* [Configuration on Atlassian Admin Portal](https://docs.byteplus.com/docs/sealsuite/docs-configuring-saml-for-atlassian#3c7f97dd)

* [Configuration on SealSuite's Admin Portal](https://docs.byteplus.com/docs/sealsuite/docs-configuring-saml-for-atlassian#1c3df606)


<span id="3c7f97dd"></span>
# Configuration on Atlassian Admin Portal


1. Log in to [Atlassian Admin Portal](https://id.atlassian.com/login?).

2. In the navigation bar, click **Settings** \> **Domains**.

3. On the **Domains** page, verify ownership of your domain by using one of the following methods:

   * DNS: Copy a TXT record to your domain name system (DNS).

   * HTTPS: Upload an HTML file to the root folder of your domain's website.

      For demonstration, we use `test-sso.sealsuite.net` as a sample domain name. After you verify your domain and claim accounts, all the Atlassian accounts with email addresses from the domain are managed by your organization.

   <div style="text-align: right">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eedab1cbd2e74ff1a87b5ecf98dba2ed~tplv-goo7wpa0wc-image.image" width="865px" />   </div>
   

4. In the top navigation bar, click **Security**.

5. On the page that appears, select **Start your 30\-day free trial** to begin your Atlassian Access trial.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8632c739be7d4d41aa1fce1cbe330d55~tplv-goo7wpa0wc-image.image) </span>

   Atlassian Access uses a different billing model from other Atlassian cloud products. For more details, refer to [Understand Atlassian Access](https://www.atlassian.com/software/access/pricing).

6. In the navigation bar, click **Security** \> **Identity providers**.

7. Complete the steps below by following the instructions on the Atlassian Admin Portal:

   1. Add an identity provider.

   2. Name your identity provider directory.

   3. Link the verified domain to your identity provider directory.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5d4f2c884b5147099b730da56c1edbf6~tplv-goo7wpa0wc-image.image) </span>

8. In the navigation bar, click **Security** \> **Authentication policies**.

9. On the page that appears, create an authentication policy to test your SAML configuration.

10. On the **SAML configuration** page, specify the following values for your Identity Provider:

* **Identity provider Entity ID**: Enter a URL using the following format: `https://example.sealsuite.net/api/idp/metadata`

* **Identity provider SSO URL**: Enter a URL using the following format: `https://example.sealsuite.net/api/idp/sso`

* **X.509 certificate**: Enter the X.509 certificate retrieved from SealSuite's Admin Portal.

   You can retrieve the X.509 certificate using SealSuite's metadata URL in the following format: `https://example.sealsuite.net/api/idp/metadata`


<span id="1c3df606"></span>
# Configuration on SealSuite's Admin Console


1. Log in to the Admin Console.

2. In the left navigation bar, click **Identity** \> **SSO**.

3. On the **SSO** page, click **Application Marketplace**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/07aa5cca80214f1eb91b0b08735dc6cb~tplv-goo7wpa0wc-image.image) </span>

4. On the **Add New Application** page, use filters to locate the Atlassian Cloud application template card and click on it.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/85c3decfe6bc4813b38c474756e0c5a3~tplv-goo7wpa0wc-image.image) </span>

5. In the lower right corner of the chosen template card, click **Add**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5d4ae2b1852641678bb11d82cfbce994~tplv-goo7wpa0wc-image.image) </span>

6. On the page that appears, complete the following steps to create your own Atlassian Cloud application.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/79d8e03d85184d81b57d218775b9a325~tplv-goo7wpa0wc-image.image) </span>

   1. In the **General** section, specify **Application Name**, **Application Address**, and **Application Description**.

   2. In the **Application Type** section, you can:

      * View and download SealSuite's metadata file under **IDP Metadata**.

      * Fill in **Atlassian unique identifier** and **Single sign\-on address for Atlassian** by using the values you have obtained from the SAML configuration page in the Atlassian Admin Portal.

         * **Atlassian unique identifier**: Fill in this option using the **Service Provider entity URL** from Atlassian.

         * **Single sign\-on address for Atlassian**: Fill in this option using the **Service Provider assertion consumer service URL** from Atlassian.

7. Click **Confirm** to save the configured settings.

   The page automatically jumps to the **Authorization** tab of the newly created application.

8. In the **Authorization** tab, complete the following steps to configure user permissions:

   1. In the **User Permissions** section, click **Add Employee** to grant the corresponding users access to the application.

   2. In the pop\-up window, select your target users and click **Confirm**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4bbd50e8b5214aa2ba7f307c6037f8ef~tplv-goo7wpa0wc-image.image) </span>
