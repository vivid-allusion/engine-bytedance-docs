---
title: "Configure SAML SSO login"
product: "BytePlus Cloud Identity"
product_code: "CloudIdentity"
source: "https://docs.byteplus.com/en/docs/CloudIdentity/Configure-SAML-SSO-login"
---

<span id="background-information"></span>
## Background information

This topic describes how to configure SSO login to the login portal of Cloud Identity based on SAML 2.0. For more information about the basic concepts and introduction, refer to [Overview of SSO on the login portal of Cloud Identity](https://docs.byteplus.com/en/docs/CloudIdentity/Overview-of-SSO-on-the-login-portal-of-Cloud-Identity).

<span id="prerequisites"></span>
## Prerequisites


1. You have an enterprise identity system that supports SAML 2.0, such as Lark, SealSuite, Azure AD, Okta, or other purchased or self\-managed systems.

2. You have created or synchronized Cloud Identity users. The usernames in Cloud Identity are correct. As each username in Cloud Identity is mapped to the information of a user (such as its ID, username, and email address) in the enterprise identity system, ensure that usernames in Cloud Identity are correct.


<span id="_1-1-process-of-sso-via-saml"></span>
## 1.1 Process of SSO via SAML

In this example, SSO via SAML is used. The following figure describes the SSO process.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_74c61bda413d2de15ffc39326748f54b.png) </span>


1. The browser of an enterprise user initiates a direct SSO request through the login portal of Cloud Identity or through a link to a third\-party IdP page. In this example, a third\-party IdP page is used.

2. The SSO service of Cloud Identity sends an SAML request to the browser of the enterprise user.

3. The browser of the enterprise user forwards the SAML request.

4. The IdP authenticates the logged\-in user and sends an SAML response containing the IAM user information corresponding to the enterprise user.

5. The browser of the enterprise user forwards the SAML response to the SSO service of Cloud Identity.

6. The SSO service parses the SAML response and verifies the authenticity of the SAML response based on the SAML trust configuration.

7. The corresponding Cloud Identity user is matched based on the internal information of the parsed SAML response.

8. The SSO service of Cloud Identity returns the URL of the login portal of Cloud Identity to the browser of the enterprise user.

9. The browser of the enterprise user redirects the enterprise user, and the enterprise user uses the identity of the Cloud Identity user to log in to the user portal of Cloud Identity.


<span id="procedure"></span>
## Procedure

To implement user SSO, you must upload relevant metadata files to the IdP and SP systems, configure mutual trust between the two systems, and create the mapping between enterprise IdP users and IAM users.

<span id="_1-operations-on-cloud-identity"></span>
### 1. Operations on Cloud Identity

First, configure the enterprise IdP as a trusted IdP on Cloud Identity.


1. Obtain the IdP metadata file from the IdP system. A metadata file must be in the standard XML format and can be up to 100 KB in size.

