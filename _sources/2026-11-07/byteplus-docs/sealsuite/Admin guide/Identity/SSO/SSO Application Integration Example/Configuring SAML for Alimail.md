---
title: "Configuring SAML for Alimail"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-alimail-x-sealsuite-custom-sso"
---

This article introduces how to configure SAML for your Alimail application in the Admin Portal.

<span id="2dcde03c"></span>
# Uses

This article is divided into two parts:


* [Configuration on Alibaba Mail's Management Console](https://docs.byteplus.com/docs/sealsuite/docs-alimail-x-sealsuite-custom-sso#44054e8e)

* [Configuration on SealSuite's Admin Portal](https://docs.byteplus.com/docs/sealsuite/docs-alimail-x-sealsuite-custom-sso#397e7c0e)


<span id="44054e8e"></span>
# Configuration on Alibaba Mail's Management Console


1. Log in to [Alibaba Mail's Management Console](https://qiye.aliyun.com/alimail/auth/login?lang=en).

2. In the left navigation bar, click **Advanced** \> **Open API**.

3. On the **Open API** page, click **Add application**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f74d887dac434b02ab4aa2b10b271ac3~tplv-goo7wpa0wc-image.image) </span>

4. In the **Add application** section, enter an application name and select all the granted APIs.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2066cb8b5f5543f8ac623d1681a6b39a~tplv-goo7wpa0wc-image.image) </span>

5. Click **Save** to save the configured settings.

6. On the **Open API** page, locate the application you just created and click **Edit** on the right.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9a67954979e0479a86a8d450fc59daf9~tplv-goo7wpa0wc-image.image) </span>

7. In the **Edit application** section, store the **Application ID** and **Secret** for later use.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bcca60c44eee4f9e898fe27364577f29~tplv-goo7wpa0wc-image.image) </span>


<span id="397e7c0e"></span>
# Configuration on SealSuite's Admin Console


1. Log in to the Admin Console.

2. In the left navigation bar, click **Identity** \> **SSO**.

3. On the **SSO** page, click **Application Marketplace**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/07aa5cca80214f1eb91b0b08735dc6cb~tplv-goo7wpa0wc-image.image) </span>

4. On the **Add New Application** page, use filters to locate the Alimail application template card and click on it.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fa45f3db87a74443a7d6fd31c921c3d1~tplv-goo7wpa0wc-image.image) </span>

5. In the area below the chosen template card, click **Add**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3cccaaa0334e4973abe42ff52ae8e222~tplv-goo7wpa0wc-image.image) </span>

6. On the page that appears, complete the following steps to create an Alimail application.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d468950e99034b91a1cd66deb05fc59c~tplv-goo7wpa0wc-image.image) </span>

   1. In the **General** section, specify **Application Name** and **Application Description**.

   2. In the **Application Type** section, complete the following steps:

      1. Set **Server URL** to the corresponding values as required in the following scenarios:

         * For SaaS applications, use `https://mailsso.mxhichina.com`

         * For on\-premises applications, use your server URL.

      2. In **App Code**, fill in this option with the **Application ID** you saved earlier.

      3. In **App Secret**, fill in this option with the **Secret** you saved earlier.

7. Click **Confirm** to save the configured settings.

8. (Optional) If you have your own redirect URL, you can create a user custom attribute by following the steps below.

   After this step is completed, you can proceed to add users' redirect URLs by editing user details in the user list under **Identity** \> **Directory**. By default, the field name is empty and the redirect URL is `https://qiye.aliyun.com/`.

   1. In the left navigation bar, click **Account Setup.** 

   2. On the **Account Settings** page, click the **Advanced Settings** tab.

   3. In the **Advanced Settings** tab, click **Add Field**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bd27e2276e54463aaf6b5342269e1fdd~tplv-goo7wpa0wc-image.image) </span>

   4. On the **Add Custom Attribute** page, complete the following steps and click **Confirm**:

      1. Set the **Field Key** to `alimail_url`.

      2. Label your attribute with any value you deem suitable using the **Field Name**.

      3. Select a data type in the **Field Type** section, and enter your redirect URL as the **Default value**.

      4. (Optional) In the **Advanced configuration** section, select your desired configuration item.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a0e55e562d2840008b92f0c7662db12a~tplv-goo7wpa0wc-image.image) </span>
