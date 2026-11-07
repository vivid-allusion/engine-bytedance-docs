---
title: "Managing Staff Network Access with Portal Authentication"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/managing-staff-network-access-with-portal-authentication"
---

Portal authentication (Web authentication) is a clientless network access method. Once connected to the network, employees can gain internet access by verifying their identity through a browser or H5 page. This method is ideal for personal devices (BYOD), contractors, guests, or as an emergency backup if the 802.1x client fails. This document provides instructions for administrators on enabling the protocol and configuring employee\-specific authentication rules and network permissions.

> For more information on selecting authentication methods, see [Selecting Network Access Authentication Methods](https://docs.byteplus.com/docs/sealsuite/selecting-network-access-authentication-methods).


<span id="452bcbe2"></span>
# Prerequisites

Before configuring employee Portal access, ensure the following requirements are met:


1. **Infrastructure integration**: You have configured a Wi\-Fi or wired network in the SealSuite Admin Console. For more information, see [Adding a RADIUS server](https://docs.byteplus.com/docs/sealsuite/docs-adding-a-radius-server), [Adding a wireless router](https://docs.byteplus.com/docs/sealsuite/docs-adding-a-wireless-router), or [Adding a switch](https://docs.byteplus.com/docs/sealsuite/docs-adding-a-switch).

2. **Network connectivity**: Ensure that UDP ports 1812 and 1813 are open bi\-directionally between your network hardware and the SealSuite RADIUS node.

3. **Redirection configuration**: Complete the following on your network hardware (AC or switch):

   * Set the redirection URL to point to the authentication page provided by the SealSuite Server.

   * Configure an authentication\-free whitelist to allow DNS traffic and access to the SealSuite login page.

4. If your hardware requires specific Portal 2.0/3.0 protocol handshakes, you must also configure the [Managing portal server node](https://docs.byteplus.com/docs/sealsuite/docs-managing-guest-portal-server).


<span id="5360b0eb"></span>
# Enabling Portal authentication access

<span id="1b05a5f6"></span>
## I. Enable the Portal authentication protocol


1. Log in to the SealSuite Admin Console.

2. In the left navigation bar, select **NAC** \> **Staff Network**.

3. Go to the **General Settings** tab and click **Select Authentication Method** in the upper\-right corner.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/04d8affbc4994ed5b3198f70f9fcb286~tplv-goo7wpa0wc-image.image) </span>

4. Select **Portal** and click **Confirm**.

> **Note**: If you enable both 802.1x and Portal authentication, ensure your SealSuite RADIUS nodes are up to date to prevent authentication failures.


<span id="b0335319"></span>
## II. Configure employee authentication rules

In the **General Settings** tab, expand **Portal Authentication Protocol** and click **Edit** to adjust the following settings:


|Configuration Item |Description |
|---|---|
|**Authentication method** |Configure the login methods allowed for employees. After you click **Modify**, the page automatically redirects to the **Authentication** tab under **Account Setup**. For details about the configuration method, see [Setting up account systems and identity authentication](https://docs.byteplus.com/docs/sealsuite/docs-managing-account-settings). |
|**Requires 2FA when employees log in to the corporate network** |Supports secondary verification during Portal login to improve account security. After you click **Modify**, the page automatically redirects to the **MFA Setup** tab under **Account Setup**. For details, see [Configuring multi-factor authentication (MFA)](https://docs.byteplus.com/docs/sealsuite/docs-configuring-multi-factor-authentication-mfa-). |
|**Detect FeiLian desktop client login using portal authentication** |After this is enabled, the user portal detects the login status of the SealSuite client before authentication. If the requirement is not met, network access is blocked and a guided download window is displayed. You can configure an administrator as the contact person for end users.<br><br>This feature is often used during the transition from Portal authentication to 802.1X authentication, requiring office endpoints to have the security baseline capabilities provided by the SealSuite client. |
|**Advanced Settings \> Device authentication expiration** |Set the device\-level "login\-free" period. During this period, the same endpoint does not need to display the Portal authentication page again when reconnecting. |


<span id="90d431c6"></span>
## III. Configure network permission policies

Use permission group policies to define user scopes and authentication lifecycles for Portal access.

<span id="166a6b0f"></span>
### Add a permission policy


1. Go to **Staff Network** \> **Authorization**, and switch to the **Portal Authentication** subtab.

2. Click  **+ Add New Policy** on the right and complete the following parameter configurations.

   
   |**Configuration Item** |**Description** |
   |---|---|
   |**Policy Name** |Custom permission group name used to identify the current policy. |
   |**Priority** |Set the matching order of the policy. The value range is 0 to 100. **A higher value indicates a higher priority.** <br><br>The system matches policies in descending priority order. Once an effective object is matched, the policy is applied and subsequent checks stop. If multiple policies have the same priority, the policy modified most recently is matched first. |
   |**Permission Type** |Specifies the access medium to which the policy applies. Options include **Staff Wi\-Fi** and **Wired Network**. Multiple selections are supported. |
   |**Scope** |Specifies the user scope covered by the policy by **department**, **role**, or **member**. |
   |**Advanced settings** |Click **Advanced settings** to expand the section and configure fine\-grained controls for the network access environment and duration.<br><br><br>* **Effective operating system scope**: Takes effect for all systems by default. You can also configure policies separately for specific systems.<br><br>* **Certification validity period**: Set the single lifecycle of this Portal authentication, in hours. When the employee’s online duration reaches the configured value, the system forcibly disconnects the employee. To continue using the internet, the employee must reopen the Portal page and log in again. |
   


<span id="f7f418e0"></span>
### Manage policy lifecycles

Maintain your policies on the permission group list page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c5936949e0444909a663ea0e9cbf74a8~tplv-goo7wpa0wc-image.image) </span>


* **Enable or disable**: Use the toggle in the **Action** column to activate or deactivate policies.

* **Filter and search**: Use filters for **Access Method**, **Department**, or **Sort**. You can also create custom filters.

* **Keyword search**: Search for departments, employees, VLAN IDs, network device names, or SSIDs.

* **Adjust priorities**: Modify the **Priority Value** directly in the list. The system automatically reorders the list from highest to lowest.

* **Modify**: Click **Edit** to update priorities, access types, effective objects, or validity periods. Users may need to reconnect for changes to take effect.

* **Delete**: Remove obsolete policies. Ensure other policies cover the affected users to prevent access issues.

* **Default group**: The fallback policy (priority 0) at the bottom of the list applies if no other policies match. It cannot be edited or deleted.


<span id="69d85c8c"></span>
# Monitoring and managing network access

Manage employee endpoints in real\-time via the **Connection Details** tab.


* **Real\-time monitoring**: Filter and search for Portal users to monitor their online status, access methods, and device types.

* **Emergency response**: If you detect abnormal activity or an employee resigns, click **Disable** to immediately terminate the session.
