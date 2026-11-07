---
title: "Configuring SAML for Microsoft Office 365"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-configuring-saml-for-microsoft-office-365"
---

This article introduces how to configure SAML for your Microsoft Office 365 application in the Admin Portal.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Due to limitations in Microsoft domain federation settings, each federation issuer must be unique. Therefore, the following solution applies only to scenarios involving a single domain, federation with Sealsuites across multiple domains is not currently supported.</div>


<span id="5deaf2ff"></span>
# Uses

This article is divided into two parts:


* [Configuration on Microsoft Azure Portal](https://docs.byteplus.com/docs/sealsuite/docs-configuring-saml-for-microsoft-office-365#dc0797b4)

* [Configuration on SealSuite's Admin Portal](https://docs.byteplus.com/docs/sealsuite/docs-configuring-saml-for-microsoft-office-365#55cea97e)


<span id="dc0797b4"></span>
# Configuration on Microsoft Azure Portal


1. Log in to [Microsoft Azure Portal](https://portal.azure.com/).

2. On the homepage, navigate to **Azure Active Directory** \> **Custom domain names** to verify your domain.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/738a2b73b74447b2b94dd996a66711f4~tplv-goo7wpa0wc-image.image) </span>

3. After your domain is verified, return to the homepage and use the search box to search for the **External Identities** service and then click it.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a638e1b294c418085e97e65de3c4779~tplv-goo7wpa0wc-image.image) </span>

4. On the **Overview** page, click **View all identity providers** under the **Set up identity providers** option.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/939ad6e1a7534a2ca7b4ebd6c1e9b213~tplv-goo7wpa0wc-image.image) </span>

5. On the **All identity providers** page, click the **New SAML/WS\-Fed IdP** tab.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/54c8327b3b7b4b96b18767f28428196e~tplv-goo7wpa0wc-image.image) </span>

6. On the **New SAML/WS\-Fed IdP** page, specify the following values and click **Save**:

   * **Display name**: Enter a name to identify your identity provider. You can use `SealSuite` or any name you deem fit.

   * **Identity provider protocol**: Select **SAML**.

   * **Domain name of federating IdP**: Enter SealSuite's domain name for federation. For example, `example.sealsuite.com`

   * **Select a method for populating metadata**: Select **Parse metadata file**.

   * **Metadata file**: Upload SealSuite's metadata file. You can download the metadata file at `https://example.sealsuite.com/api/idp/metadata`

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For demonstration, we use a sample domain name in the above URLs. You need to replace <code>example.sealsuite.com</code> with your own domain.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cffbc34532334820b5ee19473cf9145e~tplv-goo7wpa0wc-image.image) </span>

7. Complete the following steps to configure your Microsoft authentication using Windows PowerShell.

   1. Connect to your Azure Environment using your login credentials.

      ```PowerShell
      Connect-MsolService -AzureEnvironment AzureCloud
      ```
      

   2. Create a new domain and verify it.

      ```PowerShell
      $DomainName = "example.sealsuite.com"
      New-MsolDomain -Name $DomainName -Authentication Federated
      Get-MsolDomainVerificationDns -DomainName $DomainName -Mode DnsTxtRecord
      ## Use the TXT record here, and add the entry in your domain name registrar.
      ```
      

   3. Set up your domain authentication using the SealSuite SAML configurations as shown below.

      ```PowerShell
      ## Get the IDP Cert from https://example.sealsuite.com/api/idp/metadata
      $dom = "example.sealsuite.com" 
      $BrandName = "SealSuite DEMO SAML 2.0 IDP" 
      $LogOnUrl = "https://example.sealsuite.com/api/idp/sso" 
      $LogOffUrl = "https://example.sealsuite.com/api/idp/sso" 
      $ecpUrl = "https://example.sealsuite.com/api/idp/sso"
      $IssuerUri = "https://example.sealsuite.com/api/idp/metadata" 
      $Cert = "MIIDpDCCAoygAwIBAgIGAWLVA3DIM/nixrZORyOTmsaWxtd"
      $uri = "https://example.sealsuite.com/api/idp/metadata" 
      $Protocol = "SAMLP" 
      Set-MsolDomainAuthentication `
        -DomainName $dom `
        -FederationBrandName $BrandName `
        -Authentication Federated `
        -PassiveLogOnUri $LogOnUrl `
        -SigningCertificate $Cert `
        -IssuerUri $IssuerUri `
        -LogOffUri $LogOffUrl `
        -PreferredAuthenticationProtocol $Protocol
      ```
      

   4. Add a new user.

      ```PowerShell
      New-MsolUser `
        -UserPrincipalName test@example.onmicrosoft.com `
        -ImmutableId test@example.onmicrosoft.com `
        -DisplayName "Test" `
        -FirstName cp23 `
        -LastName cp23 `
        -AlternateEmailAddresses "example@gmail.com" `
        -UsageLocation "US"
      ```
      

   **Full Sample Code**

   ```PowerShell
   # 1. Connect to your Azure Environment using your login credentials.
   Connect-MsolService -AzureEnvironment AzureCloud
   
   # 2. Create a new domain and verify it.
   $DomainName = "example.sealsuite.com"
   New-MsolDomain -Name $DomainName -Authentication Federated
   Get-MsolDomainVerificationDns -DomainName $DomainName -Mode DnsTxtRecord
   ## Using the TXT record here, add the entry in your domain name registrar.
   
   # 3. Set up your domain authentication using the SealSuite SAML configurations as shown below.
   ## Get the IDP Cert from https://example.sealsuite.com/api/idp/metadata
   $dom = "example.sealsuite.com" 
   $BrandName = "SealSuite DEMO SAML 2.0 IDP" 
   $LogOnUrl = "https://example.sealsuite.com/api/idp/sso" 
   $LogOffUrl = "https://example.sealsuite.com/api/idp/sso" 
   $ecpUrl = "https://example.sealsuite.com/api/idp/sso"
   $IssuerUri = "https://example.sealsuite.com/api/idp/metadata" 
   $Cert = "MIIDpDCCAoygAwIBAgIGAWLVA3DIM/nixrZORyOTmsaWxtd"
   $uri = "https://example.sealsuite.com/api/idp/metadata" 
   $Protocol = "SAMLP" 
   Set-MsolDomainAuthentication `
     -DomainName $dom `
     -FederationBrandName $BrandName `
     -Authentication Federated `
     -PassiveLogOnUri $LogOnUrl `
     -SigningCertificate $Cert `
     -IssuerUri $IssuerUri `
     -LogOffUri $LogOffUrl `
     -PreferredAuthenticationProtocol $Protocol
   
   # 4. Add a new user.
   New-MsolUser `
     -UserPrincipalName test@example.onmicrosoft.com `
     -ImmutableId test@example.onmicrosoft.com `
     -DisplayName "Test" `
     -FirstName cp23 `
     -LastName cp23 `
     -AlternateEmailAddresses "example@gmail.com" `
     -UsageLocation "US"
   ```
   


