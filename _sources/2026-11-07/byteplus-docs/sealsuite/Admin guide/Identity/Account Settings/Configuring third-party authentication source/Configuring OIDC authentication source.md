---
title: "Configuring OIDC authentication source"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-configuring-oidc-authentication-protocol-access"
---

To facilitate the authentication and login of enterprise users, SealSuite supports OIDC protocol as an authentication source to meet the access requirements of enterprise\-owned authentication sources. Configuring the protocol as the authentication source enables users to log in to each application system more easily. This article introduces how to configure OIDC authentication source.

<span id="bc44609e"></span>
# Protocol Introduction

OIDC (OpenIDConnect) is an authentication standard protocol based on the OAuth2.0 protocol, providing a secure way for user authentication and authorization. OIDC uses the authorization server of OAuth2.0 to provide user authentication information to third\-party clients, and is suitable for various types of clients, and is fully compatible with OAuth2.0. Unlike OAuth2.0, OIDC also provides a standardized user information endpoint, making it easier for third\-party applications to obtain basic user information. For more information about OIDC, please refer to [How OpenID Connect Works](https://openid.net/connect/).

<span id="4187d1e7"></span>
# Prerequisites


* You have created an OIDC application in an OIDC\-certified source.

* You have copied the following redirect address to your OIDC authentication source.

   `https://staging.feilian.cn/api/tpslogin/callback/custom_oidc`


<span id="acef44c8"></span>
# Configuring OIDC Authentication Source


1. Log in to the Admin Console.

2. In the left navigation bar, select **Identity** \> **Account Setup** \> **Third\-Party Login**.

3. On the **Third\-Party Login** tab, click **Add Login Source** in the upper right corner.

4. In the **Select Login Source** dialog box, click the **OIDC** card.

5. Configure OIDC authentication source parameters according to the prompts. The key parameters are described as follows. After completing the configuration, click **Confirm**.

   
   |**Module** |**Configuration Item** |**Required** |**Description** |
   |---|---|---|---|
   |**General** |**Login display icon** |Yes |The identity source icon displayed on the login interface button, click **Upload** to upload the custom display icon. |
   ||**Login Abbreviation (Chinese)**  |Yes |The name below the button on the login interface, such as OIDC certification. Click the **View example here** below the input box to learn about the display effect. |
   ||**Login Abbreviation (English)**  |Yes |The name below the button on the login interface. |
   ||**Unique sign** |Yes |The unique identifier of the login source, used to distinguish tenants with different login authentication, consists of lowercase letters, numbers, and \-, which is less than 32 characters in length. Provided by SealSuite by default and cannot be modified. |
   ||**Description** |No |Authentication source description, a non\-client\-displayed field, with a length of less than 40 characters, is only used to keep track of backend notes. |
   ||**Login authentication location** |Yes |SealSuite login location allows multiple options such as **Mobile**, **Desktop**, or **Web Portal**. |
   |**Authentication Information** |**Client ID** |Yes |ClientID provided by OIDC identity service providers. You can copy the ClientID information in the OIDC authentication source details. |
   ||**Client Secret** |Yes |Client Secret provided by OIDC identity service providers. You can copy the Client Secret information in the OIDC authentication source details. |
   ||**Scope** |No |OIDC certification scope, such as openid profile, multiple parameters need to be separated by spaces. |
   ||**Token**<br><br>**authentication method** |No |The OIDC identity service provider provides a way to obtain a token, optional **client_secret_post** or **client_secret_basic**. |
   ||**Carry Nonce** |No |Whether to carry the Nonce parameter when requesting OIDC services. This parameter is disabled by default. |
   ||**Vertification ID Token** |No |Whether the verification is IDToken. Information can be obtained from the IDToken after verification. Once the toggle is turned on, you can set:<br><br><br>* **Verify ID Token Signature Algorithm**: Optional **HS256** or **RS256**.<br><br>* **Verify publication domain**: Toggle the switch to turn it on or off.<br><br>* **ID Token Issuer**: Enter the ID Token issuer. If it is left empty, the OIDC service domain name and address will be taken by default. |
   ||**User information source** |No |The source of user information can be obtained from:<br><br><br>* **ID Token**<br><br>* **User Information Endpoint**<br><br>   User information request method: optional **GET** and **POST**.<br><br>* **ID Token and User Information Endpoint**<br><br>   User information request method: optional **GET** and **POST**. |
   ||**Trust user equipment** |No |You can skip the two\-factor authentication after trusting the user device. Once the toggle is turned on, you can configure:<br><br><br>* **Trust the identity of the user device**<br><br>* **Trust the value of the user device**<br><br>* **Trust the valid period identifier of the user device**<br><br>* **Trust the valid period (hours) of the user device** |
   ||**OIDC service domain name address** |Yes |The domain name address of the corresponding OIDC service. |
   ||**Authenticated Endpoint** |Yes |The endpoint that the OIDC identity service authorizes authentication. |
   ||**Token endpoint** |Yes |The OIDC identity service gets the endpoint of the Token. |
   ||**User information Endpoint** |Yes |The endpoint at which the OIDC identity service acquires user information. |
   ||**JWKs public key endpoints** |No |The endpoint at which the OIDC identity service obtains the JWKs public key. |
   |**Advanced Settings** |**Attribute mapping strategy** |Yes |Map the user information of the third party login authentication source directly to the user information of SealSuite, that is, to establish the corresponding relationship between the third party and the user of SealSuite during the login process. You can set:<br><br><br>* **OIDC**: Select the third\-party user properties field.<br><br>* **SealSuite**: Select the SealSuite user property field.<br><br>* **Automatically update**: It is checked by default, and the login update attribute takes effect after it is checked.<br><br>* **Delete**: Delete the mapping rule.<br><br>* **Add**: Add a new mapping rule. |
   ||**Uniquely identify priority** |Yes |To match the upstream unique ID in order of priority, you need to confirm the upstream data source unique ID. |
   ||**When the login does not match the employee, select the disposal method** |No |When enterprise members log in to SealSuite, you can provide an automatic account creation service based on the matching of the organizational structure in SealSuite. You can choose between:<br><br><br>* **Automatically create employee accounts**: After selection, if the login does not match an existing user, a user account will be automatically created to associate the user with the designated department.<br><br>* **Employee login failed, account will not be created**: After selection, if the login does not match an existing user, no account will be created. |
   


<span id="28ec31c6"></span>
# Learn More

For more standard authentication source configuration, please refer to [Configuring CAS authentication source](https://docs.byteplus.com/docs/sealsuite/docs-o9681n8i40).
