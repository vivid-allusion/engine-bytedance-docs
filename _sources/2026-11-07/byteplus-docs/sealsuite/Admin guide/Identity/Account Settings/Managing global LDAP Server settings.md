---
title: "Managing global LDAP Server settings"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/managing_global_ldap_server_settings"
---

SealSuite functions as a centralized Identity Provider (IdP) by offering a built\-in LDAP service. By enabling this service, you can use SealSuite as your organization’s single source of truth, allowing third\-party applications to perform user authentication and directory queries via the standard LDAP protocol.

To maintain a consistent security posture, SealSuite allows you to define global LDAP configurations. These settings act as a security and performance baseline for all connected systems, eliminating the need to reconfigure basic rules for every individual application.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This guide covers global service rules. If you need to integrate a specific application using existing settings, see <a href="https://docs.byteplus.com/docs/sealsuite/connecting-applications-via-ldap-general-configuration">Connecting Applications via LDAP: General Configuration</a>.</div>


<span id="1d6f5686"></span>
## 1. Defining Global LDAP Rules

Before connecting external systems, configure the default operational behavior of the LDAP service. These settings apply to all general connection requests and serve as the default template for new application integrations.


1. Log in to the SealSuite Admin Console.

2. Navigate to **Identity** \> **Account Setup**.

3. Select the **LDAP Server** tab.

4. Scroll to the **General** section and click **Edit**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/da8e81bbb60943d3ab1d89f01626a8a9~tplv-goo7wpa0wc-image.image) </span>

5. Configure the following parameters based on your security requirements:

   
   |**Parameter** |**Description** |
   |---|---|
   |**Password format** |Sets the default verification logic for LDAP logins.<br><br><br>* **Static Password**: Standard SealSuite account password.<br><br>* **OTP**: One\-Time Password generated via the SealSuite App.<br><br>* **Static Password + OTP**: Enables Multi\-Factor Authentication (MFA) for enhanced security.<br><br>> Note: Application\-specific settings will override this global default. |
   |**RDN** |Determines the unique attribute used for the `uid` field in a user’s Distinguished Name (DN). This value must be unique and non\-empty.<br><br>> Note: Application\-specific settings will override this global default. |
   |**LDAP Search pagination** |A performance toggle for large\-scale directories.<br><br><br>* **Enable**: Recommended if your directory exceeds 1,000 entries and the client application supports paged results. This prevents timeouts and reduces server load.<br><br>* **Disable**: Keep disabled if the client application does not support LDAP pagination controls. |
   

6. Click **Save**.


<span id="00c0f182"></span>
## 2. Server Connection Details

Once the global rules are set, use the following parameters to point your third\-party applications to the SealSuite LDAP service.


1. Locate the **Configuration information instructions** section at the top of the **LDAP Server** page.

2. Use these values for network and directory addressing:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/beb4a49920a74f92b16ef3e32637b1b0~tplv-goo7wpa0wc-image.image) </span>

   
   |**Parameter** |**Technical Value** |**Example** |
   |---|---|---|
   |**Hostname** |The LDAP server endpoint. |* `ldap://ldap.example.com` (Standard)<br><br>* `ldaps://ldap.example.com` (Secure) |
   |**Port** |Communication port. |* `389` (Standard)<br><br>* `636` (SSL/TLS) |
   |**Search Base (Base DN)**  |The starting point for directory lookups. |`ou=users,dc=example,dc=com` |
   |**Binding DN/Administrator Account (BindDN), Password** |SealSuite enforces application isolation. There is no "Global Admin" Bind DN. You must create an entry for each specific application to generate unique credentials. |Refer to [Connecting Applications via LDAP: General Configuration](https://docs.byteplus.com/docs/sealsuite/connecting-applications-via-ldap-general-configuration). |
   


<span id="6a13cbcf"></span>
## 3. Next Steps: Integrating Applications

After establishing the global service baseline, you must register individual applications to obtain their unique connection credentials (Bind DN and Password). See [Connecting Applications via LDAP: General Configuration](https://docs.byteplus.com/docs/sealsuite/connecting-applications-via-ldap-general-configuration) for detailed instructions on application\-level setup.
