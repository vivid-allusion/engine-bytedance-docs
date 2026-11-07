---
title: "Configuring SAML for Alibaba Cloud (International)"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-alibaba-cloud-x-sealsuite-saml-international-"
---

This article introduces how to configure SAML for your Alibaba Cloud application in the Admin Portal.

<span id="1b6deadf"></span>
# Uses

There are two types of Alibaba Cloud SSO: Role\-based Alibaba Cloud SSO and User\-based Alibaba Cloud SSO. This topic will be divided into two parts, providing instructions on SAML configuration for both role\-based Alibaba Cloud SSO and user\-based Alibaba Cloud SSO.

<span id="8d501164"></span>
# Role\-based Alibaba Cloud SSO

This section comprises two distinct parts:


* [Configuration on Alibaba Cloud Management Console](https://docs.byteplus.com/docs/sealsuite/docs-alibaba-cloud-x-sealsuite-saml-international-#34c73f89)

* [Configuration on SealSuite's Admin Portal](https://docs.byteplus.com/docs/sealsuite/docs-alibaba-cloud-x-sealsuite-saml-international-#b3ae2b0d).


<span id="34c73f89"></span>
## Configuration on **Alibaba Cloud Management Console**


1. Log in to the [Resource Access Management (RAM) Console](https://ram.console.aliyun.com/overview) with your business account.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1c79ec2bb576470485d6b20a5988b531~tplv-goo7wpa0wc-image.image) </span>

2. In the left navigation bar, click **Integrations** \> **SSO**.

3. On the **SSO** page, click **Role\-based SSO** \> **SAML**.

4. In the **SAML** tab, click **Add IdP**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0c229344f07b4c39a05777ea89f6b4b9~tplv-goo7wpa0wc-image.image) </span>

5. On the **Create IdP** page, complete the following steps and click **OK**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c725feb27a234d3b9ccae0ea984e75c1~tplv-goo7wpa0wc-image.image) </span>

   1. Specify **IdP Name** to identify your identity provider (IdP).

      For demonstration purposes, this article uses SealSuite as the name of a newly created IdP.

   2. Specify **Remarks** if required.

   3. In the **Metadata File** section, click **Upload File** to upload the metadata file of the IdP.

6. On the **SSO** page, use the provided URL to download a SAML Service Provider (SP) metadata file.

   Save this metadata file in XML format for later use.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ff28602369904fc29021f780756662bd~tplv-goo7wpa0wc-image.image) </span>

7. In the left navigation bar, click **Identities** \> **Roles**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/82787698306b41d094a2c8666cdfebd4~tplv-goo7wpa0wc-image.image) </span>

8. On the **Roles** page, click **Create Role**.

9. In the **Create Role** pane, complete the following steps and click **OK**.

   1. Set the trusted entity to **IdP** and click **Next**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a75cb6b802ab41ddb3e40f430a636348~tplv-goo7wpa0wc-image.image) </span>

   2. Fill in the provided configuration items and set **Select IdP** to the IdP that you have created in Step 5.

      For demonstration purposes, this article uses SealSuiteIdP as the name of a newly created role.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7564526f384c4dfa90028e632dbe2789~tplv-goo7wpa0wc-image.image) </span>

10. On the **Roles** page, click **SealSuiteIdP** to enter the details page.

11. On the details page, locate **ARN** in the **Basic Information** section and click **Copy** on the right.

   Store the copied Alibaba Cloud Resource Name (ARN) value for later use.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d52a5507e0a545ada416cbd01a0a0133~tplv-goo7wpa0wc-image.image) </span>

12. In the left navigation bar, click **Integrations** \> **SSO**, and click **SealSuite** (the newly created IdP in Step 5).

13. On the details page of **SealSuite**, locate **ARN** in the **IdP** **Details** section and copy the **ARN** value.

   Store the copied ARN value for later use.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fbaffa63804a4436ae2e1da691fae1eb~tplv-goo7wpa0wc-image.image) </span>


<span id="b3ae2b0d"></span>
## Configuration on **SealSuite's Admin** Console


1. Log in to the Admin Console.

2. In the left navigation bar, click **Identity** \> **SSO**.

3. On the **SSO** page, click **Application Marketplace**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/07aa5cca80214f1eb91b0b08735dc6cb~tplv-goo7wpa0wc-image.image) </span>

4. On the **Add New Application** page, use filters to locate the Alibaba Cloud Role SSO application template card and click on it.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2b9e0cf02c2346958f3c5a490139f04b~tplv-goo7wpa0wc-image.image) </span>

5. In the lower right corner of the chosen template card, click **Add**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/88c95588ba0c44f3876db4811c049d70~tplv-goo7wpa0wc-image.image) </span>

