---
title: "Configuring password autofill rules"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-configuring-proxy-login"
---

For applications that support standard protocols, SealSuit recommends using Single Sign\-On (SSO) to achieve the highest level of security and integration. For legacy systems or third\-party web applications that do not support SSO, SealSuit also offers Password Autofill as an alternative solution.

Password Autofill uses a browser extension to automatically fill user credentials, seamlessly integrating non\-SSO applications into the SealSuit portal to provide a unified access point. During this process, the extension does not transmit the username and password to the browser, ensuring maximum user account security.

This article details the configuration process for Password Autofill.

<span id="78821061"></span>
## Step 1: Adding an application


1. Log in to the Admin Console.

2. In the left navigation bar, select **Identity** \> **SSO**.

3. On the **SSO** page, click **Application Marketplace**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2be13b23af7a4f0a8b445b10bccb333a~tplv-goo7wpa0wc-image.image) </span>

4. On the **Add New Application** page, use the filters on the left to find and select **Password Autofill** template.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/83ac06e9ef8f432cb2bce40364657505~tplv-goo7wpa0wc-image.image) </span>

5. Select the application you want to add, click the application card and then click  **+ Add New Application**.

   To understand the functions of application templates, please refer to [Adding SSO application](https://docs.byteplus.com/docs/sealsuite/docs-add-application).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/86668f4e941d45b4a1707a07de1aed06~tplv-goo7wpa0wc-image.image) </span>

6. On the **Fill in the application information** page, complete the following configurations and click **Confirm**.

   After that, the page will automatically jump to the configuration page of the application.

   
   |**Items** |**Required** |**Description** |
   |---|---|---|
   |Application Name |Yes |Enters the name of the current application in SealSuite. |
   |Application Address |No |Enters the access address of the current application. |
   |Application Description |No |Enters the description of current application, which helps users understand the main functions of the current application. |
   

   Upon completion, you will be automatically redirected to the '**Login Configuration**' tab for that application.


<span id="bd58a374"></span>
## Step 2: Configuring account assignment policy for the application

When configuring the policy, the system supports adding policies individually as well as bulk import and export functionality.

<span id="ad0ba253"></span>
### Adding policies individually


1. In the **Login configuration** tab, click **Add New** **Policy**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aa0748eee94d452a8c122eec53771e98~tplv-goo7wpa0wc-image.image) </span>

2. In the **Add New Policy** pop\-up box, complete the following configurations, and click **OK**.

   
   |**Items** |**Required** |**Description** |
   |---|---|---|
   |Policy Name |Yes |Enters the name of the current rule. It is suggested to use a combination of account number and authorization object to facilitate distinction and memory. For example, if you need to assign the current ShiMo account to a financial role, you can name the rule "ShiMo Finance Shared Account". |
   |Account |Yes |Enters the account name for which the rule takes effect. |
   |Password |Yes |Enters the app account password for which the rule takes effect. |
   |Scope |Yes |Specifies the scope for which the rule takes effect. |
   


<span id="c84a9cb9"></span>
### Importing policies


1. In the **Login configuration** tab, click **Import**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fa3d6ec9cc42436aa04cc5f5a5337ba7~tplv-goo7wpa0wc-image.image) </span>

2. Download the template.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d1ddd6289fda429badd8f008dffac7ce~tplv-goo7wpa0wc-image.image) </span>

3. The downloaded file will be named `import-template.xlsx`. Open the file and populate the data according to the instructions provided within it.

4. After completing the file, return to the admin console, upload the file.


<span id="d306764c"></span>
### Exporting policies

To export your configured policies, go to the **Login Configuration** tab and click the **Export** button.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9b47aa45c9b84fb89d815f8634859232~tplv-goo7wpa0wc-image.image) </span>

You'll need to check the export status by clicking the progress icon on the right. When the process is finished, click **Download** to save the file.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6b98576ab90c4754b5791277f12f2848~tplv-goo7wpa0wc-image.image) </span>

Usage notes:


* Export Options: You'll be prompted to choose between exporting all policies or just the ones you've selected. You can also select your preferred file format: CSV (.csv) or Excel (.xlsx).

* Passwords Not Included: Please note that passwords are not included in the exported file for security purposes. If you plan to import these policies into another application, you will need to manually add the necessary credentials to the file after exporting and before importing.


<span id="c69cab00"></span>
## Step 3: Installing the browser extension for password autofill


1. In the SealSuit portal, the employee clicks the icon of an application configured for Password Autofill.

2. Because the extension is not yet installed, the user will be automatically redirected to the extension installation guide page.

3. The employee clicks **Download Plugin** and follows the on\-screen tutorial to complete the installation and enablement of the extension.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ad593b66bcf74953b4a42815be14b664~tplv-goo7wpa0wc-image.image) </span>


Upon successful installation, when the employee clicks the application icon again, the browser will automatically redirect to the application's login page. The extension will then autofill and submit the user's credentials, completing the automatic login process.
