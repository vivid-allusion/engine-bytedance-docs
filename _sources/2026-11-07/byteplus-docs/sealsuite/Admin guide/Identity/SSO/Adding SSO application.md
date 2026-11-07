---
title: "Adding SSO application"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-add-application"
---

By adding Single Sign\-On (SSO) applications, you can integrate your enterprise's required apps into the Admin Console, providing employees with a unified and convenient SSO experience. Once logged into SealSuit client App, employees can access all their authorized applications with a single click, without having to re\-enter their usernames and passwords.

This article describes how to add and configure Single Sign\-On applications in the admin console.

<span id="dabb9fb4"></span>
# Description of adding methods

You can add new applications to SealSuite either using our built\-in application templates or custom methods. Below are descriptions of these two options.


|**Method** |**Description** |
|---|---|
|**Add from application marketplace templates** |SealSuite provides pre\-configured integration templates for common enterprise Single Sign\-On (SSO) applications, allowing you to complete the SSO configuration quickly.<br><br>For example, after integrating an application like GitLab, employees can access it via SSO with a single click, eliminating the need to remember a separate password for GitLab. |
|**Add Custom Application** |If a pre\-built template for your application is not available, you can add it as a custom application based on the authentication protocol it supports.<br><br>SealSuite supports the following authentication protocols: CAS, OAuth 2.0, OIDC, SAML, and LDAP. |


<span id="7e8d7af2"></span>
# Adding a template application


1. Log in to the SealSuite Admin Console.

2. In the left navigation bar, select **Identity** \> **SSO**.

3. On the **SSO** page, click **Application Marketplace**.

4. On the **Add New Application** page, filter the specified application template in either of the following ways.

   * Method one: Type the app name into the search bar located on the left side of the page.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8c6faa8a6060407db1007152c6034ca7~tplv-goo7wpa0wc-image.image) </span>

   * Method two: In the **Filters** area on the left side of the page, filter the application template by **Category** or **Protocol Type**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e7e3b4b7ab794f10a48e5cf5bb6081a9~tplv-goo7wpa0wc-image.image) </span>

5. In the **Search Results** area, click the specified application template card.

6. In the lower right corner of the expanded application template description, click **Add New Application**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d95eba3e06a4b5c87f525a714dfcae9~tplv-goo7wpa0wc-image.image) </span>

7. On the **Fill in the application information** page, configure the application information and click **Confirm**.

   Different types of applications may require different configuration parameters; please configure them according to the specific use case. For instance, after selecting the GitLab application template, you need to configure the **General** and **Protocol** settings.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f1845048405342868b642c91b51c3592~tplv-goo7wpa0wc-image.image) </span>

   Using GitLab application integration as an example, the configuration instructions are as follows:

   1. In the **General** section, please enter the **Application name**, **Application address**, and **Application description**.

   2. In the **Protocol** area, complete the following configurations.

      
      |**Configuration Item** |**Description** |
      |---|---|
      |**OAuth 2.0** |After selecting this configuration item, you need to continue to configure the GitLab single sign\-on callback address. Format example: `http://HOST_NAME:PORT/users/auth/oauth2_generic/callback`. Please configure it according to the actual situation. |
      |**CAS** |After selecting this configuration item, you need to continue to configure the GitLab single sign\-on callback address. Format example: `http://HOST_NAME:PORT/users/auth/cas3/callback` Please configure according to the actual situation. |
      |**LDAP** |After selecting this configuration item, you need to continue to configure the password format. Options include **Static Password**, **OTP**, **Static Password + OTP**. |
      |**Password Autofill** |After selecting this configuration item, employees can automatically log in to applications through the password autofill feature. |
      

8. On the **Authorization** tab, set the application's usage scope.

   Support configuration of either **Full** or **Restricted** access.

   * **Full**: This application is available for all employees within the company.

   * **Restricted**: Access is granted based on **department**, **individual**, or **role** to define the scope of usage. For example, assigning the **R&D Department** in the **Department Permissions** area restricts application access to only those employees within the **R&D Department**.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">When setting up <strong>Restricted</strong>, there is an option to select <strong>Allow employees to apply</strong>. After selecting this configuration item, employees who have access rights can copy the app link and share it with those who do not have permissions. After accessing the link, unauthorized employees can apply to use the application.      </div>
      

<span id="53384ef6"></span>
# Adding a custom application


1. Log in to the SealSuite Admin Console.

2. In the left navigation bar, click on **Identity** \> **SSO**.

3. Navigate to the  **+ Custom Application** page using any of the following options.

   * Option one:

      In the upper right corner of the **Application SSO** page, click **Custom Application**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3e4cb800b66e48069adb044b9c1de392~tplv-goo7wpa0wc-image.image) </span>

   * Option two:

      1. On the **SSO** page, click **Application Marketplace**.

      2. On the **Add New Application** page, click **Custom Application** in the upper right corner.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5b665b085c334d5ab7ab5e4ac7beb582~tplv-goo7wpa0wc-image.image) </span>

4. On the **Add Custom Application** page, select a single sign\-on protocol type or app access method, and click the corresponding tab.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e103cc4aff734546b99352fc609fd2d4~tplv-goo7wpa0wc-image.image) </span>

5. On the **Fill in the application information** page, configure the application information and click **Confirm**.

   Different applications may need different configuration parameters; please configure them based on the specific requirements. For instance, once you select the CAS application card, you must configure the application's **General** settings and **Application Type**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a765123aa11e4726819e6b49e7a3f369~tplv-goo7wpa0wc-image.image) </span>

   Taking an application supporting the CAS authentication protocol as an example, the configuration instructions are as follows:

   1. In the **Basic Info** section, fill in the **Name**, **Application address**, and **Application Description**.

   2. In the **Application Type** section, complete the following configurations.

      
      |**Configuration Item** |**Description** |
      |---|---|
      |**Callback address** |Enter the callback address, supporting HTTP and HTTPS protocols. If you need to add multiple callback addresses, please use commas to separate them. |
      |**Single sign\-out address** |Select to enter the single sign\-out address, supporting HTTP and HTTPS protocols. |
      

6. On the **Authorization** tab, configure the usage scope of the application.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ce6587e243544898a8eb9e5fd98175ec~tplv-goo7wpa0wc-image.image) </span>

   Support configuration for **Full** or **Restricted**.

   * **Full**: This application is available for all employees within the company.

   * **Restricted**: Authorization of the usage scope is required by dimensions such as **Department**, **Individual**, or **Role**. For example, by adding **R&D Department in the Department Permissions** area, the application can only be used by employees within the **R&D Department**.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">When <strong>Restricted</strong> is configured, it supports selecting <strong>Allow employees to apply</strong>. After selecting this configuration item, employees with access permission to the application can copy the application link and share it with other employees without permissions. Employees without permissions can apply to use the application after accessing the link.      </div>
      

<span id="70d5da55"></span>
# Related documentation

Add the application to the application group so that users can view the corresponding application on the homepage of SealSuite client and SealSuite portal, please refer to [Configuring application group](https://docs.byteplus.com/docs/sealsuite/docs-configuring-client-application-grouping).