<span id="55cea97e"></span>
# Configuration on SealSuite's Admin Console


1. Log in to the Admin Console.

2. In the left navigation bar, click **Identity** \> **SSO**.

3. On the **SSO** page, click **Application Marketplace**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/07aa5cca80214f1eb91b0b08735dc6cb~tplv-goo7wpa0wc-image.image) </span>

4. On the **Add New Application** page, use filters to locate the Microsoft Office 365 application template card and click on it.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9507c201ed2145d9b8d2be8067154d15~tplv-goo7wpa0wc-image.image) </span>

5. In the lower right corner of the chosen template card, click **Add**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b7bb53ea15d5443abc9931f99c97337b~tplv-goo7wpa0wc-image.image) </span>

6. On the page that appears, complete the following steps to create your own Microsoft Office 365 application.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2d7323d9ec6b459bb814198cb131eea1~tplv-goo7wpa0wc-image.image) </span>

   1. In the **General** section, specify **Application Name**, **Application Address**, and **Application Description**.

   2. In the **Application Type** section, you can:

      * View and download SealSuite's metadata file under **IDP Metadata**.

      * Upload Microsoft's metadata file under **Microsoft Metadata**.

7. Click **Confirm** to save the configured settings.


<span id="a66952e9"></span>
# Frequently asked questions

<span id="9607b6e5"></span>
## If I encounter error codes during the single sign\-on process, what should I do?


* If you encounter the following error codes, try the respective solutions listed below.

   * **Error code 1: AADSTS51004**

      The error code indicates that the user account `{UserPrincipalName}` does not exist in the `{AAD Tenant ID}`directory. To sign into this application, the user account must be added to the directory.

   * **Solution**: Complete the following steps to check if the user has an `ImmutableID` value and registered license.

      1. Use the code below to check for the value of `ImmutableID`:

         ```Bash
         Get-MsolUser -UserPrincipalName <user@domain.tld> | select ImmutableID
         ```
         

         If the value is empty, set the value of `ImmutableID` to be the same as the one of `{UserPrincipalName}`:

         ```Bash
         Set-MSOLuser -UserPrincipalName <user@domain.tld> -ImmutableID <user@domain.tld>
         ```
         

      2. If the user does not have a registered license, register a license for the user by following the steps below:

         1. On the Azure portal, go to **Azure Active Directory** \> **Licenses** \> **All products**.

         2. On the **All products** page, select the license that you want to assign to users.

            <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a49229b479b3449196674708bb93de22~tplv-goo7wpa0wc-image.image) </span>

         3. On the **Licensed users** page, add your target users.

            <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e195cd228e9f452f8d7f958109c19de2~tplv-goo7wpa0wc-image.image) </span>

   * **Error code 2: AADSTS500132**

      The error code indicates that assertion is malformed and cannot be read.

   * **Solution**: Check the Microsoft Office 365 application that you created on SealSuite's Admin Portal and see if the authorization scope is set to **Full** mode. If the scope is set to **Full** mode, switch it back to **Restricted** mode.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/41fbae15bb9b4daeb20dda4398c6f91d~tplv-goo7wpa0wc-image.image) </span>

* If you encounter other error codes, contact SealSuite's Technical Support Team.
