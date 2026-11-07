---
title: "Configuring login by LDAP account"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-configuring-login-by-ldap-account"
---

SealSuite's account system can integrate with an enterprise's LDAP (Lightweight Directory Access Protocol) server, which is a widely used protocol for centralizing authentication and managing employee accounts. This integration enables employees to log in to SealSuite using their LDAP accounts.

<span id="86a4e443"></span>
# Procedure


1. Log in to the Admin Console.

2. In the left navigation bar, click **Identity** \> **Account Setup**.

3. Under the **Authentication** tab, click **Edit** in the top right corner.

4. Enable **LDAP** in the **Account Login Method** area.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6e468e698fec46dca670e72574732839~tplv-goo7wpa0wc-image.image) </span>

5. Go to the **LDAP** Tab, and complete the following configurations according to actual needs.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e585d02ba5be4b31822127be1ace1e47~tplv-goo7wpa0wc-image.image) </span>

   
   |**Items** |**Description** |
   |---|---|
   |**LDAP login entry name** |The name will be displayed when members log in to the client or webpage of SealSuite. For example, if the name is set as ABCDE, the login page will show as follows.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/788555cd0d294532970ef039290c0637~tplv-goo7wpa0wc-image.image) </span> |
   |**Server address** |The address of the server to which deploys LDAP service. It is recommended to follow this address format, `ldaps://:`<br><br><br>* refers to the server's domain name or IP address.<br><br>* refers to port. The default port is 389 for LDAP protocol and 636 for LDAPS protocol. |
   |**LDAP Gateway** |SealSuite will query the identity information from the root LDAP gateway. For example, `dc=sealsuite, dc=com`. |
   |**Administrator DN** |Select the administrator that has permission to connect to the LDAP server. For example,`cn=admin, dc=sealsuite, dc=com`. |
   |**Administrator password** |The password of **Administrator DN**. |
   |**User object class** |User object (objectclass) should be specified. For example,<br><br><br>* OpenLDAP: inetOrgPerson<br><br>* AD domain: user or organizationalPerson |
   |**User unique identity** |A unique attribute for each user instance in LDAP. For example,<br><br><br>* OpenLDAP: uid, dn<br><br>* AD domain: sAMAccountName |
   |**Mobile phone number** |The user's phone number attribute in LDAP, you can choose either phone number or email. For example,<br><br><br>* OpenLDAP: phoneNumber<br><br>* AD domain: mobile |
   |**Email** |The user's mail attribute in LDAP, you can choose either phone number or email. For example,<br><br><br>* OpenLDAP: mail<br><br>* AD domain: mail |
   |**User departure field** |If there is an attribute in LDAP that indicates user departure, it can be filled in as an optional field. For example,<br><br><br>* OpenLDAP: employeType<br><br>* AD domain: UserAccountControl |
   |**User departure field value** |A keyword representing the departure status of the user. For example,<br><br><br>* OpenLDAP: separated<br><br>* AD domain: 514 (decimal) |
   |**Allow employee information to be automatically updated when employees log in** |When enabled, employee information will be automatically updated when employees log in through a third\-party data source, their information will be automatically updated if enabled.<br><br>Under Configuration, enter the third\-party authorized login page to configure authorization by LarkSuite, Azure, Google, and more. Multiple authorization types can be selected.<br><br>For information on configuring LarkSuite authorization login, refer to the SealSuite \- Feishu Identity Source Import & Authentication Source Login Configuration Guide (to be replaced with link). For information on configuring Azure authorization login, refer to (to be replaced with link). For information on configuring Google authorization login, refer to the SealSuite _ DingTalk Organization Import & third\-party login Configuration Guide (to be replaced with link). |
   |**Connectivity Test** |Click the button to check the network connection between the LDAP server and SealSuite server. |
   |**Third\-Party Login** |1. Click **Configuration** to enter the corresponding login page for LarkSuite, Azure, etc.<br><br>2. Choose the Authorization type and select multiple options as needed.<br><br>3. After configured, click **Save** **Changes** at the bottom of the page to apply changes immediately. |
   |**Auto\-Creation** |After enabling **Auto\-Creation**, if the third\-party data source fails to synchronize member accounts in a timely manner, SealSuite will automatically create an account upon login.<br><br>For example, if a member in the LarkSuite organization structure has not been synchronized to the SealSuite organizational structure and attempts to log in using LarkSuite authorization, the client will fail to log in and report an error if the Auto\-Creation button is disabled. However, if the button is enabled, an account will be automatically created in SealSuite for the member, allowing them to log in successfully with default permissions. |
   |**Login Method Display Order** |If you have configured third\-party authorization login to SealSuite, you can adjust the display priority of login methods. The left side has higher priority, and the first priority will be shown as the primary login method of SealSuite. Users can switch to other methods as needed.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/510d96efe41a4ad6b866274750f701ff~tplv-goo7wpa0wc-image.image) </span><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cb2805b7318145dd8fa25e956739dd18~tplv-goo7wpa0wc-image.image) </span> |
   |**Role Synchronisation** |If you want to synchronize roles and members from third\-party identity resources, you can enable **Role Synchronization**. After the synchronization tasks are completed, the roles will be displayed in the role list. |
   |**Support Contact** |In case users forget their passwords or fail to receive verification codes, the contact person will be prompted on the application's front page.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7af80ddfa45941208db4b7f3b135a088~tplv-goo7wpa0wc-image.image) </span> |
   |**Enterprise mailbox domain name** |To establish a unified mail suffix for the enterprise, you can configure the domain name suffix of the enterprise mail and select **Only support this mailbox suffix** if necessary. |
   

6. In the upper right corner of the page, click **Save** to finish the configuration.