2. In the Cloud Identity console, click [User login settings](https://console.byteplus.com/cloudidentity/region:ap-southeast-1/userLogin/). In the **Login method settings** module, click Upload near **IdP information** to upload the IdP metadata file.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After the metadata file is uploaded, you can find the employee login address under <strong>Employee login link</strong>. You can customize the login address as needed.</div>



3. In the **Login method settings** module, you can download the SP metadata file of Cloud Identity in **SP information**, or copy the ACS URL and entity ID to the IdP.


<span id="_2-operations-on-the-enterprise-identity-system"></span>
### 2. Operations on the enterprise identity system

Second, configure Cloud Identity as a trusted SP on the enterprise identity system.

On the enterprise IdP system, add Cloud Identity as a trusted SP based on the SP metadata obtained in the preceding step. You can use one of the following configuration methods based on your IdP:


1. Provide the URL of the SP metadata.

2. Upload the metadata file that you have downloaded in the preceding step.

3. Manually configure SP\-related parameters on the enterprise IdP system based on the content in the metadata file.

   1. `Entity ID`: Used to identify the SP. It must be set to the value of the **entityID** attribute of the **EntityDescriptor** element in the metadata file, which corresponds to the entity ID mentioned in Step 1.

   2. `ACS URL`: Used to declare the SAML assertion sending address. It must be set to the value of the **Location** attribute of the **AssertionConsumerService** element in the downloaded metadata file, which corresponds to the ACS URL mentioned in Step 1.


After you perform the preceding operations, the configuration is completed.

<span id="format-requirements-for-saml-responses"></span>
## Format requirements for SAML responses

When a user sends a request to log in to the login portal of Cloud Identity after logging in to the IdP, the IdP returns an SAML response to the login portal of Cloud Identity. The login portal of Cloud Identity verifies the signature in the SAML response and parses the SAML response for the identity information of the current user, ensuring secure and fast SAML SSO login for users.

When debugging the login process after completing the configuration, make sure that your SAML response is in the same format as the following sample SAML response, without any missing elements.

```xml
<samlp:Response> 
    <saml:Issuer>${Issuer}</saml:Issuer> 
    <ds:Signature> 
        ... 
    </ds:Signature> 
    <samlp:Status> 
        <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success"></samlp:StatusCode> 
    </samlp:Status> 
    <saml:Assertion> 
        <saml:Issuer>...</saml:Issuer> 
        <ds:Signature> 
            ... 
        </ds:Signature> 
        <saml:Subject> 
            <saml:NameID>${NameID}</saml:NameID> 
            <saml:SubjectConfirmation> 
                ... 
            </saml:SubjectConfirmation> 
        </saml:Subject> 
        <saml:Conditions> 
            <saml:AudienceRestriction> 
                <saml:Audience>${Audience}</saml:Audience> 
            </saml:AudienceRestriction> 
        </saml:Conditions> 
        <saml:AuthnStatement> 
            ... 
        </saml:AuthnStatement> 
    </saml:Assertion> 
</samlp:Response>
```



|**Element** |**Description** |
|---|---|
|Issuer |**Issuer** must have the same value as the EntityID element in the IdP SAML metadata file that you have uploaded to the console settings of Cloud Identity. The login portal of Cloud Identity needs to verify this field to ensure that the IdP in the login request is a trusted IdP. |
|Signature |Based on protocol specifications, the login portal of Cloud Identity requires that an SAML response must contain a signature and the signature must match the security certificate in the IdP metadata file. This ensures the response content is secure and reliable. Add a signature to the corresponding location, as shown in the sample response. **Signature** must contain the signature value, signature algorithm, and other relevant information. |
|Subject |Subject must contain the following elements:<br><br><br>1. Only one **NameID** element, which is used to specify the Cloud Identity user that needs to log in. The value of NameID is the username of the Cloud Identity user. Make sure that the user exists.<br><br>2. A **SubjectConfirmation** element, whose following fields must have unique valid values:<br><br>   1. **NotOnOrAfter**：Used to specify the validity period of an assertion in UTC time.<br><br>   2. **Recipient**: Used by the login portal of Cloud Identity to verify whether it is the recipient of the current response. Its value must be the ACS URL of the SP provided in the Cloud Identity console. The format is:[https://signin.byteplus.com/cloudidentity/${Region}/${UUId}/saml/sso](https://signin.byteplus.com/cloudidentity/$%7BRegion%7D/$%7BUUId%7D/saml/sso)<br><br><br>Sample Subject element:<br><br>```xml```<br>```<saml:Subject>```<br>```   <saml:NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent">user1</saml:NameID>```<br>```   <saml:SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">```<br>```    <saml:SubjectConfirmationData NotOnOrAfter="2024-02-28T12:26:14Z" Recipient="https://signin.byteplus.com/cloud-identity/ap-southeast-1/950***-8***8-c***9-f***8-d***b4/saml/sso"></saml:SubjectConfirmationData>```<br>```   </saml:SubjectConfirmation>```<br>```  </saml:Subject>```<br> |
|Conditions |A Conditions element must contain one AudienceRestriction element, which includes a unique valid **Audience** element that is used to specify the audience of the response. Its value must be fixed to the entity ID of the SP provided in the Cloud Identity console, in the format of [https://signin.byteplus.com/cloud-identity/saml/sso/${CloudIdentity_Instance_Id}](https://signin.byteplus.com/cloud-identity/saml/sso/$%7BCloudIdentity_Instance_Id%7D).<br><br>Sample Conditions element:<br><br>```xml```<br>```<saml:Conditions NotBefore="2024-02-28T12:20:14Z" NotOnOrAfter="2024-02-28T12:26:14Z">```<br>``` <saml:AudienceRestriction>```<br>```  <saml:Audience>https://signin.byteplus.com/cloud-identity/saml/sso/2****************</saml:Audience>```<br>``` </saml:AudienceRestriction>```<br>```</saml:Conditions>```<br> |