6. On the page that appears, complete the following steps to create a role\-based Alibaba Cloud SSO application and click **Confirm**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a121b7f92eec4de2b7d2e24269bcebc1~tplv-goo7wpa0wc-image.image) </span>

   1. In the **General** section, specify **Application Name**, **Application Address**, and **Application Description**.

   2. In the **Application Type** section, you can:

      1. View and download SealSuite's metadata file under **IDP Metadata**.

      2. Upload the SAML SP metadata file that you saved earlier under **Alibaba Cloud Metadata file**.

         Take note of the requested attributes of a metadata file and ensure your metadata file has the same elements.

         An example of metadata file is as follows:

         <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/adb101b69c41462a9f956744a5db6013~tplv-goo7wpa0wc-image.image" name="aliyun_metadata.xml">aliyun_metadata.xml</Attachment>
         

7. In the left navigation bar, click **Identity** \> **Roles**.

8. On the **Roles** page, select **Static** tab.

9. Click **Add** to create a new role.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d4fbb2f26c864220aa2ec72b0fa4d415~tplv-goo7wpa0wc-image.image) </span>

10. On the **Add Role** page, configure the following parameters and click **Confirm**.

   1. **Role Name**: Use the following format to specify a role name using the ARNs that you have saved earlier. Suggested format: ARN of Role + ',' + ARN of IdP. For example, `acs:ram::1049198330250393:role/sealsuiteidp,acs:ram::1049198330250393:saml-provider/SealSuite`.

   2. **Role Description**: Provide a description of the role as needed.

   3. **Role Type**: Select either **Static Role** or **Dynamic Role**.

      For demonstration purposes, we select **Static Role** as the role type.

   4. **Static Role Scope**: Assign the static role to specific users or departments.

11. In the left navigation bar, click **Applications List**.

12. On the **Applications List** page, locate the Role\-based Alibaba Cloud SSO application that you have created earlier and click on its name to enter the details page.

13. On the details page, click the **Authorization** tab.

14. In the **Role Permissions** section, click **Add Role** to add relevant users to the application by role.

15. In the drop\-down list that appears, select the role you have created in Step 8 and click **Confirm**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/152cd7270d984675a500feddcc5ad808~tplv-goo7wpa0wc-image.image) </span>

16. In the **Single Sign\-on** tab of the newly created application, complete the following steps to map SAML attributes to SealSuite.

17. In the **Mapping Relation** section, click **Edit**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/40e1e927dcb14241b494558cf1951dd8~tplv-goo7wpa0wc-image.image) </span>

18. In the **Edit mapping relationship** dialog box, complete the following steps and click **OK**.

19. To add a pair of associated attributes, click **Add mapping** and specify values in the SealSuite field and the Application field.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9804280721ed42c4b7e39ed0bec7b9c0~tplv-goo7wpa0wc-image.image) </span>

   When you click on an input field, a drop\-down list appears. In the drop\-down list, you can click **Add custom attribute** to create a custom attribute and select your desired attribute.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3e1d3ab5f07f4d279f1beab7bb1b91e8~tplv-goo7wpa0wc-image.image) </span>

