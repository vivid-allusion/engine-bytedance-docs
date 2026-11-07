---
title: "Configuring CAS authentication source"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-o9681n8i40"
---

To facilitate the authentication and login of enterprise users, SealSuite supports CAS2.0 protocol as the authentication source to meet the access requirements of enterprise\-owned authentication sources. Configuring the protocol as the authentication source enables users to log in to each application system more easily. This article introduces how to configure CAS2.0 authentication source.

<span id="c85c9e77"></span>
# Protocol Introduction

CAS (Central Authentication Service) protocol is a protocol for centralized authentication and single sign\-on in web applications. It allows users to access multiple applications without repeatedly entering usernames and passwords. Users only need to log in once to access all applications registered with the CAS server. The CAS protocol achieves single sign\-on through the use of tickets, which contain the user's identity information and are passed between multiple applications.

<span id="a64ee34d"></span>
# Prerequisites


* You have created a CAS application in a CAS\-certified source.

* You have copied the following redirect address to your CAS authentication source.

   `https://staging.feilian.cn/api/tpslogin/callback/custom_cas`


<span id="2e39195d"></span>
# Configuring CAS Authentication Source


1. Log in to the Admin Console.

2. In the left navigation bar, select **Identity** \> **Account Setup** \> **Third\-Party Login**.

3. On the **Third\-Party Login** tab, click **Add Login Source** in the upper right corner.

4. In the **Select Login Source** dialog box, click the **CAS** card.

5. Set the CAS authentication source parameters as prompted. The key parameters are described as follows. After completing the configuration, click **Confirm**.

   
   |**Module** |**Configuration Item** |**Required** |**Description** |
   |---|---|---|---|
   |**General** |**Login display icon** |Yes |The identity source icon displayed on the login interface button, click **Upload** to upload the custom display icon. |
   ||**Login Abbreviation (Chinese)**  |Yes |The name below the button on the login interface, such as Azure AD quick login. Click **View example here** below the input box to learn about the display effect. |
   ||**Login Abbreviation (English)**  |Yes |The name below the button on the login interface. |
   ||**Unique sign** |Yes |The unique identifier of the login source, used to distinguish tenants with different login authentication, consists of lowercase letters, numbers, and \-, which is less than 32 characters in length. Provided by SealSuite by default and cannot be modified. |
   ||**Description** |No |Authentication source description, a non\-client\-displayed field, with a length of less than 40 characters, is only used to keep track of backend notes. |
   ||**Login authentication location** |Yes |SealSuite login location allows multiple options such as **Mobile**, **Desktop**, or **Web Portal**. |
   |**Authentication Information** |**CAS service domain name address** |Yes |The domain name address corresponds to the CAS service. |
   ||**login endpoint** |Yes |The authentication endpoint of CAS. |
   ||**User Information Endpoint** |Yes |The endpoint for obtaining user information in CAS. |
   ||**Force re\-login** |No |Whether to force re\-login to the CAS service during authentication. |
   |**Advanced Settings** |**Attribute mapping strategy** |Yes |Map the user information of the third party login authentication source directly to the user information of SealSuite, that is, to establish the corresponding relationship between the third party and the user of SealSuite during the login process. You can set:<br><br><br>* **CAS**: Select the third\-party user properties field.<br><br>* **SealSuite**: Select the SealSuite user property field.<br><br>* **Automatically update**: It is checked by default, and the login update attribute takes effect after it is checked.<br><br>* **Delete**: Delete the mapping rule.<br><br>* **Add**: Add a new mapping rule. |
   ||**Uniquely identify priority** |Yes |To match the upstream unique ID in order of priority, you need to confirm the upstream data source unique ID. |
   ||**When the login does not match the employee, select the disposal method** |No |When enterprise members log in to SealSuite, you can provide an automatic account creation service based on the matching of the organizational structure in SealSuite. You can choose between:<br><br><br>* **Automatically create employee accounts**: After selection, if the login does not match an existing user, a user account will be automatically created to associate the user with the designated department.<br><br>* **Employee login failed, account will not be created**: After selection, if the login does not match an existing user, no account will be created. |
   


<span id="599b2fff"></span>
# Learn More

For more standard authentication source configuration, please refer to [Configuring OIDC authentication source](https://docs.byteplus.com/docs/sealsuite/docs-configuring-oidc-authentication-protocol-access).
