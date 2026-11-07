---
title: "Connecting Applications via LDAP: General Configuration"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/connecting-applications-via-ldap-general-configuration"
---

This guide assists IT administrators in creating LDAP applications within the SealSuite Admin Console to integrate third\-party systems.

By centralizing identity through LDAP, employees can log into various business systems using their SealSuite credentials. This eliminates the need for managing fragmented accounts, reduces maintenance overhead, and ensures security compliance throughout the account lifecycle.

<span id="20967e3c"></span>
## Step 1: Create an LDAP Application


1. Log in to the SealSuite Admin Console.

2. In the left navigation pane, go to **Identity** \> **SSO**.

3. Click  **+ Custom Application** in the top\-right corner.

4. Select the **LDAP** template.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a59f47b790647b3a8d1960ecfd1bdc4~tplv-goo7wpa0wc-image.image) </span>

5. Configure the application details as follows:

   * **General**: Enter the **Application Name**, **Access URL**, and a brief **Description**.

   * **SSO Configuration**: Customize the authentication logic for the application. Settings here will override the LDAP Server global defaults.

      
      |**Setting** |**Description** |
      |---|---|
      |**Password Format** |Choose the authentication methods supported by the application. |
      |**RDN** |Select the unique attribute (e.g., `open_id`, `user_id`) used as the `uid` in the user's Distinguished Name (DN). Ensure the chosen attribute is unique and populated for all users. |
      |**User Identifier** |Choose the key used for the user DN:<br><br><br>* **uid** (Default): e.g., `uid=jsmith,dc=...`<br><br>* **cn**: e.g., `cn=jsmith,dc=...`<br><br><br>Select based on the specific requirements of your third\-party system. |
      |**Configure Samba authentication** |Enable this only for systems requiring the Samba protocol, such as NAS or file\-sharing services.<br><br>**Security Warning**: Enabling this requires storing MD4 password hashes. If enabled, you must provide the `Workgroup` and `SID` matching your Samba server configuration. |
      

   * **User attribute field (Sync Scope)** : Define which user data the application is authorized to access.

      * **Basic Fields**: Default LDAP attributes. All are selected by default but can be modified.

      * **Custom Fields**: Extended attributes defined by your organization. These are unselected by default. Only enable them if necessary, as querying custom fields may impact performance.

6. Click **Save** to create the application.


<span id="d19ec13d"></span>
## Step 2: Configure Application Permissions

By default, new applications are restricted. You must define which users are authorized to access the system.


1. After saving, you will be redirected to the **Authorization** tab. (If not, navigate to the application's details page and select the **Authorization** tab).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f228ac37db714c688cf70b4ba9438652~tplv-goo7wpa0wc-image.image) </span>

2. Choose an authorization mode:

   * **Full**: All active employees in the organization can log in.

   * **Restricted**: Access is restricted to specific departments, roles, or individuals. Use the **Add Department / Employee / Role** buttons to define the scope. Any user outside this defined scope will be denied access even if they provide correct credentials.

3. The system saves these rules automatically upon selection.


<span id="9adae704"></span>
## Step 3: Obtain Connection Credentials

To connect your third\-party system to SealSuite, you need specific credentials found in the application details.


1. Go to the application's **SSO** tab.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2e4b16d2abb34959b5b5f5453b3f5152~tplv-goo7wpa0wc-image.image) </span>

2. Under the **General** section, locate and copy the following credentials:

   
   |**Parameter** |**Description** |
   |---|---|
   |**Domain Name (Hostname)**  |The LDAP server address (supports `ldap://` and `ldaps://`). |
   |**Port** |The communication port (`389` for standard, `636` for SSL). |
   |**Search DN/User OU (Base DN)**  |The starting point (root node) in the directory tree for user and department lookups. |
   |**Bind DN/Administrator account** |The unique "Service Account" name used by the third\-party application to connect to SealSuite. |
   |**Password** |The dedicated password for this application's Bind DN. |
   


<span id="ba68a3f2"></span>
## Step 4: Complete Setup in the Third\-Party System

Log in to the administrative interface of your third\-party application, locate the **LDAP / Directory Server** settings, and map the fields as follows:


* **Server URL / Hostname**: Enter the SealSuite Hostname.

* **Port**: Enter `389` or `636`.

* **Base DN**: Enter the Base DN from SealSuite.

* **Manager DN / Bind DN**: Use the application\-specific **Bind DN** obtained in Step 3.

* **Password**: Use the application\-specific **Password** obtained in Step 3.


**Verification**: Most systems provide a **Test Connection** or **Test Settings** button. Once the connection is successful, you can enable user synchronization or authentication.
