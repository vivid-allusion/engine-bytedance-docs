---
title: "Configuring SAML for Zendesk"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-configuring-saml-for-zendesk"
---

This article introduces how to configure SAML for your Zendesk application in the Admin Portal.

<span id="5dbf2931"></span>
# Uses

This article is divided into two parts:


* [Configuration on your Zendesk Admin Center](https://docs.byteplus.com/docs/sealsuite/docs-configuring-saml-for-zendesk#2fbc5af3)

* [Configuration on SealSuite's Admin Portal](https://docs.byteplus.com/docs/sealsuite/docs-configuring-saml-for-zendesk#d296b0ae)


<span id="2fbc5af3"></span>
# Configuration on your Zendesk Admin Center


1. Log in to [Zendesk](https://www.zendesk.com/login/).

2. In the upper right corner of the homepage, click the specified menu icon.

3. In the list that appears, click **Admin Center**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a0bb9df0410b465bb5e86d787f219b6f~tplv-goo7wpa0wc-image.image) </span>

4. In the left navigation bar of the Admin Center homepage, click **Account** \> **Security** \> **Single sign\-on**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/130cc417e7c740af88ebbf9e5a96443e~tplv-goo7wpa0wc-image.image) </span>

5. On the **Single sign\-on** page, click **Create SSO configuration** and select **SAML** in the drop\-down list.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9311dd8ae809495da84bd07963b87dd3~tplv-goo7wpa0wc-image.image) </span>

6. On the configuration page, specify the following values:

   * **Configuration name**: Enter a name to identify the configuration.

      For demonstration, we use `SealSuite` as a sample configuration name.

   * **SAML SSO URL**: Enter a URL using the the following format:`https://example.sealsuite.net/api/idp/sso`

   * **Certificate fingerprint**: The fingerprint of an X.509 certificate is a digest of the whole certificate. Obtain your fingerprint by using the following steps:

      1. Retrieve an X.509 certificate from SealSuite's Admin Portal and format it [here](https://www.samltool.com/format_x509cert.php).

         You can obtain the X.509 certificate using SealSuite's metadata URL in the following format: `https://example.sealsuite.net/api/idp/metadata`

      2. In the **X.509 cert with header** section, copy the X.509 certificate with header.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8351f83c99740d8b31491c47aabd3b3~tplv-goo7wpa0wc-image.image) </span>

      3. Use the copied certificate to calculate the **SHA256** fingerprint [here](https://www.samltool.com/fingerprint.php).

      4. Obtain the fingerprint of your X.509 certificate in either the **FingerPrint** section or the **Formatted FingerPrint** section.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/61c65e68d3684caa8a25319551af006c~tplv-goo7wpa0wc-image.image) </span>

7. In the **SAML SSO URL** section, store the **Assertion Consumer Service (ACS) URL** for later use and click **Save**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cd4103fa264c44628f72f4c66efbf57a~tplv-goo7wpa0wc-image.image) </span>

8. Assign the newly created configuration to team members or end users by completing the steps below:

   1. In the left navigation bar, choose one of the following paths to assign the newly created configuration to team members or end users.

      * To assign the configuration to team members, click **Account** \> **Security** \> **Team member authentication**.

      * To assign the configuration to end users, click **Account** \> **Security** \> **End user authentication**.

         For demonstration, we will introduce how to assign the newly created configuration to team members.

   2. On the **Team member authentication** page, you can:

      * Assign the configuration to team members by completing the following steps:

         1. Select **External authentication** \> **Single sign\-on (SSO)**  \> the configuration that you created earlier.

            <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/434f76f92f0944eabb99653f8e88ce43~tplv-goo7wpa0wc-image.image) </span>

         2. Click **Save** to save the configured settings.

      * Assign the SSO authentication to administrators or the account owner when the external sign\-in provider doesn't work. To this end, you can use the following steps:

         1. Deselect the **Zendesk authentication** option and click **Save**.

            <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/47f53637743b48ce812a8a7b86493355~tplv-goo7wpa0wc-image.image) </span>

            Zendesk passwords for all team members will be permanently deleted within 24 hours.

         2. In the left navigation bar, click **Account** \> **Security** \> **Advanced**.

         3. On the **Advanced** page, click the **Authentication** tab.

            <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b350bd64e5e44a5798d135f366038dff~tplv-goo7wpa0wc-image.image) </span>

         4. In the **Authentication** tab, complete the following steps：

            1. In the **SSO bypass** section, select either **Account owner** or **Admins** (including the account owner).

               <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c12860c60ae84d46b336a3576752592d~tplv-goo7wpa0wc-image.image) </span>

            2. Click **Save** to save the configured settings.

               In this case, in order to gain access, the account owner or an admin must request to receive an email containing a one\-time access link. By clicking the link, the person will be granted access to the account, without the need to enter the password.


<span id="d296b0ae"></span>
# Configuration on SealSuite's Admin Console


1. Log in to the Admin Console.

2. In the left navigation bar, click **Identity** \> **SSO**.

3. On the **SSO** page, click **Application Marketplace**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/07aa5cca80214f1eb91b0b08735dc6cb~tplv-goo7wpa0wc-image.image) </span>

4. On the **Add New Application** page, use filters to locate the Zendesk application template card and click on it.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/25f5d41869c0400895a2812dcefd1605~tplv-goo7wpa0wc-image.image) </span>

5. In the lower right corner of the chosen template card, click **Add**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b1551ff0713748dd8ac86e6e23e94c2b~tplv-goo7wpa0wc-image.image) </span>

6. On the page that appears, complete the following steps to create your own Zendesk application.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/52497f55eb8443ebafa379eb4d120a42~tplv-goo7wpa0wc-image.image) </span>

   1. In the **General** section, specify **Application Name**, **Application Address**, and **Application Description**.

   2. In the **Application Type** section, you can:

      * View and download SealSuite's metadata file under **IDP Metadata**.

      * Fill in **Zendesk unique identifier** and **Single sign\-on address for Zendesk** using the following URLs:

         * **Zendesk unique identifier**:`https://{YOUR_DOMAIN}.zendesk.com`

         * **Single sign\-on address for Zendesk**:`http://{YOUR_DOMAIN}.zendesk.com/access/saml/`

7. Click **Confirm** to save the configured settings.

   The page automatically jumps to the **Authorization** tab of the newly created application.

8. In the **Authorization** tab, complete the steps below to configure user permissions:

   1. In the **User Permissions** section, click **Add Employee** to grant the corresponding users access to the application.

   2. In the pop\-up window, select your target users and click **Confirm**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/44e6c765d5d84ef5a086261c31270f31~tplv-goo7wpa0wc-image.image) </span>
