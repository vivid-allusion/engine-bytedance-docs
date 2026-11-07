---
title: "Configuring RADIUS protocol source"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-configuring-radius-protocol-access"
---

To facilitate the authentication and login of enterprise users, SealSutie supports Radius protocol as an authentication source to meet the access needs of the enterprise's own authentication source. Configuring the protocol as the authentication source enables users to log in to each application system more easily. This article introduces how to configure RADIUS authentication source access.

<span id="c33fd286"></span>
# Protocol Introduction

RADIUS (Remote Authentication Dial In User Service) protocol is a client\-server protocol that facilitates distributed information exchange and helps protect networks from unauthorized access. It is often used in various network environments that require a high level of security and allow remote users to access.

<span id="9f1338e0"></span>
# Configuring RADIUS Authentication Source


1. Log in to the Admin Console.

2. In the left navigation bar, select **Identity** \> **Account Setup** \> **Third\-Party Login**.

3. On the **Third\-Party Login** tab, click **Add Login Source** in the upper right corner.

4. In the **Select Login Source** dialog box, click the **RADIUS** card.

5. Set the RADIUS authentication source parameters as prompted. The key parameters are described as follows. After completing the configuration, click **Confirm**.

   
   |**Module** |**Configuration Item** |**Required** |**Description** |
   |---|---|---|---|
   |**General** |**Login display icon** |Yes |The identity source icon displayed on the login interface button, click **Upload** to upload the custom display icon. |
   ||**Login Abbreviation (Chinese)**  |Yes |The name below the button on the login interface, such as Azure AD quick login. Click the **View example here** below the input box to learn about the display effect. |
   ||**Login Abbreviation (English)**  |Yes |The name below the button on the login interface. |
   ||**Unique sign** |Yes |The unique identifier of the login source, used to distinguish tenants with different login authentication, consists of lowercase letters, numbers, and \-, which is less than 32 characters in length. Provided by SealSuite by default and cannot be modified. |
   ||**Description** |No |Authentication source description, a non\-client\-displayed field, with a length of less than 40 characters, is only used to keep track of backend notes. |
   ||**Login authentication location** |Yes |SealSuite login location allows multiple options such as **Mobile**, **Desktop**, or **Web Portal**. |
   |**Authentication Information** |**Net Protocol** |Yes |Select the authentication protocol. UDP is selected by default. It can be modified to TCP. |
   ||**Auth Protocol** |Yes |Select the authentication protocol. PAP is selected by default. Modification is not supported. |
   ||**Secret** |Yes |Enter the password key used to encrypt. |
   ||**Server IP** |Yes |Enter the server IP address. |
   ||**Server Port** |Yes |Enter the port number. The optional range is [0\-65535]. The value is 1812 by default. |
   ||**Timeout** |No |Enter the session timeout in seconds, which can be set within the range of[1\-60]. The value is 5 seconds by default. |
   ||**Retry Interval** |No |Enter the retry interval in seconds, which can be set within the range of [0\-10]. If not set, it is 1 second by default, meaning it will retry every 1 second until the timeout occurs. A value of 0 indicates no retry. |
   |**Advanced Settings** |**Attribute mapping strategy** |Yes |Map the user information of the third party login authentication source directly to the user information of SealSuite, that is, to establish the corresponding relationship between the third party and the user of SealSuite during the login process. You can set:<br><br><br>* **Radius**: Select the third\-party user properties field.<br><br>* **SealSuite**: Select the SealSuite user property field.<br><br>* **Automatically update**: This parameter is selected by default. The login update attributes take effect after being checked.<br><br>* **Delete**: Delete the mapping rule.<br><br>* **Add**: Add a new mapping rule. |
   ||**Uniquely identify priority** |Yes |To match the upstream unique ID in order of priority, you need to confirm the upstream data source unique ID. |
   


<span id="455a36e9"></span>
# Learn More

For more standard authentication source configuration, please refer to:


* [Configuring OIDC authentication source](https://docs.byteplus.com/docs/sealsuite/docs-configuring-oidc-authentication-protocol-access)

* [Configuring CAS authentication source](https://docs.byteplus.com/docs/sealsuite/docs-o9681n8i40)