20. To add more associated attributes, repeat the above steps.

   A few SAML attributes are listed below for your reference. For more information on required SAML attributes, refer to [SAML response for role-based SSO](https://www.alibabacloud.com/help/en/resource-access-management/latest/saml-response-for-role-based-sso).



|**Attribute Name** |**Description** |
|---|---|
|`RoleSessionName` |This element is required and contains only one `AttributeValue` sub\-element. The value of `AttributeValue` sub\-element must be 2 to 64 characters in length, and can contain only letters, digits, and the following special symbols:<br><br><br>* `-`: En dash.<br><br>* `_`: Underscore.<br><br>* `.`: Dot.<br><br>* `@`: At sign.<br><br>* `=`: Equal sign.<br><br><br>The following code snippet provides an example of the `RoleSessionName` attribute.<br><br>```XML```<br>```<Attribute Name="https://www.aliyun.com/SAML-Role/Attributes/RoleSessionName">```<br>```  <AttributeValue>user_id</AttributeValue>```<br>```</Attribute>```<br> |
|`Role` |This element is required and contains one or more `AttributeValue` sub\-elements. `AttributeValue` lists the roles that can be assumed by a user in your IdP. The value of the `AttributeValue` sub\-element is a comma\-delimited pair of the ARN of the role and the ARN of the IdP. You can view the ARN of the role and the ARN of the IdP in the RAM console.<br><br><br>* To view the ARN of the role, go to the **Roles** page and click the name of the RAM role. On the page that appears, you can view the ARN of the role in the **Basic Information** section.<br><br>* To view the ARN of the IdP, go to the **SSO** page. On the **Role\-based SSO** tab, click the **SAML** tab and the name of the IdP. You can view the ARN of the IdP in the **IdP Details** section.<br><br><br>The following code snippet provides an example of the `Role` attribute.<br><br>```XML```<br>```<Attribute Name="https://www.aliyun.com/SAML-Role/Attributes/Role">```<br>```  <AttributeValue>acs:ram::$account_id:role/role1,acs:ram::$account_id:saml-provider/provider1</AttributeValue>```<br>```  <AttributeValue>acs:ram::$account_id:role/role2,acs:ram::$account_id:saml-provider/provider1</AttributeValue>```<br>```</Attribute>```<br> |


<span id="76064adf"></span>
# User\-based Alibaba Cloud SSO

This section comprises two distinct parts:


* [Configuration on Alibaba Cloud Management Console](https://docs.byteplus.com/docs/sealsuite/docs-alibaba-cloud-x-sealsuite-saml-international-#053120f8)

* [Configuration on SealSuite's Admin Portal](https://docs.byteplus.com/docs/sealsuite/docs-alibaba-cloud-x-sealsuite-saml-international-#f4e37cfa)


<span id="053120f8"></span>
## Configuration on Alibaba Cloud **Management Console**


1. Log in to the [Resource Access Management (RAM) Console](https://ram.console.aliyun.com/overview) with your business account.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1c79ec2bb576470485d6b20a5988b531~tplv-goo7wpa0wc-image.image) </span>

2. In the left navigation bar, click **Integrations** \> **SSO**.

3. On the **SSO** page, click the **User\-based SSO** tab.

4. In the **User\-based SSO** tab, complete the following steps:

   1. Use the provided URL to obtain a SAML Service Provider metadata file.

      Save the metadata file in XML format for later use.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1befb1d083de48a6a58ad1caf9b146fd~tplv-goo7wpa0wc-image.image) </span>

   2. Click **Edit** to the right of **Setup SSO**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2925de066b254368a097e77dbef6eec0~tplv-goo7wpa0wc-image.image) </span>

   3. In the **SSO Settings** pane that appears, complete the following steps and click **OK**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a82164d28d24dedaf0dbc8184fea4df~tplv-goo7wpa0wc-image.image) </span>

      1. Set **SSO Status** to **Enabled** and upload the metadata file that is obtained from the SealSuite Admin Portal.

         To obtain the metadata file, you can use a link with the following format: `https://{domain_name}/api/idp/metadata`.

      2. Enable and enter your auxiliary domain name if required.

5. In the left navigation bar, click **Identities** \> **Settings**.

6. On the **Settings** page, follow instructions below to configure advanced settings for SAML SSO.

   1. Click the **Advanced** tab.

   2. In the **Advanced** tab, edit default domain and add a domain alias.

      You can choose to verify your domain name by clicking **Domain Ownership Verification**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/423c2ab58d27453e89f14d453a064f5a~tplv-goo7wpa0wc-image.image) </span>

7. In the left navigation bar, click **Identities** \> **Users**.

8. On the **Users** page, follow instructions below to create a user on Alibaba Cloud which corresponds with the user in SealSuite for login convenience.

   1. Click **Create User**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3de08aa8a8da4e0babdf58318b181e55~tplv-goo7wpa0wc-image.image) </span>

   2. On the **Create User** page that appears, configure the provided configuration items and click **OK**.

      The **Logon Name** needs to correspond with a user's name used in the corresponding login email.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/00af5d22a6be476e9128300d11821ad2~tplv-goo7wpa0wc-image.image) </span>


<span id="f4e37cfa"></span>
## Configuration on **SealSuite's Admin** Console


1. Log in to the Admin Console.

2. In the left navigation bar, click **Identity** \> **SSO**.

3. On the **SSO** page, click **Application Marketplace**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/07aa5cca80214f1eb91b0b08735dc6cb~tplv-goo7wpa0wc-image.image) </span>

4. On the **Add New Application** page, use filters to locate the Alibaba Cloud User SSO application template card and click on it.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a52e477424154e74b19d6cfceccf6ab5~tplv-goo7wpa0wc-image.image) </span>

5. In the lower right corner of the chosen template card, click **Add**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ef1ec543104f422b98120c36d4b82b0d~tplv-goo7wpa0wc-image.image) </span>

6. On the page that appears, complete the following steps to create a user\-based Alibaba Cloud SSO application and click **Confirm**.

   After you complete this step, the page automatically jumps to the **Authorization** tab of your newly created application.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d331872a1bad4f8b80e2c18fcad205fd~tplv-goo7wpa0wc-image.image) </span>

   1. In the **General** section, specify **Application Name**, **Application Address**, and **Application Description**.

   2. In the **Application Type** section, you can:

      * View and download SealSuite's metadata file under **IDP Metadata**.

      * Upload the SAML Service Provider metadata file that you saved earlier under **Alibaba Cloud Metadata file**.

         Take note of the requested attributes of a metadata file and ensure your metadata has the same elements.

         An example of metadata is as follows:

         ```XML
         <EntityDescriptor xmlns="urn:oasis:names:tc:SAML:2.0:metadata" validUntil="0001-01-01T00:00:00Z" entityID="https://signin-intl.aliyun.com/5343775776290963/saml/SSO" ID="https___signin-intl.aliyun.com_5343775776290963_saml_SSO">
             <SPSSODescriptor xmlns="urn:oasis:names:tc:SAML:2.0:metadata" protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol" WantAssertionsSigned="true">
                 <KeyDescriptor use="signing">
                     <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
                         <X509Data>
                             <X509Certificate>MIIDLjCCAhagAwIBAgIEW3Fa4DANBgkqhkiG9w0BAQsFADBZMQswCQYDVQQGEwJDTjERMA8GA1UE&#xA;BxMISGFuZ3pob3UxFDASBgNVBAoTC0FsaWJhYmEgSW5jMQ8wDQYDVQQLEwZBcHNhcmExEDAOBgNV&#xA;BAMTB0FsaWJhYmEwHhcNMTgwODEzMTAxODA4WhcNMjgwODEwMTAxODA4WjBZMQswCQYDVQQGEwJD&#xA;TjERMA8GA1UEBxMISGFuZ3pob3UxFDASBgNVBAoTC0FsaWJhYmEgSW5jMQ8wDQYDVQQLEwZBcHNh&#xA;cmExEDAOBgNVBAMTB0FsaWJhYmEwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQCJhxKi&#xA;ZvtUMTZkMTcxZhFsbPkgEyDSpDLbQkgJuoxjCdDzH4Sm7To+NfW7VKfrVv+2KB5qCLLX0BtisFvo&#xA;qn6jEUPjaLOhkAcdRIjB8WtJe6PM/Ff2tMDbGpGxqY/VpOkyKF24lR3naRyIofz2+1BCFTqM21hu&#xA;q40QXUyTinyJxpC40bsegWOsmPHrAgWS0Rtl9Trr5TEKcotjSU+6XhOX+zizwVKG7yPWNeO0mXgR&#xA;ZDwfvSocuGhlJv6mpccQnQDd8GrDDkMtqPhoynF2le+at+Ex6eWiUhMrILYV+SuxTLvIF0Gk6tZ7&#xA;KlkjeSbTlV4/QursMjBh6Wv+vlCBk0qvAgMBAAEwDQYJKoZIhvcNAQELBQADggEBACDjIbiiT3ZB&#xA;yirDWxnJBJ+Oh+EGQU6gBlLDAhyaDQQrC2eCVs6qWXxeMTN/Ml/WoXl6FM0AzjGaWjlvAySSqoHP&#xA;NFoRVROI2QuE2kF/8LHfc0O8DoETT7iNSpXGRZz7p1IC1kqCE+XfosTUWMYUc6wqjD1uAUjMt4tV&#xA;C6RRolHxN54bJcBxK48m7jVH0SS30Wih0puBN/LCCgkOLsbl5W6HbvIXgCM8qs+HKCvb0CXu5AoT&#xA;LLiDzaLU0PwWSKBm42evOfkfoyK6ZaCh/31kZdeSnc8R0vupkJzHimhyBE6SUQt/BYTCLHBAjnaL&#xA;SP/MoAfUNsBm9hefivC3lZ8Cu6M=</X509Certificate>
                         </X509Data>
                     </KeyInfo>
                 </KeyDescriptor>
                 <NameIDFormat>urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress</NameIDFormat>
                 <NameIDFormat>urn:oasis:names:tc:SAML:2.0:nameid-format:transient</NameIDFormat>
                 <NameIDFormat>urn:oasis:names:tc:SAML:2.0:nameid-format:persistent</NameIDFormat>
                 <NameIDFormat>urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified</NameIDFormat>
                 <AssertionConsumerService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-POST" Location="https://signin-intl.aliyun.com/saml/SSO" index="0" isDefault="true"></AssertionConsumerService>
             </SPSSODescriptor>
         </EntityDescriptor>
         ```
         

7. In the **Authorization** tab, complete the following steps to configure user permissions:

   1. In the **User Permissions** section, click **Add Employee** to grant the corresponding users access to the application.

   2. In the pop\-up window, select your target users and click **Confirm**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/50fad553a160459fa15b0eddf66d0c12~tplv-goo7wpa0wc-image.image) </span>
